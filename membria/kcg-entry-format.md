---
icon: file-code
label: KCG Entry Format
order: 90
---

# KCG Entry Format for Arweave Storage

Each KCG Entry represents either an **Entity** or a **Relation** and is stored immutably on Arweave/IPFS. The entries are designed to be content-addressable and verifiable, ensuring transparency and data integrity.

## Entity Entry Example (JSON format):

```json
{
  "type": "Entity",
  "id": "kcg:0xabc123",
  "label": "Electric Vehicle",
  "attributes": {
    "category": "Product",
    "manufacturer": "Tesla",
    "region": "Global"
  },
  "evidence": {
    "source": "DoD-Query from Claude 3",
    "confidence": 0.92,
    "created_at": "2025-05-14T12:34:56Z",
    "created_by": "DoD-Agent:Node42"
  }
}
```

## Relation Entry Example (JSON format):

```json
{
  "type": "Relation",
  "id": "kcg:0xdef456",
  "source": "kcg:0xabc123",
  "target": "kcg:0xdef789",
  "relation": "depends_on",
  "context": "Global Battery Supply Chain",
  "evidence": {
    "source": "DoD-Query from GPT-4 Turbo",
    "confidence": 0.89,
    "created_at": "2025-05-14T12:36:00Z",
    "created_by": "DoD-Agent:Node42"
  }
}
```

## Arweave Transaction Tags:

Each entry is accompanied by Arweave tags for indexing and searchability:

| Tag Key       | Example Value                    |
| ------------- | -------------------------------- |
| `App`         | `KnowledgeCacheGraph`            |
| `Type`        | `Entity` / `Relation`            |
| `Relation`    | `depends_on` (for Relation type) |
| `SourceModel` | `GPT-4`, `Claude 3`              |
| `Category`    | `SupplyChain`, `Product`, etc.   |
| `Confidence`  | `0.89`                           |
| `CreatedBy`   | `DoD-Agent:Node42`               |

## Integrity and Linking:

* The `id` field is derived from the Arweave transaction ID (TXID), ensuring content-addressability.
* `source` and `target` in Relation entries refer to other Entity IDs, maintaining graph structure.
* Provenance data in `evidence` ensures transparency of origin and quality.

## Storage Optimizations:

* Bundling multiple entries in a single Arweave transaction via Bundlr to optimize costs.
* CID linkage for efficient DAG-based traversal.

This format provides a robust, scalable method for storing and retrieving validated knowledge in a decentralized, immutable graph structure.
