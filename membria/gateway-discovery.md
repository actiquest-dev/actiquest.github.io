---
icon: search
label: Gateway Discovery
order: 86
---

## Discovery and Efficient Gateway Selection

In decentralized architectures like KnowledgeCache, it is inefficient for a DoD agent to blindly contact random Gateways, especially without knowing which ones are suitable for a given task. However, established decentralized discovery mechanisms can address this without requiring knowledge of each Gateway's cache contents.

### Discovery Mechanism Overview

While not explicitly described in the documentation, the system implies a discovery model based on the Peaq Protocol:

1. **Service Discovery via Peaq Protocol:**  
   Gateways register their presence and capabilities (e.g., location, load, specialization) in a decentralized service registry. DoD agents query this registry to discover available Gateways.

2. **Capability-based Selection:**  
   After retrieving available Gateway metadata, the DoD agent selects the most appropriate node using:
   - **Geographic Proximity** to minimize latency.
   - **Load and Availability**, choosing underutilized nodes.
   - **Reputation or Staking**, favoring trusted Gateways.
   - **Domain Specialization**, optionally preferring nodes tuned for specific topics.

3. **Routing Logic Inside Gateway:**  
   Once a Gateway is selected, the DoD agent sends the request. The Gateway:
   - First checks its **off-chain Gateway KV-cache**.
   - If no match, uses **semantic and vector indexes** to locate facts in the **on-chain KCG** (Arweave).
   - Applies **contextual reasoning** to construct a prompt using the retrieved knowledge.
   - Optionally falls back to a Big LLM if necessary.

4. **Distillation and Write-back:**  
   If new insights are distilled, the DoD agent sends back the result to the Gateway for validation and permanent write to the on-chain KCG.

### Caching Strategy and Priority Layers

Gateways are designed to optimize speed and cost:
- On-device Tiny LLM KV-cache: ~20 ms latency.
- Gateway shared KV-cache: 50–200 ms.
- Public KCG access (Arweave): 300–1000 ms (direct), faster via index.
- Big LLM fallback: 800–2000 ms.

This hierarchy ensures:
- Most lookups are handled locally or via Gateway caches.
- Gateway caches are dynamically updated using usage analytics (e.g., repeated misses, request spikes).
- High-demand knowledge is promoted to “hot” or “warm” tiers for optimal reuse.

### Accelerated KCG Access via Gateway Indexes

Gateways avoid querying Arweave directly for each lookup. Instead, they:
- Maintain **off-chain semantic graphs and vector indexes** pointing into the KCG.
- Leverage these for sub-second retrieval from large knowledge graphs.
- Operate a **Federated Knowledge Mesh**, replicating indices across multiple nodes to enhance locality and fault-tolerance.
- Use multi-layered hybrid caching: on-device, Gateway-level, and public (KCG).

This design provides a scalable and low-latency infrastructure for real-time, on-demand knowledge reasoning in a fully decentralized setting.
