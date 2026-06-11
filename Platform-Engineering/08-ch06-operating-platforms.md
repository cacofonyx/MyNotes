# Chapter 6: Operating Platforms

> **Part II — Platform Engineering Practices**

> *"Rare things become common at scale."* — Jason Cohen

This is the chapter most directly connected to SRE practice — and the one that bridges platform engineering's "product" aspirations with the operational reality of keeping complex systems running. The central tension: platforms create value through leverage and efficiency, meaning constant-sized teams support scaling systems. But scale brings new problems. If you don't routinely invest in operational practices — even when times are good — you end up in "operational hell," where neglected problems cause ongoing acute business impact, eroding customer trust and stalling all feature work.

The chapter covers three essential operational practices:
1. **On-call** — scheduling engineers to respond to production issues
2. **User support** — handling the constant stream of customer questions (separate from on-call)
3. **Operational feedback** — proactive practices that catch problems before they become acute (SLOs, change management, synthetic monitoring, operational reviews)

The authors emphasize throughout: these are **practices**, not processes. Practices provide a framework; processes are situational details you tailor to your team's specific problems. Don't force processes from your last job onto your current team — understand what problem you're solving and design the process to fit.

## Table of Contents

- [On-Call Practices](#on-call-practices)
  - [Why 24x7 Coverage Matters](#why-24x7-coverage-matters)
  - [Why Merged DevOps](#why-merged-devops)
  - [Getting to a Sustainable On-Call Load](#getting-to-a-sustainable-on-call-load)
- [Support Practices](#support-practices)
  - [Why Platform Engineers Should Do Support](#why-platform-engineers-should-do-support)
  - [Stage 1: Formalize Support Levels](#stage-1-formalize-support-levels)
  - [Stage 2: Separate Support from On-Call](#stage-2-separate-support-from-on-call)
  - [Stage 3: Hire a Support Specialist](#stage-3-hire-a-support-specialist)
  - [Stage 4: Engineering Support Organization at Scale](#stage-4-engineering-support-organization-at-scale)
- [Operational Feedback Practices](#operational-feedback-practices)
  - [SLOs and SLAs Are Necessary; Error Budgets Are Optional](#slos-and-slas-are-necessary-error-budgets-are-optional)
  - [Change Management](#change-management)
  - [Synthetic Monitoring](#synthetic-monitoring)
  - [Operational Reviews](#operational-reviews)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Deep Dive] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [AI Impact]

---

## On-Call Practices

### Why 24x7 Coverage Matters

Even "noncritical" platforms (developer tools, internal-only systems) can be critical at surprising times. Deployment tools need to work during off-hours deployment windows. A bug discovered at night needs to be deployed as a fix — and if the deployment platform is broken, the application team is stuck.

The authors acknowledge rare exceptions but are blunt: "Your team likely is not one of the exceptions." Ignoring 24x7 coverage to protect engineers from off-hours work undermines your ability to operate under unforeseen circumstances and risks losing customer trust.

### Why Merged DevOps

The authors take a clear position: **platform teams should use merged (not split) DevOps on-call.** Software engineers and systems engineers should be on the same team and the same rotation.

**Why:** Platform issues can be caused by in-house code, by underlying OSS/vendor systems, or by interactions between them. Only a merged team — with both software development expertise AND systems operational expertise — can staff an on-call rotation with the required breadth of knowledge.

**Why split doesn't work for most platform teams:**
- A dedicated SRE rotation requires 4-5 people minimum (nobody on-call > 25% of time)
- Most platform teams can't afford that much dedicated SRE headcount
- Companies fudge this by having SREs cover multiple platforms — losing the deep knowledge needed for complex issues
- This recreates the dev vs. ops finger-pointing from Chapter 1

**The trade-off:** You may have to exclude some great software engineers who don't have the skills or desire to be on-call. But unless you're building FAANG-scale platforms with 10+ engineers, the merged model is worth it.

> **[SRE/Production Lens: The Merged Model in Practice]**
>
> The authors' position here is a direct rebuttal of the Google SRE book's split model. Their argument: Google can afford dedicated SRE teams because their platforms have hundreds of engineers. Most companies can't.
>
> **What merged on-call actually means:**
> - Everyone on the platform team (software engineers AND systems engineers) rotates through on-call
> - Software engineers bring code-level expertise ("I know this service, I wrote this logic")
> - Systems engineers bring infrastructure expertise ("I know how Kafka behaves under this failure mode")
> - Together, they can diagnose issues that span both layers — which is where most platform incidents live
>
> **What it DOESN'T mean:**
> - It doesn't mean software engineers debug Kafka internals alone at 3 a.m. (they can escalate within the team)
> - It doesn't mean systems engineers fix application code bugs alone (same)
> - It means the on-call person is the *starting point* for triage, with deep team support available
>
> **The hiring implication from Chapter 4:** This is why the authors insist platform software engineers must be "comfortable being on-call for business-critical systems." If your SWEs can't do on-call, the merged model breaks and you're forced into the split model — which most teams can't afford.

### Getting to a Sustainable On-Call Load

**Target:** No more than **5 business-impacting pages per week.** On-call rotation no more than 1 week out of 4 (ideally 1 out of 6-8).

The authors cite Ian's experience at Amazon (2014): an organization experiencing operational hell after rapid growth. The new VP correlated developer survey data with pager load and found:
- **< 2 pages/week:** Happy team members
- **2-5 pages/week:** Some unhappiness, but no intention to leave
- **> 5 pages/week:** Consistent unhappiness AND negative response to "Do you see yourself on this team in 12 months?"

**Four steps to sustainable on-call:**

**1. Prioritize stability.** If you're above 5 pages/week, you're not providing a stable foundation. Put aside feature work and restore stability. Communicate to stakeholders why this is in their best interest.

**2. Eliminate false alarms.** False alarms make it impossible to measure real load. Some engineers resist eliminating them ("it's a useful pulse during deployments") — invest in dashboards as alternative feedback, then kill the false alarms.

**3. Use another platform team as secondary rotation.** Follow the SRE book's practice: two related teams serve as secondary for each other. The secondary can follow runbooks or escalate — but it should be extraordinarily rare for incidents to fall through to them.

**4. Don't rely on compensation to fix unsustainable load.** Paying for on-call won't make a bad situation better. It subsidizes management that neglects making load sustainable and encourages gamesmanship. Fix the root cause (reduce pages), then fair compensation becomes straightforward.

> **[Comparison: Implementing SLOs Book Connection]**
>
> The Implementing SLOs book (Hidalgo) discusses SLO-based alerting — only alerting when the error budget burn rate is significant. This is directly relevant here: SLO-based alerts naturally reduce false alarms because they alert on *impact patterns* (significant budget consumption) rather than *individual events* (any single error).
>
> If your platform has 100 alerts firing for individual error events that don't actually affect users, replacing them with a few SLO burn-rate alerts can dramatically reduce page volume while maintaining (or improving) detection of real problems.

> **[Real-World Implementations: On-Call and Incident Management]**
>
> **SLO-based alerting — Sloth (OSS):**
> The chapter argues that SLO-based alerts reduce false alarms by alerting on *impact patterns* rather than individual events. Sloth makes this practical: you define SLOs in YAML (e.g., "99.9% of API requests succeed within 500ms") and Sloth generates multi-window burn-rate Prometheus alerting rules automatically. Instead of 100 threshold alerts ("CPU > 80%", "latency > 200ms"), you get a handful of burn-rate alerts ("error budget is being consumed at 14x normal rate for the last hour"). This directly addresses the chapter's "5 pages/week" sustainability target — SLO-based alerting collapses noisy symptom alerts into fewer, high-signal budget-burn notifications. Pyrra adds a dashboard layer: visualize remaining error budget and historical burn patterns, making operational reviews data-driven.
>
> **Merged on-call + incident orchestration — Grafana OnCall (OSS) + incident.io:**
> The chapter advocates merged DevOps on-call where software engineers and systems engineers share rotation. Grafana OnCall handles the scheduling mechanics: rotation definitions, escalation chains, override swaps, and integration with alerting (Grafana, Prometheus, PagerDuty-compatible). When an alert fires, incident.io (or Rootly/FireHydrant) automates the response ritual: creates a dedicated Slack channel, pages the on-call engineer, links relevant runbooks, starts a timeline, and posts to the internal status page — all in seconds. This reduces the "figure out what's happening" phase the chapter describes, letting the merged team focus on diagnosis rather than coordination logistics.
>
> **Runbook automation — Rundeck (OSS) / Shoreline:**
> The chapter describes how platform teams often have secondary rotations that "follow runbooks." Rundeck operationalizes this: runbooks become executable jobs (restart a service, scale a deployment, drain a node, failover a database) that the secondary on-call can trigger with a button click — no SSH access or kubectl expertise required. Shoreline takes this further with "Op Packs" — pre-built remediation scripts that fire automatically on specific alert conditions (e.g., "if disk > 90%, run log cleanup"). This maps to the chapter's progression from "page a human" to "automated remediation with human oversight."
>
> **Post-incident analysis — Jeli (now PagerDuty):**
> The chapter emphasizes that incident analysis should identify systemic patterns, not just root causes. Jeli's approach matches: it ingests the incident timeline (Slack messages, alert history, status changes) and uses narrative analysis to surface contributing factors, communication breakdowns, and points where the system surprised responders. This feeds into the "monthly aggregation" practice the chapter recommends — Jeli tracks patterns across incidents (e.g., "60% of incidents involved config changes" or "MTTR increases when the primary on-call has < 3 months tenure").

---

## Support Practices

### Why Platform Engineers Should Do Support

The authors are emphatic: **your engineers must do support, not just be on-call.** Support is a different load from on-call (on-call handles urgent production issues; support handles questions, troubleshooting, bug reports, and guidance).

Why engineers resist: support feels low-leverage compared to writing code. Why it's essential: engineers removed from user problems build platforms with unrealistic expectations — expecting users to understand platform complexity, read documentation, and have empathy for the platform team's constraints.

> *"We have seen teams sending notices to users, chiding them for 'misusing the platform' and calling out 'badly behaving applications,' as though the platform's failure to protect against edge cases is the user's fault."*

This happens when teams lose touch with users. Support keeps the feedback loop alive.

### Stage 1: Formalize Support Levels

**First:** Categorize what's in those support tickets (production troubleshooting, bugs, usage questions, feature requests disguised as bugs, PR reviews, complex design questions). Once you understand the composition, investigate for repetition you can eliminate.

**Then:** Define your support SLA — under what conditions can a customer immediately page an engineer? What's the response time otherwise? The fundamental tension: incident managers want to page all dependencies proactively (reduces MTTR), but if your platform is a dependency of *every* team, you'll get paged for everything.

**Resolution requires investment in three areas:**
1. Strong postmortem follow-through ("why did this page happen at all?")
2. User-facing observability and synthetic monitoring (so customers/incident managers can rule out your platform without paging you)
3. Leadership willing to push back against unreasonable expectations

### Stage 2: Separate Support from On-Call

When support volume overwhelms the on-call person, create a separate **business-hours support rotation.** This means on a team of 6, about a third are doing operational work at any time — but it improves quality of both operational work and development work through separation of concerns.

**Warning:** If combined operational load exceeds 50%, you'll struggle to improve the platform. That's the signal for Stage 3.

### Stage 3: Hire a Support Specialist

When the team is overloaded despite good practices: hire a specialist. But resist hiring a full-time T1/T2 support engineer immediately — platform teams are too small to offer clear career growth within support tiers.

**Better approaches:**
- If temporary need: skilled contractor for T1+T2 work while you build improvements that reduce load
- If permanent need: hire someone with a nontraditional background (boot camp, IT, T2 product support) who wants to grow into platform engineering. Their first 12 months are support-heavy; their second year opens into normal platform engineering work. At the end, they've grown skills and you restart the cycle with someone new.

### Stage 4: Engineering Support Organization at Scale

At FAANG-scale, a company-wide support organization handles T1 across all platforms. The authors bring in a case study with five key practices:

1. **Tier applications differently** — Tier 0/1 (business-critical) get proactive monitoring; lower tiers get reactive support. Different alert thresholds per tier.
2. **Require customers to be on-call** — For Tier 0/1 apps, the app team must have 24x7 on-call too. Most incidents are caused by applications, not platforms.
3. **Hire systems engineers** — The merged DevOps model needs both SWEs and systems engineers. Systems hires raised the bar for operational work across the whole team.
4. **Create an expert network for T2 support** — Train advanced customers to be the first line of support for their peers. They combine platform knowledge with application knowledge. Incentivize them with direct-to-developer channel access.
5. **Constantly review with the support org** — Biweekly meetings to identify what support can handle independently vs. what needs escalation. Drives documentation and tooling investment.

> **[AI Impact: AI-Augmented Support and On-Call]**
>
> AI is already changing platform support and on-call practices:
>
> **For support (T1):**
> - AI chatbots trained on platform documentation can handle the simplest support questions (usage help, pointing to docs, common configuration guidance) — reducing T1 volume by 30-50% at companies that have deployed them
> - AI can auto-categorize incoming tickets, detecting patterns ("this is the 5th question about connection pooling this week — do we have a doc problem?")
>
> **For on-call triage:**
> - When an alert fires, an AI agent can correlate it with recent deployments, similar historical incidents, and related service logs — presenting the on-call engineer with a probable root cause hypothesis rather than just raw alert data
> - This reduces MTTR by compressing the "figure out what's happening" phase
>
> **For the expert network model:**
> - An AI trained on platform internals can serve as a "virtual expert" — answering questions that would otherwise require paging a platform engineer, or at minimum triaging whether a human expert is actually needed
>
> **The prerequisite (from the book):** "AI will help you operate better, but only if and where you have the data." Platforms with poor telemetry, undocumented runbooks, and tribal knowledge in people's heads can't benefit from AI operations support. Investing in observability and documentation is now doubly valuable — it helps humans AND enables AI assistance.

---

## Operational Feedback Practices

The third operational area: proactive feedback loops that catch problems before they become acute. Four practices:

### SLOs and SLAs Are Necessary; Error Budgets Are Optional

The authors take a nuanced position that will surprise SRE practitioners: they believe SLIs, SLOs, and SLAs are essential — but **error budgets have been oversold** and don't always justify their cost.

**Where they agree with standard SRE literature:**
- SLIs are great for monitoring issues
- SLOs are great for triggering deep dives
- SLAs (a small number of SLOs) help leadership and customers understand commitments
- "Failing minutes" of SLOs communicate why remedial action is needed

**Their problem with error budgets as commonly framed:** The literature frames error budgets as a *contract* — "as long as there is budget remaining, new releases can push." This creates "us versus them" dynamics, finger-pointing over thresholds and false positives, rather than focusing on the actual problem.

**Critical distinction: internal vs. customer-facing SLOs:**

| Aspect | Internal SLOs (for the team) | Customer-Facing SLOs |
|--------|------------------------------|---------------------|
| **Quantity** | More is better — maximize coverage | Fewer is better — a handful at most |
| **False positives** | Don't minimize — you might miss issues | Minimize aggressively — "boy who cried wolf" effect |
| **False negatives** | Require investigation | Embarrassing but tolerable with follow-through |
| **Purpose** | Understand operating conditions and risks | Help outsiders understand you have a problem |

Customer-facing SLOs/error budgets are an expensive additional cost on top of internal observability. Require them only when teams have issues severe enough to justify the investment — chronic availability problems or unrealistic customer expectations.

> **[Real-World Implementations: SLOs and Operational Feedback]**
>
> **SLO definition as code — OpenSLO + Sloth:**
> The chapter distinguishes internal SLOs (many, for the team) from customer-facing SLOs (few, for trust). OpenSLO provides a vendor-neutral YAML spec for defining both: you declare SLIs (what to measure), SLOs (what threshold matters), and alerting policies in version-controlled files. Sloth consumes these specs and generates Prometheus recording rules + multi-window burn-rate alerts. The workflow: platform team defines SLOs in a git repo → Sloth generates alerting rules → Prometheus evaluates them → Grafana dashboards show error budget remaining. This makes "SLOs as operational practice" repeatable and auditable rather than ad-hoc spreadsheet tracking.
>
> **Synthetic monitoring — Checkly (Playwright-based):**
> The chapter argues synthetic monitoring is the most underinvested practice for platforms — and that it should measure "latency, availability, AND correctness of function." Checkly implements this using Playwright (browser automation) or API checks running on a schedule from global locations. For a platform team, this means: a synthetic test that provisions a database every 5 minutes, verifies the connection string works, runs a query, and tears it down — exercising the full self-service path the way a real developer would. When a customer says "provisioning seems slow," you immediately check your synthetic dashboard. The chapter's "triangulation" benefit: if your synthetic sees it → platform problem; if it doesn't → customer-specific. Grafana Synthetic Monitoring integrates this directly into your Grafana/Prometheus stack, so synthetic results appear alongside real traffic metrics in operational reviews.
>
> **Change management via GitOps — Argo CD (CNCF):**
> The chapter says all production changes should be "documented, reviewed, and tested" — and references the 2017 S3 outage caused by a wrong CLI parameter. Argo CD encodes this principle architecturally: the only way to change production is to commit to a git repo. Every change has a PR (documented), a reviewer (reviewed), and CI checks (tested) before Argo syncs it to the cluster. The audit trail is the git log. For platform teams specifically, this addresses the chapter's concern about stateful systems — Argo's sync waves and hooks let you control ordering (e.g., "run database migration before deploying new API version"), and its auto-rollback on health check failure provides the safety net that platforms need given their low customer tolerance for interruptions.
>
> **Operational review dashboards — Grafana golden signals:**
> The chapter describes weekly operational reviews where engineers and management review pages, support issues, and SLI/SLO dashboards together. In practice, this looks like a Grafana dashboard with: (1) SLO burn-rate panels per service (are we consuming budget?), (2) page count this week vs. trailing 4-week average, (3) support ticket volume by category, (4) deployment frequency and rollback rate, (5) capacity utilization trends with 30/60/90-day projections. The dashboard IS the meeting agenda — anomalies visible in the panels drive the discussion. Teams that do this well export a weekly snapshot (via Grafana reporting or a bot) so the review starts with "here's what changed" rather than "let's stare at dashboards for 10 minutes."

> **[Comparison: Implementing SLOs Book — A Different Take on Error Budgets]**
>
> Alex Hidalgo's *Implementing SLOs* (which we have notes for) presents error budgets as the "third layer of the Reliability Stack" — a core component. The platform engineering authors are more skeptical, arguing that the *conversation* error budgets force is valuable, but the *contract* framing often creates more political friction than productive action.
>
> The reconciliation: error budgets work well when there's genuine tension between "ship faster" (product teams) and "keep things stable" (platform teams) — they quantify the acceptable risk. They work poorly when the platform team is already struggling with stability and the error budget just becomes another metric to argue about. Fix the stability first; introduce error budgets as a governance mechanism once things are healthy enough that the trade-off between speed and stability is *actually a choice* rather than a moot point.

### Change Management

All changes to production should be: **documented, reviewed, and tested** before handling production load. The authors know this sounds like old-fashioned change advisory boards — they're not advocating that. They're advocating lightweight rigor: a short writeup acknowledged by a team member.

**Why platforms specifically need this:** Platforms tend to be stateful and architecturally complex, with customers who have low tolerance for interruptions. A cache platform that clears cache during deployment induces latency spikes affecting customer applications. Standard CI/CD practices (canaries, shadow deployments, automated rollback) require more complex logic for platforms than for applications.

**The real purpose of change management:** It creates the *feedback* that tells you when you're relying on risky behavior — forcing investment in release engineering automation while the people who understand the system's sharp edges are still around.

The authors reference the **2017 Amazon S3 outage** — a nine-year-old service with hundreds of engineers suffered a 2-hour outage because one wrong parameter was entered in a command-line tool. If Amazon needs change management discipline at that scale, so do you.

### Synthetic Monitoring

Active monitoring that simulates users interacting with the production platform — measuring latency, availability, AND correctness of function. The authors consider this the most underinvested operational practice for platforms.

**Why platforms need synthetic monitoring more than most systems:** Platforms operate complex compositions of systems they didn't write (OSS, vendor, other internal services). Passive monitoring (metrics, logs, traces) can miss failures that only manifest through specific interaction patterns. Synthetic monitoring exercises the full system the way users do.

**Four benefits:**
1. **End-to-end monitoring** — covers gaps in passive monitoring. Best way to measure what customers actually experience.
2. **Customer understanding** — building synthetic tests forces engineers to experience their platform as users do (dogfooding lite).
3. **Operational understanding** — debugging flaky synthetic tests builds the same troubleshooting skills needed during real incidents (reduces MTTR).
4. **Triangulation** — when a customer reports a problem, you can immediately check: "Is our synthetic test seeing this too?" If yes → platform problem. If no → likely customer-specific issue.

**Cost estimate from Ian's AWS experience:** 25% of ongoing development time and 10% of platform resource cost. Significant — but justified by the operational confidence it provides.

### Operational Reviews

Weekly meetings where engineers and management review operational health data together. The practice that "closes the loop" — converting observability data into action.

**Team-level (weekly, 30-60 min):** Review pages, support issues, postmortems, production changes, SLI/SLO dashboards. Curated by the person coming off on-call.

**Org-level (monthly):** Postmortems for highest-impact incidents + metric review with discussion of outliers. Well-curated by SREs to avoid wasting time on irrelevant detail.

**Why leadership engagement matters:** The point is to shift engineering time in response to operational data. If managers aren't in the room making those prioritization calls, the loop can't close. Engineering managers need to be engaged — blameless — making it clear they're accountable for maintaining a balanced investment between operations and features.

> **[Core Concept: Why Application Engineers Roll Their Eyes at Operational Reviews — And Why Platform Engineers Can't]**
>
> Ian shares a personal anecdote: before joining AWS, he worked on application systems and considered operational reviews "nonessential and burdensome." His applications were simple because *platforms abstracted the complexity*. His team managed < 2 pages/week without formal reviews.
>
> Then he moved to AWS and worked on EMR (a platform product). Same person, simpler codebase, but much higher operational load — because the platform was *composed of many underlying systems.* Operational reviews were "the only thing that kept small problems from mushrooming to dominate the time of everyone on the team."
>
> The lesson: if you're building applications ON platforms, you may not need formal operational reviews. If you're building THE platform, you almost certainly do — because the complexity you're absorbing from your users has to be managed somewhere, and that somewhere is in these reviews.

---

> **[Real-World Implementations: Support Practices]**
>
> **Slack-native ticketing — Halp (Atlassian):**
> The chapter describes how support volume grows with a broad user base, and Stage 1 is "formalize support levels." Halp turns Slack messages into tracked tickets without forcing developers to leave their workflow — they emoji-react a message and it becomes a ticket with SLA tracking, assignment, and categorization. This solves the chapter's specific concern: when support is in Slack, you can't measure it (no volume data, no categories, no SLA tracking). Halp adds structure without adding friction — developers stay in Slack, platform team gets metrics on ticket composition and response times that the chapter says are needed to identify repetition and invest in elimination.
>
> **AI-augmented T1 support — RAG over platform docs (LangChain + vector DB):**
> The chapter's Stage 3 discusses hiring support specialists, but the AI Impact section notes AI can handle simplest T1 questions. In practice: platform teams index their documentation, runbooks, and past support tickets into a vector database, then expose a Slack bot that uses retrieval-augmented generation to answer questions like "how do I configure connection pooling?" or "what's the max database size for Standard tier?" The bot cites specific doc pages. This reduces T1 volume by handling the "usage questions" and "edge cases during onboarding" categories the chapter identifies — freeing engineers for the complex "application-specific production issues" that require human judgment. Glean (enterprise AI search) provides this as a product across all internal systems, not just platform docs.
>
> **Docs-as-code for self-serve — Backstage TechDocs:**
> The chapter says "every support interaction should ask how do we prevent this question from being asked again." TechDocs implements the answer: documentation lives alongside code in each repo (Markdown files), gets auto-published to the Backstage portal on merge, and appears contextually when developers browse services in the catalog. The loop: platform engineer answers a support question → writes the answer in a docs PR → merged → next person asking the same question finds it in Backstage before filing a ticket. The key design choice: docs are reviewed in PRs alongside code changes, so when the platform changes, documentation updates are part of the same commit — preventing the staleness that makes wikis useless.
>
> **Expert network — Stack Overflow for Teams / GitHub Discussions:**
> The chapter's Stage 4 describes creating "expert networks" of advanced customers who support peers. Stack Overflow for Teams makes this searchable: questions and answers accumulate into a knowledge base that compound over time. Unlike Slack (where answers scroll away), SO/Teams answers are findable by future askers. GitHub Discussions provides a similar pattern repo-adjacent. The chapter's incentive model ("direct-to-developer channel access") maps to giving top answerers early access to beta features or dedicated office-hours slots.

---

## Wrapping Up

If you come from a systems background, little here is new — operational discipline has always been your culture. This chapter is written for those with development backgrounds who need to understand that platform success requires discipline in all three areas: on-call, support, and operational feedback.

The through-line: **invest in operational practices routinely, even when times are good.** The worst time to start caring about operations is when you're already in operational hell. By then, feature work is stalled, trust is eroding, and it takes months to recover. Proactive investment prevents that spiral.
