# Chapter 9: Bootstrapping Culture — Part 2

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 2 covers:** Career ladders, cross-functional teams, engineering processes (code review, postmortems, architecture review), chapter assessment.
See [Part 1](ch09-notes-bootstrapping-culture-part1.md) for: structure, culture, values.

## Table of Contents — Part 2

- [Writing a Career Ladder](#writing-a-career-ladder)
- [Cross-Functional Teams](#cross-functional-teams)
- [Developing Engineering Processes](#developing-engineering-processes)
- [Practical Advice: Depersonalize Decision Making](#practical-advice-depersonalize-decision-making)
- [Quarterly Ritual: Culture Infrastructure Check](#quarterly-ritual-culture-infrastructure-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping Engineering Culture](#how-genai-is-reshaping-engineering-culture)

**Block types in Part 2:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Mental Model] [The Shadow Side] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## Writing a Career Ladder

Fournier's detailed advice from her second, successful attempt:

**1. Solicit participation.** Enlisted senior managers and engineers. Asked people to highlight confusion, propose rewrites. Used subgroups for specialized areas (senior ICs worked on senior IC levels).

**2. Look for examples.** Got ladders from friends at other companies, especially larger ones with strong technical reputations.

**3. Be detailed.** "Think about the kinds of details you would look for when deciding if someone should be hired in at a level or promoted." Match your company context.

**4. Use both long-form and summary.** Spreadsheet for side-by-side comparison across levels. Long-form document that reads like "a performance review of a person operating well at each level."

**5. Career ladder relates to salary.** Each level maps to a salary band. Decisions: wide bands (fewer levels, bigger range) vs. narrow bands (more levels, tighter pay).

**6. Many early levels with narrow bands.** Engineers expect frequent raises/promotions early. Create several early levels that allow promotion every year for 2-3 years.

**7. Wide bands for senior levels.** "A strong software engineer may make more than a senior engineer" — this wiggle room retains people performing well but not ready for the next level.

**8. Identify breakpoint levels.** "What is the lowest level at which people can sit forever, never getting promoted but also not underperforming?" Usually around senior engineer. Expect your team to cluster here.

**9. Celebrate keystone promotions.** Senior engineer, staff engineer, principal engineer, director, VP. "Having keystone levels... gives people a bigger achievement to strive for beyond the next pay increase."

**10. Split management and technical tracks.** Usually split above senior engineer. Don't expect equal numbers in both tracks.

**11. Consider requiring management experience pre-split.** "Encourage everyone to have some sort of management or mentorship experience before they are eligible to be promoted above the level of the track split."

**12. Years of experience as guidance.** Not strict requirements, but "rules of thumb, especially if you are writing a ladder for the first time."

**13. Evolve over time.** "You're creating a living document that will need to evolve."

> **[SRE Lens: SRE-Specific Career Ladder Considerations]**
>
> SRE ladders need to account for:
> - **Operational skills** that don't exist on standard software engineering ladders: incident command, capacity planning, SLO design, production readiness assessment
> - **Breadth vs. depth balance:** Senior SREs often need both deep systems knowledge AND broad organizational influence. The ladder should reflect this.
> - **On-call progression:** Junior SREs shadow → carry pager with backup → carry pager independently → mentor others on-call → design on-call processes
> - **The IC/management split in SRE:** Staff SRE should be clearly defined — is it "deep technical expert" or "broad technical leader"? Both are valid but different.
> - **Cross-functional impact:** Senior SRE levels should require demonstrated impact on product teams, not just the SRE team itself.

> **[Leader's Playbook: When to Create an SRE Ladder]**
>
> You need an SRE-specific ladder (or SRE-specific modifications to the engineering ladder) when:
> - SRE engineers are being evaluated against software engineering criteria that don't capture their work
> - Promotion conversations consistently involve "but their work is different from software engineering"
> - SRE team members express confusion about what the next level looks like for them
> - You're losing SRE engineers because they see no growth path
>
> Start by adapting the existing engineering ladder. Add SRE-specific examples and expectations at each level. Get input from your senior SREs.

---

## Cross-Functional Teams

Fournier shares the success of creating cross-functional "pods" at Rent the Runway — engineers, product manager, designers, data analyst, customer service representative, all working together on a feature.

The impact: "delivered a good feature, fairly quickly, and the contributors all felt that they understood the goals of the project." Broke the "us versus them" dynamic between functions.

**Conway's Law:** "Organizations which design systems... are constrained to produce designs which are copies of the communication structures of these organizations." Cross-functional teams optimize for **effective product development and iteration** — but may produce **less technically optimal systems** than engineering-centered structures.

**How pods work:**
- Management structure doesn't change. Engineers still report to engineering managers.
- Day-to-day work is determined by the pod's roadmap.
- Keep a small infrastructure group not assigned to product development.
- Reserve 20% of engineering time for on-call, interviewing, sustaining engineering.

**Product-centric vs. engineering-centric leadership:**
- Product-centric teams value: product sense, shipping speed, cross-functional communication
- Engineering-centric teams value: complex systems design, technical depth, innovation
- Neither is universally correct — it depends on what the company most needs

> **[SRE Lens: SRE and Cross-Functional Teams]**
>
> SRE organizations face a fundamental structural question: embedded or centralized?
>
> **Embedded SRE:** SRE engineers sit in product pods. They gain deep product context and strong relationships. Risk: they lose SRE identity and get absorbed into feature work.
>
> **Centralized SRE:** SRE engineers work together as a team, supporting product pods from outside. They maintain SRE expertise and community. Risk: they become disconnected from product reality and are seen as gatekeepers.
>
> **Hybrid:** Some SREs embedded, some centralized (usually platform/infrastructure). The embedded SREs maintain membership in the SRE community through shared on-call, shared postmortems, and regular SRE team meetings.
>
> **Fournier's Conway's Law insight for SRE:** If you embed SREs in product teams, expect the reliability architecture to be product-shaped (each team has its own monitoring, alerting, and tooling). If you centralize, expect the reliability architecture to be platform-shaped (shared observability, shared deployment, shared standards). Choose the structure that produces the system architecture you want.

---

## Developing Engineering Processes

Fournier's core principle: **"Think of process as risk management."**

A complicated process should exist only for:
- Activities you expect to be rare
- Activities where risks are not obvious to people

**Two implications:**
1. **Don't put heavy process on common, low-risk activities.** If code review is too onerous, the whole team slows down on minor changes.
2. **Look for hidden risks and make them visible.** "A good political idea is one that works well in half-baked form" — processes should have value even when imperfectly followed.

> **[Insight]** "Process as risk management" is the best framing for engineers who resist process. It's not bureaucracy — it's the same risk analysis you do for systems. High-risk, infrequent operations (database migrations) get careful processes. Low-risk, frequent operations (deploying a CSS change) get lightweight processes. Match the weight of the process to the weight of the risk.

---

## Practical Advice: Depersonalize Decision Making

Fournier identifies three key processes to add as teams grow:

### Code Review

- **Code review is socialization, not bug-finding.** "For the most part, code reviews don't catch bugs; tests catch bugs." Code review ensures multiple people are aware of changes.
- **Use linters for style.** "Engineers can waste absurd amounts of time on questions of style." Automate style enforcement to prevent nitpicking and bullying.
- **Watch the review backlog.** Some companies limit outstanding review requests. Think about how to keep the queue flowing.

### The Outage Postmortem (Learning Review)

- **Resist finger-pointing.** "This blaming only results in people being afraid to make mistakes."
- **Understand context and circumstances.** Identify contributing factors — missing tests, inadequate tools, communication gaps.
- **Be realistic about takeaways.** Pick 1-2 high-risk, high-probability improvements. Don't create a laundry list that never gets addressed. "If you try to do all of them, you will end up doing none of them."

### Architecture Review

- **Be specific about what needs review.** New languages, frameworks, storage systems, developer tooling. Don't try to review every feature design — that's too frequent and slows things down.
- **The value is in preparation.** Requiring review forces people to think through why they want to make changes and what the risks are.
- **Choose reviewers wisely.** Include people most affected by the change, not a static guru panel. "There's nothing more demoralizing than having someone from a completely unrelated area veto a project."

> **[SRE Lens: SRE-Specific Processes]**
>
> Beyond Fournier's three, SRE teams commonly need:
>
> **Production Readiness Review:** Before a new service goes to production or SRE takes on-call support. Checklist: monitoring, alerting, runbooks, rollback plan, load testing, SLO definition.
>
> **On-Call Handoff:** Written summary from outgoing to incoming on-call. Recent incidents, ongoing issues, known risks, scheduled changes.
>
> **Toil Review:** Quarterly review of repetitive manual work. Which tasks should be automated? Which eliminated? Which accepted as necessary?
>
> **Incident Command Protocol:** Who does what during a major incident. Incident commander, communication lead, technical lead, scribe. Not needed for P3s; essential for P1s.
>
> **Error Budget Review:** Monthly or quarterly. Are services within their error budgets? Which are at risk? What actions are triggered when budgets are exhausted?

---

## Quarterly Ritual: Culture Infrastructure Check

> **[Quarterly Ritual]**
>
> **Structure Health:**
> - [ ] Where have we experienced failures this quarter that could be prevented by structure?
> - [ ] Where is existing structure slowing us down without providing value?
> - [ ] Are we applying Gall's Law — evolving structure from simple working systems, not designing complex systems from scratch?
>
> **Values Health:**
> - [ ] Can every team member articulate our team's core values?
> - [ ] Have I reinforced values through recognition this quarter? Specific examples?
> - [ ] Have I addressed any values conflicts directly?
> - [ ] Are we using values in hiring conversations, or defaulting to "culture fit" as friendship test?
>
> **Career Ladder Health:**
> - [ ] Does our career ladder reflect the actual work our team does?
> - [ ] Are promotion conversations clear and grounded in the ladder?
> - [ ] Is anyone confused about what "next level" looks like for them? If so, the ladder may need updating.
>
> **Process Health:**
> - [ ] Are our processes proportional to their risks? (Heavy for rare/dangerous, light for common/safe)
> - [ ] When was the last time we reviewed and updated a process?
> - [ ] Are postmortem action items being completed, or piling up?
> - [ ] Is code review functioning as socialization (healthy) or as gatekeeping/nitpicking (toxic)?

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"What is the culture of your team, really? Not the culture you've stated or aspire to, but the one that's actually operating. Ask yourself: what behaviors are rewarded? What behaviors are tolerated? What behaviors cause people to leave?"** The gap between stated culture and operating culture is your biggest cultural debt.
>
> 2. **"If a new engineer joined your team next Monday, would they understand the unwritten rules within a month? If not, those rules should be written."** Unwritten rules are invisible barriers — they privilege insiders and disadvantage newcomers.
>
> 3. **"Think about the last process you introduced. Did it solve the problem it was designed for? Did it create new problems? When was the last time you revisited it?"** Processes tend to persist long after the problem they solved has disappeared. Review them as actively as you review your code.

---

## How GenAI Is Reshaping Engineering Culture

> **[GenAI + Culture]**

**AI and Career Ladders:** AI can help analyze performance data against ladder criteria, reducing bias in promotion decisions. It can also help draft ladder documentation by analyzing patterns across existing ladders from multiple companies.

**AI and Code Review:** AI code review tools (GitHub Copilot for Pull Requests, CodeRabbit, etc.) are changing the socialization function of code review. When AI catches bugs and style issues, human reviewers can focus on design decisions, readability, and knowledge sharing. This potentially makes code review MORE valuable, not less.

**AI and Postmortems:** AI can assist postmortem facilitation — summarizing incident timelines, suggesting contributing factors, comparing with historical incidents. But the human elements — psychological safety, blame-free discussion, emotional processing — remain irreducibly human.

**AI and Engineering Processes:** AI can automate process compliance checking (production readiness checklists, architecture review requirements) without adding human overhead. This addresses Fournier's concern about process weight — AI makes it possible to have thorough processes that don't slow people down.

**The cultural question AI raises:** As AI writes more code, the culture of engineering teams shifts. What does an SRE career ladder look like when AI handles routine automation? What values matter when incident response is AI-assisted? How does code review culture change when AI is the first reviewer? These questions need proactive cultural leadership, not reactive adjustment.

**Further reading for Chapter 9:**
- [Jo Freeman, "The Tyranny of Structurelessness"](https://www.jofreeman.com/joreen/tyranny.htm) — the essay Fournier references, free online
- [*Reinventing Organizations* by Frederick Laloux](https://www.goodreads.com/book/show/20787425-reinventing-organizations) — culture as operating system
- [John Gall, *Systemantics*](https://www.goodreads.com/book/show/583785.Systemantics) — Gall's Law and system evolution
- [*An Elegant Puzzle* by Will Larson](https://press.stripe.com/an-elegant-puzzle) — career ladders, organizational design
- [*Team Topologies* by Skelton & Pais](https://www.goodreads.com/book/show/44135420-team-topologies) — modern approach to cross-functional team structures
- [Google's SRE Books](https://sre.google/books/) — SRE-specific processes: postmortems, on-call, error budgets
