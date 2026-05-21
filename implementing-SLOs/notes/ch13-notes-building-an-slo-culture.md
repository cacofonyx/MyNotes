# Chapter 13: Building an SLO Culture

> **Implementing Service Level Objectives** — Harold Treen
> *Organizational Change, Two Failure Modes, the Six-Step Path, and Making SLOs Stick*

This chapter shifts from the technical to the human. Harold Treen addresses the hardest part of SLO adoption: making it a cultural practice that persists beyond the initial enthusiast. Most SLO initiatives die not because the math is wrong or the tooling is inadequate, but because the organization treats SLOs as a project with a completion date rather than a process with continuous iteration. Treen provides a practical framework for navigating the organizational change — from getting initial buy-in through making SLOs the default way reliability decisions are made.

This is the chapter for anyone who has successfully implemented SLOs for one team and is wondering "how do I make this stick across the organization?"

## Table of Contents

- [Two Failure Modes](#two-failure-modes)
- [The Six-Step Path](#the-six-step-path)
  - [Step 1: Get Buy-In](#step-1-get-buy-in)
  - [Step 2: Prioritize Work](#step-2-prioritize-work)
  - [Step 3: Implement](#step-3-implement)
  - [Step 4: Use](#step-4-use)
  - [Step 5: Iterate](#step-5-iterate)
  - [Step 6: Advocate](#step-6-advocate)
- [Using SLOs Day-to-Day](#using-slos-day-to-day)
- [Strategies for Cultural Persistence](#strategies-for-cultural-persistence)
- [SLOs Are a Process, Not a Project](#slos-are-a-process-not-a-project)

**Block types:** [Core Concept] [Implementation Guide] [Worked Example] [Common Pitfall] [Senior EM Application] [2025 Update] [Production Thinking] [Organizational Reality]

---

## Two Failure Modes

> **[Core Concept: The Reliability Spectrum Has Two Failure Modes]**
>
> Organizations fail at reliability in two opposite ways:
>
> | Failure Mode | Symptoms | Root Cause | Outcome |
> |---|---|---|---|
> | **No reliability focus** | Constant firefighting, no error budgets, deploy-and-pray, every outage is a surprise | Reliability is nobody's job; velocity is the only metric | Chaos — users suffer, team burns out, trust erodes |
> | **Over-reliability focus** | Feature velocity near zero, change aversion, "if it's not broken don't touch it," multi-week approval processes | Reliability is everyone's *only* job; fear of failure dominates | Stagnation — competitors outpace, users leave because features never improve |
>
> **SLOs are the balance point.** They give organizations a quantitative framework for navigating between these extremes:
> - Error budget healthy → lean toward velocity (take risks, ship features)
> - Error budget depleted → lean toward reliability (slow down, fix things)
>
> The oscillation between these modes *is the system working correctly*. An organization that never depletes its error budget is over-investing in reliability. One that always depletes it is under-investing.

> **[Senior EM Application: Diagnosing Your Organization's Failure Mode]**
>
> Before starting an SLO initiative, identify which failure mode your organization is closer to. The approach differs:
>
> | If you're in... | SLO pitch emphasizes... | First win looks like... |
> |---|---|---|
> | Chaos (no reliability focus) | "SLOs will reduce firefighting by making reliability investment visible and prioritized" | First error budget exhaustion triggers a reliability sprint — team gets breathing room |
> | Stagnation (over-reliability focus) | "SLOs will show we're over-investing in reliability — error budget surplus means we can move faster safely" | Showing surplus budget unlocks feature velocity — team ships something they've been afraid to |
>
> Most organizations are in the chaos mode. But some — particularly those scarred by past outages or in regulated industries — are in stagnation mode. The SLO pitch must match the symptom.

---

## The Six-Step Path

### Step 1: Get Buy-In

> **[Implementation Guide: Starting the Conversation]**
>
> Treen's buy-in approach is deliberately lightweight at this stage:
>
> - **Don't** try to get the entire organization aligned before starting
> - **Do** get your immediate team and one level of management to agree to try
> - **Don't** promise organizational transformation
> - **Do** promise a small experiment with measurable outcomes
>
> The goal is not universal agreement — it's permission to experiment with one service.
>
> **The pitch:** "I'd like to try defining SLOs for [one service]. It will take [2 weeks] to set up. After [1 month], we'll evaluate whether the data is useful for making decisions. If not, we stop."
>
> Low commitment. Clear exit criteria. No irreversible organizational change.

### Step 2: Prioritize Work

> **[Production Thinking: Choosing the Right First Service]**
>
> Not all services are good candidates for a first SLO:
>
> | Good First Candidate | Bad First Candidate |
> |---|---|
> | Has clear users with clear expectations | Has ambiguous users or undefined purpose |
> | Already has some metrics/monitoring | Has no instrumentation at all |
> | Team is receptive to the experiment | Team is hostile or overwhelmed |
> | Moderate complexity (not trivial, not enormous) | Either too simple (nothing to measure) or too complex (months to instrument) |
> | Experiencing reliability issues that SLOs could quantify | Running perfectly fine (no pain to motivate change) |
>
> **The counterintuitive advice:** Don't start with your most critical service. Start with one that's important enough to matter but not so critical that a failed experiment has organizational consequences.

### Step 3: Implement

> **[Implementation Guide: Minimum Viable SLO]**
>
> The first implementation should be deliberately minimal:
>
> 1. Define 1-2 SLIs (availability and one latency percentile)
> 2. Set an initial SLO target (based on historical performance minus a small margin)
> 3. Build a dashboard showing current performance vs. target
> 4. Calculate error budget remaining
> 5. Set one alert (fast-burn only — keep it simple)
>
> **Do not:**
> - Build custom tooling (use what exists)
> - Define error budget policies yet (too early)
> - Roll out to multiple services simultaneously
> - Spend more than 2 weeks on initial setup

### Step 4: Use

> **[Core Concept: SLOs Must Inform Decisions or They're Just Dashboards]**
>
> The critical transition: from "we have SLOs" to "we use SLOs to make decisions." Treen identifies specific decision points where SLOs should be consulted:
>
> | Decision | Without SLOs | With SLOs |
> |---|---|---|
> | "Should we deploy on Friday?" | Opinion-based ("I feel nervous" vs. "ship it!") | Data-based ("error budget is healthy — deploy, but watch burn rate") |
> | "Should we prioritize this reliability fix?" | Whoever argues loudest | "We've burned 60% of budget in 2 weeks — reliability work is urgent" |
> | "Can we take on this risky migration?" | Risk assessment by gut feeling | "We have 35 minutes of budget remaining — not now" |
> | "Are we investing enough in reliability?" | Political negotiation | "Budget has been exhausted 4 of the last 6 months — we're under-investing" |
>
> If SLOs exist but never influence a decision, they will be abandoned. The culture shift happens at the moment someone says "let's check the error budget" instead of "what do you think?"

### Step 5: Iterate

> **[Common Pitfall: Setting It and Forgetting It]**
>
> The most common SLO death is not rejection — it's neglect. The SLOs are defined, dashboards are built, and then... nothing changes. Teams stop looking at them. Targets become stale.
>
> **Iteration triggers:**
> - Monthly: review SLO performance, check if targets still feel right
> - After incidents: did the SLO alert fire? If not, why not? If it did, was the response appropriate?
> - After significant architecture changes: do the SLIs still measure what matters?
> - Quarterly: formal review of targets, add/remove SLIs, update error budget policies
>
> **The process:** Each review asks three questions:
> 1. Are we always meeting this SLO easily? → Target may be too loose
> 2. Are we always missing this SLO? → Target may be too tight, or there's a real reliability problem
> 3. Are users complaining about things our SLOs don't capture? → Missing an SLI

### Step 6: Advocate

> **[Organizational Reality: Success Creates Advocates]**
>
> Once one team is successfully using SLOs to make decisions, the path to organizational adoption is through demonstration, not mandate:
>
> - Share the story at engineering all-hands
> - Invite adjacent teams to observe your SLO review meetings
> - When another team has a reliability debate, offer "we had the same problem — here's how SLO data resolved it"
> - Publish a brief case study internally
>
> **What doesn't work:** Top-down mandates to "adopt SLOs by Q3." Without the cultural understanding of *why* and *how*, mandated adoption produces compliance theater — SLOs are defined to check a box, but never used for decisions.

---

## Using SLOs Day-to-Day

> **[Implementation Guide: Three Operational Modes]**
>
> Treen describes three distinct operational modes based on error budget status:
>
> | Mode | Budget Status | Team Behavior | Alerting Posture |
> |---|---|---|---|
> | **Green** | > 50% remaining | Ship features aggressively, take calculated risks, experiment | Conservative — only page on fast burn (complete outages) |
> | **Yellow** | 20-50% remaining | Continue shipping but increase caution, review deploy risk before each push | Moderate — page on fast burn, ticket on slow burn |
> | **Red** | < 20% remaining | Reliability sprint — only reliability improvements ship until budget recovers | Aggressive — page on any sustained burn |
>
> **The conservative alerting start:** Treen specifically recommends starting with *only* fast-burn alerts (major outages). This prevents early alert fatigue and builds trust. Add slow-burn alerts after the team is comfortable with the fast-burn alerts and ready for more nuanced signals.

> **[Worked Example: Error Budget Driving a Sprint]**
>
> **Scenario:** Mid-month, the team notices error budget is at 30% (yellow). Analysis shows a slow burn caused by a flaky dependency timeout.
>
> **Without SLOs:** The flaky timeout has been a known issue for months. It never caused a paging incident so it never got prioritized. Product keeps pushing features.
>
> **With SLOs:** The error budget math makes the cost visible:
> - Current burn rate: 3x sustainable
> - Projected budget at month end: -15% (overspent)
> - If the timeout issue is fixed, burn rate drops to 0.5x (healthy)
>
> The data transforms the conversation from "we should fix this someday" to "if we don't fix this in the next 5 days, we'll exhaust our budget and trigger a reliability freeze."
>
> Result: The timeout fix gets prioritized above feature work. It ships in 3 days. Budget stabilizes. No freeze needed. Team returns to feature velocity.

> **[Production Thinking: Budget Surplus as Permission to Experiment]**
>
> The flip side of budget exhaustion is budget surplus. Treen emphasizes that healthy error budget is *permission*, not just absence of crisis:
>
> - "We have 80% of budget remaining with one week left in the window. We can safely attempt that risky database migration we've been deferring."
> - "Error budget has been at 90%+ for three consecutive months. Our SLO target may be too loose — let's tighten it."
>
> A team that never uses its error budget is a team that's either over-provisioned for reliability or afraid to take risks. Both represent wasted potential.

---

## Strategies for Cultural Persistence

> **[Senior EM Application: Making SLOs Survive Personnel Changes]**
>
> The greatest threat to SLO culture is not organizational resistance — it's the departure of the champion. When the person who drove SLO adoption leaves, the practice often atrophies.
>
> **Persistence strategies:**
>
> | Strategy | How | Why It Works |
> |---|---|---|
> | **Embed in process** | SLO review is a standing agenda item in sprint planning | Removes dependence on individual initiative |
> | **Embed in tooling** | SLO dashboards are the team's homepage; deploy pipelines show budget status | Makes SLOs visible without anyone having to ask |
> | **Embed in hiring** | SLO vocabulary appears in interview rubrics and onboarding | New team members arrive expecting SLO culture |
> | **Embed in promotion** | Using SLO data for reliability decisions is part of senior engineer expectations | Career incentive to maintain the practice |
> | **Multiple advocates** | Train 2-3 team members as SLO champions, not just one | Redundancy — single point of failure applies to people too |
>
> The underlying principle: culture survives personnel changes only when it's encoded in process, tooling, and incentives — not in a single person's enthusiasm.

> **[2025 Update: Platform Engineering and SLO Culture]**
>
> By 2025, the platform engineering movement has created a natural home for SLO practices:
>
> - **Internal Developer Platforms (IDPs)** often include SLO definition as part of service onboarding
> - **Golden paths** (standardized service templates) can include pre-configured SLO dashboards and alerts
> - **Service catalogs** (Backstage, Cortex) display SLO status alongside service metadata
> - **GitOps workflows** enable SLO-as-code — SLO definitions live in the same repo as the service
>
> The cultural challenge remains, but the infrastructure to support SLO culture is now much richer. The question has shifted from "how do we build the tools?" to "how do we ensure teams actually use what's built into the platform?"

---

## SLOs Are a Process, Not a Project

> **[Core Concept: The Process Mindset]**
>
> Treen's most important message: SLOs are never "done."
>
> | Project Mindset (Wrong) | Process Mindset (Right) |
> |---|---|
> | "We'll implement SLOs in Q2" | "We'll start measuring SLOs in Q2 and iterate indefinitely" |
> | "Success = SLOs are defined for all services" | "Success = SLOs are used for decisions every sprint" |
> | "Completion criteria: dashboards built" | "Health criteria: targets revised at least quarterly" |
> | "Budget: fixed allocation, then done" | "Budget: ongoing operational investment (small but perpetual)" |
>
> An SLO that hasn't been revised in a year is almost certainly wrong — either the service has changed, or the users' expectations have shifted, or the measurement has drifted. The *process* of periodic review, adjustment, and decision-making is the value — not the *artifact* of a defined SLO.

> **[Common Pitfall: Culture Change vs. Technology Implementation]**
>
> Treen warns against the most seductive trap: believing that buying an SLO tool = having an SLO culture.
>
> **What tools give you:** Measurement, dashboards, alerting, calculation.
> **What tools cannot give you:** The habit of checking budget before deploying. The discipline of enforcing a freeze. The reflex of asking "what does the SLO say?" in a planning meeting.
>
> Tools are necessary but insufficient. The cultural practice — the repeated behavior of consulting SLO data when making reliability decisions — requires deliberate cultivation through process, reinforcement, and leadership commitment.

---

**Chapter 13 establishes:** SLO adoption is a cultural change process, not a technology implementation project. Organizations fail in two opposite directions (chaos or stagnation) and SLOs provide the balance point. The six-step path (buy-in, prioritize, implement, use, iterate, advocate) is deliberately incremental — start small, prove value, expand through demonstration. Day-to-day SLO usage means operating in green/yellow/red modes based on error budget status, with budget health driving decisions about velocity vs. reliability investment. Cultural persistence requires embedding SLOs in process, tooling, hiring, and promotion — not depending on individual champions. The process mindset (continuous iteration) trumps the project mindset (one-time implementation).

**Next: Chapter 14 — SLO Evolution (Alex Hidalgo), covering when and how to change SLOs as services, users, and business context change over time.**
