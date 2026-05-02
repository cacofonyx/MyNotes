# Chapter 6: Managing Multiple Teams — Part 1

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "If your team needs a manager more than they need an engineer, you have to accept that being that manager means that you by definition can't be that engineer." — Cate Huston

This chapter marks the transition to **Director-level management** — the point where you stop writing production code and start managing the *systems* that produce code. Fournier is explicit: "your schedule has probably moved away from 'maker' and firmly into 'manager.'" The chapter covers how to stay technically relevant without coding, how to manage your time when everything feels urgent, how to delegate effectively, and how to measure team health through technical signals.

For a Senior EM aiming at Director, this is your destination chapter. Everything here describes what your next role looks like.

**Part 1 covers:** The Director job description, staying hands-on without coding, time management, the "I miss code" transition, decisions and delegation.
**Part 2 covers:** Technical health signals, measuring development teams, us-versus-them dynamics, the virtues of laziness and impatience.

## Table of Contents — Part 1

- [The Director Role](#the-director-role)
- [Staying Hands-On Without Writing Code](#staying-hands-on-without-writing-code)
- [Ask the CTO: I Miss Code!](#ask-the-cto-i-miss-code)
- [Managing Your Time](#managing-your-time)
- [Decisions and Delegation](#decisions-and-delegation)
- [Ask the CTO: Warning Signs](#ask-the-cto-warning-signs)

**Block types in Part 1:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Influence Without Authority] [First 90 Days] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## The Director Role

Fournier shares her Director-level job description. Key elements:

- **Not expected to write code daily**, but responsible for the organization's overall technical competence
- Should have a strong technical background, spend time researching new technologies, stay abreast of trends
- Expected to help debug and triage critical systems, perform code reviews, and research problems as needed
- **Primarily concerned with ensuring smooth execution of complex deliverables**
- Responsible for creating "high-performance, high-velocity organizations"
- Owns recruiting, headcount planning, career growth and training
- Impact should reach across multiple areas of the technology organization
- Responsible for creating the next generation of leadership talent
- Must strategically balance immediate product/business work with technical debt and strategic technical development
- Strong cross-functional collaborator who can simplify technical concepts for non-technical partners AND explain business direction to the tech team

> **[Insight]** Read that job description carefully. The word "code" appears only in the context of what you DON'T do much of. The action verbs are: ensuring, creating, measuring, iterating, recruiting, growing, balancing, collaborating, simplifying, explaining, guiding. This is an organizational leadership job with a technical lens, not a technical job with leadership responsibilities. The sooner you internalize this distinction, the smoother your Director transition will be.

> **[Senior EM vs. Director: The Role Shift]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Relationship to code** | Writes small features, bug fixes. Reviews code. Feels the developer experience. | Rarely writes code. Reviews architecture. Ensures process health. |
> | **Relationship to teams** | Manages one team (maybe two) directly. Knows every team member well. | Manages multiple teams through TLs and managers. Knows team health through signals and skip-levels. |
> | **Primary deliverable** | Team execution: ship commitments, maintain quality. | Organizational health: velocity, retention, quality, cross-team alignment. |
> | **Time in meetings** | 40-60% | 70-85% |
> | **Biggest danger** | Getting pulled into code and neglecting management | Getting pulled into meetings and neglecting strategy |

---

## Staying Hands-On Without Writing Code

Fournier lists ways to maintain technical credibility without writing production code:

- **Code reviews** as a secondary reviewer, especially for systems you created
- **Debugging and production support** — joining incident response where your knowledge adds value
- **Pair programming** on minor bugs or features
- Keep a **creative block of time** — at least half a day per week free from meetings for writing blog posts, preparing talks, contributing to open source, or other creative technical work

She makes a strong statement about prerequisite technical depth: you need to have achieved deep fluency in at least one programming language before going into management. "Eventually even the deepest knowledge will atrophy, but fluency... is something that sticks with you for a long time." Without this fluency, you'll struggle with "debugging team issues and keeping your teams producing quality software smoothly."

> **[SRE Lens: Staying Hands-On in SRE Leadership]**
>
> SRE Directors have natural staying-hands-on channels that product engineering Directors don't:
>
> - **Incident command:** Not as primary responder, but as escalation point or incident commander for major outages. This keeps you connected to system behavior, team capabilities, and tooling quality.
> - **Post-incident reviews:** Attend every P1 and selectively attend P2s. Read every postmortem. The patterns across incidents are visible only at your level.
> - **SLO reviews:** Monthly SLO dashboard reviews with each team. Not just red/green — dig into why metrics moved.
> - **Architecture reviews for operability:** When any team proposes a new service or significant change, review it through an operational lens. Failure modes, monitoring, runbook requirements, on-call impact.
> - **On-call burden analysis:** Quarterly review of pages per rotation, after-hours burden, escalation frequency. This is data only you synthesize across teams.
>
> **The creative half-day:** For SRE Directors, this might be writing internal engineering blog posts about reliability learnings, preparing SREcon talks, contributing to open-source SRE tooling, or writing the reliability strategy document.

> **[Anti-Pattern: The Director Who Can't Let Go]**
>
> You've been promoted to Director. You have 3 teams. But you still review every PR for the team you used to manage. You attend their standups. You debug their production issues. Your other two teams feel neglected. Their managers feel like you don't trust them.
>
> **Why this happens:** The team you know best is comfortable. Your technical contributions there feel tangible. Your other teams are less familiar, so engaging with them requires effort and vulnerability.
>
> **The cost:** Your former team doesn't grow because you're still doing the management work. Your other teams underperform because they lack your attention. You're a bottleneck, not a multiplier.
>
> **The fix:** Force yourself to spend LESS time with your former team and MORE time with the teams you're least comfortable with. Trust your former team's manager — that's why they exist. Your job is now to make ALL your teams successful, not to keep being the best manager of one team.

---

## Ask the CTO: I Miss Code!

Someone managing two complex teams asks if missing code is a sign they shouldn't be a manager.

Fournier's answer: **Almost everyone experiences this.** It's a transition, not a misfit signal.

Key points:
- Ask yourself if you've "internalized the idea that management is not a job" — the tech industry is full of people who despise management and think it's less important than coding
- Coding is full of "quick wins" — tests passing, features coming to life. Management has fewer obvious quick wins.
- "It's natural to feel some longing for simpler times" — it's like nostalgia for school days when you first started working
- "Becoming a great manager requires you to focus on the skills of management, and that requires giving up some of your technical focus"

> **[Insight]** Fournier names the real issue: the tech industry systematically devalues management. Engineers who become managers absorb this prejudice and then feel guilty about not coding. The longing for code isn't always about the code itself — it's about the dopamine of clear, measurable accomplishment in an environment (management) where accomplishments are fuzzy and delayed. A successful 1-1 doesn't give you the same rush as a passing test suite. But over time, seeing an engineer you coached get promoted, or a team you built ship something amazing — those payoffs are larger and more meaningful than any single code commit.

> **[Scenario: The Director Who Codes at Night]**
>
> You're a new Director. During the day, you're in meetings. At night, you open your laptop and write code for your team's project. You tell yourself it's "staying technical." Your partner notices you're working 12-hour days.
>
> **What's really happening:** You're doing two jobs because you haven't let go of one. The code you write at night creates two problems: (1) you're burning out, and (2) your team loses ownership of that code because the Director touched it and now no one wants to refactor "the Director's code."
>
> **The Director move:** Channel the coding energy into reviewing architecture, reading code to understand systems (without changing it), or contributing to internal tools that don't sit on the critical path. Better yet, use that evening time to invest in the management skills that will serve you for the rest of your career: read a leadership book, prepare for a difficult conversation, write a strategy document.

---

## Managing Your Time

Fournier introduces the **Eisenhower matrix** (important/urgent quadrant) as the core framework:

| | **Urgent** | **Not Urgent** |
|--|-----------|---------------|
| **Important** | Obvious work (outages, deadlines, competing offers) — do it | Strategic work (future planning, hiring plans, process improvement) — **make time** |
| **Unimportant** | Tempting distractions (email notifications, most chat, obvious meetings) — resist | Obvious avoid (internet browsing, irrelevant meetings) — eliminate |

Her key insight: **urgency is more clearly felt than importance.** Email feels urgent but rarely is. Chat feels urgent but isn't. Meetings feel necessary because they're on the calendar, but that's substituting "obvious" for "urgent."

The most common failure: "spending a lot of your time on things that are urgent but only slightly important, and sacrificing things that are important but not urgent."

Important-but-not-urgent examples: preparing for meetings, writing job descriptions, developing hiring plans, reviewing projects for problems, addressing cross-team conflicts, thinking about the future.

**On meetings specifically:** Be cautious about dropping meetings at this level. "Your attendance at these meetings is partially to pay attention to the dynamics and morale of your team. A happy team will feel energized and engaged. An unhappy or unmotivated team will feel drained or bored." Observing meetings gives you early warning signals.

At this level, "your boss will expect you to be mature enough to manage yourself and your teams independently." No one tells you how to organize your calendar. Proactive management of important-but-not-urgent work before it becomes urgent is expected.

> **[Leader's Playbook: Time Management for Directors]**
>
> 1. **Audit your calendar weekly.** Every Friday, review next week. For each meeting: Is this important? Do I need to be there, or can I delegate attendance? Is there an outcome I'm accountable for?
> 2. **Block strategic time.** Put recurring 2-hour blocks on your calendar labeled "strategic work" or "deep thinking." Defend them as aggressively as you'd defend a 1-1 with your VP.
> 3. **Batch similar activities.** Do all 1-1s on the same days. Batch email/Slack processing to 3 times per day. Group cross-functional meetings.
> 4. **Distinguish information-gathering meetings from decision-making meetings.** You might send a delegate to information-gathering meetings but must attend decision-making meetings yourself.
> 5. **Use async communication aggressively.** Status updates, FYI information, routine approvals — these should be async (email, doc comments, Slack) not synchronous (meetings).
> 6. **Say no to meetings without agendas.** If someone can't articulate what they need from a meeting, they haven't thought enough about whether it needs to happen.

> **[SRE Lens: Time Management for SRE Directors]**
>
> SRE Directors face unique time-management challenges:
>
> - **Incidents are interrupts you can't ignore.** Major incidents demand your attention regardless of what's on your calendar. Accept this — but ensure you have protocols so you're not needed for every P2. Build escalation thresholds that keep routine incidents at the manager level.
> - **Cross-team requests pile up.** Every product team wants "just a quick SRE consult." Batch these through a weekly intake meeting or a shared request queue.
> - **Operational reviews are important-not-urgent.** SLO reviews, on-call retrospectives, toil analysis — these are the strategic work that prevent future fires. Schedule them and protect them.
> - **Vendor management eats time.** Cloud providers, monitoring tools, incident management platforms — vendor meetings can consume hours weekly. Delegate where possible; attend only when strategic decisions are being made.

> **[Mental Model: Eisenhower Matrix + Maker/Manager Schedule (Paul Graham)]**
>
> Graham's insight: makers (engineers) need long, uninterrupted blocks to be productive. A single meeting in the middle of an afternoon destroys the whole afternoon. Managers, by contrast, operate in 1-hour increments — their calendar IS their workday.
>
> **The Director trap:** You're now fully on the manager schedule, but you still need some maker-schedule time for strategic thinking, writing, and creative work. Fournier's advice about the half-day creative block addresses this. Protect it. Your strategic thinking time is the highest-leverage activity you do — it's where you set direction for dozens of people.
>
> **[Go Deeper]** David Allen, *Getting Things Done.* Paul Graham's essay "Maker's Schedule, Manager's Schedule" (free online).

---

## Decisions and Delegation

Fournier describes the first months of managing multiple teams as a "death march" — "even when your hours are not excessive." Decision fatigue is real: "your once-focused attention gets sliced and diced between the various meetings that pepper your day."

She introduces the **plate spinning** metaphor: you're the juggler keeping plates spinning on poles, attending to each before it falls. "Honing your instincts about when to touch which plate is the name of the game."

**The good news:** instincts improve over time. You'll learn to recognize early warning signs of failing projects, impending attrition, and underperforming teams.

**Delegation matrix:**

| | **Frequent** | **Infrequent** |
|--|-------------|---------------|
| **Simple** | Delegate (standups, status summaries, minor code reviews) | Do it yourself (booking conference tickets, running quarterly scripts) |
| **Complex** | Delegate carefully (project planning, systems design, incident command) — biggest growth opportunity for your team | Delegate for training (performance reviews, hiring plans) — rising leaders learn these skills |

Key insight on delegation: **"If your teams can't operate well without you around, you'll find it hard to be promoted."** Delegation isn't just efficiency — it's your career strategy.

Fournier lists skills your team needs to learn that you should be teaching through delegation: project management, onboarding new team members, working with product to break down roadmap goals, production support.

> **[Leader's Playbook: Delegation for Directors]**
>
> 1. **Audit your task list.** Write down everything you do in a typical week. For each item, ask: Must I personally do this? If not, who could?
> 2. **Start with the simple-frequent quadrant.** Running standups, writing weekly status summaries, triaging bug reports — these are easy wins. Hand them to tech leads today.
> 3. **For complex-frequent tasks, invest in coaching.** Project planning, incident response, cross-team coordination — delegate these with support. Sit in the first few times, then step back progressively.
> 4. **Use infrequent-complex tasks as stretch assignments.** Performance review drafting, hiring plans, vendor evaluations. These are career-development gold for rising managers and senior engineers.
> 5. **Accept imperfection.** The person you delegate to will not do it exactly as you would. That's fine. 80% as good + they learned a new skill = net positive. Only intervene if the outcome would be truly damaging.
> 6. **Track what you've delegated.** Not to micromanage, but to remember to follow up and provide feedback. A delegated task with no follow-up teaches nothing.

> **[SRE Lens: What SRE Directors Should Delegate]**
>
> | Delegate | Keep |
> |----------|------|
> | Primary on-call | Escalation path for major incidents |
> | Running postmortems | Reading every postmortem and spotting patterns |
> | SLO dashboard creation | SLO target-setting decisions |
> | Vendor technical evaluations | Vendor strategic decisions (contract, pricing) |
> | Day-to-day cross-team support | Cross-team relationship management at peer manager level |
> | Toil identification and automation | Toil budget allocation decisions |
> | Sprint planning and execution | Quarterly goal-setting and resource allocation |

> **[The Shadow Side: Delegation Becomes Abdication]**
>
> Delegation is a strength. The shadow side: you delegate everything and lose touch with what's actually happening. You become the manager who's "always in meetings" and "never knows the details." Your skip-level reports describe you as "disconnected."
>
> **How it manifests:**
> - You delegate project oversight to a manager and never check on the project until it's late
> - You delegate incident response and don't read postmortems
> - You delegate hiring and don't meet candidates until the offer stage
> - You delegate performance management and are surprised when someone quits
>
> **The test:** Can you articulate the top 3 risks across each of your teams right now? If not, you've over-delegated and under-monitored. Delegation means "you own the execution; I own the accountability." It does NOT mean "I've stopped paying attention."

---

## Ask the CTO: Warning Signs

Fournier lists signals that something is wrong with a team:

1. **The chatty person who goes quiet.** Leaving early, staying silent in meetings, disengaging from chat. "This person is either having a major personal issue or getting ready to quit."

2. **The tech lead who hides progress.** Claims everything is going well but skips 1-1s and provides no detail. "This person may be hiding something" — usually slow progress or scope creep.

3. **The team with no energy in meetings.** Only the PM and TL talk; everyone else is silent. "A lack of engagement in meetings tends to mean the team isn't engaged by the work or do not feel like they have a say in the decision-making process."

4. **The team with a constantly changing project list.** Priorities shift weekly based on customer whims. "This team hasn't thought about its goals beyond pleasing customers."

5. **The fragmented small team.** Engineers don't know each other's systems and lack curiosity about them. "This team is more strongly identified by their day-to-day work... than by the larger team or the company."

> **[Red Flags: Extended for SRE Directors]**
>
> All of Fournier's warnings apply, plus SRE-specific signals:
>
> - **On-call engineer who stops escalating.** They used to ask for help; now they handle everything alone. Could be growth — or could be exhaustion and disengagement. Check which.
> - **Postmortem action items that never get completed.** If the same improvements appear in postmortem after postmortem, the team has learned helplessness about fixing systemic issues.
> - **Rising MTTR with stable incident count.** Incidents aren't increasing, but they take longer to resolve. Knowledge is draining from the team — either through attrition or burnout.
> - **Team that only does reactive work.** If a team hasn't shipped a proactive reliability improvement in 2+ quarters, they're drowning and may not be telling you.
> - **Manager who always reports "everything is fine."** This is the SRE equivalent of Fournier's hiding tech lead. An SRE team where everything is always fine either has perfect systems (unlikely) or a manager who's not looking closely enough.

> **[Interview Angle]**
>
> "How do you know when a team is struggling?" — Directors get this question often. A strong answer references leading indicators (engagement, communication patterns, meeting energy) not just lagging indicators (missed deadlines, attrition). Fournier's warning signs are excellent examples of leading indicators.

---

*Continued in [Part 2](ch06-notes-managing-multiple-teams-part2.md): Technical health signals, measuring development teams, us-vs-them dynamics, the virtues of laziness and impatience.*
