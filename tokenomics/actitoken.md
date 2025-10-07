# Membria Community Edition: Tokenomics v2.0

## 1. Introduction

### 1.1. Mission and Vision

Membria's mission is to build a decentralized and permanent knowledge base - a "Wikipedia for Small Language Models" (SLMs) — that elevates any local AI to GPT-4 level intelligence. Our platform enables users to run Hugging Face models on-device, build autonomous agents to automate complex workflows, and instantly augment their models with new skills through our "SkillForge" technology. This provides a hyper-personalized AI experience, underpinned by a sustainable token economy that incentivizes the creation of high-quality knowledge, rewards network participants, and ensures long-term value growth of the entire ecosystem.

### 1.2. Key Ecosystem Participants

* **Users / Knowledge Creators**: Initiators of requests to create new knowledge (DoD), and the ultimate consumers and primary creators of value.
* **Gateways**: Operators of high-performance nodes that validate, process, cache, and commit knowledge to the network.
* **Validators**: Participants who secure the Peaq blockchain, upon which Membria operates, by participating in its consensus mechanism.

### 1.3. Token Overview

The economy utilizes a hybrid model with two core assets:

1. **$ACTI (The Core Token)**: A deflationary utility token used for staking, governance, and rewarding network participants. **$ACTI is tradable on the open market.**
2. **$kCREDIT (Knowledge Credit)**: A non-transferable, non-tradable "knowledge credit" used to participate in the initial bootstrapping program. **$kCREDIT is not tradable.**

---

## 2. Core Architecture and Ecosystem

### 2.1. The Membria Client: A Personal AI Hub

The **Membria Client** transforms a user's device into a powerful, personalized AI hub:

* **Load and run** various Small Language Models (SLMs) from Hugging Face
* **Manage model "skills"** through **SkillForge** (a LoRA patch manager)
* **Deploy autonomous agents** for complex tasks
* **Store knowledge locally and privately** in SQLite with vector search support

When local knowledge is insufficient, the Client seamlessly connects to the decentralized Membria network via Gateways, enriching its local database with verified knowledge from the global KCG.

### 2.2. The Value Creation Cycle

The primary economic event is the **Distillation-on-Demand (DoD) Request** - the process through which a new, verified unit of knowledge is created to populate the Knowledge Cache Graph (KCG).

### 2.3. Payment Mechanism: Dynamic Pricing

To protect the economy from volatility, DoD pricing is pegged to USD and dynamically converted to `$ACTI`:

* **Target Price**: $0.10 per DoD request (set by DAO based on Gateway operational costs)
* **Dynamic Conversion**: `Fee_in_ACTI = $0.10 / Current_ACTI_Price`
* **Price Stability Mechanisms**:
  - 24-hour TWAP (time-weighted average price) from oracles
  - Price ceiling: $0.15 maximum (protection from volatility spikes)
  - Price floor: $0.05 minimum (protection for Gateway revenue)

### 2.4. Fee Distribution (Updated Model)

Every DoD payment in `$ACTI` is automatically distributed via smart contract:

```
100% Payment ($0.10 in $ACTI)
├─ 25% → Burn (deflationary pressure)
├─ 60% → Gateway operator (direct commission)
├─ 10% → Consensus quorum (4-5 Gateway validators)
└─ 5% → Ecosystem fund (long-term development)
```

**Critical Note**: Team-owned Gateway nodes (50% of network) do NOT receive commissions. Their allocation is redistributed proportionally among independent operators, significantly increasing their profitability.

### 2.5. The Network Accumulation Effect

While the price of a single DoD request remains stable at $0.10, the **average cost for users trends toward zero over time** as the KCG grows. Higher cache hit rates (target: 85%) mean most queries are served free from cache.

---

## 3. Deflationary Model v2.0

### 3.1. Burn Mechanics

* **Primary Burn**: 25% of every DoD transaction fee (reduced from 50% to ensure Gateway profitability)
* **Secondary Burn**: Slashing penalties from malicious Gateway operators
* **Burn Rate at Scale**:
  - 10,000 users: ~$675,000/year → 16.9M tokens/year @ $0.04 (3.4% supply)
  - 50,000 users: ~$3.375M/year → 84M tokens/year @ $0.04 (16.8% supply)

### 3.2. Supply Dynamics

