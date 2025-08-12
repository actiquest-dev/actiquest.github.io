---
icon: devices
label: KCG Architecture
order: 144
---


# **Membria: A Decentralized Knowledge Architecture**

-----

### **Abstract**

This document provides a detailed architectural specification for the integration of the Arweave network within the Membria Knowledge Cache Graph (KCG). Membria employs a **hybrid blockchain architecture**, separating the logical, transactional operations of the graph from the permanent storage of its data payloads. This brief clarifies the specific role of Arweave as the immutable data archive, details the structure and format of the data stored, and provides an in-depth, step-by-step protocol for both writing data to and reading data from the Arweave permaweb. It's intended for architects, developers, and stakeholders seeking to understand the foundational layer of trust and permanence within the Membria ecosystem.

We introduce the **Decentralized Knowledge Graph (DKG)**—a verifiable and efficient system for the continuous learning and reasoning enhancement of on-device, lightweight large language models (Tiny LLMs). Instead of costly retraining, Membria utilizes **Distillation on Demand (DoD)**, a process where knowledge from large "teacher" LLMs is re-checked, validated, and recorded as immutable events in a public graph. This approach allows Tiny LLMs to dynamically retrieve and leverage high-quality, verified knowledge through fast **Cache-Augmented Generation (CAG)** pipelines, drastically reducing latency, cost, and dependence on centralized APIs.

-----

## **1. Core Architecture: A Symbiotic Hybrid Model**

Membria's architecture is not a single blockchain but a symbiotic system that leverages the distinct strengths of two specialized networks: the Peaq Protocol for high-speed logic and Arweave for permanent data storage.

### **The Peaq Protocol: The Logic/Graph Layer**

The **Peaq Protocol** serves as the brain of the system. It manages the graph's structure, rules, and transactional state. All logical operations—such as proposing knowledge, casting consensus votes, and defining data models—occur as lightweight transactions on the Peaq chain. Its core is a **Temporal Semantic Graph**, implemented as a Directed Acyclic Graph (DAG) where every node is an **event**. An event is an atomic, immutable, and cryptographically signed record of a specific fact or action. Each event contains standardized fields, including `actor` (who created it), `timestamp` (when), and `cause` (linking it to preceding events), providing a complete and auditable history.

### **The Arweave Permaweb: The Memory Layer**

**Arweave** serves as the permanent, immutable memory for the DKG. While Peaq manages the "who, what, when, and why" of a knowledge event, Arweave stores the "heavy" data payload itself—the full text of a validated answer, for example. By offloading storage to Arweave, the Peaq chain remains fast and cost-effective, focusing solely on validating and ordering the logical event graph.

-----

## **2. The Decentralized Knowledge Graph (DKG): Layers & Components**

The DKG is a living, self-organizing system composed of two primary layers: a flexible ontological foundation and a dynamic knowledge layer.

### **The Ontology Layer: A Flexible System of Dictionaries**

Membria rejects a rigid, universal ontology in favor of a flexible and modular approach. This allows for the creation of custom ontologies tailored to specific users or domains—a concept referred to as *"онтология под заказчика"* or a "custom ontology for the client."

  * **Dictionaries as Building Blocks**: The foundation of the ontology is **"dictionaries"**—reusable, named collections of concepts and relationships for a specific domain. Users can leverage public, standardized dictionaries (e.g., based on **Schema.org**) for broad interoperability or create their own private, specialized dictionaries for unique business needs.
  * **Marketplace of Dictionaries**: The Membria ecosystem will feature a catalog or marketplace for dictionaries and semantic models. This encourages the reuse of high-quality ontologies and enhances interoperability across the network.
  * **On-Chain Definition on Peaq**: The ontology and its dictionaries exist as **genesis events** on the Peaq blockchain, making them a fundamental and verifiable part of the graph's structure.

### **The Knowledge Layer: Validated Answers as Event Chains**

This is the dynamic layer where verified facts from teacher LLMs are recorded and interlinked.

  * **Executable Semantic Models**: Every type of knowledge (e.g., a "Verified Answer") is governed by an **Executable Semantic Model** recorded on Peaq. Written in a declarative language like BSL, these models act as verifiable "knowledge contracts." They define the data structure and the validation rules (`Restrictions`) that all new knowledge events must adhere to, ensuring deterministic and transparent logic execution.
  * **Reasoning Chains as Events**: A verified answer from a teacher LLM is stored in the graph as a chain of events, cryptographically linked by the `cause` field. This provides a complete, auditable history for any fact, from the initial query to the final validation status.

