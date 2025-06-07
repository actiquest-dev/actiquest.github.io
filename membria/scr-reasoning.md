---
icon: square-circle
label: SCR Reasoning
order: 92
---

# Selective Contextual Reasoning (SCR)

Selective Contextual Reasoning is Membria’s method for delivering fast, context-aware answers without overwhelming Tiny Language Models. SCR retrieves only the most relevant knowledge fragments, confirms them, and injects them into the prompt in a structured way.

## Core Steps

1. **Semantic Retrieval**  
   The agent searches its local KV cache and the nearest gateway index for high-similarity chunks related to the current query.

2. **Filtering and Deduplication**  
   Retrieved chunks are ranked by freshness, confidence and semantic distance. Duplicates and low-scoring items are discarded.

3. **Context Assembly**  
   The agent builds a compact prompt buffer composed of:  
   - static facts (long-term)  
   - dynamic facts (query-specific)  
   - short recall from recent turns

4. **Local Inference**  
   The Tiny LM receives the trimmed context and generates a response. Because the prompt is lean, latency stays sub-200 ms even on modest hardware.

5. **Fallback to DoD**  
   If the model’s confidence is below threshold or a cache miss occurs, the agent triggers a Distillation-on-Demand cycle with a Big LLM.

## Segmented KV Buffer

| Segment        | Content Type            | Typical TTL      |
|----------------|-------------------------|------------------|
| Session Memory | Recent dialog turns     | Seconds to hours |
| Local Cache    | Personal or domain data | Hours to days    |
| Global Cache   | Gateway / KCG facts     | Days to weeks    |

A scheduler prioritizes tokens from the highest-value segments until the model’s context limit is reached.

## Performance Advantages

- **Latency** Retrieval and inference complete in < 200 ms on edge devices.  
- **Token Savings** Up to 80 percent fewer Big-LLM calls versus naive RAG.  
- **Personalization** Local cache keeps user-specific facts close to the model.  
- **Privacy** Only distilled context leaves the device when fallback is needed.

## Implementation Notes

- Embedding search uses HNSW or Faiss for sub-millisecond nearest-neighbor lookups.  
- Filtering relies on cosine similarity plus freshness weighting.  
- Prompt budgets are enforced by a hard token cap; excess chunks are paged out.  
- SCR runs in a separate thread so UI latency remains low.

Selective Contextual Reasoning turns Tiny LMs into efficient, privacy-preserving assistants capable of answering most queries without expensive cloud inference.
