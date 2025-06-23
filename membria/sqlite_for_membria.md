---
icon: package
label: SQLite for Membria
order: 92
---

---

-----

# Hybrid Vector/Relational RAG/CAG DBMS for Edge Devices with Agent Memory

## 1\. Overview and Goals

For hybrid AI systems to operate effectively on peripheral (edge) devices, a compact, fast, and reliable solution is required for storing and processing complex data structures for AI agents. This includes:

1.  **RAG (Retrieval-Augmented Generation):** Unstructured "facts" for semantic search.
2.  **Knowledge Graph:** Structured entities and their relationships, defined by an ontology.
3.  **Agent Memory:** State, history, and internal "thought" processes for multiple, distinct AI agents.

The goal of this architecture is to unify all these data types into a **single, transactional, high-performance database** with minimal overhead.

## 2\. Technology Choice: SQLite with Extensions

**SQLite** is selected as the foundation due to its unique advantages for edge scenarios:

  * **Single File:** Simplifies deployment, backup, and synchronization.
  * **Serverless Operation:** Embeds directly into the application, saving system resources.
  * **Transactional (ACID):** Guarantees data integrity.
  * **Extensibility:** Supports powerful extensions for specific tasks like vector search and JSON processing.

We will use two key extensions:

  * **`sqlite-vss`**: For efficient vector search (RAG).
  * **`JSON1`**: For native handling of structured JSON data (properties, agent memory).

## 3\. Database Schema

The entire logic is implemented within a single file, `membria_edge.db`. The schema is designed to be comprehensive, supporting all required functionalities.

```sql
/*
 =================================================================
 CORE KNOWLEDGE TABLES (RAG & Knowledge Graph)
 =================================================================
*/

-- Stores the KNOW Ontology schema itself
CREATE TABLE ontology_schema (
    item_type TEXT NOT NULL, -- "NODE" or "EDGE"
    item_label TEXT NOT NULL PRIMARY KEY,
    description TEXT
);

-- Stores Nodes (entities) of the knowledge graph
CREATE TABLE knowledge_nodes (
    id TEXT PRIMARY KEY,
    node_type TEXT NOT NULL,
    properties JSON NOT NULL,
    FOREIGN KEY (node_type) REFERENCES ontology_schema(item_label)
);

-- Stores Edges (relationships) between nodes
CREATE TABLE knowledge_edges (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    source_node_id TEXT NOT NULL,
    target_node_id TEXT NOT NULL,
    label TEXT NOT NULL,
    properties JSON,
    FOREIGN KEY (source_node_id) REFERENCES knowledge_nodes(id),
    FOREIGN KEY (target_node_id) REFERENCES knowledge_nodes(id),
    FOREIGN KEY (label) REFERENCES ontology_schema(item_label)
);

-- Stores text chunks for RAG, linkable to the knowledge graph
CREATE TABLE chunks (
    id TEXT PRIMARY KEY,
    content TEXT NOT NULL,
    embedding BLOB NOT NULL,
    related_node_id TEXT, -- Optional: Foreign key to the knowledge_nodes table
    sync_status TEXT NOT NULL DEFAULT 'local', -- for cloud sync
    FOREIGN KEY (related_node_id) REFERENCES knowledge_nodes(id)
);

-- Virtual table for fast vector search
CREATE VIRTUAL TABLE vss_chunks USING vss0(embedding(1024));


/*
 =================================================================
 AGENT MEMORY TABLES
 =================================================================
*/

-- Defines the Agents themselves (Long-Term Memory)
CREATE TABLE agents (
    agent_id TEXT PRIMARY KEY,
    description TEXT,
    system_prompt TEXT NOT NULL,
    allowed_tools JSON,
    created_ts INTEGER NOT NULL
);

-- Groups messages into conversation sessions
CREATE TABLE agent_conversations (
    session_id TEXT PRIMARY KEY,
    agent_id TEXT NOT NULL,
    user_id TEXT NOT NULL,
    start_ts INTEGER NOT NULL,
    summary TEXT, -- Optional summary for long conversations
    FOREIGN KEY (agent_id) REFERENCES agents(id)
);

-- Stores turn-by-turn message history (Episodic Memory)
CREATE TABLE conversation_history (
    message_id INTEGER PRIMARY KEY AUTOINCREMENT,
    session_id TEXT NOT NULL,
    role TEXT NOT NULL, -- 'user', 'assistant', 'system', 'tool'
    content TEXT NOT NULL,
    metadata JSON,
    timestamp INTEGER NOT NULL,
    FOREIGN KEY (session_id) REFERENCES agent_conversations(session_id)
);

-- The Agent's "scratchpad" for reasoning (Working Memory)
CREATE TABLE agent_scratchpad (
    step_id INTEGER PRIMARY KEY AUTOINCREMENT,
    session_id TEXT NOT NULL,
    thought TEXT, -- The agent's reasoning process
    action JSON,  -- The tool call it decided to make
    observation TEXT, -- The result from the tool call
    timestamp INTEGER NOT NULL,
    FOREIGN KEY (session_id) REFERENCES agent_conversations(session_id)
);
```