-----

## **3. The Lifecycle of Knowledge: A Step-by-Step Protocol**


The process of transforming a raw answer from a teacher LLM into a trusted DKG entry follows a precise, four-step lifecycle across both the Peaq and Arweave blockchains.

### **Step 1: Define the "Knowledge Contract" on Peaq**

  * **Action**: Community experts define and deploy an Executable Semantic Model on the Peaq network. This model acts as a verifiable template for a "validated knowledge entry."
  * **Protocol**: An expert sends a transaction to Peaq containing a **genesis event** with the BSL code of the model as its payload. Once finalized, the model becomes an immutable part of the on-chain ontology. Arweave is not used in this step.

### **Step 2: Propose New Knowledge via Arweave and Peaq**

This two-part step involves storing the data payload permanently and then creating a lightweight pointer to it on the logic chain.

#### **2.1: The Arweave Write Protocol**

This is the protocol for how a DoD Agent securely writes a knowledge payload to Arweave.

1.  **Trigger**: Initiated by a DoD Agent after a teacher LLM generates a response, but **before** a proposal event is created on Peaq.
2.  **Data Preparation**: The agent assembles the knowledge payload into a **JSON-LD (JSON for Linked Data)** object. This ensures the data is machine-readable and semantically interoperable.
3.  **Transaction Formation & Tagging**: The agent prepares an Arweave transaction. The JSON-LD object is the transaction's data. A set of descriptive **Tags** is added, which are critical for efficient querying without needing to download the data itself.

| Tag Name | Example Value | Purpose |
| :--- | :--- | :--- |
| `Content-Type` | `application/ld+json` | Informs clients how to interpret the data. |
| `App-Name` | `Membria-DKG` | Identifies the transaction as part of the Membria ecosystem. |
| `App-Version` | `3.0` | Versions the protocol for future upgrades. |
| `Event-Type` | `ProposedAnswer` | Specifies the type of knowledge event. |
| `Query-ID` | `{query_hash_on_peaq}` | Links this data back to the originating query on Peaq. |

4.  **Signing and Broadcasting**: The agent signs the transaction and broadcasts it to the Arweave network. For efficiency, multiple small entries can be packaged into a single base transaction via a **bundling service**, significantly reducing cost and time.
5.  **Confirmation and ID Retrieval**: The Arweave network returns a permanent, unique **Arweave Transaction ID (ArTxID)**. This 43-character string is the immutable address of the knowledge payload.

#### **Payload Example: Arweave JSON-LD Object**

The following is a detailed example of the JSON-LD object stored on Arweave, representing a proposed answer.

```json
{
  "@context": "https://schema.org",
  "@type": "Answer",
  "identifier": "proposed_answer_uuid_xyz123",
  "encodingFormat": "application/ld+json",
  "inResponseTo": {
    "@type": "Question",
    "identifier": "{query_event_hash_on_peaq}"
  },
  "author": {
    "@type": "AIApplication",
    "name": "GPT-4-Turbo",
    "version": "2024-04-09"
  },
  "dateCreated": "2025-08-12T12:50:20Z",
  "text": "The Membria architecture separates logic and data. The Peaq Protocol manages the graph's transactional logic and structure as a Temporal Semantic Graph of events, while Arweave provides permanent, immutable storage for the actual data payloads.",
  "keywords": ["Membria", "Architecture", "Peaq", "Arweave", "Hybrid Blockchain"]
}
```

## **The Adjusted Concept: The Lifecycle of Knowledge as Intent Fulfillment**

The entire process, from a query to the retrieval of verified knowledge, is treated within the Membria architecture as the fulfillment of a primary system **Intent**: the **"Knowledge Distillation Request."** This is a formalized goal, initiated by a user or a Tiny LLM, that triggers a well-defined sequence of events to achieve its objective. Each step of the protocol is a phase in this Intent's lifecycle.

### **The Four Phases of Intent Fulfillment**

* **Step 1: Defining the "Knowledge Contract"**
    * **Role in the Intent: Definition.** This phase establishes the rules and the "schema" for the successful fulfillment of all future Intents of this type.

