# Chapter 4: Choosing Good Service Level Objectives — Part 2

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Using Statistics and Historical Data to Choose Targets*

Part 1 covered the philosophy of target-setting and dependency constraints. Part 2 covers the *practical techniques*: how to use historical data, basic statistical tools, and metric attributes to arrive at a concrete target number. Hidalgo also covers percentile thresholds for handling long-tail distributions and what to do when you have no history to analyze.

## Table of Contents

- [Choosing Targets Using Past Performance](#choosing-targets-using-past-performance)
- [Basic Statistics for SLO Target-Setting](#basic-statistics-for-slo-target-setting)
  - [The Five Ms: Min, Max, Mean, Median, Mode](#the-five-ms-min-max-mean-median-mode)
  - [Ranges](#ranges)
  - [Percentiles](#percentiles)
- [Metric Attributes That Affect Target Choice](#metric-attributes-that-affect-target-choice)
  - [Resolution](#resolution)
  - [Quantity](#quantity)
  - [Quality](#quality)
- [Percentile Thresholds for Long Tails](#percentile-thresholds-for-long-tails)
- [What to Do Without a History](#what-to-do-without-a-history)

**Block types:** [Core Concept] [Worked Example] [Math Explained] [Implementation Guide] [Common Pitfall] [Tool & Platform] [AI & Observability] [Template]

---

## Choosing Targets Using Past Performance

> *"The best way to figure out how your service might operate in the future is studying how it has operated in the past."*

Hidalgo's process:
1. If your SLI metric already exists: analyze a meaningful period of historical data (at least one full calendar month)
2. If it's a new metric: collect it for a month before setting a target
3. Use the data to determine what percentage of time you've been "good"
4. Set your initial SLO based on that measured percentage
5. Iterate as you learn more about user expectations

Important caveat: you may want to **discount previous catastrophes** — severe incidents are often outlier events that you've already fixed. They're important for learning but may not represent future performance.

> *"SLOs are objectives, they're not formal agreements... There is no shame in picking a target and then changing it in short order if it turns out that you were wrong."*

---

## Basic Statistics for SLO Target-Setting

### The Five Ms: Min, Max, Mean, Median, Mode

Hidalgo introduces basic statistics through a worked example. Given this time series sample (10 observations):

| Time | 16:00 | 16:01 | 16:02 | 16:03 | 16:04 | 16:05 | 16:06 | 16:07 | 16:08 | 16:09 |
|------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
| **Value** | 1.5 | 6 | 2.4 | 3.1 | 21 | 9.1 | 2.4 | 1 | 0.7 | 5 |

Sorted ascending: 0.7, 1, 1.5, 2.4, 2.4, 3.1, 5, 6, 9.1, 21

| Statistic | Value | What It Tells You for SLOs |
|-----------|-------|---------------------------|
| **Min** | 0.7 | Best-case performance — your floor |
| **Max** | 21 | Worst-case performance — your ceiling |
| **Mean** (average) | 5.52 | Average performance — better than eyeballing a graph |
| **Median** (middle value) | 2.75 | The "typical" value — splits data in half. Here it's lower than mean, meaning outliers skew upward |
| **Mode** (most frequent) | 2.4 | The most common observation |

> **[Math Explained: What Mean vs. Median Tells You About SLI Data]**
>
> In this example: mean (5.52) > median (2.75). This means:
> - More values are *below* the average than above it (7 below, 3 above)
> - The high values are outliers that pull the mean up
> - The "typical" user experience is better than the average suggests
>
> **For SLO target-setting:** If your latency data has mean > median, you have a long tail of slow requests pulling the average up. Most users experience good performance (closer to median), but some experience significantly worse. This is exactly when percentile-based thresholds (covered below) are most valuable — they let you set targets for the "normal" experience while separately monitoring the tail.
>
> **If mean ≈ median:** Your data is symmetrically distributed — outliers are balanced. Simple threshold-based SLOs work well.
>
> **If mean < median:** Rare but indicates negative outliers (your service is occasionally *better* than normal). Unusual for reliability metrics.

### Ranges

Range = max - min = 21 - 0.7 = 20.3

A large range means high variability in your data. For SLI data, a large range suggests inconsistent user experience — some requests are great, some are terrible. This is often a sign that:
- You need percentile-based analysis (the mean isn't representative)
- There may be distinct populations in your data (e.g., cached vs. uncached requests)
- Outlier investigation is warranted (is the max value a real problem or a measurement artifact?)

### Percentiles

> *"A percentile is a simple but powerful concept when it comes to developing an understanding of SLOs."*

A percentile tells you: "X% of all values fall at or below this threshold."

**How percentiles help choose SLO targets:**

Calculate the P99 of your latency data for a month. You now know: "If I had set my SLO target at 99%, I would have met it over this period." If users were happy during that month, 99% is a reasonable starting target.

Common percentile levels: P50 (median), P90, P95, P98, P99, P99.9, P99.99

> **[Worked Example: Using Percentiles to Set a Latency Target]**
>
> You have one month of latency data for your checkout API. You calculate:
>
> | Percentile | Latency Value | Interpretation |
> |-----------|--------------|----------------|
> | P50 | 120ms | Half of requests complete within 120ms |
> | P90 | 350ms | 90% complete within 350ms |
> | P95 | 500ms | 95% complete within 500ms |
> | P99 | 1,200ms | 99% complete within 1,200ms |
> | P99.9 | 4,500ms | 99.9% complete within 4.5 seconds |
>
> Your user research says pages should load within 2 seconds. Setting threshold at 2,000ms:
> - At P99: 99% of requests are under 2s ✓
> - At P99.9: 99.9% are under 4.5s (many above 2s) ✗
>
> **Starting SLO:** "99% of checkout requests complete within 2 seconds" — this matches observed performance and user expectations.
>
> Over time, as you improve the service, you can tighten to 99.5% or 99.9% — but start where the data says you actually are.

---

## Metric Attributes That Affect Target Choice

### Resolution

Your metrics may only be reported every 10, 30, or 60 seconds. This creates a problem:

> **[Math Explained: Resolution vs. Target Interaction]**
>
> If your target is 99.95% (43.2 seconds of error budget per day) and your metrics have 60-second resolution, a *single bad observation* consumes 60 seconds — more than your entire daily budget. This means:
>
> ```
> Target: 99.95% → 43.2 sec/day allowed bad time
> Metric resolution: 60 seconds
> Problem: 1 bad data point = 60 sec = EXCEEDS daily budget
> ```
>
> **Solutions:**
> 1. **Require sustained violation:** Only count an observation as "bad" if 2+ consecutive measurements are bad (reduces false positives but lowers effective resolution)
> 2. **Choose a looser target:** 99.9% gives you 86 sec/day — now a single bad observation doesn't blow the budget
> 3. **Improve metric resolution:** Collect more frequently so each data point represents less time
>
> **Rule:** Your target must be achievable given your metric resolution. If `(1 - target) × seconds_per_day < metric_resolution`, your target is too strict for your data.

### Quantity

Some services have infrequent events — batch jobs that complete once per hour, pipelines that process daily, APIs with low traffic at night.

Hidalgo's example: a data pipeline completing once per hour. One failure in 24 hours = 23/24 = 95.83% reliability *for that day*. This is fine — but your error budget window needs to be large enough to accommodate it. Looking at single-day slices will always show volatile percentages.

**Options for low-quantity services:**
- Use larger time windows (weekly or monthly instead of daily)
- Only calculate SLOs during active hours (exclude low-traffic periods)
- Consider observations during quiet periods as automatic successes
- Use confidence intervals (Chapter 9) to handle statistical uncertainty

### Quality

Your metrics might be inaccurate, noisy, ill-timed, or badly distributed. If data quality is low:

- **Require sustained violations** before counting bad events (protects against noise)
- **Use percentage-of-percentage:** e.g., "50% of observations within a 5-minute window must be bad before we count one bad event"
- **Accept a lower target than true performance** — if your measurements aren't precise, build in buffer

> *"You can even make low-quality data work for you — though you just might need to set targets lower than what your service actually performs like for your users."*

---

## Percentile Thresholds for Long Tails

This is one of the chapter's most practical sections. Hidalgo shows how to handle services where the "long tail" of slow requests creates problems for simple threshold-based SLOs.

**The problem:** Your website has P95 latency of 1.8 seconds (under your 2-second threshold) but P99 is 4 seconds. If you set a simple SLO of "99% of requests under 2 seconds," you lose visibility into everything above P95.

**The solution:** Use percentile thresholds in your SLO definition:

> *"You could say that you want web pages to load within 2,000 ms at the 95th percentile, 99.9% of the time."*

This lets you set MULTIPLE SLOs covering different percentile bands:

```
SLO 1: P95 of requests complete within 2,000ms — 99.9% of the time
SLO 2: P98 of requests complete within 2,500ms — 99.9% of the time
SLO 3: P99 of requests complete within 4,000ms — 99.9% of the time
```

> **[Core Concept: Why Percentile Thresholds Beat Simple Percentage Targets]**
>
> | Approach | What You See | What You Miss |
> |----------|-------------|---------------|
> | **Simple: "95% of requests under 2s"** | Whether 95% are fast enough | What the other 5% looks like — could be 3s (fine) or 30s (terrible) |
> | **Percentile: "P95 under 2s, 99.9% of the time"** | Whether the typical experience is good, PLUS you can monitor P98 and P99 separately | Nothing — you have full visibility across the distribution |
>
> The percentile approach also avoids a reporting problem: a "95% target" sounds low to non-technical stakeholders. But "99.9% of the time, 95% of requests complete within 2 seconds" sounds rigorous — even though it describes the same behavior. Hidalgo notes Charity Majors' quote: *"Nines don't matter if users aren't happy."* But the reverse is also true: how you *express* your target matters for organizational buy-in.

> **[Template: Multi-Percentile SLO Definition]**
>
> ```
> Service: [name]
> SLI: Request latency (time from request received to response sent)
>
> SLO Targets:
>   - P50 latency ≤ 100ms, 99.9% of the time    (typical experience)
>   - P95 latency ≤ 500ms, 99.9% of the time    (mainstream experience)
>   - P99 latency ≤ 2000ms, 99.9% of the time   (tail experience)
>
> Window: 30-day rolling
> Budget: Events-based (good events / total events per percentile band)
>
> Rationale: User research shows satisfaction drops significantly above 500ms
>            for typical browsing. Occasional slow requests (P99) are tolerable
>            up to 2 seconds. Beyond 2 seconds, users abandon.
> ```

---

## What to Do Without a History

For new services with no historical data and no existing users:

> *"The honest answer is: just take an educated guess!"*

Hidalgo's pragmatic advice:
- Look at the SLOs of services yours will depend on (you can't exceed them)
- Look at the SLOs of services that will depend on yours (they need something from you)
- Consider similar services at your company or in your industry
- Pick a number, commit to it for a month, see what happens
- **You can change it.** SLOs are not contracts.

> *"It's also true that not every service has to have an SLO at launch — or even at all."*

If you don't have the data for mathematical target-setting, you can still practice SLO *thinking* without formal numbers. The mindset is more important than the percentage.

> **[AI & Observability: AI-Assisted Target Selection]**
>
> AI tools in 2025 can accelerate the target-setting process:
>
> | Manual Process (Hidalgo's era) | AI-Assisted (2025) |
> |-------------------------------|-------------------|
> | Collect a month of data, manually calculate percentiles | Auto-calculate P50/P90/P95/P99 with seasonal decomposition |
> | Eyeball graphs to identify outliers | ML-based anomaly detection flags outliers automatically |
> | Manually correlate SLI performance with user satisfaction | ML correlates error budget burn with support ticket volume to validate the target |
> | Guess at targets for new services | Predictive models based on similar services in your org suggest starting targets |
> | Periodically review if target is still correct | Continuous assessment: "Your users are happy at 99.5% but your target is 99.9% — consider loosening" |
>
> The human judgment Hidalgo emphasizes remains essential — AI can't tell you what "user happiness" means for your business. But it can dramatically reduce the data analysis burden.

> **[Implementation Guide: The 30-Day Target-Setting Sprint]**
>
> Hidalgo's process, made actionable:
>
> **Week 1:** Define SLI, start collecting if new. If existing metric: pull 30 days of data.
>
> **Week 2:** Calculate P50, P90, P95, P99. Identify outliers. Calculate current "reliability percentage" (good events / total events).
>
> **Week 3:** Propose a target. Apply the two-sided test:
> - "If we hit this target, would users be happy?" (validate with support tickets, NPS, churn data)
> - "If we miss by a little, would users notice?" (check if past misses correlated with complaints)
>
> **Week 4:** Publish the provisional SLO. Set up the dashboard. Begin observing against the target.
>
> **Month 2+:** Iterate. Was the target too tight (always exceeding → no decisions to make)? Too loose (users complaining even when met)? Adjust.
>
> This takes one person about 20% of their time for a month — not a full-team effort.

---

**Chapter 4 establishes:** SLO targets should make users happy when met and signal problems when missed. Being too reliable is wasteful. Don't fixate on nines — use data-driven targets at whatever percentage makes sense. Dependencies constrain your ceiling (R^N). Use historical data + basic statistics (mean, median, percentiles) to choose initial targets. Handle metric limitations (resolution, quantity, quality) by adjusting windows or using sustained-violation rules. Percentile thresholds give better visibility than simple percentage targets for long-tail distributions. If you have no history: guess, commit, iterate.

**Next: Chapter 5 — How to Use Error Budgets, the most advanced and impactful part of the Reliability Stack.**
