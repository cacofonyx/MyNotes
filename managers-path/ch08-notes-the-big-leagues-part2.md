# Chapter 8: The Big Leagues — Part 2

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 2 covers:** Changing priorities, setting strategy, delivering bad news, managing a nontechnical boss.
See [Part 1](ch08-notes-the-big-leagues-part1.md) for: leadership models, VP/CTO roles.
See [Part 3](ch08-notes-the-big-leagues-part3.md) for: senior peers, the echo, fear/trust, True North.

## Table of Contents — Part 2

- [Changing Priorities](#changing-priorities)
- [Setting the Strategy](#setting-the-strategy)
- [Challenging Situations: Delivering Bad News](#challenging-situations-delivering-bad-news)
- [Ask the CTO: I Have a Nontechnical Boss](#ask-the-cto-i-have-a-nontechnical-boss)

**Block types in Part 2:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Go Deeper]

---

## Changing Priorities

Fournier describes a common scenario: the CEO has a revelation, shares a new vision, the leadership team agrees — but the engineering teams are slow to shift because they have in-flight projects. "So, why aren't you working on the top priority?"

**Key insight:** "Leaders who are removed from the day-to-day schedules of the teams can forget that teams have long priority lists... and may take weeks or months to complete."

**How to handle priority shifts:**

1. **Do you know what the top priority is?** Does your team? If not, it's a communication problem. Saying something is top priority isn't enough — you must "go through the list of things in flight and kill or postpone work in order to make room."

2. **Push both up and down.** If current work should be finished first, make the case with data: value, status, timeline. But "expect that you'll probably need to compromise."

3. **Communicate relentlessly.** "Never underestimate how many times and how many ways something needs to be said before it sinks in." Tell leadership, hold an all-hands, send email. Prepare for questions. **The three-times rule:** "In my experience, most people need to hear something at least three times before it really sinks in."

4. **"You need to repeat information when you're communicating up."** When you want your boss to act, expect to raise the issue three times before getting traction.

> **[SRE Lens: Priority Changes and SRE]**
>
> SRE teams face unique priority-change challenges:
>
> - **Reliability work is easily deprioritized** when business priorities shift. "We need all hands on the new product launch" often means SRE reliability projects get shelved. Your job: articulate the cost of deferring reliability work in business terms.
> - **Incidents don't respect priority changes.** A P1 outage interrupts the new priority just as easily as the old one. Build this into the timeline you communicate upward.
> - **SRE teams can be the stability anchor.** When everything else is shifting, maintaining operational stability provides the foundation for the priority change to succeed. Frame SRE work as "enabling the new priority" rather than "competing with the new priority."

> **[Script: Communicating a Priority Change to Your Teams]**
>
> *"I want to share a significant change in our priorities. Starting next sprint, [new priority] is becoming our top focus. Here's why: [business context — customer impact, market opportunity, executive directive].*
>
> *What this means for current work: [Project A] will continue — it's 80% done and the remaining work is on the critical path. [Project B] is being paused — we'll pick it up in Q3. [Project C] is being descoped to [reduced version].*
>
> *I know this is frustrating, especially for those who've been deep in Project B. I want you to know that I advocated for completing it, and the work you've done isn't wasted — it'll resume when the timing is right. Right now, [new priority] is what the business needs most, and I need your help making it successful.*
>
> *Questions? Concerns? I'd rather hear them now than have them simmer."*

---

## Setting the Strategy

Fournier shares her personal story of being pushed by her CEO to create a technology strategy for a board presentation. The CEO "returned every attempt I made" until Fournier finally produced something that met her standards. This was a transformational experience.

**Her process:**

**1. Do a lot of research.** Ask the engineering team about pain points. Ask executives about future growth. Consider scaling challenges, productivity bottlenecks, technology landscape changes.

**2. Combine research and ideas.** Sit alone with a whiteboard. Draw out current systems. Slice them across different attributes (customer-facing vs. internal, backend vs. frontend). Look for patterns and opportunities.

**3. Draft a strategy.** Turn the mapping into actionable ideas. Consider how systems should evolve, what information sharing to limit or expand, how architecture enables business futures.

**4. Consider communication style.** Fournier's first draft was too technical and lacked forward-thinking ideas. Her slide deck was too sparse for a board that reads decks before meetings. Lesson: match communication to the audience.

**Key insight:** "Good technology strategy... 'enables the many potential futures of the business.' It's not just a reactive document that tries to account for current problems, but it anticipates and enables future growth."

> **[Deep Dive: Technology Strategy for SRE]**
>
> An SRE technology strategy should cover:
>
> **1. Reliability as business enabler:**
> - How does reliability enable the company's growth plans? (Geographic expansion needs latency optimization. 10x user growth needs capacity planning. New product lines need reliability foundations.)
> - What's the cost of unreliability to the business? (Quantified: revenue loss, customer trust, engineering toil.)
>
> **2. Platform evolution:**
> - Where is the observability stack heading? (Consolidated telemetry, AI-assisted incident detection, self-healing systems.)
> - Where is the deployment infrastructure heading? (Progressive delivery, feature flags, canary analysis.)
> - What's the buy vs. build analysis for major tooling?
>
> **3. Organizational evolution:**
> - How should SRE team structure evolve as the company grows? (Embedded vs. centralized? Platform engineering integration?)
> - What skills does the team need in 2 years that it doesn't have today?
> - What's the hiring plan?
>
> **4. Maturity roadmap:**
> - Where is each product team on the SRE maturity curve? (No SLOs → basic SLOs → error budgets → self-service reliability.)
> - What's the plan to advance each team?
>
> **Fournier's lesson applied:** The strategy isn't just "what systems to build." It's "how does our technical approach enable the business to succeed in multiple possible futures." For SRE: "how does our reliability approach ensure the business can grow, pivot, and compete without operational risk being the limiting factor."

> **[Leader's Playbook: Writing Your First Strategy Document]**
>
> 1. **Start with the business, not the technology.** What does the company need to achieve in the next 1-3 years? Revenue targets? Market expansion? New products? This is your north star.
> 2. **Map current state honestly.** What systems exist? Where are the bottlenecks? What's fragile? What's over-engineered? Don't sugarcoat.
> 3. **Identify the gaps.** Where does current state fail to support future needs? These gaps are your strategic priorities.
> 4. **Propose 3-5 initiatives.** Not 20. Each should: enable a business goal, have a measurable outcome, and be achievable within 12-18 months.
> 5. **Address team and process, not just systems.** Strategy includes hiring, skills development, organizational structure, and process changes.
> 6. **Get feedback before presenting.** Share with peers, senior engineers, your manager. Iterate.
> 7. **Present to non-technical audiences in business language.** Impact, cost, risk, timeline — not system architecture diagrams.

---

## Challenging Situations: Delivering Bad News

Fournier addresses delivering bad news: layoffs, team disbandments, unpopular policy changes, roadmap changes.

**Dos and Don'ts:**

**Don't: Blast an impersonal message to a large group.** Email and chat are the worst. Even all-hands can backfire — "one or two deeply unhappy members can quickly rile up the whole team."

**Do: Talk to individuals as much as possible.** Think about who'll react strongest. Give them 1-1 time to react and ask questions. For org-wide news: tell managers first with talking points → they tell their teams → then bring the whole group together.

**Don't: Force yourself to deliver a message you can't stand behind.** If you can't deliver without betraying strong disagreement, get help — another executive, HR, a trusted lieutenant.

**Do: Be honest about likely outcomes.** If there are layoffs, acknowledge it's not fun but the company needs to survive. If a team is disbanded, point out accomplishments AND new opportunities.

**Do: Think about how you would like to be told.** Personal, face-to-face where possible, with grace.

> **[Script: Delivering News of a Team Restructure]**
>
> Your SRE team is being split — half will be embedded into product teams, half will form a platform engineering team. You know some people will hate this.
>
> **Step 1: Talk to managers first.** Give them 24 hours to process before they need to tell their teams. Provide talking points.
>
> **Step 2: Talk to key individuals.** The senior engineers who will be most affected. 1-1s before the broader announcement.
>
> **Step 3: Team announcement:**
> *"I want to share a change in how our SRE organization will be structured. Starting [date], we're moving to a model where [description]. Here's why: [business reason — product teams need tighter reliability integration; platform work needs dedicated focus].*
>
> *I want to be direct about what this means: some of you will move to product teams as embedded SREs. Others will form the new platform engineering team. I've tried to match people to the roles that best fit their skills and interests, but I know not everyone will be happy with the initial assignment.*
>
> *What I can promise: nobody is losing their job. Your compensation doesn't change. Your manager will work with you on the transition. And if your initial assignment truly doesn't work after 3 months, we'll revisit.*
>
> *I know this is a lot to process. Take the rest of today to think. Your managers are available for 1-1s. I'm available too. Let's talk tomorrow about how to make this transition successful."*

---

## Ask the CTO: I Have a Nontechnical Boss

Fournier shares her experience reporting to the CEO (her first nontechnical boss). Best practices:

- **Don't hide behind jargon.** Your boss is smart but doesn't need technical details.
- **Run your own 1-1s.** Come prepared. Busy executives are hard to pin down.
- **Bring solutions, not problems.** CEOs don't want to hear about failures or peer disagreements. But don't shy from bad news.
- **Ask for advice.** "Nothing shows respect like asking for someone's advice."
- **Don't be afraid to repeat yourself.** Three times is the magic number for getting traction.
- **Be supportive.** Ask how you can help.
- **Find coaching elsewhere.** "You no longer have a manager; you have a boss." Get a coach, training, or peer group.

> **[Insight]** "You no longer have a manager; you have a boss." This distinction is profound. A manager develops you, coaches you, gives you feedback. A boss sets expectations and evaluates results. At the senior level, you need to find your own development — through coaches, peer groups, and self-reflection. If you wait for your nontechnical CEO to develop your management skills, you'll wait forever.

---

*Continued in [Part 3](ch08-notes-the-big-leagues-part3.md): Senior peers, the echo, fear vs. trust, True North.*
