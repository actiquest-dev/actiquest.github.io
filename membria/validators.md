---
icon: checklist
label: Validators
order: 88
---


# Validators

Validators provide the final layer of trust in Membria, confirming the correctness of knowledge proposals and enforcing network rules through stake-weighted consensus.

## Core Responsibilities
- **Knowledge validation**  
  Review distilled entries submitted by gateways, verify supporting evidence and ensure semantic coherence.
- **Consensus voting**  
  Sign or reject proposals in a stake-weighted quorum; finality is reached when a super-majority of signatures is recorded.
- **Proof-of-Knowledge attestation**  
  Issue cryptographic attestations that bind each accepted entry to its on-chain transaction ID, enabling end-to-end provenance.
- **Dispute resolution**  
  Arbitrate conflicts or appeals when competing claims or malicious submissions arise.

## Staking and Rewards
- Validators lock tokens as collateral; larger stakes grant higher voting power but increase potential loss on misbehavior.
- Successful validation cycles yield block rewards and a share of DoD fees.
- Slashing mechanisms penalize validators who sign fraudulent or low-quality entries.

## Infrastructure Requirements
| Component      | Minimum Spec               | Purpose                             |
|----------------|----------------------------|-------------------------------------|
| Validation node| 4 vCPU, 8 GB RAM           | Signature aggregation and voting    |
| Light index    | 20 GB SSD                  | Quick access to recent KCG entries  |
| Uptime target  | 99.5 percent               | Maintain quorum availability        |

Nodes do not store full gateway caches, keeping hardware costs modest.

## Governance Role
Validators participate in on-chain voting to adjust:
- Quorum size and signature thresholds  
- Slashing parameters and reward rates  
- Protocol upgrades affecting KCG schemas or cache policies  

This makes them stewards of both technical security and economic health.

## Fraud Detection and Auditing
- Validators run statistical and semantic checks to spot spam or contradictory claims.
- Periodic audits compare validator signatures with historical accuracy scores; repeated errors lower reputation and staking limits.
- All validator actions are logged on-chain, allowing independent review.

## Interaction with Gateways
1. Gateway packages a validated proposal and broadcasts it.  
2. Validators retrieve the package, verify evidence and cast votes.  
3. Once quorum is met, the gateway finalizes the write to KCG.  
4. Validators’ signatures become an immutable part of the record.

## Security and Resilience
- Stake-weighted voting discourages Sybil attacks.  
- Rotating committee selection prevents collusion.  
- Slashed stakes are partially burned and partially redistributed to honest validators, reinforcing correct behavior.

Validators thus serve as the cryptographic and economic backbone of Membria, ensuring that only accurate, well-sourced knowledge becomes part of the collective memory.
