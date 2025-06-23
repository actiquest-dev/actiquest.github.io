---
icon: database
label: SQLite for Membria
order: 89
---

-----

# **Architecture: A Unified RAG/CAG DBMS for Edge Devices**

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
    related_node_id TEXT,
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

The KNOW ontology provides the vocabulary and structure for the knowledge graph, ensuring data is consistent and semantically rich. The `ontology_schema` table stores the allowed node and edge types (e.g., 'Person', 'Equipment', 'MAINTAINS'), while the `knowledge_nodes` and `knowledge_edges` tables store the instance data conforming to this ontology. This enables powerful, structured queries about the relationships between entities.

## 5\. Implementing Agent Memory Architecture

To support sophisticated, stateful AI agents, the architecture defines three types of memory, implemented in the corresponding SQLite tables.

1.  **Long-Term Memory (`agents` table):** Stores the core identity of each agent—its purpose, instructions, and permitted tools (e.g., `system_prompt` for "You are a helpful safety assistant...").
2.  **Episodic Memory (`agent_conversations`, `conversation_history` tables):** Records the complete history of interactions between a user and an agent, preserving the context of each conversation.
3.  **Working Memory (`agent_scratchpad` table):** Provides a temporary "thought space" for an agent. Here, it can plan multi-step tasks, execute tools, and record the results (observations) before formulating a final response. This is critical for implementing reasoning patterns like ReAct (Reason + Act).

## 6\. Functional Workflows

### 6.1 Agent-driven Workflow

The agent is the primary driver of all other workflows. A typical interaction follows this loop:

1.  **Initialization:** The agent's identity is loaded from the `agents` table.
2.  **User Input:** A user message is logged in `conversation_history`.
3.  **Reasoning Loop (Scratchpad):**
      * The agent assesses the user's request and its conversation history.
      * It formulates a **Thought** (e.g., "I need to find the maintenance procedure for this valve").
      * It selects an **Action** (e.g., `{"tool": "graph_query", "query": "..."}`).
      * The system executes the action (by calling one of the workflows below).
      * The result is saved as an **Observation**.
      * This loop continues until the agent has sufficient information.
4.  **Final Response:** The agent generates a final answer, which is logged to `conversation_history`.

### 6.2 Supporting Workflows (Triggered by Agents)

  * **RAG Workflow:** An agent's action can trigger a vector search against the `vss_chunks` table to find relevant text passages.
  * **Graph Workflow:** An agent's action can trigger a structured SQL query against the `knowledge_nodes` and `knowledge_edges` tables to find entities and relationships.
  * **CAG Workflow:** The system can cache final agent responses in a `chains_of_thought`-like table to quickly answer repeated queries.

## 7\. "Unlimited Context" Implementation

"Unlimited context" is achieved via a **hybrid memory management system**:

1.  **Active Memory:** The LLM's native context window (KV-cache), residing in shared system RAM and accelerated by the device's NPU.
2.  **Long-Term Memory:** The entire SQLite database, which acts as a vast, searchable knowledge repository on disk.

The agent's reasoning process intelligently retrieves only the most relevant data from Long-Term Memory (via RAG and graph queries) to construct a compact, effective prompt for its Active Memory.

## 8\. Architectural Advantages

  * **Unification:** A single, coherent system for RAG, Knowledge Graphs, and stateful Agent Memory.
  * **Stateful Autonomy:** Enables multiple, distinct agents to operate on a single device, each with its own memory and purpose.
  * **Traceability:** The `agent_scratchpad` table provides a full audit trail of the agent's "thought process," which is invaluable for debugging and analysis.
  * **Efficiency & Reliability:** Achieves high performance and ACID-guaranteed data integrity with minimal resource footprint, ideal for edge deployments.
  * **Flexibility:** The combination of SQL, vector search, and JSON support provides a powerful and adaptable foundation for building sophisticated AI applications.
