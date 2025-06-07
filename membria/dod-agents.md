---
icon: container
label: DoD Agents
order: 87
---

# DoD Agents

Distillation-on-Demand (DoD) agents are lightweight runtimes that live on user devices or edge servers. They detect knowledge gaps, run local reasoning and trigger new knowledge distillation when needed.

## Core Responsibilities
- **Gap detection**  
  Spot missing or outdated facts by monitoring local queries, cache misses and confidence thresholds.
- **Selective Contextual Reasoning**  
  Retrieve the smallest relevant context from local and gateway caches, then run on-device inference to answer immediately where possible.
- **Distillation orchestration**  
  When local reasoning is insufficient, compose a distilled prompt for a Big LLM, gather responses and synthesize the best answer.
- **Local self-training**  
  Use idle cycles (for example at night) to perform QLoRA fine-tuning, baking freshly distilled knowledge into the Tiny LM.
- **Privacy guard**  
  Ensure only distilled, context-safe snippets leave the device; raw private data never reaches a gateway.

## Workflow
1. Receive user query.  
2. Attempt local answer via SCR and Tiny LM.  
3. If confidence is low, call Big LLM and aggregate multiple responses.  
4. Evaluate candidates with a Tiny reward model and choose the best.  
5. Forward distilled knowledge to a gateway for validation and caching.  
6. Schedule nightly QLoRA to update local weights.

## Incentives and Rewards
- Earn token bounties by completing gateway distillation tasks first.  
- Save on external LLM costs through cache hits and local inference.  
- Higher reputation unlocks priority tasks and larger rewards.

## Resource Requirements
| Component   | Minimum Spec | Notes                             |
|-------------|--------------|-----------------------------------|
| CPU or GPU  | 4 cores / 6 GB VRAM | Runs Tiny LM inference        |
| Storage     | 10 GB        | Local KV cache and model deltas   |
| Connectivity| Intermittent | Only needed for gateway sync      |

## Interaction with Gateways
DoD agents push distilled answers to gateways along with confidence scores and minimal context. Gateways validate, cache and reward the agent upon acceptance.

## Security and Trust
- Agents sign every distillation packet with a local key pair.  
- Repeated low-quality submissions reduce reputation and throttle DoD call limits.  
- All local private data remains encrypted at rest; only distilled summaries are transmitted.

DoD agents turn passive edge devices into active knowledge contributors, accelerating network learning while protecting user privacy.
