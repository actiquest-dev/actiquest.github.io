---
icon: book
label: Alternative Methods
---

# Alternative Knowledge Learning Methods

While Distillation on Demand (DoD) is a central mechanism in the KCG+CAG architecture, it is not the only approach available for enhancing Tiny LLMs. Several alternative methods exist, each with unique trade-offs:

1. **Full Fine-Tuning:** Comprehensive retraining of the Tiny LLM on new datasets. Although it provides deep integration of new knowledge, it is computationally intensive and impractical for frequent updates, especially on edge devices.

2. **LoRA / PEFT (Parameter-Efficient Fine-Tuning):** Lightweight techniques that adapt small parts of the model's parameters. These methods reduce training costs but still require infrastructure and do not scale efficiently for continuous, real-time adaptation.

3. **Retrieval-Augmented Generation (RAG):** Uses external vector databases to retrieve relevant documents, which are then fed into the model's context. While flexible, maintaining large vector stores is costly, and RAG does not perform reasoning-only retrieval.

4. **Prompt Injection / Prompt Templating:** Simple methods of prepending prompts with factual information. Useful for quick fixes, but limited by context length and not suitable for permanent knowledge augmentation.

5. **Cache-Augmented Generation (CAG) with KCG:** Our proposed solution leverages a shared, validated knowledge cache. Once distilled through DoD, this knowledge becomes reusable for future queries, enabling low-latency, cost-effective reasoning.

In this ecosystem, **DoD serves as the generator of missing knowledge**, addressing queries where existing caches fall short. Unlike retraining or static prompt engineering, DoD enables dynamic, real-time enrichment of Tiny LLMs by distilling knowledge from Big LLMs and recording it in the KCG for scalable reuse.

By combining DoD with Cache-Augmented Generation, we achieve a sustainable balance: costly distillation happens only when necessary, while repetitive queries benefit from fast, cached responses.

This approach ensures that Tiny LLMs can continuously evolve and deliver high-quality, verified outputs without incurring prohibitive computational or financial overhead.

This highlights the potential for substantial optimization through caching mechanisms like KCG, reducing redundant inference calls to Large Language Models (LLMs).
