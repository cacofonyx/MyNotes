# Chapter 7: Managing Managers — Part 2

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 2 covers:** The people pleaser (Good Manager, Bad Manager), managing new managers, managing experienced managers.
See [Part 1](ch07-notes-managing-managers-part1.md) for: skip-levels, manager accountability.
See [Part 3](ch07-notes-managing-managers-part3.md) for: hiring managers, debugging orgs, estimation, roadmap uncertainty.

## Table of Contents — Part 2

- [Good Manager, Bad Manager: The People Pleaser](#good-manager-bad-manager-the-people-pleaser)
- [Managing New Managers](#managing-new-managers)
- [Managing Experienced Managers](#managing-experienced-managers)

**Block types in Part 2:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Red Flags] [Mental Model] [The Shadow Side] [Go Deeper]

---

## Good Manager, Bad Manager: The People Pleaser

Fournier contrasts Marcus (people pleaser) with Maria (effective leader):

**Marcus:** Everyone's best friend. Spends his day in 1-1s with anyone who wants time. Promises to fix every problem. "He never seems to get around to fixing those problems." The colleague you complained about still got promoted. The product team is still railroading you. Goals still don't make sense. "But Marcus is so busy, you can't blame him."

**Maria:** Less well-loved. Keeps her distance unless you report to her. Can be brusque. But since she took over: roadmap makes sense, difficult colleague got feedback and improved, meetings run better, team is focused. "She seems to go home at a reasonable hour every night!"

**Two variants of people pleasers:**

**The team pleaser (Marcus):** Spends all time in 1-1s, wants to engage emotionally, makes promises he can't keep. "Amplifies drama and negativity." Inspires huge loyalty but disappoints through undelivered promises.

**The external pleaser:** Wants to make boss and partners happy. Terrified of revealing problems. Over-commits her team. "Doesn't provide much praise or feedback internally" because she avoids all difficult conversations. "Will never willingly share problems with her manager, and readily agrees to any requests."

Signs of a people pleaser:
- Team loves her personally but is frustrated with her as manager
- More interested in smooth team than excellent team
- Wears bad feelings on her face, affecting whole team confidence
- Never pushes back on work, has many outstanding tasks with excuses
- Over-promises and under-delivers
- Says yes to everyone, sends contradictory messages
- Knows about all problems but addresses none

> **[Insight]** Fournier's key point: people pleasers "make it hard for the team to fail in a healthy way." The team pleaser shields from all discomfort, preventing growth. The external pleaser sets the team up for failure through unrealistic commitments. Both types, ironically, create LESS safety despite wanting MORE approval. The externally focused people pleaser is particularly dangerous because they're your blind spot as a senior leader — "they're so focused on only talking about good things and saying yes to everything that comes their way, their managers often don't even know about problems until it's too late."

> **[SRE Lens: The People-Pleasing SRE Manager]**
>
> In SRE, the people pleaser manifests as:
>
> **Team pleaser variant:** "We'll handle it" manager who takes on every support request, every new service onboarding, every "quick favor" without pushing back. Team is drowning but manager reports "we're managing." Nobody wants to admit the truth because the manager has made it feel like admitting overwork = letting the team down.
>
> **External pleaser variant:** Says yes to every production readiness review timeline ("sure, we can review by Friday"), every product team request ("we'll find someone to embed"), every VP priority ("absolutely, we'll make it work"). The team's roadmap is in constant flux, nothing gets finished, and the manager tells you everything is on track until it catastrophically isn't.
>
> **Detection:** Look at the gap between what the manager reports and what skip-levels reveal. If the manager says "team is doing great" but skip-levels say "we're exhausted and nothing ever gets done," you have a people pleaser.

> **[Leader's Playbook: Coaching a People Pleaser]**
>
> 1. **Make the pattern visible.** "I've noticed that in the last 3 months, you've committed to 5 new projects but completed only 2. Can we talk about what's happening?" People pleasers often don't see their own pattern.
> 2. **Help them feel safe saying no.** "When the product team asks for SRE support on a new service, what would happen if you said 'not this quarter'? What are you afraid of?" Name the fear.
> 3. **Create structural support.** An intake process, a capacity board, a prioritization framework — anything that makes the saying-no decision data-driven rather than personal. People pleasers can say "the process says no" more easily than "I say no."
> 4. **Model saying no yourself.** When you decline a request in front of your manager, narrate your reasoning: "I'm saying no to this because our team is at capacity and taking it on would put Project X at risk."
> 5. **Separate the value from the behavior.** "Your care for people is a genuine strength. The problem isn't that you want to help — it's that you commit to more than is possible, which ultimately hurts the people you're trying to help."

---

## Managing New Managers

Fournier emphasizes that first-time managers "don't know what they don't know." Even people with strong interpersonal skills need specific management training.

**Invest time upfront:** "Spending quality time with your new managers is important, and you should expect this to be an up-front cost that pays long-term dividends."

**Common new manager problems:**

**1. Not doing the basics.** Not running 1-1s, not giving feedback, not tracking takeaways. "Sometimes, you just need to remind her to hold them in the first place!"

**2. Not managing at all.** Slips on management details. Team suffers. People quit because they have no career path or inspiration. "It's ultimately your responsibility."

**3. Overwork.** "A new manager who is working all the time is probably failing to hand off her old responsibilities." Trying to do two jobs at once.

**4. Control freak.** Takes to the job with gusto because she believes it's about authority. "Domineers her team." Takes away decision-making ability. Bad relationships with peers. Hides what she's doing from you. "If your new manager is skipping your 1-1s or evading questions about what the team is working on, you may have a control freak on your hands."

**5. Not owning delivery.** Doesn't realize she's responsible for the team's output. Feels "helpless in the face of challenging goals or product roadmaps."

Fournier's critical warning: **"Making the wrong person a manager is a mistake, but keeping her in that position once you've realized she's wrong for it is a critical error."**

Seek external training: HR programs, conferences on technology leadership, programs run by engineering managers.

> **[Leader's Playbook: Onboarding a New SRE Manager]**
>
> **Month 1: Foundation**
> - [ ] Weekly 1-1s with you (not biweekly — they need more support now)
> - [ ] Review how to run 1-1s, give feedback, set expectations. Don't assume they know.
> - [ ] Help them establish their management cadence: 1-1 schedule, team meetings, skip-levels
> - [ ] Make sure they understand the on-call process, incident management responsibilities, and SLO ownership
> - [ ] Explicitly tell them: "Your job is no longer to fix incidents — it's to build a team that fixes incidents."
>
> **Month 2: Coached independence**
> - [ ] Shift to discussing specific challenges in 1-1s rather than teaching basics
> - [ ] Have them run their first performance conversation with your coaching (prep before, debrief after)
> - [ ] Begin skip-levels with their team — both to support them and to calibrate
> - [ ] Watch for overwork signals. If they're working nights, help them identify what to hand off.
>
> **Month 3: Accountability**
> - [ ] Shift 1-1s to biweekly if they're doing well
> - [ ] Expect them to proactively bring you problems and proposed solutions
> - [ ] Evaluate: Are they running 1-1s consistently? Is the team delivering? Are they delegating their old IC work?
> - [ ] Have an honest conversation: "Here's what I'm seeing. Here's what's going well. Here's what needs to improve."

> **[Red Flags: Your New Manager Is Struggling]**
>
> - They're still doing their old IC work AND managing — working 60+ hours
> - Their team members come to you with questions the manager should be answering
> - 1-1s are being canceled or skipped
> - The manager can't tell you the status of their team's projects without checking
> - The manager's skip-level reports express frustration about lack of direction or feedback
> - The manager avoids conflict — never gives critical feedback, doesn't address performance issues
> - The manager makes all decisions themselves — team members have no autonomy
> - The manager hides what they're working on from you

> **[Anti-Pattern: The Promoted-and-Abandoned Manager]**
>
> You promote a strong senior engineer to manager. You're relieved — finally, that team has a manager! You move your attention elsewhere. Six months later, 2 people have quit, the new manager is burned out, and the team is worse off than before.
>
> **What went wrong:** You treated "promoting to manager" as the end of your responsibility when it should have been the beginning. New managers need MORE of your time for the first 3-6 months, not less.
>
> **The math:** Investing 3-4 extra hours per week coaching a new manager for 3 months = ~48 hours. NOT investing that time and having the person fail = months of recovery, rehiring, team morale damage. The upfront investment always wins.

---

## Managing Experienced Managers

Different challenges from new managers:

**Culture fit is paramount.** "Management tends to be a very culture-specific task." Experienced managers create subcultures, and incompatible subcultures cause friction. Fournier warns against overvaluing domain expertise at the expense of cultural and process fit. "It's easier to gain access to industry information than it is to retrain someone who doesn't know how to work in your culture."

**They'll have different ideas about management than you.** "Working out these differences is different than letting the manager do whatever he thinks is best." Be willing to learn from them but also provide your own feedback. You're responsible for the culture of your organization.

**Inspiring experienced managers:** Less coaching on management nuts and bolts, more focus on "how they can have a larger impact on strategy and direction setting." Delegate meaningful work to them. They should be "an important advisor when it comes to setting organizational direction."

> **[Deep Dive: Hiring an Experienced SRE Manager]**
>
> SRE management culture varies wildly:
> - **Google-style SRE:** Heavy on software engineering, error budgets, strong IC culture, SREs write code
> - **Operations-evolved SRE:** More operational, on-call focused, infrastructure management, less coding
> - **Platform engineering SRE:** Focused on developer experience, self-service platforms, golden paths
>
> A manager from one SRE culture joining another faces the same friction Fournier describes. The Google-style SRE manager who joins a team that's more operationally focused may dismiss their work as "not real SRE." The ops-evolved manager joining a coding-heavy SRE team may struggle with the IC expectations.
>
> **What to evaluate:** Not "which SRE philosophy do they follow?" but "can they adapt their approach to what THIS team and THIS company needs?"

> **[Script: Setting Expectations with an Experienced Manager]**
>
> An experienced SRE manager joins your team from a larger company:
>
> *"I'm excited to have your experience on the team. I want to set us up for success by being transparent about a few things.*
>
> *First, our SRE culture here is [describe]. It may be different from what you're used to. I'm very open to ideas you bring from your experience — that's part of why we hired you. But I also need you to understand and respect the existing culture before trying to change it. Spend the first 2-3 months learning why things are the way they are before proposing changes.*
>
> *Second, here's how I think about our working relationship: I expect you to manage your team independently. I'm not going to tell you how to run 1-1s or manage your on-call rotation. Where I will be involved: setting team goals, major hiring decisions, organizational direction, and cultural alignment. I'll also provide feedback — both ways.*
>
> *Third, I want you to be a strategic partner, not just a team manager. I need your input on where our SRE organization should be heading. Come to our 1-1s with ideas about that, not just status updates.*
>
> *What questions do you have? What do you need from me to be successful?"*

---

*Continued in [Part 3](ch07-notes-managing-managers-part3.md): Hiring managers, debugging dysfunctional organizations, estimation and deadlines, roadmap uncertainty.*
