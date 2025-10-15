---
icon: project-roadmap
label: Roadmap
---

# Membria: Investment Presentation - Development Roadmap

## Executive Summary

**Mission**: Build the world's first decentralized, permanent knowledge base for AI - "Wikipedia for Small Language Models"

**Market Opportunity**: $50B+ AI infrastructure market (TAM)

**Timeline**: 10 months from start to mainnet launch

**Total Investment Required**: $610K

**Expected ROI**: Break-even at Month 18, profitable by Month 24

---

## High-Level Architecture

```mermaid
%%{init: {'theme':'base', 'themeVariables': { 'primaryColor':'#3498db','primaryTextColor':'#fff','primaryBorderColor':'#2980b9','lineColor':'#34495e','secondaryColor':'#2ecc71','tertiaryColor':'#e74c3c'}}}%%
graph LR
    subgraph Users["END USERS"]
        U1[Developers]
        U2[AI Startups]
        U3[Enterprises]
    end
    
    subgraph Client["MEMBRIA CLIENT<br/>Desktop & Mobile"]
        C1[AI Agents]
        C2[SkillForge]
        C3[Local Memory]
    end
    
    subgraph Network["DECENTRALIZED NETWORK"]
        N1[Gateway Nodes]
        N2[Knowledge Graph]
    end
    
    subgraph Market["MARKETPLACE"]
        M1[LoRA Patches]
        M2[AI Agents]
    end
    
    Users --> Client
    Client <--> Network
    Network <--> Market
    
    style Client fill:#3498db,stroke:#2980b9,stroke-width:3px,color:#fff
    style Network fill:#2ecc71,stroke:#27ae60,stroke-width:3px,color:#fff
    style Market fill:#e67e22,stroke:#d35400,stroke-width:3px,color:#fff
```

---

## Development Timeline

```mermaid
%%{init: {'theme':'base'}}%%
gantt
    title Membria 10-Month Roadmap to Revenue
    dateFormat YYYY-MM-DD
    axisFormat %b
    
    section Foundation
    M1 Local MVP           :done, m1, 2026-01-01, 12w
    Token Launch           :active, token, 2026-01-27, 4w
    
    section Product
    M2 Memory & Search     :m2, 2026-03-26, 4w
    M3 SkillForge          :m3, 2026-04-23, 6w
    
    section Network
    M4 Consensus           :m4, 2026-06-04, 4w
    M5 Token Economics     :m5, 2026-07-02, 4w
    
    section Launch
    M6 Mainnet             :crit, m6, 2026-07-30, 4w
    M7 Marketplace         :crit, m7, 2026-08-27, 8w
    
    section Milestones
    MVP Ready              :milestone, 2026-03-26, 0d
    Beta Launch            :milestone, 2026-06-04, 0d
    Mainnet Live           :milestone, 2026-08-27, 0d
    First Revenue          :milestone, 2026-10-22, 0d
```

---

## Milestone Flow

```mermaid
%%{init: {'theme':'base', 'themeVariables': {'fontSize':'16px'}}}%%
flowchart LR
    M1[M1: Local MVP<br/>12 weeks<br/>$90K]
    M2[M2: Memory<br/>4 weeks<br/>$30K]
    M3[M3: SkillForge<br/>6 weeks<br/>$60K]
    M4[M4: Consensus<br/>4 weeks<br/>$70K]
    M5[M5: Token Economics<br/>4 weeks<br/>$80K]
    M6[M6: Mainnet<br/>4 weeks<br/>$100K]
    M7[M7: Marketplace<br/>8 weeks<br/>$150K]
    
    TOKEN[Token Launch<br/>Week 4-8<br/>$30K]
    
    M1 --> M2
    M1 -.Parallel.-> TOKEN
    M2 --> M3
    M3 --> M4
    M4 --> M5
    TOKEN -.-> M5
    M5 --> M6
    M6 --> M7
    
    M7 --> REVENUE[Revenue Start<br/>$5-10K MRR]
    
    style M1 fill:#e74c3c,stroke:#c0392b,stroke-width:3px,color:#fff
    style M6 fill:#2ecc71,stroke:#27ae60,stroke-width:3px,color:#fff
    style M7 fill:#3498db,stroke:#2980b9,stroke-width:3px,color:#fff
    style TOKEN fill:#f39c12,stroke:#e67e22,stroke-width:2px,color:#fff
    style REVENUE fill:#27ae60,stroke:#229954,stroke-width:4px,color:#fff
```

