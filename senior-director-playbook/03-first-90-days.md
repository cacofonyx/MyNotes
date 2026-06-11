# Chapter 03: First 90 Days as Senior Director

> *"The president of the United States gets 100 days to prove himself; you get 90."* — Michael Watkins

This isn't a generic 90-day plan. This is sequenced specifically for: Senior Director of Platform/SRE, joining a growth-phase IGA company, from enterprise background. Every week has a purpose. The sequencing matters — actions that work in week 8 would fail in week 2.

---

## The STARS Assessment: Where Are You Landing?

Before making any moves, diagnose the situation you're walking into. Watkins' STARS framework:

| Situation | What It Means for You |
|-----------|----------------------|
| **Start-up** | Building platform/SRE from scratch. No existing team, no existing practices. Pure greenfield. |
| **Turnaround** | Platform/SRE exists but is in crisis — incidents, attrition, lost trust. You're here to fix. |
| **Accelerated Growth** | Function exists and works, but company is scaling and it needs to grow fast without breaking. |
| **Realignment** | Things look okay on the surface but there's structural rot — misalignment with business needs, technical debt bomb, cultural issues beneath a functional exterior. |
| **Sustaining Success** | Healthy org, just needs steady leadership. (Unlikely at a growth-stage company hiring a new Senior Director.) |

**Most likely for your context:** Some blend of Accelerated Growth + Realignment. The company is growing (needs scale), but the platform probably has debt and misalignment accumulated from earlier stages. You're here to both grow AND reshape.

**Why this matters:** Your moves change based on STARS:
- Accelerated growth → focus on hiring, structure, scalable processes. Don't break what works.
- Realignment → focus on building the case for change. People may not agree things need to change. You need to make the invisible visible.

---

## The 90-Day Sequence

### Week 1-2: Orient and Absorb

**Your job:** Learn the machine. Meet the people. Say very little.

**Daily rhythm:**
- 3-4 meetings per day, all 1:1s
- 30 minutes after each meeting to write notes (what did I learn? what surprised me?)
- End of day: 20 minutes synthesizing — what patterns am I seeing?

**People to meet (priority order):**

| Who | Why | What to Ask |
|-----|-----|-------------|
| Your VP/boss | Expectations, context they want you to absorb, who they think you should talk to | "What does success look like at 90 days? 6 months? What's the thing you're most worried about in this area?" |
| Your direct reports (inherited managers/leads) | Understand the current org from inside | "What's working? What's broken? What would you do if you were in my seat? What have you been asking for that hasn't happened?" |
| Peer directors (Product, Engineering, Security) | How they see your function; what they need; where friction exists | "How does platform/SRE serve you today? Where does it frustrate you? What would 'great' look like from your seat?" |
| Key ICs (senior engineers, architects) | Ground truth on technical state | "Walk me through the architecture. Where are the landmines? What keeps you up at night?" |
| Your boss's peers (other VPs) | Understand the exec dynamics | "What matters most to the business right now? How does platform/SRE factor into that?" |

**The listening protocol:**
- Take notes but don't promise anything
- Don't offer solutions or opinions yet
- Don't criticize what you see — even if it's obviously broken
- Ask "why is it this way?" not "why hasn't this been fixed?"
- Ask "what's been tried before?" — prevents you from proposing something that already failed

**Deliverable:** Private assessment document. For your eyes only. Maps:
- Org structure + who's strong/weak
- Technical landscape + where the risks are
- Political landscape + who has power, who's aligned with what
- Gaps between what the business needs and what the function currently provides

### Week 3-4: Deepen and Test

**Your job:** Go deeper in specific areas. Start testing your hypotheses.

