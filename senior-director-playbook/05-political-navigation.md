# Chapter 05: Political Navigation and Alliance Building

> *"To succeed in your new role, you will need the support of people over whom you have no direct authority."* — Michael Watkins

This chapter exists because organizations don't run on logic. They run on relationships, incentives, fear, ambition, and history. If you take things at face value — assuming that good ideas win on merit, that stated goals are real goals, that people mean what they say — you will be outmaneuvered by those who read between the lines.

This isn't about becoming manipulative. It's about pattern recognition. The same way you learned to read system logs and identify failure patterns, you can learn to read organizational signals and identify political patterns. It's a learnable skill, not an innate trait.

---

## Why Platform/SRE Leaders Are Structurally Disadvantaged Politically

Before learning the game, understand why YOU specifically need to play it:

| Structural Disadvantage | Why It Exists | What It Means |
|------------------------|---------------|---------------|
| Invisible value | You succeed when nothing breaks. Success = no event. | You must actively narrate your value; it won't be self-evident. |
| Perceived cost center | Platform doesn't ship features customers buy. | Every budget cycle, someone asks "why is this team so big?" |
| Prevention vs. cure | You prevent outages; firefighters get praised for fixing them. | Prevent 50 incidents → no one notices. Fix 1 dramatic incident → hero. |
| Everyone has opinions | Every engineer thinks they know how infra should work. | Your expertise is constantly second-guessed in ways Product never experiences. |
| Long payback cycles | Platform investments pay off in 6-18 months. | Impatient executives cut funding before value materializes. |
| "No" function | Part of your job is saying "this isn't safe/ready/reliable." | You accumulate friction with teams who feel blocked by you. |

**The implication:** A platform leader who doesn't play politics will lose — not because they're wrong, but because they'll be underfunded, overruled, and eventually marginalized. The ideas will be good. The support won't be there.

---

## Signal → Interpretation: Reading Organizational Dynamics

### The Fundamental Principle

**What people say is not always what they mean. What they mean is not always what they want. What they want is not always what they'll admit.**

This isn't cynicism. It's how humans operate in hierarchies. People manage risk, protect territory, maintain relationships, and preserve optionality — often unconsciously.

### Signal-Interpretation Table

| Signal (What You See/Hear) | Naive Interpretation | Actual Interpretation |
|---------------------------|---------------------|----------------------|
| "That's interesting, let me think about it" | They'll consider it | They're not going to do it but don't want to say no to your face |
| "We should align on this offline" | They want to discuss further | They disagree but won't challenge you publicly; expect pushback in private |
| "I'm supportive in principle" | They support you | They support the idea but won't spend political capital to help it happen |
| "Let's take this to [committee/meeting]" | They want broader input | They want to slow it down or dilute your ownership |
| Peer doesn't respond to your doc/proposal | They're busy | They disagree or don't see it as important but don't want a direct conflict |
| Boss says "handle it however you think best" | Full autonomy | Might mean autonomy OR might mean "I don't want to be accountable for this decision" |
| Someone suggests adding your project to another team's scope | They're trying to help | They're trying to take ownership (or dump accountability) |
| "We tried that before and it didn't work" | Historical data point | Territory defense — they don't want YOU to succeed where they failed |
| Meeting keeps getting rescheduled | Calendaring difficulty | Decision avoidance or deprioritization |
| You're not invited to a meeting about your domain | Oversight | Deliberate exclusion — someone is making decisions without your input |
| "We need to be pragmatic about this" | Reasonable trade-off discussion | Your proposal is being characterized as impractical/academic to justify ignoring it |
| Peer publicly praises your team's work | They value you | Could be genuine OR could be building credit before asking for something big |

### How to Calibrate

You won't get these right 100% of the time. The meta-skill is: **notice the signals, generate multiple interpretations, then observe what happens next to narrow down which interpretation was correct.**

Build your calibration over time:
- When someone says "let me think about it" — did they follow up? If not, that's a data point.
- When someone says they're supportive — did they actually support you when it cost them something? If not, that's a data point.
- When someone wasn't in a meeting — did a decision happen without your input? That's a pattern, not an accident.

---

## Mapping the Political Landscape

### Step 1: Identify the Power Map

Formal org charts show reporting lines. They don't show power. Map the REAL power structure:

**Questions to identify real power:**
- Whose opinion does the CEO/CTO actually change their mind for?
- Who gets funded even when budgets are tight?
- Who can kill a project with one comment in a meeting?
- Who do people informally check with before making big decisions?
- Whose Slack messages get instant responses from execs?

**At your level, the key players are:**
- Your boss (VP): Your primary sponsor. Their support is necessary but not sufficient.
- Peer directors: Potential allies or blockers. Their cooperation determines whether your initiatives succeed.
- The product leader: Controls priority for the thing that matters most to execs (features → revenue).
- The "shadow decision-makers": Senior ICs or historical figures who have disproportionate influence due to tenure or expertise.
- Your boss's boss: The one who decides whether your function grows or gets cut.

### Step 2: Classify Stakeholders

