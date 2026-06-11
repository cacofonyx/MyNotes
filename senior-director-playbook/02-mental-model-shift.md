# Chapter 02: Mental Model Shift — Manager to Director

> *"My job wasn't to be the smartest person in the room. It wasn't to be 'right.' Rather, my role was to help the team make the best possible decisions and help them implement them in a sustainable and efficient way."* — James Turnbull

The jump from Senior Engineering Manager to Senior Director is not a promotion in the usual sense. It's a job change. The skills that made you an excellent EM — deep technical context, close team relationships, hands-on problem-solving, shipping cadence — become liabilities if you don't deliberately shed them.

This chapter maps the mental model shift: what you stop doing, what you start doing, and the uncomfortable middle ground where you're doing neither well.

---

## The Fundamental Shift: Output Definition Changes

### As Senior EM

Your output = your team's output. You're measured by:
- Did the team ship what they committed to?
- Is the technical quality high?
- Are the people growing?
- Is the team healthy and retaining?

You can directly influence all of these. You're in the standups. You see the code. You know who's stuck. Your leverage is direct.

### As Senior Director

Your output = your organization's impact on the business. You're measured by:
- Is the platform/SRE function making the company more successful?
- Are we positioned correctly for where the company will be in 12-18 months?
- Do other leaders trust and rely on your organization?
- Are the right bets being made with the right resources?

You cannot directly influence most of these. You influence them through:
- The managers you hire and develop
- The strategy you set and communicate
- The organizational design you choose
- The relationships you build with peers
- The narrative you construct about your function's value

**The disorienting truth:** Your "work product" is no longer tangible. You don't ship features. You don't review PRs. You don't fix incidents. Your work product is decisions, alignment, and organizational capability. It's invisible until it works — and only visible when it fails.

---

## Andy Grove's Managerial Leverage — Reframed for Directors

Grove's core insight: a manager's output = output of their organization + output of neighboring organizations under their influence.

At Director level, this equation shifts dramatically:

| Leverage Type | EM Level | Director Level |
|--------------|----------|----------------|
| **High-leverage activities** | Code reviews that catch architecture issues; 1:1s that unblock people; hiring great engineers | Strategy decisions that set direction for 50+ people; organizational redesigns; cross-functional alignments that unblock multiple teams simultaneously |
| **Low-leverage activities** | Email, status meetings, routine admin | Anything your managers should be doing; attending meetings for visibility only; making decisions that should be delegated |
| **Negative-leverage activities** | Micromanaging, blocking decisions | Undercutting your managers by making their decisions; being a bottleneck on approvals; context-switching so frequently that you never think deeply |

### The Director's High-Leverage Activities

1. **Setting direction** — One clear strategic decision can align 6 months of work for multiple teams. This is the highest-leverage thing you do.

2. **Organizational design** — Choosing team boundaries, reporting lines, and interaction patterns. Conway's Law means your org structure IS your architecture decision.

3. **Hiring/developing your direct reports** — A great manager multiplied by their team size compounds your impact. A weak manager divided by their team size drags everything.

4. **Cross-functional alignment** — When you align with the Product Director on platform priorities, you've eliminated months of friction for every team in both orgs.

5. **Narrative construction** — How the rest of the company understands what your function does and why it matters. This determines budget, headcount, and political support.

---

## What You Must Stop Doing

### Stop: Being the Technical Decision-Maker

**The old habit:** You had opinions on architecture, tooling, approach. Your team looked to you for technical direction. You reviewed designs and often improved them.

**Why it must stop:** If your managers can't make technical decisions, you've either hired wrong or you're not developing them. Every technical decision you make at Director level robs a manager of growth AND makes you a bottleneck.

**The exception:** When two of your managers disagree on a cross-team technical decision and cannot resolve it. Then you arbitrate — not on technical merits (they know more than you by now) but on organizational impact, strategic fit, and resource trade-offs.

**The discipline:** When someone brings you a technical question, your default response is: "What does [your manager] think?" or "Have you discussed with [relevant technical lead]?" Only engage if it's escalated AND crosses team boundaries AND has strategic implications.

### Stop: Attending Team-Level Meetings

**The old habit:** You're in sprint ceremonies, design reviews, incident debriefs. You like the detail. It keeps you "connected."

**Why it must stop:** Every hour in a team meeting is an hour not spent on director-level work. And your presence in team meetings changes their dynamic — people perform, defer, or filter. Your absence is actually a gift to your managers' authority.

**The exception:** Occasional attendance to calibrate (once a month, unannounced pattern). Critical incidents where you need to personally understand impact for executive communication. New team members where your presence signals investment.

