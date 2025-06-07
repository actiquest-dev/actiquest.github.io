---
icon: graph
label: KCG Indexing
---

# KCG Indexing with The Graph Subgraph

To achieve decentralized, scalable, and performant indexing for the Knowledge Cache Graph (KCG), we propose leveraging **The Graph Subgraph** architecture as an alternative to centralized graph databases like Neo4j.

## Storage Layer: Arweave

* All KCG entries (entities, relations, ontologies) are stored as immutable JSON-LD documents on Arweave.
* Each entry is identified by its TXID and enriched with metadata tags (e.g., `Type`, `Relation`, `Ontology`).

## Index & Query Layer: The Graph Subgraph

* A custom Subgraph mapping is created to parse Arweave transactions based on relevant tags.
* The mapping script extracts entity and relation data from JSON-LD payloads.
* Subgraph Entities include:

  * **KCGEntity:** id, type, attributes.
  * **KCGRelation:** source, target, relationType, context.
* Relationships are maintained via content-addressed links (Arweave TXIDs).

## GraphQL API Interface

* The Subgraph exposes a standardized GraphQL API for querying the KCG.
* Example query:

  ```graphql
  query {
    kcgEntities(where: {type: "Person"}) {
      id
      attributes { key, value }
      relations { target { id }, relationType }
    }
  }
  ```
* This enables Tiny LLMs and DoD Agents to perform semantic searches efficiently.

## Sync & Update Flow

* The Graph Indexers continuously monitor Arweave for new transactions matching KCG patterns.
* Updates to the knowledge graph are reflected in real-time within the Subgraph index.

## Advantages Over Centralized Graph Databases

| Aspect                  | The Graph Subgraph                      | Neo4j                                    |
| ----------------------- | --------------------------------------- | ---------------------------------------- |
| Immutable Data Indexing | Native support for Arweave Data Sources | Requires manual synchronization          |
| Query Interface         | Decentralized GraphQL API               | Proprietary Cypher Query                 |
| Scalability             | Distributed Indexer Network             | Requires federated custom deployment     |
| Decentralization        | Yes (hosted or decentralized subgraphs) | No (centralized unless custom federated) |
| Speed of Access         | Low latency for indexed queries         | Fast on dedicated infrastructure         |
| Standards Compliance    | OpenGraphQL Schema, Arweave Integration | Proprietary database format              |

## Architecture

* **Immutable Storage:** Arweave for permanent knowledge storage.
* **Decentralized Index & Query:** The Graph Subgraph for efficient search and retrieval.
* **Consumption Layer:** Tiny LLMs and DoD Agents interact via GraphQL.
* **Optional Caching:** Gateways can implement caching for ultra-low latency.

This approach ensures a fully decentralized, scalable, and performant knowledge indexing solution, aligning with the KCG+CAG principles of openness, permanence, and efficiency.
