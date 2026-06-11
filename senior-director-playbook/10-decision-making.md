# Chapter 10: Decision Making at Director Level

> *"If making decisions were easy, there would be much less need for managers."* — Andy Grove

The decisions that reach you are the ones nobody else could resolve. They're ambiguous, politically loaded, cross-boundary, and consequential. If the answer were obvious, someone below you would have already decided. Your value as a Director comes from making good calls consistently under these exact conditions.

---

## How Director-Level Decisions Are Different

### What Gets Decided at Each Level

| Level | Decision Type | Information Quality | Reversibility |
|-------|-------------|--------------------|----|
| IC | Technical implementation | High (they see the code) | Usually high |
| EM | Team priorities, people, process | Good (close to the work) | Moderate |
| Director | Strategy, org design, cross-team trade-offs, resource allocation | Incomplete, contradictory, politically filtered | Often low |
| VP+ | Company direction, major investments, personnel at director+ | Sparse, high-level, delayed signals | Very low |

**What this means for you:** The decisions you make will ALWAYS feel under-informed. You'll never have enough data. You'll never be certain. That's the job. If you wait for certainty, you've already decided (to do nothing).

### The Decisions Only You Can Make

| Decision Type | Why It Escalates to You |
|--------------|------------------------|
| Cross-team trade-offs | "Should we prioritize Team A's work or Team B's?" — your managers can't resolve this; they each advocate for their team |
| Resource allocation | "Given limited headcount, where does the next hire go?" — you see the full portfolio |
| Strategic direction | "Do we invest in X or Y?" — only you hold the strategic context |
| Organizational change | "Should we reorg? Split this team? Merge these functions?" — structural authority |
| Escalated conflicts | "Two managers disagree and can't align" — you arbitrate |
| External commitments | "Can we commit to delivering X for this enterprise customer?" — you own the commitment |
| People decisions on your managers | Hire, fire, promote, reassign at the manager level — only you |

---

## Decision Frameworks

### Framework 1: One-Way Door vs. Two-Way Door (Bezos)

**Two-way door:** Reversible. If wrong, you can undo it cheaply. Walk through, see what's on the other side, walk back if needed.

**One-way door:** Irreversible or very expensive to reverse. Once through, you're committed.

