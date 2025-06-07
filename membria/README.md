---
icon: ai-model
label: Membria
---

# Knowledge Cache Graph (KCG) for Cache-Augmented Generation (CAG)

## Introduction

This documentation describes the architecture, purpose, and benefits of Cache-Augmented Generation (CAG) and Distillation on Demand (DoD) within the Actiq ecosystem. The system combines on-device AI, distillation on demand, and a decentralized knowledge layer to create a fast, private, and evolving intelligence system that learns from user interaction and scales through distributed memory using Decentralized Knowledge Graph (DKG).

## Table of Contents

1. [Overview](overview.md)
2. [Problem Statement](problem-statement.md)
   - 2.1 Key Challenges
3. [Training Methods for Large and Tiny Models](training-methods.md)
   - 3.1 Centralized Foundation Model Training
   - 3.2 Decentralized & Self-Hosted Approaches
   - 3.3 Current Limitations
   - 3.4 Role of Distillation on Demand (DoD)
4. [Alternative Knowledge Learning Methods](alternative-methods.md)
5. [Proposed Solution](proposed-solution.md)
   - 5.1 Components
6. [Technical Architecture Overview](technical-architecture.md)
   - 6.1 Storage Layer
   - 6.2 Index & Graph Layer
   - 6.3 Access & Query Layer
   - 6.4 Distillation & Validation Layer
   - 6.5 Economic Layer
   - 6.6 Governance & Reputation Layer
   - 6.7 Architectural Principles
7. [CAG Storage, Query & Privacy Architecture](storage-query-privacy.md)
   - 7.1 CAG Storage in Arweave
   - 7.2 Fast Querying and Relationship Analysis (Graph Layer)
8. [KCG Indexing with The Graph Subgraph](kcg-indexing.md)
   - 8.1 Storage Layer: Arweave
   - 8.2 Index & Query Layer: The Graph Subgraph
   - 8.3 GraphQL API Interface
   - 8.4 Sync & Update Flow
   - 8.5 Advantages Over Centralized Graph Databases
   - 8.6 Architecture
9. [SCR-enhanced Reasoning Pipeline for KCG+CAG](scr-reasoning.md)
   - 9.1 SCR Reasoning Layer as the Default Inference Path
10. [Roles of Validators, Gateways, and DoD Agents](roles.md)
    - 10.1 DoD Agents: Knowledge Distillation Layer
    - 10.2 Gateways: Infrastructure & Access Layer
    - 10.3 Validators: Quality & Consensus Layer
    - 10.4 Role Comparison
    - 10.5 Synergy of Roles
11. [Validator Infrastructure & Placement](validator-infrastructure.md)
    - 11.1 Off-chain Validator Nodes
    - 11.2 Consensus & Proof Submission (On-chain Interaction)
    - 11.3 Validator Deployment Environments
    - 11.4 Architectural Positioning
    - 11.5 Benefits of Off-chain Validation
12. [KCG Entry Format for Arweave Storage](kcg-entry-format.md)
    - 12.1 Entity Entry Example (JSON format)
    - 12.2 Relation Entry Example (JSON format)
    - 12.3 Arweave Transaction Tags
    - 12.4 Integrity and Linking
    - 12.5 Storage Optimizations
13. [Tokenomics & Deflation Design](tokenomics.md)
    - 13.1 Sources of Token Demand
    - 13.2 Reward Distribution (Emission Side)
    - 13.3 Deflationary Burn Mechanisms
    - 13.4 Emission Control Levers
    - 13.5 Sustainability & Scarcity Model
    - 13.6 Summary Flow
14. [Token Flow and Reward Distribution](token-flow.md)
    - 14.1 Internal Validator Allocation
    - 14.2 Dynamic Complexity Adjustment
    - 14.3 DoD Agents Performance Bonuses
15. [Integrations](integrations.md)
16. [Advantages of the KCG+CAG Approach](advantages.md)
17. [Conclusion](conclusion.md)

## Purpose of Documentation

This documentation is intended for developers, researchers, and stakeholders interested in understanding the architecture and functionality of the Knowledge Cache Graph (KCG) and Cache-Augmented Generation (CAG) system. It covers technical aspects, economic model, and benefits of the approach for creating a scalable, efficient, and verifiable knowledge augmentation system for Tiny Language Models (LLMs).

## How to Use This Documentation

The documentation is organized into logical sections, each focusing on a specific aspect of the KCG+CAG system. You can read the documentation sequentially or navigate to specific sections of interest using the table of contents above.

To get started, it is recommended to read the [Overview](overview.md) and [Problem Statement](problem-statement.md) sections to understand the core concepts and challenges that the KCG+CAG system addresses.
