---
icon: workflow
label: Workwlow
order: 92
---
# Workflow Overview

The KCG+CAG system introduces an optimized workflow that allows Tiny LLMs to acquire, reason over, and integrate fresh knowledge without the need for retraining. The process leverages multi-layer caching, Selective Contextual Reasoning (SCR), and Distillation on Demand (DoD) to ensure knowledge freshness, verifiability, and efficiency.

## Full Knowledge Lifecycle Workflow

### 1. DoD Request Trigger
- A Tiny LLM or DoD Agent identifies a knowledge gap, outdated fact, or complex reasoning need.
- It initiates a **DoD query**, requesting knowledge retrieval, validation, or distillation.

### 2. SCR Reasoning Pipeline via Gateway
- The DoD Agent or Tiny LLM triggers the **Selective Contextual Reasoning (SCR)** pipeline via the Gateway:
  - **Semantic retrieval** from the KCG KV-layer and Gateway off-chain index.
  - **Filtering and confirmation step** performed locally by the agent or Tiny LLM.
  - **Contextual reasoning** using enriched prompt with retrieved knowledge.
- If sufficient reasoning is possible using the local or Gateway caches, the process completes without invoking Big LLMs.

### 3. Fallback to Big LLM (if necessary)
- For novel, ambiguous, or high-confidence-required queries, the DoD Agent escalates the request to selected Big LLM APIs (GPT, Claude, Gemini, etc.).
- Multiple models may be queried and compared.

### 4. Knowledge Distillation Proposal
- Based on SCR or Big LLM outputs, the DoD Agent synthesizes a **distilled knowledge proposal**.
- The proposal includes:
  - Summary.
  - Sources and evidence.
  - Semantic relations and context.
  - Optional embeddings for KV-caching.

### 5. Gateway Validation and Recording
- The proposal is submitted to the Gateway.
- The Gateway performs validation steps:
  - Verifies data integrity and formatting.
  - Checks evidence, references, and originality.
  - Optionally invokes Validator consensus for high-value knowledge.
- If validated, the Gateway records the entry into the KCG (Arweave).
- A corresponding **KV entry is updated in the public KCG KV-layer** for efficient future retrieval.

### 6. Confirmation and Reward Distribution
- The DoD Agent receives the finalized KCG TXID as confirmation.
- Validators and Gateways receive incentives for their role.
- A portion of tokens from the DoD query are burned to maintain deflationary tokenomics.

## Key Optimizations in the Workflow
- **SCR-first by default** reduces calls to Big LLM by up to 80%.
- **Multi-layer caching** ensures fastest possible retrieval for repeated or similar queries.
- **Federated Gateway layer** enables scaling and redundancy of knowledge retrieval and validation services.
- **Immutable KCG layer** ensures global, shared, and verifiable knowledge memory for all participants.

---