| Two-Way Doors (Decide Fast) | One-Way Doors (Decide Carefully) |
|-----------------------------|----------------------------------|
| Tool selection (can switch later) | Architectural patterns (expensive to change) |
| Process experiments (try it, revert if bad) | Major rewrites (6+ months committed) |
| Team structure tweaks (can reorganize) | Firing a manager (can't un-fire) |
| Priority shifts within a quarter | External commitments to customers |
| Trying a new vendor | Multi-year contracts |
| Communication style changes | Public positions that affect credibility |

**The discipline:** Most decisions are two-way doors that get treated as one-way doors. This causes slow, over-deliberated decision-making. The Director's job is to identify which type each decision is and calibrate speed accordingly.

### Framework 2: The DACI Model

For important decisions that involve multiple stakeholders:

| Role | Who | What They Do |
|------|-----|-------------|
| **D**river | The person responsible for the decision process | Frames the problem, gathers input, drives to conclusion |
| **A**pprover | The person with authority to approve (often you) | Makes the final call if consensus fails |
| **C**ontributor | People with relevant expertise or stake | Provide input, data, perspectives |
| **I**nformed | People who need to know the outcome | Told after decision, not consulted |

**When to use DACI:** Cross-team decisions, architectural choices, process changes, anything where it's unclear who decides.

**The Director's power move:** Assign YOURSELF as the Driver or Approver on the decisions that matter. Delegate Driver on everything else. Being clear about "who decides" prevents the death-by-committee that plagues growth companies.

### Framework 3: The Decision Journal

Keep a private record of significant decisions:

```
Date: [when]
Decision: [what you decided]
Context: [what information you had]
Alternatives considered: [what else you could have done]
Why this choice: [your reasoning]
Expected outcome: [what you predict will happen]
Review date: [when to check if it worked]
```

**Why this matters:** Human memory is terrible at learning from decisions because we retroactively rationalize outcomes. A decision journal lets you review: "Was my reasoning sound? Did I miss something? Am I systematically wrong in a particular way?"

Review monthly. Look for patterns.

### Framework 4: The Regret Minimization Frame

When stuck between options: "Which decision would I regret MORE if it turned out wrong?"

| Decision | If I do X and it fails | If I don't do X and miss out |
|----------|----------------------|------------------------------|
| Rewrite the connector framework | 6 months of effort, team frustrated, could have spent it on features | Technical debt compounds, connector reliability keeps degrading, we lose enterprise customers |
| Hire that expensive senior person | $400K/year and they might not work out | Team stays under-leveled, I remain a bottleneck, scaling takes another year |
| Push back on my VP's direction | Political risk, might damage relationship | I implement something I believe will fail, team loses confidence in me |

Often the regret of inaction exceeds the regret of action — especially for platform leaders, where the status quo quietly deteriorates.

---

## Making Decisions with Incomplete Information

### The 70% Rule

If you have 70% of the information you'd ideally want, decide. Waiting for 90% means you're too slow. Deciding at 40% means you're reckless. 70% is the sweet spot.

**What 70% feels like:** "I have a clear hypothesis. I've heard from the key people. I can see the major trade-offs. There are some unknowns, but I've identified what they are and assessed whether they're likely to change the answer."

### The "Disagree and Commit" Threshold

When to override consensus:
- You've heard all perspectives
- You still believe differently
- The dissent is genuine (not just unfamiliarity with your reasoning)
- The cost of being wrong is manageable
- The cost of NOT deciding is higher than the cost of being wrong

When to follow consensus despite disagreement:
- The people closest to the problem disagree with you
- You lack domain-specific knowledge they have
- The decision is easily reversible
- Your conviction is more about instinct than evidence

**The script:** "I've heard everyone's view. I see it differently because [reason]. I'm going to make the call to do X. I understand the risks. If new information emerges, we'll revisit. But for now, let's commit and execute."

### The Pre-Mortem

Before committing to a major decision, ask: "Imagine it's 6 months from now and this decision failed. What went wrong?"

Have your team spend 10 minutes independently writing failure scenarios. This surfaces risks that optimism bias hides:
- "We didn't account for Team X's dependency on the old system"
- "The migration took 2x longer because of data complexity we didn't model"
- "We hired for skill A but actually needed skill B"

Not every risk needs mitigation. But knowing what you're exposed to lets you decide consciously, not blindly.

---

## Decision Speed vs. Decision Quality

### The Director's Tempo

At growth-stage company, the cost of slowness usually exceeds the cost of imperfection:

| Decision Urgency | Response Time | Acceptable Quality |
|-----------------|---------------|-------------------|
| Incident/crisis | Minutes to hours | Good enough to stop bleeding, iterate later |
| This-quarter tactical | Days | 80% optimal is fine |
| Next-quarter planning | 1-2 weeks | 85-90% (worth getting right) |
| Org design/strategy | 2-4 weeks | 90%+ (consequential and hard to reverse) |
| Multi-year architecture | 4-8 weeks | 90%+ (deeply analyze, but STILL decide) |

### Accelerating Good Decisions

**Pre-decide categories:** For recurring decision types, create standing policies:
- "Any request under $10K doesn't need my approval"
- "My managers can hire ICs without my interview, up to [level]"
- "On-call rotation changes don't escalate unless someone objects"
- "Any reversible experiment can proceed without approval — just inform me"

This eliminates 60% of the decisions that currently flow to you. You only see the exceptions.

**Decision meetings:** When a decision requires discussion, structure it:
1. Decision owner presents: situation + options + recommendation (5 min)
2. Questions for clarification only (5 min)
3. Perspectives/concerns (10 min)
4. Decision (you or the designated approver): "We're going with X. Here's why." (2 min)
5. Next steps and DRI assigned (3 min)

Total: 25 minutes. If you can't decide in 25 minutes, the problem isn't well-enough framed. Send people back to frame it better.

---

## Specific Decision Patterns at Your Level

### Build vs. Buy

| Factor | Lean Build | Lean Buy |
|--------|-----------|----------|
| Core differentiator? | If yes → build | If no → buy |
| How unique is your need? | Highly unique → build | Standard → buy |
| How fast do you need it? | Can wait → build | Need now → buy |
| Do you have the skills? | Yes → build | No → buy (then learn) |
| Total cost of ownership? | Lower to build + maintain | Lower to pay vendor |
| Strategic control? | Critical → build | Nice-to-have → buy |

**For IGA platform:** Build the connector framework (differentiator). Buy monitoring/alerting (commodity). Build tenant isolation (unique needs). Buy CI/CD base (standard, customize on top).

### Invest vs. Defer

When someone asks for platform investment, assess:

1. **What's the cost of deferring?** (Does the problem get worse? How fast?)
2. **What's the opportunity cost of investing?** (What DON'T you do instead?)
3. **Is there a cheaper 80% solution?** (Often yes — and that's fine for now)
4. **Who feels this pain?** (If it's only your team: defer. If it's customer-facing: invest.)

### People Decisions

The hardest decisions. Harder than technical ones because they affect humans and aren't reversible.

**Performance management on a manager:**
- Have you been clear about expectations? (If not, that's your failure, not theirs)
- Have they had fair ramp time? (Especially if new — 6 months minimum)
- Is the gap coachable? (Skill gap: yes. Judgment gap: harder. Values gap: no.)
- What's the impact on their team if you make a change? (Short-term disruption vs. long-term benefit)

**The 6-month rule:** Unless there's a clear conduct or values issue, give a manager 6 months before deciding they're not working. Performance manage explicitly during that time. If at 6 months you still lack confidence in them — make the change. Don't let it drag to month 12 hoping it'll improve.

---

## Decision Pathologies to Watch For

### Analysis Paralysis

**Signal:** Lots of discussion, lots of options evaluated, lots of "let's get more data" — no decision.

**Root cause:** Fear of being wrong. Over-indexing on decision quality vs. decision speed.

**Fix:** Set a deadline: "We will decide by [date], with whatever information we have." The constraint forces action.

### The HiPPO Problem (Highest Paid Person's Opinion)

**Signal:** Meetings where everyone waits for the most senior person to speak, then agrees.

**Root cause:** Hierarchy suppresses dissent. People don't want to contradict the Director.

**Fix:** Speak LAST. Ask others their views first. Create safety for disagreement: "I want to hear the strongest argument AGAINST what I'm leaning toward."

### Decision Fatigue

**Signal:** You're making 30+ decisions daily. By afternoon, you're rubber-stamping or avoiding decisions.

**Root cause:** Insufficient delegation. Decisions that should be made by managers are escalating to you.

**Fix:** Audit which decisions actually need you. Probably <30% of what you're currently deciding. Push the rest down with explicit authority: "You don't need to check with me on this. I trust your judgment."

### Revisiting Settled Decisions

**Signal:** A decision is made, then re-opened 3 weeks later because someone new raises concerns.

**Root cause:** Either poor communication of the decision, or insufficient stakeholder inclusion upfront.

**Fix:** When a decision is made, communicate it with rationale AND state explicitly: "This is decided. We'll revisit only if [these specific conditions] change." Hold the line.

---

## Building Decision Culture in Your Org

Your org inherits your decision-making style. If you model good decisions, your managers will too.

### What to Model

- **Speed:** Make decisions promptly. Don't let things sit.
- **Transparency:** Explain your reasoning. "Here's why I chose X over Y."
- **Accountability:** Own outcomes. "That decision didn't work. Here's what I'll do differently."
- **Delegation:** "This is your call. I trust you."
- **Reversibility comfort:** "Let's try it. If it doesn't work, we'll adjust."

### What to Coach

When your managers struggle with decisions:
- "What are you optimizing for?"
- "What's the worst case if you're wrong?"
- "What would you do if you had to decide right now?"
- "What additional information would actually change your answer?" (Often: none)
- "Who haven't you talked to?"

---

## Chapter Summary

Director-level decisions are ambiguous, consequential, and always made with incomplete information. The frameworks (one-way/two-way door, DACI, regret minimization, pre-mortem) provide structure — but the core skill is SPEED. At growth-stage, slow decisions cost more than imperfect decisions. Build a decision culture through: delegation (push down what you can), standing policies (pre-decide categories), structured meetings (25-minute maximum), and transparent reasoning.

**The Director's decision meta-principle:** Your job is not to make perfect decisions. It's to make good-enough decisions fast enough that the organization can act, learn, and adjust. The only truly bad decision is no decision.