* **Phase 1 (0-24 months)**: Moderate inflation due to vesting schedules, offset by burn
* **Phase 2 (24+ months)**: Pure deflation as vesting ends and burn continues
* **Long-term**: Sustainable deflationary pressure without Gateway profitability compromise

---

## 4. Gateway Economics v2.0

### 4.1. Requirements for Independent Operators

| Requirement | Specification |
|-------------|--------------|
| **Minimum Stake** | $100,000 in $ACTI |
| **KYC/KYB** | Mandatory (legal entity or DID verification) |
| **Technical Audit** | 30-day testnet operation with uptime monitoring |
| **DAO Approval** | 66% vote from existing Gateway operators + token holders |
| **Slashing Reserve** | $20,000 (first 90 days probation period) |
| **Geographic Distribution** | Network requires minimum 3 continents coverage |

### 4.2. Revenue Streams

**At 10,000 users (2,250,000 paid DoD/month across network):**

| Revenue Source | Calculation | Monthly | Annual |
|----------------|-------------|---------|--------|
| **Direct Commissions** | 60% of fees ÷ 8 independent Gateway | $16,875 | $202,500 |
| **Consensus Rewards** | 10% of fees, proportional to participation | $2,800 | $33,600 |
| **Staking APR** | 8% on $100K stake | $667 | $8,000 |
| **Total Revenue** | | **$20,342** | **$244,100** |
| **Operating Costs** | Infrastructure + LLM API + blockchain fees | $10,000 | $120,000 |
| **Net Profit** | | **$10,342** | **$124,100** |

**ROI: 124% annually**

### 4.3. Operating Cost Breakdown (per Gateway/month)

| Category | Specification | Cost |
|----------|--------------|------|
| **Server Infrastructure** | 32-64 vCPU, 128GB RAM, 2TB NVMe SSD | $800-1,200 |
| **GPU Acceleration** | T4/A10 for embedding generation | $500-800 |
| **Storage** | 4TB high-speed SSD for cache | $200 |
| **CDN/Edge** | Global access optimization | $300 |
| **LLM API Costs** | OpenRouter (GPT-4o-mini, Claude Sonnet) | $5,100 |
| **Blockchain Fees** | Peaq transactions + Arweave storage | $35 |
| **Monitoring/Security** | Datadog, Cloudflare Enterprise, DDoS protection | $300 |
| **DevOps Support** | 0.2 FTE engineering time | $1,600 |
| **Contingency** | Incident response reserve | $200 |
| **Total Monthly OPEX** | | **~$10,000** |

### 4.4. Progressive Decentralization Schedule

| Phase | Period | Team Gateway | Independent Gateway | Governance |
|-------|--------|-------------|---------------------|------------|
| **Alpha** | Q1-Q2 2025 | 10 nodes (100%) | 0 nodes | Team |
| **Beta** | Q3-Q4 2025 | 12 nodes (80%) | 3 nodes (20%) | Hybrid |
| **Launch** | Q1-Q2 2026 | 8 nodes (50%) | 8 nodes (50%) | DAO vote |
| **Growth** | Q3-Q4 2026 | 6 nodes (40%) | 9 nodes (60%) | Full DAO |
| **Mature** | 2027+ | 5 nodes (30%) | 12 nodes (70%) | Full DAO |

**Key Principle**: Team never owns >50% of Gateway nodes, ensuring decentralization while maintaining quality control during early phases.

---

## 5. Security and Anti-Attack Mechanisms

### 5.1. Anti-Spam System

**Tiered Access Model:**

| Tier | Stake Required | DoD/day | Cache Queries | Priority | Price Multiplier |
|------|----------------|---------|---------------|----------|------------------|
| **Free** | $0 | 5 | 50 | Low | 1.5x |
| **Basic** | $50 in $ACTI | 20 | 200 | Normal | 1.0x |
| **Pro** | $500 in $ACTI | 100 | Unlimited | High | 0.8x |
| **Enterprise** | $5,000 in $ACTI | 1,000 | Unlimited | Premium | 0.6x |

**Dynamic Pricing Formula:**
```
Final_Price = $0.10 × Complexity_Mult × Network_Load_Mult × Reputation_Mult

Where:
- Complexity_Mult: 0.5x - 3x (based on request token count)
- Network_Load_Mult: 1x - 2x (current network congestion)
- Reputation_Mult: 0.6x - 1.5x (user's historical behavior)
```

### 5.2. Anti-Sybil Protection for Gateway

**Multi-Stage Verification:**

