---
icon: briefcase
label: Tokenomics
---
# Membria Community Edition: Tokenomics

## 1. Introduction

### 1.1. Mission and Vision

Membria's mission is to build a decentralized, self-sustaining, and permanent knowledge base - a 'Wikipedia for Small Language Models (SLMs). The goal of this tokenomic model is to construct a sustainable economy that incentivizes the creation of high-quality knowledge, rewards network participants, and ensures the long-term value growth of the ecosystem.

### 1.2. Key Ecosystem Participants

  * **Users / Knowledge Creators**: Initiators of requests to create new knowledge (DoD), and the ultimate consumers and primary creators of value.
  * **Gateways**: Operators of high-performance nodes that validate, process, cache, and commit knowledge to the network.
  * **Validators**: Participants who secure the Peaq blockchain, upon which Membria operates, by participating in its consensus mechanism.

### 1.3. Token Overview

The economy utilizes a hybrid model with two core assets to separate speculation from true utility:

1.  **$ACTI (The Core Token)**: A deflationary utility token. It is used for staking, governance, and as the primary means of rewarding network participants. **$ACTI is tradable on the open market.**
2.  **$kCREDIT (Knowledge Credit)**: A non-transferable, non-tradable "knowledge credit." It serves as a "ticket" to participate in the initial bootstrapping program and is used to make DoD requests that are then entered into the daily contest. **$kCREDIT is not tradable on the open market.**

-----

## 2. Core Architecture and Ecosystem

### 2.1. The Membria Client: A Personal AI Hub

At the center of the ecosystem is the **Membria Client**, an application that transforms a user's device into a powerful, personalized AI hub. It allows users to:

  * **Load and run** various Small Language Models (SLMs) from Hugging Face.
  * **Manage model "skills"** through **SkillForge** (a LoRA patch manager), adapting their AI for specific tasks like programming, medicine, or law.
  * **Deploy autonomous agents** for complex tasks, such as internet research and in-depth document analysis.
  * **Store knowledge locally and privately** in a personal database powered by **SQLite** with vector search support (for local RAG).

When local knowledge is insufficient, the Client seamlessly connects to the decentralized Membria network via Gateways, enriching its local database with verified knowledge from the global KCG.

### 2.2. The Value Creation Cycle

The primary economic event in the network is the **Distillation-on-Demand (DoD) Request**. This is the process through which a new, verified unit of knowledge is created to populate the Knowledge Cache Graph (KCG). Every such request requires payment.

### 2.3. Payment Mechanism: Dynamic Pricing

To protect the economy from volatility, the price for a DoD request is pegged to USD and dynamically converted to `$ACTI`.

1.  **Target Price in USD**: The network's DAO sets a target price in USD based on the calculated operational cost of a Gateway. *The final target price is **$0.10 per DoD request**.*
2.  **Dynamic Conversion**: Using price oracles, the system retrieves the real-time `$ACTI/USD` exchange rate and presents the user with a fee in the current amount of `$ACTI`.
      * **Formula:** `Fee_in_ACTI = $0.10 / Current_ACTI_Price`

### 2.4. Fee Distribution (Final Model)

Every payment for a DoD request made in `$ACTI` is automatically distributed by a smart contract according to the principle of **maximum deflation**:

  * **50% is Burned:** Irrevocably removed from circulation, exerting strong deflationary pressure.
  * **50% is Rewarded to the Gateway:** A direct incentive for processing, validating, and caching the request.

### 2.5. The Network Accumulation Effect: Decreasing Average Query Cost

While the price of a single **DoD request** remains stable, the **average cost for a user to acquire knowledge trends towards zero over time.** This is achieved as the KCG grows: the more knowledge in the network, the higher the probability of finding an answer in the cache, which is virtually free.

-----

## 3. Deflationary Model

  * **Token Burning:** The primary deflationary mechanism. **50% of every fee** from a value-creating transaction is burned, which is double the rate of previous models and aggressively reduces the total supply of `$ACTI`.
  * **Slashing:** Penalties collected from malicious or underperforming Gateways may also be partially burned.

