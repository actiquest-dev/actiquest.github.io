---
icon: briefcase
label: Self-Knowledge
order: 89
---

-----

# Local Evaluation and Self-Knowledge Checkpoint for DoD Responses

This section outlines how Membria's DoD agent determines the optimal path to answering a user query. It uses a local Self-Knowledge Checkpoint module to decide whether the query can be answered from internal knowledge, from a local RAG system, or requires external DoD inference. All reasoning is performed locally using a lightweight reward model (TinyRM), a local SLM, and optional use of the Knowledge Cache Graph (KCG).

### Objective

Efficiently select the most accurate and useful answer while minimizing unnecessary computation and external calls. The Self-Knowledge Checkpoint module ensures that retrieval and generation are invoked only when needed.

### Architecture Overview

```
User Query
   │
   ▼
Self-Knowledge Checkpoint (SLM)
   │
   ├─ LOCAL → SLM Answer Generation
   │
   ├─ CACHE → Query Knowledge Cache Graph (KCG)
   │
   ├─ LOCAL RAG → Local Retrieval-Augmented Generation
   │
   └─ DOD → Distillation-on-Demand (Big LLMs)
             │
             ▼
     Receive 3–4 LLM Answers
             ▼
   TinyRM Scoring + Optional SLM Tie-Break
             ▼
   Best Answer → Output + Optional Caching in KCG
```

### Components

1. **Self-Knowledge Checkpoint**  
   A local SLM that decides whether to answer using built-in knowledge, the cache, a local RAG system, or to escalate to external distillation. This step prevents unnecessary computation and improves response time.

2. **Local RAG Module**  
   If needed, a local vector database (e.g., FAISS, Qdrant) is queried using the input prompt to provide retrieved context for the SLM to use in answer generation.

3. **TinyRM Scoring**  
   A small reward model evaluates answers for quality and relevance based on the original query.

4. **SLM Tie-Breaker**  
   If scores are inconclusive, the SLM selects the most accurate answer with reasoning.

5. **Caching**  
   Final verified answers may be stored in KCG for future reuse.

### Pseudocode Example

```python
decision = self_knowledge_checkpoint(query)

if decision == "LOCAL":
    return slm_answer(query)
elif decision == "CACHE":
    context = query_kcg(query)
    return slm_with_context(query, context)
elif decision == "LOCAL_RAG":
    context = query_local_vectordb(query)
    return slm_with_context(query, context)
elif decision == "DOD":
    answers = call_big_llms(query)
    scores = [tinyrm_score(query, a) for a in answers]
    if max(scores) - sorted(scores)[-2] < 0.1:
        return slm_compare_all(query, answers)
    else:
        return answers[argmax(scores)]
```

### Total Latency Estimate

| Step                             | Estimated Delay     |
|----------------------------------|---------------------|
| Self-Knowledge Checkpoint (SLM)  | 100–300 ms          |
| TinyRM Scoring                   | 200–400 ms          |
| SLM Tie-break Reasoning          | 300–600 ms          |
| KCG Retrieval (if used)          | 200–500 ms          |
| Local RAG Retrieval              | 150–400 ms          |
| DoD Request (optional, external) | 800–2000 ms         |
| Output & Caching                 | 50–100 ms           |

### Overall Delay Summary

- Local only with cache or RAG: 0.8–1.6 seconds
- With external DoD inference: 2.5–5 seconds
- Fully local with fallback: 1.0–1.8 seconds

### Benefits

- **Privacy**: All routing logic is local and intelligent.
- **Speed**: Avoids unnecessary retrieval or external calls.
- **Quality**: Scales from built-in knowledge to local RAG to global distillation.
- **Learning**: Answer paths and outputs improve the cache over time.

This modular architecture allows Membria agents to act with contextual intelligence and progressive autonomy while maintaining trust and performance across environments.

---
