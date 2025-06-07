---
icon: star
label: Gateways
order: 85
---

# Gateways
Gateways sit between on-device DoD agents and the immutable Knowledge Cache Graph (KCG). They validate, enrich and route knowledge while maintaining high-performance caches and semantic indexes.

## Core Responsibilities
- **Validation and packaging**  
  Gateways receive distilled knowledge from agents, run quorum-based fact-checking and write accepted entries to the KCG.
- **Index and retrieval services**  
  Each gateway hosts vector indexes and ontology graphs that link embeddings to KCG transaction IDs, enabling sub-second Selective Contextual Reasoning (SCR).
- **Cache management**  
  A multi-tier KV cache (hot, warm, cold) stores frequently requested reasoning blocks with 50-200 ms access latency.
- **Quality enforcement**  
  Spam filters, reputation scores and stake requirements protect the network from low-value or malicious content.

## Off-Chain Index Layer and Knowledge Mesh
- Gateways publish lightweight indexes that map entities and embeddings to on-chain data.
- Indexes can be shared in a federated mesh, giving redundancy and locality without hammering Arweave for every query.
- This layer keeps SCR fast even as the global KCG scales.

## Hybrid KV Cache and Orchestration
| Layer | Purpose | Typical TTL |
|-------|---------|-------------|
| Hot   | High-frequency facts and chains | Seconds to minutes |
| Warm  | Medium-use validated knowledge | Hours to days |
| Cold  | Archived or less relevant entries | Days to weeks |

Promotion and eviction follow an importance × frequency × freshness score. Gateways monitor hit rates and dynamically rebalance the tiers.

## Knowledge Gap Detection and Proactive Distillation
- Continuous analytics flag KV misses, query spikes and repeated Big-LLM calls.
- When a gap emerges, the gateway creates a **distillation task** that describes the missing knowledge, required confidence and bounty.
- Idle DoD agents compete to fill the gap. The first validated answer earns the reward and is cached for future use.

## Incentives and Governance
- Gateways earn tokens for validation work, cache hits and task orchestration.
- Misbehavior, such as approving spam, is penalized by stake slashing.
- A portion of every DoD fee funds gateway operations while another portion is burned to maintain deflationary tokenomics.
- Governance parameters (task fees, quorum size, cache limits) are set by on-chain voting.

## Security and Privacy
- All private data stays on the user’s device until a gateway receives only the distilled, context-safe portion required for validation.
- Gateways sign their outputs, providing provenance and auditability without exposing raw user data.
Gateways form the high-performance and trust-enforcing backbone of the Membria network, reducing latency and cost while preserving the quality and integrity of shared knowledge.

---

## The Gateway role in Knowledge Validation Process
The process of data validation within a gateway typically follows these automated steps upon receiving a request (and similarly, before sending a response if applicable):

1.  **Initial Connection & Parsing:** The gateway receives the request, parses basic protocol information (e.g., HTTP headers).
2.  **Security Checks:** Authentication (e.g., API keys, OAuth tokens) and authorization (access rights) are verified first.
3.  **Parameter Validation:** Path parameters, query parameters, and headers are validated against definitions (e.g., from an OpenAPI spec for an API gateway). This includes type, format, and presence checks.
4.  **Content-Type Validation:** The gateway checks if the `Content-Type` header (e.g., `application/json`, `application/xml`) is supported and matches the actual payload format.
5.  **Message Size Validation:** The size of the request/response body is checked against configured limits to prevent denial-of-service (DoS) attacks or resource exhaustion.
6.  **Syntactic Validation:** The payload is checked for well-formedness (e.g., valid JSON or XML structure).
7.  **Schema Compliance Validation:** The payload is validated against its defined schema (e.g., JSON Schema, XSD). This is often the most intensive data validation step, checking structure, data types, required fields, and constraints.
8.  **Specific Integrity & Custom Logic Checks:** Additional data integrity checks (e.g., checksums if provided) or custom business rule validations (if configured at the gateway level) are performed.
9.  **Logging:** The outcome of validation (success or failure, with error details if any) is logged.
10. **Action:**
    * **If Valid:** The request is forwarded to the appropriate backend service (or the response is sent to the client).
    * **If Invalid:** The gateway rejects the request with an appropriate error code (e.g., HTTP 400 Bad Request) and a descriptive error message. It does not forward the invalid data.

