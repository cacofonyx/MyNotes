# Chapter 1: Management 101

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

This opening chapter is written from the **perspective of the managed, not the manager**. Fournier deliberately starts here because your management philosophy is built on your experience of being managed. The chapter establishes what you should expect from a good manager, how to be managed effectively, and how to own your own career. Even as a Senior EM, this chapter is worth internalizing — because how you want to be managed by *your* director is a mirror of what your reports should expect from you.

> "The secret of managing is keeping the people who hate you away from the ones who haven't made up their minds." — Casey Stengel

## Table of Contents

- [What to Expect from a Manager](#what-to-expect-from-a-manager)
  - [One-on-One Meetings](#one-on-one-meetings)
  - [Feedback and Workplace Guidance](#feedback-and-workplace-guidance)
  - [Training and Career Growth](#training-and-career-growth)
  - [Ask the CTO: Big Ambitions](#ask-the-cto-big-ambitions)
- [How to Be Managed](#how-to-be-managed)
  - [Spend Time Thinking About What You Want](#spend-time-thinking-about-what-you-want)
  - [You Are Responsible for Yourself](#you-are-responsible-for-yourself)
  - [Give Your Manager a Break](#give-your-manager-a-break)
  - [Choose Your Managers Wisely](#choose-your-managers-wisely)
- [Assessing Your Own Experience](#assessing-your-own-experience)
- [Quarterly Ritual: The Management Foundation Check](#quarterly-ritual-the-management-foundation-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping Management Fundamentals](#how-genai-is-reshaping-management-fundamentals)

**Block types in this chapter:** [Deep Dive] [Insight] [SRE Lens] [Senior EM vs. Director] [Anti-Pattern] [Script] [Scenario] [Leader's Playbook] [Red Flags] [Cross-Functional Play] [Interview Angle] [Mental Model] [The Shadow Side] [Influence Without Authority] [First 90 Days] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## What to Expect from a Manager

Fournier opens by asking a disarmingly simple question: *Have you ever had a good manager?* She observes that many engineers have never had one. The "best" managers some people have experienced practiced **"benign neglect"** — leaving the engineer alone to figure things out, meeting rarely, providing no feedback.

She names the common archetypes of bad managers:
- **Neglectful managers** — ignore you, brush off concerns, never give feedback, then suddenly tell you you're not meeting expectations
- **Micromanagers** — question every detail, refuse to let you make decisions
- **Abusive managers** — neglect you until they want to yell at you

Against these, she describes what *good* managers do: care about you as a person, actively help you grow, teach important skills, give valuable feedback, help you navigate difficult situations, and most importantly — **help you understand what is important to focus on, and enable you to have that focus.**

> **[Insight]** That last phrase — "help you understand what is important to focus on, and enable you to have that focus" — is Fournier's definition of a manager's core job, distilled to its essence. Not "tell you what to do" or "evaluate your performance." But *clarity* and *unblocking*. As a Senior EM managing multiple teams, this is your primary deliverable to your direct reports (tech leads and managers): not solving their problems, but ensuring they know which problems matter and have the space to solve them. If your reports are consistently confused about priorities or constantly blocked, that's a management failure — yours.

> **[SRE Lens]** In SRE specifically, "enable focus" has an operational dimension. Your teams are constantly pulled between project work (improving reliability, building platforms) and reactive work (incidents, toil, escalations). A good SRE manager protects focus time aggressively — ensuring the team isn't drowning in interrupt-driven work. The error budget model (from Google SRE) is essentially a management tool that operationalizes this: when the error budget is healthy, the team focuses on projects; when it's burning, the team focuses on reliability. Without this clarity, SRE teams default to firefighting 100% of the time.

> **[Senior EM vs. Director: "Enable Focus"]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Scope of clarity** | Sets priorities for your 2-3 teams | Sets priorities for the SRE function / org-wide reliability strategy |
> | **Unblocking** | Removes obstacles for your teams (tooling, process, cross-team deps) | Removes obstacles for your managers (headcount, budget, exec alignment, political blockers) |
> | **Focus protection** | Shields teams from ad-hoc requests and meeting bloat | Shields the entire org from reactive whiplash; negotiates with VP/C-level on what NOT to do |
> | **Time horizon** | This quarter's priorities are clear | This year's direction is clear, next year's is emerging |

> **[Red Flags: You're Not Enabling Focus]**
>
> - Your reports frequently say "I'm not sure what I should be working on" or "everything is priority 1"
> - Teams are context-switching between 4+ projects simultaneously
> - On-call engineers are being pulled into project work during their on-call shift (or vice versa)
> - You yourself can't articulate the top 3 priorities for each of your teams right now
> - Your teams are doing work because "someone asked for it" rather than because it connects to stated goals

> **[Mental Model: Task-Relevant Maturity (Andy Grove, *High Output Management*)]**
>
> Grove's framework answers: *How much should I be involved in this person's work?* The answer depends not on their overall seniority but on their **experience with the specific task at hand.**
>
> | Task-Relevant Maturity | Manager Approach | Example |
> |------------------------|-----------------|---------|
> | **Low** (new to this type of work) | Structured, detailed guidance. Frequent check-ins. Tell them what, when, how. | A senior SRE who's technically strong but is leading a cross-org architecture proposal for the first time. |
> | **Medium** (some experience, building confidence) | Collaborative. Discuss goals and approaches together. Less "how," more "what." | An SRE manager who's done one performance review cycle and is entering their second. |
> | **High** (deep experience, proven track record) | Light-touch. Set objectives, agree on metrics, get out of the way. Monitor results. | Your most experienced tech lead running an incident they've seen five variants of. |
>
> **The critical mistake:** Treating seniority as a proxy for task-relevant maturity. Your Staff SRE with 15 years of experience has *low* task-relevant maturity if they've never given a presentation to executives, managed a vendor relationship, or led a hiring loop. They need coaching on those tasks even though they need zero coaching on systems design.
>
> **For you as a Senior EM:** Your director should be adjusting their management of *you* based on task-relevant maturity too. If you've never driven an org-wide strategy document, you have low TRM for that task, and it's appropriate to ask your director for more structure and review — that's not a sign of weakness, it's intelligent self-management.

> **[The Shadow Side: Clarity Becomes Rigidity]**
>
> The strength of "enable focus" is that your teams always know what to work on. The shadow side: you become so focused on *your* priorities that you can't adapt when conditions change. A P1 incident reveals a systemic problem that doesn't fit your quarterly plan. A team member discovers an opportunity that's not on the roadmap. A VP asks for something that disrupts your neat prioritization.
>
> **How rigidity shows up in SRE:**
> - You resist reprioritizing even when production data clearly shows your assumptions were wrong
> - Your team is afraid to propose new ideas because "it's not in the quarterly plan"
> - You dismiss requests from other teams as "distractions" without evaluating whether they're actually higher-impact than your current work
>
> **The correction:** Clarity about priorities is NOT the same as inflexibility about priorities. Build explicit "re-evaluation triggers" into your planning: "If our error budget burns below 30%, we pause Project X and shift to reliability." "If a P1 root cause reveals a systemic pattern, we reprioritize within 48 hours." The best plans are firm on direction and flexible on specifics.

---

### One-on-One Meetings

1-1s serve **two purposes:**

**1. Human connection.** Not small talk for its own sake, but building enough context that stressful life events (death in family, new child, breakup, housing problems) can be communicated naturally. Great managers notice when your energy level changes.

Fournier addresses introverts directly:

> "Being an introvert is not an excuse for making no effort to treat people like real human beings. The bedrock of strong teams is human connection, which leads to trust. And trust, real trust, requires the ability and willingness to be vulnerable in front of each other."

**2. A regular private opportunity** to discuss whatever needs discussing. Should be scheduled predictably. **Not the manager's meeting to control** — the report should come with their own topics.

**What 1-1s are NOT (for ICs):** Status meetings. If your 1-1 is a boring status report, use email/chat for status and bring real topics to the 1-1.

**Shared responsibility:** Fournier puts equal onus on the managed person to make 1-1s valuable — come with an agenda, prepare, push back if meetings are constantly canceled.

> **[Deep Dive: The 1-1 as a Senior EM]**
>
> At your level, you're on both sides of the 1-1 equation:
>
> **With your director (you're being managed):** Fournier says senior people should drive their own 1-1s. For a Senior EM → Director relationship, effective 1-1 topics include:
> - Strategic alignment: "Here's what I'm prioritizing and why — does this match your expectations?"
> - Organizational challenges: "I'm seeing friction between Team X and Team Y, here's my plan"
> - Your own growth: "I want to develop skill X for the Director role — can you help me find opportunities?"
> - Preemptive escalation: "This project has a risk I want you to be aware of before it becomes a problem"
>
> **With your reports (you're managing):** You likely manage tech leads and managers. Common mistakes at this level:
> - Turning 1-1s into status meetings (you should get status from dashboards and standups)
> - Only talking about fires (you should be proactively coaching on growth)
> - Talking more than listening (your reports should talk 70%+ of the time)
>
> **The SRE-specific 1-1 trap:** SRE managers often let 1-1s devolve into incident debriefs or on-call reviews. These are valid operational topics, but if that's ALL you discuss, you're neglecting career development, team dynamics, and strategic thinking. Dedicate at least half of every 1-1 to non-operational topics.

> **[Anti-Pattern: The 1-1 Hijacker]**
>
> You sit down for your 1-1 with your report. They open their doc — they have three topics. But before they speak, you say: "Before we get to your stuff, let me tell you about the leadership meeting yesterday..." Twenty minutes later, you've vented about org politics, they've politely listened, and there are 10 minutes left for their three topics.
>
> **Why this happens:** Senior EMs carry enormous cognitive load. Your 1-1 is the first time in a busy day you have a captive, sympathetic listener. It's *relieving* to talk.
>
> **Why it's damaging:** Your report leaves feeling unheard. Over time, they stop preparing topics because "it's always about your stuff anyway." They stop bringing problems because there's no time. You lose your best signal about what's happening on the ground.
>
> **The fix:** Hard rule — their items first. Always. If you have something to share, add it to the shared doc beforehand so it competes fairly for time. If you need to vent, find a peer, not a report.

> **[Anti-Pattern: The Absent SRE Manager]**
>
> "I trust my team — they're senior, they don't need me hovering." This sounds enlightened but often masks neglect. You skip 1-1s because of incident bridges. You reschedule because of a production issue. A month goes by and you've met with each report once or twice.
>
> **Why it's especially dangerous in SRE:** SRE teams have a culture of self-reliance and "just handle it." Your senior engineers will NOT tell you they're burning out — they'll just quietly update their LinkedIn. The on-call rotation keeps running, incidents keep getting resolved, and one day your best person gives two weeks notice, and you're blindsided.
>
> **The fix:** 1-1s are as non-negotiable as your production SLOs. If you cancel, you reschedule within the same week. Period.

> **[Leader's Playbook: Running Effective 1-1s]**
>
> 1. **Set a shared doc** for each report. Both of you add topics before the meeting. Whoever has more urgent items goes first.
> 2. **Weekly for managers you manage, biweekly for senior TLs** who are more autonomous. Never less than biweekly.
> 3. **Rotate structure:** Week 1 = their agenda, Week 2 = career/growth, Week 3 = their agenda, Week 4 = feedback exchange.
> 4. **First question every time:** "What's on your mind?" (from *The Coaching Habit* by Michael Bungay Stanier). This gives them control.
> 5. **Never cancel.** Reschedule if needed, but never cancel. Canceling signals "you're not important."
> 6. **End with:** "Is there anything else you haven't said?" — this surfaces the thing they've been holding back for the entire meeting.

> **[Script: Opening a 1-1 When You Sense Something Is Off]**
>
> You notice your tech lead has been quiet in meetings, their code review comments are shorter, and they skipped the team lunch. In your 1-1:
>
> *"Hey, I wanted to check in on how you're doing — not on projects, just on you. I've noticed you seem a bit less energized lately, and I want to make sure I'm not missing something. No pressure to share anything you're not comfortable with, but I want you to know I'm paying attention and I care."*
>
> **Why this works:**
> - Names the observation without diagnosing ("less energized" not "you seem unhappy")
> - Separates the person from the work ("not on projects, just on you")
> - Gives explicit permission to not share ("no pressure")
> - Signals you're attentive without being intrusive
>
> **What NOT to say:** "Is everything okay?" (too easy to brush off with "yeah fine"), "Are you looking for a new job?" (accusatory), "You seem checked out" (judgmental).

> **[Interview Angle]**
>
> EM interviews almost always ask: "How do you run 1-1s?" or "Tell me about your management cadence." A strong answer for a Senior EM/Director-level candidate:
> - Show you have a **system** (shared doc, predictable cadence, rotating structure)
> - Emphasize that **the report owns the agenda** (shows you empower, not control)
> - Give a **concrete example** of a 1-1 that led to an important outcome (catching burnout early, identifying a promotion opportunity, surfacing a team conflict)
> - Mention **differentiation** — you adapt 1-1 style based on the person's seniority and needs
> - For Director-level: mention **skip-level 1-1s** and how you use them to calibrate your managers

---

### Feedback and Workplace Guidance

Fournier establishes several feedback principles:

**Timely feedback beats convenient feedback.** If your manager grabs you right after a meeting to give critical feedback, that's a sign of a *good* manager, not that you did something terrible. Speed matters more than setting.

**Praise publicly, criticize privately.** Standard best practice — but Fournier adds: "If you don't like public praise, tell your manager!" Preferences vary.

**Feedback is bidirectional.** You should actively *ask* for feedback — on presentations, design docs, communication. "Asking your manager for advice is also a good way to show respect."

**Your manager as career ally.** At companies with career ladders, ask your manager explicitly what you need to focus on for promotion. If you're struggling with a teammate, bring it to your manager. "If you don't ask your manager about a promotion, do not expect her to just give you one magically."

**The mundane work reframe.** Good managers help you see how unglamorous work fits into the team's goals and the company's mission. "The most mundane work can turn into a source of pride when you understand how it contributes to the overall success of the company."

**Senior-level feedback shift:** As you become more senior, personal feedback decreases. Expect the type to shift from personal behavioral feedback to **team- or strategy-related input.** It becomes even more important to *drive* your own feedback-seeking.

> **[Deep Dive: The Feedback Gap at Senior Levels]**
>
> This is one of the most important passages for someone at your level. Fournier is describing a real and dangerous phenomenon: **the higher you go, the less honest feedback you receive.** Your director is less likely to tell you "that meeting you ran was unfocused" than a peer manager would have told you 5 years ago. Your reports are unlikely to tell you "your communication style is intimidating" because of the power dynamic.
>
> **Why this happens:**
> - Your manager (director/VP) has less visibility into your day-to-day behavior
> - Your reports are afraid of negative consequences
> - Your peers are busy with their own problems
> - You're expected to "just know" at this level
>
> **How to fight it:**
> - **Skip-level 1-1s** (ask your reports' reports how things are going — you'll hear things your directs won't tell you)
> - **360 feedback** processes (formal or informal)
> - **Explicitly ask** for constructive feedback: "What's one thing I could do differently that would make your job easier?" Not "Do you have any feedback?" — the specific question gets specific answers
> - **Trusted peer network** — find 2-3 peers at your level (inside or outside the company) who will be brutally honest with you
> - **Post-incident self-reflection** — after major incidents, ask yourself not just "what went wrong technically" but "how did I handle the leadership aspects?"

> **[Mental Model: Radical Candor 2x2 (Kim Scott)]**
>
> Scott's framework is the best practical companion to Fournier's feedback principles. It maps two dimensions:
>
> |  | **Challenge Directly** (high) | **Don't Challenge** (low) |
> |--|-------------------------------|--------------------------|
> | **Care Personally** (high) | **Radical Candor** — The goal. You care enough to tell the truth. "Your incident review facilitation has been shutting people down. Let me explain what I'm seeing." | **Ruinous Empathy** — You care, so you stay silent to avoid discomfort. The person never improves. The team suffers quietly. *Most common failure mode for empathetic managers.* |
> | **Care Personally** (low) | **Obnoxious Aggression** — You're blunt but don't bother to frame it with care. "Your incident reviews are terrible." Technically accurate, relationally destructive. | **Manipulative Insincerity** — You neither care nor challenge. You say "great job" to their face and complain about them to peers. The most toxic quadrant. |
>
> **The key insight for Senior EMs:** Most of us live in **Ruinous Empathy**. We care deeply about our people and avoid hard conversations precisely *because* we care. Scott's framework reframes avoidance as a failure of caring: if you truly cared, you'd tell them the truth so they could improve. Silence isn't kindness — it's a form of abandonment.
>
> **[Go Deeper]** Read chapters 1-2 of *Radical Candor* for the full framework including the "HHIPP" model for delivering feedback (Humble, Helpful, Immediate, In Person, Private for criticism / Public for praise).

> **[Anti-Pattern: The Feedback Avoider]**
>
> You have a tech lead who is technically brilliant but alienates junior engineers with dismissive code review comments. You've noticed it for months. You keep thinking "it's not that bad" or "they'll figure it out." You don't say anything.
>
> Six months later, two junior engineers have transferred to other teams, citing "team culture" in their exit surveys. Your director asks what happened. You didn't give feedback when it was a small, correctable behavior, and it festered into a retention problem.
>
> **Why this happens to Senior EMs specifically:** At this level, your reports are often senior/staff engineers or other managers. Giving them critical feedback feels uncomfortable because they're experienced and you respect their expertise. The higher the seniority, the more we avoid the conversation.
>
> **The cost:** Avoiding feedback is not neutral — it's actively harmful. Every week you don't address the behavior, it becomes more normalized and harder to change, and more people are affected.

> **[Script: Giving Difficult Feedback to a Senior Report]**
>
> Your staff SRE has been dismissive in incident reviews, shutting down less experienced engineers:
>
> *"I want to talk about something I've observed in our recent incident reviews, and I want to share it because I think it's undermining something we both care about — building a team where everyone contributes to learning from incidents.*
>
> *In the last two reviews, I noticed that when [junior engineer] raised observations, you responded with 'that's not relevant' without exploring further. In both cases, the observations actually had merit — one of them was a contributing factor we almost missed.*
>
> *The impact I'm seeing is that less experienced team members are going quiet. They're not sharing observations anymore. And for SRE, that's dangerous — we need every pair of eyes during incidents.*
>
> *I know you don't intend to shut people down — you're focused on efficiency. But I need you to find a way to be direct without being dismissive. What if you tried 'Tell me more about what you're seeing' before evaluating whether it's relevant?*
>
> *How does this land with you?"*
>
> **Why this works:**
> - Opens with shared value ("something we both care about"), not accusation
> - Uses SBI: specific Situation, specific Behavior, specific Impact
> - Acknowledges positive intent ("you're focused on efficiency")
> - Offers a concrete alternative behavior ("tell me more about...")
> - Ends with an open question, not a command

> **[The Shadow Side: Empathy Becomes Avoidance]**
>
> Being empathetic is a genuine strength — and it's one Fournier explicitly values ("care about you as a person"). But the dark version of empathy is conflict avoidance dressed up as caring.
>
> **How it manifests:**
> - You delay a difficult performance conversation because "they're going through a tough time" — and the tough time lasts six months
> - You don't address interpersonal conflict on the team because "they're adults, they'll work it out" — and one of them quietly leaves
> - You give feedback so gently that the person doesn't register it as feedback: "You might want to think about maybe being a little more concise in meetings" vs. "Your meeting facilitation needs to improve. Here's specifically what I need to see change."
>
> **The test:** Ask yourself: "Am I protecting this person, or am I protecting *myself* from an uncomfortable conversation?" If it's the latter, that's avoidance, not empathy.
>
> **For SRE managers:** The operational culture of SRE — objective, data-driven, blameless — can actually help here. Framing feedback around data ("your on-call handoffs have resulted in 3 missed context items this month") is easier than purely behavioral feedback, and SRE managers have natural access to this data. Use it.

> **[SRE Lens]** In SRE, the "mundane work reframe" is a daily challenge. Toil reduction, runbook updates, monitoring tuning, on-call rotation management — none of it is glamorous. But as a Senior EM, your job is to connect this work to its impact: "By reducing toil by 20%, we freed up 2 engineers' worth of capacity for the reliability project that prevents the kind of outage that cost us $2M last quarter." Your ability to make this connection — and make your team *feel* it — is a core management skill.

> **[Scenario: The Toil Rebellion]**
>
> Your SRE team has spent the last quarter doing unglamorous but essential work: migrating alerting rules to a new platform, writing runbooks for 30 services, and fixing flaky integration tests. Morale is low. A senior engineer says in your 1-1: "I didn't join SRE to write documentation. When are we going to work on real engineering?"
>
> **Applying Fournier's "mundane work reframe":**
>
> *"I hear you — this quarter hasn't been the most exciting. Let me share why I prioritized this work. Before the migration, our mean time to detect was 12 minutes and we had 3 incidents per month where the on-call couldn't find the right runbook. After this work, we should see detection drop to under 5 minutes and on-call burden decrease significantly. That's the equivalent of giving every on-call engineer their weekends back. The documentation you wrote is going to prevent the kind of 3 AM scramble that happened in March. That's real engineering — it's engineering for the humans who operate the system.*
>
> *That said, you're right that we need to balance this with more technically challenging work. Let's talk about what you'd like to take on next quarter — I want to make sure you're growing."*
>
> **What this does:** Validates the feeling, connects mundane work to human impact, and pivots to growth — hitting all three of Fournier's expectations (purpose, feedback, career growth) in one conversation.

> **[Interview Angle]**
>
> Common question: "How do you give difficult feedback?" or "Tell me about a time you had to deliver bad news to a report."
>
> Strong answer structure (SBI model):
> - **Situation:** "In a post-incident review, I noticed my tech lead had been dismissive of an on-call engineer's observations..."
> - **Behavior:** "...specifically, they cut them off twice and said 'that's not relevant'..."
> - **Impact:** "...which shut down a junior engineer who actually had important context, and the team missed a contributing factor."
> - **What you did:** "I pulled the TL aside within the hour, used SBI to describe what I observed, asked for their perspective, and we agreed on how to handle it differently."
> - **Follow-up:** "In the next incident review, they actively solicited input from the same engineer."
>
> **Director-level elevation:** Also mention how you've built a *culture* of feedback, not just given it individually. "I introduced a practice where every team retro includes a 'what can we do better' section, and I model vulnerability by sharing my own mistakes first."

---

### Training and Career Growth

Your manager is the **main liaison** between you and company bureaucracy — helping find conferences, classes, books, experts, and training resources.

**Key caveat:** "Expect that you are responsible, for the most part, for figuring out what types of training you want." Your manager won't have a list of conferences at their fingertips.

**Promotion mechanics:** Your manager is involved in the promotion process — whether it's committee-based (guiding you through packet preparation) or hierarchy-determined (advocating for you). "Good managers know what the system is looking for and can help you build those achievements and skills."

**At senior levels:** "Opportunities for promotion are much more rare, and your manager may need you to find and propose the achievements that qualify you for the next level."

> **[Deep Dive: The Senior EM → Director Promotion]**
>
> Fournier's point about finding and proposing your own promotion case is especially relevant for you. The Senior EM → Director transition is one of the hardest in engineering management because:
>
> 1. **The scope change is qualitative, not quantitative.** It's not "manage more teams" — it's "set organizational direction, own cross-cutting strategy, influence without authority at the VP level."
>
> 2. **You must demonstrate the next level before you get the title.** Your director needs to see you already operating as a Director (influencing org strategy, driving cross-team initiatives, developing other managers) before promoting you.
>
> 3. **You need to articulate what "Director-level impact" looks like** in your specific context. For SRE, this might be:
>    - Defining the reliability strategy for a business unit, not just executing it
>    - Building the SRE function's maturity model and driving adoption across multiple product teams
>    - Influencing engineering-wide architectural decisions based on operational data
>    - Developing 2-3 managers who can independently run their teams
>    - Owning the relationship with senior product/business stakeholders on reliability
>
> **Tactical move:** Write a self-assessment of what you've done at Director scope in the last 6 months. Share it with your director and ask: "What's missing from this picture for me to be ready?"

> **[Senior EM vs. Director: Career Development Responsibility]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Who you develop** | Your direct reports (TLs, managers, senior ICs) | Your managers (who develop their own teams) + high-potential ICs you sponsor |
> | **Growth strategy** | Individual development plans per report | Career ladder design, promotion pipeline health, succession planning |
> | **Training investment** | Ensure team has conference/training budget | Build org-wide learning programs (dojos, guilds, rotation programs) |
> | **Promotion role** | Write promotion packets, advocate in review | Calibrate across teams, ensure fair/consistent bar, coach your managers to advocate well |

> **[Leader's Playbook: Investing in Your Team's Growth]**
>
> As a Senior EM, you're now the one *providing* career growth, not just receiving it. For SRE specifically:
>
> - **Conference budget:** Ensure every team member attends at least one conference per year (SREcon, KubeCon, Monitorama, DevOpsDays). Budget for it proactively.
> - **Rotation programs:** Rotate engineers between on-call teams, project work, and cross-team collaboration. SRE skills atrophy when people are stuck on one service forever.
> - **Tech talks and learning time:** Institute weekly tech talks or "learning Fridays." SRE teams that don't invest in learning stagnate.
> - **Career laddering:** If your company doesn't have an SRE-specific ladder, build one. Define what Staff SRE, Principal SRE, and SRE Manager look like. Without this, your people will leave because they see no growth path.
> - **Stretch assignments:** Deliberately assign projects slightly above someone's current level. The engineer who's never led an architecture review should lead the next one — with your coaching support.

> **[Cross-Functional Play: Growth Through SRE's Unique Position]**
>
> SRE sits at a cross-functional intersection that creates unique growth opportunities you can offer your team:
>
> - **Product partnership:** Have an SRE engineer join sprint planning for a product team they support. They'll learn product thinking; the product team gains reliability awareness.
> - **Security collaboration:** Post-incident reviews often surface security implications. Send an SRE to partner with the security team on a threat modeling exercise.
> - **Business exposure:** Bring a senior SRE into the capacity planning conversation with finance. Understanding cost/reliability tradeoffs from the business side is a rare skill that accelerates careers.
> - **Customer empathy:** If possible, have SREs observe customer support interactions during outages. Hearing "I can't access my account" from a real customer changes how someone thinks about SLOs.

---

### Ask the CTO: Big Ambitions

A new engineer asks: *"How do I become a CTO?"*

Fournier's advice (condensed):
1. **Learn how to work first** — the day-to-day of being a professional engineer
2. **Find the best managers and mentors** — watch them work, learn from them
3. **Build a strong peer network** — "current peers will turn into your future jobs"
4. **Communication, project management, and product sense** matter as much as technical skills
5. **Most CTOs are CTOs of small companies** — often technical cofounders. Work at companies that are "startup factories."

> **[SRE Lens]** Fournier's advice about communication and product sense applies directly to SRE leadership careers. The most impactful SRE leaders aren't the most technically deep — they're the ones who can translate reliability into business language. "We need to invest in reducing MTTR" means nothing to a VP of Product. "Our checkout page goes down for 45 minutes per quarter, costing us ~$1.5M in lost revenue, and I have a plan to cut that to 5 minutes for $200K of engineering investment" — that's speaking their language. This skill — translating technical risk into business terms — is the single biggest differentiator between SRE managers who stay at Senior EM and those who become Directors and VPs.

> **[Script: Translating SRE Into Business Language]**
>
> **In a leadership meeting where you need budget for a reliability initiative:**
>
> Don't say: *"We need to reduce our P99 latency on the payments service from 2s to 500ms and improve our error rate from 99.9% to 99.95%."*
>
> Do say: *"Our payments service is slow enough that 3% of customers abandon checkout — that's approximately $4M in lost revenue annually. I have a plan to fix this in one quarter with 2 engineers. The expected return is a 1.5% improvement in checkout conversion, worth roughly $2M per year. The total investment is about $200K in engineering time."*
>
> **The formula:** Problem in customer/business terms → impact quantified in dollars → proposed solution with cost → expected return. Always lead with the "so what" for the business, not the technical details.

> **[Cross-Functional Play: Building Your Network for Director+]**
>
> Fournier says "current peers will turn into your future jobs." At your level, this means deliberately building relationships with:
> - **Product Directors/VPs** — they need to see you as a strategic partner, not a cost center
> - **Engineering Directors in other functions** — peer relationships that become collaboration when you're both Directors
> - **Finance/Business leaders** — understanding their language and constraints is a Director prerequisite
> - **External SRE leaders** — SREcon, DevOps Enterprise Summit, local meetups. Your external reputation matters for Director-level hiring and influence.

> **[Influence Without Authority: Getting Product to Prioritize Reliability]**
>
> This is the most common "influence without authority" challenge for SRE leaders. A product team owns a service with degrading reliability. You have data showing it's causing customer impact. But they own the roadmap, and their OKRs are about feature velocity, not uptime.
>
> **Tactics that work:**
>
> 1. **Translate to their language.** Don't say "SLO violation." Say "Your checkout funnel drops 3% of users when latency exceeds 2 seconds. That's $X per month." Product managers respond to revenue, not nines.
>
> 2. **Make the cost of inaction visible.** "Your team spent 47 hours on incident response last quarter. That's the equivalent of one engineer for a month. If we invest 2 weeks in fixing the root causes, you get that capacity back for feature work."
>
> 3. **Offer to do the work, not just identify the problem.** "My team can pair with your engineers on this for two sprints. We'll bring the reliability expertise; you provide the domain knowledge. By the end, your team will own the fix and the monitoring."
>
> 4. **Escalate with data, not emotion.** If persuasion fails, escalate — but escalate with a one-page brief showing: customer impact data, engineering cost data, proposed solution, and what you've already tried. Let the data make the case, not your frustration.
>
> 5. **Use error budgets as a shared contract.** If your org has adopted SLOs, the error budget is the ultimate "influence without authority" tool. When the budget is exhausted, the policy (agreed upon in advance) mandates reliability investment. The conversation shifts from "SRE wants something" to "the system says it's time."
>
> **[Go Deeper]** Chapter 5 of *Crucial Conversations* (Patterson et al.) covers how to maintain dialogue when stakes are high and opinions differ — the exact dynamic of SRE↔Product negotiations.

---

## How to Be Managed

Fournier pivots to the other side: how to be an effective *managee*. This section is framed as advice for ICs, but every principle applies to how you interact with your own director.

### Spend Time Thinking About What You Want

> "Your manager can point out opportunities for growth. But she cannot read your mind, and she cannot tell you what will make you happy."

Fournier shares her own career uncertainty — going to grad school to escape a job she didn't know how to navigate, hitting uncertainty after climbing the technical ladder, then again after reaching executive leadership. "I expect I'll experience it every 5 to 10 years until I retire."

> "In all of this uncertainty, the only person you can rely on to pull through it is yourself. Your manager cannot do that for you."

> **[Insight]** This is Fournier at her most honest and least managerial. She's saying: uncertainty never goes away, and no one else can resolve it for you. For a Senior EM eyeing Director, this means sitting with the discomfort of "Do I actually want to be a Director, or do I want the title?" The Director role is fundamentally different from Senior EM — more politics, more ambiguity, less direct impact on teams you care about, more accountability for outcomes you don't directly control. Fournier herself experienced this: she climbed the ladder and found the challenges different, not fewer. The question isn't "Can I do it?" — it's "Is this what I want, knowing what it actually entails?"

> **[Scenario: The Director Offer You're Not Sure About]**
>
> Your director leaves the company. Their boss offers you the Director role — managing your current peers (other Senior EMs). It's what you've been working toward. But something feels off.
>
> **Applying Fournier's principle — "think about what you want":**
>
> Before you accept, ask yourself:
> - Am I excited about the *work* of a Director (org strategy, managing managers, cross-functional influence, less hands-on), or just the title and compensation?
> - Can I manage my former peers without resentment or awkwardness — theirs or mine?
> - Is this the right organization to grow into the role, or will I inherit a mess with no support?
> - What does my gut say when I imagine the first Monday morning in the new role?
>
> **The non-obvious option:** It's okay to say "not yet" or "not this one." Taking the wrong Director role can be worse than waiting for the right one. A Director role with no executive support, a team in crisis, and former-peer dynamics can set you back years.

### You Are Responsible for Yourself

Fournier's most direct, no-nonsense passage:

> "When you are persistently unhappy, say something. When you are stuck, ask for help. When you want a raise, ask for it. When you want a promotion, find out what you need to do to get it."

> "Your manager cannot force work–life balance on you. If you want to go home, figure out how to get your work done and go home."

> "You will not get everything you ask for, and asking is not usually a fun or comfortable experience. However, it's the fastest way forward."

> **[Leader's Playbook: Teaching Self-Advocacy to Your Reports]**
>
> As a manager, you *want* your reports to do what Fournier describes here. But many engineers — especially from cultures that value deference — won't naturally advocate for themselves. Your job is to:
>
> 1. **Explicitly invite it:** "What do you want to be working on in 6 months?" / "Is there anything you need that you haven't asked for?"
> 2. **Reward it when it happens:** When a report advocates for themselves well, acknowledge it: "I'm glad you brought this up. Let me see what I can do."
> 3. **Model it yourself:** Share (appropriately) how you advocate for your team and yourself. "I asked my director for budget to send three people to SREcon, and here's how I made the case."
> 4. **Coach the skill:** "Instead of saying 'I feel like I should be promoted,' try 'Here's what I've accomplished at the next level, and I'd like to discuss the gap.'"

> **[Anti-Pattern: The Martyr Manager]**
>
> You work 60-hour weeks, handle escalations at 2 AM, skip vacations, and never complain. You think this demonstrates dedication. Meanwhile, your reports see you burning out and conclude: "This is what management looks like here. I don't want that."
>
> **The damage:** You're not just hurting yourself — you're signaling to your team that self-destruction is the price of leadership. Your best potential future managers opt out of management entirely. Your existing reports feel guilty taking PTO because "the boss never does."
>
> **Fournier's principle applied:** "Your manager cannot force work-life balance on you" — and YOU cannot force it on your reports either if you're not modeling it. You have to go home. You have to take vacation. You have to let the P3 incident wait until morning. Your team will follow what you *do*, not what you say.

> **[Red Flags: Your Reports Aren't Self-Advocating]**
>
> - Promotion surprises: A strong performer is passed over and didn't even know they were being considered (or not considered). They should have been driving that conversation.
> - Passive dissatisfaction: You hear through the grapevine that someone is unhappy, but they've never mentioned it to you directly.
> - "Whatever you think" syndrome: When you ask reports what they want to work on, they defer to you. Every time.
> - PTO avoidance: Engineers don't take vacation, not because of workload but because they haven't internalized that they're *allowed*.
>
> All of these signal a culture where people don't feel empowered to own their experience — exactly what Fournier warns against.

### Give Your Manager a Break

> "This is a job. Your manager will be stressed out sometimes. She'll be imperfect."

> "Your relationship with your manager is like any other close interpersonal relationship. The only person you can change is yourself."

> "If you find yourself starting to actively resent your manager for whatever reason, you probably need to move to a different team or look for a new job. If you find yourself resenting *every* manager you work for, you may need to think about whether the cause is them or you."

**The senior-level rule:** "Remember that your manager expects you to bring solutions, not problems. Try not to make every 1-1 about how you need something, how something is wrong, or how you want something more."

> **[Insight]** "Bring solutions, not problems" is common advice that's commonly misunderstood. It does NOT mean "never escalate problems" or "pretend everything is fine." It means: when you bring a problem, also bring your analysis and a proposed approach. "We have a reliability problem with Service X" is a problem dump. "Service X has had 3 incidents in 2 weeks. I've analyzed the root causes, and I believe we need to invest 2 sprints in addressing technical debt in the database layer. Here's my proposed plan — does this align with your priorities?" — that's a solution-oriented escalation. Your director wants to see your *judgment*, not just your detection.

> **[Script: Escalating to Your Director — Solution-Oriented]**
>
> You need to tell your director that a critical platform migration is going to miss its deadline:
>
> Don't say: *"The migration is behind schedule. We're going to miss the deadline."*
>
> Do say: *"The platform migration is tracking 3 weeks behind our target. Root cause is that the legacy API had undocumented dependencies we discovered during testing — 14 services that weren't in our original inventory. I have three options: (A) extend the timeline by 4 weeks with no additional resources, (B) bring in 2 engineers from the reliability team to parallelize the remaining work and hit within 1 week of the original date, or (C) migrate the 20 highest-traffic services by the deadline and handle the remaining 14 in a follow-up phase. I recommend option C because it delivers 85% of the value on time and doesn't disrupt the reliability team's Q3 goals. What do you think?"*
>
> **Why this works:** Your director sees your judgment (analyzed root cause), your strategic thinking (three options with tradeoffs), and your recommendation. They can approve, redirect, or add context. They don't have to do the thinking.

> **[SRE Lens]** For SRE managers specifically, "bring solutions, not problems" means resisting the urge to use your 1-1 as an incident replay. Your director doesn't need to hear about every P2. They need to hear: "Our incident rate is trending up. Here's my analysis of why, here's my plan to address it, and here's where I need your help (budget/headcount/exec alignment)."

### Choose Your Managers Wisely

> "Strong managers know how to play the game at their company. They can get you promoted; they can get you attention and feedback from important people. Strong managers have strong networks, and they can get you jobs even after you stop working for them."

**Key distinction:** "There's a difference between a strong manager and a manager that you like as a friend, or even one you respect as an engineer." Great engineers often make ineffective managers because they don't know or want to deal with the politics of leadership.

> **[Deep Dive: Evaluating Your Own Manager as a Senior EM]**
>
> At your level, "choosing your manager" means evaluating whether your current director can help you reach Director yourself. Questions to ask:
>
> 1. **Does your director have organizational influence?** Can they get headcount approved, push back on unreasonable asks from VPs, and advocate for your promotion in leadership forums?
> 2. **Do they develop people?** Have other Senior EMs under them been promoted to Director? If not, why?
> 3. **Do they give you strategic exposure?** Do they bring you into director-level meetings, let you present to VPs, give you ownership of cross-team initiatives?
> 4. **Are they transparent about the game?** Do they tell you how promotion decisions actually work, who the key stakeholders are, what the political landscape looks like?
> 5. **Will they sponsor you, not just mentor you?** Mentors give advice. Sponsors put their reputation on the line to advocate for you in rooms you're not in. You need a sponsor.
>
> If the answer to most of these is "no," Fournier's advice applies: consider whether this is the right manager for your growth, even if you like them personally.

> **[Red Flags: Your Director May Be Blocking Your Growth]**
>
> - They never bring you into strategic conversations — you only hear decisions after they're made
> - They take credit for your initiatives in leadership forums
> - When you ask about promotion, they give vague answers: "just keep doing what you're doing"
> - They are themselves struggling or checked out — they can't sponsor you if they're barely surviving
> - They actively discourage you from building relationships outside your org ("you don't need to talk to the VP of Product")
> - Other Senior EMs under them have been in role for 3+ years without promotion or clear progress

> **[Mental Model: One-Way vs. Two-Way Doors (Jeff Bezos)]**
>
> Bezos distinguishes between two types of decisions:
>
> - **One-way doors (Type 1):** Irreversible or very costly to reverse. Shutting down a team, choosing a core architecture, making a senior hire. These deserve deliberation, data-gathering, and broad input.
> - **Two-way doors (Type 2):** Reversible with low cost. Trying a new 1-1 format, adjusting on-call rotation structure, choosing a monitoring tool for a pilot. These should be decided quickly — you can always walk back through the door.
>
> **The Senior EM trap:** Treating every decision like a one-way door. You agonize over the team meeting format. You run a committee to choose an alerting tool. You defer deciding the on-call compensation policy for months while gathering input. Meanwhile, your team is stuck waiting for decisions that don't require this level of deliberation.
>
> **The Director trap (looking ahead):** Treating one-way doors like two-way doors. Moving fast on decisions that are actually hard to reverse — restructuring teams, committing to multi-year platform bets, setting SLOs that become contractual — without adequate analysis.
>
> **Applying it:** Before every decision, ask: "Is this a one-way or two-way door?" If two-way: decide today. If one-way: take time, but set a deadline. Most management decisions (including most of what Fournier discusses in this chapter — 1-1 format, feedback approach, team rituals) are two-way doors. Try something, see if it works, adjust.

> **[First 90 Days: If You Started a New Senior EM Role Tomorrow]**
>
> Based on Michael Watkins' *The First 90 Days* framework, adapted for a Senior EM in SRE joining a new organization:
>
> **Days 1-30: Learn (resist the urge to fix)**
> - [ ] Meet every direct report 1-1. Ask: "What's working? What's broken? What would you change if you could?"
> - [ ] Meet every key cross-functional partner (Product leads, Engineering Directors, Security, Finance). Ask: "What do you need from SRE that you're not getting?"
> - [ ] Review: incident history (last 6 months), SLO dashboards, on-call burden metrics, team attrition data, current roadmap
> - [ ] Identify the 3 biggest risks that no one is talking about
> - [ ] Understand the political landscape: who has influence, who are allies, where are the fault lines
> - [ ] **Do NOT** change the on-call rotation, reorg teams, or introduce new processes. Not yet.
>
> **Days 30-60: Diagnose and quick wins**
> - [ ] Share your initial assessment with your director: "Here's what I'm seeing, here's what I think matters most, here's what I want to tackle first. What am I missing?"
> - [ ] Pick one visible quick win that builds credibility (fix the longest-standing toil item, resolve a chronic inter-team friction, unblock a stuck project)
> - [ ] Start building your management cadence: 1-1 schedule, team meetings, skip-levels, cross-functional syncs
> - [ ] Begin 1-1 shared docs with every report
>
> **Days 60-90: Act on what you've learned**
> - [ ] Present your 90-day assessment and proposed priorities to your director and peers
> - [ ] Begin the first meaningful initiative (the one that addresses the biggest risk you identified in month 1)
> - [ ] Set or refine team goals and communicate the "why" clearly
> - [ ] Solicit feedback on your first 90 days: "What's one thing I should do differently going forward?"
>
> **The meta-principle:** The biggest mistake new Senior EMs make is acting before understanding. The second biggest is understanding forever and never acting. 30 days of learning, then increasing bias toward action.
>
> **[Go Deeper]** *The First 90 Days* by Michael Watkins is the canonical reference. For an SRE-specific take, see Liz Fong-Jones' talks on building SRE teams from scratch at SREcon.

---

## Assessing Your Own Experience

Fournier closes with self-reflection questions:

- Have you had a manager you considered good? What did they do that was valuable?
- How often do you meet 1-1 with your manager? Do you bring topics?
- Do you feel you can tell your manager about major life events? Does your manager know something about you personally?
- Has your manager delivered good feedback? Bad feedback? Any feedback at all?
- Has your manager helped you set work-related goals for this year?

> **[Leader's Playbook: Turn These Questions on Yourself]**
>
> As a Senior EM, flip every question and ask it about yourself:
>
> - Would your reports say you're a good manager? What specifically would they point to?
> - Are your 1-1s valuable to your reports, or do they dread them?
> - Do you know your reports well enough to notice when something is off?
> - When was the last time you gave specific, actionable feedback to each of your reports? (If you can't remember, it's been too long.)
> - Does every one of your reports have clear goals for this year that *they* are excited about?
>
> **The Director-readiness test:** If your reports can answer "yes" to all of Fournier's questions about you, you're building the management foundation that Director-level leadership requires. If they can't, that's your development area before anything else.

---

## Quarterly Ritual: The Management Foundation Check

> **[Quarterly Ritual]**
>
> Every quarter, spend 60 minutes auditing your management foundations against this chapter's principles. This is your "management SLO review."
>
> **Weekly health (check these are happening):**
> - [ ] Every direct report had their 1-1 this week (no cancellations without reschedule)
> - [ ] I gave at least one piece of specific feedback (positive or constructive) to a report this week
> - [ ] I spent at least one 1-1 on career/growth topics, not just operational issues
>
> **Monthly health (check these in your monthly self-review):**
> - [ ] I conducted at least one skip-level conversation this month
> - [ ] I actively sought feedback on my own management from at least one source
> - [ ] Each team knows their top 3 priorities and can articulate why
> - [ ] I had at least one conversation with a cross-functional peer (Product, Security, Finance)
>
> **Quarterly health (this is the 60-minute audit):**
> - [ ] Every report has a current, written development plan with goals they're excited about
> - [ ] I can articulate what "next level" looks like for each of my reports — and they know too
> - [ ] I've reviewed on-call burden and toil metrics — is the balance between project and reactive work healthy?
> - [ ] I've shared at least one "mundane work → business impact" narrative with each team
> - [ ] I've updated my own Director-readiness self-assessment and discussed it with my director
> - [ ] I've reviewed my management anti-patterns list: Am I hijacking 1-1s? Avoiding feedback? Being a martyr?
>
> **The meta-question:** If I were hired from outside to replace myself today, what would I fix first? That's your highest-priority management improvement.

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> Find a trusted peer — another Senior EM, a manager friend outside your company, or a coach. Discuss these questions honestly. They're designed to surface blind spots that self-reflection alone can't reach.
>
> 1. **"Think about the last person who left your team voluntarily. Did you see it coming? If not, what signal did you miss — and what does that tell you about how well you actually know your people?"** If you saw it coming and couldn't prevent it, that's one thing. If you were blindsided, your 1-1s are not working.
>
> 2. **"When was the last time you received genuinely uncomfortable feedback from someone who reports to you — not a peer, not your boss, but someone *below* you in the hierarchy?"** If you can't remember, the power dynamic in your relationships is preventing honest upward feedback. What could you change to make it safer for them?
>
> 3. **"If your team described your management style to a stranger in three words, what would those words be? Now: what three words do you *want* them to say?"** The gap between these two sets is your development area. If you're not sure what they'd actually say, that itself is the gap — you don't have enough feedback.
>
> 4. **"Are you managing your team the way you wish you were managed — or the way *they* need to be managed?"** Fournier's chapter is about what YOU want from a manager. The trap is assuming your reports want the same thing. The engineer who wants autonomy and the engineer who wants structure need different management, even though they're at the same level.

---

## How GenAI Is Reshaping Management Fundamentals

> **[GenAI + Management]**

The concepts in this chapter — 1-1s, feedback, career growth, self-advocacy — are fundamentally human and won't be replaced by AI. But AI is changing the *context* in which they operate:

**AI and 1-1 Preparation:** AI tools can help both managers and reports prepare for 1-1s — summarizing recent work, drafting talking points, reviewing past action items. This lowers the prep burden that Fournier describes as essential but often skipped. Tools like Fellow, Hypercontext, and AI-powered meeting assistants are emerging in this space.

**AI and Feedback:** AI can help managers draft difficult feedback (using frameworks like SBI), review written feedback for tone and clarity, and even analyze communication patterns to surface blind spots. But the *delivery* of feedback — the human connection, the trust, the vulnerability — remains irreducibly human.

**AI and Career Growth for SRE:** AI is reshaping which SRE skills are most valuable. Routine toil (writing runbooks, basic monitoring queries, incident triage) is being automated. The skills that become MORE valuable: system design judgment, cross-team communication, strategic reliability thinking, business-impact analysis. As a manager, helping your team develop these future-proof skills is increasingly important.

**AI and Self-Advocacy:** AI can help engineers articulate their accomplishments more effectively — drafting self-reviews, structuring promotion packets, preparing for difficult conversations. This is a net positive: the engineers who struggle most with self-advocacy (often underrepresented groups) stand to benefit most.

**The meta-question for managers:** As AI handles more routine technical work, the *management* skills Fournier describes become relatively MORE important, not less. The ability to build trust, give feedback, develop people, and create clarity of focus — these are the skills that will differentiate humans in an AI-augmented workplace.

**Further reading:**
- [*The Coaching Habit* by Michael Bungay Stanier](https://boxofcrayons.com/the-coaching-habit-book/) — the best practical complement to Fournier's 1-1 advice
- [*Radical Candor* by Kim Scott](https://www.radicalcandor.com/) — the framework for feedback that this chapter points toward
- [*An Elegant Puzzle* by Will Larson](https://press.stripe.com/an-elegant-puzzle) — the engineering management companion focused on systems and organizational design
- [*Thanks for the Feedback* by Stone & Heen](https://www.penguinrandomhouse.com/books/313485/thanks-for-the-feedback-by-douglas-stone-and-sheila-heen/) — deep dive on receiving and giving feedback effectively
- [Google's re:Work — Manager Behaviors](https://rework.withgoogle.com/guides/managers-identify-what-makes-a-great-manager/) — data-driven research on what makes effective managers
- [*Becoming a Technical Leader* by Gerald Weinberg](https://www.goodreads.com/book/show/714344.Becoming_a_Technical_Leader) — the classic on leadership in technical organizations
- [SREcon Talks Archive](https://www.usenix.org/conferences/byname/925) — for SRE-specific leadership talks and case studies