## 4\. Implementing the Knowledge Graph & KNOW Ontology

The KNOW ontology provides the vocabulary and structure for the knowledge graph. The `ontology_schema` table stores the allowed node and edge types (e.g., 'Person', 'Equipment', 'MAINTAINS'), while the `knowledge_nodes` and `knowledge_edges` tables store the instance data conforming to this ontology. This enables powerful, structured queries about the relationships between entities.

## 5\. Implementing Agent Memory Architecture

To support sophisticated, stateful AI agents, the architecture defines three types of memory, each implemented with dedicated tables in the SQLite database.

### 5.1. The Three Types of Agent Memory

1.  **Long-Term Memory (`agents` table):** Stores the core identity of each agent—its purpose, instructions, personality, and permitted tools (e.g., the `system_prompt` defines "You are a helpful safety assistant...").
2.  **Episodic Memory (`agent_conversations`, `conversation_history` tables):** Records the complete, turn-by-turn history of interactions between a user and an agent, preserving the full context of each conversation.
3.  **Working Memory (`agent_scratchpad` table):** Provides a temporary "thought space" for an agent. Here, it can plan multi-step tasks, execute tools (like RAG or graph queries), and record the results (observations) before formulating a final response. This is critical for implementing advanced reasoning patterns like ReAct (Reason + Act).

### 5.2. The Agent Work Cycle

A typical agent interaction follows this stateful loop:

1.  **Initialization:** The application loads the agent's core instructions from the `agents` table based on the selected `agent_id`.
2.  **Conversation Start:** A new record is created in `agent_conversations` with a unique `session_id`.
3.  **User Interaction:** The user's message is saved to `conversation_history` with `role = 'user'`.
4.  **Reasoning Loop (The "Thinking" Process):**
      * **Thought:** The LLM analyzes the history and its goal, then generates a plan. This internal monologue is saved to the `thought` column in `agent_scratchpad`. (e.g., "User is asking about safety for valve VX-55. I need to query the knowledge graph for its location and then use RAG to find the relevant safety doc.").
      * **Action:** The LLM generates a structured `action` to execute a tool, e.g., `{"tool": "rag_search", "query": "safety procedure for VX-55"}`. This is also saved to the scratchpad.
      * **Observation:** The system executes the action, and the result (e.g., a text chunk from a manual) is saved to the `observation` column.
      * The loop repeats, feeding the history of thoughts, actions, and observations back into the LLM's context until it has enough information.
5.  **Final Response:** The agent generates the final answer for the user, which is saved to `conversation_history` with `role = 'assistant'`.

### 5.3. Example Query: Reconstructing Full Context

To reconstruct the full context for an agent during its reasoning loop, the application can run the following query:

```sql
-- Get all messages and scratchpad entries for a given session, ordered by time
SELECT
    'message' AS entry_type,
    role,
    content,
    timestamp
FROM conversation_history
WHERE session_id = 'session-123-abc'

UNION ALL

SELECT
    'scratchpad' AS entry_type,
    'assistant' AS role, -- The agent's own internal work
    'Thought: ' || thought || ' | Action: ' || action || ' | Observation: ' || observation AS content,
    timestamp
FROM agent_scratchpad
WHERE session_id = 'session-123-abc'

ORDER BY timestamp ASC;
```