---

## Relationship between Gateway Validation and Consensus Mechanisms
The relationship between gateway validation and consensus mechanisms depends on the system architecture:
* **Centralized/Traditional Systems:** In systems without distributed consensus for data writes (e.g., a typical microservice architecture behind an API gateway), the gateway is a primary validator. There isn't a "consensus" step for the validation itself among multiple gateways in the same way as a blockchain. However, consistency is crucial:
    * **Consistent Policy Enforcement:** If multiple gateway instances exist (e.g., for load balancing or high availability), they must all apply the *same* validation rules. This is typically achieved through centralized configuration management and deployment.
    * **Consistent Logging:** Validation results from all instances should be logged to a central system for coherent monitoring and auditing.
    * **No Data Consensus at Gateway Level:** Gateways validate independently. If data passes validation at one gateway and is written to a backend system, that backend system (e.g., a database (DB)) handles its own data consistency, possibly using its own consensus or replication mechanisms if it's a distributed DB.

* **Distributed Ledger/Blockchain Systems:** Here, validation and consensus are tightly coupled.
    * Nodes in the network (which might include specialized gateway nodes) validate incoming transactions or data submissions against the ledger's rules (format, signatures, business logic).
    * A consensus mechanism (e.g., PoW, PoS) is then used by the network to agree on the order and validity of a *batch* of these validated transactions before they are immutably recorded on the ledger.
    * In this scenario, gateway validation is an initial step, and the consensus mechanism provides the final, distributed agreement on what validated data becomes part of the shared truth.

In essence, gateways always perform validation. How this validation relates to broader consensus depends on whether the underlying system architecture relies on a formal consensus protocol for data agreement and state changes. For most non-blockchain systems, gateway validation is a critical data quality and security measure, with "consistency" across multiple gateways being an operational goal rather than a protocol-driven consensus outcome for each data packet.

---

## Gateway Reasoning Orchestration & Knowledge Gap Detection

The Gateway is more than a passive storage and query endpoint - it actively orchestrates the quality and structure of the Knowledge Cache Graph (KCG). Its core responsibility is to detect reasoning gaps, manage KV-caching layers, and coordinate the creation of new knowledge via DoD agents.

### Detecting Knowledge Gaps and Hot Topics

Gateways continuously monitor query traffic and KV cache behavior to detect:

- Frequent KV misses: repeated user queries where no matching cached KV exists.
- Spikes in similar queries: indicating a trend or emerging interest (e.g. "fine-tuning LLaMA", "RAG vs CAG").
- Redundant calls to Big LLMs: same queries triggering repeated costly API calls - a sign of missing reusable reasoning.
- Stale or outdated KV blocks: old distillations no longer consistent with updated knowledge graphs or ontologies.

This results in the identification of Knowledge Hotspots or Reasoning Deficits.

---

## Discovery and Efficient Gateway Selection

In decentralized architectures like KnowledgeCache, it is inefficient for a DoD agent to blindly contact random Gateways, especially without knowing which ones are suitable for a given task. However, established decentralized discovery mechanisms can address this without requiring knowledge of each Gateway's cache contents.

### Discovery Mechanism Overview

While not explicitly described in the documentation, the system implies a discovery model based on the Peaq Protocol:

1. **Service Discovery via Peaq Protocol:**  
   Gateways register their presence and capabilities (e.g., location, load, specialization) in a decentralized service registry. DoD agents query this registry to discover available Gateways.

