# Chapter 13: Performance Appraisal — Part 1

> **High Output Management** — Andrew S. Grove
> *Why Performance Reviews Are the Highest-Leverage Feedback, and How to Assess Performance*

This is the longest and most detailed chapter in Part IV. Grove treats performance reviews as the *"single most important form of task-relevant feedback"* a supervisor can provide — and therefore one of the highest-leverage activities in a manager's repertoire. A few hours of preparation and delivery can redirect someone's work for an entire year (or longer). Yet most managers do it poorly, and most subordinates dread it. Grove addresses both the assessment and the delivery, providing a level of practical detail unmatched by most management books.

Part 1 covers why reviews matter, how to assess performance, and the traps to avoid. Part 2 covers delivering the assessment and the three types of reviews.

## Table of Contents

- [Why Bother with Performance Reviews?](#why-bother-with-performance-reviews)
- [Assessing Performance](#assessing-performance)
  - [Output Measures vs. Internal Measures](#output-measures-vs-internal-measures)
  - [Long-Term vs. Short-Term](#long-term-vs-short-term)
  - [The Time Offset Problem](#the-time-offset-problem)
  - [Assessing Managers: Performance, Not Potential](#assessing-managers-performance-not-potential)
  - [The Potential Trap](#the-potential-trap)
  - [Promotions as Values Signals](#promotions-as-values-signals)
  - [Always Find Room for Improvement](#always-find-room-for-improvement)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Anti-Pattern] [Practical Toolkit] [Scenario] [Mental Model]

---

## Why Bother with Performance Reviews?

Grove asked middle managers three questions about reviews and got revealing answers:

**Why do we do reviews?** To assess work, improve performance, motivate, provide feedback, justify raises, reward performance, provide discipline, give direction, reinforce culture.

**What feelings do supervisors have giving reviews?** Pride, anger, anxiety, discomfort, guilt, empathy, embarrassment, frustration.

**What was wrong with reviews you received?** Comments too general, mixed messages, no indication of how to improve, negatives avoided, supervisor didn't know my work, only recent performance considered, surprises.

Grove's conclusion: *"This should tell you that giving performance reviews is a very complicated and difficult business and that we, managers, don't do an especially good job at it."*

**The fundamental purpose:** not all the things on the list above, but one thing above all others: *"to improve the subordinate's performance."* This happens through addressing two dimensions:
1. **Skill level** — what skills are missing and how to develop them (can't)
2. **Motivation** — how to move the person to a higher performance curve at the same skill level (won't)

> *"The review is an extremely powerful mechanism... it is one of the manager's highest-leverage activities."*

> **[Core Concept: Performance Review as Highest-Leverage Feedback]**
>
> Grove frames the review through his leverage lens: a few hours of preparation and delivery affect a subordinate's work for an *entire review period* (6-12 months) — potentially changing their trajectory. This leverage can be positive (redirecting effort, building motivation, developing skills) or negative (demoralizing, confusing, creating resentment). There is no neutral review.
>
> Grove also notes that this is *"the most formal type of institutionalized leadership"* — the only time a manager is *mandated* to be judge and jury. Our society and cultural training actively work against this (we're taught to avoid confrontation, skirt emotional issues). Which is why it's so hard and so often done poorly.

> **[SRE Lens: Performance Reviews for SRE Engineers]**
>
> SRE work creates unique performance review challenges:
>
> | Challenge | Why It's Hard | Grove's Framework Applied |
> |-----------|-------------|------------------------|
> | **Measuring incident response quality** | Output is "absence of bad things" — hard to quantify | Use internal measures: response time, communication quality, postmortem depth, systemic fixes implemented |
> | **Crediting reliability work** | The best reliability engineering is invisible (the incident that *didn't* happen) | Weight internal measures (preventive work, architecture improvements) alongside output measures (SLO compliance) |
> | **Evaluating on-call performance** | Some rotations are quiet, some are brutal — luck factor | Assess process quality, not just outcome. Did they follow runbooks? Communicate clearly? Escalate appropriately? |
> | **Toil vs. project balance** | Engineer spent 60% on toil — was that productive or a failure? | Assess whether they took steps to *reduce* toil, not just whether they performed it. Output: reduced toil % over time. |
> | **Cross-team influence** | SRE's impact often shows up in *other* teams' output (better reliability, faster deployments) | Use Grove's "neighboring organizations under influence" — include cross-team impact in the review |

---

## Assessing Performance

### Output Measures vs. Internal Measures

Grove applies the black box model: measure both the **output** (what came out of the box — designs completed, sales quotas met, production yields improved) and the **internal measures** (what's happening inside the box that will affect *future* output — are we developing people? maintaining morale? building sustainable practices?).

No fixed formula for weighting: it could be 50/50, 90/10, or 10/90 depending on the situation. But you must know which two variables you're trading off.

> **[Practical Toolkit: Output vs. Internal Measures for SRE Reviews]**
>
> | Output Measures (What Came Out) | Internal Measures (What's Happening Inside) |
> |-------------------------------|-------------------------------------------|
> | SLO compliance over the review period | Quality of monitoring and alerting built (enables future output) |
> | Incidents resolved and MTTR achieved | Postmortem action items completed (reduces future incidents) |
> | Toil reduction achieved (quantified) | Runbooks written or improved (enables future on-call) |
> | Projects delivered on time | Cross-training provided to teammates (reduces bus factor) |
> | Reliability improvements shipped | Relationships built with product teams (enables future influence) |
>
> A review that only looks at output is like Grove's "light from distant stars" — it reflects past investment, not current performance. A review that only looks at internal measures ignores whether the work actually produced results. Both dimensions matter.

### Long-Term vs. Short-Term

An engineer may be completing projects on schedule (short-term output) while *also* developing a design method that will benefit future work (long-term investment). Both must be evaluated. Grove suggests using "present value" thinking from finance: what will the long-term investment pay back over time?

### The Time Offset Problem

This is one of the chapter's most important warnings. Grove tells a personal story:

A manager reporting to him had a superb year — all output measures excellent. But turnover was rising and people were grumbling. Grove gave a strong positive review anyway, trusting the output numbers over the "elusive signs."

The next year: *"his organization took a nose dive. Sales growth disappeared, profitability declined, product development was delayed, and the turmoil among his subordinates deepened."*

What happened? The manager's performance had actually been *declining* during the "good year." The excellent output numbers were *"the light from distant stars"* — reflecting work done years earlier, still coasting. The internal measures (turnover, morale) were the real signal.

> *"Greatly embarrassed, I regretfully concluded that the superior rating I had given him was totally wrong. Trusting the internal measures, I should have had the judgment and courage to give the manager a much lower rating."*

It can also work the other way: an engineer building a factory from scratch has no output yet. Grove gave credit for strong internal measures even though tangible output was uncertain.

> *"We are really called upon to* judge *performance, not just to see and record it when it's in plain sight."*

> **[Anti-Pattern: The "Light from Distant Stars" Trap in SRE]**
>
> This pattern appears frequently in SRE management:
>
> - **The SRE manager whose services are stable... because of their predecessor's architecture decisions.** The current manager is coasting on inherited quality while making decisions that will cause problems in 12 months (deferring upgrades, underinvesting in monitoring, not cross-training). Output measures look great; internal measures are degrading.
>
> - **The SRE manager whose services are unstable... because they inherited technical debt.** The current manager is making excellent architectural decisions and building strong processes, but the output (incident rate, SLO compliance) still reflects the inherited mess. Output measures look bad; internal measures are improving.
>
> Grove's lesson: **you must have the judgment and courage to look past output numbers and assess the actual performance trajectory.** For SRE, this means evaluating: "Given what this person inherited, are things getting better or worse? Are the leading indicators (architecture quality, team health, process maturity) improving even if lagging indicators (incident rate, SLO) haven't caught up yet?"

### Assessing Managers: Performance, Not Potential

When reviewing a manager, assess *both* their individual performance and their organization's output. But remember:

> *"The performance rating of a manager cannot be higher than the one we would accord to his organization!"*

Grove gives a sharp example: a general manager whose unit lost money and missed targets was given a high rating by his supervisor because "he is an outstanding general manager... handles himself well." Grove rejected this:

> *"Had the manager been given a high rating, Intel would have signaled to all at the company that to do well, you must 'act' like a good manager, talk like one, and emulate one — but you don't need to perform like one."*

### The Potential Trap

> *"One big pitfall to be avoided is the 'potential trap.' At all times you should force yourself to assess performance, not potential. By 'potential' I mean form rather than substance."*

This is the distinction between *what someone does* (performance) and *what someone seems capable of* (potential). Only performance matters for the review. Potential is relevant for career development conversations, but the review must be grounded in demonstrated output.

> **[Senior EM Application: The "Potential Trap" for Senior Engineers]**
>
> The potential trap is especially seductive when reviewing senior/staff engineers:
>
> - The architect who writes brilliant design docs but whose designs are never implemented → high potential, low output
> - The engineer who gives great presentations but whose projects consistently slip → high potential, low output
> - The "thought leader" who influences Slack discussions but doesn't ship → high potential, low output
>
> In each case, the temptation is to rate them highly because they *seem* capable. Grove says: judge what they *produced*, not what they *could* produce.

### Promotions as Values Signals

> *"No action communicates a manager's values to an organization more clearly and loudly than his choice of whom he promotes."*

Grove addresses the "promote our best salesman and get a bad manager" dilemma: you still promote the best performer, because the alternative (promoting someone less competent) signals that performance doesn't matter.

### Always Find Room for Improvement

> *"No matter how stellar a person's performance level is, there is* always *room for improvement."*

Use 20/20 hindsight: compare what was done against what *could* have been done. The variance tells both of you how to do better. This applies especially to top performers (more on this in Part 2).

---

**Part 1 covered:** Why reviews are the highest-leverage feedback, how to assess performance (output + internal measures, time offsets, the "light from distant stars" problem), and traps to avoid (potential trap, form over substance).

**Part 2 covers:** Delivering the assessment (three L's — level, listen, leave yourself out), the three types of reviews (mixed, blast, ace), the five stages of problem-resolution, and practical mechanics (written vs. verbal, self-reviews, timing).
