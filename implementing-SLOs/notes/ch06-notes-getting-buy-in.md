# Chapter 6: Getting Buy-In

> **Implementing Service Level Objectives** — David K. Rensin
> *Convincing Engineering, Product, Operations, Leadership, Legal, and QA to Adopt SLOs*

This is the most *organizationally* important chapter in the book. Written by David K. Rensin (who helped numerous organizations adopt SLOs at Google Cloud), it's a tactical playbook for the political and persuasive work required to make SLOs stick. The technical implementation is irrelevant if your organization won't commit to living by the data. Rensin provides stakeholder-by-stakeholder arguments, a specific order of operations for building consensus, scripts for overcoming common objections, and hard-won lessons about the critical first test of the error budget policy.

## Table of Contents

- [Engineering Is More Than Code](#engineering-is-more-than-code)
- [Key Stakeholders and Their Concerns](#key-stakeholders-and-their-concerns)
  - [Engineering](#engineering)
  - [Product](#product)
  - [Operations](#operations)
  - [QA](#qa)
  - [Legal](#legal)
  - [Executive Leadership](#executive-leadership)
- [The Order of Operations](#the-order-of-operations)
- [Common Objections and Responses](#common-objections-and-responses)
- [Your First Error Budget Policy](#your-first-error-budget-policy)
  - [The Feature Freeze Policy](#the-feature-freeze-policy)
  - [Handling "But We MUST Ship by $DATE"](#handling-but-we-must-ship-by-date)
- [The First Test — The Most Critical Moment](#the-first-test--the-most-critical-moment)
- [Lessons Learned the Hard Way](#lessons-learned-the-hard-way)

**Block types:** [Core Concept] [Organizational Reality] [Implementation Guide] [Common Pitfall] [Senior EM Application] [Template] [2025 Update]

---

## Engineering Is More Than Code

Rensin frames the challenge: SLOs require *convincing people*, not just writing code. For some stakeholders, SLOs run counter to their goals. Others will doubt the organization is "mature enough." All objections can be overcome — but it requires patient explanation and strategic sequencing.

---

## Key Stakeholders and Their Concerns

### Engineering

**Their concern:** "The ops team will never give us free rein."

**What SLOs offer them:**
- More freedom to deploy when budget is healthy (less bureaucratic friction)
- More permission to take risks and experiment
- A real feedback loop from users (via error budget data)
- Increased feature velocity over time

### Product

**Their concern:** Shipping features as quickly as possible.

**What SLOs offer them:**
- Faster feature velocity (once friction between eng/ops is resolved)
- Data to turn the reliability-vs-features knob *with data instead of luck*
- User journeys map directly to SLIs — alignment between PRD and measurement
- If you're over-performing on reliability, you're *wasting effort* that could go to features

### Operations

**Their concern:** Getting paged at 3 AM for someone else's mistakes.

**What SLOs offer them:**
- Equal voice when engineering pushes bad code (error budget policy has teeth)
- Engineers now have skin in the game regarding stability
- Permission to remove accumulated deployment friction (because engineers accept consequences)
- The "even footing" they've always wanted

> *"I have never met an operations team that wasn't immediately enthusiastic about the idea of SLOs and error budgets."*

### QA

**Their concern:** "What happens to us?"

The uncomfortable truth: dedicated QA teams tend to get reorganized as SLOs mature. Not because QA *skills* become less valuable — they become *more* valuable. But the *organizational structure* of a separate QA team often gets absorbed into feature engineering teams.

Rensin describes the progression: engineers bypass QA → exhaust error budget → are forced to build testing → slowly rebuild QA practices within their teams → QA skills become embedded, not separate.

### Legal

**Their concern:** Business risk and SLA exposure.

**What SLOs offer them:**
- Better data to inform SLAs (currently correct only by luck)
- Proactive alerting before SLA violations (they prepare before customer claims)
- Potential competitive advantage (if you reliably exceed competitors, you can offer tighter SLAs)
- For regulated industries: demonstrates risk awareness and controls to regulators

### Executive Leadership

**Their concern:** "We strive for 100%!"

Rensin's simplified argument:
1. We have never been 100% reliable. Never.
2. No human-made system has. Ever.
3. Goals of perfection incentivize lying (people fudge numbers) or paralysis (people are scared to act)
4. We should stop trying to make *no mistakes* and start *noticing mistakes faster and limiting impact*
5. As we get better at that, we can take more risks → faster innovation → better customer experience

> *"The overwhelming majority of CEOs, CTOs, CIOs, and VPs to whom I have presented these points wind up agreeing."*

---

## The Order of Operations

Rensin is very specific about sequencing:

| Step | Who | Why This Order |
|------|-----|---------------|
| **1** | Engineering + Operations | They benefit most directly. Their agreement is prerequisite for all other conversations. |
| **2** | Product | They need to know eng+ops are aligned. Their buy-in provides the "big three" agreement. |
| **3** | Leadership | They need to see that the key functional teams agree. They provide organizational authority. |
| **4** | Legal | Low resistance once steps 1-3 are done. They get proactive risk data. |
| **5** | QA | Consumers of the decision, not decision-makers. Inform them, don't ask permission. |

> **[Senior EM Application: You Are the Person Driving This]**
>
> Rensin addresses the chapter to "the person driving your team/organization/company toward adoption." As a Senior EM in SRE, **that person is you.** This chapter is your playbook.
>
> Key tactical advice:
> - **Don't start with leadership.** Start with your peers (other EMs in engineering and ops). Build bottom-up consensus first.
> - **Get engineering excited first** by emphasizing freedom and velocity
> - **Get ops excited** by emphasizing accountability and fairness
> - **Then go to product** with both teams already aligned — product loves consensus
> - **Then go to your Director/VP** with eng+ops+product all saying yes
> - **Never go to leadership cold.** If the CEO hears about SLOs for the first time from you without pre-alignment, you'll get skepticism. If they hear it after all their reports already agree, it's a formality.

---

## Common Objections and Responses

> **[Template: The Objection-Response Script]**
>
> | Objection | From | Response |
> |-----------|------|----------|
> | "The ops team will never go for this" | Engineering | "I've already talked to them. They're thrilled. Are you on board IF they agree?" |
> | "Engineers will never accept consequences" | Operations | "They already agreed. If they don't blow budgets, your pagers don't go off. If they do, you influence their work. It's strictly better than today." |
> | "This sounds like a lot of work" | Leadership | "It is — but we'll move much faster afterward. And if we try and it doesn't work, it's cheap to go back." |
> | "We strive for 100%!" | Leadership | "We have never achieved it. Goals of perfection incentivize lying or paralysis. Let's aim for a target our users actually need." |
> | "We're not Google" | Anyone | "This isn't unique to Google. Small teams and startups use it too. It's arithmetic and discipline, not rocket science." |
> | "We're not smart enough" | Anyone | *"You can read. You can count. You can create and stick to a simple plan. You can do this."* |
> | "What happens to our SLAs?" | Legal | "No change needed if you're not already paying violations. Plus you'll get early warning before violations happen." |
> | "What happens to us?" | QA | "Your skills become MORE valuable. The org structure may change, but QA expertise becomes embedded in every team." |

---

## Your First Error Budget Policy

### The Feature Freeze Policy

Rensin's strong recommendation: **for the first year, have exactly one error budget policy, and make it a feature freeze.**

> *"Suppose you have all agreed that your service should have an availability SLO of 99.9%. That means you have an error budget of 43.2 minutes every 30 days."*

When a 60-minute outage exhausts 1.39x the budget, the team enters a 12-day feature freeze. During the freeze, only reliability improvements ship — driven by the operations team's priorities (better monitoring, faster rollback, slower rollouts, canaries).

### Handling "But We MUST Ship by $DATE"

Two approaches:

**Silver bullets:** Give product leadership 3 per year to break out of a freeze. (Rensin doesn't love this — no feedback loop, and what if you need more than 3?)

**Thaw tax (Rensin's preference):** For every day you break the freeze, add 1.5x days to the remaining freeze. Want to unfreeze for 2 days? Pay 3 days added to the freeze. This makes leaders think *carefully* before requesting an exemption.

---

## The First Test — The Most Critical Moment

> *"The most important moment is the first time you exhaust your error budget and need to enforce your policy."*

This is the make-or-break moment for the entire SLO program:

> *"Unless you legitimately think that following through would risk putting your company out of business, the most vital thing you can do is follow your policy strictly the first time it is invoked."*

If leadership caves ("let's make an exception this one time"), the organization learns that the policy isn't real. Every future invocation will be fought. Trust collapses.

If leadership holds firm, the organization learns that SLOs have teeth. Future enforcement becomes routine.

> **[Organizational Reality: Why the First Test Defines Everything]**
>
> This is the Rubicon of SLO adoption. Rensin is unequivocal: if you don't enforce the first time, you probably never will. The psychological dynamic:
>
> - **Before enforcement:** Everyone agrees to the policy in theory (it sounds reasonable in a calm meeting)
> - **First budget exhaustion:** A real feature deadline is at stake. Product is panicking. A VP is asking "can't we just...?"
> - **If you enforce:** The organization learns: "This is real. Error budget data drives decisions. We're serious." Future enforcement is easier because precedent exists.
> - **If you don't enforce:** The organization learns: "This is theater. The policy is optional. When it's inconvenient, we ignore it." No one takes SLOs seriously again.
>
> **For Senior EMs:** This is why the pre-agreement in steps 1-5 matters so much. You need your Director/VP to have explicitly committed to enforcement *before* the moment arrives. When the first budget burns, you can point to their prior commitment: "We agreed that this would happen. I know it's uncomfortable, but this is exactly the scenario we discussed."

---

## Lessons Learned the Hard Way

Rensin's distilled wisdom:

| Lesson | What It Means |
|--------|--------------|
| **Too much too soon** | Don't try to SLO-ify everything at once. Start with one failure domain, one service, one team. |
| **Less is more** | Few SLIs, few SLOs, one error budget policy. Add more later. |
| **Review early/review often** | Reevaluate targets monthly or quarterly at first. Move to yearly once stable. |
| **Be completely transparent** | Dashboards visible to anyone. Include SLI, SLO, error budget status, AND release velocity. Show the positive trend over time. |

> **[2025 Update: SLO Buy-In Has Gotten Easier (and Harder)]**
>
> **Easier because:**
> - SRE as a discipline is well-known — you don't need to explain the concept from scratch
> - Leadership has likely heard of SLOs from other companies, conferences, or vendors
> - Tooling makes implementation much faster (Datadog SLOs in minutes, not months)
> - The "we're not Google" objection has weakened as SLOs have become mainstream
>
> **Harder because:**
> - "SLO" has become a buzzword — some leadership thinks they "already have SLOs" (they have SLAs labeled as SLOs)
> - Vendor tool adoption creates false confidence ("we bought Nobl9, so we have SLOs now" — without the cultural change)
> - AI hype diverts attention ("let's focus on AI features" → reliability deprioritized)
> - Remote/hybrid work makes the consensus-building meetings harder to orchestrate
>
> Rensin's advice remains fully applicable: the challenge was never primarily technical. It was always about people, incentives, and organizational commitment.

---

**Chapter 6 establishes:** SLO adoption is primarily an organizational challenge, not a technical one. Convince stakeholders in the right order (eng→ops→product→leadership→legal→QA). Each group has specific concerns and specific benefits. Use a simple feature freeze as your first error budget policy. The first enforcement is the most critical moment — hold firm or lose credibility permanently.

**Next: Chapter 7 — Measuring SLIs and SLOs (Ben Sigelman), covering the technical practicalities of actually implementing SLI measurement.**
