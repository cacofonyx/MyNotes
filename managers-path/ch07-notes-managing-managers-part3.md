# Chapter 7: Managing Managers — Part 3

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 3 covers:** Hiring managers, debugging dysfunctional organizations, setting expectations and delivering on schedule, roadmap uncertainty, staying technically relevant, chapter assessment.
See [Part 1](ch07-notes-managing-managers-part1.md) for: skip-levels, accountability.
See [Part 2](ch07-notes-managing-managers-part2.md) for: people pleaser, new/experienced managers.

## Table of Contents — Part 3

- [Hiring Managers](#hiring-managers)
- [Ask the CTO: Managing Outside Your Skill Set](#ask-the-cto-managing-outside-your-skill-set)
- [Debugging Dysfunctional Organizations](#debugging-dysfunctional-organizations)
- [Setting Expectations and Delivering on Schedule](#setting-expectations-and-delivering-on-schedule)
- [Challenging Situations: Roadmap Uncertainty](#challenging-situations-roadmap-uncertainty)
- [Staying Technically Relevant](#staying-technically-relevant)
- [Quarterly Ritual: Managing Managers Health Check](#quarterly-ritual-managing-managers-health-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping Managing Managers](#how-genai-is-reshaping-managing-managers)

**Block types in Part 3:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [First 90 Days] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## Hiring Managers

Fournier addresses a common situation: growing fast, no internal candidates ready for management, need to hire from outside.

**The challenge:** "We're barely capable of determining if an engineer is capable of writing good code... Management is... well, what even is it? How do we interview for it?"

**The biggest risk:** "Managers can, theoretically, bullshit you more easily." Management skills are communication-based — someone who interviews well can still fail to ship anything.

**What to evaluate:**

**1. 1-1 Skills:** Have future direct reports interview the candidate by asking her to help with current or recent problems. "A good manager—even without a full understanding—should have good instincts for questions to ask and suggested next steps."

**2. Team debugging:** Ask about projects that were behind schedule. Role-play with an employee thinking about quitting. Ask about coaching struggling employees and developing strong ones.

**3. Management philosophy.** "If she doesn't have one at all, that might be a red flag."

**4. Presentation skills** (for senior roles). Not to judge content but to see how she commands a room and handles questions. "I'd caution you not to overvalue this step."

**5. Technical skills.** For coding managers: abbreviated technical interview. For non-coding: design/architecture questions about systems she's built. Can she mediate a technical debate?

**6. Cultural fit.** "By far the biggest place where it can cause grief is in a management hire." Informal vs. hierarchical culture? Servant-leadership vs. directive? Collaboration vs. loudest-voice-wins?

Fournier's strongest advice: **"Do thorough reference checks."** Even for people you've worked with before. "Ask the references to describe the ways that the person succeeds as well as the ways she fails."

> **[Leader's Playbook: Interviewing SRE Managers]**
>
> Fournier's framework + SRE-specific additions:
>
> **1-1 Role-Play:** Have a current SRE bring a real scenario: "My on-call engineer is burned out and wants to leave the rotation. How would you approach this?"
>
> **Incident Management:** "Walk me through how you'd handle a P1 with a new team you've just joined." Look for: calm demeanor, information-gathering instincts, delegation, communication to stakeholders.
>
> **Team Debugging:** "Your SRE team has a high incident rate. Walk me through how you'd diagnose the root cause — not the technical root cause of incidents, but the organizational root cause of why the team isn't improving."
>
> **Technical:** Architecture questions about systems they've managed. "What were the biggest operational risks in that system? How did you prioritize addressing them?" Look for: ability to discuss tradeoffs, not just technical depth.
>
> **Culture:** "How do you think about the relationship between SRE and product engineering?" The answer reveals whether they see SRE as a partner, a gatekeeper, or a service organization.
>
> **References:** Ask specifically: "Did this person's team have good retention? Did engineers grow under their leadership? How did they handle conflict with product teams?"

> **[Red Flags in Manager Interviews]**
>
> - Can't describe their management philosophy beyond platitudes
> - Every story positions them as the hero — no examples of developing others
> - Dismisses the importance of 1-1s or skip-levels
> - Can't give specific examples of difficult feedback they've delivered
> - Talks about "my team" in possessive terms rather than "the team I supported"
> - Has no questions about the team's current challenges — isn't curious about what they're walking into
> - References are evasive or give only generic praise

---

## Ask the CTO: Managing Outside Your Skill Set

A manager now responsible for operations and QA teams in addition to software development asks for advice.

Fournier's advice:
- **Be curious, not authoritative.** "Ask the person to teach you about the work she does. Sit down with her and treat her as if she were your mentor."
- **Devote significant time to unfamiliar areas, especially early.** Resist the temptation to spend more time in comfortable areas.
- **Don't let unfamiliarity become avoidance.** "If you view these areas as uninteresting or unworthy of your time, you may find yourself reluctant to deal with problems even when people are clearly drawing attention to them."

> **[SRE Lens: When Your Scope Expands]**
>
> For SRE Directors, scope expansion often means: adding platform engineering, adding security engineering, adding data engineering, or adding developer experience. Each has its own culture, metrics, and leadership needs.
>
> **The mistake:** Treating the new team like another SRE team. Platform engineering has different success metrics (developer adoption, self-service usage) than SRE (reliability, incident response). Applying SRE management patterns to a platform team will frustrate both of you.
>
> **The fix:** Fournier's advice — be the student. Ask the team and its leader to teach you. Learn their metrics. Understand what success looks like in their domain. Then apply your management skills (accountability, delegation, coaching) with domain-appropriate goals.

---

## Debugging Dysfunctional Organizations

Fournier draws a powerful analogy: **the best engineering managers are great debuggers.** Organizations are "complex black boxes interacting with other complex black boxes." Debugging teams uses the same skills as debugging systems.

**The diagnostic framework:**

**1. Have a hypothesis.** What do you think is wrong? Investigate "in as minimally invasive a way as possible" — like adding logging without changing the system's behavior.

**2. Check the data.** Look at team chats, emails, tickets, code reviews, check-ins, calendars. Are there lots of incidents? Are people sick? Are they bickering in code reviews? Are tickets vague or too big? Is the team chatting about fun things or purely business?

**3. Observe the team.** Sit in their meetings. Are they boring? Who talks most? Are meetings overscripted? Is there healthy conflict? But beware: **"You can't go into a team and not change the behavior of that team by being around them"** — the Schrödinger observation problem.

**4. Ask questions.** Ask the team what their goals are. Can they tell you? Do they understand why? Did they have input on the goals? A team doing only engineering projects while neglecting product work "doesn't appreciate or understand the value of the product/business projects."

**5. Check team dynamics.** Do people like each other? Collaborate? Have banter in chat? Good relationships with adjacent teams? "A bunch of people who never talk to each other and are always working on independent projects are not really working as a team."

**6. Jump in to help.** Don't just tell the manager to fix it. Sometimes help debug the team, just as you'd jump into a complex system outage even though you rarely write code.

**7. Be curious.** "The pursuit of why when it comes to organizational problems is the thing that gives you patterns to match on."

> **[Mental Model: Organization as Distributed System]**
>
> Fournier's debugging analogy extends further:
>
> | System Debugging | Organization Debugging |
> |-----------------|----------------------|
> | Read logs | Read team chats, emails, tickets |
> | Check metrics | Check velocity, incident rate, attrition |
> | Trace a request | Trace a project from idea to delivery |
> | Look for bottlenecks | Look for people/process bottlenecks |
> | Check for cascading failures | Check for cross-team dysfunction spreading |
> | Observer effect changes behavior | Your presence in meetings changes behavior |
> | Fix root cause, not symptoms | Fix structural/cultural issues, not surface problems |
>
> **For SRE Directors:** You already have this debugging instinct from years of incident response. Apply the same rigor, the same refusal to accept "it just stopped working," the same pursuit of root cause. A team that's "just slow" has a root cause, the same way a service that's "just slow" has one.

---

## Setting Expectations and Delivering on Schedule

Fournier addresses the most frustrating question engineering managers face: **"Why is this taking so long?"**

Two scenarios:
1. **The project IS over plan** — reasonable question, you need to understand and explain
2. **The project IS on plan** but leadership didn't like the original estimate or didn't ask — frustrating but common

**Her advice:** Be aggressive about sharing estimates and updates, even when people don't ask. Especially if the project is critical or will take more than a few weeks.

On estimation resistance: engineers often don't want to estimate beyond a sprint. Fournier pushes back: "few of these things are always true" (that requirements change constantly, that everything fits in two sprints). Estimates are useful even when imperfect because they "help escalate complexity" and help businesses "plan and get ideas of costs."

"When estimates are wrong, what are we learning about unknown complexity?"

On cutting scope: "As the senior manager, you may need to play tiebreaker." If you only cut technical quality, "you'll just slow down the team after the project is launched."

> **[SRE Lens: Estimation for Reliability Projects]**
>
> Reliability projects are notoriously hard to estimate because:
> - The scope of "make this reliable" is unbounded without explicit SLO targets
> - Discovery work (understanding the current system) often takes as long as the fix
> - Incident interrupts steal planned capacity unpredictably
> - Dependencies on other teams are common and often uncontrolled
>
> **Fournier's advice applied to SRE:**
> - Define clear success criteria (specific SLO targets, specific MTTR goals) so the scope isn't infinite
> - Estimate in ranges, not points: "4-8 weeks, narrowing after 1 week of investigation"
> - Budget for interrupts explicitly: "This estimate assumes no more than 2 P2 incidents during the work period"
> - Communicate proactively: weekly status updates on multi-week projects, even if there's nothing dramatic to report

---

## Challenging Situations: Roadmap Uncertainty

Fournier addresses changing product roadmaps — "where being stuck in 'middle management' feels the most unpleasant." You may have little power to push back on strategy changes from above, but you've made promises to your team.

**Strategies:**

1. **Be realistic about change likelihood.** If your startup changes plans every summer, don't promise things that require continuity past June.

2. **Break big projects into smaller deliverables.** Achieve partial value even if the grand vision is cancelled.

3. **Don't overpromise future technical projects.** "Don't promise your team exciting technical projects 'later,' because the product roadmap for later hasn't been written yet." If the project is important, get it scheduled now.

4. **Dedicate 20% to sustaining engineering.** Refactoring, bugs, process improvements, ongoing support. Build this into every planning session. "Unfortunately, 20% is not enough to do big projects," so major technical work needs separate advocacy.

5. **Apply business rigor to engineering projects.** How big? How important? Can you articulate the value? What would success mean? "Treat big technical projects the same way as product initiatives."

> **[Leader's Playbook: Making the Case for Technical Investment]**
>
> When you need approval for a major reliability/technical project:
>
> **Frame it as a business case:**
> - **Problem:** "Our checkout service has had 4 outages in the last quarter, each costing approximately $X in lost revenue."
> - **Root cause:** "The service is running on an architecture that was designed for 10% of current traffic. Incremental fixes have diminishing returns."
> - **Proposed solution:** "Rearchitect the checkout service. 2 engineers, 8 weeks."
> - **Expected outcome:** "Reduce checkout-related outages by 80%, saving ~$Y per quarter. Also enables the product team's planned checkout redesign without additional reliability risk."
> - **Cost of inaction:** "Without this investment, we expect incident frequency to increase as traffic grows 30% next quarter. Each additional outage costs ~$Z in revenue plus engineering time."
>
> **The key:** Make the value legible to non-technical stakeholders. "Reduce technical debt" is invisible. "Prevent $X in lost revenue and free up 2 engineering months per quarter" is concrete.

---

## Staying Technically Relevant

Fournier defines five areas of technical responsibility for Directors:

1. **Oversee technical investment** — ensure the team's technical bets are in the right places
2. **Ask informed questions** — sniff out misguided efforts, evaluate proposed investments
3. **Analyze engineering and business tradeoffs** — translate between technical and business perspectives
4. **Make specific requests** — filter technically infeasible ideas, map new initiatives onto existing work. Don't be a "go-between" who relays requests without adding value.
5. **Use experience as a gut check** — rely on instincts honed over years

**How to stay relevant:**
- Read code occasionally
- Ask engineers to explain unfamiliar areas (whiteboard sessions)
- Attend postmortems — "full of details about the process of writing and deploying software that you miss when you aren't coding every day"
- Keep up with industry trends in development processes
- Foster a network of technical peers outside the company
- Never stop learning

> **[SRE Lens: Technical Relevance for SRE Directors]**
>
> Adapt Fournier's list:
> - **Read postmortems religiously.** Every P1 and P2. Look for systemic patterns, not just individual incidents.
> - **Review SLO dashboards monthly.** Understand the trends, not just the alerts.
> - **Attend architecture reviews.** Ask operational questions: failure modes, scaling limits, monitoring plan, on-call implications.
> - **Stay current on observability and platform trends.** OpenTelemetry, eBPF, platform engineering, AI for ops — the SRE landscape is evolving rapidly.
> - **Shadow on-call once per quarter.** Not as primary — as observer. Feel the operational reality.
> - **Maintain your SRE network.** SREcon, KubeCon, local meetups. Your peers' war stories are your best learning resource.

---

## Quarterly Ritual: Managing Managers Health Check

> **[Quarterly Ritual]**
>
> **Manager Performance:**
> - [ ] For each manager: Are they making my life easier? Or am I frequently surprised by problems on their teams?
> - [ ] Do I have skip-level signal for each team? When was my last skip-level conversation per team?
> - [ ] Are new managers getting sufficient coaching? Am I investing upfront or abandoning them?
> - [ ] Are experienced managers being challenged with strategic work, or are they stagnating?
>
> **Team Health (across the org):**
> - [ ] Which team is my strongest? Why? Can I export those practices to other teams?
> - [ ] Which team is my weakest? What's the root cause? Is it the manager, the team composition, the workload, or the process?
> - [ ] Am I holding managers accountable for their teams' outcomes? Or am I accepting excuses?
>
> **Hiring and Development:**
> - [ ] Do I have succession plans for each manager role? If a manager left tomorrow, who steps up?
> - [ ] Am I developing the next generation of managers from within?
> - [ ] Is my interview process for managers effective? How did my last management hire work out?
>
> **Organizational Health:**
> - [ ] Is my org "purpose-bound" or "shallow-bound"? What identity are teams clustering around?
> - [ ] Am I proactively debugging, or waiting for fires?
> - [ ] Am I staying technically relevant? When did I last read code, attend a postmortem, or learn something new?

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"Which of your managers would you be most surprised to lose? That's probably the one you're paying the least attention to — because they don't need you. But 'doesn't need me' often drifts into 'doesn't feel valued by me.'"** Your best managers get the least attention because they cause the least trouble. Make sure they know you see their excellence.
>
> 2. **"If you asked each of your managers to describe YOUR management style, would their descriptions match? If not, you may be inconsistent — treating managers differently based on your comfort with them rather than their needs."**
>
> 3. **"When was the last time you discovered a problem through proactive investigation (skip-levels, data analysis, meeting observation) rather than reactive escalation?"** If you're always learning about problems after they've escalated, your information-gathering systems aren't working.
>
> 4. **"Think about your weakest team. Now be honest: is the problem the manager, or did you set the manager up to fail?"** Sometimes the issue is: wrong person in the role. But sometimes it's: insufficient support, unrealistic expectations, impossible scope, or a team composition that no manager could make work. Check your own accountability before attributing the failure to the manager alone.

---

## How GenAI Is Reshaping Managing Managers

> **[GenAI + Managing Managers]**

**AI and Skip-Levels:** AI can analyze team communication patterns, ticket velocity, and engagement signals to surface potential issues before skip-level meetings. "This team's PR review cycle time increased 3x this month" or "This team's Slack activity dropped significantly" — these are signals a human can then investigate.

**AI and Manager Coaching:** AI can help new managers with the basics: drafting 1-1 agendas, preparing performance feedback, structuring project plans. This lowers the coaching burden on you while ensuring new managers have scaffolding.

**AI and Organization Debugging:** Fournier's diagnostic framework — check data, observe, ask questions — can be partially automated. AI tools that analyze DORA metrics, incident patterns, and team sentiment data across your org give you the "organizational dashboard" that Directors desperately need.

**AI and Estimation:** AI-assisted estimation (analyzing historical velocity, identifying complexity patterns) can help managers provide better estimates, reducing the "why is this taking so long?" cycle.

**The meta-question:** AI makes it easier to manage the information flow, but the hard parts of managing managers — building trust, coaching through difficult situations, making judgment calls about people — remain irreducibly human. AI helps you see the signals; you still have to act on them.

**Further reading for Chapter 7:**
- [*High Output Management* by Andy Grove](https://www.goodreads.com/book/show/324750.High_Output_Management) — Fournier references this repeatedly; the original text on management leverage
- [*The Five Dysfunctions of a Team* by Patrick Lencioni](https://www.goodreads.com/book/show/21343.The_Five_Dysfunctions_of_a_Team) — first-team focus, trust, accountability
- [*Crucial Accountability* by Patterson et al.](https://www.goodreads.com/book/show/17118702-crucial-accountability) — how to hold people accountable without destroying relationships
- [*An Elegant Puzzle* by Will Larson, Ch. 5-6](https://press.stripe.com/an-elegant-puzzle) — managing managers, organizational design
- [*Debugging Teams* by Fitzpatrick & Collins-Sussman](https://www.goodreads.com/book/show/21343.Debugging_Teams) — team dynamics and collaboration
