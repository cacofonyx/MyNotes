# Chapter 6: Managing Multiple Teams — Part 2

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 2 covers:** Strategies for saying no, technical elements beyond code, measuring team health, us-versus-them vs. team player, laziness and impatience as virtues, chapter assessment.
See [Part 1](ch06-notes-managing-multiple-teams-part1.md) for: Director role, staying hands-on, time management, delegation.

## Table of Contents — Part 2

- [Challenging Situations: Strategies for Saying No](#challenging-situations-strategies-for-saying-no)
- [Technical Elements Beyond Code](#technical-elements-beyond-code)
- [Measuring the Health of Your Development Team](#measuring-the-health-of-your-development-team)
- [Good Manager, Bad Manager: Us Versus Them, Team Player](#good-manager-bad-manager-us-versus-them-team-player)
- [The Virtues of Laziness and Impatience](#the-virtues-of-laziness-and-impatience)
- [Assessing Your Own Experience](#assessing-your-own-experience)
- [Quarterly Ritual: Multi-Team Director Health Check](#quarterly-ritual-multi-team-director-health-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping Multi-Team Management](#how-genai-is-reshaping-multi-team-management)

**Block types in Part 2:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Influence Without Authority] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## Challenging Situations: Strategies for Saying No

Fournier identifies saying no as a core management skill at this level: to your team, your peers, and your boss. Six strategies:

**1. "Yes, and"** — from improv comedy. "Yes, we can do that project, and all we will need to do is delay the start of this other project." Transforms "no" into a negotiation about priorities. "Responding with positivity while still articulating the boundaries of reality will get you into the major leagues of senior leadership."

**2. Create policies.** When you're repeating the same "no" for the same reasons, extract the reasoning into a policy — the set of requirements for getting to "yes." Example: adopting a new language requires demonstrating production readiness, logging standards, testing patterns, and team proficiency.

**3. "Help me say yes."** For one-off cases without a clear policy. Ask questions that dig into the questionable parts. "Often, this line of questioning helps people come to the realization themselves that their plan isn't a good idea."

**4. Appeal to budget.** Lay out the current workload in plain terms. Show there's no room. Can be paired with "not right now" — but be careful: if you promise "later," later must actually happen.

**5. Work as a team.** Use cross-functional alliances. Sometimes your technical authority supports the product team's "no," and vice versa. "Playing good cop/bad cop can be a little bit dishonest, so use this sparingly."

**6. Don't prevaricate.** When you know the answer is no, say it quickly. "You'll be wrong sometimes, so when you discover that you were too quick to say no, apologize."

> **[SRE Lens: Saying No in SRE]**
>
> SRE teams are perpetual targets for scope creep — "can you also support this service?" "can you run this migration for us?" "can we skip the readiness review for this launch?"
>
> **Applying Fournier's strategies to SRE:**
>
> - **"Yes, and":** "Yes, we can onboard your new service, and we'll need your team to complete the production readiness checklist, carry primary on-call for the first 3 months, and contribute to the monitoring setup."
> - **Policy:** Create a formal production readiness review process. Document what's required for SRE support. This turns "no" into "not yet — here's what's needed."
> - **"Help me say yes":** "You want to skip load testing before the launch? Help me understand — what's our rollback plan if the service can't handle the traffic? How will we detect degradation? Who's on-call for the first 48 hours?" Let them discover their own gaps.
> - **Appeal to budget:** "Our team has 30 engineer-weeks of project capacity this quarter. Here's what we've committed to. To take on this new request, which of these should we deprioritize?"

> **[Script: Saying No to Your VP]**
>
> Your VP wants your SRE team to support a new product initiative that starts next month. You don't have capacity.
>
> *"I'm excited about this initiative, and I want SRE to support it well. Here's where we stand on capacity: we have 3 committed projects this quarter plus ongoing on-call for 12 services. Taking on this new initiative at full support would mean either deprioritizing [Project X — the reliability improvement for the payments service] or accepting reduced SRE support for the initiative — embedded consulting instead of full ownership.*
>
> *My recommendation is option B: we provide embedded consulting for the first 3 months while the product team carries primary on-call, then evaluate full SRE ownership in Q3 when [Project X] completes. This gets the initiative SRE guidance without sacrificing the reliability work that prevents the kind of payments outage we had in March.*
>
> *Does this approach work, or would you like me to present the full tradeoff analysis for deprioritizing one of the committed projects?"*

---

## Technical Elements Beyond Code

Fournier challenges the assumption that the Director job becomes "essentially nontechnical." It's technical — just differently technical. Your technical focus shifts from writing code to **observing and improving the systems of work that your developers operate within.**

She references *First, Break All the Rules* (Buckingham & Coffman), which identifies three predictive questions for team productivity:

1. **Do I know what is expected of me at work?** → if work is clear, engineers know what code to write
2. **Do I have the materials and equipment I need to do my work right?** → if tools, tickets, automation, and process are available, they can get the work done
3. **Do I have the opportunity to do what I do best every day?** → if not distracted by meetings or drowning in support, they write code daily

The health signals that answer these questions: **frequency of code releases, frequency of code check-ins, and infrequency of incidents.**

> **[Mental Model: The Three Health Signals as SLOs for Your Organization]**
>
> Fournier is essentially proposing organizational SLOs. Map them:
>
> | Signal | What It Measures | SRE Parallel |
> |--------|-----------------|--------------|
> | **Release frequency** | Speed of value delivery | Deployment frequency (DORA metric) |
> | **Code check-in frequency** | Work decomposition quality | Change lead time (DORA metric) |
> | **Incident frequency** | System quality and stability | Change failure rate + MTTR (DORA metrics) |
>
> DORA research (Forsgren, Humble, Kim) confirms Fournier's intuition with data: these metrics predict both organizational performance and team satisfaction. They're not just technical metrics — they're people metrics.

---

## Measuring the Health of Your Development Team

### Frequency of Releases

Fournier is emphatic: "frequency of code change is one of the leading indicators of a healthy engineering team." Teams that don't release frequently reveal cracks: long release processes, engineers who don't feel ownership over quality, slow rollbacks, release-induced incidents.

Even for products that can't release to users frequently (like databases), there should be a "complete artifact pushed to a beta/developer testing environment that provides a similarly valuable measure."

Her challenge to managers who say they don't have time: "Is your team working to its full capacity? Are your engineers challenged and growing? Is your product team excited by the progress you're making?" If not, release frequency is likely a contributing factor.

### Frequency of Code Check-ins

Engineers need to break work into small chunks. TDD helps with this skill. "Engineers who want to go off for weeks and write code alone without pushing it into shared version control will slow your team down."

### Frequency of Incidents

Balance is key. Too many incidents = poor quality, burning engineers out. Too much focus on incident prevention = slow processes, idle developers. "The goal here is to balance risk in such a way that neither incident frequency nor incident prevention turns into a job that takes developers away from writing code for days at a time."

On-call: if your team does its own incident management, move yourself to an escalation role. But stay in the loop.

> **[SRE Lens: The SRE Director as Organizational SRE]**
>
> This section is the heart of the SRE Director's job. You're not doing SRE for services anymore — you're doing SRE for the engineering organization itself.
>
> **Your dashboards should include:**
> - Deployment frequency per team (trending up = healthy)
> - Change failure rate per team (should be <15% per DORA research)
> - Mean time to recovery per team
> - On-call burden: pages per rotation, after-hours pages, escalation rate
> - Toil percentage: what fraction of team time goes to repetitive manual work
> - Sprint completion rate: are teams consistently hitting their commitments
> - Engineering satisfaction scores (if available)
>
> **The Director's diagnostic loop:**
> 1. Look at dashboards weekly — spot anomalies
> 2. Dig into anomalies in 1-1s with managers — understand root causes
> 3. Address systemic issues through process changes, resource reallocation, or tooling investment
> 4. Measure again next quarter — did the intervention work?
>
> You're running the same observe → hypothesize → experiment → measure loop that SRE uses for services, but the "service" is your organization.

---

## Good Manager, Bad Manager: Us Versus Them, Team Player

Fournier contrasts two managers joining startups with messy teams:

**Diana (us-vs-them):** Hires a bunch of people from her previous company. Creates a clique that sees itself as better than the rest of the organization. Technology improves but they clash with product. After a year, Diana quits, and her clique follows. Company is back to square one.

**Neil (team player):** Moves cautiously on firings. Has new hires vetted by existing team members. Works closely with product peers. Focuses on cross-functional collaboration, clear goals. "Things start out slow, but over time the entire organization feels stronger."

Fournier identifies Diana's approach as **"shallow binding"** — identity built around job function superiority. Its dysfunctions:
- Fragile to loss of leader (clique dissolves)
- Resistant to outside ideas
- Empire building
- Inflexible to organizational change

Neil's approach is **"purpose-based binding"** — aligned to company mission and values. Its strengths:
- Resilient to loss of individuals
- Driven to find better ways
- **First-team focused** — peers across the company are your first team, not your direct reports
- Open to changes that serve the purpose

> **[Insight]** "First-team focused" is one of the most important concepts in this book. Your first team is NOT your direct reports. It's your peer group — other Directors, your product counterpart, your VP. This feels counterintuitive because your reports feel like "your people." But as Fournier explains, if you optimize only for your team, you sub-optimize for the company. First-team focus means you make decisions that are best for the overall organization, even when they're not best for your specific team. This is the Director-level version of "be kind, not nice" from Ch5.

> **[SRE Lens: The SRE Us-vs-Them Trap]**
>
> SRE teams are especially vulnerable to us-vs-them dynamics because:
> - SRE often has a gatekeeper role (production readiness reviews, SLO enforcement)
> - SRE teams see the consequences of bad engineering decisions (incidents), creating a sense of "we clean up their messes"
> - SRE culture valorizes operational expertise, which can create a superiority complex toward product engineers who "don't understand production"
>
> **The fix:** SRE Directors must actively model partnership. Publicly praise product teams' reliability improvements. Attend product team celebrations. Frame SRE's role as "enabling product teams to ship reliably" not "protecting production from product teams." Use language like "our customers" not "our systems."

> **[Mental Model: First Team (Patrick Lencioni)]**
>
> From *The Five Dysfunctions of a Team:* Leaders' "first team" is their peer group, not their direct reports. When Directors optimize for their own team at the expense of the broader organization, the result is silos, resource hoarding, and misalignment.
>
> **For SRE Directors specifically:** Your first team is the engineering leadership group (other Directors, VP of Engineering, Product leadership). When there's a conflict between what's best for your SRE team and what's best for the engineering organization, the org wins. This might mean lending SRE engineers to a product team for a critical launch, even though it's inconvenient for your team's roadmap.

---

## The Virtues of Laziness and Impatience

Fournier channels Larry Wall's famous engineering virtues: "laziness, impatience, and hubris."

For managers, **impatience directed at processes and decisions** (not at people) is a virtue. Whenever something feels inefficient, question it: What is the value? Can we deliver it faster? Can we strip it down?

But "faster" does NOT mean "same number of hours but fewer total days." **"Faster is about the same value to the company in less total time."** If the team works 60 hours in a week, they haven't worked faster — "they've just given the company more of their free time."

Two practices to model:
1. **Figuring out what's important** — constantly asking: can this be done faster, do I need to be doing this at all, what value am I providing?
2. **Going home** — "Go home! And stop emailing people at all hours!" When you overwork, your team thinks it's expected. This makes them less effective.

> **[Leader's Playbook: Modeling Sustainable Pace]**
>
> - **Don't send messages outside business hours.** If you must work late, use scheduled send.
> - **Take vacation visibly.** When you take PTO, actually disconnect. Tell the team you're offline.
> - **When someone works late, ask why.** Not to praise ("wow, you're so dedicated") but to diagnose ("is there a workload problem?").
> - **Set explicit expectations.** "I do not expect you to respond to Slack after 6 PM or on weekends. If something is truly urgent, I'll call you."
> - **Track work hours if needed.** If your team is consistently working >45 hours, that's a capacity problem to solve, not a dedication metric to celebrate.

---

## Assessing Your Own Experience

Fournier's self-reflection questions, with Senior EM/Director commentary:

- **When did you last review your schedule?** If you can't identify what you accomplished last week, your time is being consumed by low-value activity.
- **If you're still writing code, how does it fit?** Are you doing it after hours? That's a warning sign — either you haven't delegated enough or you're using code as an escape.
- **What was the last task you delegated?** Was it simple or complex? If you only delegate simple tasks, you're not developing your people.
- **Who are your rising leaders?** What's your plan for developing them? If you don't have one, that IS the plan — to not develop leaders.
- **Does writing, releasing, and supporting code function smoothly?** When was the last notable incident in this process?
- **When did you last cut scope?** Did you cut features, technical quality, or both?
- **When did you last send email after 8 PM?** Did the recipient respond? Did you need them to?

---

## Quarterly Ritual: Multi-Team Director Health Check

> **[Quarterly Ritual]**
>
> **Organizational Health (across all teams):**
> - [ ] What are the DORA metrics for each team? (Deployment frequency, lead time, change failure rate, MTTR)
> - [ ] Are any teams significantly underperforming compared to others? Why?
> - [ ] What's the attrition rate and engagement score per team?
> - [ ] Is on-call burden distributed fairly across teams?
>
> **Delegation Health:**
> - [ ] List the tasks only you can do. Is this list shorter than last quarter?
> - [ ] Who are the rising leaders? What new responsibilities have you given them this quarter?
> - [ ] Could your teams operate for 2 weeks without you? If not, what's the dependency?
>
> **Time Management:**
> - [ ] How many hours/week do you spend in meetings? Is it increasing?
> - [ ] How much time did you spend on strategic (important-not-urgent) work this quarter?
> - [ ] Did you protect your creative/thinking time, or did it get eaten by meetings?
>
> **Cross-Functional Health:**
> - [ ] Is your first team your peers, or your direct reports? (Be honest.)
> - [ ] How is the relationship between your teams and their product/business counterparts?
> - [ ] Have you created any us-vs-them dynamics, even unintentionally?
>
> **Culture Health:**
> - [ ] Are you modeling sustainable pace? When did you last send a late-night message?
> - [ ] What's the average PTO usage on your teams? Are people actually disconnecting?
> - [ ] Would your team describe you as "lazy and impatient" (in Fournier's positive sense) or "overworked and accommodating"?

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"If your VP asked you right now what your three teams' biggest risks are, could you answer immediately — with specifics, not generalities?"** If yes, you're plugged in. If you'd need to check with your managers first, you may have delegated observation, not just execution. Directors must maintain a mental model of each team's state.
>
> 2. **"Think about the last time you said 'yes' to a project or request you should have said 'no' to. What was the real reason you said yes? Was it because it was the right call, or because saying no felt too uncomfortable?"** Most Director-level over-commitment comes from conflict avoidance, not misjudgment.
>
> 3. **"When was the last time you went home at a reasonable hour and felt genuinely good about what you accomplished that day?"** If you can't remember, you either have a workload problem or a satisfaction problem. Both need attention.
>
> 4. **"Are your teams united by shared purpose or by shared opposition?"** Teams that bond over complaining about product, or about the company, or about other teams — that's shallow binding. Teams that bond over their mission and impact — that's durable. Which kind are yours?

---

## How GenAI Is Reshaping Multi-Team Management

> **[GenAI + Multi-Team Management]**

**AI and Time Management:** AI assistants can help Directors with the administrative overhead that consumes time: summarizing meeting notes, drafting status updates, preparing agendas, analyzing calendar data for time allocation patterns. This frees time for the strategic work Fournier emphasizes.

**AI and Delegation:** AI can help rising leaders who are taking on delegated tasks. A new tech lead writing their first project plan can use AI to draft it, which lowers the barrier to delegation — you're less worried about the quality of the output when there's a capable AI assisting.

**AI and Team Health Signals:** AI can analyze code repositories (commit frequency, PR cycle time, code churn), communication patterns (Slack activity, meeting frequency), and operational data (incident trends, on-call burden) to surface team health signals automatically. This extends the Director's observability into areas that are hard to monitor manually across multiple teams.

**AI and Saying No:** AI can help analyze capacity and present tradeoff data clearly. When you need to say "yes, and" to a VP, having an AI-assisted capacity model that shows exactly what would need to shift makes the conversation concrete rather than abstract.

**The meta-question:** As AI handles more routine management tasks, Directors should spend MORE time on the uniquely human work: building relationships, coaching managers, navigating organizational politics, and making judgment calls under uncertainty. If AI is doing your status reports, what are you doing with the reclaimed time?

**Further reading for Chapter 6:**
- [*Getting Things Done* by David Allen](https://www.goodreads.com/book/show/1633.Getting_Things_Done) — Fournier's recommended time management framework
- [*First, Break All the Rules* by Buckingham & Coffman](https://www.goodreads.com/book/show/50937.First_Break_All_the_Rules) — the research on team productivity signals
- [*The Five Dysfunctions of a Team* by Patrick Lencioni](https://www.goodreads.com/book/show/21343.The_Five_Dysfunctions_of_a_Team) — first-team focus and trust
- [*Accelerate* by Forsgren, Humble, Kim](https://www.goodreads.com/book/show/35747076-accelerate) — DORA metrics research on deployment and team performance
- Paul Graham's "Maker's Schedule, Manager's Schedule" — foundational essay on time management for technical leaders (free online)
- [*An Elegant Puzzle* by Will Larson, Ch. 2-3](https://press.stripe.com/an-elegant-puzzle) — covers team sizing, organizational design, and systems thinking for engineering management