* **Step 2: Proposing New Knowledge**
    * **Role in the Intent: Execution.** A DoD agent, acting to fulfill the Intent, obtains data from a "teacher" LLM, stores it on Arweave, and creates a proposal event on Peaq.

* **Step 3: Gateway Consensus**
    * **Role in the Intent: Verification.** A quorum of independent gateway agents verifies that the Intent was executed correctly and that the results comply with the predefined rules (the contract).

* **Step 4: Finalizing the Result**
    * **Role in the Intent: Completion.** A final `validation_event` is created, which officially closes the Intent by recording its outcome (success or failure) in the graph.

---

### **Advantages of This Approach**

* **Precision**: This uses the key terminology of SpiralOS ("Intent") but applies it specifically to the core process that Membria implements.
* **Coherence**: It creates a stronger, more unified narrative. The entire complex protocol now has a clear purpose: to fulfill one specific "Intent."
* **Scalability**: This approach allows for the future addition of other "Intent" types (e.g., "Request to generate a report" or "Initiate a voting process"), which would logically fit into the same architecture.


---


### **The Peaq Proposal Protocol**

**Trigger:** This protocol is initiated immediately after a DoD Agent successfully writes a data payload to the Arweave network and retrieves the unique Arweave Transaction ID (ArTxID).

**Protocol:** The DoD Agent creates and broadcasts a lightweight transaction to the Peaq network. [cite_start]This transaction creates a **domain event** (`предметное событие`) that formally logs the new knowledge proposal on the logic layer[cite: 242].

The payload of this domain event is minimal but crucial, containing two key elements:

* **Data Pointer**: A direct reference to the full data payload stored on Arweave, in the format of `data_pointer: "{ArTxID}"`. This creates the essential link between the logic layer (Peaq) and the permanent storage layer (Arweave).
* **A graph edge** is created in the event's `cause` field, which contains the identifier of the original query event[cite: 72, 227]. [cite_start]This cryptographically links the new proposal to the action that prompted it, maintaining the auditable history of the Temporal Semantic Graph

**Purpose:** The successful execution of this protocol places the proposed knowledge into the DKG's logical graph. It makes the proposal discoverable by the network's Gateways and formally enters it into the next phase of the lifecycle: Gateway Consensus.

  * **Action**: The DoD Agent creates a lightweight transaction on the Peaq network to officially log the proposal.
  * **Protocol**: The transaction contains a **domain event** (`proposed_answer_event`). Its payload includes a pointer to the data (`data_pointer: "{ArTxID}"`) and a graph edge in the `cause` field linking it to the original query event.

### **Step 1: Gateway Consensus on Peaq**

  * **Action**: A quorum of Gateways reviews the proposal. They use the `ArTxID` pointer to fetch the full data from Arweave and perform a detailed validation against the rules in the Knowledge Contract.
  * **Protocol**: Gateways cast their votes (`attestation_event`) as transactions on the Peaq network. To optimize costs, these individual vote transactions can be **batched** into a single transaction before being submitted.

### **Step 2: Finalize the Result on Peaq**

  * **Action**: The outcome of the consensus vote is recorded immutably on Peaq, completing the knowledge lifecycle.
  * **Protocol**: A final `validation_event` is created on Peaq. Its payload contains the final status (e.g., `Status: Verified`, `ConfidenceScore: 0.98`). Its `cause` field points to the `proposed_answer_event`, creating the final, definitive edge in the knowledge subgraph.

---

## **4.Cost Optimization: Transaction Batching on Peaq**

[cite_start]The Membria architecture, inspired by the principles of SpiralOS, incorporates transaction batching as a core feature to optimize network traffic and reduce operational costs on the Peaq network[cite: 134].

### **How It Works**

Instead of each Gateway submitting its consensus vote (`attestation_event`) during Phase 3 of the Intent lifecycle as a separate transaction, a designated coordinator node can gather multiple votes into a single "batch." This approach is particularly effective for high-frequency, repetitive operations that are part of a single logical process.

### **The Protocol**

The batching protocol is straightforward:

1.  **Vote Submission**: Individual Gateways in the consensus quorum sign their votes and send them to a designated coordinator node.
2.  **Aggregation**: The coordinator waits to receive multiple votes and aggregates these signed events into a single array or list.
3.  **Batch Transaction**: This single array of events is then submitted as the payload of a single transaction to the Peaq network.