2. **Capability-based Selection:**  
   After retrieving available Gateway metadata, the DoD agent selects the most appropriate node using:
   - **Geographic Proximity** to minimize latency.
   - **Load and Availability**, choosing underutilized nodes.
   - **Reputation or Staking**, favoring trusted Gateways.
   - **Domain Specialization**, optionally preferring nodes tuned for specific topics.

3. **Routing Logic Inside Gateway:**  
   Once a Gateway is selected, the DoD agent sends the request. The Gateway:
   - First checks its **off-chain Gateway KV-cache**.
   - If no match, uses **semantic and vector indexes** to locate facts in the **on-chain KCG** (Arweave).
   - Applies **contextual reasoning** to construct a prompt using the retrieved knowledge.
   - Optionally falls back to a Big LLM if necessary.

4. **Distillation and Write-back:**  
   If new insights are distilled, the DoD agent sends back the result to the Gateway for validation and permanent write to the on-chain KCG.

### Caching Strategy and Priority Layers

Gateways are designed to optimize speed and cost:
- On-device Tiny LLM KV-cache: ~20 ms latency.
- Gateway shared KV-cache: 50–200 ms.
- Public KCG access (Arweave): 300–1000 ms (direct), faster via index.
- Big LLM fallback: 800–2000 ms.

This hierarchy ensures:
- Most lookups are handled locally or via Gateway caches.
- Gateway caches are dynamically updated using usage analytics (e.g., repeated misses, request spikes).
- High-demand knowledge is promoted to “hot” or “warm” tiers for optimal reuse.

### Accelerated KCG Access via Gateway Indexes

Gateways avoid querying Arweave directly for each lookup. Instead, they:
- Maintain **off-chain semantic graphs and vector indexes** pointing into the KCG.
- Leverage these for sub-second retrieval from large knowledge graphs.
- Operate a **Federated Knowledge Mesh**, replicating indices across multiple nodes to enhance locality and fault-tolerance.
- Use multi-layered hybrid caching: on-device, Gateway-level, and public (KCG).

This design provides a scalable and low-latency infrastructure for real-time, on-demand knowledge reasoning in a fully decentralized setting.

---

### KV Cache Orchestration

The Gateway maintains a multi-tiered cache structure:

- Hot Layer: High-frequency, high-importance KV blocks.
- Warm Layer: Medium-use, non-volatile knowledge.
- Cold Layer: Low-use, outdated, or weakly relevant KV blocks.

Each entry is annotated with:
- `importance_score`: provided by DoD agent or inferred via usage analytics.
- `last_accessed` timestamp.
- `source_confidence` and `validation_passed`.

Based on these signals, the Gateway:
- Ranks new KV entries using a hybrid scoring model (importance × frequency × freshness).
- Evicts or offloads stale entries to disk/off-chain cold storage.
- Recalls pages of KV blocks when relevant topics re-emerge (recency-based paging).
- Bundles KV-chains and reasoning paths for replay and reconstruction.

### Proactive Distillation Task Creation

When a pattern of deficiency is detected, the Gateway generates and queues distillation tasks:

```json
{
  "query": "how to train LLaMA on custom data",
  "pattern_id": "llama_ft_2024",
  "trigger": "miss_rate>80%",
  "task_type": "proactive_distillation",
  "bounty": 4,
  "requirements": {
    "agent_status": "idle",
    "gpu": true,
    "max_latency": "5s"
  }
}
```

These tasks are broadcast to DoD Agents that meet the resource and status conditions.

### Intelligent KV Layering and Feedback Loop

As agents submit new KV blocks and reasoning chains:
- Gateway scores and validates them.
- High-confidence blocks are pushed to the hot layer.
- Usage data is fed back to reinforce or decay importance scores.

This feedback loop ensures self-improvement of the reasoning layer over time - without requiring global retraining of any model.

### Outcome

- Better reuse of reasoning → lower Big LLM cost.
- Dynamic adaptation of the knowledge graph to user demand.
- Coordinated, decentralized creation of new verified knowledge via task-market economics.

---
