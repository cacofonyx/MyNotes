# Chapter 11: Your Platforms Are Aligned

> **Part III — What Does Success Look Like?**

> *"The purpose of a team is not goal attainment but goal alignment. When the team is fulfilling its purpose, team members are more effective because they're more directed."* — Tom DeMarco and Tim Lister, Peopleware

Alignment is the first criterion for holistically evaluating platform engineering success. Misaligned platform teams create a swamp of overlapping and incompatible products — tricky to use together, often at odds with each other's goals, and frustrating for customers who struggle with platform teams that can't see beyond their own silos. Unlike the "over-general" swamp from Chapter 1, this one is filled with duplication and competition rather than vagueness.

The chapter identifies three types of misalignment: purpose (teams lacking a holistic platform engineering mindset), product strategy (teams building in silos without cross-platform thinking), and planning (teams failing to support each other's critical projects). For each, Fournier and Nowland provide concrete tactics drawn from their experience transforming an organization of ~100 engineers with five competing compute platforms and deadlocked leadership.

Critically, the authors argue that none of what makes alignment work is unique to platform engineering — it's fundamental leadership. What IS unique is that platform teams face more discretion in choosing where to invest (since value is indirect and several steps removed from revenue), which means the failure to make hard alignment decisions is more common and more damaging here than in product engineering.

## Table of Contents

- [A Success Red Herring: Adoption Metrics](#a-success-red-herring-adoption-metrics)
- [Alignment to Purpose](#alignment-to-purpose)
  - [Align Teams with the Right Mix of People](#align-teams-with-the-right-mix-of-people)
  - [Align Culture with Common Practices](#align-culture-with-common-practices)
  - [Align Culture by Having Teams Collaborate](#align-culture-by-having-teams-collaborate)
- [Alignment of Product Strategy](#alignment-of-product-strategy)
  - [Independent Product Management](#independent-product-management)
  - [Independent Lead ICs](#independent-lead-ics)
  - [Platform-wide Customer Surveys](#platform-wide-customer-surveys)
  - [Judicious Restructuring](#judicious-restructuring)
- [Alignment of Plans](#alignment-of-plans)
  - [Align Only on Larger Projects](#align-only-on-larger-projects)
  - [Be Forthright in Confronting Misalignment](#be-forthright-in-confronting-misalignment)
  - [Final Alignment from Principled Leadership](#final-alignment-from-principled-leadership)
- [Tying It Together: Getting an Organization to Alignment](#tying-it-together-getting-an-organization-to-alignment)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Anti-Pattern] [Organizational Reality] [SRE/Production Lens] [Comparison] [Worked Example] [Real-World Implementations]

---

## A Success Red Herring: Adoption Metrics

Strong adoption *seems* like it should indicate a platform delivering value — customers eager to adopt. But this line of thinking can be taken too far, especially when your customers are a captive audience without real alternatives.

**The problems with adoption as a primary metric:**

| Problem | Effect |
|---------|--------|
| Captive audience | You forget to build what people *want* and instead build what you think they *should* want, then force them to use it |
| System-by-system measurement | Creates competition between your own teams for user attention — works *against* alignment |
| Mandatory migrations | Metric loses all value in measuring organic demand; becomes a stick to beat customers with |
| Customer-driven adoption | You drain the very productivity you're supposed to be safeguarding when you make customers responsible for their own adoption |

> **[Anti-Pattern: Adoption as a Primary Metric]**
>
> The worst-case scenario: a confusing array of platform offerings combined with constant pressure on customers to justify their lack of adoption under threat of mandatory migration.
>
> **Why this happens:** Adoption is easy to measure, easy to explain to executives, and creates a clear narrative of "progress." It's seductive precisely because it's simple.
>
> **The leverage dilution cycle:**
> 1. Platform team generates work for customers (write your own requirements, do the migration yourself)
> 2. Platform teams compete with each other for customer attention by delivering incompatible offerings
> 3. Both contribute to the complexity the platform is supposed to be *solving*
>
> **What to do instead:** Use adoption as a *secondary* metric and input to product strategy. Target adoption of your most valuable customers by working *with them* to identify measurable pain points your platform will address. You don't need every single team on every single product.

> **[SRE/Production Lens: When 100% Adoption IS Correct]**
>
> Some platforms genuinely need 100% adoption — you probably don't want multiple employee identity systems, for example. But these are the exception. Most platforms provide differential value: a CI system might be transformative for microservices teams but add friction for embedded systems engineers. Trying to force both onto the same platform loses sight of where you provide the most leverage.
>
> **The SRE parallel:** This is like mandating identical SLOs across all services. A batch job processing overnight has fundamentally different needs from a user-facing API. Forcing both into the same operational model degrades both experiences.

---

## Alignment to Purpose

**The CI/OS Platform Conflict:** A continuous integration platform had tasks regularly disrupted by the underlying OS platform running updates, increasing tail latencies. The "easy fix" (delay OS updates until no tasks running) would have been a hack on legacy infrastructure. The OS team pushed instead for the CI team to migrate to immutable images — a project requiring many developer months — while *refusing* to implement a small workaround that would fix user impact immediately.

The root cause: the OS platform team still held an "infrastructure" mindset, not a platform engineering mindset. They prioritized technical quality above all else, used unhappy customers as *leverage* to get desired migrations done faster, and failed to appreciate the product side of their decisions.

> **[Core Concept: The Four Pillars as Shared Purpose]**
>
> For platform teams to be successful, they must share a common purpose built on the four pillars from Chapter 2:
>
> | Pillar | Meaning |
> |--------|---------|
> | **Product** | Taking a curated product approach |
> | **Development** | Developing software-based abstractions |
> | **Breadth** | Serving a broad base of application developers |
> | **Operations** | Operating as foundations for the business |
>
> Each team defines additional purpose specific to their area, but these four are crucial for ALL platform teams because together they create leverage and make it possible to manage complexity.

### Align Teams with the Right Mix of People

Alignment to purpose starts with getting the right people on the team (Chapter 4). At smaller companies, everyone should be involved in hiring processes — this reinforces agreement on what platform engineering needs. At larger organizations:

- Use cross-team interviewing to support cultural intermixing
- Reorganize existing teams to ensure the right skill sets cover the right product areas
- Where functionally aligned subteams overlap (compute, networking, storage), mix things up or pull out cross-functional teams for platform initiatives

### Align Culture with Common Practices

Shared practices around the four pillars drive cultural alignment:

- **Product management culture:** Approach internal users as customers (not just stakeholders); look for partnership opportunities. This breaks the "us vs. them" mentality.
- **Operations practices:** Operability reviews, blameless postmortems, and other DevOps/SRE practices break down boundaries between teams and platforms.

### Align Culture by Having Teams Collaborate

The approach to collaboration determines much of team culture, and the more the organization collaborates, the more gelled culture becomes.

**For senior leaders:** Bring teams together frequently. Everyone should use one another's platforms ("dogfooding") — this creates common culture AND generates creative product strategy ideas.

**For engineering managers, senior ICs, product managers:** Look for chances to work with peers. Hold architecture and product strategy reviews with members of other platform teams invited to provide constructive feedback.

> **[Organizational Reality: Collaboration as Culture Engine]**
>
> Dogfooding is not just a quality practice — it's the *core source of creative ideas* for product strategy. When a storage team uses the compute platform daily, they understand its ergonomics in ways no survey could capture. When the compute team uses the storage platform, they see integration opportunities invisible from the outside.
>
> The leadership job is creating the space and expectation for this to happen. Engineers left to their own devices will stay heads-down in their own systems.

---

## Alignment of Product Strategy

**The Five Compute Platforms Disaster:** Coming out of rapid headcount growth with no cross-platform alignment, four teams made four different technology bets, each partnering with different early adopters. Result: five compute platforms where the largest was "deprecated" but the other four were "not GA-ready yet." Worse, as each of the four new teams tried to grow beyond scrappy architecture, they could only justify more engineers by trying to capture the *same* use cases — actively fighting for the same customers.

The authors recommend four tactics to align product strategy:

### Independent Product Management

**Problem:** If product managers report to engineering managers who own specific platform areas, they become extensions of engineering silos. Their narrow focus optimizes for growing within a single engineering domain but misses cross-platform improvements.

**Solution:** Keep product management reporting separated enough from engineering management that they can operate independently.

**Recommended structure:**
- All platform PMs in a separate team reporting to a PM leader
- PM leader reports to a cross-area senior platform engineering leader
- PM leader is accountable for platforms working well *together* as products
- Leadership style should be "affiliative/collaborative" (challenging PMs to cooperate) rather than "visionary" (dictating a singular unifying vision)

> **[Organizational Reality: Independent PM Structure]**
>
> There will *always* be conflict between each platform area's preferred strategies. Making it hard on PMs by having the engineering manager doing their performance review be deeply invested in just one area creates an impossible tension. Independent reporting gives PMs the structural freedom to say "actually, Platform B's approach serves users better here" without career risk.
>
> **Why not a product leader running everything?** The authors admit their bias — they're engineering leaders worried about product people managing everything when engineering and operations are so key to success. But acknowledge it might work.

### Independent Lead ICs

Sometimes architectural misalignment is *behind* product strategy misalignment.

**The storage throughput story:** A deployment platform struggling with large container images needed storage support. The storage team was occupied with their own problems and declined to help. Rather than escalating, the deployment team went deep into prototyping their own storage system — a clear misalignment of technical ownership and expertise. Since it was seen as "technical," PMs weren't involved. It was only after significant investment and delivery challenges that senior leadership learned about it and brought in the storage team.

**Solution:** Have the most senior principal/distinguished engineer in the platform org report to the same senior leader as the PM leader. Their role:

- Provide escalation and advocacy when junior engineers hit management impediments trying to reduce architectural misalignment
- Watch for teams wrongfully duplicating architecture because it's easier (or more fun) than cooperating
- Oversee cross-team architecture/design sessions for larger organizations
- Talk with customers about architecture-impacting product decisions

**Scaling:** Staff-level engineers take on this role for their own areas but are challenged by the principal engineer to think beyond their own platform.

**Warning:** Don't route every big engineering decision through one person — they become a bottleneck and lose ability to stay hands-on.

### Platform-wide Customer Surveys

Strategy conversations usually happen with a subset of users — often senior ones who've become accustomed to the platform's flaws and don't see alignment issues that frustrate newer users.

**Tactic:** Augment direct PM feedback with free-form comments from platform-wide customer surveys. When feature-level product misalignment keeps people from getting their jobs done, surveys are often the only outlet they'll use to tell you. One comment is a sample, but "where there is smoke (coming out of someone's ears), there is a smoldering fire of other users with similar frustrations."

### Judicious Restructuring

When different teams have overlapping feature sets, the temptation to solve it with reorganization is strong. Both sides make bad arguments:
- PMs eager to consolidate may argue for unification even when it means losing valuable unique features
- Engineering leaders wanting to grow teams argue cost efficiencies outweigh marginal benefits

**Key lessons from Chapters 8 and 9:** Rearchitecting, migrating, and sunsetting takes enormous work, time, and iteration. A reorganization won't change that. Worse, reorgs cause team churn and confuse customers.

> **[Core Concept: When to Restructure]**
>
> **Reserve alignment-driven reorganizations for situations where:**
> - Costs of misalignment are high AND benefits are clear
> - A strong leader has the capacity to take on more scope (or a weak leader needs their scope reduced)
>
> **The five compute platforms resolution:** Solved incrementally over 18 months, with each integration helping understand strategy. Each platform team's leader was asked to be aware of competing for use cases and work with peers to differentiate. Watching how leaders used *influence* to resolve differences (rather than dictating solutions) was how the authors learned who the strong leaders were.
>
> **The "inverse Conway maneuver"** — restructuring to drive system outcomes — is sometimes called for. But it should be a last resort for alignment, not a first response.

---

## Alignment of Plans

Returning to the OS platform team: while their forced migration to immutable images was causing issues for CI, they also faced a build-tools platform team that hadn't planned immutable images work for *another two years*. The build-tools team had stuffed their roadmap with concurrent v2 projects and argued any deviation was impossible because of customer commitments.

It wasn't enough to align on purpose and strategy — they had to drill down to aligning on plans.

### Align Only on Larger Projects

**Scope:** Only significant projects (one developer year or bigger). Look at each project's dependencies on other platform areas and justification for being a priority.

**Why not every detail:**
- Too much work, too much detail
- Prevents teams from having necessary agility
- Gamesmanship happens regardless of granularity (overly optimistic/pessimistic estimates to fit narratives)

**How to avoid gamesmanship:** Build common culture and have leadership from all teams reporting up in parallel as checks and balances. Trust that alignment and culture keep the small stuff in check.

### Be Forthright in Confronting Misalignment

Platform leaders must collaboratively make tough calls about roadmap items that benefit Platform A's users at the cost of Platform B's plans. Two challenges:

1. **Trade-offs become political.** People want to see "their" work succeed, especially when delivery ties to compensation and promotions.
2. **It's rarely clear which competing initiative is most important.** Each team's plans resolve real customer pain and move strategy forward.

> **[Anti-Pattern: Weak Leadership Avoids Confrontation]**
>
> Weak platform leadership takes the easy route of greenlighting each team's proposals to avoid confrontation, thinking they can be "agile" and course-correct later. But agility is for decisions that impact a single team. When decisions ripple to other platform teams and their customers, postponing alignment means *more* work thrown out and customers left scratching their heads over missed deadlines.
>
> **Amazon's "Have Backbone; Disagree and Commit":**
> > *Leaders are obligated to respectfully challenge decisions when they disagree, even when doing so is uncomfortable or exhausting. Leaders have conviction and are tenacious. They do not compromise for the sake of social cohesion. Once a decision is determined, they commit wholly.*
>
> People focus on "Disagree and Commit" but miss that **"Have Backbone" comes first.** Strong leaders need a forum to put forth their best case *before* they can be asked to commit to something they disagree with.

### Final Alignment from Principled Leadership

How do leaders get to a final decision they can commit to? Is it up to the biggest boss to pick winners?

**The quandary:**
- Arbitrary-seeming picks leave teams feeling the leader didn't understand or care about their needs
- But *someone* has to decide, or you make plans you can't deliver on

**The resolution:** Senior leaders apply a *deliberate rationale* that is clearly communicated. The process must be collaborative and transparent. "Disagree and commit" is NOT about the senior person arbitrarily deciding — it's about creating a process where the team understands what led to the decision.

---

## Tying It Together: Getting an Organization to Alignment

> **[Worked Example: Resolving the OS Platform vs. Build-Tools Deadlock]**
>
> **Context:** ~100-person platform organization (out of ~1,000 engineers). Multiple platforms struggling to scale. Team had culturally come together but tension remained around rearchitectures and major investments.
>
> **The deadlock:** OS platform team needed immutable images (to avoid OS updates impacting CI/low-latency customers). Build-tools team needed to decompose their platform to support Bazel. Both were large projects with large migrations, and each migration would create significant work for the other team. No way to do both simultaneously.
>
> **The resolution process (5 steps):**
>
> **Step 1 — Bottom-up roadmaps:** Each team made estimates for the upcoming year: where they'd invest, which projects needed additional funding. (Product roadmap from Chapter 5 feeding into Chapter 7's estimation process.)
>
> **Step 2 — Identify common themes:** Leadership team (area heads + PM + chief architect) identified themes speaking to both technical and product challenges. Five became high-level objectives reflecting areas everyone agreed were most important. *Example: "building blocks, not batteries included."* These objectives reprioritized product investments — projects that didn't match were cut.
>
> **Step 3 — Peer review of roadmaps:** Area heads' roadmaps reviewed by peer heads, senior ICs, and PMs. Revealed places where teams were overly optimistic about costs, especially impacts on other platform areas not previously considered. Weeded out overly optimistic projects.
>
> **Step 4 — Identify misaligned projects:** Each area head asked to bring projects they saw as misaligned to overall goals that should be dropped. *This only worked because they had built trust in one another and in Camille to prioritize for the company's best interest.* Highlighted risky or optional projects; some were cut or scope-reduced.
>
> **Step 5 — Commit:** Overall project list accommodated the most important stakeholder work. Everyone understood peers' investments. Disagreements remained, but the team committed to move forward with course correction as needed.
>
> **Outcomes:**
> - OS team saw immutable images was not a top product priority for the next 12 months
> - Ian (whose team reported to the OS org) didn't agree with Bazel migration but saw his peer had a reasoned argument and had sacrificed other projects — so he committed to supporting it
> - Some strategies failed (including Bazel migration), but others that were contentious (moving to Git) prepared foundations for important improvements over years
>
> **Key insight:** This process applies to product investment conflicts AND technical investment conflicts equally. It will be time-consuming, frustrating, and messy, but succeeds by proactively gathering details, putting up with frustration, and slowly course-correcting.

> **[SRE/Production Lens: Planning Misalignment Creates Production Risk]**
>
> The OS team's situation is familiar to any SRE who has tried to drive a security or reliability migration while depending on another team's timeline. The production implications are severe:
>
> - **Unresolved planning conflicts delay reliability improvements** — the OS team's immutable images would have improved CI reliability, but was blocked by interdependencies
> - **Forced simultaneous migrations create change management nightmares** — if both teams had pushed their migrations concurrently, customer teams would face compound change risk
> - **The "build-tools v2" pattern** — stuffing roadmaps with concurrent v2 projects is a reliability red flag. Chapter 8's lessons about rearchitecture risk apply directly here.
>
> The resolution process — accepting that both migrations can't happen simultaneously, then prioritizing based on overall impact — is essentially change management at the organizational level.

> **[Real-World Implementations: Alignment Tooling and Practices]**
>
> **OKR frameworks (Lattice, Ally.io/Microsoft Viva Goals):** Used to define cross-team objectives that force alignment conversations. The authors' "five high-level objectives" are essentially cross-team OKRs that subordinate individual team goals. The key: objectives must be used to *cut* projects that don't match, not just as aspirational labels.
>
> **Architecture Decision Records (ADRs):** Provide the written trail for why alignment decisions were made. When Ian disagrees with the Bazel decision but commits, having the reasoning documented means future leaders can understand the context without relitigating.
>
> **Backstage TechDocs / internal documentation platforms:** Enable the "sharing work to drive collaboration" pattern. When architecture and product strategy reviews are documented and discoverable, cross-team members can learn asynchronously rather than requiring synchronous attendance.
>
> **Portfolio management tools (Jira Portfolio, Aha!, ProductBoard):** Support the "only align on larger projects" principle by providing visibility into major initiatives without forcing teams to expose every task. The key is maintaining the one-developer-year threshold — below that, trust culture over tooling.

---

## Wrapping Up

How does alignment contribute to platform success? The only way to measure success is to agree on a target and aim for it. The detailed exercise of aligning teams and plans produces:
- A clearer understanding of focus areas
- Goals and work items to achieve them
- Evidence of whether your platform is getting better at what you've chosen to focus on

**The secret of this chapter:** Nothing about it is particularly unique to platform engineering. Shared purpose, strategic alignment, and execution planning are universal leadership requirements.

**What IS unique to platform engineering:** The value you produce is usually several steps removed from clear success measures like revenue growth. This leaves leadership with far more discretion to choose where to invest, which leads to the most common platform strategy failure — in the face of many possible paths and the challenge of hard alignment conversations, leaders just don't make decisions and let individual teams go their own way. This creates pockets of siloed success but prevents organizational greatness.
