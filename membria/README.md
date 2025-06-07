---
icon: ai-model
label: Membria
---

# Membria: Knowledge Cache Graph (KCG) for Cache-Augmented Generation (CAG) 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdfrLIwLcz7IlKzo2pWTTcM3ZcQ5Sz8o40nhgvFgRkVrhEKbY9gjnDme9YadAb2GIRkFTxHYW3Y752wYtwMsMN09iU3h9To1NM3T2B_0VV4BxJZIbxzg7_xCuQ9HaNFK31R3RYv?key=AsJEkgePh24159X10uUz6PJ-)

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
5. [What Are Tiny Language Models](tiny_lms.md)
6. [Proposed Solution](proposed-solution.md)
7. [Membria for Tiny LM's](capabilities.md)
8. [Technical Architecture Overview](technical-architecture.md)
   - 8.1 Storage Layer
   - 8.2 Index & Graph Layer
   - 8.3 Access & Query Layer
   - 8.4 Distillation & Validation Layer
   - 8.5 Economic Layer
   - 8.6 Governance & Reputation Layer
   - 8.7 Architectural Principles
9. [Workflow Overview](workflow-overview.md)
10. [CAG Storage, Query & Privacy Architecture](storage-query-privacy.md)
   - 10.1 CAG Storage in Arweave
   - 10.2 Fast Querying and Relationship Analysis (Graph Layer)
11. [KCG Indexing with The Graph Subgraph](kcg-indexing.md)
   - 11.1 Storage Layer: Arweave
   - 11.2 Index & Query Layer: The Graph Subgraph
   - 11.3 GraphQL API Interface
   - 11.4 Sync & Update Flow
   - 11.5 Advantages Over Centralized Graph Databases
   - 11.6 Architecture
12. [SCR-enhanced Reasoning Pipeline for KCG+CAG](scr-reasoning.md)
   - 12.1 SCR Reasoning Layer as the Default Inference Path
13. [Roles of Validators, Gateways, and DoD Agents](roles.md)
    - 13.1 DoD Agents: Knowledge Distillation Layer
    - 10.2 Gateways: Infrastructure & Access Layer
    - 10.3 Validators: Quality & Consensus Layer
    - 10.4 Role Comparison
    - 10.5 Synergy of Roles
14. [Validator Infrastructure & Placement](validator-infrastructure.md)
    - 14.1 Off-chain Validator Nodes
    - 14.2 Consensus & Proof Submission (On-chain Interaction)
    - 14.3 Validator Deployment Environments
    - 14.4 Architectural Positioning
    - 14.5 Benefits of Off-chain Validation
15. [KCG Entry Format for Arweave Storage](kcg-entry-format.md)
    - 15.1 Entity Entry Example (JSON format)
    - 15.2 Relation Entry Example (JSON format)
    - 15.3 Arweave Transaction Tags
    - 15.4 Integrity and Linking
    - 15.5 Storage Optimizations
16. [Tokenomics & Deflation Design](tokenomics.md)
    - 16.1 Sources of Token Demand
    - 16.2 Reward Distribution (Emission Side)
    - 16.3 Deflationary Burn Mechanisms
    - 16.4 Emission Control Levers
    - 16.5 Sustainability & Scarcity Model
    - 16.6 Summary Flow
17. [Token Flow and Reward Distribution](token-flow.md)
    - 17.1 Internal Validator Allocation
    - 17.2 Dynamic Complexity Adjustment
    - 17.3 DoD Agents Performance Bonuses
18. [Integrations](integrations.md)
19. [Advantages of the KCG+CAG Approach](advantages.md)
20. [Conclusion](conclusion.md)

## Purpose of Documentation

This documentation is intended for developers, researchers, and stakeholders interested in understanding the architecture and functionality of the Knowledge Cache Graph (KCG) and Cache-Augmented Generation (CAG) system. It covers technical aspects, economic model, and benefits of the approach for creating a scalable, efficient, and verifiable knowledge augmentation system for Tiny Language Models (LLMs).

## How to Use This Documentation

The documentation is organized into logical sections, each focusing on a specific aspect of the KCG+CAG system. You can read the documentation sequentially or navigate to specific sections of interest using the table of contents above.

To get started, it is recommended to read the [Overview](overview.md) and [Problem Statement](problem-statement.md) sections to understand the core concepts and challenges that the KCG+CAG system addresses.
