# Chapter 14: SLO Evolution

> **Implementing Service Level Objectives** — Alex Hidalgo
> *When to Change SLOs, Triggers for Revision, Aspirational Targets, and Identifying Incorrect SLOs*

SLOs that never change become irrelevant. Services evolve — traffic patterns shift, dependencies are introduced or retired, user expectations drift with competition, and the team's understanding of what reliability means deepens over time. This chapter provides a systematic framework for knowing *when* an SLO should change and *how* to change it without losing organizational confidence. Hidalgo covers the full lifecycle: from first-pass corrections weeks after initial deployment through mature revisions driven by market forces, and introduces the concept of aspirational SLOs that drive improvement rather than merely describe the status quo.

This chapter answers the question every team eventually asks: "We set these SLOs six months ago — should we still trust them?"

## Table of Contents

- [Why SLOs Must Evolve](#why-slos-must-evolve)
- [Triggers for SLO Revision](#triggers-for-slo-revision)
  - [First-Pass Correction](#first-pass-correction)
  - [Usage Changes](#usage-changes)
  - [Functional Changes](#functional-changes)
  - [Dependency Changes](#dependency-changes)
  - [Failures and Incidents](#failures-and-incidents)
  - [User Expectation Changes](#user-expectation-changes)
  - [Tooling and Measurement Changes](#tooling-and-measurement-changes)
  - [Intuition](#intuition)
- [Aspirational SLOs](#aspirational-slos)
- [Identifying Incorrect SLOs](#identifying-incorrect-slos)
- [Revisit Schedules](#revisit-schedules)

**Block types:** [Core Concept] [Implementation Guide] [Worked Example] [Common Pitfall] [Senior EM Application] [2025 Update] [Production Thinking] [Organizational Reality]

---

## Why SLOs Must Evolve

> **[Core Concept: SLOs Are Hypotheses, Not Constants]**
>
> An SLO is a hypothesis: "We believe that if we maintain X% reliability for this SLI, our users will be satisfied." Like all hypotheses, it can be:
>
> - **Wrong from the start** (first-pass correction needed)
> - **Right initially but outdated** (service or users have changed)
> - **Right for one user segment but wrong for another** (segments diverging)
> - **Right for the SLI but the SLI itself is wrong** (measuring the wrong thing)
>
> A static SLO assumes a static world. Since nothing in production is static — traffic grows, code changes, dependencies shift, user expectations rise — SLOs that don't evolve become increasingly disconnected from reality.
>
> **The organizational risk of stale SLOs:**
> - Too-strict SLOs trigger unnecessary reliability freezes → team loses trust in the system
> - Too-lenient SLOs never trigger → team ignores them → they become decorative
> - Either outcome leads to abandonment: "SLOs don't work for us"

---

## Triggers for SLO Revision

### First-Pass Correction

> **[Implementation Guide: The First Revision Is Expected]**
>
> Your initial SLO target is almost always wrong. This is fine. The first revision typically happens 2-4 weeks after deployment:
>
> | Signal | Problem | Correction |
> |---|---|---|
> | Error budget exhausted in first 3 days | Target too strict relative to current reliability | Loosen target to match observed performance (then improve the system to earn a tighter target) |
> | Error budget barely touched after 30 days | Target too lenient — not capturing real user pain | Tighten target incrementally until budget consumption feels meaningful |
> | SLI shows constant 100% | Measurement is wrong (not capturing failures you know exist) | Fix the SLI measurement before adjusting the target |
> | Users complaining but SLO is green | SLI doesn't measure what users actually experience | Add or change the SLI, then set a new target |
>
> **The key principle:** The first SLO target is a starting point for iteration, not a commitment carved in stone. Teams should be told this explicitly: "We will revisit this in one month and adjust based on what we learn."

### Usage Changes

> **[Production Thinking: Traffic Patterns Invalidate Assumptions]**
>
> Several usage changes can invalidate an SLO:
>
> **Increased traffic:** Higher request volume means the same error budget (in absolute terms) allows fewer bad events per user. At 1M requests/day with a 99.9% SLO, you allow 1,000 errors. At 10M requests/day with the same SLO, you allow 10,000 errors. But user perception of reliability may not scale linearly — 10,000 errors might mean every user sees at least one error per day.
>
> **Decreased traffic:** Lower volume makes SLIs statistically unreliable. A 99.9% SLO with 100 requests/day means 0.1 allowed errors per day — less than one event. The math stops being meaningful.
>
> **Changed patterns:** A service designed for business-hours traffic that starts getting 24/7 usage needs its SLO window reconsidered. A batch system that switches to real-time processing needs latency SLIs added.
>
> **Low-frequency metrics:** Some SLIs only generate enough data points to be statistically meaningful over long windows. Monthly billing runs, quarterly reports, annual processes — these may need longer SLO windows or different measurement approaches.

### Functional Changes

> **[Core Concept: New Features May Need New SLOs]**
>
> When a service gains significant new functionality:
>
> - New user journeys emerge that aren't captured by existing SLIs
> - Existing SLIs may no longer represent the primary user experience
> - The complexity increase may change what's achievable
>
> **Example:** A service that adds a real-time search feature needs a latency SLI for search — its existing availability-only SLO doesn't capture whether search is fast enough to be useful.
>
> The rule: any feature launch that changes *what users primarily do* with the service should trigger an SLO review.

### Dependency Changes

> **[Implementation Guide: Dependency Changes Require SLO Review]**
>
> | Dependency Change | SLO Impact | Action |
> |---|---|---|
> | New critical-path dependency added | Composed availability decreases | Recalculate ceiling; may need to loosen target or add redundancy |
> | Dependency upgraded (better reliability) | Composed availability increases | Opportunity to tighten target |
> | Dependency retired | One fewer failure source | Recalculate; may be able to tighten |
> | Platform migration (e.g., new cloud provider) | Unknown reliability characteristics | Set conservative targets; monitor and adjust over 1-2 months |
> | Vendor SLA change | Ceiling shifts | Verify your SLO is still below the new composed ceiling |
>
> **The dependency trap:** Teams often add dependencies without updating SLOs. Each new dependency erodes the reliability ceiling silently. Regular dependency audits (Chapter 10) should trigger SLO reviews.

### Failures and Incidents

> **[Common Pitfall: Reactive SLO Tightening After Incidents]**
>
> After a major incident, there's organizational pressure to tighten SLOs: "This must never happen again! Set tighter targets!"
>
> **Why this is usually wrong:**
> - The incident already exhausted the error budget — the SLO *detected* the problem correctly
> - Tightening the SLO doesn't prevent incidents — it just triggers alerts earlier
> - If the team can't defend the current target, a tighter target won't be defensible either
>
> **When post-incident SLO revision IS appropriate:**
> - You discover the SLI wasn't measuring what users actually experienced (fix the measurement)
> - The incident revealed that your users are more sensitive than you assumed (tighten because reality changed your understanding)
> - The incident prompted architectural improvements that genuinely raised the reliability ceiling (tighten because capability improved)
>
> The test: "Are we tightening because we're actually more capable, or because we're scared?"

### User Expectation Changes

> **[Senior EM Application: Market Forces Drive SLO Evolution]**
>
> User expectations aren't static. They shift based on:
>
> | Driver | Direction | Example |
> |---|---|---|
> | **Running too well** | Users expect current performance as baseline | You've been at 99.99% for a year; now 99.9% "feels broken" to users even though it's within your SLO |
> | **Market competition** | Competitors raise the bar | A competitor launches with sub-second response; your 3-second SLO now feels outdated |
> | **Industry standards shift** | New norms emerge | Mobile users in 2025 expect sub-100ms interactions; standards from 2020 feel slow |
> | **User sophistication** | Users become more demanding over time | Initial users forgave downtime; now paying enterprise customers expect better |
>
> **The "running too well" trap:** If you consistently over-deliver (actual performance far exceeds SLO), users calibrate to the observed performance, not your target. When you eventually regress to your SLO target (which is still technically meeting the SLO), users perceive it as degradation. The fix: periodically tighten SLOs to track actual performance within a reasonable margin.

### Tooling and Measurement Changes

> **[Production Thinking: New Instrumentation Reveals Hidden Failures]**
>
> When you improve your measurement infrastructure, you often discover that your service was less reliable than you thought:
>
> - Adding client-side measurement reveals latency the server never saw
> - Adding synthetic monitoring catches availability gaps between real-user requests
> - Adding distributed tracing reveals failures hidden by retries
>
> **The implication:** Better measurement often means your SLI values *get worse* even though the actual service hasn't changed. You're just finally seeing what was always there.
>
> **The response:** Don't loosen the SLO to accommodate the newly-visible failures. Instead, acknowledge that the previous target was based on incomplete data, investigate the newly-revealed failures, and set a realistic target for the more-accurate SLI.

### Intuition

> **[Worked Example: Proactive SLO Adjustment for Known Events]**
>
> **Scenario:** Black Friday is approaching. Historical data shows traffic will 5x and error rate spikes during the surge.
>
> **Options:**
> 1. Keep the same SLO → expect to exhaust budget during the event → trigger a reliability freeze at the worst possible time
> 2. Temporarily loosen the SLO → "adjusting for known conditions" → undermines SLO credibility
> 3. Prepare: scale infrastructure, test at load, add capacity → keep the same SLO → defend it
>
> **Hidalgo's answer:** Option 3 when possible. But if you know you can't defend the target, be transparent about it. A temporary "event SLO" with documented rationale is better than either exhausting budget or silently loosening the target.
>
> The key insight: sometimes your intuition says "something is going to change." Act on it. Don't wait for the data to prove you right while your budget burns.

---

## Aspirational SLOs

> **[Core Concept: SLOs That Drive Improvement]**
>
> An aspirational SLO is a target you cannot currently meet — set deliberately to motivate architectural or operational improvement.
>
> | Type | Description | Use Case |
> |---|---|---|
> | **Achievable SLO** | Reflects current system capability | Normal operation, alerting, error budgets |
> | **Aspirational SLO** | Reflects where you want to be in 6-12 months | Roadmap planning, investment justification, architecture decisions |
>
> **How aspirational SLOs work:**
> - You do NOT alert on aspirational SLOs (they'd fire constantly)
> - You DO track the gap between current performance and the aspirational target
> - The gap justifies specific reliability investments ("To reach our aspirational 99.95%, we need to eliminate this single point of failure")
> - When current performance reaches the aspirational target, it becomes the achievable SLO and a new aspiration is set
>
> **Example:**
> - Current achievable SLO: 99.5% availability
> - Aspirational SLO: 99.9% availability (requires auto-failover for the database)
> - Gap analysis: 80% of budget consumption comes from database failover taking 15+ minutes
> - Investment: Implement automatic database failover (3 months of engineering)
> - Result: Performance improves to 99.9% → aspirational becomes achievable

> **[Senior EM Application: Aspirational SLOs as Investment Justification]**
>
> Aspirational SLOs are powerful tools for roadmap conversations with leadership:
>
> "Our current SLO is 99.5%. Our aspirational target is 99.9% because [user research / competitive analysis / contract requirement]. The gap analysis shows we need [specific investment]. Here's the project plan and cost. Can we prioritize this?"
>
> This is far more compelling than "we should invest in reliability" — it's specific, measurable, and tied to a defined outcome.

---

## Identifying Incorrect SLOs

> **[Implementation Guide: Symptoms of Incorrect SLOs]**
>
> | Symptom | Diagnosis | Fix |
> |---|---|---|
> | Always out of budget, but users are happy | SLO is too strict — you're measuring something users don't care about at this sensitivity | Loosen target or change SLI to something more correlated with user satisfaction |
> | Always in budget, but users are unhappy | SLO is too lenient — or the SLI misses what users actually experience | Tighten target, add SLIs for uncaptured dimensions (latency? correctness? freshness?) |
> | Error budget is always exactly at zero | SLO perfectly matches current performance — no room for either velocity or improvement | This is either lucky or means the SLO is tracking performance rather than user expectation |
> | Team ignores the SLO | SLO doesn't influence any decisions — probably not connected to real user pain | Reconnect to user journeys; if that fails, retire the SLO (it's decorative) |
> | Stakeholders dispute the SLO data | Measurement doesn't match lived experience | Investigate SLI accuracy; measurement bugs are common and corrosive to trust |
>
> **The acid test:** Ask the team and the product manager: "When this SLO is violated, do users actually suffer? When it's healthy, are users actually happy?" If the answer is "not really" to either, the SLO needs revision.

---

## Revisit Schedules

> **[Implementation Guide: When to Review SLOs]**
>
> | Maturity Stage | Review Cadence | Focus |
> |---|---|---|
> | First 3 months after initial SLO | Every 2 weeks | Is the SLI accurate? Is the target in the right ballpark? |
> | 3-12 months | Monthly | Are targets still appropriate? Any new user journeys to capture? |
> | 1+ years (stable) | Quarterly | Has anything fundamental changed? Market, architecture, users? |
> | Always (event-driven) | After incidents, major launches, dependency changes | Does this event invalidate our current assumptions? |
>
> **The review meeting:** Keep it short (30 minutes). For each SLO, answer:
> 1. Current performance vs. target (are we meeting it?)
> 2. Budget consumption pattern (steady or spiky?)
> 3. Has anything changed that affects this SLO?
> 4. Any user feedback contradicting the SLO signal?
> 5. Decision: keep, tighten, loosen, or retire?

> **[2025 Update: SLO Lifecycle Management]**
>
> By 2025, SLO platforms have added lifecycle features:
>
> - **Automatic staleness detection:** Alerts when an SLO hasn't been reviewed in > 90 days
> - **Performance trend analysis:** Shows whether you're trending toward or away from your target over months
> - **Revision history:** Full audit trail of SLO target changes with rationale
> - **Aspirational tracking:** Dedicated views showing gap between current performance and aspirational targets
> - **Change correlation:** Automated detection of SLI shifts correlated with deployments, dependency changes, or traffic shifts
>
> The tooling helps, but the discipline of regular review remains a human responsibility. No tool can decide whether your users' expectations have changed — that requires judgment.

> **[Organizational Reality: The Politics of SLO Revision]**
>
> Changing an SLO can be politically charged:
>
> - **Tightening:** "Are you saying we weren't reliable enough before?" (Defensive teams resist)
> - **Loosening:** "Are you giving up? Are standards dropping?" (Leadership worries)
> - **Retiring:** "Are you abandoning reliability for that service?" (Compliance teams panic)
>
> **Navigation strategy:**
> - Frame tightening as "our capability has improved — let's capture that"
> - Frame loosening as "we were measuring the wrong thing — this new target better reflects user experience"
> - Frame retirement as "this SLO was decorative — replacing it with one that actually drives decisions"
>
> Always tie SLO changes to user impact or business outcomes, never to team performance evaluation.

---

**Chapter 14 establishes:** SLOs must evolve or they become irrelevant. Nine categories of triggers warrant SLO revision: first-pass corrections, usage changes, functional changes, dependency changes, failures, user expectation shifts, tooling improvements, and intuition about upcoming events. Aspirational SLOs drive improvement by making the gap between current and desired performance visible and investable. Incorrect SLOs can be identified by checking whether budget status correlates with user satisfaction — always out of budget but users happy means too strict; always in budget but users unhappy means too lenient or wrong SLI. Regular review cadences (from biweekly for new SLOs to quarterly for mature ones) ensure SLOs stay connected to reality.

**Next: Chapter 15 — Discoverable and Understandable SLOs (Alex Hidalgo), covering documentation, terminology, centralized repositories, and dashboards that make SLO information accessible to the entire organization.**
