# Chapter 3: Managerial Leverage — Part 3

> **High Output Management** — Andrew S. Grove
> *Time Management as Production, Span of Control, and Interruptions*

Part 1 covered the output equation and five managerial activities. Part 2 covered the leverage equation, high/negative leverage, and delegation. Part 3 completes the chapter with Grove's most practical material: applying production principles to manage a manager's most finite resource — time. He also addresses span of control (how many subordinates?) and the universal plague of interruptions.

## Table of Contents

- [Time Management via Production Principles](#time-management-via-production-principles)
  - [Find Your Limiting Step](#find-your-limiting-step)
  - [Batch Similar Activities](#batch-similar-activities)
  - [Your Calendar as a Production Planning Tool](#your-calendar-as-a-production-planning-tool)
  - [Say No Early](#say-no-early)
  - [Build in Slack](#build-in-slack)
  - [Carry a Project Inventory](#carry-a-project-inventory)
  - [Standardize Approaches](#standardize-approaches)
- [Span of Control: How Many Subordinates?](#span-of-control-how-many-subordinates)
  - [The 6-8 Rule](#the-6-8-rule)
  - [The Acting-as-Subordinate Trick](#the-acting-as-subordinate-trick)
- [Interruptions: The Plague of Managerial Work](#interruptions-the-plague-of-managerial-work)
  - [Standard Responses](#standard-responses)
  - [Batch Interruptions into Meetings](#batch-interruptions-into-meetings)
  - [The Indicator Archive](#the-indicator-archive)
  - [Office Hours, Not Hiding](#office-hours-not-hiding)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Production Thinking] [Practical Toolkit] [Anti-Pattern] [Scenario] [Mental Model]

---

## Time Management via Production Principles

Grove's core insight: **treat your workday like a factory, not a job shop.** A job shop reacts to whatever comes in the door. A factory forecasts, plans, and runs on a schedule. Most managers run their days like a job shop — reacting to interruptions, letting their calendar fill passively, and feeling perpetually fragmented. Grove applies production principles one by one.

### Find Your Limiting Step

> *"First, we must identify our* limiting step: *what is the 'egg' in our work?"*

Some activities are immovable — they *must* happen at a specific time. For Grove, it's the class he teaches: 200 students will be there regardless. For you, it might be a weekly all-hands, a standing architecture review, or an on-call rotation handoff.

> *"If we determine what is immovable and manipulate the more yielding activities around it, we can work more efficiently."*

> **[Practical Toolkit: Map Your Limiting Steps]**
>
> **Step 1:** Open your calendar for next week. Highlight every event that is truly immovable — cannot be rescheduled, has external dependencies, others are counting on your presence at that exact time.
>
> **Step 2:** These are your "eggs." Everything else should be offset around them, just as Grove offsets toast and coffee around the egg in Chapter 1.
>
> **Step 3:** Schedule your highest-leverage discretionary work (deep thinking, coaching, strategy) in the gaps between immovable commitments — don't leave those gaps to be filled by whoever sends a meeting invite first.
>
> **Common limiting steps for Senior EMs:**
> - Monday leadership sync (immovable — director expects attendance)
> - Wednesday architecture review (immovable — cross-org dependency)
> - Friday team retrospective (immovable — team expects your presence)
> - 1-1s with direct reports (semi-immovable — high leverage, shouldn't be displaced)
>
> Everything else — email, status meetings, document reviews, planning work — should flow around these fixed points.

### Batch Similar Activities

> *"Any manufacturing operation requires a certain amount of set-up time. So for managerial work to proceed efficiently, we should use the same set-up effort to apply across a group of similar activities."*

Just as the continuous egg-boiler has set-up time when changing from three-minute to four-minute eggs, managerial work has *mental* set-up time. Context-switching between unrelated tasks incurs a cognitive cost.

Grove's examples: if you have reports to read or performance reviews to approve, *"set aside a block of time and do a batch of them together, one after the other, to maximize the use of the mental set-up time needed for the task."*

> **[Senior EM Application: Batching Your Week]**
>
> | Activity Type | Batching Strategy |
> |--------------|------------------|
> | **1-1s** | Block them on the same day(s) — "1-1 Tuesday" means you're in coaching/listening mode all day, not switching between coding context and people context |
> | **PR/code reviews** | Set a 30-min block each morning — review mode once, not 5 context switches throughout the day |
> | **Email/Slack triage** | Two blocks daily (morning, late afternoon) — don't live in the inbox |
> | **Document writing** (strategy docs, RFCs, reviews) | Block 2-hour chunks — deep work can't happen in 15-minute fragments |
> | **Administrative tasks** (approvals, expense reports, scheduling) | One 30-min block, end of day Friday — batch all the low-leverage-but-necessary work |
> | **Postmortem review** | One session per week — read all recent postmortems together, spot patterns across them |

### Your Calendar as a Production Planning Tool

Grove makes a distinction that changes how you think about your calendar:

> *"Most people use their calendars as a repository of 'orders' that come in. Someone throws an order to a manager for his time, and it automatically shows up on his calendar. This is mindless passivity."*

Instead:

> *"To gain better control of his time, the manager should use his calendar as a 'production' planning tool, taking a firm initiative to schedule work that is not time-critical between those 'limiting steps' in the day."*

The calendar should be **proactive** — you fill it with your planned production schedule — not **reactive** — others fill it with demands on your time.

> **[Core Concept: The Calendar as Factory Schedule]**
>
> This is a paradigm shift. Most managers are *scheduled* — their calendars are controlled by others (meeting invites, requests, escalations). Grove says be a *scheduler* — plan your production week in advance, with time blocks for high-leverage activities, and treat incoming requests as orders that must compete for capacity.
>
> **The factory analogy:**
> - **Job shop manager:** Takes whatever work comes in. No ability to plan. Constantly interrupted. Feels busy, produces little.
> - **Factory manager:** Has a production schedule. Knows what will be produced when. Can accept new orders that fit, rejects orders that exceed capacity. Produces predictably.
>
> Your calendar is the production schedule for the factory that is your management work. Run it like a factory.

### Say No Early

> *"It is important to say 'no' earlier rather than later because we've learned that to wait until something reaches a higher value stage and then abort due to lack of capacity means losing more money and time."*

This is the "detect problems at the lowest-value stage" principle from Chapter 1, applied to your time. Saying no to a meeting request on Monday is cheap. Accepting it, attending, realizing it's a waste at minute 30, and leaving is expensive — you've lost the time AND disrupted the meeting.

> *"Remember too that your time is your one finite resource, and when you say 'yes' to one thing you are inevitably saying 'no' to another."*

> **[SRE Lens: Saying No to Protect Leverage]**
>
> SRE managers are particularly vulnerable to saying yes to everything because so much feels urgent. But every "yes" to a low-leverage request is an implicit "no" to a high-leverage activity.
>
> | Request | Leverage | Better Response Than "Yes" |
> |---------|---------|--------------------------|
> | "Can you join our design review? We'd love SRE input." | Low — if it's for a non-critical service you don't support | "My TL can attend, or I can review the doc async and comment on reliability concerns" |
> | "Can we set up a weekly sync to discuss the migration?" | Medium — but a weekly meeting might outlive its usefulness | "Let's start with 3 weekly meetings and reassess. I'll block 4 weeks on the calendar and we can extend if still needed." |
> | "Can you take on ownership of Service X's on-call?" | Low-to-negative — if your team is already at toil capacity | "My team is at 48% toil. Taking on another service pushes us past the 50% threshold. Let's discuss what we can drop, or whether the product team can own their on-call with our coaching." |
> | "We need you at the all-day offsite next week" | Depends — is this a decision-making session or a social event? | If decision-making: attend. If social: send a report as your proxy. |
>
> Grove's underlying principle: saying no is a manufacturing decision. When the factory is at capacity, you don't accept more orders — you queue them. Your time works the same way.

### Build in Slack

Grove draws from highway traffic planning:

> *"Highway planners know that a freeway can handle an optimum number of vehicles. Having fewer cars means that the road is not being used at capacity. But at that optimum point, if just a few more cars are allowed to enter the traffic flow, everything comes to a crunching halt."*

> *"There is an optimum degree of loading, with enough slack built in so that one unanticipated phone call will not ruin your schedule for the rest of the day."*

> **[Production Thinking: The Utilization Trap]**
>
> This is one of the most important and least intuitive production principles: **systems running at high utilization have catastrophically long queue times.**
>
> The math (from queueing theory):
> - At 50% utilization: wait time = 1× processing time
> - At 80% utilization: wait time = 4× processing time
> - At 90% utilization: wait time = 9× processing time
> - At 95% utilization: wait time = 19× processing time
>
> **Applied to your calendar:**
> - If your calendar is 50% booked: you handle interruptions easily, have time for deep work, can accommodate urgent requests
> - If 80% booked: interruptions start cascading, meetings get displaced, you feel constantly behind
> - If 90% booked: one unexpected P1 incident destroys your entire week. Every displaced meeting displaces another. Recovery takes days.
>
> **The Senior EM guideline:** Keep your calendar no more than 70-75% scheduled. The remaining 25-30% is not "free time" — it's slack that allows the system to function without gridlock. This slack is where:
> - Unexpected escalations get handled without destroying the schedule
> - Deep thinking happens
> - Casual information-gathering (walking around / Slack browsing) occurs
> - You process what you've learned and decide what to do about it
>
> **The SRE parallel:** This is the same principle as not running servers at 100% CPU. You leave headroom because spikes are inevitable. A calendar at 100% is like a server at 100% — one spike and everything times out.

### Carry a Project Inventory

> *"A manager should carry a raw material* inventory *in terms of projects... things you need to do but don't need to finish right away — discretionary projects, the kind the manager can work on to increase his group's productivity over the long term."*

Grove warns: without such an inventory, *"a manager will most probably use his free time* meddling *in his subordinates' work."*

> **[Practical Toolkit: Your Project Inventory]**
>
> Keep a running list of 5-10 projects that are:
> - Important but not urgent
> - Within your control (don't need other teams' cooperation to start)
> - Produce long-term leverage (improve team capacity, reduce toil, build systems)
>
> **Example inventory for a Senior EM in SRE:**
> 1. Write the SRE team's career ladder framework (high leverage — used for years)
> 2. Create an on-call training curriculum for new hires (high leverage — scales with every hire)
> 3. Analyze last quarter's incidents for systemic patterns (medium leverage — informs roadmap)
> 4. Prototype a Slack bot that summarizes SLO status daily (medium leverage — saves team time)
> 5. Draft an RFC for consolidating monitoring dashboards (medium leverage — reduces cognitive load)
> 6. Review and update team runbooks that haven't been touched in 6 months (medium leverage — on-call quality)
> 7. Write a "Working with SRE" guide for product teams (high leverage — reduces misalignment friction)
>
> **When to pull from inventory:** Whenever a meeting cancels, a block opens up, or you finish something early. Instead of checking Slack or meddling, pull a project and advance it. Even 30 minutes of focused work on a high-leverage project accumulates into significant output over weeks.

### Standardize Approaches

> *"Most production practices follow well-established procedures... But managers tend to be inconsistent and bring a welter of approaches to the same task. We should work to change that."*

Grove's caveat: standardize the approach but keep thinking critically about it. The value of a procedure isn't the document — it's the *thinking* that created it. Standardize to save set-up time, but continue questioning whether the standard is still right.

---

## Span of Control: How Many Subordinates?

### The 6-8 Rule

> *"A manager whose work is largely supervisory should have six to eight subordinates; three or four are too few and ten are too many."*

The rationale: a manager should spend about **half a day per week per subordinate** — enough time for 1-1s, monitoring, coaching, and ad hoc interaction.

- **Too few** (3-4): The manager doesn't have enough work and will meddle
- **Too many** (10+): The manager can't give adequate attention and will either abdicate or burn out
- **Just right** (6-8): Enough to stay busy, few enough to stay effective

For know-how managers who also serve as internal consultants or committee members, Grove notes: *"anyone who spends about a half day per week as a member of a planning, advisory, or coordinating group has the equivalent of a subordinate."*

So a Senior EM who manages 4 direct reports AND participates in 3 cross-org committees has an effective span of 7 — right in the sweet spot.

> **[Senior EM Application: Calculating Your Real Span]**
>
> Most Senior EMs undercount their span because they only count direct reports:
>
> | Responsibility | Equivalent Subordinates |
> |---------------|------------------------|
> | Direct reports (managers/TLs) | 4 |
> | Architecture review board membership | 1 |
> | SRE guild leadership | 1 |
> | Cross-functional sync with Product | 0.5 |
> | Mentoring a Staff engineer | 0.5 |
> | **Total effective span** | **7** |
>
> If your total exceeds 8, something suffers. Grove says either the supervision becomes shallow (abdication) or you burn out. The fix: drop a committee membership, delegate the mentoring to another senior person, or reduce your direct reports by adding a management layer.
>
> If your total is under 5, you're probably meddling (per Grove) or not leveraging your influence broadly enough.

### The Acting-as-Subordinate Trick

Grove describes a clever organizational hack: if a plant manager only has 2 direct reports (engineering lead + manufacturing lead), the span is too narrow and the manager will either idle or meddle. Solution: the manager takes on one of the roles directly — for example, acting as their own engineering manager. Now their effective span is 6 (5 engineers + 1 manufacturing lead), which is healthy.

> **[SRE Lens: When to "Act as" Your Own TL]**
>
> This pattern is common in growing SRE orgs. If you manage two small teams (say 3-4 engineers each), having a TL for each team and managing only 2 TLs leaves you with too narrow a span. Options:
>
> 1. **Act as TL for one team** — manage that team's engineers directly while the other TL manages theirs. Your span: 3-4 engineers + 1 TL = 4-5 (a bit low but workable).
> 2. **Flatten to one team with one TL** — combine into one team, single TL handles day-to-day, you manage TL + individual coaching relationships. Span: 1 TL + 2-3 senior ICs you closely mentor = 3-4 plus committee work.
> 3. **Expand influence scope** — keep the 2 TLs, but take on additional cross-org responsibilities (SRE guild, architecture board, platform team alignment) to fill your capacity. Span: 2 TLs + 3-4 committees = 5-6.
>
> The worst option: keep the 2-TL structure, have nothing else, and start meddling in both teams' work. Grove predicts exactly this outcome.

---

## Interruptions: The Plague of Managerial Work

Grove conducted an experiment: 20 Intel middle managers paired up, one identifying their most output-limiting problem, the other consulting on solutions. The most common problem: **uncontrolled interruptions**.

The interruptions came from predictable sources: subordinates, people outside the manager's immediate org whose work the manager influenced, production operators (for manufacturing managers), and external customers (for marketing managers). In short: *the consumers of the manager's authority and information.*

The most proposed solution — hiding physically — was impractical because the interrupters have *legitimate problems.* The interruptions aren't frivolous; they represent real demand for the manager's input.

Grove offers four production-based solutions:

### Standard Responses

> *"Manufacturers turn out* standard products. *By analogy, if you can pin down what kind of interruptions you're getting, you can prepare standard responses for those that pop up most often."*

Customers and subordinates don't ask totally new questions every day. The same patterns recur. Pre-built responses (templates, FAQ docs, documented policies) let you handle recurring interruptions quickly — or delegate them entirely.

> **[SRE Lens: Standard Responses for SRE Managers]**
>
> | Recurring Interruption | Standard Response |
> |----------------------|------------------|
> | "Can SRE take on-call for our new service?" | Written policy: "New service on-call criteria" doc → share link, schedule review meeting only if they meet threshold |
> | "We're seeing errors — can you look?" | Written triage guide: "Before escalating to SRE, check: 1) Is the service in your team's SLO dashboard? 2) What does the error rate graph show? 3) Have recent deployments correlated?" |
> | "Can you review our architecture for reliability?" | Written template: "Reliability review request form" → submit first, SRE reviews async, meeting only if needed |
> | "How do I set up monitoring for my service?" | Self-service docs: monitoring setup guide + golden dashboard templates |
> | "Our error budget is burning — what should we do?" | Written playbook: "Error budget response procedure" → team follows playbook, escalates to SRE manager only if actions in playbook don't work |
>
> Each standard response eliminates a future interruption — or at least reduces it from a 30-minute conversation to a 2-minute link share. This is leverage applied to interruption management.

### Batch Interruptions into Meetings

> *"If such meetings are held regularly, people can't protest too much if they're asked to batch questions and problems for* scheduled *times, instead of interrupting you whenever they want."*

Subordinates' questions and issues can accumulate and be handled in 1-1s and staff meetings. If 1-1s are weekly, most non-urgent questions can wait a few days. This converts random interruptions (job shop) into scheduled production (factory).

### The Indicator Archive

> *"By maintaining an archive of information, a manager doesn't have to do ad hoc research every time the phone rings."*

If you keep dashboards, metrics, and historical data readily accessible, you can answer many questions immediately instead of launching an investigation. The faster you can answer, the shorter the interruption.

### Office Hours, Not Hiding

> *"Instead of going into hiding, a manager can hang a sign on his door that says, 'I am doing individual work. Please don't interrupt me unless it really can't wait until 2:00.' Then hold an open office hour, and be completely receptive to anybody who wants to see you."*

The key principle:

> *"Understand that interrupters have legitimate problems that need to be handled. That's why they're bringing them to you. But you can channel the time needed to deal with them into organized, scheduled form by providing an* alternative *to interruption — a scheduled meeting or an office hour."*

> **[Core Concept: Regularity Transforms Job Shop into Factory]**
>
> Grove's closing principle for the chapter:
>
> *"To make something regular that was once irregular is a fundamental production principle, and that's how you should try to handle the interruptions that plague you."*
>
> This is the meta-principle that ties everything together. All of Grove's time management advice is a single idea: **convert irregular, reactive work into regular, planned work.** Random interruptions become office hours. Ad hoc questions become 1-1 agenda items. Unpredictable requests become standard responses. Reactive firefighting becomes proactive indicator monitoring.
>
> This doesn't eliminate all interruptions — genuine emergencies will always happen. But it reduces the baseline noise so that when a real emergency hits, you have the capacity to handle it. This is the slack principle and the factory principle combined.

> **[Senior EM Application: The Interruption Audit]**
>
> Track your interruptions for one week:
>
> | Interruption | Source | Could It Wait? | Standard Response Possible? | Action |
> |-------------|--------|---------------|---------------------------|--------|
> | "Quick question about the migration" | TL | Yes — 1-1 is tomorrow | Yes — migration FAQ doc | Write FAQ, redirect to 1-1 |
> | P2 incident — should we page? | On-call engineer | No — time-sensitive | Yes — escalation policy doc | Write clearer escalation criteria |
> | "Can you review this RFC by EOD?" | Peer EM | Partially — need not be same-day | No — requires reading | Batch into Tuesday morning RFC review block |
> | "Director wants numbers for the board deck" | Director's EA | No — executive timeline | Partially — template for recurring requests | Create quarterly metrics template pre-filled |
>
> **After one week:** You'll see patterns. Most interruptions cluster into 3-4 categories. For each category, create a standard response, a documented policy, or a scheduled time to handle it. Your interrupt rate will drop 30-50% — exactly Grove's work simplification prediction from Chapter 2.

---

## Chapter 3 Synthesis

Chapter 3 is the central chapter of the book. It establishes:

1. **Output equation:** Manager's output = output of organization + output of influenced organizations
2. **Leverage equation:** Output = Σ (Leverage × Activity) — optimize for high-leverage activities
3. **Five activities:** Information-gathering, information-giving, decision-making, nudging, role modeling
4. **Leverage patterns:** One-to-many, brief-action-long-impact, unique knowledge
5. **Negative leverage:** Unprepared, depressed, waffling, meddling
6. **Delegation:** With monitoring (not abdication, not meddling)
7. **Time management:** Factory principles — limiting step, batching, calendar as production tool, slack, inventory, standardization
8. **Span of control:** 6-8 subordinates or equivalent
9. **Interruptions:** Standard responses, batching, office hours — make the irregular regular

Every subsequent chapter builds on this foundation. Meetings (Ch4) are a *medium* for leverage. Decisions (Ch5) are a *leverage activity*. Planning (Ch6) is *high-leverage work done in advance*. Organization design (Ch7-10) determines *who influences whom* — the structure of the output equation. Motivation and performance (Ch11-16) address *how to maximize the output of individuals* within the team.

**Next: Chapter 4 — Meetings, where Grove tackles the most complained-about managerial activity and reframes it as the essential medium of managerial leverage.**
