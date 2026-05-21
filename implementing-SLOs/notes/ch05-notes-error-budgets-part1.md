# Chapter 5: How to Use Error Budgets — Part 1

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Using Error Budgets for Feature Decisions, Risk Analysis, Experimentation, and Human Processes*

Error budgets are the capstone of the Reliability Stack — the most advanced part and the most impactful when properly used. Hidalgo is careful to set expectations: not every team gets here, and getting buy-in to actually *use* error budgets for decision-making is a significant cultural achievement. But once you arrive, error budgets provide a powerful, quantitative framework for answering questions like "should we ship this?", "what should we work on?", and "is it safe to experiment?"

Part 1 covers what you can *do* with error budgets. Part 2 covers the math and policies for how to measure and enforce them.

## Table of Contents

- [Error Budgets as Communications Framework](#error-budgets-as-communications-framework)
- [Using Error Budgets for Feature Decisions](#using-error-budgets-for-feature-decisions)
  - [Budgets Are Budgets — Not Freeze Orders](#budgets-are-budgets--not-freeze-orders)
- [Using Error Budgets for Project Focus](#using-error-budgets-for-project-focus)
- [Examining Risk Factors](#examining-risk-factors)
- [Experimentation and Chaos Engineering](#experimentation-and-chaos-engineering)
  - [Load and Stress Tests](#load-and-stress-tests)
  - [Blackhole Exercises](#blackhole-exercises)
  - [Purposely Burning Budget (The Chubby Story)](#purposely-burning-budget-the-chubby-story)
- [Error Budgets for Humans](#error-budgets-for-humans)

**Block types:** [Core Concept] [Worked Example] [Common Pitfall] [Implementation Guide] [Senior EM Application] [Organizational Reality] [2025 Update] [AI & Observability]

---

## Error Budgets as Communications Framework

> *"In many ways error budgets are primarily a communications framework. They give you a common language to use in order to have discussions with others — either on your own team or across your organization or company."*

Error budgets allow statements like:
- "We are burning through our budget at the rate of 1% per day"
- "We have 15 minutes of error budget remaining"
- "Are we free to proceed as normal, or do we need to stop and examine the reliability of our service?"

This shared vocabulary is what makes error budgets so powerful organizationally. Without them, reliability conversations devolve into subjective arguments ("I think we need to focus on reliability" vs. "I think we can keep shipping"). With them, the conversation is data-driven.

> **[Core Concept: Error Budgets as Maturity Signal]**
>
> Hidalgo positions error budget adoption on a maturity spectrum:
>
> ```
> Level 1: Thinking about SLIs (user-perspective measurement)
> Level 2: Setting SLO targets (reliability objectives)
> Level 3: Calculating error budgets (measurement over time)
> Level 4: Using error budgets for decision-making ← THIS CHAPTER
> Level 5: Alerting on error budget burn rate (Chapter 8)
> ```
>
> Most organizations are at levels 1-2. Getting to level 4 requires not just technical implementation but **organizational buy-in** — product, engineering, and leadership all agreeing that error budget status drives work prioritization.

---

## Using Error Budgets for Feature Decisions

The classic use case: error budget surplus → ship features freely; error budget deficit → focus on reliability. But Hidalgo immediately complicates this:

### Budgets Are Budgets — Not Freeze Orders

> *"Rarely under this system should you actually stop releasing things. This is a frequent misconception about properly using error budgets."*

Hidalgo has seen the failure pattern: budget burns → all releases frozen → changes queue up → budget recovers → massive batch release of all queued changes → immediate new burn → freeze again → infinite cycle.

Instead, think of it like a household budget:
- Low on cash? Maybe don't book an expensive vacation. But you still buy groceries.
- Low on error budget? Maybe don't ship a risky architectural change. But you still ship bug fixes and small improvements.
- Sometimes a "vacation" is exactly what you need. Maybe shipping a feature users have been waiting for will *improve* the relationship even during a reliability downturn.

> *"Even with all of these caveats, stopping deploys is not necessarily a bad thing, especially if your organization doesn't have a robust and trusted testing and release pipeline."*

> **[Common Pitfall: The Deploy Freeze / Release Flood Cycle]**
>
> | Phase | What Happens | Why It's Bad |
> |-------|-------------|-------------|
> | Budget burns | All deploys frozen per policy | Changes accumulate in queue |
> | Budget recovers | Freeze lifted | 3 weeks of changes deployed simultaneously |
> | Massive batch deploy | Multiple changes interact in unpredictable ways | Budget burns immediately again |
> | Budget burns again | Freeze reimposed | Teams are demoralized and view SLOs as punitive |
>
> **Hidalgo's fix:** Don't freeze. Throttle. During budget pressure:
> - Continue shipping bug fixes, reliability improvements, and low-risk changes
> - Defer high-risk changes (major refactors, new dependencies, schema migrations)
> - Require additional review/canary for anything that ships during budget pressure
> - Never batch — stagger changes so each one can be evaluated independently
>
> Error budgets should *guide* decisions, not automate them. The policy should say "discuss and decide," not "freeze until green."

> **[Organizational Reality: Error Budgets Ease the Dev-Ops Tension]**
>
> The classic conflict: development wants to ship fast, operations wants stability. Error budgets transform this from a political argument into a data-driven conversation:
>
> | Without Error Budgets | With Error Budgets |
> |----------------------|-------------------|
> | "We need to slow down deploys" — "No, we need to ship" | "We have 70% budget remaining. Ship freely." |
> | "The site was down yesterday!" — "It was only 5 minutes" | "That incident consumed 12% of our monthly budget. We're at 45% with 18 days remaining." |
> | "Can we ship this risky migration?" — "I don't know, is it safe?" | "We have 3 days of budget remaining. The migration could burn up to 2 hours. The math says we can afford it if we accept being at 15% budget for the rest of the window." |
>
> The conversation shifts from opinions to math. Neither side "wins" — the data guides the decision.

---

## Using Error Budgets for Project Focus

Beyond the dev-vs-ops binary, error budgets drive **what your team works on** — especially for teams that both build and operate their software, or teams supporting open-source infrastructure they don't own the code for.

For single teams (build + operate): error budget pressure means pivoting sprint priorities from features to reliability work — or assigning a subset of engineers to reliability while others continue feature work.

For teams supporting open-source infra: you can't "stop shipping features" since you don't write the code. Instead, budget pressure triggers: configuration changes, architecture improvements, version upgrades, capacity additions, or caching layer introduction.

> **[Implementation Guide: Graduated Response to Budget Burn]**
>
> Hidalgo describes a tiered approach (formalized as policy in Part 2):
>
> | Budget Remaining | Response Level | Example for a 6-Person Team |
> |-----------------|---------------|---------------------------|
> | >66% | Business as usual | Full team on feature work |
> | 33-66% | Elevated attention | 2 engineers pivot to reliability work; rest continue features |
> | <33% | Active defense | 4 engineers on reliability; 2 on critical features only |
> | 0% (exceeded) | Full reliability focus | Entire team on reliability. Only ship changes that improve reliability. Incident retrospective mandatory. |
>
> This graduated approach avoids the binary freeze/unfreeze pattern while still ensuring that budget burn triggers proportional response.

---

## Examining Risk Factors

Error budgets measured over time reveal *what* burns your budget most — which may not be what you expect.

> **[Worked Example: The Hidden Latency Problem]**
>
> Hidalgo describes a powerful discovery pattern:
>
> You have a monthly incident that causes 30 minutes of unavailability. Big, visible, obvious. Everyone knows about it.
>
> But you also have a daily latency degradation that lasts 5 minutes. Small, subtle, easy to dismiss.
>
> Error budget math over a year:
> - Monthly unavailability: 30 min × 12 months = **360 minutes/year**
> - Daily latency issue: 5 min × 365 days = **1,825 minutes/year**
>
> The "small" daily problem is **5x more impactful** than the "big" monthly incident. Without error budget accounting, you'd focus on the flashy monthly outage. With error budget data, you discover that the boring daily latency issue deserves 5x the investment.
>
> This is the power of error budgets as a *risk analysis tool* — not just a go/no-go signal.

> **[Senior EM Application: Stack-Ranking Reliability Investments]**
>
> Error budget burn data gives you a quantitative way to prioritize reliability work:
>
> 1. Analyze error budget burn over the past quarter
> 2. Attribute burn to root causes (deploys, dependency failures, capacity, config drift, etc.)
> 3. Stack-rank by cumulative budget consumed
> 4. Invest proportionally — the causes that burn the most budget get the most engineering attention
>
> This is far more defensible than "we should fix X because it feels important." You can show leadership: "These three root causes account for 78% of our error budget burn. If we fix them, we reclaim 78% of our budget capacity for feature velocity."

---

## Experimentation and Chaos Engineering

When you have **surplus error budget**, you should spend it — not just on features, but on learning:

**Configuration experiments:** Change the cache expiry time from 1 hour to 2 hours. See what happens in production. If it degrades performance, you haven't exceeded your budget.

**Error injection:** Use tools that inject problematic data into workflows to discover edge cases during normal operations.

**Process experiments:** Switch from human-reviewed testing to automated testing. Try it when you have budget; if quality drops, revert.

**Technology swaps:** Try a different garbage collector, library, or configuration. Production is the true test.

### Load and Stress Tests

Error budgets tell you *when* it's safe to perform load tests in production. Surplus budget = safe to push systems to their breaking point. Depleted budget = postpone until recovered.

### Blackhole Exercises

Turning off an entire data center, region, or service to test failover. Extremely valuable for discovering unknown dependencies — but can burn budget fast. Only perform when you have significant surplus.

### Purposely Burning Budget (The Chubby Story)

The most advanced technique: **intentionally making your service unreliable** to enforce your published SLO and prevent dependent teams from relying on over-performance.

Hidalgo tells the famous Google Chubby story: Chubby (a distributed lock service) consistently over-performed its SLO. Every quarter, new teams would accidentally create hard dependencies on Chubby despite warnings. So every quarter, when Chubby had remaining error budget, **the service was simply shut down** for the remaining budget minutes. Teams that had secretly depended on it discovered this the hard way — and were forced to fix their dependencies.

> *"It's an advanced step to get to this point in your SLO culture, but once you get to the point that you trust your SLIs, your SLO targets, and your error budgets, there is nothing wrong with strictly enforcing them every so often to see what happens."*

> **[2025 Update: Chaos Engineering and Error Budgets Have Converged]**
>
> Since 2020, the relationship between error budgets and chaos engineering has formalized:
>
> - **Gremlin, Litmus, Chaos Mesh** all support "budget-aware" experiments that automatically abort if SLO burn rate exceeds a threshold during the experiment
> - **Steadystate hypothesis testing** (from Principles of Chaos Engineering) aligns perfectly with SLO monitoring — the "steady state" IS your SLI performing within SLO
> - **Automated game days** — scheduled chaos experiments that run when error budget is above a threshold, automatically skip when budget is low
> - **OpenSLO + chaos engineering integration** — define SLOs and chaos experiments in the same pipeline; experiments are gated by budget status
>
> The gap between "should we experiment?" and the tools to do so safely has narrowed significantly.

---

## Error Budgets for Humans

Hidalgo extends error budget thinking beyond computer services to human processes:

| Human Process | SLI | SLO Target | Error Budget Action |
|--------------|-----|-----------|-------------------|
| **Ticket response time** | % of tickets responded to within 24 hours | 95% | If below target: analyze which ticket types are slow; reassign or retrain |
| **PR review latency** | % of PRs reviewed within 4 hours | 90% | If below: investigate if certain languages or repos are bottlenecked |
| **Retrospective freshness** | "Has the team revisited retro practices this quarter?" | Yes/No | If no (exceeded): mandatory retro process discussion |
| **Vacation utilization** | % of team that has taken ≥1 week off this quarter | 80% | If below: manager checks in with those who haven't taken time off |

> *"SLO-based approaches are all about making humans happier, and you need to make sure that includes your own engineers."*

> **[Senior EM Application: Error Budgets for Management Processes]**
>
> As a Senior EM, you can apply error budget thinking to your own management activities:
>
> - **1-1 budget:** "I will hold 1-1s with all reports every 2 weeks. If I miss more than 10% of scheduled 1-1s in a quarter, I must restructure my calendar."
> - **Feedback budget:** "Each direct report receives meaningful feedback at least monthly. If any report goes >6 weeks without feedback, that's a budget violation requiring immediate correction."
> - **Cross-team alignment budget:** "I sync with each product counterpart at least biweekly. If alignment meetings drop below this rate, I must investigate what's blocking them."
>
> The power isn't the math — it's the *commitment to measure and act*. Making these implicit obligations explicit and measurable brings the same clarity that SLOs bring to service reliability.

---

**Part 1 covered:** Error budgets as a communications framework, using budgets for feature decisions (without freezing), project focus, risk factor analysis, experimentation and chaos engineering, and extending budget thinking to human processes.

**Part 2 covers:** The math of error budget calculation (events-based and time-based), rolling vs. calendar-bound windows, excluded time, choosing time windows, decision-making frameworks, and error budget policies (burn policies, exceeded policies, ownership, revisit schedules).
