# Chapter 07: Growth Phase Company Dynamics

> *"In a startup, every new person is a meaningful percentage of the company. At a growth-stage company, you're hiring faster than you can integrate."* — Will Larson

A growth-phase company ($100M-$500M ARR, 500-3000 employees, scaling rapidly toward IPO or post-IPO efficiency) operates differently from both startups and enterprises. It has the ambition of a startup, the customer expectations of an enterprise, and the organizational maturity of neither. Understanding these dynamics is essential because they shape EVERYTHING — what's possible, what's expected, and what will break.

---

## What "Growth Phase" Actually Means

### The Structural Reality

| Dimension | What It Looks Like | Implication for You |
|-----------|-------------------|---------------------|
| Headcount growth | 30-50% annually. New people everywhere. Constant onboarding. | Half your peers are also new. Institutional memory is thin. |
| Revenue pressure | Board expects 40%+ growth. Every quarter matters. | Everything gets measured against "does this help us sell more?" |
| Process debt | Grew too fast for process to keep up. Things that worked at 200 people break at 800. | You'll find surprising gaps. This is normal, not dysfunction. |
| Cultural drift | Original culture diluted by waves of new hires from different backgrounds. | "How we do things here" is contested, not settled. |
| Technical debt | Built fast to hit market windows. Now paying the interest. | Systems that "work" but are fragile, undocumented, held together by tribal knowledge. |
| Org structure churn | Reorgs every 6-12 months. Roles and scopes shift. | Don't over-invest in current structure — it will change. |
| Executive turnover | Growing companies often outgrow their early leaders. New VPs/C-suite arriving regularly. | Your boss might change. Peer directors might change. Plan for relationship volatility. |
| IPO/exit pressure | Investors want returns. Efficiency metrics start mattering alongside growth. | "Do more with less" coexists with "grow at all costs." Contradictory demands are normal. |

### The Growth Company Lifecycle (Where Saviynt Likely Sits)

```
Stage 1: Product-Market Fit ($0-$20M)
  → "Just make it work"
  → Hero culture, founders do everything

Stage 2: Go-to-Market Scaling ($20M-$100M)
  → "Sell as fast as possible"
  → Sales-led, product follows market demand
  → Platform = whatever doesn't break

Stage 3: Operational Scaling ($100M-$300M)  ← LIKELY HERE
  → "Now we need this to be sustainable"
  → Enterprise customers demand reliability
  → Platform/SRE becomes critical, not optional
  → The company hires people like YOU

Stage 4: Efficiency & IPO Readiness ($300M-$500M+)
  → "Prove we can be profitable"
  → Margins matter, automation matters
  → Platform ROI must be demonstrable
  → Every dollar spent is scrutinized
```

**Why this matters:** At Stage 3, the company is simultaneously:
- Still growing fast (urgency remains)
- Now serving enterprise customers (expectations are high)
- Discovering that what worked at Stage 2 is breaking (technical debt surfaces)
- Hiring leaders from enterprise backgrounds to "professionalize" (you)
- Not yet operating with enterprise-level patience for results

This is the fundamental tension you operate within: **startup urgency + enterprise expectations + inadequate foundation.**

---

## The Physics of Growth Companies

### Law 1: Everything Is Breaking at Scale

What worked for 50 customers doesn't work for 500. What worked for 100 engineers doesn't work for 400. What worked for 5 services doesn't work for 50.

**Manifestations you'll see:**
- Deployments that used to take minutes now take hours
- Incidents that used to affect one customer now affect hundreds
- On-call that used to be manageable is now burning people out
- Architecture decisions made for speed now cause cascading failures
- Tribal knowledge that lived in 3 people's heads is now lost as those people leave or get promoted

**Your response:** This is WHY you were hired. Don't be shocked by it. Don't judge the people who built it. They were solving different problems at a different scale. Your job is to build what comes NEXT — without condescending about what came before.

### Law 2: Everyone Is New

In a company growing 30-50% annually, within 2 years the majority of people have been there less than 18 months. This creates:

- **Thin institutional memory** — No one remembers why decisions were made
- **Constant re-negotiation** — "How we do X" changes with each wave of hires
- **Relationship instability** — Your carefully built alliances dissolve as people move/leave
- **Cultural fragmentation** — Different teams develop different norms based on who happened to join