1. **Whitelist Application**
   - KYC/KYB verification (legal entity required)
   - Technical infrastructure audit
   - 30-day testnet operation with 99.5% uptime requirement
   - Stake $100K + $20K slashing reserve

2. **DAO Voting Period (30 days)**
   - Existing Gateway operators vote (weighted by reputation)
   - Token holders vote (weighted by staked amount)
   - Requires 66% approval to pass

3. **Probation Period (90 days)**
   - Reduced rewards (50% of standard rate)
   - Enhanced monitoring and random audits
   - $20K slashing risk for misbehavior
   - Quarterly performance review

4. **Full Operator Status**
   - 100% rewards unlocked
   - Standard slashing reduced to $5K
   - Full participation in consensus quorums

### 5.3. Consensus Integrity Protection

**Heterogeneous Quorum System:**

For each DoD validation, a 5-Gateway quorum is assembled:
```
Quorum Composition:
├─ 2 Random independent Gateway operators
├─ 2 Team Gateway nodes (mandatory for quality control)
└─ 1 "Elder" Gateway (top-3 by reputation score)

Approval Threshold:
- Requires 4/5 votes OR
- Both Team Gateway + 1 independent + 1 elder
```

**Reputation Scoring:**
- Uptime: 30% weight
- Validation accuracy: 40% weight (measured via spot checks)
- Response latency: 15% weight
- Community challenges won: 15% weight

### 5.4. Knowledge Challenge System

Any stakeholder can dispute knowledge quality:

```python
Challenge Process:
1. Challenger stakes $500 in $ACTI (anti-spam bond)
2. Extended quorum (9 Gateway) re-validates the knowledge
3. If challenger is correct:
   - Receives $1,000 reward
   - Original quorum members slashed $5K each
   - Knowledge marked as invalid/outdated
4. If challenger is wrong:
   - Loses $500 stake
   - Original validation stands
```

**Temporal Verification:**
All knowledge entries have expiration dates:
- Factual claims: 6 months
- Technical documentation: 12 months
- Opinion/philosophy: Permanent

Upon expiration, automatic re-validation by fresh quorum ensures knowledge stays current.

---

## 6. Daily Knowledge Contributor Contest

### 6.1. Objective

Solve the "cold start" problem by incentivizing early users to create valuable, complex, and reusable knowledge entries.

### 6.2. Dynamic Prize Pool

**Funding**: 50% of Ecosystem Fund = 125M tokens over 4 years

| Phase | Active Users | Daily Prize | Monthly | Annual | Token Cost @ $0.04 |
|-------|--------------|-------------|---------|--------|--------------------|
| **Bootstrap** | 100-500 | $1,000 | $30K | $360K | 9M tokens/year |
| **Growth** | 500-2,000 | $2,500 | $75K | $900K | 22.5M tokens/year |
| **Scale** | 2,000-10,000 | $5,000 | $150K | $1.8M | 45M tokens/year |
| **Mature** | 10,000+ | $2,000 | $60K | $720K | 18M tokens/year |

**Rationale**: Prize pool scales with network activity but tapers at maturity when the network becomes self-sustaining through organic incentives.

### 6.3. Value Scoring Algorithm

```python
def calculate_knowledge_value_score(dod_request, answer):
    score = 0
    
    # Novelty (30% weight)
    if not exists_in_cache(dod_request):
        score += 30
    
    # Complexity (25% weight)
    reasoning_depth = measure_reasoning_steps(answer)
    score += min(reasoning_depth * 5, 25)
    
    # Reusability potential (20% weight)
    semantic_generality = measure_abstraction_level(answer)
    score += semantic_generality * 20
    
    # Factual density (15% weight)
    citations_count = count_verifiable_claims(answer)
    score += min(citations_count * 3, 15)
    
    # Consensus quality (10% weight)
    if consensus_score >= 0.95:
        score += 10
    elif consensus_score >= 0.80:
        score += 5
    
    return min(score, 100)
```

**Prize Distribution**:
- Top 10 contributors: 60% of daily pool (split proportionally by score)
- Top 11-50 contributors: 30% of daily pool
- Random lottery (all participants): 10% of daily pool

---

## 7. Token Distribution & Vesting

**Total Supply: 500,000,000 $ACTI**

