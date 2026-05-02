# Chapter 7: Managing Managers — Part 1

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "Managing managers, how do I do it without taking up all my time? How do you help with problems that you aren't in the room to see, with unreliable witnesses? I'm spending all of my time two levels deep in people problems and it's exhausting." — Fournier, in an email to her leadership coach

This chapter is the gateway to senior leadership. Managing managers introduces a new level of abstraction — things are "obscured through an additional level," and "it's easy to miss out on details because you no longer engage regularly with all of the individual developers on each team." Fournier is honest: this is where many good managers fail, because they can't adapt to the ambiguity and indirection.

**Part 1 covers:** The open-door fallacy, skip-level meetings, manager accountability, and the delegation failure CTO sidebar.
**Part 2 covers:** The people pleaser, managing new managers, managing experienced managers.
**Part 3 covers:** Hiring managers, debugging dysfunctional organizations, setting expectations/estimation, roadmap uncertainty.

## Table of Contents — Part 1

- [The New Challenge: Managing Through Others](#the-new-challenge-managing-through-others)
- [Ask the CTO: The Fallacy of the Open-Door Policy](#ask-the-cto-the-fallacy-of-the-open-door-policy)
- [Skip-Level Meetings](#skip-level-meetings)
- [Manager Accountability](#manager-accountability)
- [Ask the CTO: My Tech Lead Isn't Managing](#ask-the-cto-my-tech-lead-isnt-managing)

**Block types in Part 1:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Influence Without Authority] [Go Deeper]

---

## The New Challenge: Managing Through Others

Fournier sets the stage: this is "the first level in a much bigger game, the entrée into senior leadership." The job requires:
- Figuring out how to spend your time to "maximize your leverage across your teams"
- Honing instincts by "following through on things that you're not sure are actually important, but you just sense are off"
- Managing teams outside your skill set — "you haven't yet built up the discipline or instincts to let yourself intuitively sense where and when to dive in deep, so you need to do so more frequently"

Common failure modes at this level: falling back into individual contributor work, playing project manager instead of developing managers to do it themselves.

> **[Insight]** Fournier's email to her coach is the most honest passage in the book. She's describing the fundamental paradox of managing managers: you're accountable for outcomes you can't directly observe, through people who may be filtering or distorting information, in situations where the "witnesses" (your managers) are also the potential source of the problem. This is why she says you need to "find your discomfort, chase it down, and sit with it unblinking." If something feels off but you can't explain why, investigate anyway. Your instincts at this level are your most valuable diagnostic tool.

> **[SRE Lens: Managing SRE Managers]**
>
> Managing SRE managers adds unique challenges:
> - **Operational reality is hard to hide but easy to misinterpret.** Incident data is objective, but the story behind the data isn't. A manager might present rising MTTR as "the systems are getting more complex" when the real issue is knowledge loss from attrition they haven't reported.
> - **SRE managers who came from IC roles** often struggle to let go of incident response. They jump in to fix things instead of coaching their team. You need to coach them to coach.
> - **Cross-team SRE dynamics** are invisible unless you look. Is one SRE team supporting 5 services while another supports 20? Is on-call burden equitably distributed across the managers' teams?

---

## Ask the CTO: The Fallacy of the Open-Door Policy

Fournier dismantles a common management myth: "I've told my team I have an open-door policy... and yet they aren't coming."

**Why it doesn't work:**
- "It takes an extremely brave engineer to willingly take the risk of going to her boss's boss to tell him about problems"
- People may not even know what the problems are well enough to explain them
- Some people are "great at managing up and hiding problems in their organizations"
- "These problems are very expensive to fix the longer they go on, and they won't bring themselves to your doorstep"

Fournier's conclusion: **your job is to proactively ferret out problems.** Passive accessibility isn't enough.

> **[Anti-Pattern: The Accessible Hermit]**
>
> You tell everyone "my door is always open." You hold office hours. You post your calendar publicly. And then you sit in your office, waiting. No one comes. You assume everything is fine.
>
> Meanwhile: one manager is hiding a project that's 3 months behind. Another has a toxic engineer she's afraid to address. A third team has had 5 people update their LinkedIn profiles this week.
>
> **Why this fails:** Accessibility is necessary but not sufficient. People need to trust you, believe it's safe to share bad news, AND believe it's worth the effort. Most skip-level reports have learned that "my door is open" is what every executive says, and very few mean it.
>
> **The fix:** Don't wait for people to come to you. Go to them. Skip-level meetings, team lunches, attending standups, reading chat channels — these are active information-gathering, not passive availability.

---

## Skip-Level Meetings

Fournier identifies skip-level meetings as "one of the critical keys to successful management at levels of remove."

**Two formats:**

**1. Individual skip-level 1-1s (quarterly).** Direct meeting with each person who reports to your direct reports. Benefits:
- Creates personal relationships so people aren't just "resources"
- Gives individuals time to ask questions
- Detects problems your managers may be hiding or not seeing

Suggested prompts:
- What do you like best/worst about your current project?
- Who on your team has been doing well recently?
- Any feedback about your manager — what's going well, what isn't?
- What changes would you make to the product?
- What opportunities are we missing?
- How's the organization doing overall?
- What areas of business strategy don't you understand?
- What's keeping you from your best work right now?
- How happy are you here?

**Scaling limitation:** Once you have >60 people, individual quarterly 1-1s become impractical (one per day for 60 working days).

**2. Skip-level lunches/group meetings.** Buy lunch for a whole team, talk about whatever's happening. Benefits:
- Efficient use of time
- Sense of group dynamics
- Answer strategic questions from the team

Limitation: People act differently in groups; they won't complain about their manager in front of peers.

**Critical purpose:** Detecting managers who are "managing up" well but failing their teams. "Having people who manage up well in your organization is always a hard situation to detect and respond to."

> **[Leader's Playbook: Running Effective Skip-Level Meetings]**
>
> **Individual skip-levels:**
> 1. Send prompts 24 hours before. "This meeting is for you. Here are some topics you might want to discuss."
> 2. Open with: "How are you? Not the project — you personally." Build the human connection.
> 3. Ask about their manager carefully. Not "is your manager good?" but "what could your manager do more of or less of?" Specific phrasing gets specific answers.
> 4. Ask about the team: "If you could change one thing about how this team works, what would it be?"
> 5. Close with: "Is there anything you wish I knew that you think I don't?"
> 6. **Do NOT solve problems in the moment.** Take notes. Follow up with the manager (carefully — without betraying confidences). Only intervene directly if there's something egregious.
>
> **Group skip-levels:**
> 1. Keep it informal. Lunch, coffee, team outing. Don't make it feel like a review.
> 2. Share organizational context. Answer their questions about strategy and direction. People crave this information and rarely get it from anyone senior.
> 3. Watch the dynamics. Who speaks? Who's silent? Is there tension? Energy? Is the manager dominating or are team members engaged?
>
> **After skip-levels:**
> - Pattern-match across conversations. If 3 people independently mention the same issue, it's real.
> - Share general themes (not attributable quotes) with the manager: "I'm hearing that the team feels X. What's your take?"
> - If you discover a serious problem, address it with the manager directly and promptly.

> **[Red Flags from Skip-Level Meetings]**
>
> - People can't articulate what they're working on or why it matters — their manager isn't providing context
> - Multiple people mention the same unresolved issue — the manager is avoiding something
> - People say "everything is fine" in a flat, unconvincing way — they don't feel safe being honest with you
> - The manager's self-assessment doesn't match the team's experience — the manager is either self-deceptive or actively misleading you
> - People ask you questions their manager should be answering — the manager isn't communicating
> - The most talented people seem disengaged — flight risk is high

---

## Manager Accountability

Fournier states the universal goal for manager relationships: **"they should make your life easier."** Managers exist to take teams and help those teams succeed. When they repeatedly fail, they're failing at their job.

But: "sometimes managers make your life easier by hiding problems and telling you what you want to hear."

Three scenarios, all with the same answer — **yes, the manager is accountable:**

**1. Unstable product roadmap.** The team is unproductive and attriting, but the product org keeps changing goals. Is the manager accountable? **Yes** — the manager should identify the disruption, work with product to refocus, and escalate to you if that fails.

**2. Errant tech lead.** The TL has been down a rabbit hole for months. No design doc, work piling up. **Yes** — the manager should bring the TL out and help make the design process transparent.

**3. Full-time firefighting.** Legacy systems constantly breaking, team consumed by support. **Yes** — the manager should create a plan to address root causes and come to you with resource requests.

In many cases, **you'll need to help your managers:** provide organizational clout, find mentors for struggling TLs, approve headcount requests. "This is what making your job easier looks like — not hiding information, but bringing you clear problems before they turn into raging fires."

> **[Deep Dive: Accountability vs. Blame in SRE Management]**
>
> Fournier's accountability framework maps directly to SRE management challenges:
>
> | Scenario | Manager's Accountability |
> |----------|------------------------|
> | Team is drowning in incidents | Create a plan to reduce incident sources. Come to you with data and resource request if needed. NOT acceptable: "the systems are just old" with no plan. |
> | On-call engineer is burning out | Detect it through 1-1s and on-call metrics. Redistribute burden, adjust rotation, or escalate capacity need. NOT acceptable: being surprised when the person quits. |
> | Reliability project is behind schedule | Identify the blockers early, communicate revised timeline, propose scope cuts. NOT acceptable: silence followed by "we need 3 more months." |
> | Product team ignoring SLO violations | Escalate with data. Work with product to reprioritize. Come to you for organizational support if peer conversation fails. NOT acceptable: complaining about the product team without having tried to resolve it. |
>
> **The key phrase:** Accountability means "identify the problem, create a plan, bring it to me if you need help." It does NOT mean "solve everything alone without ever escalating."

> **[Script: Holding a Manager Accountable]**
>
> Your SRE manager's team has missed delivery on a reliability improvement for the second consecutive quarter. In your 1-1:
>
> *"I want to talk about the observability project. This is the second quarter it's slipped. I'm not looking to assign blame — I'm looking to understand what's happening and how I can help.*
>
> *Walk me through what caused the slip this quarter. Was it scope, capacity, unexpected work, or something else?*
>
> [Listen. Then:]
>
> *What I need from you is a realistic assessment: given what you now know, what does the path to completion look like? If you need something from me — air cover from product requests, additional engineers, scope reduction — tell me now. What I can't accept is another quarter of 'we'll try harder.' I need a plan that accounts for the things that derailed us this time."*
>
> **Why this works:** It separates accountability from blame. It asks for root cause analysis. It offers help. And it sets a clear expectation: a plan, not just effort.

---

## Ask the CTO: My Tech Lead Isn't Managing

A manager discovers that a tech lead hasn't followed up on design review feedback or created a project plan for a junior engineer. How to handle it without stepping in?

Fournier's diagnosis:
1. **TL is busy and forgot** — remind her that mentoring/oversight needs to be scheduled alongside code
2. **TL doesn't know how to push the junior** — coach her on how to ask for deliverables, even when it feels uncomfortable

"The best thing to do here is to work with your tech lead to give her the skills and confidence to ask for reports from other members of the team. It will be slower than stepping in and asking for them yourself, but you'll teach the team to respect her requests and teach her how to lead the team independently."

> **[Insight]** This sidebar illustrates a meta-principle of managing managers: **always coach through the manager, not around them.** When you step in and fix the problem directly, you've solved the immediate issue but created three new ones: (1) the TL didn't learn, (2) the team learns to go around the TL to you, (3) the TL's authority is undermined. The slower path — coaching the TL to handle it — is always the right investment unless the situation is urgent and the person is at risk.

> **[Anti-Pattern: The Bypass]**
>
> You discover a problem on one of your manager's teams. Instead of telling the manager and coaching them to fix it, you directly intervene — you talk to the engineer, you attend the team's standup, you reassign work. The manager finds out from their team, not from you.
>
> **Why this happens:** It's faster. You see the problem clearly. The manager seems overwhelmed. You're "just helping."
>
> **Why it's devastating:** The manager's authority is destroyed. The team learns that the real decision-maker is you, and their manager is just a proxy. The manager either becomes passive ("why bother if you're going to do it yourself?") or resentful. Future managers you hire will hear about this pattern and be reluctant to join.
>
> **The rule:** Problems on a manager's team go THROUGH the manager, except: (1) the problem IS the manager, (2) there's an urgent safety/ethical issue, or (3) the manager has explicitly asked you to step in. In every other case, coach the coach.

---

*Continued in [Part 2](ch07-notes-managing-managers-part2.md): The people pleaser, managing new managers, managing experienced managers.*