**The discipline:** If you're in a meeting and the primary purpose is execution-level coordination, you're in the wrong meeting. Your meetings should be: strategy, alignment, decision-escalation, cross-functional, or 1:1s with your directs.

### Stop: Being the Smartest Person in the Room

**The old habit:** You've built a career on being technically sharp, having the right answer, seeing the issue others miss.

**Why it must stop:** At Director level, being "the smart one" creates dependency. People stop thinking because they know you'll think for them. Your job is now to make YOUR PEOPLE the smartest people in their rooms.

**The discipline:** In meetings, count to 10 before speaking. Ask questions instead of stating opinions. When you DO have a strong view, frame it as "have we considered..." rather than "we should..."

### Stop: Knowing Everything That's Happening

**The old habit:** You knew the status of every workstream. You could answer any question about your team's work. Being informed felt responsible.

**Why it must stop:** With 3-5 teams (30-60 people), you CANNOT know everything. Trying to creates either bottleneck (everything flows through you) or theater (you attend meetings where you don't contribute, just to "stay informed").

**The discipline:** You need to know: (1) Are we on strategy? (2) Are there risks to committed outcomes? (3) Is anyone stuck on something that needs my help? Everything else is your managers' job to know.

---

## What You Must Start Doing

### Start: Thinking in Systems, Not Tasks

**The new habit:** Instead of "what work needs to be done," think "what organizational capability needs to exist."

Example shift:
- EM thinking: "We need to improve our deployment pipeline. Let me plan the work, assign it, track progress."
- Director thinking: "We need deployment velocity as an organizational capability. Which team owns this? Do they have the right skills? Is this the right priority given our strategy? How does this interact with what Product needs next quarter? What does 'good enough' look like vs. 'gold-plated'?"

### Start: Operating on Multiple Time Horizons Simultaneously

**The new habit:** You're always holding three frames:
1. **This quarter** — Are committed outcomes being delivered? (Mostly your managers' job, you just watch for risk)
2. **Next quarter** — Is the plan right? Are we staffed for it? Are dependencies identified? (You actively shape this)
3. **Next year** — Where should we be positioned? What capabilities do we need to build? What bets should we make? (This is YOUR unique job)

If you only operate in horizon 1, you're a well-paid EM. If you only operate in horizon 3, you're a strategist disconnected from reality. The skill is holding all three simultaneously.

### Start: Making Decisions with Incomplete Information

**The new habit:** At EM level, you could usually get enough data to make a confident call. At Director level, you often can't — and waiting for complete information IS a decision (the decision to stay still while things move around you).

The Director decision framework:
- Is this decision reversible? → Decide fast, adjust later.
- Is this decision irreversible? → Get the minimum viable information, then decide. "Minimum viable" is NOT "complete."
- What's the cost of delay vs. the cost of being wrong? Usually delay costs more.

### Start: Actively Managing Your Narrative

**The new habit:** What your organization does is only half the story. The other half is: does the rest of the company understand what you do, why it matters, and what it would cost to lose?

Platform/SRE work is structurally invisible — you succeed when nothing breaks, which looks like nothing happening. You must actively construct a narrative:
- Here's what we enabled this quarter (in business terms, not technical terms)
- Here's what risk we retired (in customer/revenue terms)
- Here's what we're investing in next (framed as business capability, not technical project)

If you don't tell this story, someone else will — and their version will be "that team that costs a lot and says no to things."

---

## The Identity Crisis (It's Normal)

### What It Feels Like

The first 3-6 months of operating as a Director when your identity is still "engineer/EM" feels like:

- **Guilt** — You're not "producing" anything. Your calendar is meetings and thinking. That feels lazy.
- **Loss** — You miss the craft. Technical problem-solving was satisfying. Strategic ambiguity is not.
- **Imposter syndrome** — Everyone around you seems to know how to "be a Director." You're faking it.
- **Boredom/anxiety oscillation** — Bored because you're not in the action; anxious because you don't know if your people are handling it.
- **Control withdrawal** — You used to know if things were going well because you COULD SEE THEM. Now you only know through reports, which might be filtered.

### What to Do About It

**Accept the uncomfortable middle.** There's a period where you've stopped doing EM work but aren't yet competent at Director work. You'll feel useless. This is the growth zone, not a failure state.

**Find new sources of satisfaction.** The Director equivalent of "I shipped a feature" is:
- "My manager handled that crisis without needing me"
- "The cross-functional alignment I built meant zero friction on that initiative"
- "The strategy I set 6 months ago is playing out — the team is in the right position"
- "I hired someone who's already making their team better"

**Build a peer group.** Other directors (inside or outside the company) who understand the altitude. You need people you can be honest with about "I don't know what I'm doing" without it affecting your organizational credibility.

---

## Practical Rebalancing: How Your Time Should Shift

### EM Time Allocation (What You're Used To)

| Category | % | Activities |
|----------|---|-----------|
| Team delivery | 35% | Standups, design reviews, unblocking, code review |
| People management | 25% | 1:1s, career growth, coaching, feedback |
| Technical work | 20% | Architecture, hands-on problem-solving, investigations |
| Cross-team coordination | 15% | Dependency management, peer alignment |
| Strategy/planning | 5% | When asked to contribute to planning cycles |

### Director Time Allocation (Where You Need to Get To)

| Category | % | Activities |
|----------|---|-----------|
| Strategy & planning | 25% | Technical vision, roadmap, org design, positioning |
| Cross-functional leadership | 25% | Peer relationships, alignment, executive communication |
| People (your directs) | 20% | 1:1s with managers, coaching them on THEIR challenges, hiring |
| Decision-making & escalations | 15% | The calls only you can make |
| Learning & thinking | 10% | Reading, external perspectives, deep thought on complex problems |
| Team-level involvement | 5% | Selective, intentional appearances |

**The test:** If you can't articulate what you spent last week on, and it's mostly in the bottom three rows of the Director table — you're doing the wrong job.

---

## The Director's New Relationships

### Your Directs Change

You no longer manage ICs. You manage managers. This means:

| With ICs (before) | With Managers (now) |
|-------------------|---------------------|
| You help them solve problems | You help them develop judgment |
| You have the context to help directly | You help them build their own context |
| You can see their work | You see their work indirectly through outcomes |
| Feedback is about their execution | Feedback is about their leadership |
| You can compensate for their gaps | You must develop them past their gaps or make a change |

### Your Peers Change

Your peer set is now other directors — Product, Engineering, Security, Data. These relationships are no longer "coordination" — they're strategic alliances. The quality of these relationships determines whether your initiatives succeed or fail (Chapter 05).

### Your Boss Changes

Your boss is likely a VP or C-level. This relationship is fundamentally different from the EM→Director relationship you had before:
- Less frequent, higher stakes per interaction
- They want synthesis, not detail
- They want "here's the situation, here's my recommendation" not "here's the problem, what should I do?"
- They're evaluating your judgment, not your execution (Chapter 06)

---

## Applying This at a Growth-Phase IGA Company

### What Makes This Shift Harder Here

At Saviynt specifically, the Director role likely involves:
- **Building while running** — You're not inheriting a well-oiled machine. You're building the platform org while delivering on current commitments.
- **Ambiguous scope** — Platform/SRE at a growth-stage company means the boundaries of your responsibility are negotiated, not defined.
- **Speed expectations** — Enterprise timelines for "getting up to speed" don't apply. They need Director-level contribution faster than you'd get at a Fortune 500.
- **Technical debt context** — The existing platform likely has significant debt from earlier stages. Your strategic framing has to account for "where we are" not just "where we should be."

### What Makes It Easier Here

- **Greenfield org design** — You get to shape the org structure, not inherit a frozen one. This is a gift.
- **Clear technical domain** — SRE/Platform for IGA has concrete, measurable outcomes (uptime, deployment velocity, developer productivity). Easier to narrate than some Director roles.
- **Growth = resources** — Growing companies add headcount. You'll likely get to build, not just optimize.
- **Lower organizational inertia** — Fewer layers, fewer vetoes, faster decision cycles. Your Director-level decisions actually happen, instead of dying in committee.

---

## Chapter Summary

The Manager→Director shift is a job change, not a promotion. Your output definition changes from "team delivery" to "organizational impact." You must stop doing the high-competence work that got you here (technical decisions, team-level involvement, knowing everything) and start doing the uncomfortable new work (systems thinking, narrative construction, incomplete-information decisions, multi-horizon planning). The identity crisis is normal and lasts 3-6 months. Your time allocation should flip from 60% execution/20% people/15% coordination/5% strategy to roughly the inverse.

**The hardest truth:** No one will tell you to stop doing EM work. It feels productive. Your team might even appreciate it. But every hour you spend operating as a very-experienced EM is an hour you're NOT operating as the Director they hired. The company doesn't need another EM. It needs what only a Director can provide: strategy, organizational design, cross-functional alignment, and forward-looking judgment.