-----

## 4. Participant Incentives and Rewards

### 4.1. Gateway Rewards

Gateway operators receive two types of rewards:

1.  **Direct Fees:** 50% of each DoD request fee to cover operational expenses (OPEX).
2.  **Staking Rewards:** A stable APR on their locked `$ACTI` stake to cover capital expenses (CAPEX).

### 4.2. A Competitive Knowledge Market

Inspired by Bittensor's model, Gateways with a higher reputation (validation quality, speed, uptime) can be prioritized or receive a larger share of rewards, creating a competitive environment that values quality.

-----

## 5. Gateway Consensus and Knowledge Integrity (L2 Application Layer)

To protect the KCG from hallucinations and low-quality data, Membria employs a multi-layered consensus system among Gateways, operating like a scientific peer-review process.

  * **Individual Validation:** The Gateway that first handles a user's DoD request (the **initiator-gateway**) performs an initial deep validation using its Scorer LLM.
  * **Distributed Quorum Consensus:** If the knowledge passes the initial check, the initiator-gateway sends it for review to a **random quorum** of other active Gateways. The knowledge is only approved if a **supermajority** (e.g., 2/3) of the quorum votes to confirm it.
  * **Final Commit:** Only after achieving consensus does the **initiator-gateway** commit the data to Arweave and the corresponding transaction to Peaq for subgraph indexing. A portion of the initiator's fee is shared with the quorum members to incentivize quality reviews.

-----

## 6. Stimulating Network Growth: The Daily Knowledge Contributor Contest

To solve the "cold start" problem, the ecosystem uses a gamified incentive system.

  * **Objective:** To motivate early users to create valuable, complex, and reusable knowledge.
  * **Evaluation Mechanism:** A **"Scorer LLM"** on the Gateways analyzes all contributions daily and assigns a **"Value Score"** based on criteria like novelty, depth, complexity, factual richness, and reusability potential.
  * **Reward System:** A **dynamic prize pool** is funded by the Ecosystem Fund, with its daily size depending on network activity.

| Activity Level | Active Participants | **Daily Prize Pool Size** |
| :--- | :--- | :--- |
| **"Start" Level** | 1 - 100 participants | **$500 / day** |
| **"Growth" Level** | 101 - 500 participants| **$2,500 / day** |
| **"Scale" Level** | 501+ participants | **$5,000 / day** |

This pool is distributed daily in liquid `$ACTI` to the top-ranked contributors.

-----

## 7. Token Distribution & Vesting

The total supply of **500,000,000 $ACTI** is allocated according to the following schedule. This structure is designed to heavily fund ecosystem growth and incentives while ensuring controlled market entry for other participants.

| Category | Emission % | Token Amount | Vesting Schedule |
| :--- | :--- | :--- | :--- |
| **Ecosystem Fund**| **50%** | **250,000,000** | **48% at TGE (120M)**, then 24-month linear vesting for the remainder (≈5.42M/month) |
| **Private(1) Sale**| 5% | 25,000,000 | 20% at TGE, then 18-month linear vesting |
| **Private(2) Sale**| 3,33% | 16,666,667 | 10% at TGE, then 18-month linear vesting |
| **Public Sale**| 5% | 25,000,000 | 25% at TGE, 3-month cliff, then 12-month linear vesting |
| **Liquidity**| 5% | 25,000,000 | 5% at TGE | then 20-month linear vesting |
| **Contributors**| 10% | 50,000,000 | 0% at TGE | 18-month cliff, then 24-month linear vesting (≈1.33M/month) |
| **Partnerships**| 10% | 50,000,000 | 18-month cliff, then 18-month linear vesting (≈2.78M/month) |
| **Advisors** | 5% | 25,000,000 | 4% at TGE (1.25M), 5-month cliff, then 18-month linear vesting (≈1.33M/month) |
| **DAO Reserve**| 8,67% | 43,333,333 | Locked for 12 months, then 24-month linear vesting |
| **Total**| **100%** | **500,000,000** | |

