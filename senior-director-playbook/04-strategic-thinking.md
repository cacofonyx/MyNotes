# Chapter 04: Strategic Thinking for Platform/SRE at Director Level

> *"A good strategy honestly acknowledges the challenges being faced and provides an approach to overcoming them."* — Richard Rumelt

Strategy at Director level is not "what should we build next quarter." It's: "Given where the business is going, where does my organization need to be in 18 months, and what sequence of moves gets us there?" It's the difference between planning and positioning.

For Platform/SRE specifically, strategic thinking is harder because:
- Your work is invisible when successful
- Your value is defined by other teams' ability to ship
- Your investments have long payback horizons
- Leadership often confuses "infrastructure" with "cost center"

This chapter covers how to think strategically in this domain — and how to translate that thinking into action the business supports.

---

## What Strategy Actually Is (And Isn't)

### Rumelt's Kernel of Strategy

A good strategy has three components:
1. **Diagnosis** — What's actually going on? (Not the superficial symptoms, the structural reality)
2. **Guiding policy** — Given the diagnosis, what's our overall approach? (A choice that EXCLUDES alternatives)
3. **Coherent actions** — What specific moves flow from that policy? (And are they mutually reinforcing?)

**Bad strategy** (which is most of what passes for strategy in tech companies):
- A list of goals without a plan ("improve reliability, scale the platform, reduce toil")
- Aspirations without trade-offs ("we'll do all of it")
- Refusal to choose ("our strategy is to be excellent at everything")

### Platform/SRE Strategy: A Worked Example

**Bad version:** "Our strategy is to improve developer productivity, increase reliability, and modernize the platform while supporting rapid growth."

This says nothing. It makes no choices. It could apply to any platform team anywhere.

**Good version:**

**Diagnosis:** Our IGA product is winning enterprise deals but deployment velocity is 10x slower than competitors. Connector reliability directly causes customer churn. We have 3 years of infrastructure debt from single-tenant architecture that will block multi-region expansion. Our team is understaffed relative to the platform surface area we support.

**Guiding policy:** For the next 18 months, we prioritize deployment velocity and connector reliability over platform modernization. We do NOT attempt the multi-tenant migration until we've stabilized what we have and doubled the team. We accept that some architectural debt will accumulate in areas outside our focus.

**Coherent actions:**
- Q1: CI/CD pipeline rebuilt (deploy time from 4 hours → 30 minutes)
- Q2: Connector observability + auto-recovery (reduce MTTR by 60%)
- Q2-Q3: Hire 6 engineers into reliability and platform teams
- Q3-Q4: Begin multi-region readiness (with the larger team)
- Not now: Full multi-tenant re-architecture, Kubernetes migration, ML-ops infrastructure

**Why this works:** It makes a clear choice (velocity + reliability OVER modernization), explains WHY (the business constraint: enterprise deals + connector churn), and sequences actions that reinforce each other.

---

## Strategic Thinking Frameworks

### Framework 1: The Three Horizons

| Horizon | Time Frame | Your Job | IGA/Platform Example |
|---------|-----------|----------|---------------------|
| H1: Run | This quarter | Deliver committed outcomes, keep the lights on | SLOs met, deployments work, incidents resolved |
| H2: Grow | 2-4 quarters | Build capabilities that enable next stage | New deployment pipeline, observability platform, team scaling |
| H3: Transform | 1-3 years | Place bets on where the world is going | Multi-cloud, platform-as-product, AI-assisted operations |

**The Director's job:** Ensure appropriate investment across all three horizons.

**The common failure:** All resources on H1 (firefighting) with nothing invested in H2/H3. You feel productive but you're running in place. In 18 months you're fighting the SAME fires because you never built the systems to prevent them.

**The allocation question:** What % of your team's capacity is in each horizon?
- Crisis mode: 80/15/5 (H1/H2/H3) — unsustainable, but sometimes necessary short-term
- Healthy growth: 50/35/15 — enough operational capacity plus real investment in the future
- Mature platform: 30/40/30 — operations are largely automated, most investment is forward-looking

### Framework 2: Platform as Product (Strategic Lens)

