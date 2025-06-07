---
icon: cache
label: Cache Indexing
order: 89
---

## Hybrid Cache Management and Data Versioning

In the Membria system, the "cold" cache layer and data versioning are managed through a multi-tiered caching architecture and the immutability of the Knowledge Cache Graph (KCG) on Arweave.

### Cold Layer Cache Management

The "cold" KV-cache layer is designed for "low-frequency, outdated, or weakly relevant KV-blocks". Management involves:

-   **Movement to Cold Layer:** Entries are moved from "hot" and "warm" layers based on low usage frequency, low importance score, last accessed timestamp, and overall freshness. Gateways rank entries using a hybrid scoring model (importance x frequency x freshness) and evict or offload stale entries.
-   **Storage:** Outdated entries are offloaded to "disk/off-chain cold storage".
-   **Access and Retrieval:** Data from the cold layer can be recalled if relevant topics re-emerge, using a "recency-based paging" mechanism.

### Data Obsolescence Criteria

Data in the KCG or KV-cache is considered "outdated" based on:

-   **Time Since Last Access:** Entries that haven't been accessed for a long time.
-   **Newer, More Relevant Information:** Gateways track "stale or outdated KV-blocks: old distillations no longer consistent with updated knowledge graphs or ontologies". This means if new, validated information on the same topic appears, the old information may be considered outdated.
-   **Low Relevance or Utility:** Entries that the system deems weakly relevant to current queries or of low importance.
-   **Validation of New Information:** The validator process for new knowledge implicitly helps identify outdated data if the new information refutes or replaces the old.

### Handling Outdated Data and Versioning in an Immutable KCG

Since the KCG is stored on Arweave and is immutable, outdated entries cannot be directly deleted or modified within the KCG. Instead, the system uses the following approaches:

-   **Creation of New Versions:** When information is updated, a new entry is created in the KCG. This new entry undergoes validation by Gateways and Validators.
-   **Updating Indexing Layers:** While the KCG data itself is immutable, the indexing layers managed by Gateways (e.g., Gateway KV-cache, off-chain semantic indexes) are mutable. These layers are updated to point to the latest and most relevant versions of knowledge in the KCG. The "Workflow Overview" states that after validation, the Gateway records the entry into the KCG, and a "corresponding KV entry is updated in the public KCG KV-layer for efficient future retrieval". This "update" likely refers to adding new pointers or updating metadata associated with pointers to immutable KCG data to ensure access to the current version.
-   **Marking and Deprioritization:** Outdated entries can be marked as such or deprioritized in the mutable Gateway indexes. This ensures that when a query is made, the Selective Contextual Reasoning (SCR) system retrieves the current information.
-   **Semantic Overlap:** Newer, more complete, or more accurate knowledge entries may semantically overlap with older ones. The older entry remains on Arweave, but the system prioritizes the newer one.

Although the document does not explicitly mention protocols like ArFS (Arweave File System) or ArNS (Arweave Name System), the described architecture is compatible with using such systems for version management (e.g., where a name points to the TXID of the current knowledge version). This would allow for maintaining current pointers to the latest knowledge versions within immutable storage.

### Accessing "Cold" Data (Off-Chain Cold Storage)

-   **Latency:** The document does not specify exact latency values for accessing "off-chain cold storage". However, it implies that access to this layer will be slower compared to the "hot" and "warm" cache layers. Retrieving data from cold storage would impact overall response time.
-   **Cost:** Specific cost metrics are not detailed. Primary costs would be associated with maintaining this storage (disk space, I/O operations). The system aims to minimize calls to the cold layer through efficient management of faster cache tiers.

Thus, Membria addresses data obsolescence and versioning in the immutable KCG by creating new entries for updated information and managing access to these versions through flexible, mutable indexing and caching layers controlled by Gateways.

### Membria's Hybrid Cache Architecture

Membria employs a hybrid approach to knowledge storage and caching, leveraging both on-chain immutability and off-chain speed and flexibility.

The core, immutable Knowledge Cache Graph (KCG) is designed for decentralized networks like Arweave, including a "Public KV-layer in KCG" that is part of this immutable, community-verified cache.

However, to ensure speed, efficiency, and flexibility, Membria also utilizes several off-chain caching and indexing layers managed by various system participants:

-   **Gateway KV-cache:** This is a "high-performance, shared caching of validated knowledge and reasoning shortcuts" managed by Gateways. It resides on the Gateway's infrastructure, not on Arweave, and provides fast access to frequently requested data.
-   **Gateway Off-Chain Index Layer:** Gateways maintain "lightweight off-chain semantic graphs, vector indexes, and retrieval services". These indexes are also off-chain and accelerate the Selective Contextual Reasoning (SCR) pipelines.
-   **On-device Tiny LLM KV-cache:** This is a "fast, personalized cache of frequently used knowledge" located directly on user devices.
-   **Off-chain cold storage:** The "KV Cache Orchestration" section mentions that Gateways "evict or offload stale entries to disk/off-chain cold storage". This storage is used by Gateways for data that has become less relevant to their active ("hot" or "warm") caches, and it is also off-chain.

This hybrid architecture means:

-   **On-chain (Arweave):** Stores the primary, immutable, and verifiable knowledge layer (KCG), including the public KV-layer.
-   **Off-chain:** Various levels of caching and indexing exist (on Gateways, on devices, in Gateway cold storage) to provide fast access, personalization, and efficient data lifecycle management. These off-chain systems can store copies of frequently used data from Arweave, derived data (e.g., indexes), or temporary data.

The off-chain components are crucial for system performance, allowing Tiny LLMs to quickly access knowledge without needing constant direct interaction with the (potentially slower) Arweave storage for every operation.

---
