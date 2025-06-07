---
icon: hash
label: Graph Data Model
order: 90
---


# Knowledge Cache Graph (KCG) Data Model & Indexing

The Knowledge Cache Graph (KCG) serves as the immutable, decentralized knowledge memory layer for the ecosystem. It is optimized to store, retrieve, and reason over distilled knowledge efficiently, while ensuring verifiability and traceability.

## KCG Data Types

### Distilled Knowledge Entries
- Core units of validated knowledge.
- Contain:
  - Distilled summaries.
  - Supporting evidence and sources.
  - Metadata (creation date, proposer, validator signatures).
  - Optional embeddings for KV-layer indexing.

### Entities
- Discrete concepts, objects, or named entities.
- Serve as graph nodes for semantic linking.
- Example: `"Sparse Transformer"`, `"Switch Transformer"`.

### Relations
- Semantic links between entities and knowledge entries.
- Types:
  - `isA`
  - `relatedTo`
  - `usedBy`
- Include descriptions, confidence scores, and provenance data.

### Reasoning Chains
- Multi-step logical explanations or derivations.
- Stored as ordered steps with supporting evidence.
- Enable Tiny LLMs to shortcut complex reasoning by using pre-validated chains.

### FAQ Patterns
- Standardized question-answer pairs.
- Cover frequent queries and enable ultra-fast retrieval for common reasoning needs.

## Data Format
- All data is stored as **JSON-LD** following linked data principles.
- Ensures compatibility with semantic web standards and decentralized querying.

## Indexing Strategies

### KV-Cache Layer
- Distilled entries and reasoning chains are indexed by:
  - Query embeddings.
  - Canonical questions.
  - Topics and categories.
- This layer supports ultra-fast retrieval by agents and Tiny LLMs.

### Semantic Graph Indexes
- Gateways and off-chain nodes maintain semantic graphs of relations and entities.
- These indexes support complex reasoning paths and chaining queries.

### Proof-of-Knowledge and Metadata
- Each entry contains:
  - TXID from Arweave (content-addressed, immutable).
  - Validator signatures and consensus proofs.
  - Timestamps and provenance records.

## Key Benefits
- **Efficient retrieval** for Tiny LLMs without requiring expensive Big LLM inference.
- **Verifiability and immutability** via Arweave/IPFS storage.
- **Semantic reasoning-ready** via graph relations and reasoning chains.
- **Optimized for caching and reuse** via KV-layer and embeddings.
