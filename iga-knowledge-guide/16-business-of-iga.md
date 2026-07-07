# Chapter 16: The Business of IGA

> *"Understanding the commercial context isn't optional for a platform leader. When you know WHY customers buy and WHAT they value, your engineering decisions get better."*

---

## Why a Platform Leader Should Care About Business Context

| Without Business Context | With Business Context |
|-------------------------|----------------------|
| "We need to fix 50 connector bugs" | "These 5 connector bugs are blocking $2M in pipeline — fix those first" |
| "Let's improve p99 latency" | "Cert campaign performance impacts renewal conversations — prioritize during cert windows" |
| "All features are equal priority" | "Cloud governance is our wedge into SailPoint accounts — platform stability there is revenue-critical" |
| "The architecture is elegant" | "The architecture enables faster deployments which reduces professional services cost which improves deal economics" |

---

## How IGA Is Sold

### The Buying Process

```
TYPICAL IGA DEAL TIMELINE: 6-18 months

Discovery          Evaluation         Proof of Concept    Negotiation      Close
(1-3 months)       (2-4 months)       (1-3 months)       (1-3 months)     
│                  │                  │                  │                │
│ Pain identified  │ Vendor shortlist │ Deploy in         │ Contract,      │ Revenue!
│ Budget explored  │ RFP/demo         │ customer env      │ pricing,       │
│ Stakeholders     │ Feature compare  │ With real data    │ legal,         │
│ aligned          │ Reference calls  │ Prove value       │ security       │
│                  │                  │                  │ review         │
└──────────────────┴──────────────────┴──────────────────┴────────────────┘
```

### Deal Sizes

| Segment | Annual Contract Value (ACV) | Typical Org Size | Deal Complexity |
|---------|----------------------------|-----------------|-----------------|
| Enterprise | $500K - $3M+ | 50,000+ employees | Multi-year, multi-stakeholder, POC required |
| Mid-Market | $100K - $500K | 5,000 - 50,000 | 6-12 months, simpler evaluation |
| Growth | $50K - $150K | 1,000 - 5,000 | Faster, fewer stakeholders |

### Pricing Models

| Model | Description | Trend |
|-------|-------------|-------|
| Per-identity | Price per managed identity (human + machine) | Most common |
| Per-module | Base + add-ons (IGA + CPAM + AAG) | Common for converged platforms |
| Tiered | Standard/Professional/Enterprise features at different prices | Growing |
| Consumption | Pay per provisioning operation, certification, etc. | Emerging |

---

## Buyer Personas

### Who's Involved in an IGA Purchase

| Persona | Role in Decision | What They Care About |
|---------|-----------------|---------------------|
| **CISO** | Final authority (usually) | Risk reduction, board-reportable metrics, vendor trust |
| **VP of Identity/IAM** | Primary champion, evaluator | Capabilities, roadmap, technical fit |
| **Director of GRC** | Requirements driver | Compliance coverage, audit readiness, SoD |
| **CIO/CTO** | Budget approval | TCO, architecture fit, consolidation |
| **IT Operations** | Implementation owner | Deployment complexity, ongoing ops burden |
| **CISO Staff** | Technical evaluation | Security architecture, integration, APIs |
| **Procurement** | Contract negotiation | Price, terms, SLA guarantees |
| **Legal/Privacy** | Data handling review | Data processing agreements, privacy |
| **Internal Audit** | Requirements input | Evidence quality, audit automation |

### What Each Persona Values

```
CISO: "Will this keep us out of headlines and pass audits?"
       → Metrics: Risk score reduction, audit findings closed, 
         certification completion rates

VP Identity: "Can this replace our 3 current tools and be deployed by Q3?"
              → Metrics: Connector coverage, migration timeline, 
                consolidation savings

GRC Director: "Will auditors accept the evidence this produces?"
               → Metrics: Framework coverage, evidence quality, 
                 SoD detection rate

CTO: "Does this fit our cloud strategy and reduce vendor sprawl?"
      → Metrics: Architecture (cloud-native), API quality, 
        integration with existing stack
```

---

## Competitive Dynamics

### Why Customers Switch

| Trigger | Frequency | Competitive Play |
|---------|-----------|-----------------|
| Current vendor end-of-life | Common | Any vendor can compete |
| Cloud migration (on-prem → SaaS) | Very common | Cloud-native wins (Saviynt advantage) |
| Audit failure / compliance gap | Common | Vendor with strongest compliance story wins |
| Consolidation (reduce vendors) | Growing | Converged platform wins (Saviynt positioning) |
| Cost pressure | Moderate | Lower TCO vendor wins |
| Poor vendor support/relationship | Moderate | Better service/partnership wins |

### Common Competitive Scenarios

#### Saviynt vs. SailPoint

