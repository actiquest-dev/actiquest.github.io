---
icon: database
label: SQLite for Membria
order: 92
---

-----

# Hybrid Vector/Relational in-memory DBMS for RAG/CAG/Agents running on Edge Devices

## 1\. Overview and Goals

For hybrid AI systems to operate effectively on peripheral (edge) devices, a compact, fast, and reliable solution is required for storing and processing complex data structures for AI agents. This includes:

1.  **RAG (Retrieval-Augmented Generation):** Unstructured "facts" for semantic search.
2.  **Knowledge Graph:** Structured entities and their relationships, defined by an ontology and tracked over time.
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

-- Stores Edges (relationships) between nodes with temporal tracking
CREATE TABLE knowledge_edges (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    source_node_id TEXT NOT NULL,
    target_node_id TEXT NOT NULL,
    label TEXT NOT NULL,
    properties JSON,
    valid_from_ts INTEGER NOT NULL, -- Unix timestamp of when the relationship became valid
    valid_until_ts INTEGER,         -- Unix timestamp of when it ceased to be valid. NULL means it's current.
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

## 4\. Implementing the Knowledge Graph: Ontology & Temporality

### 4.1. The KNOW Ontology

The KNOW ontology provides the vocabulary and structure for the knowledge graph. The `ontology_schema` table stores the allowed node and edge types (e.g., 'Person', 'Equipment', 'MAINTAINS'), while the `knowledge_nodes` and `knowledge_edges` tables store the instance data conforming to this ontology.

### 4.2. Implementing a Temporal Graph

A key feature of advanced memory systems is temporality—the ability to understand how relationships change over time. This is achieved by adding `valid_from_ts` and `valid_until_ts` columns to the `knowledge_edges` table.

**How it works:** Instead of deleting or overwriting relationships, we preserve history. When a relationship changes:

1.  The old record is updated by setting `valid_until_ts` to the current timestamp, "closing" it.
2.  A new record is inserted with `valid_from_ts` as the current timestamp and `valid_until_ts` as `NULL`, indicating it's the new "current" state.

**Example: An employee promotion**

1.  **Initial State:** John Doe is a 'Technician'. An edge is created with `valid_from_ts` = (start\_date) and `valid_until_ts` = `NULL`.
2.  **State Change:** He is promoted to 'Senior Technician'.
3.  **Action:** The old edge is updated with `valid_until_ts` = (promotion\_date). A new edge is inserted with the 'Senior Technician' role, `valid_from_ts` = (promotion\_date), and `valid_until_ts` = `NULL`.

This allows for powerful historical queries.

**Example Temporal Query:** "What was John Doe's role on January 1st, 2024?"

```sql
SELECT target_node_id AS role_id
FROM knowledge_edges
WHERE
    source_node_id = 'person:john_doe'
    AND label = 'HAS_ROLE'
    AND 1704067200 BETWEEN valid_from_ts AND COALESCE(valid_until_ts, 9999999999);
```

The `COALESCE` function correctly handles currently valid relationships where `valid_until_ts` is `NULL`.

## 5\. Implementing Agent Memory Architecture

To support sophisticated, stateful AI agents, the architecture defines three types of memory:

1.  **Long-Term Memory (`agents` table):** Stores the core identity of each agent—its purpose, instructions, and permitted tools.
2.  **Episodic Memory (`agent_conversations`, `conversation_history` tables):** Records the complete history of interactions.
3.  **Working Memory (`agent_scratchpad` table):** Provides a "thought space" for an agent to plan multi-step tasks, execute tools, and record observations before formulating a final response.

## 6\. Functional Workflows

The agent is the primary driver of all other workflows. A typical interaction follows a "Reason-Act" loop where the agent uses its Working Memory (`agent_scratchpad`) to plan steps, and then executes actions by triggering RAG, CAG, or temporal Graph workflows to gather information before generating a final response.

## 7\. "Unlimited Context" Implementation

"Unlimited context" is achieved via a **hybrid memory management system**:

1.  **Active Memory:** The LLM's native context window (KV-cache), residing in shared system RAM and accelerated by the device's NPU.
2.  **Long-Term Memory:** The entire SQLite database, which acts as a vast, searchable, and time-aware knowledge repository on disk.

## 8\. Architectural Advantages

  * **Unification:** A single, coherent system for RAG, temporal Knowledge Graphs, and stateful Agent Memory.
  * **Stateful Autonomy & Historicity:** Enables multiple agents to operate with full conversational history and understand how knowledge changes over time.
  * **Traceability:** The `agent_scratchpad` provides a full audit trail of the agent's "thought process".
  * **Efficiency & Reliability:** Achieves high performance and ACID-guaranteed data integrity with minimal resource footprint.

-----

## Appendix A: Hardware Provider Overview (NVIDIA / AMD / Intel)

  * **NVIDIA:** Leader in AI acceleration with its GPUs (e.g., RTX series) and the mature CUDA software ecosystem. Powers cloud inference in the Membria architecture.
  * **AMD:** Leader in high-performance CPUs (e.g., Threadripper) and a growing competitor in AI with its Instinct GPUs and Ryzen AI NPUs for edge devices.
  * **Intel:** Leader in client CPUs and edge AI with its Core Ultra processors featuring integrated NPUs, making them an ideal hardware base for the Membria edge device.

-----

## Appendix B: Comparison of Agent Memory Approaches

| Criteria | Unified SQLite (Proposed) | AI Frameworks (LangChain) | Specialized Memory Stores (Mem0, Zep) |
| :--- | :--- | :--- | :--- |
| **Deployment Model**| **Embedded.** Ideal for offline edge. | **Primarily Client-Server.** Not ideal for offline-first. | **Client-Server.** Deployed as separate services. Not for offline edge. |
| **Dependencies & Footprint** | **Minimal.** A single, lightweight library. | **High.** Potentially bloated for edge use. | **High.** Requires running and managing separate, often containerized, services. |
| **Key Feature** | **Unification & Reliability.** RAG, Graph, and Agent Memory in one ACID-compliant store. | **Rapid Prototyping.** High-level abstractions for quick development. | **Managed Memory.** Provides ready-to-use APIs for semantic and temporal memory search. |
| **Data Integrity (ACID)**| **Excellent.** Full ACID transactions ensure memory consistency. | **Dependent.** Depends on the underlying database; not guaranteed at the framework level. | **Managed by the service.** Typically high. |
| **Flexibility & Control**| **Maximum.** Full control over schema and logic via standard SQL. | **Limited.** Abstractions can be restrictive and hard to customize. | **Limited.** Restricted to the capabilities of their API. |
| **Best for...** | **Reliable, production-grade edge applications** requiring efficiency and control. | **Rapid prototyping** and cloud-based agents where development speed is prioritized. | **Cloud-native applications** that need a managed, off-the-shelf memory solution. |

### Analysis

For the Membria EE use case, which demands **offline-first autonomy, resource efficiency, and transactional reliability**, the proposed unified SQLite architecture is superior. High-level frameworks and managed memory services, while powerful in the cloud, introduce dependencies and a client-server model that are unsuitable for a disconnected edge environment. The SQLite solution provides the required control, reliability, and performance with the lowest possible footprint.
