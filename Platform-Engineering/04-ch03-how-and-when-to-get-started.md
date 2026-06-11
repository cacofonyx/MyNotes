# Chapter 3: How and When to Get Started

> **Part II — Platform Engineering Practices**

> *"Once upon a time, there were three little pigs. One pig built a house of straw, while the second pig built his house with sticks. They built their houses very quickly and then sang and danced all day because they were lazy. The third little pig worked hard all day and built his house with bricks."* — "The Three Little Pigs"

This is the chapter that answers "okay, but when do we actually START doing platform engineering?" — and the answer depends entirely on where your organization is today. The authors address three different starting points, each with its own advice:

1. **Small startups (~5–50 engineers):** You don't need a platform team yet. Foster cooperation around shared code and tooling.
2. **Growing companies (~50–250 engineers):** The cooperative model is breaking down. It's time to create your first formal platform team — but don't over-engineer it.
3. **Large established companies:** You already have infrastructure teams. The challenge is transforming them from traditional operations into platform engineering — a cultural shift, not just a technical one.

The authors' framework metaphor is fitting: sometimes it's perfectly fine to build with straw or sticks. What matters is knowing when you need bricks — and not building a brick fortress when a straw hut would serve you better.

## Table of Contents

- [Fostering Platform Cooperation at Small Scale](#fostering-platform-cooperation-at-small-scale)
  - [Stage 1: Ad Hoc — Just Getting Started](#stage-1-ad-hoc--just-getting-started)
  - [Stage 2: Somewhat Managed — Hunting and Gathering](#stage-2-somewhat-managed--hunting-and-gathering)
  - [Knowing When to Move Up](#knowing-when-to-move-up)
- [Creating the Platform Teams That Replace Cooperation](#creating-the-platform-teams-that-replace-cooperation)
  - [Are the Benefits Worth the Costs?](#are-the-benefits-worth-the-costs)
  - [Realize the Collective Dynamic Is Gone](#realize-the-collective-dynamic-is-gone)
  - [Focus on Solving Problems, Not New Technology](#focus-on-solving-problems-not-new-technology)
  - [Beware of New Engineers from Big Companies](#beware-of-new-engineers-from-big-companies)
  - [Be Slow to Hire Product Managers](#be-slow-to-hire-product-managers)
  - [Bonus: Integration/Shared Services Platforms](#bonus-integrationshared-services-platforms)
- [Transforming a Traditional Infrastructure Organization](#transforming-a-traditional-infrastructure-organization)
  - [Your Whole Engineering Culture Has to Change](#your-whole-engineering-culture-has-to-change)
  - [Identify the Most Promising Areas to Start](#identify-the-most-promising-areas-to-start)
  - [Don't Just Add Product Managers](#dont-just-add-product-managers)
  - [Change Support, Hiring, Recognition, and Structure](#change-support-hiring-recognition-and-structure)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Deep Dive] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [AI Impact]

---

## Fostering Platform Cooperation at Small Scale

This section is contributed by **James Turnbull** — a DevOps pioneer, author of books on Puppet, Docker, and Prometheus, and an experienced startup executive. His perspective: at early-stage companies, platform engineering is overkill. What you need is cooperation — lightweight shared practices that keep things from devolving into chaos without the overhead of a dedicated team.

The key principle throughout this section: **"Is this core business for me? If not, outsource it."** At a small startup, almost nothing about infrastructure is core business. Your core business is finding product-market fit. Everything else should be as low-effort as possible.

### Stage 1: Ad Hoc — Just Getting Started

When you're a few engineers sitting around a table building a product, you don't need platform engineering. You need the bare basics and speed. The focus: removing friction between code being written and code being deployed.

**What to do:**
- **Always use source control.** (Sounds obvious, but many startups start later than you'd think.)
- **Automated continuous deployment.** Get code from merge to production with minimal human intervention. Use off-the-shelf platforms (Heroku, Vercel, Netlify, Northflank). Does your app need Kubernetes from day one? **No, it does not. Seriously, no.** Don't overthink future scaling — if you go from 10 users to 100,000, that's a great problem to solve later.
- **Lightweight process.** Track work in a simple ticket system. Don't overcomplicate with formal Agile ceremonies. Turnbull cites Kevin Stewart's adaptation of Michael Pollan's food laws: *"Use a process. Not too much. Mostly agile."*

**What NOT to do:** Don't rush to create a platform team. You don't have the resources, and you'll risk slowing the rapid iteration you need. Cooperative part-time efforts are much better at this stage.

> **[Core Concept: "Is This Core Business?"]**
>
> This question is the guiding principle for all technology decisions at early-stage companies, and it's worth internalizing even at larger orgs:
>
> - CI/CD pipeline? Not core business → use a hosted service (GitHub Actions, CircleCI)
> - Monitoring? Not core business → use a SaaS (Datadog, Sentry)
> - Database? Not core business → use a managed service (RDS, PlanetScale)
> - Feature flags? Not core business → use a SaaS (LaunchDarkly, Flagsmith)
> - The billing logic for your specific product? Core business → build it yourself
>
> The trap startups fall into: treating infrastructure as a fun engineering challenge rather than a means to an end. Engineers love building things. But at Stage 1, building your own CI/CD system is the same mistake as a restaurant building their own stove instead of buying one. Your job is to cook food (build product), not manufacture kitchen equipment (build infrastructure).

### Stage 2: Somewhat Managed — Hunting and Gathering

As the startup finds product-market fit and grows (roughly 20-50 engineers), pressures increase. More people interacting with the codebase means more complexity in writing, reviewing, merging, and deploying. Platform components emerge — not as a formal initiative, but as managed infrastructure evolving from the ad hoc stage.

**Key changes at this stage:**

**Local development:** Automate the local development environment. Start simply (shell script around containers), but evolve to colocating dev environment setup with source code. Git hooks can prompt updates as part of normal pull/push workflows.

**More robust testing and deployment:** Going directly to production gets riskier with more engineers. Invest in:
- Better test coverage (measure it, grow it, enforce "no tests, no merge")
- Branch-based deployments / ephemeral environments
- Feature flags (buy, don't build — it's not core business)

**Observability:** You should have basic metrics and alerting for your platform and workflows by now. Extend your existing product observability to cover your development infrastructure too.

**Infrastructure automation:** Fully manage your production environment with infrastructure-as-code. Use this as the foundation for CI/CD and ephemeral environments.

**Socialize decision making:** As changes affect more people, individual developer choices must be considered in the broader context. Introduce a lightweight RFC (Request for Comments) or ADR (Architecture Decision Record) process. Keep it lightweight — but make the pattern of "propose, discuss, decide" formal enough that people can't just unilaterally adopt new tools that affect everyone.

> **[Organizational Reality: Knowing When Stage 2 Is Breaking]**
>
> Turnbull is honest: "Often, the first time you know a tool or process is at breaking point is when it breaks." You don't get a polite warning. One failure cascades into others.
>
> Signs that you're outgrowing Stage 2:
> - The same person keeps getting pulled into every infrastructure decision because nobody else understands the system
> - Deployments are failing more often, and debugging them requires institutional knowledge that only 1-2 people have
> - New engineers take weeks to become productive because the development environment is fragile and undocumented
> - Security patches sit unapplied because nobody owns the responsibility
> - Two teams made incompatible infrastructure choices and now can't integrate their services
>
> When these signals appear, it's time for Stage 3 — creating a real platform team. But the transition needs to be deliberate, not reactive.

---

## Creating the Platform Teams That Replace Cooperation

This section addresses the critical transition: when cooperative, ad hoc shared ownership stops working, and you need a dedicated platform team. This usually happens around **Dunbar's number** — when the cooperative group reaches 50-250 people and it's no longer possible for everyone to know all other members. At that point, you need formal ownership and accountability.

The authors' key framing: **even at companies that already have platforms, each new platform team usually struggles out of the gate.** The cooperative mechanisms, despite their flaws, were in place and functional. A new centralized team displaces them — and creates new conflicts that didn't exist before (who's responsible for what? the platform team or the customer team?).

### Are the Benefits Worth the Costs?

Before creating a platform team, ask whether centralization actually provides **leverage** — not just efficiency. The argument "we could have 2 engineers building a common platform instead of 5 engineers working on similar code" is insufficient. Centralizing anything creates a new coordination point that makes application teams' jobs harder. The bar should be: **does centralization provide outsized value that is hard to replicate?**

A useful quick test: if the system requires a large team to build and maintain, and it can support multiple teams without significant per-team customization — it's a good candidate for platforming. But if it has a small build cost and each team wants to extend it differently — it's probably better left decentralized.

> **[Core Concept: Leverage vs. Efficiency — The Centralization Test]**
>
> This distinction is crucial and often confused:
>
> - **Efficiency argument:** "Five teams each spend 10% of their time on caching. One team could do it for all of them." This sounds compelling but ignores coordination costs. Now those five teams depend on a central team's priorities, timeline, and abstractions. They've traded 10% of their time for a dependency relationship that may slow them down by more than 10%.
>
> - **Leverage argument:** "Our billing system touches 12 regulatory frameworks, requires PCI compliance, handles multi-currency, and integrates with 5 payment processors. No individual team can build this to the required quality. A centralized team with deep domain expertise can build it once, correctly, and serve 8 product lines." This is genuine leverage — the centralized team creates value that individual teams *cannot replicate* on their own.
>
> **The test:** Ask yourself: "Can each team reasonably solve this themselves?" If yes (caching, basic CI/CD, simple APIs), centralization is efficiency — nice to have, but not always worth the coordination cost. If no (billing compliance, database reliability at scale, security infrastructure), centralization is leverage — and probably necessary.
>
> Some things seem like leverage but aren't: "Do you really have to have only one caching solution? Does every team need to use the same standardized web framework?" Sometimes the answer is genuinely no — and forcing standardization here creates coordination costs without proportional value.

### Realize the Collective Dynamic Is Gone

When a new platform team forms, there's often nostalgia for the old ways. Application engineers remember when they could "just open a PR on the shared codebase." They complain that the new team creates process, slows things down, and adds bureaucracy.

The authors acknowledge this is real — but also inevitable. What worked for 50 people cannot work for 500. The challenge goes both directions:
- **Customers** have rose-colored glasses about the old cooperation model and resist change
- **Platform teams** underestimate how much change costs have grown — they think "five good engineers in a room" can still represent all perspectives, but with more users and use cases, they can't

### Focus on Solving Problems, Not New Technology

When a new platform team inherits a messy codebase (poor API boundaries, duplicate implementations, library-level shared code), it's tempting to step back and propose a grand rearchitecture with new technology. The authors firmly advise against this:

**Why the new-technology approach fails:**
- At this scale, a full migration may take *years* to complete
- New tech won't help your in-production teams with pressing problems *today*
- It takes potential resources away from faster fixes to current systems
- Your team has zero trust so far — only goodwill. Trust requires delivering value quickly.

**What to do instead:** Detangle, don't rearchitect. Fix the most pressing problems in the existing mess. Deliver incremental value fast. Think of your job as "detangling more than rearchitecting." Build trust through quick wins before proposing larger transformations.

> **[Anti-Pattern: The "Let's Rewrite It" New Platform Team]**
>
> This is one of the most common failure modes for newly formed platform teams. It happens because:
> 1. The team is formed from strong engineers who are excited about "doing it right"
> 2. They inherit a mess (because if it were clean, there wouldn't be a need for a dedicated team)
> 3. They propose building a clean v2 from scratch, because the existing system is "beyond saving"
> 4. They spend 12-18 months on the v2 while the existing system continues to rot
> 5. By the time v2 is ready, requirements have changed, trust has evaporated, and application teams have built workarounds
>
> **The authors' prescription:** Deliver value within the first 3 months — even if it's ugly. Fix the thing that's causing the most pain right now. Show that you're making things better, not just planning to make things better someday. Only propose larger changes after you've earned trust through demonstrated delivery.
>
> Chapter 8 (Rearchitecting Platforms) goes deep on how to do major architectural changes *correctly* — incrementally, safely, while maintaining trust.

### Beware of New Engineers from Big Companies

A cautionary note about hiring: when staffing a new platform team, be careful about senior engineers from very large tech companies (Google, Amazon, Meta). They've "seen the next order of magnitude of scale" — but they didn't work on platforms at *your* current scale. They know what the fully delivered solution looked like at a much larger company with a different culture.

The risk: they arrive very confident they know the answer, because they've seen a working solution at scale. But they don't know what the right solution is for *your scale, culture, and constraints*. They'll push for big-company patterns that don't fit.

The authors aren't saying never hire these people — just interview for skills and attitude, not big-company credentials. The "design" interview slot is a good place to detect this: if candidates always jump to "at Big Company X we used Technology Y" without analyzing trade-offs for the current context, they'll likely do the same on the job.

### Be Slow to Hire Product Managers

The authors give specific timing advice: you need a fully staffed and working engineering team *before* hiring product managers, and you need to wait even longer for project managers. Three reasons:

1. **Optics:** Hiring non-engineers before proving engineering delivery suggests you can't communicate with customers yourself — which looks bad.
2. **Early work is straightforward:** In the first year or two, the work is mostly obvious problem-solving through tech build-out. Engineers and EMs can do lightweight requirements gathering.
3. **Culture setting:** Early engineers and EMs need to build the habit of customer empathy firsthand. If you bring in a PM too soon, engineers will offload customer interaction and never develop that muscle.

**Ratios the authors recommend:**
- Product managers: between the number of team-level managers and managers-of-managers (roughly 1 PM per 2-4 teams)
- Project managers: about 1 per 50 platform engineers (and ideally never go above that ratio)

> **[Organizational Reality: Why Too Many Project Managers Is a Smell]**
>
> If you think you need more project managers than 1:50, the authors say you should instead invest in better platform abstractions. If your migrations require extensive cross-team coordination tracked by project managers, that's a sign your platform's interfaces aren't clean enough — changes leak across boundaries, requiring human coordination where software should provide isolation.
>
> In other words: needing lots of project management is often a *symptom* of poor platform architecture, not a *solution* to organizational complexity. Fix the architecture, and the coordination problem shrinks.

### Bonus: Integration/Shared Services Platforms

The authors briefly address a special case: platform teams that horizontally support multiple *external* products (billing, user identity, mobile app frameworks, shared application services like notifications and search). These are trickier because they have surface area visible to external customers.

**Key challenges:**
- You need an external-facing product manager earlier (business-facing decisions require it)
- But watch out for PMs who prioritize only customer-visible UI polish (the "bike shed") while core architecture (the "nuclear plant") rots
- **Discoverability** is a major problem: engineers at your company may not know your platform exists and will build their own solution instead. Don't give platforms cutesy names — call your billing platform "Billing Platform," not "Glengarry"

These teams are "stuck in the middle" — between application teams above and core infrastructure below. They get errors from both directions and may lack the privileged access that core platform teams have. Keep them aligned with core platforms even if they're not in the same org chart.

---

## Transforming a Traditional Infrastructure Organization

The final section addresses the hardest scenario: large companies where the move to platform engineering means transforming an existing infrastructure engineering organization. This requires not just a skill set change but a **major cultural change** — from siloed, process- and tech-focused to portfolio-, usability-, and customer-focused.

### Your Whole Engineering Culture Has to Change

The authors are blunt: "Yes, seriously."

Traditional infrastructure organizations are good at many things: cost management, vendor negotiations, running systems at scale, deep specialization (databases, networking, kernel debugging), triaging bug requests, coordinating migrations.

What they're usually NOT good at: thinking about the people who use their systems, taking user preferences into account, and treating internal users as customers to be retained. Why would they be? Their users are usually a captive audience — there's no alternative to the central infrastructure team.

A culture focused on cost, scale, and process over people and usability is very hard to change. And you don't want to lose those rare specialization skills in the process.

### Identify the Most Promising Areas to Start

Don't try to change everything at once. Start with teams that are already closest to platform engineering: those delivering modern offerings, with concentrations of software engineers, bespoke software with high rates of change, and large pent-up demand for modernization (e.g., moving from VMs to containers).

Look for teams with a blend of software engineers and systems engineers — they're primed for the transition.

### Don't Just Add Product Managers

> *"Recognize That You Can't Just Rub Product Managers on It and Call It a Day"*

Even if you could find enough good PMs who want this type of job, they're useful only when paired with *willing* engineering teams. If the engineering teams don't feel ownership for delivering a great product, PMs become "glorified backlog groomers" rather than true product leaders.

Start introducing product-oriented approaches in areas that are already more customer-centric. Expand from there.

### Change Support, Hiring, Recognition, and Structure

The authors list specific organizational changes needed for the transformation:

**Change support practices:** The ticket system "black hole" makes customers feel like a burden. Engineers should spend time directly supporting their products. If a senior engineer can't engage productively with users, "this person is probably not building products that are easy to use."

**Update interviews:** Add "customer empathy screening" to all hiring. Even simple questions: "How do you think about writing code so other developers can understand it?" This sets the tone that platform engineers must think about users, not just systems.

**Update recognition and rewards:** If you only promote people who solve big technical problems, you'll lose the people who smooth usability edges, listen to customers, and fix pain points. Ensure your engineering ladder and promotion criteria include product-oriented work, not just technical depth.

**Limit project managers:** Too many project managers is a signal that your platform's interfaces require too much human coordination for changes. Force engineers to own project management work — the good ones will build automation to avoid it, which benefits everyone.

**Accept team restructuring:** Some leaders and senior ICs won't make the cultural jump. That's okay — but don't let them block the transition.

**Keep it fun:** By the time companies attempt this transition, there's often an adversarial relationship between infrastructure and application teams. Celebrate improvements. Share kudos. Make the culture shift feel like an exciting opportunity, not a punishment.

> **[Comparison: DevOps Transformation Parallels]**
>
> The authors explicitly draw the parallel: this cultural shift echoes the DevOps/SRE transformation from a decade ago. Engineers in SRE/DevOps organizations stopped "throwing code over the wall to ops." In the same way, platform engineering asks engineers to stop "building infrastructure without considering its users."
>
> Both transformations ask more of engineering teams. Both deliver higher-quality outcomes. Both are expensive and take time. The DevOps transformation taught the industry that "dev and ops are one concern." The platform engineering transformation teaches that "infrastructure and developer experience are one concern."
>
> If your organization successfully adopted DevOps — you've already done a version of this cultural change once. Platform engineering is the next iteration: not just "dev and ops together" but "dev, ops, AND product thinking together."

> **[AI Impact: AI Accelerating the Transformation]**
>
> For organizations undergoing the infrastructure → platform engineering transformation, AI can help bridge capability gaps during the transition:
>
> - **Documentation generation:** Infrastructure teams that never wrote user-facing documentation can use AI to generate initial docs from code, config files, and tribal knowledge — then refine them with user feedback. This is faster than waiting for a "documentation initiative" that never happens.
>
> - **Self-service MVP:** Before building a full self-service portal, an AI chatbot trained on your platform's documentation and APIs can answer common questions and guide users through standard workflows. It's not a replacement for proper self-service, but it bridges the gap while you build it.
>
> - **Customer empathy at scale:** AI can analyze support tickets, Slack messages, and incident reports to surface patterns ("70% of questions this month are about database connection pooling configuration"). This gives the transforming team product-oriented insights without requiring every engineer to read every ticket.
>
> - **Interview assistance:** Teams building customer empathy interviews for the first time can use AI to generate scenario-based questions that test for product thinking — calibrating their interview process faster.
>
> None of these replace the fundamental cultural change. But they lower the activation energy for teams that want to transform but don't know where to start.

---

## Wrapping Up

The chapter maps three journeys to platform engineering:

| Starting Point | Key Advice | Main Risk |
|---------------|-----------|-----------|
| **Small startup** (5-50 eng) | Don't create a platform team. Foster cooperation. Automate deployment. Keep it simple. | Over-engineering too early. Building platform infrastructure when you should be building product. |
| **Growing company** (50-250 eng) | Create a platform team when cooperation breaks down. Deliver value fast. Don't rearchitect immediately. | Hiring for big-company patterns, adding too much process, losing connection to customer teams. |
| **Large enterprise** (transforming infra org) | Change the culture, not just the tools. Start with willing teams. Update hiring, promotion, support practices. | Trying to transform everything at once. Losing specialized skills. Getting blocked by resistant leaders. |

The unifying thread: **start where you are, not where you wish you were.** Don't build a Platform with a capital P before you need one. Don't add enterprise processes to a startup. Don't rearchitect a working system just because it's ugly. Solve today's problems, build trust through delivery, and expand from there.

> **[Core Concept: The Timing Decision — "When Is It Time?"]**
>
> Across all three starting points, the authors identify similar signals that it's time to evolve:
>
> - A single failure cascades because nobody owns the shared thing that broke
> - Growth in the team/product creates coordination problems the current model can't handle
> - Engineers are spending increasing time on infrastructure/platform work that isn't their core focus
> - The quality of shared systems is declining because volunteer maintenance isn't enough
> - Security, compliance, or reliability requirements exceed what ad hoc cooperation can deliver
>
> The meta-principle: you don't need platform engineering until you do. When you need it, you'll know — because something will break, and nobody will be accountable for fixing it. The goal is to recognize the signal *slightly before* the crisis, rather than *during* it. This chapter gives you the framework to recognize those signals earlier.
