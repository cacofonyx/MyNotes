# Chapter 5: Managing a Team — Part 1

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "It's a short step from managing a person or two to managing a whole team, but managing a team is more than just doing the job of managing the individuals." — Fournier

This is where management fundamentally shifts. Chapters 1-4 were about managing *people*. Chapter 5 is about managing a *team* — a system of people, processes, and technology that must produce outcomes greater than the sum of its parts. Fournier explicitly says the theme is "the job beyond people management" — the technical, strategic, and leadership dimensions that new managers underinvest in because they're overly focused on the people side.

For a Senior EM, this chapter is your current operating level. You've already internalized the people management of Ch4. Now: can you lead a team as a system? Can you stay technical enough to be credible? Can you debug organizational dysfunction the way you'd debug a production system? Can you be the right kind of shield without becoming a helicopter parent?

**Part 1 covers:** Becoming a people manager, staying technical, debugging dysfunctional teams, the shield concept, and managing former peers.
**Part 2 covers:** Driving good decisions, conflict management, team cohesion destroyers, advanced project management, and joining a small team.

## Table of Contents — Part 1

- [The Job Has Changed](#the-job-has-changed)
- [Becoming a People Manager](#becoming-a-people-manager)
- [Staying Technical](#staying-technical)
- [Debugging Dysfunctional Teams: The Basics](#debugging-dysfunctional-teams-the-basics)
  - [Not Shipping](#not-shipping)
  - [People Drama](#people-drama)
  - [Unhappiness Due to Overwork](#unhappiness-due-to-overwork)
  - [Collaboration Problems](#collaboration-problems)
- [The Shield](#the-shield)
- [Ask the CTO: Managing a Former Peer](#ask-the-cto-managing-a-former-peer)
- [Quarterly Ritual: Team Health Diagnostic (Part 1)](#quarterly-ritual-team-health-diagnostic-part-1)
- [Peer Reflection Prompt (Part 1)](#peer-reflection-prompt-part-1)

**Block types in Part 1:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Influence Without Authority] [First 90 Days] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## The Job Has Changed

Fournier opens with the engineering lead job description she used, which is worth examining because it encodes her philosophy of what team management IS:

> "The engineering lead will spend less time writing code, but they still engage in small technical deliverables, such as bug fixes and small features, without blocking or slowing down the progress of their team. More than writing code, they hold responsibility for identifying bottlenecks in the process and roadblocks to success for their team and clearing these roadblocks."

She further describes this person as: identifying high-value projects and keeping the team focused, partnering with product on scope, recruiting, managing across skill sets, communicating expectations, soliciting and delivering feedback frequently, leading the technical roadmap, communicating timelines/scope/risks, and identifying strategic technical debt with cost/benefit analysis.

> **[Insight]** Read that job description again. It's not a people management job. It's a *systems integration* job. The engineering lead is the node that connects: the technical system (code, architecture, debt), the people system (skills, growth, dynamics), the product system (roadmap, customers, scope), and the organizational system (stakeholders, resources, timelines). No other role sits at this intersection. Your value isn't in any one of those domains — it's in being the integrator. If you're spending all your time in one domain (usually people management for new managers, or technical work for promoted engineers), you're failing the integrator role.

> **[Senior EM vs. Director: The Integration Job]**
>
> | Dimension | Senior EM (Team Lead) | Director |
> |-----------|----------------------|----------|
> | **Technical integration** | Hands-on enough to smell technical problems; guides architecture decisions for your teams | Sets technical direction across teams; holds architects and TLs accountable for decisions |
> | **People integration** | Manages individuals, develops TLs and senior ICs | Manages managers; builds the people-development system itself |
> | **Product integration** | Partners with one product manager on scope and priorities | Partners with product leadership on strategy; balances competing product demands across teams |
> | **Org integration** | Communicates up (status, risks) and down (context, priorities) | Shapes org structure; influences resource allocation; represents the function in leadership forums |
> | **Time horizon** | This quarter's execution | This year's strategy, next year's vision |

> **[Mental Model: The Manager as System Operator]**
>
> Think of your team as a production system. You are the SRE for that system. Apply the same diagnostic thinking:
>
> - **Observability:** Do you have signals for team health (engagement, velocity, attrition risk, on-call burden)? Or are you flying blind until someone quits?
> - **SLOs:** What are your team's "SLOs"? Delivery velocity, quality (bugs/incidents), retention, satisfaction? Are they defined and measured?
> - **Incident response:** When something goes wrong (missed deadline, interpersonal conflict, burnout), do you have a playbook, or do you improvise every time?
> - **Capacity planning:** Are you managing team capacity like you'd manage infrastructure capacity — with headroom, with forecasting, with a plan for scaling?
> - **Toil reduction:** What repetitive management overhead could be automated or eliminated? Status meetings that could be async? Approval chains that could be delegated?
>
> **The parallel isn't perfect** — people aren't servers — but the diagnostic mindset transfers powerfully. The best engineering managers apply systems thinking to human systems, while remembering that the "components" have feelings, aspirations, and agency.

---

## Becoming a People Manager

Fournier shares bethanye Blount's story of transitioning from informal team lead to official people manager in a company that had previously resisted managers. Key details:

- The role was new to the company; everyone was uncertain
- Some reports were comfortable with the transition, others weren't
- Blount managed engineers far more senior technically than herself — "It was the first time that I couldn't rely on having the most knowledge as my main leadership tool"
- One senior engineer was collaborative and gave ongoing feedback; the other couldn't adjust, transferred away, then returned months later

The takeaway: **"Being a good manager isn't about having the most technical knowledge. The work of supporting people was far more important to management success."**

> **[Insight]** Blount's story is deceptively simple but contains a profound lesson: the two senior engineers had the same situation (a less-technical peer becoming their manager) but different outcomes. The difference wasn't about Blount — it was about *their* ability to accept a new relationship dynamic. This is important for you as a Senior EM because you will create these dynamics regularly: promoting someone over their peers, restructuring teams, changing reporting lines. The people who struggle aren't necessarily wrong — they're processing a relationship change, and that takes time. The engineer who left and came back? That's a healthy arc. He needed to try something else to realize the original situation was fine.

> **[SRE Lens]** In SRE specifically, the "less technical than your reports" dynamic is extremely common. You may manage specialists in areas you've never worked in: kernel performance engineers, network infrastructure experts, database reliability engineers. Your value isn't out-debugging them. It's removing obstacles, securing resources, translating their work's impact to leadership, and ensuring they have the organizational air cover to do deep technical work. The moment you try to prove you're the smartest person in the room, you've lost.

> **[Anti-Pattern: The Technical Imposter]**
>
> You're a new engineering manager who was promoted from a different specialty. Your team includes a senior engineer who knows far more about distributed systems than you do. In meetings, you find yourself over-explaining technical points to prove you belong. You second-guess their design decisions, not because you have better ideas, but because agreeing too quickly feels like admitting you don't understand. You start attending deep technical meetings you don't need to be in, "just to stay in the loop."
>
> **Why this is destructive:** Your senior engineer sees through it. They interpret your behavior as distrust or micromanagement. Worse, you're spending time performing technical credibility instead of doing the management work only you can do — clearing roadblocks, securing headcount, building cross-team alignment.
>
> **The fix:** Explicitly own the dynamic. Tell your senior engineer: "You're the technical authority here. I'm going to rely on you for technical decisions. My job is to make sure you have what you need, and to represent our work to the rest of the org. If I ask dumb questions, it's because I need enough context to advocate for your work effectively — not because I'm second-guessing you."

> **[Script: Acknowledging the Skill Gap]**
>
> In your first 1-1 with a report who is significantly more technical:
>
> *"I want to be upfront about something — you have deeper expertise in [distributed tracing / kernel performance / database internals] than I do. That's not going to change, and I'm not going to pretend otherwise. What I bring is a different set of skills: I can clear organizational obstacles, advocate for resources, connect our work to business priorities, and make sure you have the space to do your best technical work. For that to work, I need you to help me understand enough about what you're doing that I can represent it accurately. In return, I'll trust your technical judgment and not second-guess decisions I'm not qualified to make. How does that sound?"*
>
> **Why this works:** It names the elephant, reframes the relationship as complementary rather than hierarchical on technical matters, and asks for a specific exchange (context for autonomy).

---

## Staying Technical

Fournier makes a strong, specific argument for engineering managers staying in the code, at least at the team-lead level:

1. **Writing small code helps you feel where process problems are.** "If the build is really slow or deploying code takes too long or on-call is a nightmare, you'll feel it in the difficulties you, an experienced engineer, have in knocking out trivial programming tasks." Observing metrics is inferior to experiencing the pain firsthand.

2. **You can evaluate feasibility.** When the product manager has a "crazy idea," you need confidence to assess how hard it is to implement. Strong engineering managers "identify the shortest path through the systems to implement new features."

3. **You can identify strategic technical debt.** Being in the code gives you the context to spot debt and do cost/benefit analysis for addressing it.

She adds a warning for companies that split management and technical tracks too cleanly — where managers immediately get large teams and zero coding time. Her advice: *"Stay technical until you feel that you have truly mastered what you want to learn for writing code and designing systems, and then decide if you want to switch careers into management."*

> **[Deep Dive: What "Staying Technical" Actually Means at Each Level]**
>
> Fournier says managers at this level should "implement small features and bug fixes." But what does "staying technical" look like as you progress?
>
> | Level | What "Staying Technical" Looks Like |
> |-------|-------------------------------------|
> | **Engineering Lead (this chapter)** | Write small features, fix bugs, do code reviews. Feel the developer experience. 20-30% coding time. |
> | **Senior EM (your level)** | Rarely write production code. Read code regularly. Review architecture docs. Do occasional deep-dives into systems during incidents or design reviews. Understand enough to ask the right questions and smell bad answers. 5-10% hands-on. |
> | **Director** | Almost never write code. Stay technical through: architecture reviews, technical strategy docs, hiring bar-setting (can you evaluate a senior engineer's design?), incident reviews, and reading broadly about technology trends. 0-5% hands-on. |
> | **VP/CTO** | Technical judgment at the strategic level. Can evaluate technology bets, set architectural principles, and call bullshit on hand-wavy technical plans. Zero hands-on, but decades of pattern recognition. |
>
> **The trap at each level:** Staying hands-on longer than appropriate. The Senior EM who's still writing features is neglecting team strategy and cross-team work. The Director who's still reviewing code is micromanaging and not developing their managers. The right amount of "technical" shifts from *doing* to *evaluating* to *directing*.

> **[SRE Lens: Staying Technical in SRE Management]**
>
> SRE managers have a unique advantage here: **incidents are your code reviews.** Every incident you participate in refreshes your technical context without requiring dedicated coding time.
>
> **Concrete ways SRE managers stay technical:**
> - **Carry a light on-call rotation** — not primary, but shadow or escalation path. Even one week per quarter reconnects you to operational reality.
> - **Attend post-incident reviews** — not just the summary, but dig into the timeline, the debugging steps, the system behavior. Ask "why did the system behave this way?" until you understand.
> - **Review SLO dashboards weekly** — not just red/green, but understand the trends. Why did latency increase 15% this month? Is that a workload change or a regression?
> - **Read architecture proposals** — when a team proposes a new service or system change, read the design doc. Ask about failure modes, scalability, operability.
> - **Pair on tooling** — SRE teams often build internal tools (dashboards, automation, deployment pipelines). Pair with an engineer on one of these for an afternoon every few weeks.
>
> **What NOT to do:** Don't take critical-path work. Don't be the one who deploys the production fix at 2 AM. Don't gatekeep technical decisions. You're building technical context, not doing technical work.

> **[The Shadow Side: Staying Technical Becomes Hiding From Management]**
>
> The strength of staying technical is credibility and context. The shadow side: using technical work as an escape from the harder, less comfortable management work.
>
> **How it manifests:**
> - You spend two hours debugging an interesting problem when your real job is the difficult conversation with the underperforming engineer
> - You volunteer for the on-call escalation instead of letting your team handle it — because incidents have clear resolution, unlike the ambiguous team conflict you should be addressing
> - You attend every design review because "staying technical" — but you haven't updated anyone's development plan in months
> - Your calendar is packed with technical meetings, leaving no time for 1-1s, skip-levels, or cross-functional work
>
> **The test:** Am I doing this technical work because it genuinely makes me a better manager? Or because it's more comfortable than the management work I'm avoiding?
>
> **For Senior EMs specifically:** The pull toward technical work gets stronger, not weaker, as you move up — because the management challenges get harder and more ambiguous. The Director role Fournier will describe later requires almost zero hands-on technical work. If you can't let go now, you won't be able to let go then.

> **[Interview Angle]**
>
> "How do you stay technical as a manager?" is a common EM/Director interview question. Strong answers demonstrate:
>
> - **Awareness of the tension:** "I know my job is management, not engineering. But I also know that credibility and context require ongoing technical engagement."
> - **Concrete practices:** "I shadow on-call one week per quarter, attend every architecture review, review SLO trends weekly, and pair on internal tooling when I can."
> - **Level-appropriate boundaries:** "I don't take critical-path work — that would make me a bottleneck. I focus on building enough context to ask good questions and evaluate proposals."
> - **The 'why':** "Staying technical helps me detect process problems early, evaluate feasibility honestly, and hold technical leaders accountable for their decisions."
>
> **Red flag answer:** "I still write code every day" (at Senior EM level, this suggests you're not spending enough time on strategy and people) or "I don't need to be technical anymore" (suggests you'll lose credibility quickly).

---

## Debugging Dysfunctional Teams: The Basics

Fournier introduces four basic dysfunctions that "creep into tech teams." Her framing is explicitly diagnostic: identify the symptom, understand the root cause, apply the fix.

### Not Shipping

Fournier's key insight: even teams doing research have deliverables. **"Humans, by and large, feel good when they set small goals and meet them regularly."**

Common root causes for not shipping:
- Tools and processes make it hard to get work done quickly
- Infrequent releases (weekly or less) that hide pain points: poor tooling, manual testing, features that are too big, developers who can't break work down
- Manager afraid of "pushing too hard," so they let deadlines slide without consequence

Her concrete example: a critical system that released once a week, with painful hours-long releases. They improved automation and pushed to daily releases. **"It turns out that releases can be a point of resource contention. When people are contending for a scarce resource, conflicts and unhappiness among team members are almost inevitable."**

> **[SRE Lens: Not Shipping Is an SRE Problem]**
>
> This is Fournier making a DevOps argument without using the word. Every SRE should recognize this pattern: low deployment frequency → large batch sizes → higher failure rate → more painful rollbacks → fear of deploying → even lower frequency. The DORA metrics (deployment frequency, lead time, change failure rate, MTTR) are the quantitative framework for exactly what Fournier is describing qualitatively.
>
> **For SRE managers specifically:**
> - If your team supports services with infrequent releases, that's a reliability risk, not just a velocity problem. Large changes are harder to roll back and harder to debug.
> - If your SRE team itself isn't shipping (tooling improvements, automation, platform features), apply the same diagnosis. Is it because on-call burden is consuming all available time? Is it because the team doesn't know how to break work down? Is it because they're afraid of shipping changes to production infrastructure?
> - **The error budget connection:** If a team is afraid to ship because they're close to their error budget, that's actually the system working correctly — the risk aversion is appropriate. But if they're afraid to ship even when the error budget is healthy, that's cultural debt.

> **[Leader's Playbook: Diagnosing Why Your Team Isn't Shipping]**
>
> When your team isn't delivering, run this diagnostic (in order — start with environment, not people):
>
> 1. **Is the deployment pipeline healthy?** How long does it take to go from merged code to production? If >1 day, that's your first bottleneck.
> 2. **Is the test suite reliable?** Flaky tests erode confidence and slow everything down. If engineers are ignoring or re-running tests, the test suite is broken.
> 3. **Is work being broken down small enough?** If the average PR is >500 lines, work isn't decomposed well. Coach on smaller increments.
> 4. **Are there hidden dependencies?** Does the team need approval or work from other teams to ship? Map the dependency chain.
> 5. **Is the team overloaded?** If they're juggling 5 projects plus on-call, nothing moves fast. Cut scope.
> 6. **Is there a skills gap?** Sometimes a team is stuck because they don't know how to solve the problem, and they're afraid to say so.
> 7. **Only then: are there individual performance issues?** People problems are rarely the first cause — usually the environment is broken first.

> **[Mental Model: Theory of Constraints (Goldratt)]**
>
> Goldratt's *The Goal* offers a framework directly applicable to Fournier's "not shipping" diagnosis: **every system has exactly one bottleneck, and improving anything that isn't the bottleneck is waste.**
>
> Before you "push the team to ship faster," identify the bottleneck:
> - If the bottleneck is code review (PRs sit for days), hiring more engineers won't help. Fix the review process.
> - If the bottleneck is QA (manual testing takes 3 days per release), making engineers code faster won't help. Automate testing.
> - If the bottleneck is decision-making (the team is blocked waiting for your approval), you're the constraint. Delegate.
> - If the bottleneck is on-call burden (the team spends 40% of time on incidents), no amount of project management will increase output. Reduce incident load first.
>
> **Find the constraint, fix the constraint, repeat.** Don't spray effort across all problems simultaneously.
>
> **[Go Deeper]** *The Goal* by Eliyahu Goldratt. Also: *The Phoenix Project* by Gene Kim (which applies Theory of Constraints to IT/DevOps).

### People Drama

Fournier identifies two variants:

**The brilliant jerk** — "that person you think can't be replaced because he's just so productive and so smart, but who isn't a team player and makes everyone around him unhappy." (Covered in depth later in the Challenging Situations section.)

**The negative person** — dwells on negativity, gossips, plays us-against-them games. Easier to deal with than the brilliant jerk: give clear feedback with examples, act quickly. Sometimes this person is just unhappy and the best outcome is helping them leave on good terms.

Fournier's core advice: **"Be brave and nip people drama in the bud quickly."** Be prepared that your manager may have a harder time seeing the problem — "She isn't seeing the immediate impact on team dynamics; she's just seeing someone who gets things done."

> **[Deep Dive: People Drama in SRE Teams]**
>
> SRE teams are especially vulnerable to people drama because of:
>
> - **On-call pressure:** High-stress environments amplify interpersonal friction. Small annoyances become grudges when you're sleep-deprived from a 3 AM page.
> - **The "hero culture" trap:** SRE teams sometimes celebrate firefighters over preventers. The engineer who dramatically saves production gets praise; the one who quietly prevented the incident gets nothing. This creates perverse incentives and resentment.
> - **Cross-team blame dynamics:** When incidents cross team boundaries, the "who caused this" question can become toxic. SRE teams that position themselves as "the team that catches other teams' mistakes" create an adversarial dynamic.
> - **Skill hierarchies:** Teams with wide experience ranges (new grad SRE alongside 20-year veteran) can develop unhealthy "you're not qualified to have an opinion" dynamics, especially in incident response.
>
> **SRE-specific interventions:**
> - Make blameless postmortems genuinely blameless — not just in name. If someone says "well, if the dev team had tested properly..." redirect immediately.
> - Rotate on-call pairs to prevent clique formation and ensure knowledge sharing.
> - Celebrate prevention and toil reduction with the same visibility as incident heroics.
> - When a senior engineer dismisses a junior's incident observation, address it immediately. In SRE, every observation matters — the junior who's dismissed today stops reporting signals tomorrow.

> **[Anti-Pattern: The Drama Proxy]**
>
> You have a report who frequently comes to your 1-1 to complain about a teammate. "Did you hear what Alex said in the meeting?" "Alex never reviews my PRs on time." "Alex takes all the interesting projects." You nod sympathetically. You mention it vaguely to Alex. Nothing changes. Meanwhile, you've become a relay station for interpersonal friction instead of resolving it.
>
> **What should happen:** When someone complains about a teammate, ask: "Have you talked to Alex directly about this?" If no — coach them on how. If yes and it didn't work — now you step in, but with both people, not as a proxy. The goal is direct communication between teammates, with you as facilitator only when needed.
>
> **The Senior EM layer:** If you manage managers and one of them is acting as a drama proxy for their team, coach them out of it. "Your job isn't to carry messages between teammates. Your job is to build a team culture where they address issues directly."

### Unhappiness Due to Overwork

Fournier says this is "much easier to solve" because it has addressable root causes:

**If overwork is from production instability:** "It's your job as the manager to slow down the product roadmap in order to focus on stability." She recommends **dedicating 20% of planning time to sustainability work** (she prefers "sustainability" over "technical debt").

**If overwork is from a time-critical release:** Two rules:
1. **Be the cheerleader.** Support them however needed — help with the work, order dinner, acknowledge the effort, promise explicit break time after. "They'll remember whether their manager was with them during the stressful period."
2. **Learn from it.** Cut features, push back on dates, prevent recurrence. "Crunch periods will happen, but there is no reason they should happen frequently."

> **[SRE Lens: Overwork Is the Default in SRE — Fight It]**
>
> SRE teams are chronically overworked because their work is often invisible and unbounded. Product teams have sprints with defined scope. SRE teams have sprints PLUS incidents, escalations, toil, and "can you take a look at this" requests from every other team.
>
> **Fournier's 20% sustainability rule, SRE-adapted:**
> - Reserve 20% of team capacity for sustainability: reducing toil, improving tooling, paying down operational debt
> - Reserve another explicit allocation for on-call and incident response — don't pretend it takes zero time. Most SRE teams lose 15-25% of capacity to reactive work. If you plan at 100% capacity, you're planning to fail.
> - **The math:** 10 productive weeks per quarter (Fournier's estimate) × 5 engineers = 50 engineer-weeks. Minus 20% sustainability (10 weeks), minus 20% reactive (10 weeks) = 30 engineer-weeks for project work. If leadership expects 50 weeks of project output from your team, that's the conversation you need to have.
>
> **The on-call-specific overwork cycle:**
> - High incident rate → engineers exhausted from on-call → less time for reliability improvements → incident rate stays high → more exhaustion
> - Breaking this cycle requires the explicit "slow down product roadmap to focus on stability" action Fournier describes. This is one of the hardest conversations SRE managers have with product leadership, and one of the most important.

> **[Script: Telling Product Leadership You Need to Slow Down]**
>
> Your SRE team is overworked because production is unstable. Product wants to keep shipping features. You need to make the case:
>
> *"I need to flag a situation that's going to affect our roadmap commitments. Our incident rate has increased 40% over the last quarter — we had [X] P1/P2 incidents, which consumed [Y] engineering hours. That's equivalent to losing [Z] engineers from project work for the quarter.*
>
> *More importantly, my team is burning out. On-call satisfaction scores are at their lowest. I've had two engineers tell me they're reconsidering SRE because of the operational burden. If we lose experienced people, incident resolution gets slower and the problem compounds.*
>
> *My proposal: for the next 6 weeks, we shift 60% of team capacity to reliability work — specifically [top 3 root cause categories from incidents]. I expect this will reduce incident rate by 50%, which frees up [N] engineering hours per quarter going forward. We'll still make progress on [highest-priority project], but [lower-priority items] will slip by approximately one month.*
>
> *The alternative — continuing at current pace — risks losing people and having MORE disruption to the roadmap. I'd rather take a planned slowdown now than an unplanned one when someone quits."*
>
> **Why this works:** Quantified impact, specific proposal, comparison to the cost of inaction, and a plan — not just a complaint.

> **[Red Flags: Your Team Is Overworked and You Don't Know It]**
>
> - On-call engineers consistently work more than 2 hours of unplanned work during their rotation (on a "quiet" week)
> - Your team's planned work completion rate is below 60% per sprint
> - PTO usage is low — people aren't taking vacation because there's "too much to do"
> - Meeting load exceeds 30% of the work week for individual contributors
> - Team members are working evenings/weekends regularly and you only know because you see Slack timestamps
> - You haven't asked your team "how's the workload?" in more than a month

### Collaboration Problems

Fournier addresses two variants:

**Cross-team collaboration failures:** The fix starts with regular touch-bases with peer managers and gathering actionable feedback. She warns: "You can make the situation worse by undermining your peers in front of your team" — stay positive about other teams publicly, even when frustrated.

**Intra-team collaboration failures:** Create opportunities for the team to bond outside work context — team lunches, leaving early for a fun event, encouraging humor in chat, asking about people's lives. "Even most introverts want to have a feeling of relatedness with their team."

> **[Cross-Functional Play: When SRE and Product Teams Don't Collaborate]**
>
> This is arguably the most common collaboration problem in SRE organizations. The dynamic:
> - Product teams see SRE as a gate/blocker: "They keep rejecting our designs for not being 'reliable enough'"
> - SRE sees product teams as reckless: "They keep shipping half-baked services and expecting us to keep them running"
>
> **Structural fixes that actually work:**
>
> 1. **Embedded SRE model:** Assign an SRE engineer to sit in the product team's sprint ceremonies. Not to gatekeep — to advise early, when design changes are cheap.
> 2. **Shared on-call:** Product engineers carry primary on-call for their own services, with SRE as secondary/escalation. Nothing teaches reliability faster than being woken up by your own bugs.
> 3. **Joint postmortems:** When an incident involves both teams, run the postmortem together. Shared understanding of what went wrong builds empathy.
> 4. **SLO negotiation as partnership:** Frame SLO-setting as a collaborative exercise ("what do our customers need?") not an SRE dictate ("here's the number you must hit").
> 5. **Celebrate wins together:** When a reliability investment pays off — "zero incidents this quarter for Service X after the rewrite" — make sure the product team shares the credit.
>
> **The Senior EM's role:** You own the relationship between SRE and the product teams your group supports. If the relationship is adversarial, that's a leadership failure — yours. Model the collaboration you want to see: speak well of product partners in public, address friction in private, and never let your team develop an "us vs. them" identity.

> **[Influence Without Authority: Fixing Cross-Team Friction You Don't Control]**
>
> Sometimes collaboration problems come from teams you don't manage. A platform team ships breaking changes without warning. A security team mandates a new policy with zero implementation support. A partner team's manager is checked out and their deliverables are late.
>
> **The escalation ladder (try each before moving to the next):**
>
> 1. **Direct conversation:** Talk to the other team's manager. Assume good intent: "I think there's a gap in how our teams coordinate. Can we talk about it?"
> 2. **Propose a structural fix:** Don't just describe the problem — propose a solution. "What if we had a 15-minute weekly sync between our tech leads?"
> 3. **Create shared visibility:** Build a dashboard or shared tracker that makes the collaboration gap visible. "Here are the 5 blockers my team has from your team's pending work."
> 4. **Involve your shared manager:** If you can't resolve it peer-to-peer, bring it to the person who manages both of you — but bring data and a proposed solution, not a complaint.
> 5. **Organizational design conversation:** If the collaboration problem is structural (teams that need to work together are in different orgs with different priorities), raise it as an org design question with your director.

---

## The Shield

Fournier has "mixed feelings" about the common advice that managers should be a "bullshit umbrella." She agrees that shielding from unnecessary distractions is important, but identifies two failure modes:

**Failure mode 1: Over-shielding denies context.** "Humans usually need some sort of context into WHY these goals have been set, and thereby into what problems they're working to solve." If you withhold all organizational context and just hand down clear goals, your team can't make good local decisions. "It's not your job to make all of those decisions by yourself."

**Failure mode 2: Denying reality creates distrust.** If layoffs happen in another part of the company and the team hears about it from someone else, "rather than shielding your team from drama, you've created a situation where they feel like something bad is happening and no one wants to admit it." Communicate factual information in a "straightforward, low-emotion way."

Her sharpest point: **"You may be a shield, but you are not a parent."** Treating adults like fragile children who need protection leads to a dysfunctional parenting dynamic where you take their mistakes personally and get emotionally over-invested.

> **[Deep Dive: The Shield Spectrum]**
>
> Fournier is describing a spectrum with two toxic extremes and a healthy middle:
>
> | **Over-Shielding** | **Healthy Shielding** | **Under-Shielding** |
> |--------------------|-----------------------|---------------------|
> | Team knows nothing about org context | Team knows what affects them and why | Team knows everything — every rumor, every political fight |
> | Team can't make informed decisions | Team has enough context to make good local decisions | Team is paralyzed by anxiety about things they can't control |
> | Manager is a single point of failure for all context | Manager filters for relevance and presents with appropriate framing | Manager dumps raw information with no framing |
> | Team is surprised by every change | Team understands the direction of change even if details shift | Team is overwhelmed by constant change signals |
>
> **The healthy middle:** Share information that (a) affects your team's work, (b) affects your team's people (reorgs, layoffs, policy changes), or (c) provides useful context for decision-making. Filter information that (d) is interpersonal drama in other teams, (e) is speculative/unconfirmed, or (f) your team has zero ability to influence.

> **[SRE Lens: The SRE Shield Has Unique Challenges]**
>
> SRE managers face shielding challenges that don't exist in feature teams:
>
> - **Incident fatigue from other teams:** Your SRE team sees incidents across the entire organization. Without shielding, they become cynical about the engineering quality of every team they support. Your job: share the systemic patterns ("we're seeing a trend in deployment-related incidents") without letting your team develop contempt for specific teams.
>
> - **Executive panic during outages:** When a major outage hits, VPs and C-levels want updates every 5 minutes. Your job: be the interface to leadership so the incident commander can focus on resolution, not status reporting. This is literal shielding — and one of the highest-value things you can do during an incident.
>
> - **Organizational uncertainty about SRE's role:** Many companies are still figuring out where SRE fits — is it a cost center? A platform team? An embedded function? Your team hears these debates and feels existentially threatened. Your job: communicate what you know, advocate for your team's value, and — critically — keep the team focused on the work that demonstrates that value, rather than spiraling about organizational politics.
>
> - **Toil requests disguised as "just this once":** Other teams constantly ask your team for "quick favors" — manual deployments, one-off data fixes, special monitoring for a launch. Each one is small; collectively, they consume weeks of capacity. Shield your team by being the one who says no (or negotiates scope) to these requests.

> **[Anti-Pattern: The Helicopter Manager]**
>
> You've internalized "be a shield" so deeply that you intercept ALL communication between your team and anyone outside the team. Product managers can't talk directly to your engineers. Your director can't have skip-levels without it feeling like a violation. Other teams' engineers have to go through you to ask your team a technical question.
>
> **Why this happens:** Control feels like protection. If you route everything through yourself, nothing "bad" reaches the team. Also: it makes you feel essential.
>
> **Why it's destructive:**
> - You become a bottleneck for all information flow
> - Your team can't build cross-functional relationships (critical for their career growth)
> - You miss information that would surface in direct conversations
> - Your team feels babied, not protected
>
> **The fix:** Default to connecting your team members directly with the people they need to talk to. Filter strategically, not comprehensively. Shield from chaos, not from the organization.

> **[Script: Communicating Organizational Uncertainty to Your Team]**
>
> Your company just announced a 10% reduction in force. Your team isn't affected, but they're anxious.
>
> *"I want to address what happened directly. The company announced a reduction that affected [X number] of people across [Y teams]. Our team is not impacted — I confirmed this with [my director]. I know that doesn't eliminate the anxiety. People you know and work with have been let go, and it's natural to wonder if more changes are coming.*
>
> *Here's what I know: [share what you actually know — e.g., 'the stated goal was to reach a specific cost target, and leadership says they've reached it']. Here's what I don't know: [be honest — e.g., 'I can't promise there will never be another round']. Here's what I believe based on what I've seen: [your honest assessment].*
>
> *What I can tell you is this: our team's work is directly tied to [business-critical function]. The projects we're working on are funded and prioritized. The best thing we can do — for ourselves and for the colleagues who are leaving — is to keep doing excellent work.*
>
> *If you're feeling unsettled, my door is open. If you want to talk about your own career stability, let's do that in our 1-1. And if you're thinking about whether this is the right place for you, I'd rather have that honest conversation than have you quietly disengage."*
>
> **Why this works:** Addresses the situation head-on (not pretending it didn't happen), separates facts from interpretation, gives permission to feel anxious, offers individual support, and redirects to meaningful work. The final sentence — inviting honest conversation about staying — is counterintuitively trust-building.

> **[Mental Model: The Kurtz Snowflake — Information Radiation vs. Information Refrigeration]**
>
> Think about information flow as temperature:
>
> - **Information radiators** broadcast everything — dashboards, open Slack channels, shared docs. Good for operational transparency. Bad for unverified rumors and executive deliberations.
> - **Information refrigerators** store information and release it selectively — 1-1s, carefully crafted announcements, need-to-know sharing. Good for sensitive situations. Bad when overused (creates "what are they hiding?" anxiety).
>
> **The healthy manager:** Radiates operational information (team metrics, project status, cross-team dependencies) and refrigerates sensitive information (personnel decisions, unconfirmed reorgs, someone's performance issues). Fournier's complaint about over-shielding is about managers who refrigerate EVERYTHING, and her complaint about under-shielding is about managers who radiate EVERYTHING. Be deliberate about which channel each piece of information belongs in.

---

## Ask the CTO: Managing a Former Peer

Someone asks about being promoted over a peer who also wanted the job. Fournier's advice:

1. **Acknowledge the awkwardness.** "Be honest and transparent... You'll need his help."
2. **Be vulnerable.** "You won't be perfect the first time around."
3. **Don't use managerial power to override technical decisions.** "Using your managerial power to override technical decisions is usually a bad idea."
4. **Don't micromanage.** Former peers are "going to be sensitive to the feeling that you've been 'rewarded.'"
5. **Let go of old responsibilities.** Give former peers more control over technical work you used to own. "This is also an opportunity to give new challenges to more junior members."
6. **Show the team your role adds, not takes.** "Your new role isn't taking anything away from the rest of the team."
7. **Pick your battles.** Former peers "may even do things to try to undermine you." Handle with maturity.

> **[Scenario: Promoted Over Your Best Engineer]**
>
> You've been promoted to manage a team of 7 in SRE. One of the engineers — Priya — is technically the strongest person on the team. She applied for the same manager role and didn't get it. She's been cool but distant since the announcement. In team meetings, she subtly challenges your suggestions with "well, technically..." caveats. She's started having sidebar conversations with teammates after your decisions, offering her alternative takes.
>
> **Applying Fournier's framework:**
>
> **Step 1 — Acknowledge (Week 1).** In your first 1-1 with Priya:
> *"I want to acknowledge that this transition is probably awkward for you. You wanted this role, and I respect that — it shows ambition and leadership. I want you to know that I see your technical strength as essential to this team's success. I need you as a partner, not just a report. I'm going to make mistakes, and I'd value your direct feedback when I do."*
>
> **Step 2 — Increase her ownership (Weeks 2-4).** Give Priya meaningful technical ownership: lead architect for the next system design, tech lead for the most complex project, owner of the team's technical standards. Make it visible that her scope GREW because of this change.
>
> **Step 3 — Address the undermining (if it continues past Week 4).** In a 1-1:
> *"I've noticed that after some team decisions, you've been sharing alternative approaches with teammates in side conversations. I want to understand — is there a concern about my decisions that you're not raising directly with me? I'd much rather you challenge me in the room or in our 1-1, where we can actually adjust course. The sidebar conversations undermine the team's confidence in our direction."*
>
> **Step 4 — Accept the possible outcome.** If Priya can't work under you after genuine effort on both sides, help her find another role — either on another team or outside the company. Fournier notes this: sometimes people transfer away, and sometimes "a bit contrite, [they] return." Give Priya space to make that choice.

> **[Interview Angle]**
>
> "Tell me about a time you managed a difficult team dynamic" — the former-peer scenario is a powerful answer because it demonstrates emotional intelligence, not just management mechanics.
>
> Strong answer structure:
> - **Context:** "I was promoted over a peer who also wanted the role. They were technically stronger than me."
> - **Self-awareness:** "I knew this was going to be awkward, and I didn't pretend otherwise."
> - **Proactive action:** "In our first 1-1, I acknowledged the situation directly and asked for their partnership."
> - **Structural solution:** "I expanded their technical scope — they became the team's technical authority, which is what they really wanted."
> - **Outcome:** Ideally positive ("we developed a strong working relationship"). But even if the person left, show you handled it with maturity: "They eventually decided to pursue a lead role on another team, and I supported that transition."

---

## Quarterly Ritual: Team Health Diagnostic (Part 1)

> **[Quarterly Ritual]**
>
> Every quarter, audit the team-level health indicators from Part 1 of this chapter. This complements the people management audit from Ch4 — this one is about the team as a system.
>
> **Technical Health:**
> - [ ] How much time have I spent in the code/systems this quarter? Was it enough to maintain technical context? Too much (avoiding management)?
> - [ ] Can I articulate the top 3 technical risks in my team's systems right now?
> - [ ] When was the last time I participated in a design review, architecture discussion, or incident deep-dive?
> - [ ] Has our deployment frequency changed? If it decreased, why?
>
> **Shipping Health:**
> - [ ] What did the team ship this quarter? Does the list match what we planned?
> - [ ] If we missed deliverables, do I understand the root cause? (Scope creep? Dependencies? Skills gap? Overwork?)
> - [ ] Are we releasing frequently (daily/weekly) or batching (monthly/quarterly)? If batching, what's the barrier to more frequent releases?
>
> **Drama Health:**
> - [ ] Are there interpersonal conflicts I'm aware of but haven't addressed?
> - [ ] Is there a "brilliant jerk" or chronic negativity source I've been tolerating?
> - [ ] Am I acting as a proxy for conflicts instead of facilitating direct resolution?
>
> **Workload Health:**
> - [ ] Is my team's capacity planned at 100%, or is there slack for reactive work and sustainability?
> - [ ] How many hours per week is the average on-call engineer spending on unplanned work?
> - [ ] When was the last time each team member took a real vacation (not "working from the beach")?
>
> **Shield Health:**
> - [ ] Am I over-shielding (team lacks context for decisions) or under-shielding (team is drowning in org noise)?
> - [ ] Does my team know about the major organizational changes that affect them?
> - [ ] Am I the bottleneck for communication between my team and other teams?
>
> **Collaboration Health:**
> - [ ] How is the relationship between my team and its primary cross-functional partners (Product, other engineering teams)?
> - [ ] When was the last time I had a 1-1 with my peer managers in Product and other Engineering teams?
> - [ ] Does my team have a healthy rapport with each other? When was the last time they socialized?

---

## Peer Reflection Prompt (Part 1)

> **[Peer Reflection Prompt]**
>
> 1. **"When was the last time you were genuinely surprised by a technical problem in your team's systems — something you should have seen coming but didn't? What does that tell you about how connected you are to the technical reality?"** If you're always surprised by incidents and technical debt revelations, you've drifted too far from the code. If you're never surprised, you might be too deep in the weeds.
>
> 2. **"Think about the last time your team missed a deadline. Was the root cause a people problem, a process problem, or a technical problem? Did you diagnose it correctly at the time, or did you default to blaming one category when the real cause was another?"** Most managers default to one diagnostic lens — people-oriented managers blame skills/motivation, process-oriented managers blame methodology, technical managers blame tools/architecture. Check whether your diagnostic instinct matches reality.
>
> 3. **"If you disappeared for two weeks with no notice, what would break first on your team? That's your single point of failure — and your top priority to fix."** If the answer is "nothing would break," either you've built an excellent self-sustaining team, or you're not adding enough value. If the answer is "everything would break," you haven't delegated enough.
>
> 4. **"How much organizational context does your team actually have? If you asked each team member to explain WHY they're working on their current project — not what they're doing, but why it matters — could they? If not, you're over-shielding."**

---

*Continued in [Part 2](ch05-notes-managing-a-team-part2.md): Driving Good Decisions, Conflict Management, Team Cohesion Destroyers, Advanced Project Management.*
