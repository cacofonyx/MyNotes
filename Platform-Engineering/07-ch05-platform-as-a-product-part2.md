# Chapter 5: Platform as a Product — Part 2: Execution, Roadmaps, and Failure Modes

> **Part II — Platform Engineering Practices** *(continued from Part 1)*

Part 1 covered how to build a product culture and discover what to build. This part covers how to *execute*: turning insights into a roadmap, aligning teams around a strategy, and delivering iteratively. It closes with the most common failure modes — the ways platform teams stumble when first adopting product management practices.

## Table of Contents

- [Successful Product Execution: Creating a Product Roadmap](#successful-product-execution-creating-a-product-roadmap)
  - [Vision: Long Term](#vision-long-term)
  - [Strategy: Middle Term](#strategy-middle-term)
  - [Goals and Metrics: This Year](#goals-and-metrics-this-year)
  - [Milestones: Quarterly](#milestones-quarterly)
  - [The Customer-Facing Roadmap](#the-customer-facing-roadmap)
  - [Specification of Features](#specification-of-features)
- [Product Failure Modes](#product-failure-modes)
  - [Underestimating the Migration Cost](#underestimating-the-migration-cost)
  - [Overestimating the Change Budget for Users](#overestimating-the-change-budget-for-users)
  - [Overestimating the Value of New Features When Stability Is Poor](#overestimating-the-value-of-new-features-when-stability-is-poor)
  - [Having Too Many Product Managers](#having-too-many-product-managers)
  - [Having PMs Doing Engineering Management Work](#having-pms-doing-engineering-management-work)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Deep Dive] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [AI Impact]

---

## Successful Product Execution: Creating a Product Roadmap

A common scenario the authors describe: you have a compute platform team. Some people work on base OS/container/VM images, some on configuration management, some on legacy OpenStack, some on Kubernetes, some on Terraform for cloud. Each area is going "OK" — but there's no overarching concept of how these pieces create a complete, integrated experience. Each sub-team builds within their silo. The overall experience remains "disjointed and confusing."

The fix: step back and create a product roadmap that goes from vision to reality. The process layers from abstract to concrete:

```
Vision (aspirational, long-term)
  → Strategy (what's preventing the vision, middle-term)
    → Goals & Metrics (this year, measurable)
      → Milestones (quarterly delivery)
        → Feature Specs (individual work items)
```

### Vision: Long Term

The vision paints a picture of the essential characteristics of a better future platform. It may never be fully realized — it's aspirational. It serves to *align* all the tactical work.

**Example:** "Enable a developer to provision the environment they need in two hours, whether on premises, in the cloud, or in the DMZ."

Simple. Clear. Tells everyone which direction to walk without prescribing the steps.

### Strategy: Middle Term

Strategy = understanding what's *preventing* you from achieving your vision. Engineering identifies technical challenges. Product management identifies user-facing requirements (pain points, preferred interfaces, frequency of interactions, who the real users are).

**Example:** After research, the strategy might be: "Fast containerized compute provisioning: reduce application provisioning time for new containerized environments to minutes." This narrows the vision to an achievable intermediate target — rather than trying to speed up all provisioning for all types at once.

The point of having a strategy between vision and plan: it documents *why* you're making specific choices. Without it, teams jump from vision to implementation and can't explain their trade-offs to stakeholders.

### Goals and Metrics: This Year

Written in OKR-like format. The objective is an opinionated goal statement; key results detail specific focus areas with measurable outcomes.

**Example OKR:**
- **Objective:** Bring fast compute provisioning for containerized environments to the user's development context
- **Key Results:**
  - Enable provisioning from IDE or command line for 50% of supported compute types
  - Reduce time from provisioning request to completion by 25%
  - Drive down usage of legacy VM platform by 20%

### Milestones: Quarterly

Break the year into delivery chunks. What technical work needs to be delivered each quarter? When will features reach customers? Where do you need to pause and reevaluate?

### The Customer-Facing Roadmap

An important distinction: for internal communication with customers, share only *user-visible feature delivery*. If customers ask why something takes long, you can share the underlying technical roadmap — but proactively exposing internal technical milestones invites accusations of "building things engineers think are cool" instead of focusing on business delivery.

> **[Core Concept: Internal Technical Roadmap vs. External Customer Roadmap]**
>
> This is a practical communication principle that many platform teams get wrong:
>
> **Internal (for the team):** All the work — infrastructure upgrades, refactoring, scalability improvements, migration tooling, new feature development. Sequenced by dependencies and risk.
>
> **External (for customers):** Only what changes for them — new capabilities they'll get, migration timelines they need to prepare for, deprecations coming. Sequenced by when they'll see value.
>
> **Why the distinction matters:** When customers see "Q1: Upgrade Kafka to 3.x, refactor consumer SDK internals, re-shard topic partitions" they think "why isn't the team working on things that help me?" They can't connect infrastructure work to the features they'll eventually get. But when they see "Q2: Self-service topic creation with automatic schema validation" they understand the value — even if Q1's invisible infrastructure work was prerequisite.
>
> Platform teams that share only the internal roadmap get constant pushback about priorities. Teams that share only the customer roadmap maintain support and buy time for necessary infrastructure investment.

### Specification of Features

Once you have a roadmap, you need feature specs. The process:
1. PM documents **feature outcomes** — why it's important, what customers need, how it fits the vision
2. PM shares with engineering leads
3. Discussion between PM and engineering produces the **what** (constrained by technical, budget, and human realities)
4. Any "what" taking longer than ~1 month gets broken into sub-steps
5. Document as product requirements / user stories / whatever your org uses

The authors emphasize: "Deciding what to build cannot be done by the product manager alone" — engineering leadership must co-own this. PM brings the *why*, engineering brings the *constraints and possibilities*, together they produce the *what*.

> **[Organizational Reality: "Practice Makes Perfect" — This Is Hard]**
>
> The authors are refreshingly honest about roadmapping:
>
> - Developing a compelling vision is hard
> - Breaking it into measurable items reflecting impact (not output) is hard
> - Documenting feature outcomes and working with engineering to determine what to build is hard
> - Doing all of this while maintaining customer relationships and operational excellence is hard
>
> Their advice: keep doing the exercise. Over time you develop a sense of what "good" feels like. The first roadmap will be imperfect — the third will be better — the seventh will feel natural.
>
> **What to do when customers ask for things that aren't on the roadmap:** The authors address this common frustration — a customer can't tell you what they want up front, but they also can't just wait for whatever you decide to build. The answer: don't expect customers to participate in abstract design meetings. Instead, build incrementally, get feedback quickly on what you build, and validate demand throughout delivery. "We can't just ask our customers what to build, but we can use them to validate our ideas by getting their feedback quickly on what we build."

---

## Product Failure Modes

The authors close with five specific failure modes they've observed when platform teams first adopt product management. Each is common, recognizable, and avoidable with awareness.

### Underestimating the Migration Cost

> **[Worked Example: The Code Search Disaster]**
>
> Camille describes a real case: a developer experience PM was convinced a new code search tool would add tremendous value. He created a compelling pitch, got buy-in from engineering, customers, and (reluctantly) from leadership. The migration from the existing open source search tool was "assured to be reasonably straightforward."
>
> **What actually happened:**
> - Links to the old tool were *everywhere* — the team had to build a redirect service
> - The old tool had been configured to ignore certain repos/branches — replicating these edge cases in the new system was harder than expected
> - Nobody had analyzed user access patterns — some workflows didn't translate 1:1, requiring user training
> - Changing something deeply ingrained in developer workflow generated massive complaints
>
> The migration took *years*. The product itself was fine. But the migration cost dominated the experience, and users viewed the work as "sloppy and ill-considered."
>
> **The lesson:** Migration costs — both engineering AND user experience — can dwarf the value of a new offering. PMs must include migration analysis in product planning from day one, not as an afterthought.

### Overestimating the Change Budget for Users

Internal customers have a finite capacity for change. They have their own roadmaps, their own fires, their own deadlines. Adopting a new platform offering has to compete with all of that — and unless it's a must-have, it will lose.

The authors use the term **"change budget"** — each team can absorb only so much platform change per year. You're not the only one asking: multiple platform teams, infrastructure migrations, security requirements, and compliance mandates all compete for the same limited change capacity.

**Practical implications:**
- Think about how much change you'll push through the company in a year
- Find ways to reduce adoption cost (easy migration, backwards compatibility, gradual rollout)
- Ensure immediate benefits — users need to see value quickly after adopting, not 6 months later
- Be realistic: people say yes to theoretical things. When actual effort is required, many lose interest.

> **[SRE/Production Lens: Stability Creates Change Budget]**
>
> The authors make an observation that's pure SRE wisdom applied to product management: stability and change budget are directly related.
>
> When your platform is unstable:
> - Your team spends time firefighting instead of building
> - Users spend time working around failures instead of adopting new features
> - Nobody has spare capacity for voluntary migration
> - The change budget is effectively zero
>
> When your platform is rock-solid:
> - Your team has capacity to build new things
> - Users have mental space to learn and adopt new offerings
> - The change budget expands
>
> This is why the next failure mode (overestimating value of features when stability is poor) is so important — it's the product manifestation of a reliability failure.

### Overestimating the Value of New Features When Stability Is Poor

This is "painful but true": both engineers and PMs mistake novelty as the most important offering. But when your existing platform is unreliable, nobody cares about new features. Who wants to adopt something new from a team that can't keep the existing system running?

> *"When your platform is having stability issues, it's almost always better to invest engineering time into improving stability instead of adding more features or products onto an unreliable base."*

You might miss product goals for the year — but that's better than shipping features onto a foundation nobody trusts.

> **[Core Concept: Trust Before Features]**
>
> This principle applies broadly: you cannot build product adoption on an unreliable foundation. The trust stack for platforms:
>
> 1. **First:** The platform works (stability, reliability, basic operational excellence)
> 2. **Then:** The platform is easy to use (good UX, self-service, documentation)
> 3. **Then:** The platform adds value beyond basics (advanced features, new capabilities)
>
> Jumping to step 3 while step 1 is failing is the #1 product mistake platform teams make. It feels productive (we're shipping features!) but it destroys trust (users experience new features on an unstable foundation, blame the platform for both the instability AND the poorly-timed new work).
>
> The analogy: a restaurant that can't consistently get orders right shouldn't be adding new menu items. Fix the kitchen first.

### Having Too Many Product Managers

A surprising one — but real. Too many PMs relative to engineering creates specific dysfunctions:

- PMs start doing work engineers should own (execution management, tech decisions)
- Engineers "shut off their brains" and become order-takers implementing specs
- Creativity and ownership get cut off from the engineering side
- The team operates like external contractors: specs in, code out

The authors' ratio guidance: "feel stretched for PMs but not starving." Somewhere between the number of second-line managers and first-line managers. This varies by product maturity and nature of work (fewer PMs needed when most work is operational/scaling).

### Having PMs Doing Engineering Management Work

When PMs groom backlogs, spoon-feed work to teams, and do project management — engineers hide behind them. "The PM didn't prioritize that work, so we didn't address the tech debt." This gives engineering an out for things they should own.

Engineering management must **co-own the work plan**. PMs are not glorified scrum masters. Product management is about shaping strategy, not managing sprints. The "product owner" role in Agile (focused on backlog grooming, short-term prioritization, status reporting) is explicitly insufficient for platform product work.

> **[Anti-Pattern: The PM-as-Scrum-Master Trap]**
>
> This happens most commonly when companies hire product managers for internal platform teams by promoting technical program managers (TPMs) into PM roles. TPMs are excellent at execution (tracking work, unblocking dependencies, reporting status) but less experienced with ambiguous strategic decisions.
>
> **Signs you're in this trap:**
> - PM's weekly report is mostly "status of tickets in progress"
> - PM spends more time in sprint ceremonies than talking to customers
> - Engineering says "ask the PM what we should work on" for everything, including tech debt
> - Nobody can articulate the platform's product strategy beyond "deliver the roadmap"
>
> **The fix:** Separate execution (project management, sprint mechanics, status tracking) from strategy (product vision, user research, prioritization framework, market analysis). PMs should spend the majority of their time on strategy. If they're spending >50% on execution mechanics, you either need a TPM to handle that, or you need to simplify your execution process.

---

## Wrapping Up

The authors categorize platform product failures into three broad categories:

| Category | Failure Mode | Symptom |
|----------|-------------|---------|
| **Culture** | Team fails to adopt product culture | Expects users to tell them what to build; focuses on technology/operations over customers |
| **Product-market fit** | Fails to evaluate ideas against internal market needs | Builds things customers don't want; no impact metrics to clarify opportunity |
| **Execution** | Doesn't align work with product strategy | Ignores migration/change overhead costs; misuses PMs for engineering management work |

The authors close with an important acknowledgment: **great products are always situational.** There's no surefire recipe. Success comes from deep insight into what people need, combined with understanding of what's realistic to build. Platform engineering doesn't have to be the *source* of product innovation — many of the best ideas will come from other teams. The platform team's job is to not "completely drop the ball of customer focus and product discipline in favor of technical and operational concerns."

> **[AI Impact: AI and Platform Product Management]**
>
> AI affects platform product practices in several ways:
>
> **Faster prototyping for product discovery:** When the platform team wants to test whether a new offering has demand, AI coding tools let them build functional prototypes faster — reducing the cost of "partner to prototype" experiments. This means more hypotheses can be tested before committing to a full product investment.
>
> **AI-assisted market research:** Rather than manually surveying teams, AI can analyze existing signals (support tickets, Slack conversations, code review comments, incident reports) to identify unmet needs at scale. "43% of incidents in Q4 involved manual database failover" → strong signal for automated failover as a platform product.
>
> **Roadmap communication:** AI can help translate between internal technical roadmaps and customer-facing communications — generating clear, non-technical explanations of what's coming and why. This reduces the communication burden that often keeps platform teams from sharing their plans.
>
> **Change budget estimation:** AI analyzing historical adoption patterns can predict how much change capacity exists in the organization — "Based on past patterns, engineering teams typically complete 2 major platform migrations per year. You're already planning 3 — one will likely slip."
>
> None of these replace product judgment. But they reduce the effort required to gather inputs for product decisions — making it more likely that platform teams actually do the product work rather than skipping it because "we don't have time for user research."