| Dimension | Saviynt Pitch | SailPoint Counter |
|-----------|--------------|-------------------|
| Architecture | Cloud-native, born in cloud | "We have cloud too (ISC), AND on-prem option" |
| Convergence | One platform: IGA+CPAM+AAG+DSAG | "Our ecosystem has best partners for each" |
| Cloud governance | Deep native cloud understanding | "Our AI platform leads" |
| Installed base | Growing fast, proven at scale | "Fortune 500 trust us, larger community" |
| Time to value | 3-6 months | "Depends on scope" |

#### Saviynt vs. Microsoft Entra

| Dimension | Saviynt Pitch | Microsoft Counter |
|-----------|--------------|-------------------|
| Depth | Full IGA capabilities (SoD, roles, deep certs) | "Good enough for most, zero deployment" |
| Multi-system | Governs 200+ systems including non-Microsoft | "Everyone has Microsoft already" |
| Complexity | Handles complex enterprise governance | "Simple is better for most orgs" |
| Cost | Purpose-built, best at governance | "Bundled in E5 license you already pay for" |

### How Engineering Decisions Impact Competition

| Engineering Decision | Competitive Impact |
|---------------------|-------------------|
| Faster connector development | More systems supported → more deal-ready |
| Better provisioning reliability | Fewer implementation issues → faster time-to-value |
| Improved cert campaign performance | Better UX → higher customer satisfaction → retention |
| AI recommendation quality | Differentiation in demos → wins evaluations |
| API quality/documentation | Developer adoption → stickiness |
| Multi-region deployment | New geographies accessible → new market segments |
| FedRAMP maintenance | Government deals accessible → unique revenue |

---

## Revenue Models and Growth Metrics

### How IGA Companies Grow

```
GROWTH VECTORS:

1. NEW LOGOS (net-new customers)
   └── Win competitive deals, expand to new segments/geos

2. EXPANSION (existing customers)
   ├── More identities (customer grows → more licenses)
   ├── More modules (IGA → add CPAM → add AAG)
   ├── More connectors (govern additional systems)
   └── Higher tier (Standard → Enterprise)

3. RETENTION (prevent churn)
   └── Platform reliability, customer success, product fit
```

### Key Business Metrics

| Metric | What It Measures | Why Platform Team Cares |
|--------|-----------------|------------------------|
| **ARR** (Annual Recurring Revenue) | Total subscription revenue | Company health |
| **NDR** (Net Dollar Retention) | Revenue growth from existing customers | >120% = great (expansion > churn) |
| **Logo churn** | Customers leaving | Reliability issues → churn |
| **NPS / CSAT** | Customer satisfaction | Platform performance impacts this directly |
| **Time-to-value** | Days from contract to production | Faster = better economics |
| **Professional services ratio** | PS revenue vs. subscription | Lower = better (product is self-service) |
| **Gross margin** | Revenue - hosting/delivery costs | Platform efficiency directly impacts this |

### Platform Team's Impact on Business Metrics

```
ENGINEERING → BUSINESS CONNECTION:

Platform reliability ──→ Customer satisfaction ──→ Retention (NDR)
     │
Fast provisioning ──→ Quick implementation ──→ Lower PS cost ──→ Better margins
     │
Multi-tenant efficiency ──→ Lower hosting cost ──→ Better gross margin
     │
API quality ──→ Self-service integration ──→ Reduced support cost
     │
Connector reliability ──→ Fewer escalations ──→ Better NPS
     │
Security posture ──→ SOC 2 / FedRAMP maintained ──→ Enterprise/Gov deals possible
```

---

## TCO (Total Cost of Ownership) Arguments

### What Enterprise Customers Calculate

```
TOTAL COST OF IGA OWNERSHIP:

Year 1:
├── License/subscription fee: $500K
├── Implementation (SI partner): $400K
├── Internal team time: $200K
├── Training: $50K
├── Infrastructure (if on-prem): $150K
└── TOTAL Year 1: $1.3M

Ongoing (per year):
├── Subscription: $500K (grows with identity count)
├── Maintenance/operations: $100K (internal team)
├── Annual reviews/tuning: $75K
└── TOTAL per year: $675K

5-Year TCO: $1.3M + (4 × $675K) = $4M
```

### How Cloud-Native Reduces TCO

| Cost Component | On-Prem Legacy | Cloud-Native (Saviynt) |
|---------------|---------------|------------------------|
| Infrastructure | Customer pays ($150K+/yr) | Included in subscription |
| Upgrades | Major project every 2-3 years ($200K+) | Continuous, included |
| Operations staff | 2-3 FTEs dedicated | Shared (vendor manages) |
| Implementation | 12-18 months | 3-6 months (less SI cost) |
| Customization | Heavy (then stuck) | Configuration (portable) |
| **5-year comparison** | **$5-7M** | **$3-4M** |

---

## The ROI Conversation

### How Customers Justify IGA Spend

