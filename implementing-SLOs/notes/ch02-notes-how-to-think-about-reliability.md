# Chapter 2: How to Think About Reliability

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Reliability Engineering, Implied Agreements, Why 100% Is Impossible and Unnecessary, and the True Cost of Perfection*

This chapter establishes the *mindset* that must precede any SLO implementation. Hidalgo argues that reliability is broader than availability, that it's a concept as old as engineering itself (not a tech invention), that users determine reliability through their experience, and that the cost of approaching perfection grows non-linearly. He walks through a detailed video streaming example that shows how many dimensions reliability actually encompasses, and closes with the uncomfortable truth: there is no single answer to "how reliable should you be?" — only ongoing conversations informed by data.

## Table of Contents

- [Reliability Engineering Is Not New](#reliability-engineering-is-not-new)
- [Past Performance and Implied Agreements](#past-performance-and-implied-agreements)
  - [Hyrum's Law and Unexpected Requirements](#hyrums-law-and-unexpected-requirements)
- [A Worked Example: Video Streaming Reliability](#a-worked-example-video-streaming-reliability)
- [Why 100% Is Impossible and Unnecessary](#why-100-is-impossible-and-unnecessary)
- [Reliability Is Expensive — The Non-Linear Cost Curve](#reliability-is-expensive--the-non-linear-cost-curve)
- [How to Think About Reliability](#how-to-think-about-reliability)

**Block types:** [Core Concept] [Worked Example] [Common Pitfall] [Math Explained] [Senior EM Application] [2025 Update] [AI & Observability] [Organizational Reality]

---

## Reliability Engineering Is Not New

Hidalgo opens by warning against tech-industry solipsism. Terms like "reliability engineering," "complex systems," and "resilience engineering" are not inventions of the software world — they are **decades-old disciplines** studied across mechanical engineering, aerospace, civil engineering, and safety science. Bridges don't collapse because reliability engineering exists. The tech industry has partially adopted these terms without always bringing their full rigor.

> *"Using an SLO-based approach to service reliability is just one step in turning software engineering into a true engineering discipline."*

The key takeaway: SLOs are not just a monitoring technique. They are a **reliability engineering methodology** that gives you data to make systems more reliable — one tool among many (alongside resilience engineering, safety engineering, chaos engineering, etc.).

> **[Core Concept: SLOs Are a Data Tool, Not a Solution]**
>
> Hidalgo is careful to set expectations: SLOs don't *make* your system reliable. They provide *data* that helps you have better discussions and make better decisions about reliability. The actual improvements come from engineering work informed by that data — architecture changes, automation, redundancy, testing, capacity planning.
>
> Think of SLOs like a blood pressure monitor: it doesn't lower your blood pressure, but knowing your numbers enables the doctor (and you) to make informed treatment decisions. Without measurement, you're guessing.

---

## Past Performance and Implied Agreements

Hidalgo introduces a crucial concept: **your service has already made reliability promises to its users, even if you've never written an SLO or SLA.**

> *"When a service has been operating at a certain level for a certain amount of time, your users will see this as an agreement with them — it won't matter if you're lacking documentation or a contract stating as much."*

If your service has been running at 99.95% availability for two years, your users *expect* that level going forward. Their planning, their SLOs (if they have them), and their user experience are all calibrated to your historical behavior. This is an *implied agreement* whether you intended it or not.

**This doesn't mean you're locked in.** Your current state may not be what you *should* strive for. But you must acknowledge the implied baseline when setting formal SLOs — departing dramatically from what users have come to expect requires communication.

Hidalgo also emphasizes: **don't hide your SLOs from users.** Transparency lets them plan around your targets, voice concerns, and set their own reliability targets based on yours (critical for dependency chains).

### Hyrum's Law and Unexpected Requirements

Hidalgo introduces Hyrum's Law (coined by Google engineer Hyrum Wright):

> *"With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviors of your system will be depended on by somebody."*

This means your users may depend on reliability dimensions you never imagined. They might rely on the *exact order* of items in a response, the *specific timing* of a notification, or the *format* of an error message — none of which you intended to guarantee. As you develop SLIs, expect to discover reliability requirements you didn't know existed.

> **[Common Pitfall: Ignoring Implied Agreements]**
>
> **The scenario:** Your service has been running at 99.99% availability for 3 years (because you over-provisioned, not because you targeted it). You formally adopt SLOs and set a target of 99.9% — a rational target that gives you 10x more error budget for development velocity.
>
> **The problem:** Users have calibrated to 99.99%. Downstream services have set *their* SLOs assuming your 99.99% baseline. When you "relax" to 99.9%, it feels like a degradation to them — even though 99.9% is still excellent.
>
> **The fix:** Communicate proactively. Share your formal SLO with dependent teams. If you've been over-performing, acknowledge this: "Our formal target is 99.9%. We have historically exceeded this, but we do not commit to maintaining 99.99% — please plan accordingly." This is what Hidalgo means by making SLOs discoverable and transparent.

---

## A Worked Example: Video Streaming Reliability

Hidalgo walks through a video streaming service to show how many *dimensions* of reliability exist for even a single service. This is one of the book's most valuable teaching sections because it demolishes the myth that reliability = availability.

**Dimensions of reliability for a video streaming service:**

| Dimension | What "Reliable" Means | Failure Mode |
|-----------|----------------------|-------------|
| **Stream playback** | When you press play, the video actually plays | Total playback failure |
| **Start latency** | Buffering at the beginning is acceptable but bounded | Excessive initial buffer time |
| **Mid-stream continuity** | No buffering interruptions during playback | Buffering mid-video (worse than at start) |
| **Content correctness** | You get the movie you selected, not a different one | Wrong content delivered |
| **Video quality** | Acceptable resolution (varies by subscription tier) | Degraded resolution |
| **Audio presence** | Sound is present and synced to video | Missing or desynced audio |
| **Subtitle correctness** | If needed: present, synced, correct language, readable | Wrong language, desynced, or missing subtitles |
| **Search relevance** | Relevant results for queries | Irrelevant search results |
| **Queue persistence** | Items added to your queue stay there | Queue items disappearing |
| **Content metadata** | Preview text matches the selected movie | Wrong descriptions |
| **Auto-play behavior** | Next episode plays correctly, settings are honored | Wrong next episode, settings ignored |
| **Content filtering** | Kids profile shows only appropriate content | Adult content on kids profile |
| **Billing correctness** | Correct amount, correct timing, package persists | Overcharging, incorrect plan |

Hidalgo's point: *"I could go on and on and on. I've barely scratched the surface."* Reliability is not a single metric — it's a multidimensional space, and different users weight different dimensions differently.

> **[Senior EM Application: The Multidimensional Audit for Your Service]**
>
> Before setting SLIs, conduct this exercise with your team:
>
> 1. **List every way your service can fail from a user's perspective** (not server perspective). Not "the database connection pool fills up" but "the user can't load their dashboard."
> 2. **Group failures by dimension**: availability, latency, correctness, freshness, durability, etc.
> 3. **Rank by user impact**: which failures would cause users to churn vs. shrug?
> 4. **Identify current measurement gaps**: which dimensions do you measure today? Which are blind spots?
>
> The video streaming example shows why a single "availability" SLO is insufficient for any complex service. You likely need 2-5 SLIs covering different reliability dimensions. Chapter 3 covers how to develop these.

---

## Why 100% Is Impossible and Unnecessary

Hidalgo makes the case through everyday analogies:

| Analogy | Imperfection | Why Users Accept It |
|---------|-------------|-------------------|
| **Car starting** | Doesn't always start on the first attempt | As long as it starts on the second try, nobody buys a new car |
| **Watch accuracy** | Loses a minute every few months | Easily corrected; user adapts |
| **Pizza delivery** | Wrong topping occasionally | Still edible; acceptable if rare |
| **Pizza latency** | Usually 30-40 min, occasionally an hour | 90% on time is good enough for loyal customers |

The point: users are *already* accustomed to imperfection in every domain. Software doesn't need to be held to a higher standard than the physical world.

> *"Nothing is ever 100% perfect 100% of the time. We can even get pedantic and point to the problem of induction: even if something has been 100% reliable since time immemorial, you really have no logical case to make that it will continue to be so."*

---

## Reliability Is Expensive — The Non-Linear Cost Curve

Hidalgo explains why the cost of reliability grows non-linearly:

**Financial costs:**
- Distributed architecture (multi-region, redundancy)
- Testing infrastructure (QA teams, staging environments, canary systems)
- Monitoring and observability stack
- Each additional "nine" requires more infrastructure, more complexity, more people

**Human costs:**
- At 99.99% (4.3 minutes/month downtime): on-call must respond in *seconds*
- Engineers need to be within arm's reach of a laptop at all times during shifts
- No movies, no dog walks, no being away from the computer
- Requires globally distributed follow-the-sun rotations = many employees

**The math that makes it visceral:**

> **[Math Explained: The Non-Linear Cost of Nines]**
>
> Moving from 99.9% → 99.95% seems similar to moving from 99.95% → 99.99%. But the math shows otherwise:
>
> | Transition | Unreliability Change | Factor of Improvement | Monthly Downtime Reduction |
> |-----------|--------------------|-----------------------|---------------------------|
> | 99.9% → 99.95% | 0.1% → 0.05% | **2x** improvement | 43 min → 21 min (save 22 min) |
> | 99.95% → 99.99% | 0.05% → 0.01% | **5x** improvement | 21 min → 4.3 min (save 17 min) |
> | 99.99% → 99.999% | 0.01% → 0.001% | **10x** improvement | 4.3 min → 26 sec (save 4 min) |
>
> Each additional nine requires *multiplicatively* more effort than the last. Going from 99.95% to 99.99% is 2.5x harder than going from 99.9% to 99.95% — and the absolute time saved (17 min vs 22 min) is actually *less*.
>
> **The question for every SLO target:** "Is the marginal cost of the next nine worth the marginal benefit to our users?" For most services, the answer becomes "no" well before 99.99%.

> **[Senior EM Application: Using Cost-of-Nines in Budget Conversations]**
>
> When leadership asks "why aren't we at 99.99%?" — this math is your answer:
>
> ```
> Current state: 99.9% (43 min/month downtime)
> Cost to maintain: $X infrastructure + Y engineers on-call with 30-min response SLA
>
> To reach 99.99% (4.3 min/month downtime):
> - Multi-region active-active (2x infra cost)
> - Auto-remediation for top 5 failure modes (2 engineer-quarters)
> - Follow-the-sun on-call with <60 second response (3x on-call headcount)
> - Estimated additional cost: $Z/year
>
> Benefit: 38.7 fewer minutes of downtime per month
> Question: Is 38.7 minutes of monthly downtime actually causing user churn
> or revenue loss that exceeds $Z?
> ```
>
> Often the answer is no — and the investment is better spent on feature development that *adds* reliability dimensions users care about (correctness, freshness, new capabilities) rather than chasing the next nine of availability.

---

## How to Think About Reliability

Hidalgo closes honestly: there's no single formula.

> *"SLOs are meant to be changing things that can be adapted to your current reality and your current situation. There will be times when it is true that you should hold fast and enforce your error budget strongly. There will be other times where you experience a black swan event and have to temporarily ignore what the numbers tell you."*

The answer to "how reliable should you be?" is always: **it depends, and it will change.**

What SLOs give you is not the answer — they give you **a structured way to have the conversation.** Better data → better discussions → better decisions. That's the entire value proposition.

> **[2025 Update: Reliability as Competitive Differentiator]**
>
> Since Hidalgo wrote in 2020, several trends have raised the stakes of reliability:
>
> - **AI workloads** demand different reliability dimensions — not just "is the API up?" but "are the model responses accurate and timely?" LLM-powered features introduce new failure modes: hallucinations, latency variance, context window exhaustion.
> - **Platform consolidation** — as companies consolidate onto fewer platforms (Kubernetes, major cloud providers), individual service reliability becomes more dependent on platform reliability. Hidalgo's point about "you can only be as reliable as your dependencies" has intensified.
> - **User expectations have risen** — with the maturation of cloud-native architecture, users expect higher baseline reliability. What was "good enough" in 2020 may not be in 2025.
> - **Regulation** — EU Digital Services Act, FedRAMP, SOC2 increasingly require *demonstrated* reliability targets with evidence. SLOs are becoming compliance artifacts, not just engineering tools.

> **[AI & Observability: AI and the New Dimensions of Reliability]**
>
> Hidalgo's video streaming example identified ~15 reliability dimensions for a traditional service. AI-powered services add new ones:
>
> | New Dimension | What "Reliable" Means | Failure Mode |
> |--------------|----------------------|-------------|
> | **Response accuracy** | AI provides factually correct answers | Hallucinations, outdated information |
> | **Response consistency** | Same input produces semantically consistent output | Non-deterministic responses confuse users |
> | **Response completeness** | AI doesn't cut off mid-response | Token limit exceeded, timeout |
> | **Bias/fairness** | AI doesn't produce biased or harmful content | Discriminatory outputs |
> | **Latency variance** | Response time is predictable | Some prompts take 200ms, others take 30s — unpredictable |
>
> Traditional SLIs (availability, latency) still apply but are insufficient for AI services. The "correctness" dimension — which Hidalgo mentions for the video streaming case — becomes the *dominant* concern. This is an active area of development in the SLO community; tools like LangSmith and Arize are building SLI-like measurements for LLM quality.

---

**Chapter 2 establishes:** Reliability is broader than availability. Your users have already formed implied agreements about your reliability level. Use Hyrum's Law to anticipate unexpected requirements. 100% is impossible, unnecessary, and non-linearly expensive to approach. The right reliability level depends on context and will change over time. SLOs provide data for the conversation, not the answer itself.

**Next: Chapter 3 — Developing Meaningful Service Level Indicators, where Hidalgo gets practical about how to measure reliability from the user's perspective.**
