---
icon: database
label: Storage, Query & Privacy
order: 93
---

# CAG Storage, Query & Privacy Architecture

## CAG Storage in Arweave

For immutable and verifiable knowledge storage, Arweave is the preferred solution due to its permanent data availability. Each fragment of the Knowledge Cache Graph (KCG)-nodes, edges, ontologies, and indices - is stored as an individual Arweave transaction (TX). Key characteristics include:

* Each KCG object receives a unique TXID, serving as a perma-link derived from its content hash.
* Large graphs are stored using chunked storage with CID-based linking for efficient traversal.

**Example:**

* Entity Node X → Attributes file → TXID: 0xabc123.
* Relation (X relates to Y) → Separate file → TXID: 0xdef456.
* The entire graph is connected via an index file or JSON-LD structure with its own TXID.

Filecoin offers a similar decentralized storage model but relies on signed storage contracts (6-12 months), making it less practical for permanent knowledge preservation. Therefore, Arweave remains the primary storage layer for long-term knowledge caching.

## Fast Querying and Relationship Analysis (Graph Layer)

While Arweave and Filecoin serve as robust storage layers, efficient graph querying necessitates an additional index and query layer.

**Graph Layer Architecture:**

1. **Off-chain Graph Indexing:**

   * Network participants (indexers) parse Arweave data using TXIDs and CIDs.
   * The graph structure is reconstructed and maintained locally using graph databases (e.g., Neo4j, TypeDB, custom RDF stores).
   * Index layers can be decentralized via IPFS/DAG protocols.

2. **Semantic Query API:**

   * Provides REST or GraphQL endpoints for graph traversal, relationship queries, and semantic searches.
   * Example query: "Retrieve all relationships from Node X to Category Y within period T."

**Best Practices & Tools:**

* Utilize The Graph's Subgraph architecture with Arweave Data Sources.
* Explore OriginTrail DKG integrations with Arweave/IPFS.
* Develop a custom micro-subgraph indexer tailored for CAG.

**Caching Popular Relationships:**

* Frequently requested paths are cached by indexers.
* Merkle Proofs ensure data freshness and integrity without needing to re-fetch from Arweave.
