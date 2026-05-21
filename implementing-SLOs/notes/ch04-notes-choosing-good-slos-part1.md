# Chapter 4: Choosing Good Service Level Objectives — Part 1

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Reliability Targets, User Happiness, the Nines Trap, and Service Dependencies*

Chapter 3 taught you how to develop meaningful SLIs — measurements from the user's perspective. Chapter 4 answers the next question: **what target should you set for those measurements?** How reliable is "reliable enough"? Hidalgo walks through the philosophy of target-setting (user happiness as the north star), common traps (being too reliable, fixating on nines, having too many SLOs), and the critical role of service dependencies in constraining what you can actually promise. Part 2 covers the practical techniques for choosing targets using statistics and historical data.

## Table of Contents

- [What SLO Targets Really Are](#what-slo-targets-really-are)
  - [User Happiness as the Criterion](#user-happiness-as-the-criterion)
- [The Problem of Being Too Reliable](#the-problem-of-being-too-reliable)
- [The Problem with the Number Nine](#the-problem-with-the-number-nine)
- [The Problem with Too Many SLOs](#the-problem-with-too-many-slos)
- [Service Dependencies and Components](#service-dependencies-and-components)
  - [Hard Dependencies](#hard-dependencies)
  - [Soft Dependencies](#soft-dependencies)
  - [Turning Hard into Soft](#turning-hard-into-soft)
  - [Dependency Math](#dependency-math)
  - [Single-Team vs. Multi-Team Component Services](#single-team-vs-multi-team-component-services)
- [Reliability for Things You Don't Own](#reliability-for-things-you-dont-own)

**Block types:** [Core Concept] [Worked Example] [Common Pitfall] [Math Explained] [Implementation Guide] [Senior EM Application] [2025 Update] [Template]

---

## What SLO Targets Really Are

> *"If a service level indicator gives you a good way to think about whether your service is performing in the manner it should be, a service level objective gives you a good way to think about whether your service is doing so often enough."*

Hidalgo frames SLOs as fundamentally about *frequency of failure*: complex systems will always fail. SLOs define how often that failure is acceptable.

### User Happiness as the Criterion

Good SLOs have two traits:

1. **If you're exceeding your SLO target, your users are happy** with the state of your service
2. **If you're missing your SLO target, your users are unhappy** with the state of your service

"Happiness" here means *contentment* — not active joy, but the absence of dissatisfaction. Users not complaining, not churning, not seeking alternatives. For internal services, "happiness" means other engineers aren't building workarounds or leaving the company because your platform is too unreliable.

> **[Core Concept: The Two-Sided Test for SLO Targets]**
>
> Any proposed SLO target must pass BOTH sides of this test:
>
> | Test | Question | If it fails... |
> |------|----------|---------------|
> | **Too loose** | "If we hit this target, are users actually happy?" | Your SLO allows too much failure — users are unhappy even when you're "meeting" the target. Tighten it. |
> | **Too tight** | "If we miss this target slightly, are users actually unhappy?" | Your SLO is stricter than users need — you're investing in reliability nobody notices. Loosen it. |
>
> The sweet spot: the narrowest band where exceeding = happy and missing = unhappy. If there's a gap where you can miss your target and users don't notice, your target is too strict. If users are unhappy even when you're meeting your target, it's too loose (or your SLI isn't measuring the right thing).

---

## The Problem of Being Too Reliable

This is one of the book's most counterintuitive arguments: **being too reliable is a problem.**

Hidalgo's scenario: your SLO is 99.9%, but you're routinely running at 99.99%. Even if your published target is 99.9%, users start *expecting* 99.99% because humans expect the future to look like the past (Chapter 2's implied agreements). Now if you ever drop to your actual target of 99.9%, it feels like degradation.

**But the deeper problems are:**

1. **You lose the freedom SLOs provide.** If you're too reliable, you have no error budget to spend on experiments, chaos engineering, faster feature shipping, or learning from failures.

2. **Operational underload.** People learn by handling failures. If things never break, your team never develops incident response skills. When the inevitable big failure comes, they're unprepared.

3. **Raised expectations are hard to walk back.** Once users expect 99.99%, formally targeting 99.9% becomes politically difficult — even though 99.9% was always adequate.

> **[Senior EM Application: The "Too Reliable" Conversation]**
>
> This is one of the hardest conversations for a Senior EM: explaining to leadership why *reducing* reliability investment might be correct.
>
> **The argument:**
> "Our SLO is 99.9%. We've been running at 99.98% for 6 months. This means:
> - We're spending engineering effort maintaining reliability that users don't need
> - Our error budget is essentially full at all times — we've never tested our incident response under budget pressure
> - We've never had a meaningful error budget conversation because there's nothing to discuss
> - We could redirect 20% of reliability engineering effort toward [feature X / platform improvement Y] without any user impact
>
> I propose we *intentionally* relax our reliability posture slightly — not by being careless, but by investing less in preventing the rare failures that our users have shown they tolerate."
>
> This requires confidence in your SLO target. If you're not sure 99.9% is actually sufficient for user happiness, you can't make this argument. The two-sided test (above) must be validated first.

> **[Common Pitfall: The Ratchet Effect]**
>
> The pattern:
> 1. Set SLO at 99.9%
> 2. Over-perform at 99.99% for a year
> 3. Users and leadership notice: "We're at four nines! Great!"
> 4. Someone says: "Let's make 99.99% our new target"
> 5. Now you're committed to a target you never needed, at much higher cost
> 6. Error budget shrinks 10x (from 43 min/month to 4.3 min/month)
> 7. Teams can no longer deploy aggressively or experiment
> 8. Velocity drops. Leadership asks "why are we shipping so slowly?"
>
> **The fix:** When you over-perform, proactively communicate: "We exceeded our target this quarter. This is nice but not our goal — our goal is to maintain 99.9% while maximizing feature velocity. We will not ratchet the target upward unless user research shows they need it."

---

## The Problem with the Number Nine

People think about SLOs in terms of "nines" — 99%, 99.9%, 99.99%, 99.999%. Hidalgo argues this is an arbitrary constraint that limits good target-setting.

**The nines translated to time:**

| Target | Per Day | Per Month | Per Year |
|--------|---------|-----------|----------|
| 99.999% | 0.9 seconds | 26.3 seconds | 5 min 16 sec |
| 99.99% | 8.6 seconds | 4 min 23 sec | 52 min 36 sec |
| 99.9% | 1 min 26 sec | 43 min 50 sec | 8 hr 46 min |
| 99% | 14 min 24 sec | 7 hr 18 min | 3 days 16 hr |

**But why only nines?** Hidalgo argues there's nothing wrong with targets like 99.97%, 99.7%, 98%, or even 87%. The target should be derived from user needs and operational reality, not from what "sounds good."

| Target | Per Day | Per Month | Per Year |
|--------|---------|-----------|----------|
| 99.95% | 43.2 sec | 21 min 36 sec | 4 hr 23 min |
| 99.7% | 4 min 19 sec | 2 hr 10 min | 1 day 2 hr |
| 99.3% | 10 min 5 sec | 5 hr 7 min | 2 days 13 hr |
| 98% | 28 min 48 sec | 14 hr 37 min | 7 days 7 hr |

> *"Some of the most useful SLOs I have personally worked with have been set at carefully measured numbers like 97.2%, and there is nothing wrong with that."*

Hidalgo suggests sometimes starting with *time* rather than percentage: "We need to account for about 2 hours of unreliability per month (due to dependency downtime, backup locks, etc.)" → that's 99.7%.

> **[Implementation Guide: Don't Start with Nines — Start with Acceptable Bad-Time]**
>
> Instead of asking "how many nines should we target?" ask:
>
> 1. "How much bad time per month can our users tolerate before they're unhappy?"
> 2. Convert to a percentage: `target = 1 - (bad_minutes / total_minutes_in_month)`
> 3. Round to something meaningful — NOT to the nearest nine
>
> ```
> Example:
> - Users tolerate ~2 hours of degraded service per month (based on support ticket analysis)
> - 2 hours = 120 minutes
> - Total minutes in 30 days = 43,200
> - Target = 1 - (120 / 43,200) = 1 - 0.00278 = 99.72%
>
> Your SLO is 99.72% — not 99.9% (too tight) or 99% (too loose).
> ```

---

## The Problem with Too Many SLOs

Hidalgo warns against SLO proliferation. The right number depends on service complexity and organizational maturity, but common problems emerge when you have too many:

1. **Harder to make decisions.** Too many data points = analysis paralysis. The purpose of SLOs is clarity about reliability status; 47 SLOs for one service produces the opposite.

2. **Harder to communicate.** If you can report 3-5 SLOs to stakeholders, they can understand your reliability story. If you present dozens, they can't.

3. **Statistical noise (multiple comparison problem).** With many measurements, you'll *always* find something that looks slightly off — sending you down rabbit holes investigating non-problems.

> *"Every system is unique, and there is no perfect answer to the question of how many SLOs you should define for any particular service."*

Hidalgo's example: a storage service with a cache layer doesn't need separate SLOs for cache-hit latency and cache-miss latency. One SLO for "general read latency" suffices — the separate metrics are diagnostic tools used when the SLO indicates a problem.

> **[Common Pitfall: SLO Proliferation]**
>
> | Symptom | Root Cause | Fix |
> |---------|-----------|-----|
> | Team has 20+ SLOs for one service | Confused SLOs with monitoring metrics | Reduce to 3-5 SLOs that cover critical user journeys; keep the 20 metrics as diagnostics |
> | Every microservice has its own SLO | Bottom-up measurement without user-journey thinking | Define SLOs at the user journey level (which crosses multiple services), not per-component |
> | SLO dashboards are overwhelming | No curation or prioritization | Create a "top-level" view with 3-5 SLOs that tell the reliability story; details available on drill-down |
> | Nobody looks at SLO dashboards | Too many numbers, no clear signal | If you can't answer "are we healthy or not?" in 5 seconds, you have too many SLOs |

---

## Service Dependencies and Components

### Hard Dependencies

A hard dependency is one that **must** be reliable for your service to be reliable. Your service cannot be more reliable than its hard dependencies.

> *"If the reliability of your service directly depends on the reliability of another service, your service cannot be any more reliable than that one is."*

Two ways to determine hard dependency reliability:
1. **Measure it yourself** — you're the user; measure how it behaves from your perspective
2. **Look at the dependency's published SLOs** — if they practice SLO-based reliability, their targets tell you what to expect

### Soft Dependencies

A soft dependency **impacts** but doesn't **nullify** your reliability when it fails.

Hidalgo's example: a maps app has a hard dependency on map tile data (no maps = no service). But traffic overlay, restaurant reviews, and satellite view are soft dependencies — the app still works without them, just with less functionality.

### Turning Hard into Soft

One of the best reliability investments: convert hard dependencies into soft ones.

Example: your service has a hard dependency on a database. Introducing a cache turns it into a *soft* dependency for reads — if the database is down, you serve from cache (stale but available). The service degrades gracefully instead of failing completely.

### Dependency Math

> **[Math Explained: Why 40 Services at 99.9% = Only 96% Overall]**
>
> If your service has N components, each with reliability R, and all are hard dependencies with equal weight, the composite reliability is:
>
> ```
> Composite reliability = R^N
> ```
>
> Example: 40 components at 99.9% each:
> ```
> 0.999^40 = 0.9608 = ~96.1%
> ```
>
> **40 services, each "three nines" reliable, give you a composite service that's barely "two nines."**
>
> This is why:
> - Individual component SLOs don't automatically translate to service-level SLOs
> - Reducing hard dependencies is high leverage (each one removed improves the exponent)
> - Caching, circuit breakers, and graceful degradation convert hard → soft dependencies, removing them from the multiplication
>
> **Practical implication:** If you're setting an SLO for a service composed of many microservices, you CANNOT just say "each service is 99.9%, therefore we're 99.9%." You must either: (a) calculate the composite, (b) measure end-to-end from user perspective (which automatically captures dependency effects), or (c) accept that your service-level SLO must be lower than your component SLOs.

> **[2025 Update: Dependency Mapping Has Gotten Easier]**
>
> When Hidalgo wrote, identifying all dependencies was largely manual. By 2025:
>
> - **OpenTelemetry service graphs** automatically map which services call which, with latency and error rates for each edge
> - **Service mesh observability** (Istio, Linkerd) provides complete dependency graphs without code changes
> - **eBPF-based tools** (Pixie, Groundcover) can discover dependencies at the kernel level, catching even undocumented connections
> - **Backstage service catalog** + auto-discovery plugins maintain a living dependency map
> - **AI-powered dependency analysis** correlates failures across services to identify hard vs. soft dependencies empirically
>
> The dependency math Hidalgo describes is the same, but *discovering* what your dependencies are is dramatically easier.

### Single-Team vs. Multi-Team Component Services

**Multi-team services:** Each component team should have its own SLIs/SLOs (for their own decision-making), PLUS there should be SLOs for the overarching user-facing service. Question: who owns the top-level SLO? (Chapter 15 covers ownership.)

**Single-team services:** You probably don't need SLOs for every internal component. Define SLIs at the user-journey level that spans components. Use per-component metrics as diagnostic tools when the journey-level SLO degrades.

Hidalgo's example: a logging pipeline (message queue → indexer → storage) owned by one team doesn't need three SLOs. One SLI measuring end-to-end latency (insert → queryable) plus one for data integrity covers most user needs.

---

## Reliability for Things You Don't Own

Hidalgo addresses situations where the classic "stop features, fix reliability code" doesn't apply:

**Open source or hosted services:** You can't change the code, but you can change configuration, architecture, and complementary code. Use SLO data to justify renewing contracts or finding new vendors.

**Hardware:** You need large datasets for meaningful statistical analysis. Options:
- If you have enough hardware: measure your own failure rates
- If you don't: use aggregated data from vendors or public reports (e.g., Backblaze hard drive failure reports)
- Apply statistical models from Chapter 9 to sparse data

**The bottom-up ideal:** In a perfect world, every dependency would have a published SLO, from power delivery to network switches to VMs to your application. In practice, start wherever you can and expand over time.

> **[Senior EM Application: Using Dependency SLOs in Vendor Negotiations]**
>
> As a Senior EM, you often manage vendor relationships (cloud providers, SaaS tools, managed databases). Hidalgo's dependency math gives you a quantitative framework for these conversations:
>
> "Our service needs to be 99.9% reliable for our users. We have 5 hard dependencies on your platform. If each dependency runs at 99.95%, our composite is 0.9995^5 = 99.75% — which exceeds our target. But if any dependency drops to 99.5%, our composite becomes 0.995 × 0.9995^4 = 99.3% — which violates our target.
>
> Therefore, we need your SLA to guarantee at least 99.95% per dependency, and we need visibility into per-dependency SLO performance (not just aggregate uptime)."
>
> This is far more productive than the usual conversation: "We need you to be more reliable."

---

**Part 1 covered:** What SLO targets represent (frequency of acceptable failure), user happiness as the criterion, why being too reliable is a problem, why nines are arbitrary, why too many SLOs is counterproductive, and how dependencies constrain your targets (including the composite reliability math).

**Part 2 covers:** Practical techniques for choosing targets — using historical data, basic statistics (min/max/mean/median/mode, ranges, percentiles), metric attributes (resolution, quantity, quality), percentile thresholds for long-tail distributions, and what to do when you have no history.
