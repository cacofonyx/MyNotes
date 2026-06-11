# Chapter 13: Your Platforms Manage Complexity

> **Part III — What Does Success Look Like?**

> *"We must design for the way people behave, not for how we would wish them to behave."* — Donald A. Norman, Living with Complexity

The book started by describing the "why" behind platform engineering: rapid increase of technology complexity slowing application teams down, with the business getting less value per developer over time. This chapter brings that full circle. Platforms generate leverage by *effectively managing* complexity, not eliminating it. As a platform leader, you must become comfortable addressing complexity in everything you do.

The chapter highlights four areas where complexity needs active management: accidental complexity (where attempts to address complexity just move the problem somewhere else, often creating new human work), shadow platforms (balancing application team agility against proliferation), uncontrolled growth (the temptation to hire rather than simplify), and product discovery (iterative attempts to find the right product offering). The key insight: technology approaches are necessary but not sufficient — leverage comes from combining technology with understanding of human and organizational dynamics.

The chapter's centerpiece is a detailed four-year story of a Data Reliability Engineering (DRE) team that went through three failed approaches to managing PostgreSQL/Kafka/Cassandra complexity before a product discovery reset (driven by shadow platforms FoundationDB and MongoDB) finally yielded curated offerings that met customer needs while limiting platform team growth.

## Table of Contents