### **The Advantage**

This method drastically reduces transaction costs. [cite_start]The base network fee is paid once for the entire batch rather than for each individual micro-transaction[cite: 134]. For processes like consensus voting, where many small, similar events are generated in a short period, batching provides a significant efficiency gain and makes the system more economical to operate.

-----

## **5. Gateway Functionality: Reading and Managing Knowledge**

Gateways are intelligent nodes that serve as the primary interface to the DKG for on-device agents.

### **The Read Protocol: An Intelligent Query Processor**

Gateways use a multi-layered strategy to find information, prioritizing speed and cost-efficiency. They **do not** blindly search the entire Arweave network.

1.  **Check "Hot" Cache (50-200 ms)**: The Gateway first searches its own high-speed, off-chain KV-cache for a direct hit.
2.  **Search Off-Chain Indexes**: If there's no cache hit, the Gateway consults its local semantic and vector indexes. These indexes act as a "map" of the entire DKG, allowing it to quickly locate relevant event hashes on Peaq.
3.  **Retrieve Data from Arweave (300-1000 ms)**: Only after the indexes have identified a relevant event on Peaq does the Gateway read its `data_pointer`. It then makes a targeted HTTP GET request to an Arweave gateway using the specific `ArTxID` to retrieve the "heavy" data payload.
4.  **Assemble Context (SCR)**: The Gateway aggregates the retrieved data into an enriched prompt for the Tiny LLM using the **Selective Contextual Reasoning (SCR)** pipeline.
5.  **Fallback to DoD**: If a high-confidence answer cannot be constructed from the DKG, the request is escalated to external "teacher" LLMs, triggering a new knowledge lifecycle.

### **Versioning and Updates**

Knowledge stored on Arweave is **permanent and cannot be overwritten**. To update an entry, a new version of the JSON-LD object is uploaded to Arweave, receiving a **new ArTxID**. The logical graph on Peaq is then updated with a new event that supersedes the old one, and the mutable Gateway indexes are updated to point to the new ArTxID as the canonical version. All previous versions remain accessible on Arweave, providing a complete and verifiable audit trail.

-----

## **5. Trust, Validation, and Privacy**

The integrity of the DKG is secured by a multi-faceted trust model executed on the Peaq Protocol.

  * **Hybrid Consensus Mechanism**: Consensus among Gateways occurs exclusively on the Peaq blockchain. The network combines **Proof-of-Stake (PoS)** for validator security with **Byzantine Fault-Tolerant (BFT)** algorithms for rapid transaction finality.
  * **Dispute Resolution Protocol**: An economically-incentivized challenge system allows any stakeholder to challenge a verified fact. The outcome is determined by a stake-weighted re-vote among validators, with **slashing** penalties for those who approved incorrect information or made a frivolous challenge.
  * **Privacy with Zero-Knowledge Proofs**: The system integrates **Zero-Knowledge Proofs** via the **Peaq ZK Layer**. This enables confidential operations, such as a Gateway proving it has checked a fact against a private database without revealing the database, or a user proving they have the right to access knowledge without revealing their identity.

-----

## **6. Advanced On-Device Agent Capabilities**

Membria's architecture is designed to directly enhance the performance of on-device Tiny LLMs.

  * **Context and Memory Management**: Membria uses a **Segmented KV Buffer** for context window optimization and a hybrid **Persistent Memory** system (Local RAG Store + Disk-Based KV Archive) to prevent model "amnesia" between sessions.
  * **Synergy with Periodic LoRA Adaptation**: An automated offline pipeline uses knowledge accumulated in the DKG to periodically fine-tune the base Tiny LLM using **QLoRA**. This enhances the model's foundational understanding and embeds frequently used knowledge patterns directly into the model, often with minimal or no increase in its final size on the device.

-----

## **7. Conclusion: The Symbiotic Relationship**

Arweave provides the indispensable foundation of **trust, permanence, and verifiability** for the Membria DKG. By serving as the immutable archive for all knowledge payloads, it allows the Peaq Protocol to operate as a fast, flexible, and efficient logic layer. This symbiotic relationship enables Membria to create a knowledge graph that is both dynamic and eternally auditable, solving the core problem of creating a lasting, shared memory for decentralized AI.
