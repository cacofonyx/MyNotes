# Chapter 9: Bootstrapping Culture — Part 1

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "Culture is how things get done, without people having to think about it." — Frederick Laloux

This chapter addresses what senior leaders often underestimate: the deliberate creation and maintenance of engineering culture. Fournier argues that culture is infrastructure — neglect it and "your job will be harder."

**Part 1 covers:** The case for structure, the tyranny of structurelessness, assessing your org, creating culture, applying core values, creating cultural policy.
**Part 2 covers:** Career ladders, cross-functional teams, engineering processes (code review, postmortems, architecture review), chapter assessment.

## Table of Contents — Part 1

- [Structure as Learning](#structure-as-learning)
- [The Tyranny of Structurelessness](#the-tyranny-of-structurelessness)
- [Assessing Your Role](#assessing-your-role)
- [Creating Your Culture](#creating-your-culture)
- [Applying Core Values](#applying-core-values)
- [Creating Cultural Policy](#creating-cultural-policy)

**Block types in Part 1:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Mental Model] [The Shadow Side] [Go Deeper]

---

## Structure as Learning

Fournier reframes structure for skeptics: "Instead of talking about structure, I talk about learning. Instead of talking about process, I talk about transparency." The purpose isn't bureaucracy — it's learning from successes and mistakes and sharing those lessons transparently.

Her core principle: **"We don't set up systems because structure and process have inherent value. We do it because we want to learn from our successes and our mistakes."**

> **[SRE Lens: Structure = Reliability]**
>
> SRE teams understand this instinctively. Every SRE practice is structure-as-learning:
> - **SLOs** = structure for defining what "good enough" means
> - **Postmortems** = structure for learning from failure
> - **Runbooks** = structure for encoding operational knowledge
> - **On-call rotations** = structure for distributing operational responsibility
> - **Production readiness reviews** = structure for ensuring launch quality
>
> SRE organizations that resist "process" are actually resisting learning and transparency. When someone says "we don't need a postmortem process, we just fix things," what they're really saying is "we don't want to learn from our failures in a structured way."

---

## The Tyranny of Structurelessness

Fournier references Jo Freeman's essay (originally about feminist collectives), applying it to startups. Freeman's insight: **"Pretending to lack structure tends to create hidden power structures."**

Unstructured groups work only when:
- Task-oriented with narrow, specific function
- Small and homogeneous (shared language, shared expectations)
- High communication (everyone knows everything)
- Low skill specialization (people are interchangeable)

Fournier observes this maps to early startups: collocated "full stack" engineers hired from the same networks, building as a unified team. But this model breaks as the company grows.

**The value of structure:** "Structure is how we scale, diversify, and take on more complex long-term tasks. We do it to our software, we do it to our teams, and we do it to our processes."

Gall's Law: **"A complex system that works is invariably found to have evolved from a simple system that worked."** You can't design the perfect structure from scratch. Start simple, evolve as failure reveals where structure is needed.

> **[Insight]** Fournier makes an overlooked connection: the same skills that make great systems designers (identifying structure, drawing it out, making it explicit) make great organizational leaders. "Strong leaders are capable of identifying and shaping underlying team structures and dynamics, and doing so in a way that supports the long-term goals of the team." This is architecture — just for humans instead of software.

> **[Mental Model: Structure as Technical Debt Management for Organizations]**
>
> Just as code without structure accumulates technical debt, organizations without structure accumulate organizational debt:
> - No career ladder → retention problems, unfair pay, unclear expectations
> - No postmortem process → repeated failures, no learning
> - No code review → inconsistent quality, knowledge silos
> - No onboarding process → slow ramps, frustrated new hires
>
> Like technical debt, organizational debt is invisible until it causes failures. And like technical debt, the best time to address it is before it becomes critical — by evolving structure as the organization grows.

---

## Assessing Your Role

Fournier identifies four factors that determine how much structure you need:

**1. People:** More people → more structure needed. "Leaders who want a high degree of control... tend to need more structure."

**2. Age:** Older companies have more entrenched habits. But also more stability.

**3. Size of existing infrastructure:** More business rules, code, and physical infrastructure → more need for clarity on how to handle them.

**4. Risk tolerance:** Regulated industry or high stakes → more structure. Unregulated, small → less.

She uses the vehicle analogy: startup = race car (fast, risky, agile). Growing company = commercial plane (more people, more careful). Large company = spaceship (slow to turn, goes far, many passengers).

> **[SRE Lens: Structure and SRE Maturity]**
>
> SRE maturity directly correlates with appropriate structure:
>
> | Stage | Structure Level | What It Looks Like |
> |-------|----------------|-------------------|
> | Early SRE | Minimal | Ad-hoc incident response, no SLOs, firefighting mode |
> | Growing SRE | Moderate | Defined on-call, basic SLOs, postmortem process, some automation |
> | Mature SRE | Comprehensive | Error budgets, production readiness reviews, toil tracking, self-service platform |
> | Advanced SRE | Evolving | Structure exists but is continuously questioned and improved; automation replaces manual process |
>
> **The mistake:** Jumping from "minimal" to "comprehensive" overnight. Gall's Law applies — evolve structure as the team's failures reveal where it's needed.

---

## Creating Your Culture

Fournier defines culture: **"The generally unspoken shared rules of a community."** Culture guides decision-making in complex, uncertain environments where group interest must override individual interest.

Key insights:
- **Culture isn't optional.** "The early employees will form the culture, for good or for bad — or likely for a mixture of both."
- **Not every person will fit every company.** "The sooner you realize this, the better."
- **Values should be real values, not demographics.** "'Engineers who graduated from MIT' is not a culture. 'People who value technology innovation, hard work, intellect, scientific process, and data' might be." The first allows only a narrow subset; the second allows broad diversity with shared principles.
- **If you join a company with existing values, you'll be measured against them** whether you realize it or not. Employees who match values naturally do well. Those who don't will experience more friction.

> **[Deep Dive: SRE Culture Specifically]**
>
> SRE teams should articulate their own cultural values layered on the company's. Examples:
>
> - **Blameless accountability:** We hold systems accountable, not people. We fix processes, not humans.
> - **Data over opinions:** When we disagree, we look at the data. SLOs, metrics, and incident data arbitrate debates.
> - **Sustainable operations:** On-call should be manageable. Heroics are a symptom, not a solution.
> - **Teaching over gatekeeping:** We share reliability knowledge broadly, not hoard it.
> - **Customer-centric reliability:** We care about uptime because customers depend on us, not because dashboards should be green.
>
> These values guide decisions. When someone proposes skipping production readiness review to ship faster, the team can evaluate against shared values rather than having a power struggle.

---

## Applying Core Values

Fournier's framework:

**1. Define your culture.** Map company values onto your team. Add team-specific values. Example: her team at Rent the Runway explicitly valued diversity and layered a learning culture on top of company values.

**2. Reinforce culture through recognition.** Praise people for exhibiting values. Share stories at all-hands. Include values alignment in performance reviews. This "reinforces desired behavior in a positive way."

**3. Spot values conflicts.** If your company values "roll up your sleeves" and someone pushes off work, that's a values conflict. Use values to coach — it transforms "ambiguous friction" into concrete, articulable misalignment.

**4. Use values in hiring.** Remind interviewers of team values. Ask them to evaluate values alignment. But **NOT** "culture fit" as friendship test. "Culture fit as determined by friendship tests is almost certain to be discriminatory." Humans form friendships with similar backgrounds → race, class, gender bias. Instead: "Be specific. What are the values of this team, and where have you noticed any match or mismatch?"

> **[Leader's Playbook: Operationalizing SRE Values]**
>
> 1. **Write them down.** Not a poster — a working document. 5-7 values with definitions and examples.
> 2. **Include in onboarding.** New SRE team members should hear the values in their first week.
> 3. **Reference in decisions.** "We're choosing to invest in automation here because we value sustainable operations."
> 4. **Include in performance reviews.** "You've been excellent at blameless postmortems — that's a core part of how we operate."
> 5. **Use in hiring.** "This candidate was dismissive of the idea of SLOs. That conflicts with our data-over-opinions value."
> 6. **Evolve them.** Review annually. As the team grows, values may need updating.

---

## Creating Cultural Policy

Fournier shares her career ladder story as a case study in cultural policy creation. She borrowed a ladder from a friend's startup (8 levels, 4 categories). It flopped at her company because the teams had different backgrounds and needed more detail.

**Lesson:** "What works for one company... will not always translate well to another company, even if the companies have a lot of things in common."

Her friend's team was mostly from one big tech company — shared cultural habits. Her team was diverse in work backgrounds — no shared understanding. Same template, different results.

> **[Insight]** This is one of the most practical passages in the book. Copying another company's processes without understanding your own team's needs is a common and expensive mistake. This applies to everything: SRE practices borrowed from Google, incident management copied from PagerDuty's playbook, on-call models from Netflix. The PRINCIPLES transfer. The IMPLEMENTATION must be adapted to your context.

---

*Continued in [Part 2](ch09-notes-bootstrapping-culture-part2.md): Career ladders, cross-functional teams, engineering processes, chapter assessment.*
