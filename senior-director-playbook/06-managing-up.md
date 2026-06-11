# Chapter 06: Managing Up — The VP/C-Suite Relationship

> *"No other single relationship matters more than the one with your boss."* — Michael Watkins

Your relationship with your VP (or whoever you report to) is the single highest-leverage relationship in your role. They control: your budget, your headcount, your air cover, how your work is interpreted to the exec team, and ultimately whether you succeed or fail. A great boss relationship multiplies your effectiveness 3-5x. A broken one makes everything impossible.

This isn't about pleasing your boss. It's about managing the relationship deliberately — the way you'd manage any critical system.

---

## What Your VP Actually Needs From You

### The Job They Hired You For (Unstated Version)

What the job description said: "Lead Platform/SRE, define strategy, build teams, drive reliability..."

What they actually need:

| What They Need | What It Means in Practice |
|---------------|--------------------------|
| **One less thing to worry about** | They don't want to think about platform. They want to trust that you've got it. Silence = health. |
| **Clear signal when something IS wrong** | When things go sideways, they hear it from you FIRST — before peers, before their boss. |
| **Executive-ready narratives** | When THEIR boss asks "how's the platform?" — they need a crisp answer. You provide the talking points. |
| **Political alignment** | You don't create problems with other teams that escalate to their level. You resolve your own friction. |
| **Strategic thinking they can trust** | They want to say "I trust [your name]'s judgment on this" in exec meetings without checking. |
| **Growth trajectory** | They want you to grow INTO the role fast enough that they don't need to manage you closely. |

### The Meta-Need: Make Them Look Good

Not in a sycophantic way. In a real way:
- When your org performs well → they made a good hire (you) and a good investment (your team)
- When your strategy proves right → they backed the right direction
- When you solve cross-functional problems → their org is a good partner
- When you communicate well upward → they have a reliable signal source

**The inverse is also true:** When you fail, they fail. When you create political friction, it escalates to them. When you're unclear, they look uninformed. This is why the relationship matters so much — your outcomes are coupled.

---

## The Communication Contract

### What to Communicate, How Often

| Category | Cadence | Format | Example |
|----------|---------|--------|---------|
| Strategic direction | Monthly | Brief doc or deck section | "Here's where we're heading and why" |
| Progress on committed goals | Bi-weekly or weekly | Bullet points in 1:1 | "On track / at risk / blocked" |
| Risks and issues | As they arise (IMMEDIATELY) | Verbal first, written follow-up | "X happened. Impact is Y. I'm doing Z." |
| Decisions you've made | Weekly (in 1:1) | FYI, not ask | "Decided to do X because Y. Letting you know." |
| Decisions you need from them | As needed (batched) | Framed as recommendation | "I recommend X. The alternative is Y. Here's the trade-off." |
| Wins and good news | As they happen | Quick Slack/email | "Shipped X — 3x improvement in deploy time" |
| Bad news | IMMEDIATELY | Direct, verbal preferred | Never in a group meeting. Never as a surprise. |

### The Cardinal Rule: No Surprises

Your boss should NEVER learn about a problem from someone else. Not from their boss. Not from a peer. Not from an incident channel. The first person to tell them about an issue in your domain should be YOU.

Why this matters more than anything:
- Surprises feel like loss of control
- Learning about YOUR problem from someone else makes them question your awareness
- It puts them in the impossible position of reacting without context
- It damages trust faster than any other single thing you can do

**The discipline:** The moment you become aware of something that might reach your boss through another channel — even if you don't have full information yet — send a heads-up: "You might hear about X. Here's what I know so far. I'm investigating and will update you by [time]."

### The Update Format: Bottom Line Up Front (BLUF)

Your boss doesn't have time for context→analysis→conclusion. They need:

**Structure every communication as:**
1. Bottom line (what do they need to know?)
2. So what? (why does it matter?)
3. What's needed from them? (or: nothing needed, FYI only)
4. Context (only if they ask for it)

**Bad:** "So we've been investigating the deployment pipeline, and there are several issues we've identified. The CI stage takes too long because of dependency caching problems, and the CD stage has flaky integration tests. We think we need to refactor the test suite and add caching layers..."

**Good:** "Deploys take 4 hours. Root cause identified — two fixes needed, both in-flight. We'll cut this to 30 minutes by end of Q1. No decision needed from you — just informing."

---

## The Five Conversations (Ongoing, Not Just First 90 Days)

Watkins' framework isn't one-and-done. These conversations recur:

### 1. Situation Conversation (Quarterly)

