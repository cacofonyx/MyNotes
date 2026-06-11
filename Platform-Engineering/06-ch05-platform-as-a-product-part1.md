# Chapter 5: Platform as a Product — Part 1: Culture and Discovery

> **Part II — Platform Engineering Practices**

> *"What's an internal platform but an external platform being built in a hypoxic, lightless, dungheap of an environment?"* — Coda Hale

This is the book's longest chapter, and for good reason — the authors believe that adopting a product mindset is the single hardest and most important transformation for platform teams. Many teams interpret "platform as a product" as simply "hire product managers." The authors argue this is like saying "become a restaurant by hiring a chef" — there's a lot more to it than one role. The entire team needs to adopt a product culture: understanding customers, measuring outcomes, making strategic trade-offs, and resisting the gravitational pull toward feature shops and relationship-based decision making.

Part 1 covers: product culture (understanding and empathizing with internal customers), product discovery (finding what to build), market analysis (validating investments), and metrics (knowing if you're succeeding). Part 2 covers: roadmapping, execution practices, and common failure modes.

## Table of Contents

- [Product Culture Focuses on the Customer](#product-culture-focuses-on-the-customer)
  - [Characteristics of Internal Customers](#characteristics-of-internal-customers)
  - [Collaborating with Internal Customers](#collaborating-with-internal-customers)
  - [Empathizing with Customers](#empathizing-with-customers)
  - [Escaping the Feature Shop Trap](#escaping-the-feature-shop-trap)
- [Product Discovery and Market Analysis](#product-discovery-and-market-analysis)
  - [Identifying Potential Platform Products](#identifying-potential-platform-products)
  - [Evolving Existing Offerings: Smoothing Edges vs. Rethinking the Problem](#evolving-existing-offerings-smoothing-edges-vs-rethinking-the-problem)
  - [Market Research: Validating New Investments](#market-research-validating-new-investments)
- [Product Metrics](#product-metrics)

**Block types:** [Core Concept] [Deep Dive] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [AI Impact]

---

## Product Culture Focuses on the Customer

The first step to creating a product culture is understanding and appreciating your customers. This sounds obvious — but internal customers are deceptively tricky to work with. They're your colleagues. You see them every day. But that proximity doesn't mean they can articulate what they need, that they'll adopt what you build, or that keeping them happy means doing everything they ask.

The authors insist on calling internal users **"customers"** rather than "stakeholders" — because the word *customer* implies obligations. You owe them a product that works well. You're responsible for their experience. The word *stakeholder* implies a political relationship to manage, not a product to deliver.

### Characteristics of Internal Customers

The authors identify five characteristics that make internal customers uniquely challenging:

**1. Small customer base.** You might have hundreds of users, not millions. A/B testing with an audience of hundreds doesn't teach you much. Metrics-driven strategies are harder — you need to be more thoughtful about what you measure to ensure you're capturing real signals, not noise.

**2. Captive audience.** Your platform may be the only option — application teams can't always "just build their own." This creates two failure modes:
- You ignore adoption metrics because "they have to use us anyway" — and fail to notice you've built something useful to only a tiny subset
- You use adoption as a stick to *force* usage of a system that doesn't work for them — mandating without quality

Neither is acceptable. "Having a captive audience doesn't excuse you from the work of building something they need and want."

**3. Conflicting incentives.** Internal customers may also be the ones whose budget pays for your team. They see your headcount and think "what could I do with that budget instead?" They may expect bespoke features or developer loans in exchange for "funding" you. This creates transactional dynamics that poison the product relationship.

**4. Customer happiness is a moving target.** Internal customers quickly take improvements for granted. The minute you remove one bottleneck, they focus on the next. New hires arrive with fresh expectations — they don't know how much worse things were a year ago. Customer satisfaction is often "simple indifference" — nobody praises the plumbing until it breaks.

**5. Customers as competitors.** When internal customers are engineers and you can't keep up with their needs, they'll build their own solutions rather than wait. Staying ahead of their needs — and making it clear that waiting for your team is better than rushing ahead alone — is an ongoing challenge.

> **[Organizational Reality: The Captive Audience Trap]**
>
> The captive audience dynamic is one of the most damaging things about internal platform work. It removes the market discipline that forces external products to be good.
>
> **In the external world:** If your product sucks, customers leave. Revenue drops. The feedback loop is immediate and unambiguous. You MUST be good to survive.
>
> **In the internal world:** If your platform sucks, customers... keep using it. They have no choice. They complain in Slack. Morale degrades slowly. Leadership gets vague reports of "developer productivity issues" but nothing as clear as "revenue dropped 30%." The platform team can coast for *years* on a captive audience before the consequences become visible enough for leadership to act.
>
> **How to fight this:** Treat voluntary adoption as your primary metric even when you have a captive audience. Track "what percentage of potential users are *happily* using this platform?" not just "what percentage of users are using this platform." Run satisfaction surveys. Watch for shadow platforms (teams building their own solutions). If teams are going off-platform despite having no formal alternative — that's the equivalent of customers churning, and it should scare you just as much.

### Collaborating with Internal Customers

The authors draw a sharp distinction between two models:

**The "relationship model"** (common, but wrong for platforms): Build exactly what customers ask for, as fast as possible, to maintain the relationship and keep stakeholders happy. Shield yourself from blame by delivering precisely what was requested.

**Why this fails for platforms:**
- Engineering teams "don't precisely know what they want." Even if you build exactly what they asked for, they might not adopt it.
- When they don't adopt it (despite asking for it), *you* still get blamed: "too slow," "didn't prioritize right," "we moved on to other concerns."
- Platforms serve *many* similar-but-not-identical customers. You can't faithfully comply with every individual team's requests and get something broadly useful.

The alternative: **look at revealed preferences** (how people actually use systems, what tasks they perform) rather than stated preferences (what they say they want). Understand what customers are *actually doing* and derive plans from observation, not just asking.

> **[Core Concept: Stakeholder Management ≠ Product Management]**
>
> The authors make this distinction explicit because so many platform teams conflate the two:
>
> **Stakeholder management** = horse trading, power structure appreciation, CYA. Making the most important person happy. A political act. You can have excellent stakeholder management and build crappy products — stakeholders vaguely feel dissatisfied but signed off on everything, so they're part of the problem.
>
> **Product management** = figuring out what the company actually *needs*, based on deep understanding of current and future demands, and shaping the product to meet those needs in measurable ways. It's risky — you're making bets about what to build — which is why impact metrics matter (to show whether your bets paid off).
>
> Both are necessary. You can't ignore stakeholders (Chapter 10 covers this). But don't substitute stakeholder management for product management. Many platform teams that claim to be "product-focused" are actually just managing up — keeping powerful people happy without building great products.

**Practical advice for asking better questions:** Don't ask "Do you want a system that is near real-time?" (everyone says yes). Ask "How quickly do you need to be able to do X while using this system?" — this reveals what's actually necessary vs. what sounds nice, and often leads to a much simpler design.

### Empathizing with Customers

Building customer empathy is a coaching and culture challenge. The authors provide a practical checklist:

- **Interview for empathy** (as discussed in Chapter 4)
- **Set customer-focused goals** — not just technical delivery but adoption, satisfaction, engagement metrics
- **Bring users to team meetings** — honest feedback, kudos, real problems
- **Have PMs present user research regularly**
- **Put engineers on support rotation** — nothing creates empathy like seeing users struggle with your product

Key measurement questions to ask:
- "If this makes people more productive, how much time will it actually save? How do you know?"
- "How many hours a year do customers spend reacting to our upgrades and migrations?"
- "Are support requests about common repeated issues (bad UX/docs) or unusual situations (healthy state)?"

> **[Deep Dive: Customer Empathy Is Not Customer Obedience]**
>
> The authors make a subtle but critical point: empathy means *understanding* customers, not *obeying* them.
>
> When the team adds PMs, engineers sometimes pull back entirely from customer interactions — "that's the PM's job now." This is a step backward. PMs are one input, not the sole voice. Engineering partners still need direct customer contact, especially for technically complex decisions.
>
> Equally, empathy doesn't mean building whatever customers ask for. It means understanding the *problem* behind their request, then applying engineering judgment about the best *solution*. A customer says "I need feature X." Empathy means understanding why — and then possibly solving their underlying need with feature Y that also helps 10 other teams, rather than building X as a one-off.

### Escaping the Feature Shop Trap

The Feature Shop Trap is the culmination of everything that goes wrong with internal customer relationships. A platform team ends up doing nothing but triaging feature requests across customers, unable to deliver a strategic product roadmap.

**How it happens (example: cloud enablement platform):**
1. Platform team helps teams adopt new cloud services — a hands-on enablement role
2. Demand spikes (company-wide cloud push). Team goes into triage mode.
3. Political pressure arrives: important leaders want *their* services prioritized. Others complain about fairness.
4. Team invents "fair share algorithms" for prioritization (each org picks what they want).
5. All PM time goes to picking and justifying individual work items. No time for strategy.
6. Team is trapped in "enablement request Tetris with no end in sight."

**Two root mistakes that create the trap:**
1. Scaling adoption before architecture is ready to handle demand (self-service isn't built)
2. Assuming that because customers give precise requests, the best response is faithful compliance

**How to escape:** Don't implement individual feature requests. Look at the *patterns* they represent. Ask: "How can the platform evolve so that categories of features can be unlocked by customers themselves?" Build self-service capabilities that address classes of requests rather than individual ones.

> **[Anti-Pattern: The Feature Shop — Detailed Anatomy]**
>
> You're in a feature shop if:
> - Your backlog is 100% customer requests, 0% strategic platform work
> - You can explain every item in your roadmap as "Team X asked for this"
> - You've never said "no" to a request — just "not yet" (which is functionally the same as "never")
> - Your PMs spend all their time prioritizing the queue rather than thinking about what the platform should become
> - You're adding the same type of feature over and over (variant for Team A, variant for Team B, variant for Team C) instead of building a general capability
>
> **The lazy engineer test** (from the authors): "Do you really want to implement variants of the same thing over and over? If you were a user, would you want to wait for the platform team before you could proceed? How can you approach your offering to allow others to plug their code in?"
>
> **The strategic fix:** Before releasing a new product, anticipate how demand will follow successful adoption. What should the platform support users building *for themselves*, and what should it provide *for everyone*? "A good platform takes on and gets rid of common tasks for many customers, rather than providing bespoke implementations for a few."

---

## Product Discovery and Market Analysis

### Identifying Potential Platform Products

The authors describe platform teams as **"settlers and town planners"** rather than pioneers. They take ideas successfully pioneered by smaller groups and expand them to broad usefulness. Four approaches to finding new products:

**1. Assimilate and expand.** Take over a system that another team built for themselves, if it solves a problem worth solving broadly. "You already have a reasonably satisfied customer base to start with!" Many platform teams resist this because they don't want to live with others' decisions — but they forget they're getting proven product-market fit for free.

**2. Partner to prototype.** Embed engineers in a customer team to understand a problem. Build a prototype together. Extract the generalizable parts into a platform offering. Key risk: don't become a "solutions engineering team" that builds bespoke things forever without creating broad-use products.

**3. Look for products with realistic paths to adoption.** The product work isn't just building something — it's figuring out the migration strategy. "Despite having captive audiences, platform teams are notorious for creating half-finished product offerings that somehow fail to get adopted." If you can't find compelling customer benefits that encourage voluntary adoption, your company may not have real demand for this product.

**4. "You aren't Google, so don't build when you don't have to."** Don't imitate big-company systems just because they're popular or open-sourced. Those solutions encode assumptions about ecosystems and cultures you don't have. Start with a clear understanding of *your* problem, *your* ecosystem, *your* culture — then decide whether building is the right answer. Often, a conversation with the top data producers or a bit of query tuning solves what seems like a storage scaling problem.

> **[AI Impact: AI Changes Product Discovery for Platforms]**
>
> AI introduces new dynamics to the "how do you find what to build?" question:
>
> **AI as a discovery tool:** LLMs can analyze support tickets, Slack messages, and incident postmortems at scale to identify patterns that humans might miss. "72% of support questions in Q4 were about networking configuration" — this signal can emerge from AI analysis of unstructured text, pointing the platform team toward their highest-leverage product investment.
>
> **AI-generated prototypes:** The "partner to prototype" approach gets faster when AI can generate initial implementations. A platform engineer can prototype a batch job platform in days rather than weeks using AI coding assistants — getting to the "proof of concept" stage faster and cheaper, which means more experiments can be tried before committing to a full build.
>
> **The "You aren't Google" principle applies to AI too:** Every company is hearing "you need an AI platform" — but most don't yet have the scale or use cases to justify one. Apply the same discipline: start with a clear understanding of the problem, evaluate whether a managed service solves it, and build only when you've exhausted alternatives.

### Evolving Existing Offerings: Smoothing Edges vs. Rethinking the Problem

> *"If I had asked people what they wanted, they would have said faster horses."* — Henry Ford (maybe)

When deciding how to evolve an existing platform, there are two fundamentally different approaches:

**Smoothing the edges:** Make existing things easier — performance improvements, better UX, cleaner integrations. Important when optimizing human-in-the-loop processes that involve collaboration.

**Rethinking the problem:** Don't just make something easier — ask whether users need to think about it *at all*. Can you remove their need to manage this task entirely? This usually means operating something on their behalf and providing a rock-solid abstraction.

**The authors' decision framework:**

| Signal | Approach |
|--------|----------|
| Optimizing a human-in-the-loop process with multiple collaborators | **Smooth the edges** — reduce context switching, highlight work, improve UX |
| Supporting machine processes and data | **Rethink** — operate a platform that manages these, don't write playbooks |
| The human doesn't have to be in the loop | **Rethink** — remove the human's work entirely (e.g., decouple auth into a sidecar) |
| Creating a meta-platform combining many existing activities | **Smooth the edges** — great UX wrapping underlying complexity (the Heroku model) |

> **[Core Concept: The Rethinking Test — "Can We Remove the Need to Think About This?"]**
>
> This is one of the most powerful product questions a platform team can ask. Examples:
>
> - **Edge-smoothing:** "Make Kubernetes YAML easier to write" (give them templates, a generator, better docs)
> - **Rethinking:** "Make developers never write Kubernetes YAML" (they describe intent, the platform generates all config)
>
> - **Edge-smoothing:** "Make database upgrades less painful" (better runbooks, compatibility testing tools)
> - **Rethinking:** "Make database upgrades invisible to users" (platform handles upgrades transparently behind the API)
>
> - **Edge-smoothing:** "Make TLS certificate management easier" (dashboards showing expiry, CLI for renewal)
> - **Rethinking:** "Make TLS certificate management automatic" (platform provisions and rotates certs, users never think about it)
>
> Rethinking requires you to own the full operational lifecycle of whatever you're removing from users' plates. Many teams fail to deliver true platforms because they don't want to own that operation. But this is precisely where platform leverage comes from — and it's what justifies a dedicated platform team.

### Market Research: Validating New Investments

Before building something new, validate that there's real demand. The authors provide a structured approach:

**1. Does the context match?** Solutions from other companies encode undocumented assumptions about their ecosystem, culture, and scale. What works at Google may not work for you — and what Google open-sourced may rely on 10 other internal systems that weren't open-sourced.

**2. Who are you targeting?** Identify personas. Estimate how many teams would use this. Find alpha testers willing to sponsor the initiative.

**3. What's the appetite for immediate adoption?** Consider:
- Onboarding cost for customers
- Whether migration is required (and whether customers will do it)
- Whether the offering is only useful for new applications (how many are planned?)

**The market analysis checklist:**
1. Verify potential user base
2. Quantify potential benefit
3. Present adoption cost to potential users
4. Estimate how quickly users can migrate and see benefits
5. Evaluate user willingness
6. Take into account current budget climate

> **[Organizational Reality: "Adoption Drag" — Why Good Products Still Fail]**
>
> The authors identify a pattern that surprises many platform engineers: you build something genuinely good, but adoption is painfully slow. The reason isn't quality — it's adoption drag:
>
> - Users are busy with their own roadmaps and can't prioritize migration
> - The benefits are real but not urgent enough to justify the switching cost
> - Budget climate changed between "yes we'd love that" and "time to actually adopt it"
> - Other teams' migrations compete for the same change budget
>
> This is why the authors emphasize measuring *willingness* and *budget climate* alongside technical merit. A platform team that ships a great product nobody has time to adopt has a product management failure, not an engineering success.

---

## Product Metrics

The authors bring in **Leif Walsh** (senior platform product manager) to discuss metrics. The key insight: platform engineers naturally gravitate toward operational metrics (throughput, latency, error rate). But product strategy needs higher-level metrics about *users* — their behaviors, their outcomes, whether the platform is making their work better.

**Four high-level metrics every platform should track:**
1. **Cost of using the platform:** How much migration/adoption overhead do you impose?
2. **Benefit of adopting the platform:** How much time or money are you saving users?
3. **Customer demand:** What percentage of potential users voluntarily adopt?
4. **Customer opinion:** CSAT/NPS score for the platform?

**Three types of metrics:**
- **Impact metrics** — explain effectiveness of teams and projects upward. Provide targets to focus engineers.
- **Guardrail metrics** — prevent tunnel vision on impact metrics. (DORA example: change failure rate guards against optimizing only for deployment frequency.)
- **General product health** — find opportunities, detect at-risk products, prioritize.

**Impact metrics require an "impact theory"** — a hypothesis about cause-and-effect. Example: "If we improve storage throughput → data science runs more experiments → better recommendations → more engagement → more revenue." You collect metrics at interesting nodes in this causal graph to verify (or falsify) your theory and adjust strategy.

> **[Comparison: DORA Metrics Connection]**
>
> The authors' guardrail metric concept comes directly from the DORA framework (Accelerate):
> - Deployment frequency and lead time measure *speed*
> - Change failure rate and MTTR measure *stability*
> - Each guards against over-optimizing the other
>
> For platform teams, analogous pairs might be:
> - "Time to provision" (speed metric) guarded by "percentage of provisions with misconfigurations" (stability metric)
> - "Number of new platform features shipped" (output metric) guarded by "platform availability" (reliability metric)
> - "Adoption rate of new offering" (growth metric) guarded by "satisfaction score of existing users" (retention metric)
>
> The principle: never track a single metric in isolation. Every metric that encourages one behavior needs a guardrail that prevents that behavior from going too far.

**Practical advice on getting metrics from your team:**
- Engineers will first offer throughput/latency/error rate. Ask "Why is that important?" to get to higher-level questions.
- Start where the team is comfortable, then iterate toward what you actually need to make product decisions.
- Frame initial metrics as a prototype to be refined — overcomes resistance from engineers who fear misuse.
- Document schemas and data generation processes — prevents misinterpretation later.

*→ Continued in Part 2: Product Execution, Roadmaps, and Failure Modes*