**Activities:**
- Shadow on-call (even if you're not on rotation). See what the operational reality looks like.
- Read incident postmortems from the last 6 months. What patterns?
- Read the last 2 planning documents. What was promised vs. delivered?
- Attend 1-2 team ceremonies. Not to intervene — to observe dynamics.
- Follow a deployment end-to-end. Understand the pipeline, the pain points, the time it takes.

**Start the Five Conversations with your boss** (Watkins framework):
1. **Situation conversation:** "Here's what I'm seeing. Am I reading this right?" Get calibration before you act.
2. **Expectations conversation:** "Let me confirm what you need from me. Here's what I think the priorities are — do you agree?"
3. **Resource conversation:** "Given those priorities, here's what I have and what I'll need."
4. **Style conversation:** "Here's how I operate. Here's what I need from you."
5. **Personal development conversation:** "Where should I be growing?"

Don't do all five in one meeting. Space over week 3-4.

**Hypothesis testing:**
- Share observations (not conclusions) with 2-3 trusted people. "I'm noticing X — is that how you see it too?"
- Test one small read: make a minor suggestion. See how it lands. Did people engage? Push back? Ignore? This calibrates how much change appetite exists.

### Week 5-6: Synthesize and Align

**Your job:** Form your initial assessment. Align with your boss on priorities.

**The 30-Day Assessment** (present to your boss, verbally first):
- "Here's what I see as the current state" (3-4 bullet synthesis)
- "Here's what I think the top 3 priorities should be" (with reasoning)
- "Here's what I'd like to focus on for the next 60 days"
- "Here's what I need from you to make that happen"

**Critical:** Get agreement BEFORE acting. Your boss validating your assessment means when you act, you're acting with air cover. If your boss pushes back on your read, you've just learned something crucial — recalibrate before proceeding.

**Start sharing perspectives externally:**
- In peer meetings, start offering observations (still framed as questions): "I've been looking at X — my sense is Y. How does that match what you're seeing?"
- This signals: "I'm forming views, I'm informed, I'm ready to contribute" without the arrogance of "I've figured this place out in 5 weeks."

### Week 7-8: First Moves

**Your job:** Take your first visible actions. Carefully chosen, high-signal, achievable.

**What makes a good "early win" at Director level:**

| Good Early Wins | Bad Early Wins |
|----------------|----------------|
| Fix something everyone agrees is broken (a process, a meeting, a bottleneck) | Launch a big new initiative before you have buy-in |
| Remove an obstacle your teams have been asking about for months | Reorganize anything |
| Create clarity where ambiguity exists (write down something everyone "knows" but no one has documented) | Make a personnel change |
| Deliver one visible improvement to a peer's team (cross-functional goodwill) | Try to change the tech stack |
| Ship one thing that demonstrates your team's value in a new way | Take on a high-risk project with uncertain scope |

**Principles for early wins:**
- They should be achievable within 2-3 weeks (not dependent on months of work)
- They should be visible to people outside your org (builds reputation)
- They should align with the priorities you've aligned with your boss
- They should not require anyone else to change significantly
- They should demonstrate YOUR value — your judgment, your leadership, your taste for what matters

**IGA/Platform-specific early wins that usually work:**
- Publish an internal "Platform State of the Union" — where are we, what are our SLOs, how are we doing
- Fix the most common developer complaint about the platform (there's always one that's cheap to fix)
- Establish a regular reliability review cadence (if none exists)
- Create a visible dashboard showing platform health that execs can glance at
- Unblock one cross-team dependency that's been stuck for weeks

### Week 9-10: Build Momentum

**Your job:** Convert early wins into a forward agenda. Start building alliances for bigger moves.

**Activities:**
- 1:1 with each peer director specifically about "here's where I want to take Platform/SRE — how does that affect you? What do you need from me?"
- Begin socializing your 6-month vision (informally, not as a doc yet)
- Identify your first "coalition of the willing" — 2-3 people (peers or skip-levels) who are natural allies for your agenda
- Start making the structural changes you've been holding back on: team boundaries, process changes, priority shifts

**If things are going well:** People come to you proactively. Peers mention your early wins in other forums. Your boss expresses confidence.

**If things are NOT going well:** You're still mostly unknown. Peers haven't sought you out. Your team is unsure of your direction. Your boss is asking "what are you working on?" → Accelerate relationship building, be more visible, communicate more frequently.

### Week 11-12: The 90-Day Plan Delivery

**Your job:** Present your strategic direction. Make it real.

**The 90-Day Output** (formal, shared with boss + peers):
- "Assessment: where we are today" (1 page)
- "Vision: where we need to be in 12 months" (1 page)
- "Strategy: how we get there" (priorities, sequencing, trade-offs — 2 pages max)
- "What I need" (resources, alignment, decisions from others)
- "How we'll measure progress" (3-5 metrics/milestones for next quarter)

**Present it in this order:**
1. Boss first (get buy-in, adjust if needed)
2. Peers second (share direction, get input)
3. Your team third (give clarity and direction)

**After 90 days, you should have:**
- Clear, validated view of the current state
- Agreed priorities with your boss
- 1-2 visible early wins that established credibility
- Relationships with all key peers
- A communicated direction for your org
- First hires or re-orgs in motion (if needed)

---

## The Conversations Calendar

| Week | Key Conversations | Purpose |
|------|-------------------|---------|
| 1 | Boss (first 1:1), direct reports (all) | Expectations, current state from inside |
| 2 | Peer directors, key ICs, architects | External view, technical ground truth |
| 3 | Boss (situation/expectations), customers (product teams) | Calibrate your read, understand demand side |
| 4 | Boss's peers (other VPs), returning to directs with follow-up | Political landscape, deeper team assessment |
| 5-6 | Boss (30-day assessment), trusted advisor | Alignment, validation before action |
| 7-8 | Peers (early win visibility), team (direction signals) | Build reputation, give clarity |
| 9-10 | Peer directors (alliance building), boss (resource) | Set up bigger moves, secure investment |
| 11-12 | Boss (90-day plan), peers (strategic direction), team (vision) | Formalize direction, create accountability |

---

## Pitfalls Specific to This Transition

### "The Enterprise Savior" Anti-Pattern

**What it looks like:** You see the gaps clearly (because you've seen mature enterprises) and immediately start prescribing enterprise solutions: "We need a proper change management process," "We should have a CAB," "Let me introduce ITIL-based incident management."

**Why it fails:** The company hired you for your enterprise expertise — but not to transplant enterprise wholesale. They want the PRINCIPLES translated to their context, not the PROCESSES copied from somewhere else.

**Instead:** Frame improvements in their language, at their scale. "I've seen this pattern before. Here's a lightweight version that works at our size..." Always start lighter than you think is appropriate. You can add rigor later; removing premature rigor is politically expensive.

### "Fixing the Team Before Understanding the System" Anti-Pattern

**What it looks like:** By week 3, you've identified people you think are underperforming. You start managing them out or restructuring around them.

**Why it fails:** You don't yet understand what "good" looks like HERE. Someone who seems underperforming might be under-supported, mis-scoped, or carrying context no one else has. And you'll be judged harshly for early personnel moves — "they haven't even been here a month and they're already firing people."

**Instead:** Nobody moves for 90 days unless there's a clear, urgent performance or conduct issue. After 90 days, you have enough context to distinguish "wrong person" from "wrong setup" from "wrong expectations."

### "I Need to Show I'm Technical" Anti-Pattern

**What it looks like:** You dig into code, architecture, operational details to prove you belong. You offer technical opinions in design reviews. You signal "I'm not just a manager, I'm an engineer."

**Why it fails:** At Director level, proving you're technical is table stakes — it was proven when you got hired. Spending your limited early capital on demonstrating technical depth wastes time you should spend on strategic credibility and relationship building.

**Instead:** Let your technical depth show through the QUALITY of your questions, not through direct technical contributions. "Have we considered the failure mode where..." demonstrates depth more powerfully than reviewing code.

---

## The Hidden Curriculum: What No One Tells You

### Your First Skip-Level (Boss's Boss)

You'll probably meet the CTO or SVP Engineering in your first week or two. What they're looking for:
- Confidence without arrogance
- Self-awareness about what you don't know yet
- A clear "how I operate" signal
- Evidence that you'll make their life easier, not harder

What to prepare: one sentence on your approach, one question that shows you're thinking at their level, zero complaints about what you've inherited.

### The "Listening Tour" Is Also a Performance

You think you're passively absorbing. But everyone you meet in weeks 1-4 is evaluating YOU. Every 1:1 is a two-way interview.

What they're assessing:
- Is this person smart? (Quality of their questions)
- Are they humble enough to learn? (Or are they already prescribing?)
- Will they be easy or hard to work with?
- Do they seem like they "get" our context?
- Would I want to work for/with this person?

Be genuinely curious. But also be aware: the listening tour IS your first impression campaign.

### Your First Incident (It Will Come)

Sometime in the first 90 days, something will go wrong in production. This is your moment. Not to solve it — to SHOW how you lead during pressure.

What to do:
- Be present but not commanding (unless it's critical and no one else is stepping up)
- Ask "what do you need from me?" not "let me drive this"
- After resolution: lead the postmortem discussion. Show blameless culture in action.
- Communicate upward crisply: what happened, impact, what we're doing about it, whether this is systemic

This one incident, handled well, builds more credibility than weeks of strategic planning.

---

## Week-by-Week Checklist

| Week | Done? | Activity |
|------|-------|----------|
| 1 | ☐ | Boss 1:1 (expectations, immediate priorities, who to meet) |
| 1 | ☐ | All direct reports 1:1 (understand their world) |
| 1 | ☐ | IT/access/tooling fully set up (don't waste week 1 on logistics) |
| 2 | ☐ | Peer directors 1:1 (how they see your function) |
| 2 | ☐ | Key architects/senior ICs (technical ground truth) |
| 2 | ☐ | Read: last 3 incident postmortems, last planning doc, team retros |
| 3 | ☐ | Shadow on-call shift or review on-call runbook |
| 3 | ☐ | Follow a deployment end-to-end |
| 3 | ☐ | Boss conversation: situation + expectations |
| 4 | ☐ | Meet boss's peers (other VPs) |
| 4 | ☐ | Map: org chart (real, not formal), decision-making patterns |
| 4 | ☐ | Identify 2-3 candidate early wins |
| 5 | ☐ | Present 30-day assessment to boss (verbal) |
| 5 | ☐ | Start sharing observations with peers |
| 6 | ☐ | Secure boss alignment on top 3 priorities |
| 6 | ☐ | Begin executing first early win |
| 7 | ☐ | First visible output/improvement delivered |
| 8 | ☐ | Second early win in motion |
| 8 | ☐ | Boss conversation: resources, style |
| 9 | ☐ | Peer conversations: future direction (informal) |
| 9 | ☐ | Identify first alliance partner |
| 10 | ☐ | Draft 6-month vision |
| 10 | ☐ | Begin any org structure changes (if needed) |
| 11 | ☐ | 90-day plan reviewed with boss |
| 12 | ☐ | 90-day plan shared with peers and team |
| 12 | ☐ | Retrospective: what worked, what to adjust in next quarter |

---

## Measuring Your Own Progress

### Green Signals (On Track)

- Boss says "you're ramping well" unprompted
- Peers seek your opinion on things outside your org
- Your team says "it's clear where we're going"
- You've made one visible improvement others noticed
- You feel uncomfortable but not lost

### Yellow Signals (Course Correct)

- Boss is asking "what are you working on?" by week 6
- Peers haven't engaged with you beyond initial intros
- Your team is doing fine but doesn't see your value-add yet
- You're still mostly consuming information at week 8
- You feel comfortable (meaning you haven't pushed yourself to the new altitude)

### Red Signals (Urgent Action Needed)

- Boss expresses concern about pace or direction
- A peer goes around you to your boss
- Your team is confused about priorities or your role
- You've made a visible mistake (wrong call, bad meeting, overstepped)
- You feel paralyzed or are avoiding key conversations

---

## Chapter Summary

The first 90 days are sequenced: absorb → test → align → act → formalize. The sequence protects you from acting before understanding and from understanding without acting. Your deliverables are: a validated assessment, boss alignment, early wins that demonstrate value, peer relationships, and a communicated direction. Everything else — the big strategy, the reorg, the cultural change — comes AFTER you've earned the right to lead it.

**The meta-principle:** You're not just solving problems in the first 90 days. You're establishing HOW you lead. People are forming permanent impressions of your judgment, your tempo, your values. The early wins matter less for their content and more for what they signal about how you operate.