| Category | % | Token Amount | Vesting Schedule | Purpose |
|----------|---|--------------|------------------|---------|
| **Ecosystem Fund** | 50% | 250,000,000 | 40% at TGE (100M), 24-month linear vest | Contests, grants, liquidity bootstrapping |
| **Team Gateway Reserve** | 8% | 40,000,000 | Locked 36 months | Stake for 8-10 team-operated Gateway nodes |
| **Private Sale (1)** | 5% | 25,000,000 | 20% TGE, 18-month linear vest | SAFT/KOL round |
| **Private Sale (2)** | 3.33% | 16,666,667 | 10% TGE, 18-month linear vest | Strategic VC round |
| **Public Sale (IDO)** | 5% | 25,000,000 | 25% TGE, 3-month cliff, 12-month vest | Public launchpad |
| **Liquidity** | 5% | 25,000,000 | 5% TGE, 20-month linear vest | DEX/CEX liquidity |
| **Contributors** | 10% | 50,000,000 | 18-month cliff, 24-month linear vest | Core team |
| **Partnerships** | 10% | 50,000,000 | 18-month cliff, 18-month linear vest | Hugging Face, ASI, etc. |
| **Advisors** | 2.67% | 13,333,333 | 4% TGE, 5-month cliff, 18-month vest | Advisory board |
| **DAO Reserve** | 1% | 5,000,000 | 12-month lock, 24-month linear vest | Emergency governance fund |

**Key Changes from v1.0:**
- New allocation: **Team Gateway Reserve** (8%) to ensure team can operate quality control nodes
- Reduced DAO Reserve from 8.67% to 1% (reallocated to Gateway operations)
- More aggressive TGE unlock on Ecosystem Fund (40% vs 48%) for sustainable contest funding

---

## 8. Network Metrics & Projections

### 8.1. At 10,000 Users (Target: Q2 2026)

**Monthly Activity:**
- Total queries: 15,000,000
- Cache hit rate: 85%
- Paid DoD requests: 2,250,000
- Total revenue: $225,000/month

## At 10,000 Users (Target: Q2 2026)

**Monthly Activity:**
- Total queries: 15,000,000
- Cache hit rate: 85%
- Paid DoD requests: 2,250,000
- Total revenue: **$225,000/month**

**Token Flows:**

| Flow | Amount/month | Amount/year |
|------|--------------|-------------|
| **Burn (25%)** | $56,250 | $675,000 |
| **Independent Gateway (8 nodes)** | $135,000 | $1,620,000 |
| **Consensus rewards (10%)** | $22,500 | $270,000 |
| **Ecosystem fund (5%)** | $11,250 | $135,000 |
| **TOTAL** | $225,000 | $2,700,000 |

---

**Burn Impact** (at $0.04/token):
- 16,875,000 tokens burned/year
- 3.4% of total supply annually
- Cumulative 5-year burn: ~15% of supply (assuming stable usage)

### 8.2. At 50,000 Users (Target: 2027)

**Monthly Activity:**
- Paid DoD requests: 11,250,000
- Total revenue: $1,125,000/month

**Independent Gateway Economics** (12 nodes by this phase):
- Average revenue per Gateway: $56,000/month
- Average OPEX: $10,000/month
- **Net profit: $46,000/month = $552,000/year**
- **ROI: 552% annually**

**Burn Impact**:
- $3,375,000/year → 84M tokens @ $0.04
- 16.8% of supply annually
- Strong deflationary spiral supporting token price appreciation

---

## 9. Roadmap

### Q3 2025: Foundation
- Tokenomics v2.0 finalized
- Gateway infrastructure setup (10 team nodes)
- Completing private sale 
- Testnet launch with 100 whitelist users

### Q4 2025: TGE & Launch
- Token Generation Event via launchpad
- Mainnet alpha launch
- Daily Contest begins ($1K/day pool)
- Scale to 2,000 users
- 5 independent Gateway operational
- ASI Alliance integration

### Q1 2026: Beta Testing
- Security audits (smart contracts, Gateway infrastructure)
- Closed beta: 500 users
- Measure real cache hit rate and adjust pricing if needed
- First 2 independent Gateway onboarded

### Q2 2026: Growth Phase
- Target: 10,000 active users
- 8 independent Gateway (50/50 with team)
- Public API release
- Joint hackathons with Hugging Face
- Daily Contest scales to $5K/day peak
- DAO governance launch

### Q3-Q4 2026: Expansion
- Scale to 20,000+ users
- 9 independent Gateway (60% of network)
- Enterprise partnerships
- Multi-language support