---

## Investment Allocation

```mermaid
%%{init: {'theme':'base'}}%%
pie title Investment Allocation - $610K Total
    "Engineering (62%)" : 370
    "Security & Audits (11%)" : 65
    "Marketing (7%)" : 40
    "Infrastructure (7%)" : 40
    "Legal (4%)" : 25
    "Operations (5%)" : 30
    "Reserve (5%)" : 30
```

---

## Quarterly Investment Breakdown

| Quarter | Duration | Investment | Key Deliverables | End State |
|---------|----------|------------|------------------|-----------|
| **Q1: Foundation** | Month 1-3 | **$120K** | Local MVP complete<br/>Token launched on testnet<br/>Core infrastructure | Working prototype<br/>1,000+ community members<br/>100+ events in DKG |
| **Q2: Enhancement** | Month 4-6 | **$150K** | 3-tier memory system<br/>SkillForge operational<br/>Web automation agents | 100 active beta users<br/>10,000+ events<br/>Agent capabilities proven |
| **Q3: Network** | Month 7-9 | **$250K** | BFT consensus live<br/>Token economics deployed<br/>Mainnet launch | 1,000+ daily users<br/>50+ Gateway operators<br/>100,000+ events |
| **Q4: Revenue** | Month 10 | **$90K** | Marketplace launch<br/>20+ LoRA patches<br/>10+ AI agents | First revenue stream<br/>$5-10K MRR<br/>Path to profitability |

**Total**: $610K over 10 months

---

## Detailed Milestone Breakdown

### M1: Local MVP (Week 1-12) - Foundation Layer

| Week | Component | Core Features | Technical Stack | Success Criteria |
|------|-----------|--------------|-----------------|------------------|
| 1-2 | **Client Foundation** | CLI interface<br/>AI Core engine<br/>Configuration system | Python, Click, llama.cpp | Can run local LLM models<br/>Config loads correctly |
| 3-4 | **Local Knowledge Layer** | SQLite storage<br/>DuckDB analytics<br/>Document indexing | SQLite (WAL), DuckDB, HTTPFS | 100+ documents indexed<br/>Fast retrieval |
| 5-6 | **Basic Agent** | State machine<br/>Hot/Warm memory<br/>Tool framework | FSM, asyncio, JSON storage | Complete 3-step tasks<br/>Memory persists |
| 7-8 | **Gateway Core** | FastAPI server<br/>Request router<br/>LLM integration | FastAPI, httpx, OpenRouter | Query to answer flow works<br/>Sub-3s latency |
| 9-10 | **GraphRAG** | Semantic chunking<br/>Vector embeddings<br/>Graph search | NetworkX, transformers, pgvector | 80%+ search accuracy<br/>Sub-200ms queries |
| 11-12 | **Blockchain** | Peaq pallet<br/>Arweave upload<br/>Integration test | Rust, Substrate, Arweave SDK | Full end-to-end flow<br/>Data stored immutably |

**Budget**: $90K (2 backend devs + 1 blockchain dev × 3 months)

---

### M2: Enhanced Memory & Search (Week 13-16)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 13-14 | **Cold Memory** | DuckDB long-term archive<br/>Memory compression<br/>Semantic search over history | Search 10,000+ old conversations<br/>Sub-500ms query time |
| 15-16 | **Gateway Fast Path** | Redis hot cache<br/>PostgreSQL semantic index<br/>Query optimization | 70%+ cache hit rate<br/>Sub-100ms cached queries<br/>1,000+ events indexed |

**Budget**: $30K (3 devs × 1 month)

---

### M3: SkillForge & Advanced Orchestration (Week 17-22)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 17-18 | **SkillForge MVP** | LoRA patch loading<br/>Dynamic application<br/>Skill registry | Load .safetensors files<br/>Switch skills in under 5 seconds<br/>5+ test skills working |
| 19-20 | **Advanced Agent** | Multi-agent hierarchy<br/>Tool calling framework<br/>Idem-Prompt reliability | Parent spawns child agents<br/>95%+ tool call success<br/>Zero format errors |
| 21-22 | **Web Automation** | Playwright integration<br/>Search & browser tools<br/>Research agent | Navigate websites<br/>Extract clean content<br/>Multi-step research works |

