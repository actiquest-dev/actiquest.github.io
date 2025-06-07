---
icon: briefcase
label: What are Tiny LM's
order: 94
---

# Specifications for "Tiny LLMs"

## 1. Definition

"Tiny LLMs" are a specific segment of Small Language Models (SLMs) characterized by a parameter count typically ranging from **4 billion to 30 billion parameters**. They are designed for greater efficiency, reduced computational cost, and suitability for more specialized tasks or resource-constrained environments compared to very large language models (LLMs, often 100B+ parameters). Tiny LLMs aim to balance performance with operational feasibility.

## 2. Parameter Range

* **Specified Range:** 4 billion to 30 billion parameters.
    * This defines "Tiny LLMs" as a distinct category within the broader SLM landscape. Many SLMs exist with fewer than 4 billion parameters (sometimes in the millions).
    * The upper limit of ~30 billion parameters is a generally recognized threshold for what can be considered a "small" language model in contrast to large-scale ones.

## 3. Supported Architectures

* **Primary Architectures:**
    * **Transformer:** Predominantly decoder-only (e.g., GPT-style) for generative tasks. Encoder-decoder architectures (e.g., T5-style) may also be used for specific tasks.
    * **Mixture of Experts (MoE):** Some models in this range utilize MoE to activate only a subset of parameters per input, improving efficiency while allowing for a larger total parameter count.
    * **Hybrid Architectures:** Emerging designs may combine Transformer elements with other efficient structures like State Space Models (SSMs).

* **Common Optimization & Compression Techniques:**
    * **Attention Mechanism Variants:** Grouped-Query Attention (GQA), Multi-Query Attention (MQA), Sliding Window Attention, and other efficient attention methods to reduce computational load.
    * **Quantization:** Reducing the numerical precision of model weights (e.g., to 8-bit integers (INT8), 4-bit (NF4, GPTQ)) to significantly shrink model size and accelerate inference, crucial for resource-limited deployment.
    * **Pruning:** Removing less critical weights or structural elements from the neural network.
    * **Knowledge Distillation:** Training a smaller "student" model to mimic the behavior of a larger, more capable "teacher" model.
    * **Low-Rank Factorization (LoRA & variants):** Widely used for efficient fine-tuning by adapting a small number of additional parameters.

## 4. Typical Computational Resources

The goal for Tiny LLMs is to be runnable on more accessible hardware compared to their larger counterparts.

* **CPUs:**
    * Modern multi-core CPUs (e.g., Intel Core i7/i9, AMD Ryzen 7/9, or newer Arm-based processors like those in high-end laptops or servers).
    * CPU-only inference is possible, especially for smaller models in this range (4-8B) or heavily quantized versions, but will be slower than GPU-accelerated inference.
* **GPUs:**
    * **4-8 Billion Parameter Models:** Often runnable on consumer-grade GPUs with 8GB-12GB+ VRAM (e.g., NVIDIA GeForce RTX 3060/4060) especially with 4-bit or 8-bit quantization.
    * **8-15 Billion Parameter Models:** Typically require high-end consumer GPUs with 12GB-24GB VRAM (e.g., NVIDIA GeForce RTX 3080/3090, RTX 4070/4080/4090).
    * **15-30 Billion Parameter Models:** Push the limits of single consumer GPUs, generally needing 24GB VRAM (e.g., RTX 3090/4090) and aggressive quantization. Professional GPUs or multi-GPU setups might be considered for smoother performance without heavy optimization.
* **RAM (System Memory):**
    * Minimum: 16GB, especially if a capable GPU with sufficient VRAM is handling most of the load.
    * Recommended: 32GB or more, particularly for larger models within this range, CPU-only inference, or multitasking.
* **Edge Devices & Specialized Accelerators (NPUs/TPUs):**
    * Models on the lower end of this range (4-8B) or heavily optimized versions of larger ones are increasingly targeted for deployment on edge devices.
    * This includes devices with Neural Processing Units (NPUs) (e.g., in smartphones, embedded systems), and Tensor Processing Units (TPUs) or other AI accelerators for efficient, low-latency inference.

## 5. Advantages

* **Efficiency:** Lower computational demand and faster inference compared to large LLMs.
* **Cost-Effectiveness:** Reduced expenses for training (if applicable), fine-tuning, and deployment.
* **Accessibility:** More feasible for individuals or organizations with limited hardware resources.
* **Customization:** Easier and quicker to fine-tune for specific tasks or domains.
* **On-Device Deployment:** Enables local data processing, leading to lower latency, enhanced privacy, and offline capabilities.
* **Reduced Energy Consumption:** More environmentally friendly due to lower power needs.
* **Task-Specific Performance:** Can achieve high accuracy and relevance on narrower tasks for which they are optimized.

## 6. Limitations

* **Reduced Generalization:** May not perform as well as larger LLMs on very broad, complex, or novel tasks outside their training/fine-tuning domain.
* **Smaller Knowledge Base:** Inherently possess less factual knowledge than models trained on vastly larger and more diverse datasets.
* **Potential for Task-Specificity Trade-off:** High performance on a niche task might come at the cost of broader applicability.
* **Fine-tuning Dependency:** Often require careful fine-tuning to achieve optimal performance on specific downstream tasks, including adherence to complex output formats.

## 7. Examples (Illustrative, within or near the 4-30B range)

*(Parameter counts are approximate and can vary by specific model version or quantization)*

* **Phi-3 Family (Microsoft):**
    * Phi-3 Mini (3.8B, 4k/128k context) - *Slightly below, but demonstrates the trend*
    * Phi-3 Small (7B, 8k/128k context)
    * Phi-3 Medium (14B, 4k/128k context)
* **Gemma Family (Google):**
    * Gemma 7B
    * Gemma 2 (9B, 27B)
* **Llama 3 Family (Meta):**
    * Llama 3 8B
* **Mistral Models (Mistral AI):**
    * Mistral 7B (a popular base for many fine-tuned models)
    * Other variants from Mistral AI or the community may fall into this range.
* **Qwen2 Family (Alibaba Cloud):**
    * Qwen2-7B
* **Granite Series (IBM):**
    * Granite 8B
    * Some MoE variants like Granite 3B-A800M (3B total parameters, ~800M active) illustrate efficient designs.


---
