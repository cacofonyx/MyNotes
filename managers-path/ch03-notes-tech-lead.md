# Chapter 3: Tech Lead

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

The Tech Lead chapter is critical for a Senior EM — not because you ARE a tech lead, but because **you manage tech leads**. Understanding the role deeply means you can identify struggling TLs early, develop promising ones, and design the role effectively for your teams. Fournier covers what the TL role actually is (vs. misconceptions), the three core responsibilities, project management skills, the IC-vs-manager decision point, and two key anti-patterns (Alpha Geek from Ch2, and the Process Czar introduced here).

## Table of Contents

- [What Is a Tech Lead?](#what-is-a-tech-lead)
- [All Great Tech Leads Know This One Weird Trick](#all-great-tech-leads-know-this-one-weird-trick)
- [Being a Tech Lead 101](#being-a-tech-lead-101)
  - [The Main Roles of a Tech Lead](#the-main-roles-of-a-tech-lead)
- [Managing Projects](#managing-projects)
  - [Managing a Project — Guidelines](#managing-a-project--guidelines)
- [Decision Point: Stay on the Technical Track or Become a Manager](#decision-point-stay-on-the-technical-track-or-become-a-manager)
  - [Imagined vs. Real Life of a Senior IC](#imagined-vs-real-life-of-a-senior-ic)
  - [Imagined vs. Real Life of a Manager](#imagined-vs-real-life-of-a-manager)
- [Good Manager, Bad Manager: The Process Czar](#good-manager-bad-manager-the-process-czar)
- [How to Be a Great Tech Lead](#how-to-be-a-great-tech-lead)
- [Quarterly Ritual: Tech Lead Health Check](#quarterly-ritual-tech-lead-health-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping the Tech Lead Role](#how-genai-is-reshaping-the-tech-lead-role)

**Block types in this chapter:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Go Deeper] [Cross-Functional Play] [Quarterly Ritual] [Peer Reflection Prompt]

---

## What Is a Tech Lead?

Fournier opens with her own story: she became a tech lead despite not being the most senior person on her team. Her advantages: she was a good communicator (clear docs, presentations, cross-team conversations), good at prioritizing, and "willing to pick up the pieces and do what needed to be done to make progress."

She also describes a TL who floundered: "an amazing engineer, wrote great code, but hated talking to people and often got distracted by technical details." While this TL chased rabbit holes, the product manager "took advantage of his absence to railroad the rest of the team into committing to feature delivery that was both poorly designed and way too aggressive."

> "The idea that the tech lead role should automatically be given to the most experienced engineer, the one who can handle the most complex features or who writes the best code, is a common misconception that even experienced managers fall for."

**Rent the Runway's definition:** The tech lead role is "not a point on the ladder, but a set of responsibilities that any engineer may take on once they reach the senior level." It may or may not include people management. The tech lead is "learning how to be a strong technical project manager... scaling themselves by delegating work effectively without micromanaging."

**Patrick Kua's shorthand** (from *Talking with Tech Leads*): "A leader, responsible for a (software) development team, who spends at least 30 percent of their time writing code with the team."

> "You can't lead without engaging other people, and people skills are what we're asking the new tech lead to stretch, much more than pure technical expertise."

> **[Deep Dive: The Tech Lead in SRE — A Unique Variant]**
>
> The SRE tech lead role has dimensions that don't exist in product engineering:
>
> | Dimension | Product TL | SRE TL |
> |-----------|-----------|--------|
> | **Primary output** | Features shipped | Reliability maintained/improved |
> | **Project planning** | Feature roadmap → tasks | Reliability roadmap + interrupt-driven work (incidents, toil) |
> | **Technical decisions** | Architecture, frameworks, APIs | SLOs, monitoring strategy, on-call structure, incident response |
> | **"Customer"** | End users | Internal engineering teams (product teams they support) |
> | **Crisis mode** | Launch deadlines | Production incidents (unplanned, high-stress, high-visibility) |
> | **Success metric** | Did we ship on time with quality? | Did we keep systems reliable while also improving them? |
>
> **The unique SRE TL challenge:** balancing planned project work (platform improvements, toil reduction, observability) with unplanned reactive work (incidents, escalations, on-call burden). A product TL can plan their sprint with reasonable confidence. An SRE TL must always hold capacity for the unexpected.

> **[Insight]** Fournier's point that the TL role is "a set of responsibilities... not a point on the ladder" has a specific implication: **the same person shouldn't be TL forever**. The role should rotate among senior engineers to develop leadership skills across the team. As a Senior EM, if you have one person who's been TL for 3+ years and no one else has had the chance, you're creating a single point of failure AND stunting the growth of others.

> **[Senior EM vs. Director: How You Relate to Tech Leads]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Relationship to TLs** | You directly manage TLs. You coach them, evaluate them, develop them. | You manage managers who manage TLs. You set the standard for what "good TL" means across the org. |
> | **TL selection** | You choose who becomes TL on your teams | You ensure your managers are selecting TLs well (not just defaulting to "most senior engineer") |
> | **TL development** | You personally coach TLs on project management, communication, and leadership | You create TL development programs: peer groups, training, rotation |
> | **TL failure** | You intervene directly when a TL is struggling | You coach your manager on how to intervene. You step in only if the manager can't handle it. |

---

## All Great Tech Leads Know This One Weird Trick

The "trick": **willingness to step away from code and balance technical work with the team's needs.**

> "You have to stop relying entirely on your *old* skills and start to learn some *new* skills. You're going to learn the art of balance."

Fournier identifies the core tension: "It can be hard to balance the work of project management and oversight with hands-on technical delivery. Some days you're on a maker's schedule, and some days you're on a manager's schedule."

Practical advice:
- Manage your time to get appropriately sized blocks for focused work
- Don't let yourself get pulled randomly into meetings
- Help other stakeholders (boss, product manager) respect the team's focus time
- You probably won't have multi-day coding stretches anymore — learn to break your own work into smaller chunks

**Caitie McCaffrey's sidebar** describes exactly this challenge: becoming TL meant her focus shifted "less about me and working on the most technically challenging idea... instead, my focus is more on my team." She prioritized technical debt and operations over new features, even though features were more fun. Result: "reduced the number of critical paging alerts by 50%, and in the following quarter we almost doubled the number of deploys."

> **[Mental Model: Maker's Schedule vs. Manager's Schedule (Paul Graham)]**
>
> Graham's famous essay describes two fundamentally different ways of organizing time:
>
> - **Maker's schedule:** Long, uninterrupted blocks (4+ hours). One meeting in the afternoon can ruin a whole day of coding because it fragments the available time into unusable pieces.
> - **Manager's schedule:** Time sliced into 30-60 minute blocks. Meetings are the unit of work, not an interruption to it.
>
> **The tech lead's dilemma:** They live on BOTH schedules simultaneously. Coding requires maker time; coordination requires manager time. The key is deliberate boundary-setting: "Monday/Wednesday/Friday mornings are maker time — no meetings. Tuesday/Thursday are available for manager time."
>
> **For SRE TLs specifically:** Add a third schedule — **operator's schedule**: unplanned, interrupt-driven, reactive. An SRE TL might have a "maker morning" destroyed by a P2 incident at 10 AM. This is why SRE TLs often need MORE calendar protection than product TLs, and why splitting the on-call lead and the TL roles can be valuable for busy teams.

> **[The Shadow Side: Staying Too Close to Code]**
>
> Fournier's description of the TL who "went chasing after the next refactoring" is the most common TL failure mode. The shadow side of technical excellence: **retreating to code when leadership gets hard.**
>
> **How it manifests in SRE:**
> - The TL spends all week building a custom monitoring dashboard instead of having the difficult conversation with the product team about SLO violations
> - The TL takes the most technically interesting incident post-mortem action items themselves instead of delegating to develop the team
> - The TL writes perfect automation scripts but never talks to the team about on-call burden or career goals
>
> **The diagnostic question (for you as their manager):** "If I look at this TL's calendar and git history for the last two weeks, what's the ratio of code-to-leadership work?" If it's above 70% code, they're probably hiding in the codebase. The target should be ~40-60% code for a TL, per Kua's 30%+ guideline plus realistic overhead.

> **[Anti-Pattern: The Reluctant Tech Lead]**
>
> Your most senior SRE says they don't want to be TL. They love deep technical work — building the next-gen monitoring platform, optimizing incident detection, writing chaos experiments. They don't want "all those meetings."
>
> **The temptation:** Force them into TL because they're the most senior, or find someone less experienced who's willing.
>
> **Fournier's advice:** "I have a strong opinion on pushing people into management roles, which is that you shouldn't do it." But she adds nuance: "At some point, to progress in your career, you'll probably need to do the tech lead job."
>
> **The Senior EM play:**
> 1. Don't force it. Respect their choice.
> 2. But be honest about the career implications: "I respect that you don't want TL right now. I want you to know that our Staff/Principal track still requires demonstrated leadership and cross-team influence. We can find ways to build those skills without the TL title — leading architecture reviews, mentoring junior SREs, driving a cross-team initiative."
> 3. Find the right TL from someone who IS willing — even if they're less senior. Then give the reluctant senior engineer a well-defined technical leadership scope that doesn't require the TL coordination overhead.

---

## Being a Tech Lead 101

### The Main Roles of a Tech Lead

Fournier describes three distinct hats:

**1. Systems architect and business analyst:** Identify critical systems that need to change and features that need to be built. "Have a good sense of the overall architecture... and a solid understanding of how to design complex software." Translate business requirements into software.

**2. Project planner:** Break work into rough deliverables. Find efficient ways to break down work for parallel execution. "Gather input from the experts on your team." Identify priorities — which pieces are critical, which are optional?

**3. Software developer and team leader:** Write code (but not too much), communicate challenges, delegate. "Even if you are tempted to pull a rabbit out of the hat yourself, you must communicate this obstacle first."

> "Teams often fail because they overworked themselves on a feature that their product manager would have been willing to compromise on."

> **[Leader's Playbook: How to Evaluate Your Tech Leads]**
>
> Use Fournier's three hats as an evaluation framework. For each TL, ask:
>
> | Hat | Strong Signal | Weak Signal |
> |-----|--------------|-------------|
> | **Architect/Analyst** | Designs systems that are clear to others, identifies risks early, translates business requirements into technical plans | Over-engineers solutions, misses business context, designs in isolation without team input |
> | **Project Planner** | Breaks work into parallelizable chunks, knows what's critical vs. optional, estimates reasonably | Always surprised by delays, doesn't break work down, can't articulate what's left to do |
> | **Developer/Leader** | Writes code AND delegates, communicates blockers early, involves the team in decisions | Hoards interesting work, doesn't delegate, communicates problems only when it's too late |
>
> **Quarterly coaching conversation:** Walk through the three hats with your TL. "Which hat do you feel strongest in? Which feels most uncomfortable?" Their discomfort zone is their development area.

> **[SRE Lens: The SRE Tech Lead's Fourth Hat — Operational Leader]**
>
> SRE TLs have a hat Fournier doesn't mention because it's domain-specific:
>
> **4. Operational leader:** Sets on-call standards, leads or coaches incident response, reviews post-mortems for quality, manages the balance between project and reactive work, owns the team's SLO targets and error budget.
>
> This fourth hat often DOMINATES the SRE TL's time — which is why the other three hats (architect, planner, coder) suffer. As a Senior EM, you may need to split responsibilities: have the TL own hats 1-3, and designate a separate "on-call lead" or "incident lead" for hat 4. Or rotate hat 4 among senior team members on a weekly/monthly basis so it doesn't fall entirely on the TL.

---

## Managing Projects

Fournier shares her first project management experience in vivid detail — breaking down a complex distributed systems project with her boss Mike. "It was one of the worst experiences ever."

She lists what made it painful: figuring out dependencies, ordering tasks, identifying hardware needs, estimating integration testing time. "I would go into Mike's office, sit across from him at this big wooden desk, and we would go over task descriptions, dates, and breakdowns."

> "This was not something I enjoyed doing... It almost killed me. And it was one of the most important learning experiences of my career."

**On Agile not replacing project management:** "Doesn't agile software development get rid of the need for project management? No." You'll have projects that don't fit into single sprints, need estimates for management, or require significant architecture planning.

> "Ultimately, the value of planning isn't that you execute the plan perfectly... it's that you enforce the self-discipline to think about the project in some depth before diving in and seeing what happens."

**The outcome:** "Did the project run perfectly according to plan? Of course not... However, amazingly, we still delivered the project fairly close to on time, and there was no string of sleepless nights required."

**Michael Marçal's sidebar — "Take the Time to Explain":** A PhD mathematician told him his thesis was exceptional because he "had taken the trouble to explain the basic ideas." The same applies to technology leadership — senior leaders don't automatically "get" what we do. "I've always been surprised how grateful senior technical managers have been when I can explain some very basic modern ideas to them in a nonthreatening and noncondescending way."

> **[Insight]** Marçal's sidebar is one of the most practically useful passages in the entire book for a Senior EM aiming at Director. Your ability to explain complex SRE concepts to non-technical leaders — in a way that's "nonthreatening and noncondescending" — is a Director-level skill. The CIO doesn't know what an SLO is. The VP of Product doesn't understand error budgets. The CFO doesn't know why you need 20% headcount for toil reduction. Your job is to explain these things so clearly that they feel smart for understanding, not dumb for not knowing.

### Managing a Project — Guidelines

Fournier's project management framework:

1. **Break down the work.** Start with biggest pieces, then break down further. Ask experts for help on parts you don't understand. "Hand those tasks off to the people who can actually turn them into ticket-sized work."

2. **Push through the details and the unknowns.** "The trick of project management is not to stop when you feel a little bit stuck, or tired of it." A good manager will help — ask questions, prompt you, work through some of it with you.

3. **Run the project and adjust the plan as you go.** "As things slip (and they always do), keep everyone apprised of the status."

4. **Use planning insights to manage requirements changes.** "If the changes add significant risk to the project, be clear about the cost of those changes."

5. **Revisit the details as you get close to completion.** Run a **premortem** — go through everything that could fail on launch. "Decide where the line for 'good enough' is, socialize it, and commit to it." Make a launch plan AND a rollback plan. "Don't forget to celebrate!"

> **[Deep Dive: The Premortem — A Critical Practice for SRE]**
>
> Fournier mentions premortems briefly, but they deserve emphasis. A premortem (coined by psychologist Gary Klein) asks: "Imagine the project has failed spectacularly. What went wrong?"
>
> **Why it works:** It's psychologically easier to imagine failure than to predict it. By framing it as "this already happened," people feel safe naming risks they'd otherwise suppress ("I don't want to sound negative").
>
> **For SRE launches/migrations:**
> - "The database migration took 4x longer than expected because we didn't test with production-scale data"
> - "The new service couldn't handle the load because we only load-tested to 50% of peak"
> - "Rollback failed because the schema change was irreversible"
> - "The on-call team couldn't support the new system because the runbooks weren't ready"
>
> **How to run one:** 15-20 minutes. Everyone writes silently for 5 min: "It's 3 months from now. This project failed. Why?" Then go around the room and collect answers. No debating — just collecting. Then prioritize: which of these are we going to mitigate?
>
> **[Go Deeper]** Gary Klein, "Performing a Project Premortem," *Harvard Business Review*, 2007. Short, practical, transformative.

> **[Interview Angle]**
>
> A very common Senior EM/Director interview question: "Tell me about a project that was at risk of failing. How did you turn it around?" or "How do you manage complex, multi-team technical projects?"
>
> **Strong answer structure:**
> 1. **The project and its stakes** — keep it to 2 sentences
> 2. **How you identified the risk** — what signals told you things were off? (shows diagnostic skill)
> 3. **How you replanned** — what did you cut, rescope, or restructure? (shows judgment)
> 4. **How you communicated** — who needed to know, and how did you frame it? (shows leadership)
> 5. **The outcome and what you learned** — don't claim perfection; show learning
>
> For Director-level: elevate from "I managed the project" to "I set up the system that catches project risk early across multiple teams" — skip-level check-ins, project health dashboards, regular premortem cadence.

---

## Decision Point: Stay on the Technical Track or Become a Manager

This is one of the most beloved sections of the book — Fournier's honest comparison of the imagined vs. real versions of both the IC and manager tracks.

### Imagined vs. Real Life of a Senior IC

**Imagined:** Deep thinking, solving fun hard problems, collaborating with other deep thinkers. Lots of autonomy, just the right meetings, junior devs hanging on your every word. Industry fame via books and talks. "The perfect balance of engaging work, fame, and accumulated expertise."

**Real:** When you find the right project at the right lifecycle stage, it's great. But: "Those big projects that prove you to be an invaluable architect are hard to find." Your manager expects *you* to find them. Pick the wrong project and you waste months or years. Junior developers are "a mixed bag." Your manager isn't terribly supportive of your open source ambitions. You suspect you're "missing out on crucial information because you aren't in the right meetings, but every time she invites you to sit in those meetings you remember how boring and inefficient they are."

**The silver lining:** "You get to build things most of the time... And you just found out that you get paid more than your manager!"

### Imagined vs. Real Life of a Manager

**Imagined:** You have control. You tell the team to write more tests and they do it. People give you open feedback. Other managers respect your advice. Path to promotion is clear.

**Real:** "Getting people to do something is harder than just telling them to do it." You're in meetings all day. You've lost touch with code. "More than making decisions yourself, you're helping the team make decisions." Some people quit before you notice they're unhappy. Other managers "find you meddling and get competitive when they think you're encroaching on their turf." You discover the staff engineer who works for you makes more than you do.

> "My final advice is to remember that you can switch tracks if you want... Nothing about this choice has to be permanent."

> **[Insight]** Fournier's brutal honesty about the reality of management is rare and valuable. She's not selling the management track — she's inoculating you against disillusionment. For a Senior EM, the key passage is about other managers being competitive rather than collaborative. This is the reality of Director-level politics: your peer Directors are simultaneously your collaborators AND your competitors for headcount, budget, and executive attention. Learning to navigate this — genuine collaboration while being politically aware — is a Director survival skill.

> **[Scenario: Your Best Engineer Wants to Be a Manager — But Shouldn't Be One (Yet)]**
>
> Your strongest Staff SRE comes to you: "I've been thinking about my career, and I want to try management. Can you help me find a management role?"
>
> You know this person is technically exceptional but has some red flags: they're impatient with less experienced engineers, they prefer to solve problems themselves rather than delegate, and they haven't shown much interest in the people side (career conversations, team dynamics, conflict resolution).
>
> **Applying Fournier's framework:**
>
> *"I'm glad you're thinking about this. Let me be honest with you — I think you have the potential to be a great manager, but there are some skills I'd want to see you develop first. Management is less about technical decision-making and more about helping others grow and make decisions. Here's what I'd suggest: take on the TL role for the next 6 months. Focus specifically on delegating the interesting technical work — not doing it yourself — and on coaching one of our mid-level SREs through a project they're struggling with. If you thrive in that, we'll talk about a formal management transition. If you find it draining, that's valuable information too."*
>
> **Why not just let them try management directly?** Because a failed management transition hurts everyone — the new manager, their team, and the organization. The TL role is a lower-risk proving ground, exactly as Fournier describes.

---

## Good Manager, Bad Manager: The Process Czar

The second anti-pattern (after Alpha Geek in Ch2):

**The Process Czar:** "Believes that there is one true process that, if implemented correctly and followed as designed, will solve all of the team's biggest problems." May be obsessed with agile, Kanban, scrum, lean, or waterfall. "Good at knowing the rules and following them precisely."

**At their best:** Valuable on project management teams, ensures nothing is forgotten.

**At their worst:** "Blame all problems on a failure to follow the best process, instead of acknowledging the need for flexibility." Focus on easy-to-measure things (hours in office) and miss nuance. "Constantly push new tools and processes on the team as solutions to the messier problems of human interactions."

**Fournier's antidote:** The Agile Manifesto values — individuals over processes, working software over documentation, responding to change over following a plan.

> "If you find yourself playing the role of taskmaster—criticizing people who break the rules or don't follow the process—see if the process itself can be changed to be easier to follow."

> **[Anti-Pattern: The Process Czar in SRE — "The Incident Process Police"]**
>
> SRE is particularly susceptible to process czars because the domain genuinely requires process — incident response, change management, on-call procedures, post-mortems. The SRE process czar:
>
> - Insists on a 47-step incident response checklist that no one follows in the heat of a P1
> - Rejects post-mortems that don't follow the exact template, even when the content is insightful
> - Blocks deployments because a change request field wasn't filled in, even when the change is low-risk
> - Measures team health by "percentage of post-mortems completed within 48 hours" rather than "quality of learnings"
>
> **The correction (from Fournier):** "Look for self-regulating processes." In SRE, this means: instead of a 47-step checklist enforced by a human, build automated pre-deployment checks that block unsafe changes without requiring a human to play rules cop. Instead of mandating post-mortem format, provide a good template and judge by insight quality, not template compliance.

> **[Mental Model: The Cynefin Framework (Dave Snowden) — Matching Process to Problem Type]**
>
> The Cynefin framework helps determine *when* rigid process is appropriate and when it isn't:
>
> | Domain | Characteristics | Right Approach | SRE Example |
> |--------|----------------|---------------|-------------|
> | **Clear** (formerly Simple) | Cause-effect obvious. Best practice exists. | Follow the process. | Restarting a known-flaky service. Follow the runbook. |
> | **Complicated** | Cause-effect discoverable with expertise. Good practices exist. | Analyze, then act. Expert consultation. | Capacity planning for next quarter. Requires analysis but is solvable. |
> | **Complex** | Cause-effect only clear in retrospect. No best practice. | Probe → Sense → Respond. Experiment safely. | A novel cascading failure across multiple services. No runbook applies. |
> | **Chaotic** | No cause-effect relationships. Crisis. | Act → Sense → Respond. Stabilize first. | Full production outage with unknown cause. Get service back, investigate later. |
>
> **The Process Czar's mistake:** Treating every problem as Clear or Complicated — where process and analysis work. In Complex and Chaotic domains (where SRE spends a lot of time), rigid process *harms* because it prevents the adaptive, creative responses that novel situations require.
>
> **The leadership lesson:** Build strong processes for Clear/Complicated work (deployment checklists, standard change management). Build *principles and judgment* for Complex/Chaotic work (incident response guidelines, not scripts; blameless culture, not blame-avoidance checklists).

---

## How to Be a Great Tech Lead

Fournier's four characteristics:

### Understand the Architecture
"If you go into a tech lead role and you don't feel that you fully understand the architecture you are supporting, take the time to understand it." Visualize it, understand connections, data flow, how it reflects the products it supports.

### Be a Team Player
"If you're doing all of the interesting work yourself, stop." Look at tricky, boring, or annoying areas and unstick them. But don't only do boring work either — take on some harder tasks. "Give yourself a fun task occasionally."

### Lead Technical Decisions
"If you start to make all of the technical decisions without soliciting the input of your team, they'll resent you and blame you when things go wrong." Determine which decisions you must make, which to delegate, which need the whole team. Communicate the outcome clearly.

### Communicate
> "Your productivity is now less important than the productivity of the whole team."

Practice writing and speaking: design documents, blog posts, team meetings, meetups. And listen — "Give others a chance to speak."

> "If you can't communicate and listen to what other people are saying, your career growth from this point on will suffer."

> **[Leader's Playbook: Developing Your Tech Leads]**
>
> As a Senior EM, here's how to develop each of Fournier's four TL characteristics in your reports:
>
> 1. **Architecture understanding:** Assign them to lead an architecture review of their own system. Ask them to draw the system diagram from memory — gaps reveal areas they need to learn.
> 2. **Team player mentality:** Watch their git history. Are they hoarding the interesting work? In 1-1s, ask: "What's the last task you deliberately gave to someone else because it would help them grow?"
> 3. **Technical decision leadership:** Practice in low-stakes settings first — let them run the team's design review meeting. Coach them on when to decide, when to delegate, when to facilitate consensus.
> 4. **Communication:** Have them write the next project proposal or quarterly update. Review it with them before it goes out. Send them to represent the team in a cross-team meeting you'd normally attend yourself.

> **[Script: Coaching a TL Who Isn't Delegating]**
>
> *"I've been looking at the last sprint, and I noticed that you picked up the three most technically complex tasks. [Mid-level SRE] and [junior SRE] worked on configuration changes and runbook updates. I know those complex tasks play to your strengths, but I'm concerned about two things: first, [mid-level SRE] is ready for more challenging work and isn't getting it. Second, if you're always the one who understands the complex parts, we have a bus factor of 1 on those areas.*
>
> *For next sprint, I'd like you to deliberately assign the most interesting task to [mid-level SRE] and be available as a coach — not the implementer. You'll probably have to resist the urge to take it back when they struggle. Can we try this?"*

---

## Quarterly Ritual: Tech Lead Health Check

> **[Quarterly Ritual]**
>
> For each tech lead you manage:
>
> **Monthly:**
> - [ ] TL is spending 30-60% of time on code (not 0%, not 90%)
> - [ ] TL is actively delegating — not hoarding interesting work
> - [ ] TL is communicating project status proactively (you hear about risks before they're crises)
>
> **Quarterly:**
> - [ ] Review the three hats: Is the TL effective as architect, planner, AND leader? Where's the gap?
> - [ ] Ask the TL's team (in skip-levels): "Does [TL] make you more productive, or are they a bottleneck?" The answer tells you everything.
> - [ ] Review whether the TL role should rotate. Has this person held it long enough? Is someone else ready?
> - [ ] Assess: Is this TL showing interest and aptitude for management? If so, what's the development plan?
> - [ ] Check for alpha geek or process czar tendencies. If present, address in the next 1-1.
>
> **For yourself:**
> - [ ] Am I coaching my TLs on all three hats, or just evaluating them?
> - [ ] Am I giving TLs enough autonomy, or am I micromanaging because I used to be a TL myself?

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"When you were a tech lead, what was the hardest thing to let go of?"** For most Senior EMs, it was code. Recognizing what you lost — and still grieve — helps you empathize with TLs who are going through that same transition right now.
>
> 2. **"Do any of your tech leads remind you of the 'floundering TL' Fournier describes — technically brilliant but chasing rabbit holes while the team drifts?"** If so, what's stopping you from having that conversation? Refer back to the Feedback Avoider anti-pattern from Ch2.
>
> 3. **"Are you, as a Senior EM, guilty of any TL anti-patterns at your own level?"** The Alpha Geek shows up at Senior EM as "I'm the smartest management thinker in the room." The Process Czar shows up as "If we just implement the right OKR process / sprint cadence / incident framework, everything will be fine." The retreat-to-code shows up as "I'll just build this dashboard myself" instead of empowering a team to do it.

---

## How GenAI Is Reshaping the Tech Lead Role

> **[GenAI + Management]**

**AI makes the "code" hat easier and the "people" hats more important.** AI pair programmers (Copilot, Claude) can handle a significant portion of the coding that TLs do — generating boilerplate, writing tests, debugging. This frees TL time for the hats that AI can't wear: architecture decisions requiring judgment, project planning requiring human collaboration, team leadership requiring empathy.

**AI and project planning:** AI can help break down projects (listing tasks, identifying dependencies, estimating effort), but the *judgment* calls — what to cut when timelines slip, how to communicate risk to stakeholders, when to push back on requirements — remain human. AI can draft the project plan; the TL makes it real.

**AI and the alpha geek risk:** AI democratizes technical knowledge — junior engineers with good AI skills can punch above their weight technically. This threatens alpha geeks who derive their status from knowing more. It's a net positive for teams but requires TLs to shift their value from "knowing the answers" to "asking the right questions."

**AI and SRE tech leads specifically:** AI can triage alerts, draft incident summaries, suggest runbook steps, and analyze post-mortem patterns. This is genuinely useful — but the TL's judgment about severity, blast radius, communication strategy, and human factors during incidents remains irreplaceable.

**Further reading:**
- [Patrick Kua, *Talking with Tech Leads*](https://www.goodreads.com/book/show/23270194-talking-with-tech-leads) — the definitive companion to this chapter, with interviews from dozens of TLs
- [Paul Graham, "Maker's Schedule, Manager's Schedule"](http://www.paulgraham.com/makersschedule.html) — the original essay on time management for technical leaders
- [*The Staff Engineer's Path* by Tanya Reilly](https://www.oreilly.com/library/view/the-staff-engineers/9781098118730/) — for the IC track alternative Fournier describes
- [Gary Klein, "Performing a Project Premortem," HBR 2007](https://hbr.org/2007/09/performing-a-project-premortem) — the premortem technique Fournier mentions
- [Dave Snowden's Cynefin Framework](https://thecynefin.co/) — for matching management approach to problem complexity