### 2027+: Maturity & Full Decentralization
- 50,000+ users target
- 70% independent Gateway operators (12+ nodes)
- Contest tapering to $2K/day (network self-sustaining)
- Cross-chain bridges (Ethereum, Solana)
- Full DAO control of all parameters

---

## 10. Go-to-Market Strategy

### 10.1. Strategic Partnerships

**Hugging Face Integration:**
- Co-marketing: Membria as "the knowledge layer" for HF models
- Technical integration: One-click setup from HF model pages
- Joint developer grants program

**ASI Alliance (Fetch.ai):**
- Agent economy synergy: Membria provides verified knowledge for autonomous agents
- Cross-token utility: $FET holders get discounts on DoD requests
- Shared developer ecosystem

**Academic Partnerships:**
- IISC (Indian Institute of Science): AI safety research, Scorer LLM validation
- University partnerships: Student competitions for knowledge contribution

### 10.2. Target Markets

**Q3 Focus: Enterprise + Edge (Membria EE)**
- Industries: Automotive, Finance, Healthcare, Telecoms
- Pilot program with 6 enterprise clients
- Custom ontology development for domain-specific knowledge

**Q4 Focus: Consumer + Edge (Membria CE)**
- Marketing: "Perplexity on your laptop"
- Distribution: Bundle with AI hardware (Jetson, NPU laptops)
- Community: Reddit, Twitter, AI Discord communities

---

## 11. **Membria's Moat:**
1. Only solution offering **verified, permanent knowledge** for edge AI
2. Economic incentives align users, operators, and knowledge quality
3. Hybrid edge/cloud architecture balances privacy and intelligence
4. Open ecosystem (any LLM) vs. proprietary walled gardens

---

## 12. Risk Analysis & Mitigation

### 12.1. Technical Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Cache hit rate < 80%** | Medium | High | 6-month beta testing to measure real CHR; adjust pricing to $0.12 if needed |
| **Scorer LLM bias/exploitation** | Medium | Medium | Academic partnerships (IISC), open model testing, DAO-controlled versioning |
| **Arweave economics collapse** | Low | High | Hybrid storage: fallback to IPFS/Filecoin, maintain last 12 months on Gateway local storage |

### 12.2. Economic Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Low post-subsidy activity** | Medium | High | Network effect of KCG, developer grants for dApps, enterprise partnerships |
| **Token price volatility** | High | Medium | USD-pegged pricing with TWAP, price floor/ceiling mechanisms |
| **Gateway centralization** | Low | Medium | Progressive decentralization schedule, hard cap on team ownership (≤50%) |

### 12.3. Regulatory Risks

| Risk | Probability | Impact | Mitigation |
|------|-------------|--------|------------|
| **Token classification uncertainty** | Medium | High | Legal consultation in key jurisdictions, focus on clear utility (not security) |
| **Data privacy regulations (GDPR)** | Low | Medium | 100% local processing, optional cloud via Gateway with user consent |
| **AI regulation (EU AI Act)** | Medium | Low | Transparent consensus mechanism, human-in-loop via challenges, audit trails |

---

## 13. Team & Governance

### 13.1. Core Team

