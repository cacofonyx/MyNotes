# Chapter 9: Migrations and Sunsetting of Platforms

> **Part II — Platform Engineering Practices**

> *"A platform is meant to be the stable thing that provides an enduring surface to build on, like a foundation. Platform engineering requires building those stable foundations and not externalizing work onto the things that people build on top of it."* — C. Scott Andreas

Migrations are the existential challenge of platform engineering. The underlying systems never stop changing: security patches, vendor changes, hardware updates, EKS/EoL timelines compressing from decades to 1-2 years. Without a deliberate strategy, platforms become a source of migration pain that outweighs their value. But here is the key insight: great platform teams see migrations as an opportunity to prove their value. They absorb the pain of mandatory change so application teams can focus on delivering features.

The chapter covers three domains: (1) engineering practices that make migrations cheaper and more transparent, (2) coordination practices that smooth the human side of migrations, and (3) sunsetting — the special case of migrating to nothing. The authors are pragmatic throughout: sometimes deadlines and mandates are necessary, but they should be the option of last resort, not the default approach.

A migration, as defined here, is any mandatory change to your platforms that requires some work by users to adopt — a spectrum from data center moves, to backward-breaking API changes, to in-place upgrades needing acceptance testing.

## Table of Contents

- [Migration Antipatterns](#migration-antipatterns)
  - [Context-Free Deadlines](#context-free-deadlines)
  - [Unclear Requirements](#unclear-requirements)
  - [Untested Migrations](#untested-migrations)
  - [Clipboard-Carrying Scolds](#clipboard-carrying-scolds)
- [Engineering Easier Migrations](#engineering-easier-migrations)
  - [Tackle Migrations Early](#tackle-migrations-early)
  - [Use Product Abstractions That Minimize Glue](#use-product-abstractions-that-minimize-glue)
  - [Architect for Transparent Migrations](#architect-for-transparent-migrations)
  - [Agreements: Chaos Testing, Acceptance Tests, Maintenance Windows](#agreements-chaos-testing-acceptance-tests-maintenance-windows)
  - [Do Monorepos Help with Migrations?](#do-monorepos-help-with-migrations)
  - [Track Usage Metadata](#track-usage-metadata)
  - [Centrally Track Ownership Metadata](#centrally-track-ownership-metadata)
  - [Develop Automation to Avoid Clipboards](#develop-automation-to-avoid-clipboards)
  - [Document On-Ramps and Off-Ramps](#document-on-ramps-and-off-ramps)
- [Coordinating Smoother Migrations](#coordinating-smoother-migrations)
  - [Scope, Limit, and Prioritize Planned Changes](#scope-limit-and-prioritize-planned-changes)
  - [Communicate Early and Publicly](#communicate-early-and-publicly)
  - [Push Through the Final 20%](#push-through-the-final-20)
  - [Use Mandates Sparingly](#use-mandates-sparingly)
- [Sunsetting Platforms](#sunsetting-platforms)
  - [Deciding When to Sunset](#deciding-when-to-sunset)
  - [Coordinating the Sunsetting](#coordinating-the-sunsetting)
  - [Don't Be Afraid to Sunset When It Makes Sense](#dont-be-afraid-to-sunset-when-it-makes-sense)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [Real-World Implementations]

---

## Migration Antipatterns

The authors identify four recurring antipatterns that make migrations painful across the industry. These compound: context-free deadlines create stress, unclear requirements waste time, untested systems generate failures, and then someone gets tasked with chasing everyone down.

### Context-Free Deadlines

Deadlines handed down from on high with no discussion or appreciation for what teams will have to defer. Sometimes the deadline is legitimate (end-of-life date), but it arrives as short notice because everyone ignored the migration for months. The deadline scramble doesn't feel better just because the procrastination was collective.

### Unclear Requirements

Migration notices that start with "If you're using Product X version Y or earlier..." where half the users don't even know what Product X is. They either ignore the notice or spend hours figuring out whether it applies to them.

### Untested Migrations

Users try to migrate and the new offering doesn't work. Gaps in the new offering, broken features, missing instructions. The platform team scrambles to fix things, piling on tech debt just to make the deadline.

### Clipboard-Carrying Scolds

People tasked with chasing users through meeting after meeting: are you on track? Why not? What will it take? "Wall of shame" dashboards that add stress, defensiveness, and frustration — especially when users tried to migrate but got blocked by broken features.

> **[Anti-Pattern: The Migration Pain Spiral]**
>
> The four antipatterns are not independent — they form a self-reinforcing cycle:
>
> 1. **Context-free deadline** arrives with short notice
> 2. Users scramble to figure out **unclear requirements** — who does this even apply to?
> 3. Those who try find an **untested migration** with broken features and gaps
> 4. Progress stalls, so management deploys **clipboard-carrying scolds**
> 5. Scolds report blockers, but by then there's no time left to fix them properly
> 6. Tech debt is incurred to hit the deadline
> 7. Next migration starts with even less trust from application teams
>
> The authors acknowledge that deadlines and clipboards may sometimes be necessary as **last resort** — but they become toxic when used as the default approach. The key distinction: have you done everything possible through engineering, automation, and communication first?

> **[SRE/Production Lens: Migration Risk as Operational Risk]**
>
> From an SRE perspective, every migration is an operational risk multiplier:
> - **Rushed migrations** produce undertested configurations that fail under production load
> - **Simultaneous migrations** confound root-cause analysis when things break (is it the OS upgrade or the auth change?)
> - **Forced deadlines** push teams to skip validation, creating latent reliability issues that surface weeks later as pages
>
> The chapter's antipatterns map directly to incident patterns: the "context-free deadline" causes hurried changes that become the next P1. The "untested migration" IS a deployment with no canary or rollback plan. Treating migrations with the same rigor as production deployments — canary analysis, gradual rollout, automated rollback — is the operational mindset this chapter argues for.

---

## Engineering Easier Migrations

The first and primary approach should always be engineering, not process. Before communication planning, program management, or mandates — think about what you can build to ease migration pain now and in the future.

### Tackle Migrations Early

At small scale, migrations are annoying but you can lean on goodwill and scrappy engineers. At hundreds of engineers, scrappy energy breaks down. Migration support should be one of the first things a new platform team tackles — not "perfect rearchitecture to make future migrations cheap," but doing whatever scrappy work you can to make the next pressing migration as cheap as possible.

> **[Core Concept: Migrations as First Platform Investment]**
>
> This is a subtle but critical prioritization insight. When you form a platform engineering team, the temptation is to immediately start building the "right" architecture. The authors say: don't. Instead, take the next painful migration that's bearing down on the organization and reduce its cost. Why?
>
> 1. **Immediate trust-building** — you demonstrate value before asking anyone to trust your grand vision
> 2. **Real learning** — you discover actual dependencies, ownership gaps, and automation opportunities
> 3. **Credibility for later** — "they made the last migration painless" earns you political capital for architectural changes
>
> This echoes the Chapter 3 advice: start with real problems, not theoretical architectures.

### Use Product Abstractions That Minimize Glue

"Glue" (from Chapter 1): code, automation, and configuration built to hold disparate systems together. Glue is OK in moderation, but the more glue that exists, the more work required when any piece changes. The problem is worst when every application team has created its own glue.

A good platform abstraction means application teams have minimal glue of their own to change during migration of underlying components. Limiting the number of versions of the same system reduces testing permutations.

> **[Core Concept: Glue as Migration Tax]**
>
> Every piece of glue code an application team writes is a future migration tax they'll have to pay. The math:
> - 50 application teams x custom glue per team = 50 separate migration efforts
> - 50 application teams using a platform abstraction = 1 migration effort (by the platform team)
>
> This is the fundamental leverage argument for platforms, but stated through the lens of change cost rather than build cost. It also explains why platform teams that don't limit variation suffer: supporting 5 versions of Kafka means testing 5 migration paths, not 1.

### Architect for Transparent Migrations

The ideal migration: customers don't have to do any work and never even see it. The platform provides a stable interface while the team executes migrations with minimal to no customer impact.

The authors recommend achieving this with a combination of judicious APIs and technologies that make it easier to run multiple versions in production during migration:

- **Container-based packaging** for fast, lightweight application deployment
- **Autoscaling** that supports changing system size without restarts
- **Deployment techniques** (canary, blue/green) combined with advanced health monitoring for fast rollback

These support both application teams deploying their software AND platform teams updating the platform without disrupting developers.

> **[SRE/Production Lens: Transparent Migration as Advanced Deployment]**
>
> A "transparent migration" is really just a deployment — but of the platform itself rather than an application. The same SRE principles apply:
>
> | Deployment Principle | Migration Application |
> |---------------------|----------------------|
> | Canary analysis | Migrate 1% of workloads, compare error rates |
> | Blue/green | Run old and new platform versions simultaneously |
> | Progressive rollout | Move customers in waves, not all at once |
> | Automated rollback | Detect regression, move workloads back to old version |
> | Health monitoring | Customer-facing SLIs, not just platform-internal metrics |
>
> The key difference: platform "deployments" affect other people's workloads, not your own. This means you need **external** signals (customer SLIs, acceptance tests) not just internal ones. You can't just check that your pods are healthy — you need to verify that customer applications are still behaving correctly on the new version.

### Agreements: Chaos Testing, Acceptance Tests, Maintenance Windows

To take full advantage of transparent migration capabilities, you need agreements with users up front:

**Chaos testing and stability guarantees:** If you want blue/green upgrades, you need to restart processes and move workloads. If users expect the underlying system will never restart, they won't handle the change. Solution: add automatic chaos (random node restarts) to force customers to detect and fix structural bugs and get used to not controlling underlying infrastructure.

**Acceptance tests:** Ask users to maintain tests you can run to validate their applications work after a platform change. Your platform team also needs its own thorough acceptance tests — ideally a sample application you own and operate as the first validation pass.

**Maintenance windows:** Nothing "cloud native" about them, but when planned downtime is necessary, don't negotiate ad hoc. Create up-front expectations of when maintenance is allowed so both teams can plan.

> **[Worked Example: Chaos Testing as Migration Enabler]**
>
> The authors describe a team that added automatic chaos to their managed Kubernetes offering — randomly restarting customer nodes as a default behavior (with an opt-out for legacy systems). This served dual purposes:
>
> 1. **Forced customers to build resilient applications** — applications that can't handle a node restart can't handle a blue/green platform upgrade either
> 2. **Established the norm** that infrastructure providers could restart instances — so when a real platform migration moved workloads, it wasn't a surprise
>
> This is brilliant because it converts a one-time migration negotiation ("can we restart your pods?") into a continuous baseline expectation. By the time you need to do a real migration, customers have already proven their workloads handle restarts gracefully.
>
> Compare to Netflix's Chaos Monkey — same principle but applied to platform operations rather than application resilience. The goal isn't just "applications should be resilient" but "we need the freedom to operate the platform without asking permission every time."

> **[Comparison: Google SRE and Platform Migration Agreements]**
>
> The agreements here parallel structures from the Google SRE books:
>
> | This Chapter | Google SRE Equivalent |
> |-------------|----------------------|
> | Acceptance tests | SLO-based validation ("is the user still within their error budget?") |
> | Chaos testing | DiRT (Disaster Recovery Testing) exercises |
> | Maintenance windows | Planned maintenance risk budgets |
>
> The difference: Google SRE frames these as observational (we measure whether you're OK), while this chapter frames them as contractual (we agree up front what "OK" means and who maintains the tests). The contractual approach is more practical for platform teams that don't have the luxury of massive SRE organizations monitoring everyone's SLIs.

### Do Monorepos Help with Migrations?

Short answer: not much for platform migrations specifically. The authors explain why the apparent benefit is limited:

1. **Platforms have service components** — any client/API change isn't complete until all clients redeploy. Since customers won't redeploy on your schedule, you need multiple API versions regardless.
2. **Thick clients depend on external code** — OSS/vendor libraries used by platforms are also used directly by customers for other purposes, creating coupled changes. You can version internal clients to manage this, but that defeats the monorepo value.

Monorepos help more for pure in-house library changes than for platform migrations generally.

> **[Organizational Reality: The Monorepo as Migration Silver Bullet]**
>
> This is a refreshingly honest take that pushes back against a common belief at large tech companies: "if only we had a monorepo, migrations would be easy because we could change everyone's code at once."
>
> The reality: even at Google (the canonical monorepo company), platform migrations are still hard, still take years, and still require program management. The monorepo helps with *code-level* dependency changes (update an import, change a function signature) but does nothing for *system-level* migrations (upgrade the database engine, move to a new compute platform, change the networking model).
>
> Platform migrations are hard because they involve running systems, not just code. You can't `sed` your way through a Kafka version upgrade — you need to actually run both versions, validate behavior, and coordinate cutovers.

### Track Usage Metadata

One of the trickiest parts of migrating: understanding dependencies. Build automatic asset tracking for technologies, deployments, and dependencies. Create graphs of running infrastructure.

Things to track:
- Who is using the platform
- Which applications are using which parts of the platform
- Who owns those applications

This is much easier to build at a smaller company than to backfill into a legacy environment. Make sure you gather metadata about the state of the world, know what is deployed where, and understand how to tie code/deployments to people and teams.

### Centrally Track Ownership Metadata

Tracking ownership (which teams/individuals own specific systems) helps run smooth migrations, target communication, and operate well. While each platform could track this separately, centralizing avoids suffering from organizational drift.

> **[Organizational Reality: Organizational Drift as Migration Blocker]**
>
> The authors describe a scenario every growing company experiences: people come and go, and now there are technology assets still used but no one owns. Cron jobs no one has looked at for ages. Forgotten data pipelines that run until they break and everyone scrambles to figure out who's responsible.
>
> **Why this blocks platform engineering specifically:**
> - A massive data pipeline hogging platform resources with no owner means the platform team can't get it fixed or migrated
> - Platform engineers can help application developers, but can't own those applications long-term
> - During migrations, "who owns this?" becomes a showstopper question
>
> **The recommendation:** Partner with HR to establish offboarding processes that reassign system ownership. Create automatic tracking that ties technology assets to human ownership and reassigns when people leave or move teams.
>
> This is one of those problems that seems like "someone else's job" until it completely blocks your platform migration. The authors say directly: if no one else is thinking about how systems react to organizational changes, it falls to you to prompt the conversation.

> **[SRE/Production Lens: Asset Tracking as Incident Readiness]**
>
> Asset and dependency tracking isn't just for migrations — it's critical for incident response:
> - During an incident: "who owns the service that's calling us 10x normal rate?" If you can't answer this in minutes, your MTTR suffers.
> - During a migration: "which teams need to validate before we cut over?" If you can't enumerate all consumers, you'll miss someone and break them.
> - During capacity planning: "what's growing fastest on our platform?" If you don't track usage by team/application, you can't forecast or charge back.
>
> The authors frame this as "metadata for migrations" but operationally it's a prerequisite for running any complex platform at scale. A service mesh with observability (what calls what, how often, who owns it) is both a migration tool and an operational tool.

### Develop Automation to Avoid Clipboards

A good platform team makes migration painless through planning and automation. A bad one exposes developers to churn and pain. Rather than giving up and running everything through human clipboard carriers, use this as an opportunity to think about system design and automation.

> **[Worked Example: Camille's OS Upgrade Story]**
>
> Camille managed a base platform team that owned standard Linux distributions. The company had performance-sensitive C/C++, making distribution upgrades painful. A delayed upgrade had dragged on so long they risked losing vendor support for even the newer version.
>
> **The request:** The team wanted headcount to hire project managers to manage the next upgrade.
>
> **Camille's pushback:** "I will allow hiring of project managers only when you've proven we've done everything we can to automate the work those project managers might do. Show me we've tried without PM and hit the wall."
>
> **The result:** The team discovered upgrades were a dependency tree — one system couldn't upgrade until subsystems were validated. They built:
> 1. A **dependency map** tied to a migration cadence
> 2. **Automatic detection** of when dependencies were complete, triggering the next step
> 3. **Context-rich tickets** explaining what a user needed to do, delivered at the right time
> 4. **Observability and tracking workflow tools** built with customers in mind
>
> The migration still needed some human PM work toward the end, but it was a massive improvement. The team took on the heavy lifting so there was "little debate when it came time for customers to finish."
>
> **The principle:** "You must plan for and take on the bulk of the work for customer migrations if you want to claim this role" as a modern platform team.

> **[Core Concept: Automation Before Program Management]**
>
> The sequence matters:
> 1. First, automate everything you can — dependency detection, sequencing, customer notification, validation
> 2. Then, see what's left that actually requires human coordination
> 3. Only then hire PMs for the irreducible human coordination work
>
> Most teams invert this: they hire PMs first, who then create spreadsheets, meetings, and status reports for work that could have been automated. The PM becomes the clipboard carrier — not because the work requires human judgment, but because no one invested in automation.
>
> This doesn't mean PMs are never needed. It means: prove the automation wall before adding humans. The automation you build for one migration pays dividends for every future migration. The PM spreadsheet dies when the project ends.

### Document On-Ramps and Off-Ramps

When migrations can't be automated for customers (e.g., moving to a new service management platform), consider the on-ramps and off-ramps. Show customers how to do partial migrations — move parts of their system to test the new platform before committing all traffic.

Usage-level documentation (API descriptions, code samples, getting started guides) is usually underinvested in, but migrations are a case where it's a major differentiator. Since migrations are one-off exercises, you can write documentation once without worrying about it becoming outdated.

**How to figure out what documentation/automation you need:** Dogfooding and partnership.
1. Have other platform teams go through as alpha testers
2. Approach advanced customers as early adopters
3. Embed your team members with early customers during their migration
4. Use insights from early teams to smooth the process for everyone else

> **[Core Concept: Dogfooding Migrations]**
>
> The testing strategy for a migration is different from testing a product:
>
> | Product Testing | Migration Testing |
> |----------------|-------------------|
> | Does the feature work? | Does the transition path work? |
> | Can users accomplish tasks? | Can users move their existing workloads? |
> | Is the API correct? | Is the gap between old and new bridgeable? |
> | What's the happy path? | What are the edge cases that block completion? |
>
> You need real users going through the actual migration to discover the real problems. Your own team using the platform is incomplete — you know too much about the internals. Early customer partners give you "fresh eyes" on the migration experience, revealing missing tools, documentation gaps, and broken assumptions.

---

## Coordinating Smoother Migrations

Most migrations require some coordination with customers despite your best engineering efforts. The goal: make it as easy as possible while balancing your own team's workload.

### Scope, Limit, and Prioritize Planned Changes

Three forms of limiting accidental overlap:

**1. Scope backward from hard deadlines in the next 12 months.**

Some migrations are beyond your control (OSS deprecation, vendor API changes). These "immovable objects" restrict later choices — work out how to handle them as soon as possible.

Key insight: deadlines beyond 12 months are far more nominal than they seem. When a wide swath of industry is affected, dates slip, and industry-wide solutions often emerge (e.g., AWS shipping "Classiclink" so customers didn't need bespoke VPC migration solutions). Don't force users to migrate today based on events well beyond their planning period — it creates friction and is often wasted work.

For deadlines >12 months out: spend the time making the migration easier. Leave heavy coordination until the 12-month horizon.

**2. Limit coupling of in-flight customer work.**

Don't bundle migrations unless the bundle reduces net customer work. Two cases:

- **OK to bundle:** When migration already requires rearchitecture (e.g., on-prem VMs to containers), adding related changes (auth upgrade) doesn't add much complexity. Works best when migration is somewhat optional with high value.
- **Don't bundle:** When you have a hard deadline (data center lease expiring), limit other changes. Resist piling on restrictions just because teams "have to migrate anyway."

**3. Keep track of major outstanding requests and prioritize.**

Don't do a major OS upgrade and company-wide auth change in the same quarter. Platform leadership should see planned migrations across all teams and ask: should these happen simultaneously? What's the impact of overlap?

> **[SRE/Production Lens: Migration as Change Management]**
>
> This section maps directly to SRE change management principles:
>
> - **Don't stack changes** — The same reason you don't deploy multiple services simultaneously (can't isolate failures) applies to migrations. If you're doing an OS upgrade and an auth migration in the same quarter, and things break, which one caused it?
> - **Respect the blast radius** — A migration that touches every application team has company-wide blast radius. Treat it like you'd treat a company-wide infrastructure change: staged rollout, monitoring at each stage, hold points.
> - **The 12-month rule** — This is essentially a "planning horizon" for change management. Beyond 12 months, requirements are too uncertain to commit teams to action. Within 12 months, you have enough signal to plan concretely.
>
> The practical implication for platform teams: maintain a **migration calendar** analogous to a deployment calendar. When two migrations want to overlap, someone needs to make the priority call — just like two teams wanting to deploy to the same shared system simultaneously.

### Communicate Early and Publicly

Tell customers about migrations as soon as you know they're coming (information-only for >12 month deadlines). Build migrations into roadmaps, repeat through newsletters, quarterly planning, and frequent customer engagements.

For changes requiring platform-layer work: hold off until confident the project is closer to shipping and you know what customer work will be — perhaps once you have an alpha customer on the new version.

At large scale, application teams may designate someone to evaluate incoming migration requests. When customers are creating "migration intake roles," it's time to formalize migration coordination. Checks for your annual planning process:

- Where are known major changes coming that will require customer work?
- Where can you bundle related changes to reduce work? Where should you delay due to planned churn?
- Does your plan give enough confidence to communicate major changes for the next 2-3 quarters?

**Dedicated communication channel:** Public, well-curated. Customers often help each other through common gotchas. Use it to collect FAQs and identify rough edges to automate.

> **[Core Concept: The Communication Asymmetry]**
>
> There's a fundamental asymmetry in migration communication:
>
> - **Platform team's perspective:** "We told everyone 6 months ago in the newsletter"
> - **Application team's perspective:** "I get 50 platform emails a month, most don't apply to me, and by the time one does, it's already urgent"
>
> The solution isn't just "communicate more" — it's communicate *relevantly*. This requires the usage/ownership metadata from the previous section: if you know who uses what, you can target communication to the people who actually need to act, rather than broadcasting to everyone and hoping the right people notice.
>
> The dedicated channel serves a different purpose: it's pull-based (I go there when I'm actively migrating) rather than push-based (another email in my inbox). Pull channels work because they reach people at the moment they're ready to act.

### Push Through the Final 20%

You've automated 80% of the workload. The remaining 20% is still there — highest-risk applications, oldest, most critical, most customized. The last 5% might seem impossible.

**Three complications of the final 20%:**

**1. It takes longer than you think.** Someone must run the old system for as long as migration takes. If you allow most of the team to focus entirely on the new system, people stuck on legacy feel underappreciated, burn out, and leave. Figure out the work balance ahead of time.

**2. Unexpected dependencies surface.** Example: Camille's team was in final migration stages when the data center team insisted old servers had to be replaced (dying fans). Her team had to negotiate getting only the fans replaced rather than buying new servers for a 6-month remaining timeline.

**3. Unclear ownership of the final work.** Will the platform team do it? The application teams? You may discover the new system won't work for some edge-case users (leading to sunsetting). For the rest, expect ongoing negotiation. The better the new platform and the migration experience so far, the more trust and willingness you'll find among laggards.

> **[Organizational Reality: The Last 20% Problem]**
>
> The final 20% is where migrations die — not because of technical impossibility, but because of organizational fatigue:
>
> - **The platform team** is excited about the new system and wants to move on
> - **The remaining users** are the ones who had the hardest time migrating (most customized, most legacy, most edge-case)
> - **Management** sees 80% done and declares victory, reallocating people
> - **The old system** becomes a "zombie" — still running, minimally staffed, slowly degrading
>
> The authors' warning about team morale is crucial: if you leave 1-2 people maintaining the old system while everyone else works on the exciting new thing, those people WILL leave. This is a leadership failure, not an individual failure. Plan the staffing model for the full migration timeline, including the unglamorous final phase.
>
> **The SRE parallel:** This is identical to the "toil reduction" problem. Toil that's 80% automated still requires 20% human work — and that 20% is often the hardest, most irregular, most frustrating part. The remaining 20% of migrations IS toil in its purest form.

### Use Mandates Sparingly

At scale, you lose the personal trust that made migrations work when the company was small. People instinctively fight migration work because they've seen migrations go sideways before.

**The mandate temptation:** Get the CTO to declare everyone must complete the migration. But:
- You're competing with many other "must do" initiatives (cost-cutting, compliance, security, business expansion)
- There's limited organizational attention for mandates
- People stop paying attention when too many mandates accumulate

**Better approach:** Save mandate requests for truly essential work and align them with other mandatory efforts:
- Platform improves security posture AND saves money? Go in with the CISO and CFO.
- Business wants to change pricing? Great time to uplift the billing platform.
- Mandates are most effective for the final 20% when "we all know this is the right thing."

**Warning:** Overusing mandates creates a culture where application engineers feel they only exist to serve platform team projects. This destroys the product relationship.

> **[Organizational Reality: Mandate Economics]**
>
> Think of mandates as a scarce organizational currency:
>
> - A company can absorb maybe 2-3 organization-wide mandates per year before "mandate fatigue" sets in
> - Every mandate you spend on a migration is one you can't spend on security, compliance, or cost optimization
> - Unlike money, mandate currency depreciates with overuse — the 5th mandate of the year carries far less weight than the 1st
>
> **Strategic alignment** is the force multiplier: if your migration aligns with something leadership already cares about (cost reduction, security posture, regulatory compliance), it doesn't cost a "mandate slot" — it rides along with another initiative's mandate. This is political sophistication, not manipulation: you're making it easy for leadership to approve work that serves multiple goals.
>
> The authors' framing — "strategically planning migrations as part of other important work" — is the mature platform leader's approach to organizational dynamics.

> **[Comparison: Team Topologies and Migration Friction]**
>
> Team Topologies (Skelton & Pais) would frame the migration challenge as a **cognitive load** problem:
>
> - Every migration adds extraneous cognitive load to application teams (work that doesn't directly deliver user value)
> - Platform teams exist to absorb intrinsic complexity and reduce extraneous load
> - When migrations externalize work onto application teams, the platform is failing its fundamental Team Topologies purpose
>
> The "X-as-a-Service" interaction mode from Team Topologies is what this chapter's "transparent migration" achieves: the platform provides a service, and the underlying implementation changes without the consumer needing to know or act. The "collaboration" mode is what the final 20% requires: platform and application teams working together to solve edge cases.
>
> The Manager's Path (Fournier) also connects here: the "clipboard-carrying scold" is what happens when you assign responsibility without authority. The person chasing migrations has neither the power to mandate nor the engineering capacity to help — just a spreadsheet and a meeting invite.

---

## Sunsetting Platforms

Sunsetting is different from migration: you're not just moving people from one system to another — you're asking them to move off without providing a near-equivalent replacement. You may not have capacity to support a full migration, but you still need to ease the transition.

### Deciding When to Sunset

**First rule:** For widely used legacy systems that need to be turned off, don't go directly to sunsetting. First figure out a path to another offering. True sunsetting should be reserved for:

**1. There are not very many users.** Common scenarios:
- Prematurely expanded the product to support configurations that few people need
- A new product team insisted on a specific subtype (e.g., a graph database for one feature) that didn't pay off
- Built a workflow that only a tiny group adopted (superuser features, particular interaction models)

**2. The cost of supporting the offering is high.** Low-adoption systems that require high support burden. The cost may be indirect — complex and fragile features make other platform changes harder too.

**3. You have other things to focus on.** When you need to redirect engineering investment elsewhere, sometimes the only way to free bandwidth is to get rid of distractions.

If sunsetting because of redeployment pressure: get specific about where you'll redeploy people. Include this in your communication to impacted users and stakeholders.

> **[Anti-Pattern: Premature Sunsetting Without Empathy]**
>
> The authors include an explicit warning: platform teams can lack empathy with edge-case customers, taking an attitude of "they should have known that would never scale." This is not product-centric.
>
> **When this backfires:** If you try to remove features critical for more than a small number of edge cases, you generate enough backlash to force supporting both offerings indefinitely — the worst possible outcome. You end up maintaining more than if you'd handled the sunset properly.
>
> **The rule:** Make sure removed features really impact only the tail 0.1% of use cases, and begin sunsetting only after early consideration and communication of all options. Sunsetting should come at the very tail end of a migration, when you're down to customers deeply coupled to a feature that cannot be supported by the new system.

> **[Organizational Reality: When Builders Resist Sunsetting]**
>
> One of the most insightful observations in the chapter: sometimes it's not customers who resist sunsetting — it's the team that built the system.
>
> **The story:** A build and test tool that the team had been trying to make work for years. A few application teams were using it, but no clear path to broad adoption. The original problems it was solving had mostly been resolved. Supporting both old and new was too much.
>
> **The hardest part:** Getting the team to accept their project was at a dead end. They wanted so much for their investment to succeed that acceptance was nearly as hard as the actual sunsetting.
>
> **The cautionary tale:** It took more than leadership pushing — it took the die-hard believers *leaving the team* to actually finish killing the initiative. When you staff a team through passion about a particular technology, those people are likely to leave if that technology doesn't pan out.
>
> **Why this matters for leaders:**
> - Sunk cost fallacy is emotional, not rational — you can't logic people out of attachment to their creation
> - Long-running "almost there" projects drain energy from the whole team, not just believers
> - Sometimes you need to be willing to lose people in order to make the right strategic decision
> - The longer you delay the sunset conversation, the more invested (and resistant) the team becomes

### Coordinating the Sunsetting

Options for executing a sunset:

**1. Can you give the system back to the consuming team?** Sometimes the burden is beyond your capacity but another team is dependent enough to operate it themselves. Negotiate: they may expect you to give them people, but you're cutting because you don't have people to spare. Offer training and a transition timeline with pairing. Moving 1-2 people may be worth freeing up many others.

**2. Identify possible off-ramps:**
- Document steps to migrate to a different system so they understand the effort
- Connect them with customers who've already been through it
- Explain how they might build their own version using your platform (if it's a minor feature)
- Show how to get the same outcomes with different tools/features

**3. Talk to users directly and create timelines with their input.** If you're sunsetting, the user base should already be small — talk to them, don't just send announcements. Be prepared to negotiate timelines (quarters to years, depending on size and criticality). Give as much warning as possible.

> **[Core Concept: The Sunsetting Spectrum]**
>
> Sunsetting isn't binary — it's a spectrum of options:
>
> | Option | When to Use | Cost to You |
> |--------|------------|-------------|
> | Transfer to consuming team | Team dependent enough to self-operate | Training + maybe 1-2 people |
> | Provide migration path to alternative | Another system covers 80%+ of use cases | Documentation + support |
> | Help them build their own | Minor feature, capable team | Consulting time |
> | Hard cutoff with timeline | Low-impact feature, tiny user base | Communication + negotiation |
>
> The worst option — which the authors implicitly argue against — is neglect: stop investing in the system without formally sunsetting it. This creates a zombie platform that still incurs operational cost (pages, security patches, infrastructure) while providing no path forward for users. It's worse than a clean sunset because the uncertainty prevents users from planning.

### Don't Be Afraid to Sunset When It Makes Sense

It's not fun to tell stakeholders you can't support them, but it's worse to degrade everyone's experience because your team is spread too thin supporting one-off offerings. Edit your offerings when something goes almost nowhere. The right thing for the company sometimes means disappointing a few people.

---

## Wrapping Up

Migrations and sunsetting are two of the least fun parts of owning a platform. No one likes making customers do work just to stay in place — migrations feel like a tax. But this is exactly why the authors see migrations as one of the biggest opportunities for platform teams.

The key argument: the levy will come whether application teams use your platforms or a smattering of cloud/OSS/vendor systems. ALL underlying software must be updated occasionally. The promise of platform engineering is minimizing the cost of change for the whole organization through better automation, communication, and execution.

Common themes echoed throughout:
- Think about users and their experience
- Do as much as you can up front to make that experience better
- Communicate thoughtfully and often
- Find places where software and automation replace manual processes
- When hard conversations are necessary (sunsetting), the trust you've built makes them easier

> **[Real-World Implementations: Migration Tooling and Practices]**
>
> **Dependency tracking and migration orchestration — Backstage (Spotify, OSS):**
> The chapter emphasizes tracking who uses what, who owns applications, and managing migration as a dependency graph. Backstage's software catalog provides exactly this: a registry of all services, their owners, dependencies, and metadata (language, framework version, deployment target). When a platform migration requires action, you can query Backstage to identify every affected team rather than broadcasting blindly. The TechDocs plugin lets you publish migration guides alongside the catalog entries for affected services. Backstage's scaffolder ("Golden Path" templates) can also generate migration PRs — if the change is mechanical (update a dependency version, swap a config value), the template creates the PR and assigns it to the owning team automatically. This is the automation-before-clipboards approach in practice.
>
> **Progressive delivery and transparent migrations — Argo Rollouts / Flagger (OSS):**
> The chapter's "architect for transparent migrations" section describes running multiple platform versions simultaneously and gradually moving workloads. Argo Rollouts and Flagger implement this pattern for Kubernetes: define a rollout strategy (canary with 5%/25%/50%/100% traffic steps), attach analysis (Prometheus queries checking error rates and latency), and the controller automatically promotes or rolls back based on metrics. For platform migrations specifically, you can use this to migrate workloads from old infrastructure to new: route a small percentage of traffic to services running on the new platform version, validate SLIs, then progressively increase. If SLIs degrade, traffic automatically shifts back. This converts a risky "big bang" cutover into an observable, reversible progression.
>
> **Ownership tracking and organizational drift — OpsLevel / Cortex:**
> The chapter's warning about organizational drift (people leave, ownership becomes unclear, abandoned systems block migrations) is addressed by service ownership platforms. OpsLevel and Cortex maintain a live registry mapping services to teams, with automatic staleness detection: if a team is dissolved or an owner leaves, the system flags orphaned services. They also track "maturity scorecards" (does this service have runbooks? acceptance tests? documented owners?) that directly feed migration readiness: you can query "which services on platform v1 have owners AND acceptance tests AND are ready for migration?" versus "which are orphaned and need intervention first." This is the metadata layer the chapter argues you need.
>
> **Migration-as-workflow — Terraform / OpenTofu + Atlantis:**
> For infrastructure platform migrations (moving between regions, upgrading cloud services, changing networking), Terraform's plan/apply model provides natural on-ramps and off-ramps. Teams can `terraform plan` to see exactly what a migration will change before committing. Atlantis (or Spacelift/Env0) adds collaboration: the migration plan runs as a PR comment, reviewable by both platform and application teams, with the apply gated on approval. For large-scale migrations, you can generate per-team Terraform changes programmatically (the "automation to avoid clipboards" approach) and open PRs against each team's infrastructure repo with the exact changes needed — no clipboard carriers, just PR reviewers.
>
> **Chaos engineering as migration enabler — Litmus (OSS) / Gremlin:**
> The chapter describes adding chaos (random node restarts) as a default to establish the norm that infrastructure can change without notice. Litmus provides Kubernetes-native chaos experiments: pod kill, node drain, network partition, disk fill — run as CronJobs to continuously validate workload resilience. By running these as baseline chaos (not just pre-migration testing), you establish the "agreement" the chapter describes: applications must handle restarts, and if they can't, they discover that continuously rather than on migration day. Gremlin adds targeting and safety: limit blast radius to specific namespaces, automatically halt experiments if error rates spike, and generate reports showing which services are chaos-ready (and thus migration-ready).

> **[SRE/Production Lens: Migration as the Ultimate Reliability Test]**
>
> The chapter's argument — that migrations are an opportunity to prove platform value — has a deeper SRE implication: a migration is the ultimate test of your platform's operational maturity.
>
> **What a smooth migration proves:**
> - You have accurate dependency graphs (you know who's affected)
> - You have working observability (you can detect problems during rollout)
> - You have rollback capability (you can undo if things go wrong)
> - You have automation (you can execute at scale without human error)
> - You have trust with customers (they believe you when you say "this will work")
>
> **What a painful migration reveals:**
> - Undocumented dependencies ("we didn't know Service X depended on that")
> - Missing observability ("we didn't notice the regression for 3 days")
> - No rollback path ("we can't go back, we already decommissioned the old system")
> - Manual processes that don't scale ("we need 50 engineers to do this by hand")
> - Broken trust ("last time they said it would be painless, and it wasn't")
>
> In this sense, treating migration quality as a reliability metric (track migration completion rate, customer-reported issues during migration, time-to-complete, rollbacks required) gives you an ongoing signal about platform operational health — not just during the migration itself.
