---
icon: stack
label: Ecosystem Roles
order: 92
---
# Roles and Responsibilities

The KCG+CAG ecosystem is supported by distinct roles, each playing a critical part in ensuring the quality, efficiency, and scalability of the knowledge reasoning pipeline.

## DoD Agents
- **Role**: Orchestrators of Distillation on Demand (DoD) queries and reasoning pipelines.
- **Responsibilities**:
  - Identify knowledge gaps or outdated information.
  - Initiate SCR reasoning pipelines.
  - Aggregate outputs from SCR, local caches, and Big LLM APIs.
  - Propose distilled knowledge entries for validation.
  - Use and maintain local KV-caches for fast reasoning.
- **Incentives**:
  - Earn rewards for initiating valuable DoD queries.
  - Benefit from lower inference costs via SCR and caching.

## Gateways
- **Role**: Federated nodes serving as intermediaries between agents and the KCG.
- **Responsibilities**:
  - Validate, package, and record knowledge into KCG.
  - Manage off-chain semantic indexes and vector stores.
  - Operate KV-caching services for Tiny LLMs and agents.
  - Enforce quality and anti-spam measures.
  - Distribute SCR-ready prompts and knowledge to agents.
- **Incentives**:
  - Earn transaction fees and validation rewards.
  - Maintain economic sustainability by hosting caching and reasoning infrastructure.

## Validator Nodes
- **Role**: Guardians of knowledge correctness and consensus.
- **Responsibilities**:
  - Participate in voting and validation of proposed knowledge entries.
  - Ensure factual correctness, source verification, and semantic consistency.
  - Provide audit trails and proof-of-knowledge attestations.
  - Optionally participate in dispute resolution and governance processes.
- **Incentives**:
  - Earn validation rewards from token flows.
  - Receive staking benefits and governance rights.

## Off-Chain Indexing Nodes (Optional Layer)
- **Role**: Specialized nodes supporting Gateways.
- **Responsibilities**:
  - Maintain lightweight off-chain semantic graphs and vector indexes.
  - Serve SCR pipelines with ultra-fast retrieval.
  - Optimize query routing and ranking.
- **Incentives**:
  - Earn rewards from Gateway operators or network treasury.

---