For each key player, assess:

| Person | Position on Your Agenda | Influence Level | What They Want | What They Fear |
|--------|------------------------|-----------------|----------------|----------------|
| [Name] | Supporter / Neutral / Opponent | High / Medium / Low | [Their primary motivation] | [What threatens them] |

**Why "what they fear" matters:** People are more motivated by loss aversion than gain. If you can frame your agenda as PROTECTING something they care about (rather than only as adding something new), you'll get stronger support.

### Step 3: Identify Winning and Blocking Alliances

**Winning alliance:** The minimum set of people whose support guarantees your initiative moves forward.
- Usually: your boss + the most influential peer director + one exec champion

**Blocking alliance:** Anyone who can single-handedly prevent your initiative.
- Usually: the product leader (if they say "not a priority"), the CTO (if they disagree technically), or any VP who sees your work as threatening their scope

**Your job:** Secure the winning alliance BEFORE going public. Neutralize the blocking alliance in advance (through inclusion, compromise, or pre-commitment from their boss).

---

## Influence Strategies

### Strategy 1: Consultation (Most Powerful for Platform Leaders)

**What it is:** Going to stakeholders BEFORE you have a final proposal. Asking their input, incorporating it, then presenting a solution that already has their fingerprints on it.

**Why it works:** People support what they helped create. If the Product Director's input shaped your platform roadmap, they'll defend it in exec meetings because it's partly THEIRS.

**How to do it:**
- "I'm thinking about how to approach [X]. You know the product side better than anyone — what would you need from a solution?"
- Incorporate their answer. When you present the final plan: "As [Name] and I discussed, we're aligning on..."
- They can't attack a plan they co-created without attacking themselves.

**The trap:** Don't consult so broadly that you lose ownership. Consult 2-3 key people. Not the whole company.

### Strategy 2: Alliance Before Announcement

**What it is:** Never present a major initiative to a large group without having pre-aligned key supporters.

**Why it works:** Large meetings are for ratification, not persuasion. If you present something controversial to 20 people without pre-work, you'll face public objections that harden into positions. But if 3 of those 20 are already aligned and speak up in support, momentum carries.

**How to do it:**
- Identify the 2-3 most influential voices in the room
- Have 1:1 conversations BEFORE the meeting: "I'm going to propose X. Here's why. I'd value your support."
- In the meeting, they don't need to be prompted — they'll naturally weigh in
- The undecided middle follows the first few voices

### Strategy 3: Trade and Reciprocity

**What it is:** Building a bank of goodwill that you can draw on when you need support.

**Why it works:** Humans are wired for reciprocity. If you've helped someone — genuinely, without strings — they'll feel obligated (often unconsciously) to help you.

**How to build your bank:**
- Loan an engineer to help a peer's team with a deadline
- Share credit generously ("Product team did amazing work on X, we just provided the platform")
- Solve a small problem for someone proactively (before they ask)
- Give someone a heads-up about something that affects them before it becomes public

**How to withdraw:**
- "I need your support on [X] in the next leadership meeting. Here's what it involves..."
- Don't be explicit about the trade ("I helped you so..."). Just make the ask. The reciprocity operates unconsciously.

### Strategy 4: Framing and Narrative

**What it is:** How you present something determines how people evaluate it. Same initiative, different frame = different reaction.

**Platform-specific reframes:**

| What You Want | Losing Frame | Winning Frame |
|--------------|-------------|---------------|
| Headcount for SRE | "We need more people to handle the operational load" | "We're at risk of a major customer-facing incident. This investment prevents $XM in churn." |
| Tech debt paydown | "We need time to clean up the code" | "Our deployment speed is 10x slower than our competitors. This unblocks 4 product initiatives." |
| New tooling investment | "Our current tools are inadequate" | "This reduces developer cycle time by 3x — equivalent to hiring 10 engineers for the cost of 2." |
| Process change | "We need more governance" | "We had 3 incidents last quarter that were preventable. This specific change addresses the root cause." |

**The principle:** Always frame in terms of what the AUDIENCE cares about (revenue, speed, risk), not what YOU care about (technical quality, operational health).

### Strategy 5: Graduated Commitment

**What it is:** Instead of asking for full buy-in on a big initiative, get incremental yeses that build momentum.

**Why it works:** A small yes creates psychological consistency. After saying yes to step 1, saying no to step 2 feels inconsistent. The commitment escalates naturally.

