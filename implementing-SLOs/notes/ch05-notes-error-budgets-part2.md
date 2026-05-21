# Chapter 5: How to Use Error Budgets — Part 2

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Error Budget Math, Time Windows, and Error Budget Policies*

Part 1 covered what error budgets are *for*. Part 2 covers how to *calculate* them (events-based and time-based approaches), how to choose time windows (rolling vs. calendar-bound), and how to formalize decision-making through **error budget policies** — the documents that turn error budget data into organizational action.

## Table of Contents

- [Error Budget Measurement: Two Approaches](#error-budget-measurement-two-approaches)
  - [Events-Based Error Budget Math](#events-based-error-budget-math)
  - [Time-Based Error Budget Math](#time-based-error-budget-math)
  - [Comparing the Two Approaches](#comparing-the-two-approaches)
- [Time Windows](#time-windows)
  - [Rolling vs. Calendar-Bound Windows](#rolling-vs-calendar-bound-windows)
  - [Excluding Time](#excluding-time)
  - [Choosing the Right Window](#choosing-the-right-window)
- [Error Budget Policies](#error-budget-policies)
  - [Owners and Stakeholders](#owners-and-stakeholders)
  - [Error Budget Burn Policies](#error-budget-burn-policies)
  - [Error Budget Exceeded Policies](#error-budget-exceeded-policies)
  - [Justification and Revisit Schedule](#justification-and-revisit-schedule)

**Block types:** [Core Concept] [Math Explained] [Worked Example] [Implementation Guide] [Common Pitfall] [Template] [Tool & Platform] [Senior EM Application]

---

## Error Budget Measurement: Two Approaches

### Events-Based Error Budget Math

The simpler of the two approaches. You already have good/total events from your SLI; error budget math just compares actual performance against the target over a time window.

> **[Math Explained: Events-Based Error Budget Calculation]**
>
> **Given:**
> - SLO target: 99.8%
> - Time window: 30 days rolling
> - Total events in window: 20,000,000
> - Bad events observed: 36,513
>
> **Step 1: Calculate allowed bad events (total error budget)**
> ```
> allowed_bad = total_events × (1 - target)
> allowed_bad = 20,000,000 × (1 - 0.998) = 20,000,000 × 0.002 = 40,000
> ```
>
> **Step 2: Calculate budget remaining**
> ```
> budget_remaining = allowed_bad - actual_bad
> budget_remaining = 40,000 - 36,513 = 3,487 events remaining
> ```
>
> **Step 3: Express as percentage of total budget**
> ```
> budget_remaining_pct = budget_remaining / allowed_bad
> budget_remaining_pct = 3,487 / 40,000 = 8.7% remaining
> ```
>
> **Interpretation:** "We have 8.7% of our error budget remaining this month — 3,487 more bad events before we exhaust it."
>
> **When budget is exceeded** (153,872 bad events observed):
> ```
> budget_remaining = 40,000 - 153,872 = -113,872
> exceeded_factor = 153,872 / 40,000 = 3.85x over budget
> ```
> "We've exceeded our error budget by 3.85x. Immediate action required."

**Key terms:**
- **Error budget surplus** — you have budget remaining
- **Error budget deficit** — you've exceeded your budget (negative remaining)
- **Error budget burn** — subtracting from budget (e.g., "burning 3 minutes per hour")
- **Error budget recovery** — bad observations falling out of the rolling window, adding budget back

### Time-Based Error Budget Math

More complex but handles low-resolution/low-quantity metrics better. Instead of counting bad events, you count bad *time intervals*.

> **[Math Explained: Time-Based Error Budget Calculation]**
>
> **Given:**
> - SLO target: 99.7%
> - Time window: 30 days
> - Base time unit: 1 second
>
> **Step 1: Calculate total data points in window**
> ```
> total_points = 1 × 60 × 60 × 24 × 30 = 2,592,000 seconds
> ```
>
> **Step 2: Calculate error budget (allowed bad seconds)**
> ```
> budget = (1 - target) × total_points
> budget = (1 - 0.997) × 2,592,000 = 0.003 × 2,592,000 = 7,776 seconds
> → 2 hours, 9 minutes, 36 seconds of allowed bad time
> ```
>
> **Step 3: Calculate current status** (3,888 bad seconds observed)
> ```
> remaining = 7,776 - 3,888 = 3,888 seconds remaining
> → 1 hour, 4 minutes, 48 seconds of budget left
> → 50% of budget consumed
> ```
>
> **If metrics have lower resolution** (e.g., 30-second intervals):
> ```
> total_points = 1 × 2 × 60 × 24 × 30 = 86,400 data points
> (multiply by 2 because there are 2 thirty-second intervals per minute)
> ```
>
> **Converting to human-readable time:**
> ```
> remaining_time = remaining_points × base_unit_seconds
> Example: 26.28 points × 30 seconds = 788.4 seconds = ~13 minutes
> ```

### Comparing the Two Approaches

| | Events-Based | Time-Based |
|--|-------------|------------|
| **Calculation complexity** | Simple — just divide and subtract | More complex — need to manage time units and resolution |
| **Best for** | High-traffic services with clear event boundaries | Any service; handles low-traffic/low-resolution well |
| **Communication** | "We have 3,487 bad events remaining" (less intuitive to non-engineers) | "We have 1 hour of error budget left" (very intuitive) |
| **Burn rate math** | Easier — rates expressed as events/time | Harder — rates expressed as time/time |
| **Latency SLIs** | More natural — individual "bad" requests are events | Less natural — latency violations happen per-request, not per-second |
| **Availability SLIs** | Works fine | More natural — availability failures manifest as periods of time |
| **Hidalgo's preference** | Use for monitoring and burn-rate alerting | Use for communication and reporting to humans |

> **[Implementation Guide: Use Both]**
>
> Hidalgo recommends calculating *both* for every SLO:
> - **Events-based** → powers your monitoring and alerting systems (burn rate math is easier)
> - **Time-based** → powers your dashboards and reports to stakeholders ("43 minutes remaining" is universally understood)
>
> One underlying data source, two views. Most SLO platforms (Nobl9, Datadog SLOs, Sloth) support both representations.

> **[Tool & Platform: Error Budget Calculation in Practice (2025)]**
>
> You rarely need to implement this math from scratch:
>
> | Tool | Error Budget Support |
> |------|---------------------|
> | **Datadog SLOs** | Native events-based and time-based; auto-calculates remaining budget; supports burn-rate alerts |
> | **Google Cloud Service Monitoring** | Native SLO/error budget with auto burn-rate alerting |
> | **Nobl9** | Full SLO management platform; OpenSLO-compatible; multi-source SLIs |
> | **Sloth** (open source) | Generates Prometheus recording rules for multi-window multi-burn-rate SLOs |
> | **Grafana SLO** | Native SLO tracking with error budget visualization in Grafana Cloud |
> | **Prometheus + recording rules** | DIY approach; requires manual configuration but fully flexible |
> | **OpenSLO** | Vendor-neutral definition format; implementations available for multiple platforms |
>
> The DIY Prometheus approach was dominant in 2020. By 2025, purpose-built SLO platforms have made the calculation, visualization, and alerting much easier — especially for organizations with many services.

---

## Time Windows

### Rolling vs. Calendar-Bound Windows

**Rolling window:** Moves forward continuously (e.g., "the last 30 days from right now"). Bad events fall out as they age beyond the window edge. Your budget continuously updates.

**Calendar-bound window:** Tied to calendar months or quarters. Resets at a fixed point (e.g., "from the 1st of this month"). Budget returns to 100% on the first day of each period.

| | Rolling | Calendar-Bound |
|--|---------|---------------|
| **Advantage** | Reflects recent performance continuously; no "reset day" | Easier to explain ("this month we've used X%"); aligns with business reporting cycles |
| **Disadvantage** | Harder to explain; never fully "resets" | Past failures can fall off the day after they happen if they occur near month-end; creates perverse incentives |
| **Best for** | Technical teams making day-to-day decisions | Business reporting, SLA alignment, quarterly reviews |

> **[Common Pitfall: The Calendar-Bound Reset Cycle]**
>
> Hidalgo describes a destructive pattern with calendar-bound windows:
>
> 1. Month 1: Error budget exceeded → feature freeze per policy
> 2. Rest of Month 1: Teams queue up features (can't ship them)
> 3. Month 2, Day 1: Budget resets to 100% → ALL queued features ship simultaneously
> 4. Massive batch change → immediate budget burn in Month 2
> 5. Month 2: Budget exceeded again → freeze again → cycle repeats
>
> **The fix:** If using calendar-bound windows:
> - Never batch deploys after a freeze — stagger releases over the first 1-2 weeks
> - Consider whether rolling windows would serve your team better for operational decisions (use calendar for reporting only)
> - Have explicit policy about post-freeze release cadence

### Excluding Time

Some services don't need to be reliable 24/7. Examples: point-of-sale systems (business hours only), databases with daily backup windows, batch systems that only run certain hours.

**Options:**
1. Don't collect metrics during excluded time
2. Collect but mark all observations as "good" during excluded time
3. Simply subtract excluded time from the total window calculation

```
Example: 2-hour daily maintenance window
Total seconds/day: 86,400
Excluded: 7,200 (2 hours)
Effective seconds/day: 79,200
Use 79,200 as basis for error budget calculations
```

### Choosing the Right Window

Hidalgo's guidelines:

- **Default:** 28 or 30 days — familiar, aligns with billing cycles, matches human expectation
- **For customer-facing products:** Consider 90-day (quarterly) windows — humans remember bad experiences longer than 30 days; a monthly reset might let you ignore problems your users haven't forgotten
- **For internal services:** 30-day rolling usually fine — internal consumers are more forgiving and iterate faster
- **Keep it familiar:** Use units people know (weeks, months, quarters) — not arbitrary periods like "17 days"

> *"Don't discount that humans often think in terms of the units of time they're used to."*

---

## Error Budget Policies

The policy is what turns error budget *data* into organizational *action*. Without a written policy, teams have data but no agreement about what to do when the numbers change.

### Owners and Stakeholders

Every error budget policy needs a clear owner:
- **For individual microservices:** The team responsible for that service
- **For multi-service products:** Managers of managers or directors
- **For entire business products:** CTO or CEO level

The owner doesn't do all the work — but they're responsible for **starting the conversations** that error budget changes demand.

### Error Budget Burn Policies

Graduated response when budget is *being consumed* but not yet exceeded:

> **[Template: Error Budget Burn Policy]**
>
> ```
> Service: [name]
> SLO: [target]
> Window: [time period]
>
> BURN RESPONSE TIERS:
>
> Tier 1 — Budget at 66-100% remaining:
>   - Business as usual
>   - Weekly SLO status check in staff meeting
>   - MAY ship features freely
>
> Tier 2 — Budget at 33-66% remaining:
>   - SHOULD assign 1-2 engineers to reliability work
>   - MUST include reliability status in daily standup
>   - MAY continue feature work for remaining engineers
>   - SHOULD investigate top budget-burning causes
>
> Tier 3 — Budget at 0-33% remaining:
>   - MUST assign majority of team to reliability work
>   - MUST defer high-risk changes (migrations, major refactors)
>   - SHOULD escalate to [director/VP] for visibility
>   - MAY continue low-risk feature work
>
> Tier 4 — Budget exceeded (deficit):
>   - MUST focus entire team on reliability
>   - MUST conduct incident retrospective
>   - MUST communicate to dependent teams
>   - MUST NOT ship changes that don't directly improve reliability
>   - REQUIRED: retrospective findings shared within [X days]
> ```
>
> **Note the language:** `MUST` for non-negotiables, `SHOULD` for strong recommendations, `MAY` for options. Hidalgo explicitly recommends RFC 2119 language for clarity.

### Error Budget Exceeded Policies

When budget is fully exhausted:
- **Incident retrospective is mandatory** — even if the conclusion is "our target was wrong"
- **Communication to dependent teams** — they need to know your reliability has degraded
- **Escalation proportional to blast radius** — microservice team → director; entire product → CTO
- **More trust, less prescription** — use `should` and `may` where possible; trust people to make good decisions

Hidalgo addresses the inevitable conflict: *"What do you do if your error budget policy says you must halt feature work, but your CEO says that you must ship a certain feature?"* His answer: there's no formula for this. But error budget data gives you **a quantitative basis for pushback** that you wouldn't otherwise have.

### Justification and Revisit Schedule

Every policy should include:
- **Why these thresholds were chosen** — helps future readers understand the reasoning
- **When the policy will be reviewed** — new policies: monthly review; mature policies: quarterly or yearly
- **What would trigger an off-schedule review** — major incident, team restructure, significant service change

> **[Senior EM Application: Getting the Error Budget Policy Signed]**
>
> The error budget policy is the document where the rubber meets the road. It's where product leadership agrees *in advance* that they'll defer features when reliability suffers. Getting this signed requires:
>
> 1. **Before the crisis:** Present the policy during a calm period. Frame it as "here's how we'll handle things when reliability degrades — so we don't have to argue in the moment."
> 2. **Include product leadership as co-owner:** The policy works best when the product EM or Director is a co-signer. This prevents "SRE is blocking us" narratives.
> 3. **Make it reciprocal:** "When budget is healthy, SRE will not block deploys or impose extra gates." Product gets something too — freedom during surplus.
> 4. **Start conservative:** Set thresholds that are unlikely to trigger often. Build trust. Then tighten if needed.
> 5. **Point to data when it triggers:** "Per our agreed policy, we're at Tier 3. This means [specific actions]. Here's the data."
>
> The hardest part is getting the signature *before* the crisis. Once you're in a crisis without a pre-agreed policy, every decision is political. With a signed policy, it's procedural.

> **[AI & Observability: AI-Powered Error Budget Management (2025)]**
>
> AI is adding intelligence to error budget workflows:
>
> | Capability | How It Works |
> |-----------|-------------|
> | **Predictive burn-rate** | ML projects current burn rate into the future: "At current rate, budget exhausts in 6 hours" — triggers pre-emptive action |
> | **Budget attribution** | AI correlates budget burn with concurrent events (deploys, dependency changes, traffic spikes) to auto-identify root causes |
> | **Policy recommendation** | AI analyzes historical burn patterns and suggests optimal tier thresholds: "Based on past behavior, triggering at 40% instead of 33% gives you 2 extra days of lead time" |
> | **Automated tier escalation** | Integrate error budget tiers with PagerDuty/Opsgenie: automatic escalation policies based on budget remaining |
> | **Natural language summaries** | "Your checkout service has consumed 62% of error budget this month, primarily due to 3 deployment-related incidents on days 5, 12, and 18. Recommendation: increase canary duration from 10 to 30 minutes." |
>
> The math hasn't changed since Hidalgo wrote. The *automation* of responding to that math has advanced significantly.

---

**Chapter 5 establishes:** Error budgets are the most advanced and most impactful part of the Reliability Stack. They enable feature decisions, project focus, risk ranking, experimentation, and chaos engineering — all driven by data rather than opinion. Two calculation methods (events-based for alerting, time-based for communication). Rolling windows for operations, calendar-bound for reporting. Error budget policies formalize the organizational response and must be agreed *before* the crisis hits.

**Next: Chapter 6 — Multiwindow, Multi-Burn-Rate Alerts, where the book transitions from philosophy to implementation with the alerting math that makes error budgets operationally useful.**