The "Incentives" allocation is the primary engine for the **Daily Knowledge Contributor Contest** and other growth programs. The large TGE unlock is specifically designed to fund the aggressive bootstrapping phase detailed in the Roadmap.

-----

## 8. Token Architecture and Network Choice: Why Peaq?

The strategic choice to issue `$ACTI` as a native token on the **Peaq** network is dictated by the need for maximum security, performance, and cost-efficiency for core protocol operations like staking, DAO governance, and reward distribution. The architecture uses a "core on Peaq, liquidity via bridges" model, which is an industry standard for building robust and secure Web3 applications.

-----

## 9. Network Infrastructure and Operator Economic Model

### 9.1. Operating Model: Open-Source and Decentralized Operators

Membria functions on a model with a clear separation of roles:

  * **Membria Team:** Acts as the architect and developer of the core technologies.
  * **Independent Operators:** Professional teams with DevOps expertise who run and maintain Gateway nodes.

### 9.2. Infrastructure Requirements: Number of Gateways

To support **10,000 active knowledge creators**, the network requires **10 to 20 high-performance Gateways**.

### 9.3. Gateway Economics: Final ROI Model

The economic model for a Gateway operator is balanced to attract professional participants:

| Metric | Value |
| :--- | :--- |
| **Starting $ACTI Price** | **$0.04** |
| **Capital Requirement (Stake)**| **$100,000** (`2,500,000 $ACTI`) |
| **Annual ROI** | **\~34%** |
| **Payback Period** | **\~3 years** |

### 9.4. Transaction Priority Fund

To ensure network performance during peak L1 load, a special fund is created, capitalized by the Ecosystem Fund. When network congestion is detected, a DAO-controlled keeper bot will automatically sell a small amount of `$ACTI` to buy native `$PEAQ` tokens. These `$PEAQ` tokens are then used to add "tips" to Gateway transactions, increasing their priority.

### 9.5. $ACTI Supply Dynamics: Deflation and Staking

With the 50% burn model, at a load of 10,000 users, **1,875,000 `$ACTI`** will be burned monthly. During the vesting period, the network will experience moderate net inflation. However, once vesting ends, the burn rate will make the model **purely deflationary**.

-----

## 10. Roadmap

  * **Q3 2025: Preparation:** Finalize tokenomics, alpha testing, security audits.
  * **Q4 2025: Launch:** TGE, Mainnet launch, start of Contributor Contest, ASI/Fetch.ai integration.
  * **H1 2026: Growth:** Expand contributor program, release public API, launch joint hackathons.
  * **H2 2026 - 2027: Decentralization:** Launch full on-chain DAO, phase out subsidies, transition Gateways to independent operators.

-----

## 11. Go-to-Market Strategy

Our GTM strategy focuses on strategic partnerships to bootstrap the KCG with high-quality data. Key partners include **Hugging Face** (AI/ML community), **IISC/FSID** (academic expertise), and **Fetch.ai / ASI Alliance** (autonomous agent economy).

-----

