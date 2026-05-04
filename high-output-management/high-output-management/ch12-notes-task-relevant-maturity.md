# Chapter 12: Task-Relevant Maturity

> **High Output Management** — Andrew S. Grove
> *Why There Is No Single Best Management Style — and How to Choose the Right One*

This chapter answers the question that follows naturally from Chapter 11's motivation discussion: **once you know what motivates someone, how should you manage them?** Grove's answer: there is no universal best management style. The right style depends on **task-relevant maturity (TRM)** — the subordinate's experience, readiness, and achievement orientation *for the specific task at hand.* A veteran engineer with 15 years of experience has high TRM for system design but possibly low TRM for leading an architecture review or managing a vendor relationship. The management style must match the TRM for each task, not the person's overall seniority.

## Table of Contents

- [No Single Best Management Style](#no-single-best-management-style)
- [Task-Relevant Maturity Defined](#task-relevant-maturity-defined)
- [The Three Management Styles by TRM Level](#the-three-management-styles-by-trm-level)
- [TRM Is Dynamic, Not Fixed](#trm-is-dynamic-not-fixed)
- [TRM and Managerial Leverage](#trm-and-managerial-leverage)
- [Why Managers Choose the Wrong Style](#why-managers-choose-the-wrong-style)
- [The Friendship Question](#the-friendship-question)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Practical Toolkit] [Anti-Pattern] [Scenario] [Mental Model]

---

## No Single Best Management Style

Grove opens by reviewing management style history: autocratic (early 1900s), humanistic (1950s), behavioral science experiments (1960s+). No research could demonstrate a single best approach.

His own observation at Intel confirms this: when managers are rotated between groups, *"neither the managers nor the groups maintain the characteristic of being either high-producing or low-producing."* Performance depends on the *combination* of manager and group, not on either alone.

> *"This also suggests that a given managerial approach is not equally effective under all conditions."*

---

## Task-Relevant Maturity Defined

TRM is a combination of:
- **Achievement orientation** — how driven the person is to succeed at this task
- **Readiness to take responsibility** — willingness to own outcomes
- **Education, training, and experience** — relevant skills and knowledge

**Crucially, TRM is specific to the task.** Grove illustrates: a superstar sales manager was moved to run a factory unit. Despite his personal maturity and proven competence, his *task-relevant* maturity for manufacturing was low, and his performance initially deteriorated. *"We confused the manager's general competence and maturity with his task-relevant maturity."*

TRM can also drop when the environment changes: *"A person's TRM can be very high given a certain level of complexity, uncertainty, and ambiguity, but if the pace of the job accelerates or if the job itself abruptly changes, the TRM will drop."*

---

## The Three Management Styles by TRM Level

| TRM Level | Management Style | What It Looks Like |
|-----------|-----------------|-------------------|
| **Low** | **Structured / task-oriented** | Tell *what*, *when*, *how*. Detailed instructions. Frequent check-ins. Close supervision. |
| **Medium** | **Individual-oriented / communicating** | Two-way communication. Emotional support. Mutual reasoning. Focus on the *person* as much as the task. |
| **High** | **Minimal involvement / monitoring** | Agree on objectives. Manager monitors results. Subordinate has autonomy over approach. |

> *"Do not make a value judgment and consider a structured management style less worthy than a communication-oriented one. What is 'nice' or 'not nice' should have no place in how you think or what you do. Remember, we are after what is most* effective."

Grove uses a parent-child development analogy:
- **Toddler (low TRM):** Tell them "no" — they can't understand the reasoning
- **Child learning to ride a bike (medium TRM):** Accompany them, support them, talk about safety while still holding the bike
- **Teenager (high TRM):** Set expectations, monitor occasionally, let them ride independently
- **College student (very high TRM):** Agree on goals (get a degree), monitor from a distance

**Important:** The structure doesn't disappear at high TRM — it *moves from externally imposed to internally given.* The teenager *knows* not to cross a busy highway. The knowledge is internalized; the parent no longer needs to state it.

> **[Core Concept: TRM Is Per-Task, Not Per-Person]**
>
> This is the insight that 95% of managers miss (per Horowitz's foreword). When asked "are you hands-on or hands-off?" most managers give a single answer, as if they have one management style. Grove says you need *multiple* styles active simultaneously — different for each person AND for each task that person handles.
>
> **Example for a Senior EM managing a TL:**
>
> | Task | That TL's TRM | Your Style |
> |------|-------------|-----------|
> | Running sprint planning | High — they've done it for 2 years | Minimal — agree on goals, check outcomes quarterly |
> | Giving difficult performance feedback | Low — first time managing an underperformer | Structured — tell them specifically what to say, when, how. Roleplay the conversation. Review what happened. |
> | Architecture design for familiar domain | High — they're the domain expert | Minimal — review the RFC, ask a few questions |
> | Vendor evaluation (first time) | Low — never evaluated a vendor before | Structured — define evaluation criteria together, review each vendor assessment, approve the recommendation |
> | On-call rotation management | Medium — they've done it but struggled with fairness | Communicating — discuss principles, share your approach, let them draft the rotation, review together |

> **[SRE Lens: TRM for Common SRE Tasks]**
>
> | SRE Task | Typical Low-TRM Person | Typical High-TRM Person | Style Adjustment |
> |----------|----------------------|------------------------|-----------------|
> | **Incident response (IC)** | New hire, first rotation as IC | Senior engineer who's run 50+ incidents | Low TRM: pair with experienced IC, detailed runbook adherence, debrief every incident. High TRM: let them lead, intervene only if escalation is needed. |
> | **Writing SLOs** | Product engineer unfamiliar with SLI/SLO concepts | Staff SRE who's defined SLOs for 10 services | Low: teach the framework, co-author the first SLO, review together. High: "Here's the service — propose the SLOs and we'll discuss." |
> | **Postmortem facilitation** | Engineer who's attended postmortems but never led one | Experienced facilitator with blameless-retro training | Low: provide the template, attend the session, coach real-time. High: review the written postmortem, give feedback. |
> | **Capacity planning** | New SRE manager, first time owning capacity | Senior EM who's done 8 capacity planning cycles | Low: structured — walk through the model together, review assumptions, approve the plan. High: agree on targets, review the output. |
>
> **The mistake to avoid:** Treating all SREs the same regardless of task. Your Staff SRE with 10 years of experience has *low TRM* for people management if they're mentoring for the first time. Give them structured guidance on that task while giving them full autonomy on technical work. This isn't inconsistency — it's TRM-appropriate management.

---

## TRM Is Dynamic, Not Fixed

TRM changes when the environment changes. Grove's military analogy: a sergeant who's casual with his soldiers (high TRM — everyone knows their routines) reverts to barking orders (low TRM) when the enemy attacks. After weeks of fighting from the same position, the fighting becomes routine and TRM rises again, allowing the sergeant to relax his style.

> *"A manager's ability to operate in a style based on communication and mutual understanding depends on there being enough time for it."*

And the key warning:

> *"Even if we achieve [monitoring mode], if things suddenly change we have to revert quickly to the what-when-how mode."*

> **[Scenario: TRM Drop During a Major Incident]**
>
> Your SRE team normally operates with high TRM — they handle incidents confidently, you monitor from a distance. Then a novel incident hits: a cascading failure across a system nobody fully understands, triggered by a configuration change in a service your team doesn't own.
>
> **TRM drops for the entire team** — not because they've become less capable, but because the task (debugging an unfamiliar cross-system failure) is new. Your management style must shift immediately:
>
> - **Before the incident:** Monitoring — you check the SLO dashboard occasionally
> - **During the novel incident:** Structured — you join the bridge, help decompose the problem, assign specific investigation tasks, coordinate with the other team
> - **After resolution:** Communicating — debrief together, help the team process the experience, discuss what to build to handle this class of failure next time
> - **After the fix is in place:** Return to monitoring — the team now has high TRM for this failure class

---

## TRM and Managerial Leverage

Grove connects TRM to the leverage equation:

1. **High TRM subordinates require less management time** → the supervisor has capacity for more leverage elsewhere
2. **High TRM enables delegation** → the supervisor's leverage multiplies
3. **High TRM means self-actualized motivation** → the most powerful and self-sustaining energy source

Therefore: **raising subordinates' TRM is one of the highest-leverage activities a manager can perform.** Every increment of TRM freed from one subordinate is time the manager can invest in other high-leverage activities.

The transmission of **operational values** is key. If the subordinate internalizes *how* the organization does things, they make decisions the way the manager would. Without that shared foundation, delegation fails — the subordinate makes reasonable-seeming decisions that don't align with organizational values.

Grove's devastating example: *"'He has to make his own mistakes. That's how he learns!' The problem with this is that the subordinate's tuition is paid by his customers. And that is absolutely wrong."*

---

## Why Managers Choose the Wrong Style

Grove identifies two failure modes:

**1. Style preference overrides TRM assessment.** Even when a manager correctly identifies medium TRM, they tend to default to either fully structured (micromanaging) or fully minimal (abdication). The communicating middle ground is the hardest to sustain.

**2. Self-perception gap.** Grove tested this: ~90% of supervisors rated their style as more communicating/delegating than their subordinates did. Managers think they're delegating when subordinates experience them as either too absent or too controlling.

Additional complication: *"Sometimes a manager throws out suggestions to a subordinate who receives them as marching orders"* — the power differential distorts communication.

> **[Anti-Pattern: The "Hands-Off" Identity]**
>
> Many Senior EMs take pride in being "hands-off." They see it as a sign of maturity — "I hire great people and get out of their way." Grove says this is only appropriate when TRM is high *for the specific task*. A manager who is uniformly hands-off:
>
> - Leaves low-TRM subordinates floundering (abdication, not delegation)
> - Misses early signs of problems because they're not monitoring
> - Produces the "he has to make his own mistakes" failure — at the customer's expense
>
> The correct identity: "I calibrate my management style to each person's TRM for each task." Not as catchy, but actually effective.

---

## The Friendship Question

Grove addresses whether managers should be friends with subordinates:

> *"Everyone must decide for himself what is professional and appropriate here. A test might be to imagine yourself delivering a tough performance review to your friend. Do you cringe at the thought? If so, don't make friends at work. If your stomach remains unaffected, you are likely to be someone whose personal relationships will strengthen work relationships."*

Friendship makes communicating style easier (you already have rapport) but makes structured style harder (giving orders to a friend feels wrong). The key: a social relationship is not the same as a communicating *management* style. Skiing together doesn't mean you're managing well.

---

**Chapter 12 establishes:** No single management style is best. TRM (task-relevant maturity) — specific to the task, not the person — determines the effective style. Low TRM → structured. Medium → communicating. High → monitoring. TRM is dynamic and drops when circumstances change. Raising TRM is one of the highest-leverage activities a manager can perform. Most managers overestimate how much they delegate and underestimate how much structure their subordinates need.

**Next: Chapter 13 — Performance Appraisal, where Grove tackles the most dreaded (and most high-leverage) task in management.**
