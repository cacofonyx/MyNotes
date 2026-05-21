# Chapter 13: Performance Appraisal — Part 2

> **High Output Management** — Andrew S. Grove
> *Delivering the Assessment: Three L's, Three Types of Reviews, and the Five Stages*

Part 1 covered assessment. Part 2 covers the delivery — the actual conversation. Grove provides the "three L's" framework, walks through three types of reviews (mixed, blast, ace), and gives detailed guidance on the five stages of problem-resolution that play out when a subordinate faces difficult feedback.

## Table of Contents

- [Delivering the Assessment: Three L's](#delivering-the-assessment-three-ls)
  - [Level](#level)
  - [Listen](#listen)
  - [Leave Yourself Out](#leave-yourself-out)
- [Three Types of Reviews](#three-types-of-reviews)
  - [The Mixed Review ("On the One Hand...")](#the-mixed-review-on-the-one-hand)
  - [The Blast (Major Performance Problem)](#the-blast-major-performance-problem)
  - [Reviewing the Ace](#reviewing-the-ace)
- [The Five Stages of Problem-Resolution](#the-five-stages-of-problem-resolution)
- [Practical Mechanics](#practical-mechanics)
- [Acceptable vs. Desirable Outcomes](#acceptable-vs-desirable-outcomes)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Practical Toolkit] [Anti-Pattern] [Scenario] [Mental Model]

---

## Delivering the Assessment: Three L's

### Level

*"You must level with your subordinate — the credibility and integrity of the entire system depend on your being totally frank."*

Grove notes that **praising** frankly can be as hard as criticizing — managers often understate positive feedback just as they soften negative feedback.

### Listen

Grove redefines "listening" for performance reviews: it doesn't mean just hearing words. It means using *all sensory capabilities* to verify that your message is actually being received.

> *"Does your subordinate give appropriate responses to what you are saying? Does he allow himself to receive your message? If his responses — verbal and nonverbal — do not completely assure you that what you've said has gotten through, it is* your responsibility *to keep at it until you are satisfied that you have been heard and understood."*

The subordinate may be too emotional to process, too busy formulating rebuttals to hear, or mentally checked out as a defense mechanism. The supervisor must watch for all of these and adjust.

> *"Don't imitate your worst professors while delivering performance reviews."* — professors who lecture to the blackboard, avoiding eye contact to avoid seeing confusion they don't want to deal with.

### Leave Yourself Out

> *"The performance review is about and for your subordinate. So your own insecurities, anxieties, guilt, or whatever should be kept out of it."*

The supervisor's emotions — guilt about not providing enough support during the year, anxiety about the subordinate's reaction, discomfort with confrontation — must be controlled. This is the subordinate's "day in court," not the supervisor's therapy session.

---

## Three Types of Reviews

### The Mixed Review ("On the One Hand...")

Most reviews contain both positive and negative assessments. The main pitfalls: superficiality, clichés, laundry lists of unrelated observations.

**The finite capacity principle:**

> *"Your subordinate has only a* finite capacity *to deal with facts, issues, and suggestions. You may possess seven truths about his performance, but if his capacity is only four, at best you'll waste your breath on the other three."*

**The worksheet method:**

1. Consider as many aspects as possible — scan progress reports, quarterly objectives, 1-1 notes
2. Write everything on a blank sheet — major, minor, trivial, no editing, no order
3. Put supporting documentation away
4. Look for relationships between items — different manifestations of the same phenomenon
5. Group related items into **messages** (2-3 themes, not 7 disconnected points)
6. Ask: can my subordinate *remember* all these messages? If not, delete the less important ones

> **[Practical Toolkit: The Review Worksheet in Practice]**
>
> Grove shows an example worksheet:
>
> **Positives:** planning process improved (quick start), good report to Materials Council, helped on Purchasing cost analysis
>
> **Negatives:** spec process zero, meetings are "all mushy," poor kick-off for spec training
>
> **Messages distilled:**
> 1. Good results on planning system (analytical background useful)
> 2. Hard time setting clear, crisp goals — satisfied with activities instead of driving results!
> 3. ~~(No — let's just concentrate on #2!)~~
>
> Notice: Grove *crosses out* message 3 to stay within the subordinate's absorption capacity. Two clear messages are better than three fuzzy ones.
>
> **For SRE reviews, the message distillation might look like:**
>
> Raw observations: good incident response, slow postmortem completion, excellent dashboard design, poor documentation, strong Slack communication, weak written RFC skills
>
> Messages distilled:
> 1. Strong operational work and real-time communication (incidents, Slack, dashboards) — this is a real strength
> 2. Needs to develop *asynchronous written communication* (postmortems, RFCs, documentation) — this is the growth area
>
> Two messages. One strength to build on, one area for development. The subordinate walks away knowing exactly what to continue and what to improve.

### The Blast (Major Performance Problem)

When you have a subordinate who, *"unless turned around, could get fired,"* the review becomes an exercise in conflict resolution. This is where the five stages (next section) play out.

The key: the supervisor's job is to get the subordinate to move through *all* stages until they **assume responsibility** for the problem. Without that, no solution is possible.

### Reviewing the Ace

Grove makes a counterintuitive argument: most supervisors invest heavily in reviewing poor performers (detailed corrective action plans) but give top performers brief, retrospective reviews that merely justify the high rating.

> *"I think we have our priorities reversed. Shouldn't we spend more time trying to improve the performance of our stars? After all, these people account for a disproportionately large share of the work in any organization."*

Improving a star's performance is **high-leverage** because their output multiplier is already large. A 10% improvement in a top performer's output may exceed a 50% improvement in an average performer's output.

> *"No matter how stellar a person's performance level is, there is* always *room for improvement."*

> **[Senior EM Application: Reviewing Stars Is Where Most Managers Fail]**
>
> This is one of the most actionable insights in the chapter. Most Senior EMs:
> - Spend 3 hours preparing a PIP-style review for a struggling engineer
> - Spend 30 minutes on a "you're great, keep it up" review for their Staff engineer
>
> Grove says invert this. The Staff engineer is your highest-leverage investment. Questions to prepare for their review:
> - "Given your abilities, what could you have accomplished this year that you didn't?"
> - "Where did you choose safe approaches when a bolder one would have had more impact?"
> - "What skill, if developed, would allow you to operate at the Principal level?"
> - "You led X well — here's how you could have made it even more impactful by doing Y differently"
>
> The ace *wants* this feedback. They're in self-actualization mode (Chapter 11) and are hungry for feedback that helps them grow. A "you're great" review provides no racetrack.

---

## The Five Stages of Problem-Resolution

When delivering a "blast" review (or any review with significant negative feedback), the subordinate typically moves through five stages:

| Stage | Subordinate's Behavior | Manager's Response |
|-------|----------------------|-------------------|
| **1. Ignore** | Passively ignores the problem. Doesn't acknowledge it exists. | Present facts and examples that make the problem undeniable. |
| **2. Deny** | Actively denies the problem. "I don't see an issue here." | More evidence. Specific examples with data. |
| **3. Blame others** | Admits there's a problem but says it's not theirs. "It's because Team X didn't deliver" or "The tools are inadequate." | This is where things get stuck. The manager must persistently redirect to what the *subordinate* can control. |
| **4. Assume responsibility** | "Yes, this is my problem, and I need to do something about it." | **This is the critical transition.** It's emotional, not intellectual. Once here, finding solutions becomes relatively easy. |
| **5. Find a solution** | Collaborative problem-solving between manager and subordinate. | Shared task. Manager provides guidance; subordinate drives the plan. |

> *"The move from blaming others to assuming responsibility constitutes an emotional step, while the move from assuming responsibility to finding the solution is an intellectual one, and the latter is easier."*

**The supervisor's key discipline:** Know which stage you're in. If the subordinate is still blaming others (stage 3) and you're trying to discuss solutions (stage 5), nothing happens. You must move through the stages *together*, in sequence.

> **[Mental Model: The Five Stages Applied to Incident Postmortems]**
>
> The same five stages play out in blameless postmortems, but at the team level:
>
> | Stage | Postmortem Equivalent |
> |-------|---------------------|
> | **Ignore** | "This wasn't really an incident. The customer probably didn't notice." |
> | **Deny** | "Our service was fine. The upstream service caused it." |
> | **Blame others** | "The product team deployed without telling us. It's their fault." |
> | **Assume responsibility** | "We didn't have monitoring that would have caught this early. That's our gap." |
> | **Find solution** | "We need burn-rate alerting on this SLO. I'll implement it this sprint." |
>
> The postmortem facilitator's job — like the review supervisor's — is to guide the group through all five stages to responsibility and solution. Getting stuck at "blame others" is the most common failure mode for both reviews and postmortems.

---

## Practical Mechanics

**When to give the written review:** Grove recommends giving it *before* the face-to-face discussion. The subordinate reads it privately, digests it, reacts and overreacts, then re-reads. By the meeting, they're emotionally and rationally prepared.

**Self-reviews:** Grove is against having subordinates write their own reviews: *"If you have to tell your supervisor about your accomplishments, he obviously doesn't pay much attention to what you are doing."* The supervisor's independent judgment must be preserved — it's the integrity of the system.

**Subordinate evaluating the supervisor:** Can be useful, but must be framed as advisory, not authoritative. *"He is not your leader; you are his. And under no circumstances should you pretend that you and your subordinates are equal during performance reviews."*

---

## Acceptable vs. Desirable Outcomes

Grove distinguishes between three possible outcomes of a difficult review:

1. **Subordinate agrees with assessment AND commits to the cure** — desirable
2. **Subordinate disagrees with assessment BUT commits to the cure** — acceptable
3. **Subordinate disagrees AND does not commit** — unacceptable

> *"Any outcome that includes a* commitment *to action is acceptable."*

If you can't get agreement, accept commitment. Grove tells a personal story: a subordinate clearly disagreed with his assessment but finally said, *"Andy, you will never convince me, but why do you insist on wanting to convince me? I've already said I will do what you say."*

> *"Don't confuse emotional comfort with operational need. To make things work, people do not need to side with you; you only need them to commit themselves to pursue a course of action."*

If even commitment isn't forthcoming, use position power explicitly:

> *"This is what I, as your boss, am instructing you to do. I understand that you do not see it my way... But I am not only empowered, I am required by the organization for which we both work to give you instructions."*

> **[Core Concept: Agreement vs. Commitment — A Crucial Distinction]**
>
> This parallels Chapter 5's "disagree and commit" decision-making model. In both cases, Grove separates emotional buy-in (agreement) from behavioral buy-in (commitment). The organization needs commitment. Agreement is desirable but not required.
>
> **For Senior EMs:** When your direct report disagrees with a performance assessment but commits to the improvement plan, that's a win. Don't keep pushing for agreement — you'll waste time, damage the relationship, and make the review about *your* comfort rather than *their* performance.

---

**Chapter 13 establishes:** Performance reviews are the highest-leverage feedback mechanism. Assessment requires weighing output vs. internal measures, accounting for time offsets, and judging performance (not potential). Delivery follows the three L's: level, listen, leave yourself out. Use the worksheet method to distill messages to the subordinate's absorption capacity. The five stages of problem-resolution must be traversed in order. Commitment to action is the minimum acceptable outcome. Invest more review effort in top performers — that's the highest-leverage application.

**Next: Chapter 14 — Two Difficult Tasks, covering hiring and retention (talking someone out of quitting).**