**How it works for platform:**
1. "Can we agree that deployment velocity is a problem?" (Easy yes — everyone feels it)
2. "Can we agree the root cause is [X]?" (Still relatively easy)
3. "Can we agree that fixing [X] requires [Y investment]?" (Now they've committed to the logic)
4. "Here's the plan for [Y investment]. You've already agreed on the diagnosis and the approach — shall we execute?"

---

## Political Patterns at Growth-Stage Companies

### Pattern: "The Founder's Ear"

**What it is:** At growth-stage companies, often one person (founder, early engineer, original architect) has outsized influence through historical trust. They may not be in the formal hierarchy but their opinion carries more weight than anyone at your level.

**How to handle:** Identify this person. Build a direct relationship with them early. Get their buy-in on your direction BEFORE presenting it formally. If they're skeptical, their skepticism will quietly kill your agenda without you ever knowing why.

### Pattern: "Product Supremacy"

**What it is:** In growth companies, Product/Sales is usually the dominant function. Revenue = survival. Everything else is "support."

**How to handle:** Don't fight this hierarchy. Work within it. Position platform work as "what enables Product to ship faster/better/more reliably." Speak product language. Make the product leaders' lives easier, and they'll advocate for your resources.

**The specific move:** Find the ONE product initiative that's currently blocked or slowed by platform limitations. Fix it visibly. Now you have a product leader saying "platform team unblocked us" — which is worth more than any strategy deck.

### Pattern: "The Territory War"

**What it is:** As companies grow, scope boundaries between teams become contested. "Who owns CI/CD?" "Is security tooling platform's job or security team's job?" "Does SRE own incident response or does each team own theirs?"

**How to handle:** Don't assume these get resolved by logic or org charts. They get resolved by whoever moves first AND builds alliances to defend the position.

**When you WANT the territory:** Move decisively, deliver value quickly, then defend through demonstrated excellence. "We built this, it works, people use it, here's the data."

**When someone takes YOUR territory:** Don't fight publicly. Go to your boss: "I want to make sure we're aligned on scope. Here's what I understand our charter to be. Is that still right?" Let your boss fight the battle at their level.

### Pattern: "The Executive Attention Cycle"

**What it is:** Executive attention moves in cycles. There's a flavor of the quarter: "We're focused on enterprise deals." Then: "We need to fix retention." Then: "AI is the priority." The strategic landscape shifts every 3-6 months.

**How to handle:** Frame your work in terms of whatever the current executive attention cycle is focused on. Your platform work is the SAME — but how you describe it changes.

- When the focus is growth: "Platform enables us to onboard 3x more customers"
- When the focus is retention: "Platform reliability is what keeps customers renewing"
- When the focus is efficiency: "Platform automation saves $XM in engineering costs"
- When the focus is AI: "Platform provides the infrastructure for AI-powered governance features"

Same work. Different story. Tuned to the audience's current concerns.

---

## Building Your Political Intelligence Over Time

### Weekly Political Awareness Practice

Spend 15 minutes each Friday:
1. What decisions were made this week that affect my org?
2. Who made them? Who influenced them?
3. Were there any signals I might be misreading?
4. Is anyone's behavior toward me/my team changing? Why?
5. Where is executive attention focused right now?

### Relationship Maintenance

Key relationships don't maintain themselves. Budget time for:
- Monthly informal conversation with each peer director (not about work — build the relationship)
- Bi-weekly touch point with your boss (even if no agenda — just maintaining the channel)
- Quarterly check with your boss's boss (stay visible one level up)
- Occasional outreach to people you don't need anything from right now (bank building)

### Debrief Conversations

After any important meeting or decision:
- What happened?
- What was the stated reason for the outcome?
- What might the UNSTATED reasons be?
- Who got what they wanted? Who didn't? What will the losers do next?
- Did I miss any signals?

Talk this through with a trusted peer or mentor. They'll see things you missed.

---

## Anti-Patterns

### "I Don't Do Politics"

**What it means in practice:** "I will be politically naive and then surprised when my good ideas don't get traction."

**Reality:** Not doing politics means other people do politics TO you. They set your budget, define your scope, take your headcount, and characterize your team's value — because you opted out of that conversation.

**Instead:** Reframe politics as "building relationships that enable your team to succeed." That's it. That's all it is. It's not dirty. It's how organizations work.

### "But I Was Right"

**What it means:** You presented a technically correct proposal. It got rejected. You're frustrated because the logic was airtight.

**Reality:** Being right is necessary but not sufficient. The Alexia case (First 90 Days) — she was RIGHT about the marketing strategy. She lost because she presented a rational solution to a political problem.

**Instead:** Right + supported > right + alone. Always. Budget time for building support, not just building the case.

### "I'll Let My Work Speak for Itself"

**What it means:** You deliver excellent results and assume that will be noticed, rewarded, and lead to expanded influence.

**Reality:** Invisible work stays invisible. Platform/SRE is structurally invisible. Your work will NOT speak for itself. You must speak for it.

**Instead:** Develop a regular cadence of making your work visible. Monthly updates to leadership. Quarterly showcases. Celebratory announcements when big milestones hit. This isn't bragging — it's informing.

---

## Chapter Summary

Politics is pattern recognition, not manipulation. Platform/SRE leaders must play the political game because their work is structurally invisible and disadvantaged. The core skills: reading signals beyond face value, mapping the power structure, building alliances before announcements, framing in terms of what your audience cares about, and maintaining relationships as an ongoing practice (not just when you need something).

**The principle that binds it all:** People support what they helped create, what aligns with their interests, and what comes from people they trust. Your job is to create all three conditions before asking for anything significant.