**Budget**: $60K (4 devs × 1.5 months)

---

### M4: Consensus & Archive (Week 23-26)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 23-24 | **BFT Consensus** | Multi-validator setup<br/>Attestation voting<br/>Dispute resolution | 5+ validators running<br/>Zero forks observed<br/>Sub-30s finality |
| 25-26 | **Archive Engine** | Event processor<br/>Parquet batching<br/>HTTPFS queries | Auto-batch 1000 events/hour<br/>5:1+ compression<br/>Remote queries work |

**Budget**: $70K (4 devs + security auditor × 1 month)

---

### M5: Token Economics (Week 27-30)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 27-28 | **Staking System** | Gateway staking contract<br/>Reward distribution<br/>Slashing logic | 20+ operators staking<br/>500K+ ACTI locked<br/>Automated payouts |
| 29-30 | **Bridge & Marketplace** | Peaq to EVM bridge<br/>Marketplace backend API<br/>Payment processing | Test transfers successful<br/>API functional<br/>ACTI tradeable on DEX |

**Budget**: $80K (3 devs + legal + marketing × 1 month)

---

### M6: Mainnet Launch (Week 31-34)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 31-32 | **Production Infrastructure** | Multi-region deployment<br/>Load balancing<br/>Monitoring & alerts | 50+ Gateway nodes<br/>Sub-200ms global latency<br/>99.5%+ uptime |
| 33-34 | **Security & Launch** | Full security audit<br/>Bug fixes<br/>Public mainnet deployment | Zero critical issues<br/>Audit report published<br/>1,000+ users Week 1 |

**Budget**: $100K (5 devs + auditor + marketing × 1 month)

---

### M7: Marketplace Launch (Week 35-42)

| Week | Component | Core Features | Success Criteria |
|------|-----------|--------------|------------------|
| 35-38 | **LoRA Marketplace** | Web UI (React)<br/>Creator dashboard<br/>Payment & rating system | 20+ LoRA patches listed<br/>10+ creators onboarded<br/>End-to-end purchase flow |
| 39-42 | **Agent Marketplace** | Agent catalog<br/>One-click deployment<br/>Subscription system | 10+ agents available<br/>500+ subscriptions<br/>$5-10K MRR achieved |

**Budget**: $150K (5 devs + designer + BD × 2 months)

---

## Component Dependencies

```mermaid
%%{init: {'theme':'base'}}%%
graph TD
    subgraph Phase1["PHASE 1: Foundation (Week 1-12)"]
        A1[Client]
        A2[Gateway]
        A3[GraphRAG]
        A4[Blockchain]
    end
    
    subgraph Phase2["PHASE 2: Enhancement (Week 13-22)"]
        B1[Memory System]
        B2[SkillForge]
        B3[Web Agents]
    end
    
    subgraph Phase3["PHASE 3: Network (Week 23-34)"]
        C1[Consensus]
        C2[Token Economics]
        C3[Mainnet]
    end
    
    subgraph Phase4["PHASE 4: Revenue (Week 35-42)"]
        D1[Marketplace]
        D2[First Revenue]
    end
    
    Phase1 --> Phase2
    Phase2 --> Phase3
    Phase3 --> Phase4
    
    TOKEN[Token Launch<br/>Week 4-8] -.Parallel.-> Phase1
    TOKEN --> C2
    
    style Phase1 fill:#e8f5e9,stroke:#4caf50
    style Phase2 fill:#e3f2fd,stroke:#2196f3
    style Phase3 fill:#fff3e0,stroke:#ff9800
    style Phase4 fill:#f3e5f5,stroke:#9c27b0
    style TOKEN fill:#fff9c4,stroke:#fbc02d
```

---

## Technical Milestones

