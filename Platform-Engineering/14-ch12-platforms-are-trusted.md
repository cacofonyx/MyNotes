# Chapter 12: Your Platforms Are Trusted

> **Part III — What Does Success Look Like?**

> *"Trust is like the air we breathe — when it's present, nobody really notices; when it's absent, everybody notices."* — Warren Buffett

After the internal focus on building alignment (Chapter 11), this chapter turns outward: earning the trust of everyone else. The authors argue trust must come *before* results, not after them. Platforms in production today need customer trust — in the form of patience and partnerships for testing, validation, and adoption — to deliver improvements. Without trust, a single unfortunate event can render carefully crafted product roadmaps useless, forcing throwaway work to manage a crisis.

The chapter identifies three ways platforms lose trust: operational failures at the scale customers need, big investments made without buy-in, and becoming a bottleneck to business delivery. For each, the authors provide tactical remedies drawn from extended real-world examples — including the "Icicle" team stalemate over high-performance compute and Diego Quiroga's turnaround of a team on the brink of becoming a business bottleneck.

The chapter culminates in the "Case of the Overcoupled Platform" — a detailed story of how a "batteries included" philosophy led to deep coupling, v2 rewrites, and dissipated trust, and how the pivot to "building blocks, not batteries included" corrected course by stabilizing, decoupling, and providing composable abstractions that prioritized stability and flexibility over polished usability.

## Table of Contents