| ROI Category | Metric | Value |
|-------------|--------|-------|
| **Audit cost reduction** | Weeks of prep eliminated | $200K-$500K/year in labor |
| **Incident prevention** | Breaches avoided (probabilistic) | $4.88M avg breach cost × probability |
| **Productivity** | Faster onboarding (days saved × new hires × daily cost) | $100K-$300K/year |
| **Labor reduction** | Manual processes automated | 2-5 FTEs worth of manual work |
| **Fine avoidance** | Compliance violations prevented | Variable ($100K-$20M per incident) |
| **Tool consolidation** | Replacing multiple tools | $100K-$500K in eliminated licenses |

### The "Board Metric"

What CISOs report to the board (and therefore what drives IGA purchases):

```
BOARD-LEVEL METRICS FROM IGA:

"% of access that has been reviewed in the last 90 days: 97%"
"Average time to revoke terminated employee access: 47 minutes"
"SoD violations: 23 (down from 145 last year, all with compensating controls)"
"Audit findings related to access: 0 (down from 12)"
"% of access that is birthright (automated): 78%"
```

---

## Market Trends Shaping the Business

### 1. Platform Consolidation

Customers actively reducing vendor count:
- 2020: Average enterprise had 76 security tools
- 2025: Active effort to consolidate to <50
- IGA vendors that offer IGA + PAM + cloud governance win consolidation deals

### 2. Compliance-as-a-Service

Shift from "buy tool, build program" to "buy outcome":
- Customers want "make me SOX compliant" not "give me a certification engine"
- Pushes vendors toward packaged compliance solutions
- Reduces professional services dependency

### 3. Identity Security (Broader Category)

IGA expanding from "governance tool" to "identity security platform":
- Include threat detection (ITDR)
- Include posture management
- Include attack path analysis
- Analyst firms creating new categories

### 4. Developer-Led Adoption

New entrants (Opal, ConductorOne, Veza) targeting developers:
- Bottom-up adoption vs. top-down enterprise sale
- API-first, developer-friendly
- Threat: could capture new market segments before enterprise IGA adapts
- Opportunity: enterprise IGA vendors that add developer experience win both personas

### 5. AI as Competitive Differentiator (2024-2026)

Every vendor claiming AI. Differentiation through:
- Actual shipped capabilities (not roadmap promises)
- Measurable improvement in certification quality
- Demonstrated reduction in manual governance work
- Customer evidence of AI-driven risk reduction

---

> **🔧 Platform Engineering Lens**
>
> Understanding the business of IGA helps you make better engineering decisions:
>
> **Prioritization:**
> - "This reliability improvement prevents churn of 3 enterprise accounts (worth $4M ARR)" → P1
> - "This performance improvement helps win competitive POCs" → invest
> - "This architecture change reduces hosting cost 20%" → directly improves gross margin
>
> **Communication:**
> - To CISO customers: speak in risk reduction, compliance coverage
> - To your executives: connect platform work to ARR, NDR, margin
> - To engineering: translate business priority into technical work
>
> **Strategy:**
> - If market is moving to consolidation → invest in platform supporting multiple modules efficiently
> - If developer experience is a competitive wedge → invest in APIs, CLI, self-service
> - If AI is a differentiator → invest in inference infrastructure, evaluation pipelines
>
> A platform leader who understands the business makes fundamentally different (better) decisions than one who optimizes engineering metrics in isolation.

---

## Self-Test Questions

1. Who are the key personas in an IGA buying decision? What does each value?
2. Why is "time-to-value" a critical metric for IGA companies? How does platform engineering affect it?
3. How does platform reliability directly impact revenue metrics (NDR, churn)?
4. What's the TCO argument for cloud-native IGA vs. on-prem? How does each cost component differ?
5. How would you frame a platform reliability investment in business terms (not just engineering metrics)?
6. Why should a platform engineering leader understand competitive dynamics?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **ARR** | Annual Recurring Revenue — total subscription revenue annualized |
| **NDR** | Net Dollar Retention — revenue growth/shrinkage from existing customers |
| **ACV** | Annual Contract Value — revenue from a single customer per year |
| **TCO** | Total Cost of Ownership — all costs over a time period (not just license) |
| **Logo Churn** | Rate at which customers leave |
| **Time-to-Value** | Duration from purchase to productive use |
| **Professional Services** | Paid implementation/consulting work (separate from subscription) |
| **POC** | Proof of Concept — trial deployment to validate product fit |
| **RFP** | Request for Proposal — formal vendor evaluation document |
| **Gross Margin** | Revenue minus direct costs (hosting, delivery) as % of revenue |
| **NPS** | Net Promoter Score — customer likelihood to recommend |
| **SI** | Systems Integrator — partner firm that implements the product |
| **Competitive Displacement** | Winning a deal by replacing an incumbent vendor |