"Here's how I see the current state of our org and its context."

**Purpose:** Ensure you and your boss have the same read on reality. Misalignment here cascades into everything else.

**Watch for:** Your boss may have information you don't (budget pressures, exec conversations, company direction changes). This conversation surfaces that.

### 2. Expectations Conversation (Quarterly)

"Here's what I understand you expect of me and my org. Is that right?"

**Purpose:** Explicit alignment on what success looks like. Prevents the scenario where you deliver X beautifully but they expected Y.

**Watch for:** Expectations SHIFT — especially at growth-stage companies. What your boss needed in Q1 may not be what they need in Q3. Re-calibrate regularly.

### 3. Resource Conversation (As Needed)

"Given the expectations, here's what I need to deliver. Here's the trade-off if I don't get it."

**Purpose:** Your boss controls resources. You need to make the case clearly — and accept the answer when it's no.

**The key move:** Never present resource needs in isolation. Always present as: "If I get X, I can deliver Y. If I don't get X, I can deliver Z instead. Which do you prefer?" This gives them a choice, not a demand.

### 4. Style Conversation (Once, then adapt)

"Here's how I operate. Here's what I need from you. Here's what works best for communication between us."

**Purpose:** Prevent style mismatches from creating friction. A boss who wants daily check-ins with a direct who provides weekly summaries → both frustrated.

**Things to align on:**
- How much detail do they want? (Some bosses want "just tell me it's handled." Others want to see the work.)
- How do they want bad news? (Verbal? Slack? Document?)
- How much autonomy do they want to give? (Some want to be consulted on big decisions; others want you to decide and inform.)
- What's their response time expectation? (If they Slack you at 9 PM, do they expect same-night response?)

### 5. Personal Development Conversation (Semi-Annually)

"Where should I be growing? What would make me more effective in this role?"

**Purpose:** Shows humility and growth orientation. Also gives you early signal if they're concerned about anything.

**Watch for:** If they can't name anything — that's either "you're doing great" or "I haven't thought about you much." Ask follow-up: "If you had to pick one area where I could have more impact, what would it be?"

---

## Reading Your Boss: Types and How to Adapt

### The "Tell Me the Answer" Boss

**Characteristics:** Wants recommendations, not problems. Gets frustrated by open-ended exploration. Values decisiveness.

**How to adapt:**
- Always come with a recommendation, never just a question
- "I recommend X because Y. The risk is Z. I'm prepared to proceed unless you see something I don't."
- Save the analysis for backup — lead with the answer

### The "Think Together" Boss

**Characteristics:** Wants to be part of the thinking process. Enjoys exploring options. May feel excluded if you present a fait accompli.

**How to adapt:**
- Bring the thinking to them at 70% baked, not 100%
- "I'm leaning toward X, here's why. But I want your perspective before I commit."
- Give them room to shape the answer — but don't come with nothing

### The "Don't Bother Me Unless It's Important" Boss

**Characteristics:** Gives maximum autonomy. Rarely checks in. Expects you to surface only what they need to know.

**How to adapt:**
- Be disciplined about what you escalate — they'll lose confidence if you bring trivial things
- Over-communicate in writing (so there's a record) even if they don't respond
- But: if they're TOO hands-off, you're flying blind on expectations. Force the calibration conversations.

### The "Data-Driven" Boss

**Characteristics:** Wants metrics, evidence, quantified trade-offs. Distrusts intuition-based arguments.

**How to adapt:**
- Always have numbers: "Deployment frequency improved 40% this quarter"
- Frame trade-offs quantitatively: "Option A costs $X and delivers Y. Option B costs..."
- If you don't have data, say so explicitly: "I don't have numbers on this yet. My judgment based on [experience] is..."

### The "Relationship-First" Boss

**Characteristics:** Decisions influenced by how they feel about the people involved. Loyalty matters. Trust is personal.

**How to adapt:**
- Invest in the personal relationship, not just the professional one
- Show up for things that matter to them (their priorities, their presentations, their initiatives)
- Never let a disagreement feel personal — always frame as "different read on the situation, same goal"

---

## When Things Go Wrong

### Your Boss Is Wrong About Something

This will happen. Your boss will make a call or hold a position you disagree with.

**The framework:**
1. Is this a reversible decision? → If yes, disagree and commit. Revisit with data later.
2. Is this heading toward a cliff? → If yes, push back clearly, once. "I want to flag that I see [risk]. I understand the decision and will execute, but wanted my concern on record."
3. Are they wrong about YOUR domain? → This is where you need to push hardest. You were hired for your expertise. If they're overriding your technical judgment, that's worth a serious conversation.

**What NOT to do:**
- Passive-aggressive compliance ("fine, we'll do it your way" then half-assing execution)
- End-running to their boss
- Relitigating after the decision is made (unless new information emerges)
- Silent disagreement (they think you're aligned; you're not; it explodes later)

### Your Boss Isn't Advocating for You

**Signals:** Your org doesn't get funded. Your initiatives die at the exec level. Your wins aren't mentioned in company updates. Other directors get what they ask for; you don't.

**Possible reasons:**
- They don't understand your value yet (communication gap — fix it)
- They're not politically strong themselves (their advocacy doesn't carry weight — find alternative sponsors)
- They don't agree with your direction (alignment gap — have the direct conversation)
- They're managing you out (start looking — but verify before panicking)