- [A Success Red Herring: Trust in a Leader vs. Trust in the Platform](#a-success-red-herring-trust-in-a-leader-vs-trust-in-the-platform)
- [Trust in How You Operate](#trust-in-how-you-operate)
  - [Accelerate the Curve: Hire and Empower Experienced Leaders](#accelerate-the-curve-hire-and-empower-experienced-leaders)
  - [Optimize the Curve: Order Use Cases by Tolerance](#optimize-the-curve-order-use-cases-by-tolerance)
- [Trust in Your Big Investments](#trust-in-your-big-investments)
  - [Seek Technical Stakeholder Buy-in for Rearchitectures](#seek-technical-stakeholder-buy-in-for-rearchitectures)
  - [Seek Executive Sponsorship for New Products](#seek-executive-sponsorship-for-new-products)
  - [Maintain Old Systems to Retain Trust](#maintain-old-systems-to-retain-trust)
  - [Gaining Trust Requires Flexibility on "Right"](#gaining-trust-requires-flexibility-on-right)
- [Trust to Prioritize Delivery](#trust-to-prioritize-delivery)
  - [Create a Culture of Velocity](#create-a-culture-of-velocity)
  - [Prioritize Projects to Free Up Capacity (Diego Quiroga)](#prioritize-projects-to-free-up-capacity-diego-quiroga)
  - [Challenge Assumptions About Product Scope](#challenge-assumptions-about-product-scope)
- [Tying It Together: The Case of the Overcoupled Platform](#tying-it-together-the-case-of-the-overcoupled-platform)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Anti-Pattern] [Organizational Reality] [SRE/Production Lens] [Comparison] [Worked Example] [Real-World Implementations]

---

## A Success Red Herring: Trust in a Leader vs. Trust in the Platform

> **[Anti-Pattern: The Benevolent Dictator]**
>
> One of the worst management mistakes: when the team leader oversteps their role as facilitator and personally makes ALL calls — management, engineering, and product decisions.
>
> **Why it's seductive:**
> - Seems efficient with a small team and few users
> - Leader uses 1:1 meetings to understand all conflicts
> - Short-circuits lengthy trade-off documents and contentious meetings
> - Provides fast decisions with clear accountability
>
> **Why it's brittle:**
> - Only works because ONE person with deep expertise has time for regular conversations with ALL users and stakeholders
> - Once the number of customers grows too large for one person, or that person moves on (often burned out), you're left with NO decision maker AND no trust
> - The team has to start from scratch building group mechanisms — months or years to figure out how to negotiate decisions
>
> **The lifecycle:**
> 1. **Scrappy/scalable stages:** Pioneer or settler mindset leader making fast decisions — this IS appropriate here
> 2. **Growth stage:** Must start delegating — will slow decision-making in the short term
> 3. **Mature stage:** Stakeholders trust the whole team, not just one person — sustainable for the long term
>
> **The leadership challenge:** If you are such a leader, challenge yourself to delegate. Your stakeholders will resist it. You will resist it. But you're building long-term trust in the team at the cost of short-term velocity.

---

## Trust in How You Operate

You can tick all the boxes (on-call rotations, SLOs, change management, operational reviews) and still lack operational trust from senior application engineers. Before migration: standoffs, prolonged timelines, demands for vague "proofs of concept." After adoption: pressure to build "simpler" shadow platforms.

**The root challenge:** "There is no compression algorithm for experience. You can't learn certain lessons without going through the curve." You only get good at operating foundational systems at scale by operating foundational systems at scale.

> **[Core Concept: Two Levers for Operational Trust]**
>
> | Lever | Mechanism |
> |-------|-----------|
> | **Accelerate the curve** | Hire and empower leaders with operational experience at scale |
> | **Optimize the curve** | Order new use cases based on tolerance for operational risk |
>
> These are not shortcuts — they're ways to move faster up a curve you still must traverse.

### Accelerate the Curve: Hire and Empower Experienced Leaders

**Camille's first platform job:** Team inherited was struggling with operational stability. Systems built scrappily, grown without investment in improvements. But all ingredients to solve the problem were already there: talented experienced managers, strong engineers, CTO support.

**Camille's contribution was empowerment:**

1. **The Operational Excellence OKR:** Historical OKRs focused only on new capabilities. She established an objective of improving operational stability with measurable key results from each leader.

2. **Broad communication:** Shared at engineering OKR town hall, team all-hands, and executive management quarterly reports.

3. **Ownership delegation:** Assigned this objective to up-and-coming leaders, giving them cross-organization leadership opportunities.

4. **Evidence for impact:** Tracked OKR provided evidence for promotion conversations that had previously only valued feature delivery.

**Outcomes:**
- Customer satisfaction surveys showed measurable improvements
- On-call burden became more manageable (team happiness improved)
- Senior conversations moved from blaming platforms for operational failures to collegial discussions about new opportunities

> **[SRE/Production Lens: The Operational Excellence OKR]**
>
> This is a powerful pattern because it solves multiple problems simultaneously:
>
> - **Creates permission** for managers to explain to stakeholders why they're doing stability work instead of features
> - **Makes the work visible** so the team takes it seriously
> - **Provides promotion evidence** — historically, only feature delivery counted. Now operational excellence has measurable impact artifacts.
> - **Attracts the right talent** — engineers who care about operational quality see it valued and recognized
>
> **The SRE parallel:** This is essentially what Google's SRE book calls "error budget policy" at the organizational level — creating structural permission and incentive to invest in reliability over features. The difference: instead of an automated budget, it's a leadership-driven cultural mandate backed by OKR tracking.

### Optimize the Curve: Order Use Cases by Tolerance

**The premature adoption problem:** Compute and storage platforms were new. Teams wanted to drive adoption to prove value. But they hadn't done enough performance testing to understand actual (vs. theoretical) SLOs. When applications tried to migrate, systems struggled to meet performance needs. Even controlled PoC failures fed into lack of trust.

**The solution: Use performance sensitivity as a lens for ordering adoption.**

Instead of considering an offering "done" with one customer onboarded, the teams took a staged approach:
1. Start by onboarding less critical applications (internal workflows that tolerate some latency/downtime)
2. Use these applications for performance tuning and bug fixes
3. Use improvements to gain trust of the next tranche of more critical use cases
4. Repeat

> **[Comparison: Push vs. Pull Adoption Models]**
>
> | Push model (broken) | Pull model (trust-building) |
> |--------------------|-----------------------------|
> | "Our platform is ready, migrate now" | "Here's what we can guarantee today" |
> | Performance failures destroy trust | Less critical apps provide data for tuning |
> | One failure = "platform isn't ready" narrative | Each success = trust for the next tier |
> | Adoption metric drives behavior | Operational confidence drives behavior |
>
> The key insight: there are no shortcuts to scaling operational ability. But empowering the right leaders who put trust ahead of adoption moves you faster up the curve.

---

## Trust in Your Big Investments

Big investments (new platforms, major rearchitectures) require enormous faith ahead of demonstrated value. They pull developers away from delivering faster value on current platforms. Customers waiting on results will accuse the team of "resume-driven development" — putting fancy technologies ahead of more mundane work providing immediate business value.

**The trust failure cascade:**
1. Skip getting buy-in ("Trust me, this is important")
2. Users come with pain points; you say "can't help, we're rearchitecting"
3. Users complain upward
4. Senior stakeholders ask pressing questions about your strategy
5. Your entire roadmap gets flipped over

### Seek Technical Stakeholder Buy-in for Rearchitectures

Spend time explaining to stakeholders what you're doing and WHY *before* starting work. Produce a formal decision-making process (Chapter 8) generating a record showing not just justifications but that your teams are held to high standards for such justifications.

Management stakeholders are satisfied by evidence of strict vetting. **Senior ICs want more** — particularly around technical decisions. Even without a company-standard RFC process, produce a yearly project proposal (Chapter 7).

**The Amazon principle applies:** If you don't let senior engineers in customer teams give feedback before you start, don't expect them to "shut up and commit" when you later push for adoption.

### Seek Executive Sponsorship for New Products

New products present an opportunity to get executive sponsors who bring bigger-picture business perspective. Platform leaders often focus on technical goals (scale, operate, reduce costs) in a vacuum, forgetting:
- These engineers could be building other things (high opportunity cost)
- The existence of a new platform isn't an outcome
- Other leaders may have different views on what matters (not everyone cares about the same thing)
- Their technology strategy may diverge from your assumptions

### Maintain Old Systems to Retain Trust

Even with stakeholder buy-in, big investments are high-risk. Executive sponsorship lasts only so long. For projects taking 12+ months:

- Get out of the mindset that legacy improvements are "pointless throwaway work"
- Keep investing in system improvements until load on the old system is *significantly* falling
- This is not just basic KTLO — add new features to accommodate urgent business needs or mollify customers

> **[Organizational Reality: The Trust Cost of Neglecting Legacy]**
>
> No matter how confident you are in the big investment, others will have reasonable doubts. If you don't give ground on maintaining old systems in the meantime, you lose trust.
>
> **The emotional dynamic:** Customers stuck on the old system while watching the platform team build shiny new things feel *abandoned*. Every bug they hit becomes evidence that the platform team doesn't care about them. The new system becomes a symbol of the platform team's ego rather than an investment in the future.

### Gaining Trust Requires Flexibility on "Right"

> **[Worked Example: The Icicle Team Stalemate]**
>
> **Context:** Ian's compute platform team was digging out of operational instability. One business-critical team ("Icicle") had a workload extremely sensitive to performance latency. They'd historically solved this with highly customized bare-metal servers — low utilization, high cost.
>
> **The stalemate (technical framing):**
> - Icicle's business leadership wanted better cost efficiency
> - But they trusted their engineering team's judgment over the platform team's
> - The platform's cost reduction approach (oversubscription) caused unpredictable latency — unacceptable to Icicle
> - Compute team wanted "hard SLOs" from Icicle to design a solution
> - Icicle wanted an extensive "stress test engine" to prove platform performance
> - Result: low trust, Icicle proposed staffing their own shadow platform team
>
> **The resolution (product strategy change):**
> 1. Ian's team changed not just their roadmap but their *product strategy*
> 2. Created a new offering that **ripped out all oversubscription features** — more expensive than the standard offering, but still a substantial improvement over bare metal
> 3. Even with this concession, Icicle engineering team remained unconvinced
> 4. Platform team first shipped to data science users — delivered improved performance to a highly visible business group, built confidence through demonstrated operational success
> 5. After **six months** of demonstrated success, earned enough trust for Icicle to commit to migration
>
> **Key insight:** By being flexible on what is "right" (accepting higher cost to remove the unacceptable latency risk) and showing operational commitment through a staged rollout, the team moved past a stalemate that was fundamentally about lack of trust. The technical answer wasn't the blocker — trust was.

---

## Trust to Prioritize Delivery

Platforms that bottleneck business delivery clearly have questionable leverage *in that moment*. Even when the work is understood to be difficult (e.g., standing up platforms on a new cloud vendor), people outside the platform team underestimate complexity. As the bottleneck drags on, they question every aspect of decision making — sometimes the utility of the platform entirely.

Three activities to avoid bottlenecks: velocity of delivery, prioritization, and challenging product scope assumptions.

### Create a Culture of Velocity

When stakeholders blame bottlenecks on "lack of planning," they may have a point — if you haven't done any planning. But in the face of an agile and dynamic business, planning alone doesn't solve all trust issues.

**Why "wait until next quarter's OKRs" is destructive:**
- If application teams have two-week iteration cycles, a platform team insisting on quarterly planning destroys momentum
- You waste their time seeking clarity of value the business cannot provide
- You create a culture blaming the business for not providing perfect roadmap requirements — which is a *fact of life*, not a fault

> **[Core Concept: Balancing Throughput with Responsiveness]**
>
> Ian's approach when leading a platform organization crucial to application teams' dynamic needs:
>
> - **Goal 1:** Stress to his team that it was NOT acceptable to resist a new application ask just because it wasn't in earlier plans
> - **Goal 2:** Remind stakeholders that not telling his team early about their needs would result in higher costs (because the plan would have to change)
>
> This is the core tension of platform velocity: you cannot be purely responsive (that's chaos) or purely planned (that's waterfall). The culture must hold both values simultaneously.

### Prioritize Projects to Free Up Capacity (Diego Quiroga)

> **[Worked Example: Diego Quiroga's Bottleneck Turnaround]**
>
> **Context:** Small platform team managing foundational services for an enterprise social network. Application teams relied on diverse capabilities to build features. Each quarter, asks exceeded capacity; backlog grew. Previously, the team had compromised operations investment to tackle the backlog — leading to increased on-call burden AND negative perceptions of operational stability.
>
> **The diagnosis:** With fixed headcount as a constraint, analyzed a year of customer requests seeking patterns. Found several recurring requests (e.g., configuration changes across a complex chain of services to establish new feeds) that could be packaged as self-service.
>
> **The challenge:** Making the case for team efficiency investment while being an active bottleneck. Balancing immediate feature value against a promise of increased throughput was a tough sell. **Critical success factor:** demonstrating impact with clear visuals and metrics to maintain leadership trust.
>
> **Results:**
> - Requests that previously demanded a platform engineer's undivided attention for an entire month now required only a few consulting sessions
> - Similar strategy applied to support requests: troubleshooting dashboards, self-diagnosis tools, and "canned responses" directing users to documentation reduced 30 weekly support requests
> - Freed capacity allowed consistent addressing of performance and reliability issues
> - Team established a reputation for operational excellence
> - Engineers got more interesting, impactful, high-leverage work (engagement increased)
>
> **Key insight:** In a scenario where a long-term roadmap from application teams isn't available, relying on past trends for investment decisions is a calculated bet. "Absolutely critical in transitioning us from being a bottleneck for the business to being its trusted foundation."

### Challenge Assumptions About Product Scope

Some platforms have characteristics that create *inherent* bottlenecks:
1. Large surface area of functionality
2. Diverse set of applications to support
3. Can't trust users to unblock themselves

**Classic example:** Centralized cloud enablement team charged with ensuring developers can access cloud offerings quickly AND significant security vetting of offerings and usage patterns.

**The scope reduction approach:**
- Instead of unlocking cloud primitives for everyone, build platforms that orchestrate compute and storage for major use cases
- Provide a smaller but focused surface area
- Platform team makes the right choices about underlying cloud infrastructure management
- Integrate core company concepts (identity management, security)
- Handle cloud complexity on behalf of users

> **[Core Concept: Four Questions for Managing Platform Scope Bottlenecks]**
>
> Where you build platforms to enable users without granting too much trust:
>
> 1. **Have you considered limiting scope** by supporting only certain types of applications?
> 2. **Have you iterated to identify the right abstraction** that supports customers without exposing such a large surface area?
> 3. **Have you designed a system where users can contribute to unblocking themselves** by limiting control points requiring security/compliance review?
> 4. **Have you included extensibility mechanisms** for some platform features to be augmented by users themselves?
>
> You may need all four: limited scope with good abstractions for common cases, and better practices for extensibility and user-driven contributions for the edges.

---

## Tying It Together: The Case of the Overcoupled Platform

> **[Worked Example: From "Batteries Included" to "Building Blocks"]**
>
> **The starting point:** A two-year push for "batteries included" platforms — a reaction to a prior generation of siloed benevolent dictators whose platforms didn't work together. The vision: heavily aligned approach where platforms enabled "workflows," customers didn't have to build things themselves, operations was invisible underneath.
>
> **Why it sounded ideal:**
> - End-to-end focus (the Apple products analogy)
> - Customers use platforms without building anything themselves
> - Operations of underlying systems hidden from users
>
> **What went wrong:**
> - The high bar of "batteries included" meant designing end-to-end workflow impact for EVERY use case before writing code
> - Initial offerings took shortcuts → everything became deeply coupled
> - Deep coupling made rearchitectures especially hard
> - Teams decided they needed v2 rewrites to deliver architectural improvements with feature innovations
> - Ambitious v2 scopes caused massive delays and increasing frustration
>
> **The trust failure:** While "batteries included" was a great trust unifier in early days of close collaboration, as delivery ground to a halt and the only solution was more v2s, trust dissipated. Stakeholder feedback: "your organization builds new platforms for the sake of building new platforms."
>
> **The correction — "Building Blocks, Not Batteries Included":**
>
> | Principle | Meaning |
> |-----------|---------|
> | **Building blocks are foundational** | Pause workflow features to make blocks solid. Fix component-level integration → use well-defined APIs. Poorly defined interfaces led to systems difficult to change, test, and monitor. |
> | **Blocks are composable** | Component coupling slowed feature delivery AND precluded advanced customers from building their own workflows. Individual platform abstractions isolate side effects. Trusted customers can "pierce" the workflow abstraction and unblock themselves. |
> | **Blocks can be switched out incrementally** | Proposals evaluated on: (1) can it be delivered incrementally as rearchitecture, (2) migration costs, (3) executive support for business value. No more "v2 will solve everything eventually." |
>
> **The trade-off:** In some places, the team BACKTRACKED on usability to stabilize, decouple, and remove bottlenecks. The platform offerings became more like early Android devices — not as polished, but allowing more options.
>
> **The authors' position:** For internal engineering platforms, the value of stability and future flexibility for platform customers CANNOT be sacrificed in the name of ideal usability.
>
> See also: Will Larson's article "Providing Pierceable Abstractions" for a larger writeup of the piercing concept.

> **[SRE/Production Lens: Coupling as Operational Risk]**
>
> The "batteries included" approach creates operational anti-patterns that SREs recognize immediately:
>
> - **Blast radius expansion:** Component-level coupling means one platform's failure cascades through workflow features into other platforms. The opposite of fault isolation.
> - **Untestable systems:** Poorly defined interfaces make it impossible to test components in isolation — integration tests become the only safety net, and those are slow and flaky.
> - **Monitoring gaps:** When systems are coupled at the component level rather than through APIs, it's unclear where to draw observability boundaries. Metrics exist per-component but workflow-level health is invisible.
> - **Change risk multiplication:** Changes in one platform have "unexpected side effects in other parts of the workflow" — the definition of high change failure rate.
>
> The "building blocks" approach is fundamentally an operational architecture decision: composable, API-connected services with clear boundaries, independent deployability, and isolated failure domains.

> **[Real-World Implementations: Trust-Building Patterns in Practice]**
>
> **Operational Excellence OKRs in practice:** Honeycomb and Datadog provide the instrumentation layer, but the organizational practice is what matters. Teams like Spotify's platform org have published versions of "reliability as a top-level objective" with tracked SLOs per platform offering and regular stakeholder reporting. The key is making the data *external-facing*, not just internal dashboards.
>
> **Staged rollout / progressive delivery (Icicle pattern):** Tools like LaunchDarkly, Argo Rollouts, and Flagger enable the technical mechanism, but the trust-building pattern is the organizational commitment to not pushing a platform on high-value customers until lower-risk customers have validated it. Netflix's approach with their internal compute platform followed a similar staged trust model.
>
> **Self-service to eliminate bottlenecks (Quiroga pattern):** Backstage's scaffolding templates, Humanitec's Score specifications, and internal developer portals follow this pattern — converting repeated human-in-the-loop requests into self-service workflows. The measurement practice (tracking request volume reduction with clear visuals) is what maintains leadership trust during the investment period.
>
> **"Pierceable abstractions" architecture:** Kubernetes itself follows this pattern — high-level Deployments/Services for common cases, but ability to pierce down to Pods, init containers, sidecars, and custom controllers for advanced users. Crossplane similarly provides high-level composite resources while allowing piercing to underlying managed resources.

---

## Wrapping Up

Trust takes much longer to build than to destroy. Events outside your control can erode it: black swan operational issues, major business changes you can't keep up with, team turnover leaving you unable to execute despite thorough planning.

**The most common way platform leaders fail their companies:** Through their own hubris, they believe they know better, don't communicate with adequate transparency, and trust their teams to the exclusion of listening to customers and stakeholders.

**The acceptance:** When you accept that success requires building and maintaining trust, you take the steps necessary to deliver trustworthy platforms that keep up with business demands.
