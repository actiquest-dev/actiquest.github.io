---
icon: check
label: Knowledge Gaps
order: 87
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