| Milestone | Target Week | Key Metrics | Impact |
|-----------|-------------|-------------|--------|
| **MVP Complete** | Week 12 | Working end-to-end flow<br/>100+ events in DKG<br/>1 demo user | Proves technical feasibility |
| **Beta Launch** | Week 22 | 100 active users<br/>10,000+ events<br/>Web agents operational | Validates product-market fit |
| **Consensus Live** | Week 26 | 5+ validators<br/>Zero forks (30 days)<br/>Preliminary audit passed | Achieves decentralization |
| **Mainnet Launch** | Week 34 | 1,000+ users<br/>100,000+ events<br/>50+ Gateway operators | Production ready |
| **First Revenue** | Week 42 | Marketplace live<br/>20+ LoRAs, 10+ agents<br/>$5-10K MRR | Path to profitability |

---

## Business Milestones

| Milestone | Target Week | Key Metrics | Strategic Value |
|-----------|-------------|-------------|-----------------|
| **Token Launch** | Week 8 | 500+ token holders<br/>1,000+ community members<br/>Testnet operational | Early community building |
| **Staking Active** | Week 30 | 20+ operators<br/>500K ACTI staked<br/>Rewards distributed | Network security |
| **Marketplace Open** | Week 38 | 20+ LoRA patches<br/>10+ agents<br/>100+ transactions | Revenue model proven |
| **Break-Even** | Month 18 | $40K MRR<br/>Positive monthly cash flow | Financial sustainability |

---

## Growth Projections

```mermaid
%%{init: {'theme':'base'}}%%
xychart-beta
    title "User Growth Projection (First 24 Months)"
    x-axis [M1, M3, M6, M9, M12, M15, M18, M21, M24]
    y-axis "Active Users" 0 --> 25000
    line [1, 100, 1000, 2500, 5000, 10000, 15000, 20000, 25000]
```

```mermaid
%%{init: {'theme':'base'}}%%
xychart-beta
    title "Revenue Projection (Monthly Recurring)"
    x-axis [M7, M9, M11, M13, M15, M18, M21, M24]
    y-axis "MRR ($K)" 0 --> 100
    line [5, 8, 15, 25, 35, 50, 70, 80]
```

---

## Financial Projections

### Revenue Model

| Revenue Stream | Launch Month | Year 1 | Year 2 | Year 3 |
|----------------|--------------|--------|--------|--------|
| **Marketplace Fees** (30% commission) | Month 11 | $50K | $250K | $800K |
| **Agent Subscriptions** | Month 11 | $30K | $200K | $600K |
| **Enterprise Licensing** | Month 14 | $20K | $150K | $500K |
| **Gateway Staking Fees** | Month 10 | $10K | $50K | $100K |
| **Total Annual Revenue** | | **$110K** | **$650K** | **$2M** |

### Path to Profitability

| Period | Investment | Cumulative Cost | Revenue | Cumulative Revenue | Net Position |
|--------|------------|-----------------|---------|-------------------|--------------|
| **Q1 (M1-3)** | $120K | $120K | $0 | $0 | -$120K |
| **Q2 (M4-6)** | $150K | $270K | $0 | $0 | -$270K |
| **Q3 (M7-9)** | $250K | $520K | $0 | $0 | -$520K |
| **Q4 (M10)** | $90K | $610K | $10K | $10K | -$600K |
| **Q5 (M11-12)** | $70K | $680K | $40K | $50K | -$630K |
| **Q6 (M13-15)** | $105K | $785K | $90K | $140K | -$645K |
| **Q7 (M16-18)** | $105K | $890K | $135K | $275K | -$615K |
| **Q8 (M19-21)** | $105K | $995K | $210K | $485K | -$510K |

**Break-Even**: Month 18  
**Full ROI**: Month 24-26  
**Expected Return**: 70x over 5 years

---

## Key Performance Indicators

### Technical KPIs

| Metric | M1 (Week 12) | M3 (Week 22) | M6 (Week 34) | M7 (Week 42) |
|--------|--------------|--------------|--------------|--------------|
| **Active Users** | 1 (demo) | 100 (beta) | 1,000 (mainnet) | 5,000 |
| **Events in DKG** | 100+ | 10,000+ | 100,000+ | 500,000+ |
| **Gateway Nodes** | 1 (dev) | 3 (test) | 50+ (prod) | 100+ |
| **Query Latency (cached)** | 3s | 1s | 100ms | 50ms |
| **Uptime** | 95% | 99% | 99.5% | 99.9% |

### Business KPIs