## 6\. "Unlimited Context" Implementation

"Unlimited context" is achieved via a **hybrid memory management system**:

1.  **Active Memory:** The LLM's native context window (KV-cache), residing in shared system RAM and accelerated by the device's NPU.
2.  **Long-Term Memory:** The entire SQLite database, which acts as a vast, searchable knowledge repository.

The agent's reasoning process intelligently retrieves only the most relevant data from its Long-Term and Episodic Memory to construct a compact, effective prompt for its Active Memory.

## 7\. Architectural Advantages

  * **Unification:** A single, coherent system for RAG, Knowledge Graphs, and stateful Agent Memory.
  * **Stateful Autonomy:** Enables multiple, distinct agents to operate on a single device, each with its own memory and purpose.
  * **Traceability:** The `agent_scratchpad` table provides a full audit trail of the agent's "thought process," invaluable for debugging, analysis, and safety.
  * **Efficiency & Reliability:** Achieves high performance and ACID-guaranteed data integrity with minimal resource footprint, ideal for edge deployments.

-----

## Appendix A: Hardware Provider Overview (NVIDIA / AMD / Intel)

This section provides a brief overview of the three main semiconductor companies and their roles in an AI architecture like Membria.

  * **NVIDIA:** The leader in AI acceleration due to its powerful GPUs (e.g., RTX series for the edge, Blackwell for the cloud) and the mature CUDA software ecosystem. In this architecture, it powers cloud inference.
  * **AMD:** A leader in high-performance CPUs (e.g., Threadripper for cloud nodes) and a growing competitor in AI with its Instinct GPUs and Ryzen AI NPUs for edge devices.
  * **Intel:** A dominant player in client CPUs and a leader in edge AI with its Core Ultra processors featuring integrated NPUs, making them an ideal hardware base for the Membria edge device.

-----

## Appendix B: Comparison of Agent Memory Approaches

While the proposed unified SQLite architecture is optimized for this project's goals, other approaches exist for implementing agent memory.

| Criteria | Unified SQLite (Proposed) | AI Frameworks (LangChain/LlamaIndex) | Specialized Architectures (e.g., MemGPT) | Traditional DBMS Stack (e.g., Postgres+Redis) |
| :--- | :--- | :--- | :--- | :--- |
| **Deployment Model**| **Embedded.** Single file, no server process. Ideal for offline edge. | **Primarily Client-Server.** Can wrap local stores, but designed around service calls. Not ideal for offline-first. | **Embedded, but complex.** A self-contained architectural pattern. | **Client-Server.** Requires network connection to multiple database servers. Not for edge. |
| **Dependencies & Footprint** | **Minimal.** A single, lightweight library. | **High.** Brings in a large number of dependencies, potentially bloated for edge use. | **Very High.** Emulates OS-level memory management, resource-intensive. | **High.** Requires running and managing multiple, heavy server processes. |
| **Data Integrity (ACID)**| **Excellent.** Full ACID transactions ensure memory consistency. | **Dependent.** Integrity depends on the underlying database; not guaranteed at the framework level. | **Managed by framework.** | **High (Postgres),** but consistency between Redis and Postgres must be handled by the application. |
| **Flexibility & Control**| **Maximum.** Full control over schema, queries, and logic via standard SQL. | **Limited.** Abstractions can be restrictive and hard to customize or debug. | **Limited.** Imposes its specific hierarchical memory structure. | **Maximum.** |
| **Best for...** | **Reliable, production-grade edge applications** requiring efficiency and control. | **Rapid prototyping** and cloud-based agents where development speed is prioritized. | **Research** and agents needing to manage very long-running, evolving contexts. | **High-performance, scalable cloud applications** with a dedicated DevOps team. |

### Analysis

For the Membria EE use case, which demands **offline-first autonomy, resource efficiency, and transactional reliability**, the proposed unified SQLite architecture is superior. High-level frameworks like LangChain, while excellent for prototyping, introduce unnecessary overhead and dependencies for a production edge environment. The SQLite solution provides the required control, reliability, and performance with the lowest possible footprint.