* **Michael Aprossine** ([LinkedIn](https://linkedin.com/in/miguel2020)) – CEO, 2 exits, IoT, AI domains
* **Mike Keer** ([LinkedIn](https://linkedin.com/in/mikhail-kiriukhin-97389957)) – CTO, CV/AI architect (EU EIC projects)
* **Phillippe Khomenok** ([LinkedIn](https://linkedin.com/in/gsarskyes)) – COO, $10M ARR operations experience
* **Ankit Sahu** ([LinkedIn](https://linkedin.com/in/ansahu)) – CFO, 20 years at Bank of America/UBS Asset Management

### 13.2. Scientific Advisory Board

* **Dr. Ty Vachon, MD** ([LinkedIn](https://linkedin.com/in/tyvachon)) – Sports Medicine Radiologist, former DoD Innovation
* **Leonard Khiroug, PhD** ([LinkedIn](https://linkedin.com/in/leonardkhiroug)) – Neuroscience, University of Amsterdam
* **Vencatesh Babu, PhD** ([LinkedIn](https://www.linkedin.com/in/venkatesh-babu-radhakrishnan-4a8816235)) – AI, Indian Institure of Science, Bangalor

### 13.3. Strategic Partners

* Fetch.ai / ASI Alliance team (advisors on agent economy integration)
* Peaq Network (technical partnership for blockchain infrastructure)
* Arweave Foundation (permanent storage layer)

### 13.4. DAO Governance Model

**Governance Token**: Staked $ACTI with 2x voting power multiplier

**Governance Scope**:
- Economic parameters (DoD pricing, burn rate, staking APR)
- Gateway admission/removal votes
- Ecosystem fund allocation
- Protocol upgrades (via Membria Improvement Proposals - MIPs)
- Emergency actions (pause, upgrade, parameter changes)

**Voting Mechanism**:
```
Voting Power = Staked_ACTI × 2.0 × Time_Weight

Where Time_Weight:
- < 3 months: 0.5x
- 3-6 months: 1.0x
- 6-12 months: 1.5x
- > 12 months: 2.0x
```

**Proposal Process**:
1. Draft MIP posted on governance forum (7-day discussion)
2. Formal submission (requires 10K $ACTI bond, refunded if passed)
3. Voting period (14 days)
4. Execution delay (48 hours timelock)
5. Implementation by core team or community developers

---

## 14. TGE Details

### 14.1. Fundraising Rounds

**1. Private Round (SAFT/KOL) - COMPLETED**
- Price: $0.02
- Terms: 20% TGE unlock, 5-month cliff, 12-month linear vesting
- Dates: September 2024 - November 2025
- Raised: $150,000
- Participants: Strategic angels

**2. Seed Round (VC) - IN PROGRESS**
- Price: $0.05
- Terms: 20% TGE unlock, 5-month cliff, 18-month linear vesting
- Target date: January 2026
- Target raise: $500,000
- Participants: VCs and institutional investors
- **Currently Available**: $500K allocation, minimum check $20K

**3. Public Round (IDO)**
- Price: $0.07
- Terms: 25% TGE unlock, 3-month cliff, 12-month linear vesting
- Date: January 15, 2026
- Target raise: $1,000,000
- Platform: TBD launchpad (Polkastarter, Seedify, or DAO Maker)

**4. Exchange Listings**
- Listing price: $0.07
- Date: January 20, 2026
- Initial market cap: ~$450,000 (circulating supply at TGE)
- Target exchanges: Binance Alpha → Gate.io → HTX → Crypto.com

### 14.2. Token Metrics Summary

- **Total Supply**: 500,000,000 $ACTI
- **Initial Circulating Supply** (TGE): ~6.4M tokens (1.3% of total)
- **Fully Diluted Valuation** (FDV) at $0.07: $35,000,000
- **Initial Market Cap**: $450,000

**Circulating Supply Schedule:**
- Month 0 (TGE): 6.4M (1.3%)
- Month 6: 89M (17.8%)
- Month 12: 143M (28.6%)
- Month 24: 247M (49.4%)
- Month 42: 500M (100%)

---

## 15. Financial Projections

### 15.1. Revenue Model

**Assumptions:**
- DoD price: $0.10 (fixed in USD)
- Cache hit rate: 85% (to be validated in beta)
- User query frequency: 50/day
- Paid DoD rate: 15% of all queries

**Year 1 (2026):**
- Average users: 5,000
- Monthly revenue: ~$112,500
- Annual revenue: $1,350,000
- Token burn: $337,500/year (8.4M tokens @ $0.04)

**Year 2 (2027):**
- Average users: 25,000
- Monthly revenue: ~$562,500
- Annual revenue: $6,750,000
- Token burn: $1,687,500/year (42M tokens @ $0.04)

**Year 3 (2028):**
- Average users: 75,000
- Monthly revenue: ~$1,687,500
- Annual revenue: $20,250,000
- Token burn: $5,062,500/year (126M tokens @ $0.04)

### 15.2. Gateway Network Economics

**Year 1 (8 independent Gateway):**
- Network OPEX: $960K (8 × $10K/month × 12 months)
- Network revenue: $1,012,500 (75% of $1.35M)
- Net profit per Gateway: ~$6,600/month
- Network-wide ROI: 6.6%

**Year 2 (12 independent Gateway):**
- Network OPEX: $1,440K
- Network revenue: $5,062,500 (75% of $6.75M)
- Net profit per Gateway: ~$25,000/month
- Network-wide ROI: 253%

**Year 3 (15 independent Gateway):**
- Network OPEX: $1,800K
- Network revenue: $15,187,500 (75% of $20.25M)
- Net profit per Gateway: ~$74,900/month
- Network-wide ROI: 899%

---

## 16. Conclusion

Membria's updated tokenomics v2.0 creates a **sustainable, economically viable ecosystem** that solves the critical flaws of v1.0:

**Key Improvements:**
- Gateway operators achieve positive ROI (124% vs -30%)
- Team maintains quality control through 50% Gateway ownership
- Burn rate balanced at 25% (sustainable deflation without killing profitability)
- Comprehensive anti-attack mechanisms (KYC, rate limiting, heterogeneous consensus)
- Contest funding sustainable over 4-year bootstrap period
- Clear path to decentralization with hard ownership caps

**Critical Success Factors:**
1. **Beta validation of cache hit rate** - must achieve ≥80% CHR to validate pricing
2. **First 5 independent Gateway onboarding** - prove operational model works
3. **Enterprise pilot success** - demonstrate value for custom ontology use cases
4. **Community contest traction** - achieve 500 active contributors by Q4 2025

**Investment Thesis:**
Membria is building the **infrastructure layer for the edge AI economy**. As AI moves from cloud to device (driven by privacy, cost, and latency concerns), there will be an exponential need for verified, permanent knowledge that can update local models in real-time. Membria's decentralized Knowledge Cache Graph, secured by economic incentives and cryptographic proofs, is positioned to become the

**Investment Thesis (continued):**
Membria is building the **infrastructure layer for the edge AI economy**. As AI moves from cloud to device (driven by privacy, cost, and latency concerns), there will be an exponential need for verified, permanent knowledge that can update local models in real-time. Membria's decentralized Knowledge Cache Graph, secured by economic incentives and cryptographic proofs, is positioned to become the **de facto standard for edge AI knowledge infrastructure**.

**Comparable Market Opportunity:**
- Vector database market: $2.1B by 2028 (Pinecone valued at $750M)
- Enterprise AI search: $4.5B by 2027 (Glean valued at $2.3B)
- **Membria TAM: $8B+ (edge AI + enterprise knowledge + consumer AI assistants)**

**Token Value Accrual Mechanisms:**
1. **Burn deflationary pressure**: 3.4% supply/year at 10K users → 16.8% at 50K users
2. **Staking demand**: Gateway operators lock $100K each (15 operators = $1.5M+ locked)
3. **Utility demand**: Users must hold/spend $ACTI to access network (pay-per-use model)
4. **Network effects**: Each new knowledge entry increases value of entire graph

**Risk-Adjusted Return Profile:**
- **Bear case** (CHR = 70%, slow adoption): $0.04 → $0.10 (2.5x over 3 years)
- **Base case** (CHR = 85%, 10K users by 2026): $0.04 → $0.25 (6.25x over 2 years)
- **Bull case** (CHR = 90%, 50K+ users, enterprise adoption): $0.04 → $1.00+ (25x over 3 years)

---

## 17. Investment Opportunities

### 17.1. Current Round: Seed (VC)

**Available Allocation**: $500,000
- **Price**: $0.05 per $ACTI
- **Tokens**: 10,000,000 $ACTI (2% of total supply)
- **Minimum check**: $20,000
- **Vesting**: 20% at TGE, 5-month cliff, 18-month linear unlock
- **Target close**: November 2025

**Investor Benefits:**
- 25% discount vs. public sale price ($0.05 vs $0.07)
- Early access to Membria Enterprise pilot program
- Priority Gateway operator licensing (if qualified)
- Quarterly advisory board participation
- Co-marketing opportunities for Web3 VCs

**Use of Funds:**
- 40% - Gateway infrastructure deployment (10 nodes for 6 months)
- 30% - Team expansion (3 engineers, 1 BD, 1 community manager)
- 20% - Marketing & community building (KOL partnerships, hackathons)
- 10% - Legal & compliance (token legal opinion, entity setup)

### 17.2. Contact & Due Diligence

**Investment Inquiries:**
- Email: hello@membria.xyz
- Telegram: @membria_bd
- Calendar: [Book DD call](https://calendly.com/actiq)

**Due Diligence Materials:**
- Full tokenomics v2.0 (this document)
- Technical architecture whitepaper
- Financial model (Excel with scenarios)
- Legal opinion on token classification
- Team backgrounds & LinkedIn verification
- Smart contract audit reports (available Q1 2026)

---

## 18. Appendix A: Glossary

**DoD (Distillation-on-Demand)**: The process of creating a new, verified knowledge entry by querying a teacher LLM and validating the result through Gateway consensus.

**KCG (Knowledge Cache Graph)**: The decentralized, permanent graph database of verified knowledge stored on Peaq (index) and Arweave (data).

**Gateway**: A high-performance node that routes queries, validates knowledge, maintains cache, and commits transactions to the blockchain.

**SCR (Selective Context Retrieval)**: The pipeline for efficiently retrieving relevant knowledge from the KCG to augment local LLM prompts.

**SkillForge**: Membria's LoRA patch management system that allows instant fine-tuning of local models without gradient-based training.

**CHR (Cache Hit Rate)**: The percentage of user queries that can be answered from cached knowledge without requiring a paid DoD request.

**Quorum**: A group of 5 Gateway operators who collectively validate the quality of a knowledge entry before it's committed to the permanent graph.

**Slashing**: The penalty mechanism where misbehaving Gateway operators lose a portion of their staked $ACTI.

---

## 19. Appendix B: Technical FAQ

**Q: How does Membria differ from RAG (Retrieval-Augmented Generation)?**

A: Traditional RAG retrieves from static documents. Membria's KCG is a live, verified, and constantly-updated knowledge graph with consensus validation. It's "RAG + Wikipedia + Blockchain."

**Q: What prevents Gateway operators from colluding to approve fake knowledge?**

A: Three mechanisms: (1) Heterogeneous quorums always include team-operated Gateway, (2) Economic slashing penalties ($5K per bad validation), (3) Open challenge system where anyone can dispute knowledge and earn rewards.

**Q: Can users trust that their data stays private?**

A: Yes. All inference happens locally on the user's device. Only when the local model can't answer does it request knowledge from the network—and even then, only the *query* is sent (not user documents). The answer comes back and is cached locally.

**Q: What happens if Arweave fails or becomes too expensive?**

A: Membria has a hybrid storage strategy. Recent knowledge (last 12 months) is also stored on Gateway local storage. If Arweave economics break, the DAO can vote to migrate to IPFS/Filecoin while maintaining the Peaq index layer.

**Q: How do you ensure the Scorer LLM isn't biased toward certain types of knowledge?**

A: The Scorer model is open-source, version-controlled, and selected by DAO vote. Academic partners (IISC) audit the scoring algorithm quarterly. The community can challenge scores via the dispute mechanism.

**Q: What's the minimum hardware to run a Membria client?**

A: Very modest: Any laptop with 8GB RAM can run a 3B parameter model. For best experience: 16GB RAM + GPU (even integrated) allows 7B models. The heavy lifting (teacher LLM queries) happens on Gateways, not user devices.

---

## 20. Appendix C: Comparison to v1.0 Tokenomics

| Parameter | v1.0 (Rejected) | v2.0 (Current) | Impact |
|-----------|-----------------|----------------|--------|
| **Burn Rate** | 50% | 25% | Gateway operators now profitable |
| **Gateway Revenue Share** | 50% | 75% (60% direct + 10% consensus + 5% ecosystem) | Massive ROI improvement |
| **Team Gateway Ownership** | 0% | 50% (8 nodes) | Quality control + cost efficiency |
| **Gateway ROI** | -30% (loss) | +124% (profit) | Attracts professional operators |
| **Anti-Spam** | None | Rate limiting + KYC + dynamic pricing | Prevents abuse |
| **Anti-Sybil** | Weak | Whitelist + DAO vote + probation | Prevents fake Gateway |
| **Consensus Model** | Unspecified | Heterogeneous quorum (team + independent + elder) | Prevents knowledge poisoning |
| **Contest Duration** | Unclear | 4 years with tapering | Financially sustainable |
| **Staking Rewards** | Unspecified | 8% APR | Covers Gateway CAPEX |
| **Price Stability** | None | TWAP + floor/ceiling | Protects from volatility |
| **Token Allocation** | No team Gateway fund | 8% Team Gateway Reserve | Enables 50% team ownership |

-----

## 21. Token metrics:

- [Tokenomics and Vesting](https://t.ly/at-yI)


[**Link to SAFT**](https://docs.google.com/document/d/1DE6JaA7tzphjvPbdHjHOFraa63-rKg1QPaqLeLEyqgU/edit?tab=t.0)

-----