## 12. Team & Scientific Board

  * **Michael Aprossine** ([LinkedIn](https://www.google.com/search?q=https://linkedin.com/in/miguel2020)) – **CEO**, 2 hardware exits.
  * **Mike Keer** ([LinkedIn](https://www.google.com/search?q=https://www.linkedin.com/in/mikhail-kiriukhin-97389957)) – **CTO**, CV/AI architect (EU EIC projects).
  * **Phil Khomenok** ([LinkedIn](https://www.google.com/search?q=https://linkedin.com/in/gsarskyes)) – **COO**, $10M ARR ops experience.
  * **Ankit Sahu** ([LinkedIn](https://www.linkedin.com/in/ansahu)) – **CFO**, 20 yrs at Bank of America / UBS Asset Management.
  * **Dr. Ty Vachon, MD** ([LinkedIn](https://www.google.com/search?q=https://linkedin.com/in/tyvachon)) – **Scientific Advisor**, Sports-Medicine Radiologist, fmr. DoD Innovation.
  * **Leonard Khirug, PhD** ([LinkedIn](https://www.google.com/search?q=https://linkedin.com/in/leonardkhiroug)) – **Scientific Advisor**, Neuroscience, University of Amsterdam.
  * **Strategic Advisors & Partners from the Fetch.ai (ASI Alliance) team.**

-----

## 13. Competitive Analysis

| Parameter | **Membria (Our Project)** | **Asimov Protocol** | **OriginTrail** |
| :--- | :--- | :--- | :--- |
| **Primary Goal**| Augment local LLMs with verified knowledge | Enable AI-to-AI communication | Verify real-world asset data |
| **Source of Truth** | Human/Gateway consensus on knowledge | Emergent truth from AI dialogue | Verifiable data from real-world sources |
| **Analogy** | **"Wikipedia for AI"** | **"The UN for AI"** | **"Decentralized Notary for Assets"** |

-----

## 14. DAO Governance Model

Membria will be governed by a DAO with a hybrid structure, evolving toward full decentralization. Staked `$ACTI` will have a 2x voting power multiplier. The DAO will control key economic and network parameters via a formal Membria Improvement Proposal (MIP) process.

-----

## 15. Risk Analysis and Mitigation

| Category | Risk | Mitigation Strategy |
| :--- | :--- | :--- |
| **Technical** | Bias or exploitation of the Scorer LLM. | Academic partnerships (IISC), open testing, DAO governance over model versions. |
| **Economic** | Low network activity post-subsidy phase. | Network effect of the KCG, developer grants to build dApps that create demand. |
| **Ecosystem** | "Cold start" failure to attract Gateways and Creators. | Contributor Contest, key partnerships, clear ROI for operators. |
| **Regulatory** | Unclear legal status of tokens. | Legal consultation, focus on the clear utility of the tokens within the ecosystem. |

-----

## 16. Conclusion: A Sustainable Knowledge Economy

The proposed tokenomics create a self-sustaining, closed-loop system. Users pay for the creation of real value. These payments incentivize operators to maintain a high-quality, secure infrastructure, while simultaneously reducing the total token supply, which contributes to long-term value accrual. It is a sustainable model designed for the growth and prosperity of a decentralized "Wikipedia for AI."

-----

## 17. TGE Roadmap

1. Private round (SAFT/KOL): $0.04, price depends on the amount of the investment check
- Terms: 20% unlock on TGE, 5 month cliff period, then 12 months vesting with linear monthly unlock of the balance.
- Dates: [01/09/2025 – 10/11/2025] (Partially Fulfilled. Paused. Remaining allocation transferred to VC round)
- Raise: **$300,000**
- Participants: SAFT Investors and KOL's.

2. Seed round (VC), $0.05
- Terms: 20% unlock on TGE, 5 month cliff period, then 18 months vesting with linear monthly unlock of the balance.
- Date: Starts at [01/10/2025] (Planned to reach in early January 2025)
- Raise: **$500,000**
- Participants: Private investors, VC’s.

3. Public round (IDO), $0.07
- Terms: 25% unlock on TGE, 3 month cliff period, then 12 months vesting with linear monthly unlocking of the balance.
- Date: Starts at [15/01/2026]
- Raise: **$1,000,000**
- Participants: Launchpads

4. Listing on exchanges: $0.07
- Listing start date: [20/01/26]
- Initial market capitalization: **$450,000**
- Exchanges: Mexc=>Gate=>HTX=>Сrypto.com

-----

## 18. Token metrics:

- [Tokenomics and Vesting](https://t.ly/at-yI)

-----

## 19. Available $ACTI allocations for sale

- KOL/SAFT round: $150K, min check $50K, price $0,04 (Cliff 5m, Vesting 12m, TGE unlock 20%)
- Private (VC) round: $500K, min check $20K, price $0,05 (Cliff 5m, Vesting 18m, TGE unlock 15%)

-----

[**Link to SAFT**](https://docs.google.com/document/d/1DE6JaA7tzphjvPbdHjHOFraa63-rKg1QPaqLeLEyqgU/edit?tab=t.0)

-----
