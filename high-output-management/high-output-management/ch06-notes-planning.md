# Chapter 6: Planning — Today's Actions for Tomorrow's Output

> **High Output Management** — Andrew S. Grove
> *The Three-Step Planning Process, Management by Objectives, and Why Today's Gap Is Yesterday's Planning Failure*

Grove demystifies planning by applying the same production principles from Chapters 1-2. Planning, he says, is not a lofty executive activity — it's the same thing you do when you check your gas gauge on the way to work. The chapter introduces a three-step planning process (assess demand, assess current status, close the gap), explains why the *output* of planning is not the plan document but the decisions and actions it generates, and introduces Management by Objectives (MBO) as planning applied to daily work. The chapter contains one of the most quoted lines in the book: *"Today's gap represents a failure of planning sometime in the past."*

## Table of Contents

- [The Three-Step Planning Process](#the-three-step-planning-process)
  - [Step 1: Environmental Demand](#step-1-environmental-demand)
  - [Step 2: Present Status](#step-2-present-status)
  - [Step 3: Close the Gap (Strategy)](#step-3-close-the-gap-strategy)
- [The True Output of Planning](#the-true-output-of-planning)
  - [Today's Gap Is Yesterday's Planning Failure](#todays-gap-is-yesterdays-planning-failure)
  - [Planning Horizons](#planning-horizons)
  - [Who Should Plan?](#who-should-plan)
  - [Saying Yes Means Saying No](#saying-yes-means-saying-no)
- [Management by Objectives (MBO)](#management-by-objectives-mbo)
  - [Objectives and Key Results](#objectives-and-key-results)
  - [The Columbus Case Study](#the-columbus-case-study)
  - [MBO Is a Compass, Not a Contract](#mbo-is-a-compass-not-a-contract)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Production Thinking] [Practical Toolkit] [Anti-Pattern] [Modern Lens] [Scenario]

---

## The Three-Step Planning Process

Grove's planning process mirrors factory production control:

### Step 1: Environmental Demand

Ask: **What will the environment demand from you?** Treat your group as a stand-alone company. Your "environment" is your customers (internal or external), your vendors (teams you depend on), and your competitors (teams doing similar work, or external alternatives).

Examine this in two time frames: *now* and *one year from now*. The critical output is the **difference analysis** — the gap between what's demanded now and what will be demanded in the future. That gap is what your plan must address.

Key discipline: don't adjust demand forecasts based on your perceived capacity. If your real demand is 100 units but you think you can only produce 10, forecasting 10 means you'll *never* tool up for the real demand. *"Should you at this stage consider what practical steps you can actually take to handle matters? No, that will just confuse the issue."*

### Step 2: Present Status

Ask: **What are you producing now, and what will you produce from your current pipeline?** List current capabilities and in-progress projects in the *same units* as demand (if demand is measured in shipped features, measure your pipeline in features, not story points or PRs).

Factor in loss: just as manufacturing assumes ~80% of started material gets finished, assume some of your projects will be scrapped or stalled. *"It is prudent to factor in some percentage of loss for managerial projects as well."*

### Step 3: Close the Gap (Strategy)

Ask two questions separately:
1. What do you *need* to do to close the gap?
2. What *can* you do to close the gap?

The set of actions you decide upon is your **strategy**. The tactical execution of that strategy happens at the next level down.

> **[Core Concept: Strategy vs. Tactics — A Nesting Hierarchy]**
>
> Grove's definition is simple and practical: *"The most abstract and general summary of those actions meaningful to you is your strategy. What you'll do to implement the strategy is your tactics."* And critically: *"A strategy at one managerial level is the tactical concern of the next higher level."*
>
> Example for SRE:
> - **VP of Engineering's strategy:** "Achieve 99.99% platform reliability by EOY"
> - **Senior EM's strategy (VP's tactic):** "Migrate critical services to multi-region architecture"
> - **TL's strategy (Senior EM's tactic):** "Implement database failover for the payments service by Q3"
> - **Engineer's strategy (TL's tactic):** "Configure active-passive replication with automated failover testing"
>
> Each level's strategy fulfills the level above's tactical need. This nesting is how organizational alignment works — and why planning must happen at every level, not just at the top.

> **[Practical Toolkit: The SRE Quarterly Planning Process Using Grove's Three Steps]**
>
> **Step 1 — Environmental Demand:**
> - What reliability level do our customers (internal product teams, external users) need next quarter?
> - What new services are launching that need SRE support?
> - What compliance requirements are coming?
> - What capacity growth is projected?
> - What are peer SRE orgs doing that we should match or exceed?
>
> **Step 2 — Present Status:**
> - Current SLO compliance across all services
> - Current project pipeline and expected completion dates (factor in 20% loss)
> - Current team capacity (headcount minus PTO, on-call burden, toil %)
> - Current tooling capabilities and gaps
>
> **Step 3 — Close the Gap:**
> - **Need:** 3 new services onboarded, 2 SLO violations resolved, observability gaps filled, 1 migration completed
> - **Can:** With current team and capacity, realistically complete 2 of 4
> - **Strategy:** Prioritize the 2 highest-impact items, defer or descope the others, present gap analysis to Director as basis for headcount or scope negotiation

---

## The True Output of Planning

### Today's Gap Is Yesterday's Planning Failure

This is the chapter's most important passage:

> *"I have seen far too many people who upon recognizing today's gap try very hard to determine what decision has to be made to close it. But today's gap represents a failure of planning sometime in the past."*

> *"Forcing ourselves to concentrate on the decisions needed to fix today's problem is like scurrying after our car has already run out of gas. Clearly we should have filled up earlier."*

The true question planning must answer:

> *"What do I have to do* today *to solve — or better, avoid —* tomorrow's *problem?"*

And the true output of planning is not the plan document:

> *"The output of Intel's annual plan is the actions taken and changes prompted as a result of the thinking process that took place throughout the organization. I, for one, hardly ever look at the bound volume finally called the Annual Plan."*

> **[SRE Lens: Reliability Planning and "Today's Gap"]**
>
> Grove's insight applies devastatingly to reliability:
>
> | Today's Gap (the incident/problem) | Yesterday's Planning Failure |
> |------------------------------------|-----------------------------|
> | Single-region outage takes service down for 4 hours | 18 months ago, the decision was made to defer multi-region architecture "until next year" |
> | On-call engineer can't diagnose issue — no runbook exists | 6 months ago, the team shipped the service without completing the production readiness review |
> | Error budget burned in Week 1 of the quarter | Last quarter's retro identified the instability pattern but no one was assigned to fix it |
> | Key SRE leaves and no one can cover their services | 1 year ago, cross-training was deprioritized because "everyone is too busy with projects" |
>
> **The Senior EM's planning obligation:** Every quarter, look at your team's current gaps (not just projects, but resilience gaps, knowledge gaps, capacity gaps) and ask: "Which of these will become crises in 3-6 months if I do nothing?" Those are the items that go into your plan *now* — not when the crisis hits.
>
> **The "fill up earlier" principle for SRE:**
> - Invest in multi-region *before* the single-region outage
> - Write runbooks *during* service development, not *after* the first incident
> - Cross-train engineers *before* the bus factor becomes critical
> - Reduce toil *before* it crosses the 50% threshold
> - Hire *before* the team is overwhelmed, using backward planning from expected need

### Planning Horizons

Grove reveals Intel's approach: they plan five years ahead, but only *implement* the first year. The remaining four years are replanned annually.

> *"We will have another chance to replan the second of the five years in the next year's long-range planning meeting, when that year will become the first year of the five."*

This is the stagger chart principle from Chapter 2 applied to planning itself. You don't need a perfect 5-year plan. You need a 1-year plan informed by 5-year thinking.

He also cautions against planning too *frequently*: *"We should be careful not to plan too frequently, allowing ourselves time to judge the impact of the decisions we made."* You need feedback before replanning.

### Who Should Plan?

> *"The idea that planners can be people apart from those implementing the plan simply does not work."*

Planning cannot be delegated to a "strategic planning" department. The operating managers who will execute the plan must create it. This ensures the plan is grounded in reality and that the planners are committed to the outcome.

### Saying Yes Means Saying No

> *"By saying 'yes' — to projects, a course of action, or whatever — you are implicitly saying 'no' to something else. Each time you make a commitment, you forfeit your chance to commit to something else."*

> *"People who plan have to have the guts, honesty, and discipline to drop projects as well as to initiate them, to shake their heads 'no' as well as to smile 'yes.'"*

> **[Anti-Pattern: The Plan That Says Yes to Everything]**
>
> The most common planning failure in engineering: a roadmap that commits to more than the team can deliver, because the planners lacked the *"guts, honesty, and discipline"* to say no.
>
> **How this happens:**
> 1. Product team requests 10 features
> 2. Leadership requests a platform migration
> 3. SRE team identifies 5 reliability improvements needed
> 4. Tech debt is accumulating and needs 20% allocation
> 5. The plan includes all of the above, with a note that "we'll adjust as we go"
>
> **What happens:** Items 3 and 4 get deferred every sprint because items 1 and 2 have external stakeholders applying pressure. By quarter's end, no reliability improvements were made and tech debt is worse. Today's gap is created.
>
> **Grove's fix:** The plan must explicitly state what you're *not* doing. "We are doing items 1, 3, and part of 2. We are NOT doing items 4 and 5 this quarter. Here's why, and here's the risk." This forces the conversation about trade-offs upfront rather than discovering them in Week 10 when nothing got done.

---

## Management by Objectives (MBO)

Grove introduces MBO as planning applied to short-range, daily work. The system answers two questions:

1. **Where do I want to go?** → the **objective**
2. **How will I pace myself to see if I'm getting there?** → the **key results**

### Objectives and Key Results

Grove illustrates with a driving analogy: the objective is catching a flight in an hour. The key results are reaching towns A, B, and C at 10, 20, and 30 minutes respectively. If you haven't reached town A by minute 20, you know you're off track — time to ask for directions.

Properties of good key results:
- **Specific wording** — no ambiguity about what "done" means
- **Specific dates** — deadlines that create unambiguous pass/fail
- **Short-range** — quarterly or monthly, not annual. *"For the feedback to be effective, it must be received very soon after the activity it is measuring occurs."*
- **Few in number** — *"If we try to focus on everything, we focus on nothing."*

### The Columbus Case Study

Grove tells the story of Columbus as an MBO case study:

- **Queen Isabella's objective:** Increase Spain's wealth (to fund the war against the Moors)
- **Columbus' objective (nested under Isabella's):** Find a new trade route to the Orient
- **Columbus' key results:** Obtain ships, train crews, conduct shakedown cruise, set sail — each with a deadline

The nesting hierarchy: if Columbus meets his objective, Isabella meets hers.

But then the twist: Columbus hit every key result on schedule — ships obtained, crew trained, voyage completed. *"But he most certainly did not find a new trade route to China, and therefore failed to meet his objective."* He did, however, discover the New World, which generated *"incalculable wealth for Spain."*

### MBO Is a Compass, Not a Contract

> *"It is entirely possible for a subordinate to perform well and be rated well even though he missed his specified objective."*

> *"The MBO system is meant to pace a person — to put a stopwatch in his own hand so he can gauge his own performance. It is not a legal document upon which to base a performance review, but should be just one input used to determine how well an individual is doing."*

> **[Modern Lens: From MBO to OKRs]**
>
> Grove's MBO framework directly inspired John Doerr's OKR (Objectives and Key Results) system, which Doerr introduced to Google in 1999 (having learned it from Grove at Intel). The connection is explicit — Doerr's book *Measure What Matters* credits Grove directly.
>
> | Grove's MBO | Modern OKRs | What Changed |
> |------------|-------------|-------------|
> | Objectives set by negotiation between manager and subordinate | Objectives set at multiple levels — company, team, individual — with alignment between them | Broader organizational adoption; OKRs cascade through the org |
> | Key results = milestones with deadlines | Key results = measurable outcomes (often quantitative) | Shift from "did you do it?" to "did it work?" |
> | Short-range focus (quarterly) | Typically quarterly, sometimes with annual "big-picture" OKRs | Essentially unchanged |
> | Few in number | Best practice: 3-5 objectives, 3-5 KRs each | Grove's "focus on few" principle formalized |
> | Compass, not contract — judgment required | "Stretch goals" at 60-70% achievement = success; 100% means goals were too easy | Explicit expectation management about target-setting |
>
> **What Grove would say about modern OKR dysfunction:**
> - **Too many OKRs** → violates "focus on few" → everything is a priority → nothing gets done. Grove: *"If we try to focus on everything, we focus on nothing."*
> - **OKRs as performance review inputs** → Grove explicitly warns against this. OKRs should be a self-pacing tool, not a contract.
> - **KRs that are activities, not outcomes** → "Complete the migration" is an activity. "Reduce P99 latency from 2s to 500ms" is an outcome. Grove would insist on the latter — output, not activity.
> - **Missing the "environmental demand" step** → teams set OKRs based on what they *want* to do, not what the environment *demands*. Grove's Step 1 comes first — understand demand before planning supply.

> **[SRE Lens: OKRs for Reliability]**
>
> Applying Grove's MBO/OKR framework to SRE:
>
> **Objective:** Improve checkout service reliability to support Black Friday traffic
>
> **Key Results:**
> 1. Achieve 99.95% availability SLO (currently 99.8%) by Nov 1
> 2. Reduce P99 latency from 1.2s to 400ms by Oct 15
> 3. Complete multi-region failover capability with successful DR test by Oct 1
> 4. Reduce on-call page volume by 40% (from 25/week to 15/week) by Nov 1
>
> **Notice:** Each KR is a measurable outcome with a specific date. Not "improve reliability" (vague) or "implement caching" (activity). You know unambiguously whether you hit each one.
>
> **The Columbus lesson for SRE:** You might hit all KRs but miss the objective — Black Friday overloads the CDN in a way nobody anticipated, and the checkout service goes down despite meeting all its SLOs. You might also miss a KR but exceed the objective — the latency is 500ms instead of 400ms, but the DR failover works perfectly and saves the day during an actual regional outage. Grove says: use judgment, not rigid scoring.

---

**Chapter 6 establishes:** Planning is three steps (assess demand, assess status, close the gap). The output of planning is actions taken, not the document produced. Today's crises are yesterday's planning failures. MBO/OKRs translate plans into daily work. Focus on few objectives. Saying yes means saying no.

**Next: Chapter 7 — The Breakfast Factory Goes National, where Grove introduces the organizational challenge of scaling from one factory to many.**
