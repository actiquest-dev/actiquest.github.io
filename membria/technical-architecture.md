---
icon: organization
label: Architecture
order: 94
---
# Technical Architecture Overview

The KCG+CAG ecosystem is composed of several interconnected layers and actors, forming a decentralized, efficient, and verifiable knowledge reasoning pipeline optimized for Tiny LLMs.

## Components Overview

### Knowledge Cache Graph (KCG)
- **Immutable Knowledge Layer**: Stored on Arweave.
- **Stores**:
  - Distilled knowledge entries (facts, QA pairs, reasoning chains).
  - Semantic relations and ontologies.
  - KV-cache entries for fast retrieval (keyed by embeddings, queries, or topics).
  - Proof-of-knowledge and validator signatures.
- **Public and verifiable**: Accessible by any Gateway, agent, or user.

### Cache-Augmented Generation (CAG) Layer
- **Reasoning Layer** on top of KCG and KV-caches.
- **Enables Tiny LLMs to perform fast retrieval and reasoning over verified knowledge without retraining**.
- Utilizes **Selective Contextual Reasoning (SCR)** pipelines:
  - Semantic retrieval.
  - Filtering and confirmation.
  - Context-enriched generation.

### Distillation on Demand (DoD) Agents
- Specialized agents or Tiny LLMs acting as initiators of DoD queries.
- Responsible for detecting outdated knowledge, gaps, or novel queries.
- Orchestrate SCR reasoning pipelines.
- Propose distilled knowledge entries to Gateways for validation.

### Gateways
- Federated nodes acting as intermediaries between DoD agents and KCG.
- Responsible for:
  - Knowledge validation and packaging.
  - Recording entries into KCG.
  - Managing off-chain semantic indexes and vector stores for ultra-fast retrieval.
  - Serving enriched knowledge and SCR-ready prompts to Tiny LLMs and agents.
- Gateways control write-access to KCG and enforce quality standards.

### Validator Nodes
- Participate in consensus voting, knowledge verification, and proof-of-knowledge processes.
- Ensure correctness, prevent spam, and provide auditability.
- Optionally contribute to off-chain indexing or SCR pre-computation services.

### Hybrid KV-Cache Architecture
- **On-device Tiny LLM KV-cache**: Fast, personalized cache of frequently used knowledge.
- **Gateway KV-cache**: High-performance, shared caching of validated knowledge and reasoning shortcuts.
- **Public KV-layer in KCG**: Immutable, community-validated cache ensuring knowledge persistence and transparency.

---

This modular, multi-layered architecture ensures:
- **Tiny LLMs can reason, learn, and update dynamically without retraining.**
- **Gateways and validators enforce knowledge quality and validation.**
- **Caching at multiple layers reduces inference costs, latency, and dependence on Big LLMs.**

---
