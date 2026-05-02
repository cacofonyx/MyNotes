# Chapter 4: Managing People

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "New engineering managers think of the job as a promotion, giving them seniority on engineering tasks and questions. This is a great approach for ensuring they remain junior managers, and unsuccessful leaders at that. It's hard to accept that 'new manager' is an entry-level job with no seniority on any front, but that's the best mindset with which to start leading." — Marc Hedlund

This chapter is the most practice-dense in the book — the full toolkit for managing individuals: onboarding new reports, running different styles of 1-1s, delegation vs. micromanagement, continuous feedback, performance reviews, cultivating careers, and firing underperformers. For a Senior EM, the relevance is twofold: you do these things for your reports (managers and TLs), AND you coach your managers to do them well for their reports.

## Table of Contents

- [Starting a New Reporting Relationship Off Right](#starting-a-new-reporting-relationship-off-right)
  - [Build Trust and Rapport](#build-trust-and-rapport)
  - [Create a 30/60/90-Day Plan](#create-a-306090-day-plan)
  - [Communicate Your Style and Expectations](#communicate-your-style-and-expectations)
  - [Get Feedback from Your New Hire](#get-feedback-from-your-new-hire)
- [Communicating with Your Team](#communicating-with-your-team)
  - [Different 1-1 Styles](#different-1-1-styles)
- [Good Manager, Bad Manager: Micromanager, Delegator](#good-manager-bad-manager-micromanager-delegator)
  - [Practical Advice for Delegating Effectively](#practical-advice-for-delegating-effectively)
- [Creating a Culture of Continuous Feedback](#creating-a-culture-of-continuous-feedback)
- [Performance Reviews](#performance-reviews)
- [Cultivating Careers](#cultivating-careers)
- [Challenging Situations: Firing Underperformers](#challenging-situations-firing-underperformers)
- [Quarterly Ritual: People Management Health Check](#quarterly-ritual-people-management-health-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping People Management](#how-genai-is-reshaping-people-management)

**Block types in this chapter:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## Starting a New Reporting Relationship Off Right

### Build Trust and Rapport

Fournier provides a specific list of questions to ask new reports:

- **How do you like to be praised, in public or in private?** — "Some people really hate to be praised in public. You want to know this."
- **What is your preferred method of communication for serious feedback?** — Written (time to digest) or verbal (less formal)?
- **Why did you decide to work here? What are you excited about?**
- **How do I know when you're in a bad mood or annoyed?** — "Maybe a direct report fasts for religious reasons, which sometimes makes him cranky. Maybe he always gets stressed out while on-call."
- **Are there any manager behaviors that you know you hate?** — Fournier's own answer: "skipping or rescheduling 1-1s, neglecting to give me feedback, and avoiding difficult conversations."
- **Do you have any clear career goals I should know about?**
- **Any surprises since you've joined, good or bad?**

She references Lara Hogan's blog post on the topic for more ideas.

> **[Leader's Playbook: The "User Manual" for Your Reports]**
>
> Fournier's question list is the seed of a practice that's become widespread since the book was published: the **Manager README** or **Personal User Manual**. The idea: both you and your report write a short document about how you work best, and share it.
>
> **Your README to them should include:**
> - How I prefer to communicate (Slack for quick things, email for anything requiring thought, 1-1 for anything sensitive)
> - What I expect from you (own your work, raise risks early, come to 1-1s prepared)
> - What I'm bad at (I sometimes forget to follow up — hold me accountable)
> - How I give feedback (directly, in private, usually within 24 hours)
> - Things that bother me (being surprised by bad news in a group meeting, passive-aggressive Slack messages)
>
> **Their README to you should answer Fournier's questions above plus:**
> - How do you learn best? (Reading, pairing, trial-and-error, structured training)
> - What's your working style? (Early bird, night owl, long focus blocks vs. frequent breaks)
> - What de-energizes you? (Meetings without agendas, ambiguous requirements, on-call during holidays)
>
> **SRE-specific additions:** "How do you handle being paged at 2 AM?" "What's your preferred incident communication style?" "Do you want me to join incident bridges when you're on-call, or do you prefer autonomy?"
>
> **[Go Deeper]** Lara Hogan's "Questions for our first 1:1" blog post at larahogan.me is the definitive reference.

### Create a 30/60/90-Day Plan

Create clear goals for new hires that are achievable in the first 90 days. "The more senior the hire, the more he should participate in creating this plan."

**Dual purpose:** Helps new hires learn the right things AND catches mis-hires quickly. "Create a set of realistic milestones based on your prior hires, the current state of your technology and project, and the level of the person coming in."

> **[SRE Lens: The SRE 30/60/90]**
>
> | Period | Goals | Evidence of Success |
> |--------|-------|-------------------|
> | **30 days** | Understand the team's systems, complete shadow on-call, commit first change, update onboarding docs | Can explain the top 5 services the team owns and their dependencies |
> | **60 days** | Complete first on-call rotation (with backup), contribute to a post-mortem, take on a small project | Handled an on-call shift without escalating more than peers do |
> | **90 days** | Own a meaningful project independently, contribute to SLO discussions, provide feedback on team processes | Delivering work at expected pace, integrated into team dynamics |
>
> **The mis-hire signal in SRE:** If by 60 days the person cannot handle a standard on-call shift or consistently needs hand-holding for routine operational tasks, you have a data point. Not a firing trigger — but a conversation trigger.

### Communicate Your Style and Expectations

"Your new hire needs to understand your expectations and your style just as much as you need to understand his." Be specific: how often you'll meet, how you'll share information, how often you'll review work, how long they should work alone before asking for help.

### Get Feedback from Your New Hire

"Get as much feedback as you can about the new hire's perspective on the team in that first 90 days. This is a rare period, where a new person comes in with fresh eyes." But take observations with appropriate context — they don't know the history.

> **[Insight]** The tension Fournier identifies — "fresh eyes are valuable but lack context" — is a management judgment call. The practice that resolves it: when a new hire critiques something, don't dismiss it OR act on it immediately. Instead, say "That's an interesting observation — here's the history behind why it's that way. Given what you now know, do you still think it should change?" This validates their perspective, provides context, and lets them refine their assessment. Often, after hearing the history, they'll STILL think it should change — and they're usually right.

---

## Communicating with Your Team

> "Regular 1-1s are like oil changes; if you skip them, plan to get stranded on the side of the highway at the worst possible time." — Marc Hedlund

**Default:** Weekly 1-1s. Adjust only if both parties agree it's more than needed. "Weekly means that you talk frequently enough to keep the meetings short and focused, and it gives you room for the occasional missed week."

**Scheduling advice:** Avoid Mondays and Fridays (long weekends). Try morning before things get busy. Respect maker schedules — don't put 1-1s in the middle of productive flow time.

**When to adjust frequency** — depends on:
- How often you interact offhand during the week
- How much coaching the person needs (junior = more, but also senior pushing through a hard project = more)
- How good the person is at pushing information up
- Quality of the relationship ("Don't make the fatal error of spending all your time with your problem employees and ignoring your stars")
- Stability of the team/company

### Different 1-1 Styles

Fournier describes five styles:

**1. The To-Do List Meeting:** Both parties come with a list. "Professional and efficient, if sometimes a bit cold." Danger: feels like it could've been an email. Fournier mentions a manager who used a shared Google spreadsheet — a practice now widespread.

**2. The Catch-up:** More fluid, driven by the report. Fournier's preferred style. "I view a 1-1 session as much as a creative discussion as a planning meeting." **Danger:** "If it's left unchecked, it can turn into a complaining session or therapy." She warns: "If you start focusing a lot of energy on hearing reports' complaints and commiserating, you're quite possibly making the problem worse."

**3. The Feedback Meeting:** Devoted to informal feedback and coaching. "Quarterly is frequent enough to give the topic attention without it feeling like all you talk about is career development." For underperformers: more frequent, and **document these meetings**.

Fournier gives critical timing advice: "If someone does something that needs immediate corrective feedback, don't wait for the 1-1... The longer you wait, the harder it will be for you to bring it up. The same goes for praise!"

**4. The Progress Report:** Only useful when someone is on a side project you're not overseeing. "If your 1-1s are frequently status updates, try breaking out of the habit."

**5. Getting to Know You:** "Leave room to get to know the person reporting to you as a human being." Career history, long-term goals, family, hobbies. "Show that you are invested in helping them now and in the future."

**Practical tip:** "Keep notes in a shared document, with you the manager playing note taker." Running notes of 1-1s, takeaways, to-dos — essential for writing reviews and remembering feedback given.

> **[Deep Dive: Choosing the Right 1-1 Style Per Person]**
>
> Fournier presents these as styles to choose between, but the real skill is **mixing them based on the person and the moment:**
>
> | Report Type | Primary Style | Why |
> |-------------|--------------|-----|
> | New hire (first 90 days) | Getting to Know You + To-Do List | Build rapport AND ensure onboarding is on track |
> | Junior engineer (year 1-2) | Catch-up + Feedback | They need space to raise concerns + regular coaching on growth |
> | Senior engineer (steady state) | Catch-up (they drive) | They know what they need; your job is to listen and unblock |
> | Senior engineer (stretch project) | To-Do List + Feedback | Structured check-ins on the project + coaching on new skills |
> | Tech Lead | Catch-up + Progress (on team, not themselves) | Discuss team dynamics, project risks, leadership challenges |
> | Manager (your report) | Catch-up + Progress + Feedback | Team health, project status, their growth as a manager |
> | Underperformer | Feedback + To-Do List (documented) | Clear expectations, documented progress, frequent check-ins |
>
> **The meta-skill:** Ask each report which style works best for them. Revisit quarterly. People's needs change.

> **[Anti-Pattern: The Therapy Session 1-1]**
>
> Fournier warns about 1-1s becoming "complaining sessions or therapy." This is a real trap, especially in SRE where there's always something to complain about (on-call burden, toil, unreliable systems, uncooperative product teams).
>
> **How to tell the difference:**
> - **Healthy venting:** The person names a specific problem, expresses frustration, then pivots to "here's what I think we should do." Duration: 5-10 minutes. Ends with energy.
> - **Therapy session:** The same problems come up every week. No solutions are proposed. The person leaves feeling temporarily better but nothing changes. Duration: the entire 1-1. Ends with both of you drained.
>
> **The correction (from Fournier):** "Problems in the workplace need to be either dealt with or put aside by mutual agreement." When you notice the pattern, name it:
>
> *"I've noticed we've talked about the on-call burden in three of our last four 1-1s. I hear you — it's a real problem. Let's either make a plan to address it this quarter, or agree that it's something we can't fix right now and stop spending our 1-1 time on it. Which would you prefer?"*

---

## Good Manager, Bad Manager: Micromanager, Delegator

Fournier illustrates with two parallel stories:

**Jane (Micromanager):** Gives TL Sanjay a big project. Gets worried about the deadline. Starts attending standups she normally skips, questions the team directly, looks through tickets and reassigns them, overrides a scope decision, then takes over the project entirely. Project ships — but Sanjay tells her he doesn't want to be TL anymore. He becomes disengaged. "Her best team member has become a low performer seemingly overnight."

**Sharell (Effective Delegator):** Gives Beth her first big project. Instead of tracking every detail, works with Beth to determine which meetings to attend and which details to escalate. Beth feels confident AND supported. When things get stressful, Beth enlists Sharell's help to cut scope. Beth emerges more confident and ready for bigger projects.

> "Autonomy, the ability to have control over some part of your work, is an important element of motivation. This is why micromanagers find it so difficult to retain great teams."

> "Delegation is not the same thing as abdication. When you're delegating responsibility, you're still expected to be involved as much as is necessary to help the project succeed."

> **[Mental Model: The Delegation Dial — Not a Binary]**
>
> Most managers think of delegation as on/off: either I do it or they do it. In reality, delegation is a spectrum:
>
> | Level | What You Do | What They Do | When to Use |
> |-------|------------|-------------|-------------|
> | **1. Tell** | Make the decision, tell them to execute | Execute your decision | Crisis situations, irreversible decisions with low TRM |
> | **2. Sell** | Make the decision, explain your reasoning | Execute with understanding of why | Important decisions where you need buy-in |
> | **3. Consult** | Ask for input, then you decide | Provide input and perspective | Complex decisions where you need expertise |
> | **4. Agree** | Discuss together, decide together | Share in decision-making | Decisions affecting both of you significantly |
> | **5. Advise** | They propose, you give advice/feedback | Make the decision with your input | Most decisions for experienced reports |
> | **6. Inquire** | They decide, tell you what they decided | Decide and inform | Routine decisions from trusted, experienced people |
> | **7. Delegate** | They decide, you don't need to know | Full ownership | Low-risk decisions, high-TRM individuals |
>
> **Jane's mistake:** She was at Level 5-6 (appropriate for Sanjay's experience), then panic-jumped to Level 1 when the deadline seemed at risk. The whiplash is what destroyed Sanjay's motivation.
>
> **Sharell's approach:** She started at Level 5 (Beth proposes, Sharell advises) and stayed there, adjusting the frequency of check-ins but never taking over control.
>
> *Source: Jurgen Appelo, "Delegation Poker and Delegation Board," Management 3.0*

> **[The Shadow Side: Delegation Becomes Abdication]**
>
> Fournier warns: "Delegation is not the same thing as abdication." The opposite of micromanagement isn't hands-off — it's **calibrated involvement.**
>
> **In SRE, abdication looks like:**
> - "I delegated the SLO review to my TL" → but you never check whether SLOs are actually being reviewed
> - "My team owns on-call" → but you don't review on-call burden metrics, and your team is silently burning out
> - "I trust my manager to handle performance issues" → but you never ask how their underperformer conversations are going
>
> **The test:** Can you describe, right now, the current status of the three most important projects across your teams? If not, you may have delegated past the point of awareness.

### Practical Advice for Delegating Effectively

Fournier's five principles:

1. **Use goals to decide what to dig into.** "If the team is making progress on its goals, the systems are stable, and the product manager is happy, I rarely dig into the details." If there are no clear goals, help the team create them first.

2. **Gather information from systems before going to people.** "Look at the version control system and the ticketing system. If you want to know how stable the systems are, subscribe to information about the alerts, look at the metrics." Don't constantly ask for info you could get yourself.

3. **Adjust focus by project stage.** More involved in beginning (design) and end (delivery). During normal workflow, "it's usually enough to know what's moving forward and what is taking longer than expected."

4. **Establish standards.** Code standards, testing requirements, when decisions need broader review. "Putting standards in place here helps people know which details are important."

5. **Treat sharing of information, good or bad, neutrally.** Don't punish people for sharing bad news. "If you treat a struggling engineer or project as a massive failure, she is going to hide information from you in the future."

> **[SRE Lens: Delegation and On-Call Autonomy]**
>
> SRE has a built-in delegation tension: you want on-call engineers to make autonomous decisions during incidents (speed matters), but you also need oversight of those decisions (blast radius matters).
>
> **The SRE delegation framework:**
> - **During incidents (P1-P2):** On-call engineer has full autonomy to take action. No approval needed for standard mitigations (restart, rollback, failover). Escalation required for non-standard actions (customer-facing communication, data-affecting changes).
> - **During project work:** Standard delegation based on seniority and TRM. Review designs before implementation, check in at milestones, review output.
> - **For SLO/error budget decisions:** These are strategic — you should be involved. But the *data collection* and *recommendation* should be delegated to the team.
>
> Fournier's "gather info from systems first" principle is gold for SRE managers. You have dashboards, alert histories, incident timelines, deployment logs, on-call metrics. Use them before asking your team "what's going on?"

---

## Creating a Culture of Continuous Feedback

Fournier describes continuous feedback as "a commitment to regularly sharing both positive and corrective feedback" — not waiting for the review cycle.

**Steps to be great at continuous feedback:**

1. **Know your people.** Goals, strengths, weaknesses, current operating level, areas for improvement. Read previous reviews AND ask for their perspective.

2. **Observe your people.** "You can't give feedback if you aren't paying attention." Look for talents and achievements first. "If you spend most of your time trying to get people to correct weaknesses, you'll end up with a style that feels more like continuous criticism."

**Practical habit:** "Task yourself with regularly identifying people who deserve praise. Every week there should be at least one thing you can recognize about someone on your team."

3. **Provide lightweight, regular feedback.** Start with positive — it's easier and makes people more receptive to later critical feedback. Give critical feedback quickly for obvious missteps. Use continuous feedback for things that "don't seem to be going well as you start to notice them."

4. **Bonus: Provide coaching.** Go beyond "good job" to engage with details and form a partnership. "Coaching is most important for your early-career team members, or those who have the potential or desire for advancement."

> **[Deep Dive: The SRE Feedback Challenge — "Nothing Bad Happened" Is Not Observable]**
>
> SRE creates a unique feedback problem: much of the team's best work is **invisible**. The incident that DIDN'T happen because your engineer wrote a good alert. The outage that was 5 minutes instead of 5 hours because someone wrote a great runbook. The reliability improvement that prevented 3 incidents per quarter.
>
> **How to give feedback on invisible work:**
> - Track and celebrate **negative metrics** going down: "Our MTTR dropped from 45 min to 12 min this quarter. That's because of the runbook overhaul you led. I want to make sure you know that matters."
> - Praise incident response *skills*, not just outcomes: "The way you communicated during Tuesday's incident — clear status updates, appropriate escalation, calm under pressure — that's exactly the model I want for the team."
> - Make toil reduction visible: "You automated the certificate rotation. That's 4 hours per month we'll never spend on that again. Let's make sure this shows up in your review."
> - During on-call handoffs, ask the incoming person: "Was anything noteworthy about the outgoing person's shift?" Surface the quiet competence.

> **[Script: Giving Corrective Feedback That Builds Trust]**
>
> Your SRE manager (your direct report) has been avoiding a difficult conversation with their underperforming engineer for weeks. You need to give them feedback on giving feedback:
>
> *"I want to check in on the situation with [underperforming engineer]. Last time we talked, you said you'd have a direct conversation with them about the quality issues. What happened?"*
>
> [They say they haven't had the conversation yet — "it didn't feel like the right time."]
>
> *"I understand — these conversations are uncomfortable. But here's what I'm seeing: every week this goes unaddressed, [engineer]'s teammates pick up the slack, and their frustration grows. Right now the problem is contained — it's a performance conversation with one person. If we wait much longer, it becomes a team morale problem, which is much harder to fix.*
>
> *I want to help you prepare for this conversation. Let's spend 15 minutes right now scripting what you'll say, and let's commit to you having it before next Friday. I'll check in with you next 1-1 on how it went. Does that work?"*
>
> **Why this works:** You're not doing their job for them (which would be micromanagement). You're coaching them on HOW to do it (which is what their manager should be doing). You set a specific deadline. You offer concrete help (scripting together). And you created accountability (will check next 1-1).

---

## Performance Reviews

Fournier covers the 360 model extensively: feedback from manager, teammates, reports, coworkers, plus self-review.

**Value:** "360 reviews give you at least a high-level view into what other people are thinking about your direct reports." The writing process forces you to look at the big picture over a longer period.

**How they go wrong:** Not enough time prioritized, recency bias, underlying biases, and some managers don't take them seriously.

### Writing and Delivering Performance Reviews

**Give yourself enough time.** "Plan to spend solid, uninterrupted time working on reviews. Work from home if you need to."

**Account for the whole year, not just recent months.** Keep running notes from 1-1s. Look through email to recall projects month by month.

**Use concrete examples and excerpts from peer reviews.** "If you can't use a concrete example to support a point, ask yourself if the point is something you should be communicating."

**Spend plenty of time on accomplishments and strengths.** Don't let people skip to areas for improvement. "Those strengths are what you'll use to determine when people should be promoted."

**Keep areas for improvement focused.** Look for themes in peer feedback. Use judgment on scattershot feedback — "If only one reviewer mentions sloppy work, is the problem that the work is sloppy, or that the reviewer has higher standards?"

**What if there's little meaningful feedback for improvement?** "This indicates that the person is ready to be promoted or given more challenging work."

**Avoid big surprises.** "If someone is underperforming across the board, the review should not be his first time getting that feedback."

**Schedule enough time for discussion.** Fournier gives the review printed the evening before, so people can read at home and come prepared. "Don't let them skip over [strengths] and jump straight into the areas for improvement."

> **[Senior EM vs. Director: Performance Review Responsibility]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Who you review** | Your direct reports (TLs, managers, senior ICs) | Your direct reports (Senior EMs, managers) |
> | **Calibration role** | Ensure your own reviews are fair and consistent | Calibrate across your managers — ensure THEIR reviews are fair and consistent |
> | **Bias mitigation** | Watch for your own biases (recency, affinity) | Watch for systemic biases across your org (gender, tenure, team visibility) |
> | **Quality assurance** | Write strong reviews yourself | Review your managers' review drafts and coach them to improve |

> **[Anti-Pattern: The Copy-Paste Review]**
>
> You're managing 8 people and review season hits while you're also handling a production migration. You pull up last year's reviews, update the projects section, change a few adjectives, and send them off. Time saved: hours. Trust destroyed: immeasurable.
>
> **Why it's damaging:** Your reports can tell. When the "areas for improvement" are the same as last year, with no acknowledgment that they addressed them, the message is: "My manager doesn't pay attention to my growth." When the strengths section is generic ("great team player, solid technical skills"), the message is: "My manager doesn't actually know what I do."
>
> **The fix:** If you're too busy to write good reviews, that's a capacity problem — raise it with your director. Don't solve it by delivering bad reviews. One strong review with specific examples is worth more than five generic ones.

---

## Cultivating Careers

Fournier shares her experience with the VP promotion process in finance — gathering evidence of projects shipped, signs of leadership, and work beyond the immediate team. "My boss/mentor knew exactly how to play the game."

**Your role as manager:**
- Learn how the promotion process works at your company. "How are these decisions made? How early do you need to start preparing packets?"
- Be transparent with your team about the process
- Identify promotion-worthy projects and assign them to people who are close to promotion
- Recognize that "many companies expect you to be acting at the next level before you get promoted"

**On "potential":** Fournier pushes back hard on credential-based potential assessment:

> "A person who has never shown reasonable performance, and who has been with a company long enough for you to observe performance, probably doesn't actually have potential, at least within that company."

> "Real potential shows itself quickly. It shows itself as working hard to go the extra mile, offering insightful suggestions on problems, and helping the team in areas that were previously neglected."

> **[Insight]** The "potential" passage is one of the most contrarian and important in the book. Fournier is pushing back against a deeply held bias in tech: that pedigree (school, previous company, interview performance) equals potential. Her claim is that potential is visible in *actions*, not credentials. "The sooner you can get over the disappointment that a high-potential person didn't work out, the sooner you can identify the true high-potential stars." For a Senior EM, this means: stop giving the benefit of the doubt to the engineer who interviews brilliantly but delivers inconsistently. Start paying attention to the quiet engineer who keeps making the team better in ways no one asked them to.

> **[SRE Lens: What SRE Promotion Evidence Looks Like]**
>
> SRE work is often poorly captured by standard promotion criteria ("shipped features," "led projects"). Coach your team to document:
> - Incidents resolved and what they did specifically (not "helped with incident" but "identified root cause in 12 minutes by correlating error rates across three services")
> - Toil eliminated with measurable impact (hours saved per month/quarter)
> - Reliability improvements with business impact (MTTR reduced, availability increased, customer-facing errors decreased)
> - Systems designed or improved (monitoring frameworks, deployment pipelines, chaos experiments)
> - Cross-team influence (taught product teams about SLOs, influenced architecture decisions, championed a reliability practice)
> - On-call improvements (reduced pages by X%, improved handoff process, created training materials)

---

## Challenging Situations: Firing Underperformers

Fournier provides practical guidance on the most dreaded management task.

**The performance improvement plan (PIP):** "A set of clearly defined objectives that the person must achieve within a fixed period of time." She's candid: "Often the plan is written in such a way that the person can't possibly hope to achieve the goals in the allotted time, and it's just a generous way of giving someone time to look for another job."

**The core rule:** "The process of coaching someone out should begin long before any performance improvement document is filed with HR." Rule of no surprises.

**Coaching out vs. firing:** When someone is stuck and can't grow to the next level despite your efforts, be clear: "You aren't firing him, but you are telling him that he needs to move on if he wants to progress." Let them go with goodwill.

**Warning:** "Don't put anyone on a plan whom you wouldn't be happy to lose." Smart employees take a PIP as a signal to leave.

> **[Deep Dive: The Underperformance Spectrum in SRE]**
>
> Not all underperformance is the same. The diagnosis determines the intervention:
>
> | Pattern | What It Looks Like | Root Cause | Intervention |
> |---------|-------------------|------------|--------------|
> | **Skill gap** | Can't handle incidents at expected level, slow to learn systems | Wrong level or insufficient training | Coach, train, pair. Give 90 days with support. |
> | **Will gap** | Capable but disengaged. Does minimum. Avoids stretch. | Burnout, wrong role, personal issues | Honest conversation about what's going on. May need a change (role, team, break). |
> | **Culture gap** | Technically fine but toxic — dismissive, blaming, hoarding knowledge | Personality mismatch or Alpha Geek | Direct feedback with concrete behavior changes. If no improvement in 60 days, likely need to exit. |
> | **Misalignment** | Doing good work, but not the right work | Unclear goals, wrong team, interests diverge | Realign goals or help them find a better fit (coaching out). |
>
> **The SRE-specific trap:** Keeping underperforming on-call engineers too long because "we can't afford to lose headcount." Every month an underperformer is on the rotation, the rest of the team carries extra burden, which burns out your good people. The "can't afford to lose them" calculation should include the cost of the stronger people you'll lose by keeping the weaker one.

> **[Interview Angle]**
>
> Very common Director-level question: "Tell me about a time you had to let someone go" or "How do you handle underperformance?"
>
> **Strong answer structure:**
> 1. **The pattern you observed** — specific, documented, objective
> 2. **The feedback you gave** — show you didn't jump to firing; you gave clear, specific, documented feedback with a timeline
> 3. **The support you provided** — coaching, training, pairing, role adjustment. Show you tried.
> 4. **The decision point** — how you knew it wasn't going to work despite your efforts
> 5. **How you handled the exit** — with dignity, goodwill, and fairness
> 6. **What you learned** — about your hiring process, onboarding, feedback cadence, or your own management
>
> **The Director-level nuance:** Also mention how you've coached YOUR managers through this process. "I've had to fire someone once myself, but more importantly, I've coached three of my managers through their first termination. The coaching is harder than doing it yourself, because you have to let them do it while making sure the person being exited is treated fairly."

---

## Quarterly Ritual: People Management Health Check

> **[Quarterly Ritual]**
>
> **Weekly:**
> - [ ] Every report had their 1-1 (no cancellations without same-week reschedule)
> - [ ] I gave at least one piece of specific, named feedback this week
> - [ ] I checked the systems (dashboards, tickets, alerts) before asking my team for status
>
> **Monthly:**
> - [ ] Each report knows their top priority and why it matters
> - [ ] I've done one career-focused 1-1 with each report (not just operational topics)
> - [ ] Anyone underperforming has received documented feedback with specific expectations
>
> **Quarterly:**
> - [ ] Every report has an up-to-date development plan they're excited about
> - [ ] I've reviewed my delegation levels — am I micromanaging anyone? Abdicating anyone?
> - [ ] I've re-read Fournier's list of new-report questions and asked them of anyone I've managed <6 months
> - [ ] Performance conversations are documented — no one will be surprised at review time
> - [ ] I've identified at least one promotion-track project and matched it to a developing report
> - [ ] I've reviewed on-call burden data — is the distribution equitable across the team?

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"Think about the last performance review you wrote. Would YOU want to receive that review?"** If it's generic, vague, or could apply to anyone on the team, it fails the test. Every review should contain at least one thing that could only apply to that specific person.
>
> 2. **"Where on the delegation spectrum do you default?"** Fournier shows that micromanagement and abdication are both failures. Most managers have a default — are you a Jane or a Sharell? And does your default change under stress? (Most of us micromanage more under pressure — which is exactly when we need to delegate more.)
>
> 3. **"Is there someone on your team right now who you suspect is underperforming but you haven't had the conversation?"** Fournier is blunt: feedback avoidance is management failure. If the answer is yes, what's stopping you? Name the specific fear. Then decide: is that fear worth the cost of inaction?
>
> 4. **"How would your team describe your feedback style — do they get enough, too much, or the wrong kind?"** You might think you're giving continuous feedback, but your reports may experience it differently. The only way to know is to ask.

---

## How GenAI Is Reshaping People Management

> **[GenAI + Management]**

**AI and performance reviews:** AI can help draft review summaries from running 1-1 notes, peer feedback, and project data. This reduces the "I forgot what happened 9 months ago" problem Fournier describes. But the *judgment* — weighing conflicting peer feedback, identifying the right themes, deciding what's fair — remains human. Use AI as a first draft, never a final draft.

**AI and continuous feedback:** AI tools can remind you to give feedback ("You haven't given specific feedback to [report] in 2 weeks"), surface data to support feedback ("[report]'s PR merge rate has increased 40% this quarter"), and help you phrase difficult feedback. But delivering it face-to-face with empathy and nuance? That's you.

**AI and the "invisible SRE work" problem:** AI can help surface and quantify the work that's hardest to see — toil hours automated away, incident response improvements, on-call burden trends — making it easier to give specific feedback and write promotion cases for SRE work that traditional metrics miss.

**AI and delegation:** AI can handle many of the "gather information from systems" tasks Fournier describes — summarizing project status from tickets, tracking deployment frequency, monitoring alert trends. This frees you to spend your time on the human judgment that AI can't do: deciding when to step in, when to coach, and when to let your team learn from their own mistakes.

**Further reading:**
- [Lara Hogan, "Questions for our first 1:1"](https://larahogan.me/blog/first-one-on-one-questions/) — the definitive reference Fournier points to
- [*Radical Candor* by Kim Scott](https://www.radicalcandor.com/) — the feedback framework that complements this chapter perfectly
- [*High Output Management* by Andy Grove](https://www.penguinrandomhouse.com/books/324878/high-output-management-by-andrew-s-grove/) — the classic on task-relevant maturity and managerial leverage
- [*The Hard Thing About Hard Things* by Ben Horowitz](https://www.harpercollins.com/products/the-hard-thing-about-hard-things-ben-horowitz) — especially Chapter 6 on firing, the most honest treatment in print
- [*Thanks for the Feedback* by Stone & Heen](https://www.penguinrandomhouse.com/books/313485/thanks-for-the-feedback-by-douglas-stone-and-sheila-heen/) — understanding why feedback is hard to receive, from the receiver's perspective
- [Jurgen Appelo, "Delegation Poker"](https://management30.com/practice/delegation-poker/) — the delegation levels model referenced in this chapter