**The move:** Direct conversation. "I've noticed [X concrete pattern]. Help me understand — is there something I should be doing differently? Or is there a constraint I'm not seeing?"

### You Messed Up

You will. A bad call. A missed signal. A public mistake.

**The only play:**
1. Go to your boss immediately. Don't hide, minimize, or explain away.
2. Own it: "I made a mistake. Here's what happened. Here's the impact. Here's what I'm doing to fix it. Here's what I'll do differently."
3. Execute the fix visibly and well.
4. Don't over-apologize or collapse. One clear acknowledgment, then back to competence.

Most bosses can forgive a mistake. Very few can forgive being blindsided or lied to about one.

---

## The 1:1 as Operating System

Your 1:1 with your boss is the primary channel for the entire relationship. Treat it with the same seriousness as production infrastructure.

### Structure

| Time | Content |
|------|---------|
| First 5 min | Their agenda (always yield first) |
| Next 10 min | Your updates (BLUF format: status, risks, wins) |
| Next 10 min | Decisions/input needed (come with recommendations) |
| Last 5 min | Strategic alignment (anything shifting in context you should know about?) |

### Preparation (Non-Negotiable)

Before every 1:1, spend 10 minutes:
- What do they need to hear from me?
- What do I need from them?
- Is there anything that could surprise them that I should pre-empt?
- What decision am I asking them to make? (Come prepared for that discussion)

### Skip the 1:1 at Your Peril

Even when things are going well. Even when you're busy. Even when there's "nothing to discuss." The 1:1 isn't just for information exchange — it's for relationship maintenance. A boss you haven't talked to in 2 weeks starts filling in the blanks themselves — and their imagination is usually worse than reality.

---

## Managing Up in IGA/Platform Specifically

### The Translation Problem

Your boss likely came from Product, Engineering Management, or General Management. They may not deeply understand platform/SRE work. You are their translator.

**What they hear vs. what you mean:**

| What You Say | What They Hear | What to Say Instead |
|-------------|---------------|---------------------|
| "We need to reduce technical debt" | "Expensive work with no visible outcome" | "Our shipping speed is constrained by [X]. Fixing it unlocks [Y product capability]." |
| "We need better observability" | "We want new tools" | "We can't detect issues before customers do. This investment cuts MTTR by [X]%." |
| "SLO compliance is at 97%" | "I don't know if that's good or bad" | "We promised customers 99.9%. We're below that. Here's the impact and the plan." |
| "Connector stability is a problem" | "Something is always a problem in infra" | "3 of our top 10 accounts flagged connector reliability in their last QBR. Risk to renewal: $XM." |

### What Makes YOU Easy to Manage

Your boss has 5-8 direct reports. They have their own boss breathing down on them. They're in back-to-back meetings. The director who is easiest to manage gets the most goodwill.

**Easy to manage means:**
- No surprises
- Crisp communication (short, clear, action-oriented)
- You solve your own problems (they hear about solutions, not just problems)
- You're aligned with company priorities (not off on your own mission)
- You're low-drama (you don't create interpersonal friction that escalates)
- You make THEIR boss think they're doing a great job (because your org delivers)

---

## Chapter Summary

Your boss relationship is infrastructure — invest in it continuously, not just when something breaks. The core contract: no surprises, BLUF communication, always with a recommendation, explicit alignment on expectations. Read their style and adapt your communication to match. When things go wrong, speed and ownership beat explanation. The 1:1 is your operating system — prepare for it, protect it, never skip it.

**The principle:** Your boss doesn't need to understand the details of what you do. They need to trust your judgment, feel informed at the right altitude, and know that your org makes THEM successful. Build that trust and you'll have the air cover, resources, and autonomy to do your actual job.