**Your response:** Accept that relationships need constant maintenance. Document decisions and reasoning (so they survive the turnover). Build systems that work regardless of who's operating them (resilience to people-churn, not just system-churn).

### Law 3: Priorities Shift Faster Than You're Used To

In enterprise: annual planning, quarterly review, priorities change maybe twice a year.
In growth companies: priorities can shift quarterly or even monthly based on:
- A big deal won/lost
- A competitor announcement
- Board feedback
- A major incident
- A new executive's arrival

**Your response:** Build strategy with quarterly waypoints that deliver standalone value. Don't invest everything in an 18-month bet that depends on stable priorities. Make each quarter's work valuable even if the plan changes next quarter.

### Law 4: "Good Enough" Beats "Perfect"

The cost of delay in a growth company is measured in: deals lost to competitors, market position eroded, burn rate accumulating without corresponding revenue. This creates genuine pressure for speed over quality.

**The implication:** Your enterprise instinct for thoroughness, risk mitigation, and "doing it right the first time" is in TENSION with this environment. Both instincts are valid. The skill is calibration:

| Situation | Lean Enterprise (Thorough) | Lean Growth (Speed) |
|-----------|---------------------------|---------------------|
| Customer-facing reliability | ✓ | |
| Security/compliance | ✓ | |
| Internal tooling | | ✓ |
| Architecture decisions (hard to reverse) | ✓ | |
| Process design | | ✓ (iterate, don't perfect) |
| Hiring | ✓ (bad hire costs more than slow hire) | |
| Feature experiments | | ✓ |
| Data migrations | ✓ | |

### Law 5: The Company You Joined Will Not Be the Company in 12 Months

Growth companies are shape-shifters. The org chart, the priorities, the leadership, the culture, the customers — all change continuously. You cannot optimize for a static state.

**Your response:** Build for adaptability, not just for today's requirements. Modular teams that can be reorganized. Platforms that support multiple use cases. Relationships across many people (not dependence on one champion). Strategy that works under multiple scenarios.

---

## How Growth Dynamics Affect Platform/SRE Specifically

### The Scaling Curve Problem

```
Demand on Platform (grows with company):  ████████████████████████████████████
Platform Team Capacity (always lags):     ██████████████████████
Gap (where pain lives):                              ██████████████████
```

This gap is PERMANENT in growth companies. You will never have enough capacity to satisfy all demand. The strategic question is not "how do I close the gap?" (you can't) but "where do I invest the limited capacity I have for maximum impact?"

### The "Shadow Platform" Risk

When your team can't meet demand, teams build their own:
- Team A sets up their own deployment pipeline
- Team B builds their own monitoring
- Team C writes their own CI configuration
- Now you have 5 different versions of "platform" — none maintained, all fragile

**This is YOUR failure mode at Director level.** Not because those teams are wrong — they're solving real problems — but because it fragments the platform, creates maintenance burden, and eventually causes reliability incidents.

**Prevention:** You can't prevent all shadow platforms. Instead:
- Identify the top 3 requests from product teams. If you can't serve them, acknowledge that and offer a "blessed path" that's lightweight.
- Make the official platform so easy that building your own is more work.
- Distinguish between "this MUST use the platform" (security, deployments) and "this CAN use whatever" (internal dashboards, dev tools).

### The Talent Market Compression

Growth companies compete for the same SRE/platform talent as FAANG and other high-growth companies. You'll face:
- Difficulty hiring senior people (they have many options)
- Retention risk (your best people get recruited constantly)
- Compensation pressure (growth company equity ≠ FAANG total comp, usually)
- The "10x engineer" bottleneck (one person holding together critical systems)

**Your response:** Build systems that don't depend on heroes. Document everything. Cross-train aggressively. Accept that you'll hire more junior and develop them — which means investing in mentorship and ramp time even when things are urgent.

---

## The Executive Dynamics at Growth Phase

### What the Board Cares About

At this stage, the board is watching:
- **ARR growth rate** (are we still growing fast enough?)
- **Net Dollar Retention** (are existing customers expanding?)
- **Gross margins** (can we be profitable at scale?)
- **Enterprise deal wins** (are we moving upmarket?)
- **Rule of 40** (growth rate + profit margin > 40%)

**How this filters down to you:**
- "Platform reduces cost-per-customer" → margins
- "Platform enables faster feature delivery" → growth rate
- "Platform ensures reliability for enterprise" → enterprise deals and NDR
- "Platform reduces engineering headcount needed" → efficiency / margins

### The CFO's Growing Influence

As companies approach IPO, the CFO gains power. They start asking:
- "Why is infrastructure cost growing faster than revenue?"
- "What's the ROI on the platform team?"
- "Can we reduce headcount in SRE through automation?"

**Your response:** Have answers BEFORE you're asked. Track and communicate:
- Cost per deployment
- Infrastructure cost per customer
- Ratio of platform engineers to product engineers
- Incidents per month (trend line)
- Developer hours saved by platform tooling

Numbers that show efficiency and leverage. If you can't quantify your value, someone else will quantify your cost.

### The Constant Reorg

Growth companies reorganize frequently because:
- New leaders arrive with different philosophies
- The company outgrows its current structure every 12-18 months
- M&A creates integration challenges
- Markets shift and organizational focus follows

**How to survive reorgs:**
- Don't over-invest in current reporting relationships (they'll change)
- Build relationships broadly (so you survive any reorg with allies)
- Make your team's value visible beyond one VP's org (so you're valued regardless of where you land)
- When a reorg is rumored: don't panic, don't politic excessively. Quietly ensure your boss knows your value and your preferences.

---

## Growth Phase Anti-Patterns

### "Let's Wait Until Things Settle Down"

**What it means:** You're waiting for stability before making big moves.

**Why it's fatal:** At a growth company, things NEVER settle down. If you wait for calm, you wait forever. Act within the chaos. Build amid the construction. That's the job.

### "We Need to Hire Before We Can Do Anything"

**What it means:** You've made all your plans contingent on headcount you don't have yet.

**Why it's dangerous:** Hiring takes 3-6 months per senior role. If nothing happens until they arrive, you've wasted half a year. Meanwhile, the company's needs haven't paused.

**Instead:** What can you accomplish with the team you have NOW? Start there. Use early wins to justify the additional headcount, not the other way around.

### "At My Last Company We Had This Figured Out"

**What it means:** You're comparing an 800-person growth company to a 50,000-person enterprise.

**Why it's counterproductive:** Those processes existed because 20 years of iteration built them. This company hasn't had that time. Your job is to build the RIGHT process for THIS stage — not transplant a mature company's operating model onto an adolescent one.

### "The Architecture Is Wrong, We Need to Rewrite"

**What it means:** You've looked at the systems and they offend your engineering sensibility.

**Why it's usually wrong at growth stage:** The architecture isn't wrong — it's a survivor. It got the company to $100M+ ARR. It has problems, yes. But a rewrite is 12-18 months where you deliver nothing visible while the business continues needing features. You'll lose support by month 6.

**Instead:** Strangler pattern. Incremental replacement. One component at a time, each delivering standalone value. Never bet the company on a Big Rewrite.

---

## What Growth Phase Companies Need from Senior Directors

Not what they TELL you they need. What they actually need:

| Stated Need | Actual Need |
|-------------|-------------|
| "Fix reliability" | Build a reliability CULTURE and the systems to sustain it |
| "Move faster" | Remove the structural bottlenecks, not just throw bodies at it |
| "Scale the platform" | Make architectural bets that work at 10x current load |
| "Reduce costs" | Build efficiency into the system so costs scale sub-linearly with revenue |
| "Hire a team" | Build an organization that can grow without you as bottleneck |
| "Improve developer experience" | Create leverage — make 400 engineers 30% more effective (= 120 engineer-equivalents) |

The Director's job: interpret the stated need into the structural solution. This is where your enterprise experience HELPS — you've seen what mature versions of these solutions look like. You know the end state. Now build toward it in growth-company increments.

---

## Chapter Summary

Growth-phase companies have specific physics: constant change, speed pressure, scaling breakdowns, thin institutional memory, and competing demands (grow AND be efficient AND be reliable). Everything is breaking at scale — that's why you were hired. Your enterprise instincts are valuable but must be calibrated to the speed, ambiguity, and resource constraints of this environment. The core skill: deliver value in short cycles while building toward a longer vision, within a landscape that shifts quarterly.

**The fundamental insight:** A growth company doesn't need you to be perfect. It needs you to be fast enough to keep up with the growth, strategic enough to see around corners, and resilient enough to operate in permanent ambiguity. Comfort with discomfort is the prerequisite.
