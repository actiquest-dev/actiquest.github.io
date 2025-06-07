---
icon: star
label: Alternative Methods
order: 88
---

# Advanced Caching Strategies & SCR Pipeline
---
To maximize reasoning efficiency, minimize inference costs, and enable dynamic knowledge integration for Tiny LLMs, the KCG+CAG architecture incorporates advanced caching strategies enhanced by **Selective Contextual Reasoning (SCR)** pipelines.

## Selective Contextual Reasoning (SCR)
Inspired by state-of-the-art research (arXiv:2503.05212), SCR enables Tiny LLMs to perform **lightweight, dynamic reasoning over external knowledge caches without modifying model weights**.
- **Step 1: Semantic Retrieval** - Retrieve relevant knowledge entries from the KV-cache and semantic graph indexes.
- **Step 2: Confirmation and Filtering** - Tiny LLMs or Gateways filter, confirm, and deduplicate retrieved entries, ensuring contextual fit and factual accuracy.
- **Step 3: Contextual Reasoning** - Construct an enriched prompt using confirmed knowledge, allowing Tiny LLMs to perform high-quality reasoning locally.
- **Step 4: Fallback to DoD and Big LLMs** - Only if SCR fails or lacks confidence, a DoD escalation is triggered.

---