Your platform has customers (internal teams), a product (capabilities they consume), and a market (the company's evolving needs). Think like a product strategist:

**Who are your customers?** (Segment them)
- Product engineering teams (largest consumer — they need velocity + reliability)
- Security/compliance teams (need audit, control, governance)
- Data teams (need infrastructure, compute, pipeline)
- Executives (need cost visibility, risk reduction)

**What do they actually need?** (Not what they ask for)
- Product teams ask for "faster deploys" → they need: ability to ship confidently 10x/day
- Security asks for "more controls" → they need: compliance evidence without slowing product
- Execs ask for "cost reduction" → they need: predictable cost scaling, not just lower absolute cost

**What's your product roadmap?** (Prioritize by customer value × strategic alignment)

**What's your competitive threat?** (Shadow platforms, teams building their own, vendor solutions that bypass you)

### Framework 3: Wardley Mapping for Platform Decisions

For each capability your platform provides, assess where it sits on the evolution axis:

| Stage | Characteristics | Strategic Implication |
|-------|----------------|---------------------|
| Genesis | Novel, uncertain, custom-built | Invest in experimentation. Expect failure. Keep small. |
| Custom-built | Understood but unique to you | Build it, but expect to commoditize eventually. |
| Product | Well-understood, many solutions exist | Buy or adopt. Don't build. Differentiation is elsewhere. |
| Commodity | Utility, everyone uses the same thing | Use the cheapest/simplest option. Zero investment in differentiation. |

**IGA-specific application:**
- Connector framework: Custom-built (your competitive advantage — build, invest heavily)
- CI/CD pipeline: Product stage (use existing tools, don't build from scratch)
- Monitoring/alerting: Product→Commodity (Datadog/Grafana, don't build your own)
- Tenant isolation layer: Custom-built→Genesis (novel for your scale/domain — invest, experiment)
- Kubernetes/container orchestration: Commodity (managed service, minimal custom work)

**The strategic error:** Building custom solutions for things that are already commodity. Every engineer maintaining a custom CI/CD system is an engineer NOT building your connector framework.

### Framework 4: Technical Strategy as Business Strategy

At Director level, your technical strategy must be expressed in business terms or it won't get funded.

| Technical Investment | Business Translation |
|---------------------|---------------------|
| Multi-region deployment | "We can win deals in EU/APAC that require data residency — $XM pipeline currently blocked" |
| Deployment velocity | "Product can ship features 3x faster → faster time-to-value for customers → reduced churn" |
| Connector reliability | "Every connector outage risks a renewal. Top 10 accounts have connector SLA in contract." |
| Platform observability | "We detect and resolve issues before customers notice → NPS improvement → lower support cost" |
| Multi-tenant architecture | "Our cost-per-customer drops 60% → unit economics work at scale → enables SMB tier" |

**The discipline:** Every strategy document you write should answer "why does the business care?" within the first paragraph. If you can't connect it to revenue, retention, or risk — it won't be prioritized.

---

## How to Build Your Strategic POV

### Step 1: Map the Business Context

Understand where the company is in its growth trajectory and what the executive team cares about:

| Company Stage | What Execs Care About | What That Means for Platform |
|--------------|----------------------|------------------------------|
| Pre-PMF | Speed to iterate | Stay out of the way, minimize process |
| Growth ($50M-$200M) | Scale + enterprise readiness | Reliability, compliance, multi-tenant |
| Scale ($200M-$500M) | Efficiency + expansion | Cost optimization, multi-region, platform leverage |
| Public/mature ($500M+) | Predictability + margins | Automation, self-service, engineering efficiency metrics |

For a growth-phase IGA company like Saviynt: likely in the Growth→Scale transition. Enterprise customers demand reliability and compliance. International expansion demands multi-region. And engineering efficiency matters because headcount is expensive.

### Step 2: Identify the Structural Constraints

What makes YOUR platform challenge different from a generic one?

IGA-specific structural constraints:
- **Security is the product** — Platform failures ARE security failures for customers
- **Hybrid deployment** — You operate cloud + customer-premises agents. This doubles complexity.
- **Connector combinatorics** — Hundreds of target systems, each with unique APIs, auth patterns, failure modes
- **Compliance as gating function** — FedRAMP, SOC2, data residency requirements constrain architectural choices
- **Burst patterns** — Access certification campaigns create 100x traffic spikes
- **Customer-specific configuration** — Every tenant has custom workflows, policies, integrations

These constraints aren't problems to solve — they're the landscape you strategize WITHIN.

### Step 3: Identify the Leverage Points

Where does a small investment create disproportionate value?

| Leverage Point | Why It's High-Leverage | Investment Required |
|---------------|----------------------|---------------------|
| Deployment pipeline | Every product team benefits. Currently THE bottleneck for shipping speed. | Medium — mostly tooling + process |
| Connector framework | 100+ connectors built on the same foundation. One framework improvement multiplies across all. | High — but ROI is massive |
| Observability | Can't fix what you can't see. Every reliability improvement depends on this. | Medium — instrumentation + dashboards |
| Self-service tenant provisioning | Currently manual = sales bottleneck. Automating unblocks revenue. | Medium-High |
| Incident response automation | Reduce MTTR at scale. Each improvement saves across every future incident. | Low-Medium |

### Step 4: Sequence for Compounding Returns

Order investments so each one makes the next one easier:

```
Observability → Connector reliability → Deployment velocity → Multi-region
     ↓                    ↓                       ↓                    ↓
 (enables)          (depends on          (depends on            (depends on
  measurement)       visibility)          stable base)          all three)
```

Bad sequencing: trying to do multi-region before you have reliable deployments and observable connectors. You'll build on sand.

Good sequencing: each phase creates the foundation the next phase requires. This is strategic coherence.

---

## Common Strategic Mistakes at Director Level

### Mistake: "Strategy by Accretion"

**What it looks like:** Your roadmap is a pile of requests from different stakeholders. Product wants X, Security needs Y, Exec asked for Z. You try to do all of it. The "strategy" is just a prioritized backlog.

**Why it's not strategy:** No diagnosis, no guiding policy, no choices. You're being reactive, not strategic. You'll do everything poorly instead of a few things well.

**Fix:** Force yourself to answer: "If I could only accomplish ONE thing in the next year, what creates the most value?" Start there. Everything else is sequenced after.

### Mistake: "Technical Purity as Strategy"

**What it looks like:** Your strategy is about achieving some technical ideal state — "migrate to microservices," "zero technical debt," "fully automated." The strategy reads like an architecture document.

**Why it fails:** Technical excellence is a means, not an end. No executive funds "clean architecture." They fund "we can ship 3x faster" or "we'll stop losing customers to outages."

**Fix:** Start every strategy statement with a business outcome. The technology is HOW, not WHAT or WHY.

### Mistake: "Ignoring the Political Economy"

**What it looks like:** You have a brilliant strategy that requires Product teams to change their workflow, Security to adopt your tooling, and Execs to fund a 30% headcount increase. You present it as a technical plan.

**Why it fails:** Strategy that requires others to change without addressing their incentives is a wish list. You need to understand what each stakeholder gains from your strategy — and if they don't gain, you need to make them gain or find a different path.

**Fix:** For every strategic initiative, answer: "Who needs to say yes? What's in it for them? What do they lose? How do I address that?"

### Mistake: "Infinite Time Horizon"

**What it looks like:** Your strategy is a beautiful 3-year vision with no intermediate milestones. "In 3 years we'll have a fully self-service, multi-region, AI-operated platform."

**Why it fails:** Three-year visions are fine as North Stars. But strategy that doesn't create value in the NEXT quarter will lose funding, attention, and patience. Especially at a growth-stage company.

**Fix:** Strategy must have quarterly waypoints. Each quarter should deliver something visible while building toward the longer vision. "This quarter we deliver X (standalone value), which also sets up Y (next quarter) and eventually Z (end state)."

---

## Translating Strategy into Operating Rhythm

Your strategy lives in three artifacts:

### 1. The Vision Document (Annual)
- Where we're going and why
- 1-2 pages, written in business language
- Updated yearly, referenced constantly
- Audience: your team, your peers, your boss

### 2. The Quarterly Plan (Quarterly)
- What we're doing THIS quarter to advance the strategy
- Specific goals, owners, measurable outcomes
- What we're explicitly NOT doing (and why)
- Audience: your team (execution) and your boss (accountability)

### 3. The Weekly Signal (Ongoing)
- Are we on track? What's changed? What decisions are needed?
- Not a status report — a strategic health check
- Audience: yourself (are we still on the right path?)

---

## Chapter Summary

Strategy at Director level means making choices — not just listing what you want to do. The core skill is connecting technical investments to business outcomes, sequencing for compounding returns, and maintaining investment across multiple time horizons. Platform/SRE strategy is harder because your value is invisible and your investments have long paybacks — so you must be exceptionally clear about WHY each investment matters in business terms.

**The test of a good strategy:** If you can't explain what you're NOT doing and why, you don't have a strategy. You have a wish list.