- [A Success Red Herring: The Single Pane of Glass](#a-success-red-herring-the-single-pane-of-glass)
- [Managing the Accidental Complexity of Human Coordination](#managing-the-accidental-complexity-of-human-coordination)
  - [Managing Migration Complexity](#managing-migration-complexity)
- [Managing the Complexity of Shadow Platforms](#managing-the-complexity-of-shadow-platforms)
  - [The FoundationDB Shadow Platform Story](#the-foundationdb-shadow-platform-story)
- [Managing Complexity by Controlling Growth](#managing-complexity-by-controlling-growth)
- [Managing Complexity Through Product Discovery](#managing-complexity-through-product-discovery)
- [Tying It Together: Balancing Internal and External Complexity](#tying-it-together-balancing-internal-and-external-complexity)
  - [Burning Out on OSS Operations](#burning-out-on-oss-operations)
  - [Trying (and Failing) to Change the Game](#trying-and-failing-to-change-the-game)
  - [Shadow Platforms Force a Reset](#shadow-platforms-force-a-reset)
  - [Executing on the Reset](#executing-on-the-reset)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Anti-Pattern] [Organizational Reality] [SRE/Production Lens] [Comparison] [Worked Example] [Real-World Implementations]

---

## A Success Red Herring: The Single Pane of Glass

The idea of bundling everything into a "single pane of glass" is popular in tech UX. Many tools promise a single UI to control your whole system. Reducing cognitive load seems smart. These initiatives usually start strong and deliver value for common use cases, but early success rarely sustains itself.

> **[Anti-Pattern: The Single Pane of Glass Trap]**
>
> **Camille's DevEx team story:** Developers had too many places for information (code reviews, build progress, tickets, code search, editor, command line). Team built a single web UI to improve flow and reduce context switching.
>
> **What went wrong:**
> - To keep everyone in the in-house interface, they had to re-create ALL workflows from each underlying vendor tool
> - Each vendor was itself trying to become the single pane of glass (hooks and integrations with each other)
> - Over time, the in-house UI became either an extra stop between the developer and the real UI, or a worse version of the real thing
> - **The persona problem:** Developers are picky about how they work. Many want command line only; others want IDE integration; others want ChatOps (but only when on-call). The same human operates as different personas depending on their role that day. A single pane only works for one persona.
>
> **The team's realization:** Better to rely on integrations available in GitHub, Slack, Jira, etc., and integrate their platform INTO these common offerings.

> **[Core Concept: APIs Over UIs]**
>
> The single pane of glass concept should be generalized: the goal is not the pane itself but the *ergonomics of a setup where everything a user needs is within reach*.
>
> **The correct starting point is the API and data model:**
> - Start with accessible, documented, coherent API access
> - Follow REST standards as closely as possible
> - Name things consistently
> - Do one thing per call; don't require stateful sequences to do one thing
> - Plan for backward consistency; don't change APIs often once released
>
> **Then layer experiences on top:**
> - Easy UI for basic use cases
> - Command-line integration for developers who prefer it
> - Chatbot interfaces
> - IDE support
> - Web interfaces
>
> **Bottom line:** UIs are inherently complex and hard to build right. If your goal is reducing complexity, start with the API layer. If you neglect that, a UI won't solve the problem.

> **[Real-World Implementations: APIs-First Platform Design]**
>
> **Backstage (Spotify's open-source IDP):** Demonstrates both the appeal and the limitations of the single-pane approach. It works well as a *catalog* and *scaffolding* tool (API-driven underneath), but teams that try to make it the single destination for ALL developer workflows inevitably hit the same re-implementation problem Camille's team encountered.
>
> **Kubernetes API:** The exemplar of APIs-over-UIs in platform engineering. The kubectl CLI, various dashboards (Lens, k9s, Rancher), GitOps tools (ArgoCD, Flux), and IDE extensions all work because the underlying API is well-designed and consistent. No single UI wins for everyone, but the API serves all personas.
>
> **GitHub Actions / GitLab CI:** Succeed by providing an API-first platform where the "UI" is the YAML configuration in your repository. Different users interact differently (edit YAML directly, use VS Code extensions, use the web editor, use gh CLI), but the underlying model is consistent.
>
> **Terraform/OpenTofu:** Another API-first pattern — the "UI" is HCL configuration. Terraform Cloud adds a web UI on top, but the core value is the declarative API model that different tools can target.

---

## Managing the Accidental Complexity of Human Coordination

A key measure of success: how much glue do application teams still need to build to work with your platforms? Platforms should create abstractions eliminating the need for each team to build their own glue. But there's another type of glue: **human glue**.

"Human glue" is what Tanya Reilly describes in "Being Glue": manual workarounds, documentation, and coordination needed to resolve gaps between what a team needs to do and what they're actually doing.

> **[Core Concept: Human Glue as Accidental Complexity]**
>
> In a quest to limit technical glue, some platform teams create NEW accidental complexity by over-relying on human coordination.
>
> **The car with a welded-shut hood analogy:** You don't expect most drivers to fix their engine, but they still need to know where the smoke is coming from. When a platform hasn't provided enough diagnostic tools:
> - Incident happens
> - Application team is stuck
> - They get on a call with the platform team to figure out if the platform is the culprit
> - Frustrating for both teams
>
> **The rule of thumb:** How often do you rely on "human glue" to resolve issues? Manual processes to coordinate OSS upgrades? Humans to drive fixes for common outages?
>
> **The engineering belief:** Humans should be reserved for managing the truly complex scenarios. Software should resolve the merely complicated.
>
> **Exposing platform metrics and synthetic monitors (Chapter 6)** is key to avoiding escalations. Complex outages will still happen, but proper tooling stops you from using platform engineers and DevOps/SREs as "human dashboards."

### Managing Migration Complexity

> **[Worked Example: Automated Migration Without Project Management]**
>
> **Context:** Major operating system version upgrade. Camille challenged her team to complete the migration without human project management support.
>
> **What they built:**
> 1. Small piece of code tracking each host: whether it needed upgrade, and by whom
> 2. Run daily to produce a progress report
> 3. Report fed into Jira, which automatically created and assigned tickets with details
>
> **The key enabler:** Ownership metadata registry (Chapter 2) — tracked which code belonged to which team. Used to bootstrap figuring out where to assign tickets. Code applied heuristics to system resource identifiers to find the most likely person — minimized incorrect assignments.
>
> **How it evolved:**
> - Turned into a useful system for tracking/maintaining ownership data broadly
> - Powered other migrations
> - Changed how most migration exercises were approached company-wide
> - More nuanced dependency mappings and smart reminders over time
> - More time automating common migration elements (less work for customer teams)
> - Biggest challenge: too many groups wanted to use it to drive migrations BEFORE they'd thought through migration process details
>
> **The TPM evolution:**
> - **Before:** Hand-to-hand combat with each team in the migration path
> - **After:** Overseers and ambassadors. Scaled to support more migrations. Focused on the "weird 20%"
> - **Example:** Big customer storage system upgrade needing coordination → deploy TPM support to unblock another automatable tranche
>
> **Goal:** Treat TPMs as rare specialists brought in when you can't think of engineering-driven tricks to make migrations automatic or self-service. You'll still need them, but they should be the few you admire for discipline, attention to detail, and organizational savvy.

> **[SRE/Production Lens: Ownership Metadata as Infrastructure]**
>
> The ownership metadata registry is one of the most underappreciated pieces of platform infrastructure. Without it:
> - Migrations require manual detective work to find who owns what
> - Incidents require "human dashboards" to route pages correctly
> - Compliance audits become archaeology projects
> - Security patches can't be automatically assigned
>
> **With it:**
> - Migrations become automatable (assign tickets to the right team programmatically)
> - Incident response can auto-route to owners
> - Compliance becomes queryable
> - Security patches can be tracked to completion without spreadsheets
>
> **The pattern:** Invest in metadata about your systems (ownership, dependencies, SLOs) BEFORE you need it for a specific initiative. It pays dividends across every operational process.

---

## Managing the Complexity of Shadow Platforms

Shadow platforms (duplicative platforms application teams build for themselves) increase overall complexity but usually reduce complexity for a particular area. The goal is NOT to restrict all of them, but to be *aware* of them.

**Why you can't stop all of them:**
- At scale, it's impossible
- It's ill-advised to halt all platform-related experimentation outside your org
- Application teams are experts on their own needs and will take a pioneering mindset
- They might build the first draft of your next valuable platform offering

**How to wrangle them:**
- Build on trust (Chapter 12) — that's what keeps you in the loop
- Being informed gives you a chance to prepare:
  - Embed one of your engineers into the project
  - Get regular updates
  - Set expectations about what would happen if they want you to take over

**When you take over a shadow platform:** You'll inevitably create new complexity (expanding surface area beyond original team). The trick: reduce pioneer-driven complexity while keeping new complexity within your platform team rather than leaking to users.

### The FoundationDB Shadow Platform Story

> **[Worked Example: Managing the AI Platform Pioneer]**
>
> **Context:** Six months after Ian took over one of five in-house compute platforms, CTO pushed for AI/data science. A new leader was hired — a pioneering visionary eager for radical change. His belief: the barrier to AI innovation was coupling to existing "flawed" in-house platforms. His vision: each data scientist gets their own cloud account, using whatever IaaS/OSS they want, like a small startup.
>
> **Ian's first mistake:** Assuming everyone could see how complex this would be, and the pioneer would quickly change course. After all, most data scientists could barely administer their own workstations.
>
> **What the pioneer argued:** ~10% of data scientists came from engineering backgrounds and could handle the complexity. Since this was experimental work needing a rewrite for production, they could deal with architectural issues "later."
>
> **Ian's response (once he realized the plan would stick):**
> 1. Regular meetings with the pioneer's team to understand what it would take to cover beyond the 10%
> 2. Meetings exposed overlooked complexity: no migration plan (hundreds of developer years), no administration story for non-technical users
> 3. But the CTO backed the effort — Ian had to choose: let them build without support, or compromise to influence the work
>
> **The compromise:**
> - Freed up two developers to support the initiative (CTO attention provided cover for roadmap changes)
> - Chose "settler types" with a difficult remit: "Don't slow the project down, but find places where you can build the right 'long-term' components earlier than we would have"
> - Succeeded about halfway — keeping things fast always means some non-scalable glue
>
> **What happened as the system became real:**
> - The 10% of advanced data scientists could successfully access the cloud for experimentation
> - The remaining 90% tried the system — concerns around operations, administration, and integration became obvious to everyone
>
> **Resolution:** Took a couple of years before the whole thing was sunset in favor of an integrated platform. But in those years, the company benefited from innovation that otherwise wouldn't have been possible. Became a case study for how the platform org could partner without slowing things down.
>
> **Key insight:** This is successful management of a shadow platform — messy, iterative, and a well-managed compromise rather than a black-and-white picture of great execution.

> **[Organizational Reality: The Politics of Shadow Platforms]**
>
> The shadow platform dynamic is always political:
> - **Pioneers** want freedom and will build around platform teams they see as slow
> - **Platform teams** see pioneers creating operational debt they'll eventually inherit
> - **CTOs/executives** care about business velocity and often back pioneers
> - **The compromise** must give pioneers enough runway while embedding platform influence
>
> The key insight: you cannot "win" the argument by being right about complexity. You must demonstrate that partnership produces better outcomes than either pure pioneering or pure platform control. Sometimes this takes years.

---

## Managing Complexity by Controlling Growth

Growth is addictive. After scaling a platform team from early days to a stable organization, it's tempting to think adding more people is the only way to accomplish more.

> **[Anti-Pattern: Growth as Complexity Management]**
>
> **How unchecked growth CONTRIBUTES to complexity:**
>
> | Growth habit | Complexity outcome |
> |-------------|-------------------|
> | Throw bodies at problems instead of automating | Creates tedious work engineers don't want to do |
> | Build without regard to customer needs | Spawling portfolio of half-baked products |
> | Managers build empires rather than aligning with peers | Products don't fit together |
> | Growth provides excuses | "Another person to point the finger at, a newcomer who doesn't know how things work" |
> | Delay automation investments | Eventually stuck in non-scalable staffing model |
>
> **The platform engineering mandate is NOT driving efficiency through any means (e.g., outsourcing manual approaches).** You achieve efficiency by strategically simplifying through software engineering and product discovery.

> **[Core Concept: The Non-Linear Growth Principle]**
>
> Good platform leaders understand that platforms deliver *leverage*, which means they shouldn't need to grow at the same rate as the overall engineering team once that leverage point is established.
>
> **The guardrail rule of thumb:** Most new work in established areas should be funded by existing people on those teams.
>
> **What this forces:**
> - If KTLO workload has gotten out of hand — find ways to reduce cost
> - Strong sense of most important areas — divest from features that are "good enough" or haven't shown promised value
> - Manage complexity so platforms support far more users than developers
> - Don't linearly scale platform engineers for every new thing in an area
>
> **What this does NOT mean:**
> - Cut yourself to the bone with no slack
> - Never grow (new product areas may require growth)
> - Ignore scaling needs during company growth
>
> **The measurement:** KTLO + mandates + operational improvements gives you the absolute bottom of team size (that number + 20% so everyone doesn't quit). Above that baseline, exercise discretion about investments. Being thoughtful about next work, incorporating customer demand, team demand, and strategic insights before asking for growth = mature platform planning.

> **[Comparison: Platform Teams vs. Application Teams on Growth]**
>
> Why the growth discipline argument applies more strongly to platform teams:
>
> - **Application teams** are revenue-generating — growth is tied to business expansion
> - **Platform teams** are more likely seen as "cost centers" where efficiency is expected
> - **Platform leverage** means 10 platform engineers should enable 100+ application engineers
> - **Growth without leverage** suggests the platform isn't doing its job of managing complexity
>
> This doesn't make the reality easier to live with — when you're barely keeping up with rapid company growth, slowing your own growth feels counterintuitive. But guiding a culture of smart efficiency IS the mandate for leaders in this space.

---

## Managing Complexity Through Product Discovery

Product discovery: understanding customer demands and creating "a product solution to this problem that is usable, useful, and feasible" (Silicon Valley Product Group). Not just for products built from scratch — critical for platforms based on open source systems.

**The common predicament:** Under pressure from potential shadow platforms, teams provide whichever OSS system the customer asks for without determining if it's the right product solution. Result: teams stuck with operational complexity that grows linearly with users and use cases.

**Why OSS systems are particularly prone to this:**
- Distributed OSS for data processing (PostgreSQL, MySQL, Cassandra, MongoDB, Kafka) are highly complex by nature
- OSS vendor model drives competition through adding more features
- This means very broad interfaces
- Each system's full surface area exposed to users = linear operational scaling

**The standardization challenge:**
- Application developers may agree fewer choices would help
- They rarely agree on WHAT the limited set should be
- Forcing it can backfire (slow application teams down, politically unpopular)
- Usually only happens when support burden hits a breaking point

> **[Core Concept: The Middle Path for OSS Platform Complexity]**
>
> Between "let a thousand flowers bloom, until you can't stand it" and "offer a strict platform allowing very little variation" lies the product culture approach:
>
> 1. Take time to understand your customers
> 2. Explore WHY teams use their chosen tools (habit vs. must-have features)
> 3. Through iterative product discovery, develop insight to curate offerings
> 4. Reduce complexity while better meeting customer needs
>
> This is not a quick fix — the DRE team's story below took four years. But it's the only path that produces platforms managing complexity for BOTH the customer and the platform team.

---

## Tying It Together: Balancing Internal and External Complexity

> **[Worked Example: The DRE Team's Four-Year Product Discovery Journey]**
>
> **Starting point:** Ian had ~10 people owning PostgreSQL, Kafka, and Cassandra. The team followed a Data Reliability Engineering (DRE) approach: providing provisioning and support, with proactive engineering spent on automation (resilience, autoscaling).

### Burning Out on OSS Operations

**The unsustainable state:**
- Each OSS system had a large feature surface area
- Operational complexity of running these as company foundation → constant strain
- Even with two pager rotations (following the sun), high-severity incidents per week were closer to **50 than 5**
- DRE team had reached the limits of efficiency from automation alone

**The demand disconnect:**
- Application teams were happy with the flexibility of extensive feature sets
- Primary demand: DRE should expand portfolio with MORE offerings
- When DRE leaders explained they needed 2x engineers to sustainably manage EXISTING workload before adding more — met with disbelief
- The only way to grow: agree to support more systems/configurations → same unsustainable scaling point

### Trying (and Failing) to Change the Game

> **[Anti-Pattern: Three Failed Approaches to Complexity Reduction]**
>
> **Attempt 1 — "Get out of the game" (vendor hosted OSS):**
> - Move to vendor IaaS implementations where application teams own operations
> - **Why it failed:** Multicloud requirements meant vendor differences were too hard for application teams to operate themselves. DRE team was still constantly paged because application teams lacked debugging depth.
> - **Lesson:** "Get out of the game" really meant "stay in the game, but as an operations team."
>
> **Attempt 2 — SLA documentation (shared operational model):**
> - Clear documentation of what team could and could not support within SLA
> - Help application teams understand bespoke configurations couldn't be supported by DRE alone
> - **Why it failed:** Sounded like a lawyerly abdication of responsibility to customers. Customers saw the team using rules to position themselves as advisors rather than owners.
> - **What happened:** Ian brokered top-down handover for one big customer, forcing trade-offs. But the approach wasn't sustainable without constant conflict and politics.
> - **Lesson:** Rational compromise is not the same as an approach customers will accept.
>
> **Attempt 3 — Full encapsulation (service API layer):**
> - Create a service API fully encapsulating OSS APIs, giving platform team control
> - Tied to a multiregion reads/writes feature with simple (key, value) semantics
> - **Early success:** First customers satisfied
> - **Why it stalled:** No one else interested in multiregion in the short term. Everyone wanted full SQL.
> - **The drift:** Team started planning secondary indices toward supporting SQL semantics.
> - **Ian's intervention:** Building an in-house global SQL database is "less thinking big and more of an impossible dream."
> - **Lesson:** Don't let a successful niche feature blind you to the actual breadth of customer needs.

### Shadow Platforms Force a Reset

During the three failed attempts, frustrated application teams built shadow platforms:
- **MongoDB** for document support
- **FoundationDB** for transactional write semantics with horizontal scaling

These had the usual lifecycle: application teams happily owned operations during growth, then wanted to offload to the platform team as initial engineers moved on.

**The reset:**
- Brought in managers with experience building *product-oriented* infrastructure
- They started with product discovery: looking across all offerings, investigating what application teams *actually needed* (as opposed to just preferred) from Cassandra, MongoDB, PostgreSQL, Kafka, and FoundationDB

**Two major opportunities discovered:**

| Opportunity | Product solution |
|-------------|----------------|
| **Simplification** | High demand for cross-application configuration platform where (key, value) semantics were fine. Leveraged the FoundationDB shadow platform investment to power a managed service focused on this use case. |
| **Coupling multiple primitives** | Demand for schema-aware storage, but discovery revealed it was as much about caching and search as ACID transactions. Combined PostgreSQL with searchability and caching → more limited SQL system satisfying most customers. |

**The sunset opportunity:** If both projects succeeded, Cassandra AND MongoDB could be sunset.

### Executing on the Reset

- Collaborated closely with application teams that had pressing demands
- Result: rapid development of scrappy-but-satisfying platforms
- Early customers became advocates throughout the company
- Long list of application teams signed up as platforms matured

**Timeline: ~4 years of iteration** to identify the right product offering meeting major application needs while limiting platform team complexity.

> **[SRE/Production Lens: The 50-Incidents-Per-Week Reality]**
>
> 50 high-severity incidents per week across two rotations is an operational emergency by any standard. For context:
>
> - Google SRE targets ~2 events per on-call shift as sustainable
> - 50/week means ~7/day, meaning on-call engineers cannot do ANY project work during their rotation
> - Following the sun helps (spreading across time zones) but doesn't fix the volume problem
> - The automation ceiling: you can reduce the *coefficient* of linearity but not eliminate the *linear scaling* without changing the product
>
> **The lesson for SRE teams managing OSS:** Automation alone cannot solve a product/architecture problem. If the surface area exposed to users is too broad, every new user and use case adds operational complexity that no amount of automation can fully absorb. The solution must come from *limiting the surface area* — which is a product decision, not an operations decision.
>
> **The honest cost:** At the time of writing, the team is in year 2 of a 5-year plan to fully deprecate MongoDB and Cassandra offerings. This is the true timeline for complex platform transformations.

> **[Organizational Reality: Why Product Discovery Takes Years]**
>
> You may wonder whether a process involving three false starts and a multiyear migration is really a success. The authors' answer: **yes, this IS the reality of delivering platforms that manage your company's unique complexity.**
>
> Why it takes so long:
> - Each failed approach teaches something (vendor hosting doesn't work for multicloud; SLA documentation is perceived as abdication; encapsulation works but only for narrow use cases)
> - Shadow platforms provide evidence of actual demand (FoundationDB proved the config store use case)
> - The "right" product isn't viable at the time you identify the problem (you need the shadow platforms to exist first)
> - Migrations from old to new platforms take years even after the new platform is built
>
> **Don't be afraid to keep iterating.** Trade-offs are hard, and sometimes the best solution isn't even viable at the time you identify the problem.

> **[Real-World Implementations: OSS Platform Complexity Management]**
>
> **Aiven, Confluent, MongoDB Atlas (managed OSS):** These are the "vendor hosted OSS" approach from Attempt 1. They work well when you're single-cloud and can accept vendor lock-in. But for multicloud organizations, the DRE team's experience is common — differences across cloud vendors still push debugging back to internal teams.
>
> **CockroachDB, TiDB, PlanetScale:** These represent the "in-house global SQL" endpoint that Ian correctly identified as an impossible dream for a platform team to build. Purpose-built distributed SQL databases exist precisely because building one in-house is infeasible.
>
> **FoundationDB (Apple's open-source release):** Used by Apple, Snowflake, and others as a foundational layer that provides transactional key-value semantics upon which higher-level abstractions are built. The DRE team's use of FoundationDB for the config store use case follows this pattern — using it for its strongest capability (ordered key-value with transactions) rather than trying to make it do everything.
>
> **Internal platform composition pattern (PostgreSQL + cache + search):** This mirrors what Supabase offers externally: PostgreSQL as the core with built-in caching (connection pooling, edge caching) and full-text search (pg_tss, or Elasticsearch sidecar). The insight is that customers don't want "just SQL" — they want a data platform that handles the common adjacent needs.

---

## Wrapping Up

Alignment and trust are challenging but achievable goals. Managing complexity, on the other hand, is a **North Star** — you'll use it to guide your organization, but you're unlikely to ever fully accomplish the task.

**What you can do:**
- Detect complexity (human coordination overhead, shadow platforms)
- Practice controlling it (automation, ownership metadata, staged rollouts)
- See it as opportunity (develop new ways to automate, simplify, understand customer needs)

**What you must accept:**
- Complexity will always be there
- Too much growth too fast makes it harder to keep in check
- The iterative process of product discovery is critical to finding the simplest scalable solution among more complex options
- The more time you spend thinking about and driving down complexity for users, the more mature your platform becomes