| Metric | M5 (Week 30) | M6 (Week 34) | M7 (Week 42) | Month 15 |
|--------|--------------|--------------|--------------|----------|
| **Token Holders** | 500+ | 2,000+ | 5,000+ | 10,000+ |
| **ACTI Staked** | 500K | 1M | 2M | 5M |
| **Marketplace Listings** | 0 | 0 | 30+ (20 LoRAs, 10 agents) | 80+ (50 LoRAs, 30 agents) |
| **Monthly Transactions** | 0 | 0 | 100+ | 1,000+ |
| **MRR** | $0 | $0 | $5-10K | $30K+ |

---

## Risk Assessment

| Risk | Probability | Impact | Mitigation Strategy | Reserve Budget |
|------|-------------|--------|---------------------|----------------|
| **Development Delays** | Medium | High | 20% time buffer built into schedule<br/>Phased delivery approach<br/>MVP-first methodology | $30K |
| **Security Vulnerabilities** | Low | Critical | 2-3 independent audits<br/>Bug bounty program ($50K pool)<br/>Gradual rollout with monitoring | $70K |
| **Low Market Adoption** | Medium | High | Seed marketplace with quality content<br/>Early adopter incentives<br/>Partnership with influencers | $15K |
| **Regulatory Issues** | Low | High | Early legal review<br/>Utility token structure<br/>KYC for marketplace creators | $15K |
| **Consensus Instability** | Medium | Critical | Extensive testnet period<br/>Fallback to federated model<br/>External security audit | $20K |
| **Key Person Dependency** | Low | High | Comprehensive documentation<br/>Code review processes<br/>Knowledge sharing protocols | - |

**Total Risk Reserve**: $150K (included in $610K total budget)

---

## Team Requirements

### Current Team
- Technical Co-founder (Full-stack + Blockchain)
- ML/AI Specialist (Architecture oversight)

### Hiring Plan

| Role | Start Month | Monthly Salary | Duration | Total Cost |
|------|-------------|----------------|----------|------------|
| **Senior Backend Developer** | Month 1 | $10K | 10 months | $100K |
| **Blockchain Developer** (Rust/Substrate) | Month 1 | $12K | 10 months | $120K |
| **ML Engineer** | Month 4 | $10K | 7 months | $70K |
| **DevOps Engineer** | Month 4 | $8K | 7 months | $56K |
| **Frontend Developer** | Month 8 | $8K | 3 months | $24K |
| **Community Manager** (Part-time) | Month 2 | $3K | 9 months | $27K |
| **Security Auditors** (Contract) | Month 7-8 | One-time | - | $50K |
| **Legal Counsel** (Contract) | Month 7 | One-time | - | $15K |

**Total Team Cost**: $462K  
**Remaining Budget**: $148K (infrastructure, marketing, operations, contingency)

---

## Market Opportunity

### Total Addressable Market (TAM)
- **AI Infrastructure Market**: $50B+ by 2025 (Gartner)
- **Local AI Model Downloads**: 10M+ monthly (Hugging Face)
- **Enterprise AI Spending**: $200B+ by 2027 (McKinsey)

### Serviceable Addressable Market (SAM)
- **AI Developers Globally**: 5M (Stack Overflow Survey)
- **AI-First Startups**: 50K+ (Crunchbase)
- **Target Capture**: 1% = 50K users × $50/month = **$30M ARR potential**

### Beachhead Strategy
- **Year 1**: Individual AI developers (10K users)
- **Year 2**: AI startups and small teams (100 companies)
- **Year 3**: Enterprise deployments (10 large clients)

---

## Competitive Advantages

### Technical Moat
1. **Hybrid Architecture**: Unique combination of local AI + decentralized knowledge graph
2. **GraphRAG Implementation**: Advanced semantic search with temporal ontology
3. **SkillForge Platform**: First LoRA marketplace for instant model specialization
4. **3-Tier Memory System**: Solves context explosion in agent systems
5. **Patent-Pending Technology**: Agent orchestration and adaptive memory systems

### Market Position
1. **First Mover**: No direct competitor in "AI OS for local models" category
2. **Network Effects**: More knowledge → better answers → more users → more knowledge
3. **Open Ecosystem**: Compatible with existing tools (Ollama, LM Studio)
4. **Community-Driven**: Token economics incentivize quality contributions

### Economic Advantages
1. **Marketplace Revenue**: 30% commission on all transactions
2. **Staking Requirements**: Barriers to entry for Gateway operators
3. **Data Permanence**: Arweave ensures knowledge cannot be deleted or censored
4. **Cross-Side Network Effects**: Users attract creators, creators attract users

---

## Exit Strategy (5-Year Horizon)

### Potential Outcomes

| Scenario | Probability | Valuation | Multiple | Return on $610K |
|----------|-------------|-----------|----------|-----------------|
| **Strategic Acquisition**<br/> | 40% | $50-100M | 8-16x ARR | 82-164x |
| **IPO / Public Token Market** | 20% | $200M+ | 20x+ ARR | 328x+ |
| **Sustainable Private Business**<br/>(Bootstrap to profitability) | 30% | $10-30M | 5-15x ARR | 16-49x |
| **Failure / Pivot Required** | 10% | <$5M | - | <8x |

**Weighted Expected Return**: ~70x over 5 years

---

## Investment Highlights

### Why Invest Now

1. **Market Timing**: Local AI adoption accelerating (10M+ downloads per month on Hugging Face)
2. **Proven Team**: [Highlight founder experience and track record]
3. **Clear Revenue Path**: Marketplace launches Month 11, revenue visible Month 11
4. **Technical Differentiation**: 3+ years ahead of potential competitors
5. **Network Effects**: First-mover advantage in knowledge marketplace creates defensible moat
6. **Token Utility**: Real use case beyond speculation (staking, payments, governance)
7. **Strategic Value**: High acquisition potential from major AI companies

### De-Risking Factors

- **Rapid MVP**: Working prototype in 3 months enables early validation
- **Phased Rollout**: Test each component before scale
- **Multiple Revenue Streams**: Not dependent on single monetization method
- **Open Source Core**: Community can continue development if needed
- **Convergence Thesis**: Positioned at intersection of Web3 and AI mega-trends

---

## Investment Terms

### Primary Raise: $600K Seed Round

**Use of Funds**:

| Category | Amount | Percentage | Purpose |
|----------|--------|------------|---------|
| **Engineering** | $370K | 62% | Core development team (5 engineers × 10 months) |
| **Security** | $65K | 11% | Multiple security audits + bug bounty program |
| **Infrastructure** | $40K | 7% | Servers, databases, CDN, monitoring tools |
| **Marketing** | $40K | 7% | Community building, PR, launch campaigns |
| **Legal & Compliance** | $25K | 4% | Token legal structure, regulatory review |
| **Operations** | $30K | 5% | Software licenses, tools, miscellaneous |
| **Reserve** | $30K | 5% | Emergency buffer for unforeseen issues |

---

## Next Steps

### For Interested Investors

1. **Due Diligence Materials Available**:
   - Technical architecture deep-dive document
   - Detailed financial model (5-year projections)
   - Team backgrounds and references
   - Competitive analysis report

2. **Product Demonstration**: Schedule live demo of M1 prototype (available Week 12)

3. **Advisory Opportunities**: Limited positions available on Strategic Advisory Board

4. **Investment Structure**: SAFE agreement with standard seed round terms

### Timeline for Closing

- **Week 1-2**: Investor meetings and initial due diligence
- **Week 3**: Term sheet negotiation and agreement
- **Week 4**: Legal documentation and closing
- **Week 5**: Fund transfer and development kickoff

---

## Appendix: Technical Stack Summary

| Layer | Technology | Purpose |
|-------|------------|---------|
| **Client** | Python, Click, Rich, llama.cpp | Desktop application and CLI |
| **AI Core** | llama.cpp, GGUF, PEFT/LoRA | Local model inference |
| **Memory** | SQLite (WAL), DuckDB, Redis | 3-tier memory system |
| **Agent** | Python asyncio, FSM, NetworkX | Agent orchestration |
| **Gateway** | FastAPI, uvicorn, httpx | HTTP API server |
| **Search** | PostgreSQL, pgvector, transformers | Semantic search |
| **Blockchain** | Rust, Substrate, Polkadot.js | Peaq pallet development |
| **Storage** | Arweave SDK, Bundlr, DuckDB HTTPFS | Permanent storage |
| **Web** | Playwright, Brave Search API | Web automation |
| **Frontend** | React, TypeScript, Tailwind CSS | Marketplace UI |

---
