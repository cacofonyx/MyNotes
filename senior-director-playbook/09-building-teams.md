# Chapter 09: Building and Structuring Multiple Teams

> *"Organizational design is the art of turning business strategy into team structure."* — Will Larson

At Senior Director level, you don't build a team. You build an ORGANIZATION — multiple teams with different missions, different skills, and different interaction patterns. The structure you choose IS an architectural decision: Conway's Law guarantees that your org shape will mirror into your system shape. Choose wisely.

---

## The Team Topology for Platform/SRE at IGA Scale

### Team Topologies Applied

Using Skelton and Pais' framework, Platform/SRE organizations typically contain:

| Team Type | What They Do | IGA Example |
|-----------|-------------|-------------|
| **Platform team** | Build and maintain shared infrastructure as a product | Deployment pipeline, observability stack, compute platform |
| **Enabling team** | Help other teams adopt platform capabilities | Developer experience, onboarding, migration support |
| **Stream-aligned team** | Deliver continuous value on a specific workflow | Connector reliability, tenant provisioning automation |
| **Complicated-subsystem team** | Own deeply specialized technical domains | Cryptography/key management, performance/scale engineering |

### A Realistic Org Structure (Target State for 30-50 People)

```
Senior Director (You)
├── Manager: Platform Infrastructure
│   ├── Compute & Orchestration (K8s, container platform)
│   ├── Data Platform (databases, caching, streaming)
│   └── Networking & Service Mesh
├── Manager: Developer Experience & Delivery
│   ├── CI/CD Pipeline
│   ├── Developer Tooling & Self-Service
│   └── Internal Platform Product (portal, docs, SDK)
├── Manager: Site Reliability Engineering
│   ├── Production Operations & On-Call
│   ├── Observability & Monitoring
│   └── Incident Response & Reliability Engineering
├── [Optional] Manager: Security Infrastructure
│   ├── Secrets Management & Key Infrastructure
│   ├── Compliance Automation
│   └── Security Tooling
└── Staff/Principal Engineers (reporting to you or dotted-line)
    ├── Platform Architect
    └── Reliability Architect
```

**You don't start here.** You inherit or start with maybe 10-15 people and grow to this over 12-24 months. The target state informs your hiring plan, even if current reality is much smaller.

---

## Principles of Org Design at Director Level

### Principle 1: Optimize for Team Independence

Each team should be able to:
- Make decisions without needing approval from other teams
- Deploy their work independently
- Have clear ownership of their domain
- Measure their own success

**Why:** Interdependent teams create coordination overhead that scales quadratically with team count. Independent teams scale linearly.

**IGA-specific challenge:** High coupling between infrastructure components. Connector reliability depends on compute, networking, and observability simultaneously. You can't fully decouple — but you can minimize required synchronization points.

### Principle 2: Align Teams to Value Streams, Not Technical Layers

**Anti-pattern:** "Database team," "Frontend infrastructure team," "Monitoring team" — organized by technical specialty.

**Better:** "Connector reliability team" (owns the full stack for making connectors reliable), "Deployment velocity team" (owns everything from code merge to production), "Tenant experience team" (owns provisioning, scaling, isolation end-to-end).

**Why:** Layer-oriented teams require coordination across layers for any user-visible improvement. Stream-oriented teams can deliver end-to-end value independently.

**The exception:** Some genuinely cross-cutting concerns (observability, security) are better as platform/enabling teams that serve stream-aligned teams. Don't force everything into streams.

### Principle 3: Conway's Law Is Your Tool, Not Your Enemy

Your team structure WILL shape your system architecture. Use this deliberately:

- Want microservices? → Organize teams around service boundaries.
- Want a unified platform experience? → Create a single team responsible for the platform interface layer.
- Want connector independence? → One team owns the framework; connector-specific work is distributed.
- Want fast incident response? → Embedded SREs or on-call rotation that creates ownership.

**The design question:** "Given the system architecture we WANT in 18 months, what team structure would naturally produce it?"

### Principle 4: Size Teams for Cognitive Load

Team Topologies' key insight: a team should own only what they can cognitively manage. If a team owns too much, they either:
- Drop balls (things fall through cracks)
- Become bottlenecks (everything queues waiting for them)
- Burn out (unsustainable pace)

**Rule of thumb:** 5-8 people per team. Owns 2-4 services/systems max. Can be fully understood by any team member within 6 months of joining.

**When to split a team:** When the cognitive load is visibly too high — long backlogs of unaddressed work, frequent context-switching, people only understanding "their part" of the team's ownership.

---

## Building the Org Over Time

### Phase 1: Inherit and Understand (Month 1-3)

You likely inherit SOMETHING — maybe a small team, maybe individuals scattered across other orgs, maybe nothing formal at all.

**First moves:**
- Map what exists: who does what, what they own, where the gaps are
- Don't reorganize immediately — understand the current state's LOGIC before changing it
- Identify: what's working (don't break it), what's clearly broken (first priorities), what's missing (inform hiring plan)

**Critical assessment questions:**
- Who are your strongest people? (Protect and invest in them)
- Who's in the wrong seat? (Not bad — just mismatched to role)
- What single-points-of-failure exist? (One person holding critical knowledge)
- Where is the team over-loaded? (Work that requires 3 people but has 1)

### Phase 2: First Hires (Month 3-6)

**Hire your managers FIRST.** You cannot build 3-4 teams if you're personally managing all of them. Your first hires should be:

1. **The strongest manager you can get** for the most critical gap
2. **A senior IC** who can be the technical backbone while teams form
3. **Fill the burning gap** — whatever is causing daily pain

**What to look for in managers you hire:**
- Have they managed in growth-stage environments? (Enterprise-only managers will repeat your adaptation challenge)
- Can they operate autonomously? (You can't micromanage 4 managers)
- Do they complement your skills? (If you're strategic, hire operators. If you're technical, hire people-leaders.)
- Are they comfortable building? (Not just running established teams)

**Hiring pitfall:** Don't hire all from enterprise. Don't hire all from growth-stage. Mix gives you both calibration and credibility.

### Phase 3: Structure and Charter (Month 4-8)

Once you have 2-3 managers and 15+ people, formalize team structure:

- Each team gets a written charter (1 page): mission, ownership, what's NOT theirs, how they interface with other teams
- Each team gets metrics they own: SLOs, velocity measures, or capability metrics
- Each team gets explicit interaction patterns: who do they support? How do they take requests? What's their interface?

**The chartering exercise:**
- Involve the managers in designing it (they'll be more committed to a structure they shaped)
- Socialize with peer directors (they'll depend on knowing how to engage your teams)
- Review and adjust quarterly (first attempt won't be perfect)

### Phase 4: Scale (Month 8-18)

Growing from 15 to 40 people introduces new challenges:

| Challenge | What to Do |
|-----------|-----------|
| Communication breaks down | Introduce lightweight rituals: weekly all-hands (30 min), cross-team demos |
| Quality of hires varies | Standardize interview process, calibrate across managers |
| Teams drift apart | Regular manager sync (you + all your directs), shared roadmap visibility |
| New people don't know the "why" | Onboarding process, architecture docs, decision records |
| Middle management gap | You can't skip-level manage everyone; trust your managers, coach them |

---

## Managing Managers (The New Skill)

### What Changes When Your Directs Are Managers

| Managing ICs | Managing Managers |
|-------------|-------------------|
| You can observe their work directly | You observe outcomes, not process |
| Feedback on execution | Feedback on judgment and leadership |
| You unblock them | You coach them to unblock themselves |
| You know their team members well | You know their team through them (and occasional skip-levels) |
| You can rescue if they struggle | If they struggle, 5-10 people are affected — rescue is expensive |

### The Manager 1:1

Your 1:1 with each manager covers:

1. **Their team health** — Retention risk? Performance issues? Morale?
2. **Their delivery** — On track? Risks? Blockers they need you to remove?
3. **Their decisions** — What calls have they made? (Not to second-guess — to calibrate)
4. **Their growth** — Where are they struggling? How can you help?
5. **Cross-team issues** — Anything that requires your orchestration?

**The coaching stance:** "Tell me about a hard decision you made this week" → listen → ask what they considered → offer alternative frames they might not have seen → let them reach their own conclusion.

### Skip-Level Meetings

Meet with people 2 levels below you (the ICs) quarterly or semi-annually:
- To calibrate: Is the picture your manager paints accurate?
- To stay connected: Senior leaders who are invisible create anxiety
- To spot issues early: Retention risks, cultural problems, capability gaps
- To signal investment: "My boss's boss cares about my growth"

**Rules for skip-levels:**
- Never undermine the manager. If someone complains about their manager, say: "That sounds frustrating. Have you talked with [manager] about it? I'll check in with them."
- Don't make promises. You're listening, not acting.
- Share what you learn with the manager (in general terms, not violating confidence). "Your team seems concerned about X — have you noticed?"

---

## Team Health and Dynamics

### The Health Metrics

| Metric | Healthy | Warning | Intervention Needed |
|--------|---------|---------|---------------------|
| Attrition | <10% annual | 10-15% | >15% — something is wrong |
| On-call burden | Sustainable (2-3 incidents/week) | Heavy (daily pages) | Crushing (people losing sleep regularly) |
| Delivery predictability | Team commits and hits ~80% | ~60% | <50% — scope or capacity problem |
| Engagement | People volunteer for challenges | People do assigned work only | People are checking out or job-hunting |
| Cross-team collaboration | Teams help each other naturally | Teams escalate conflicts | Teams actively avoid each other |

### When to Reorganize

Reorg is expensive. It breaks relationships, creates uncertainty, disrupts delivery for 4-6 weeks, and signals instability. Don't do it casually.

**Reorg IS warranted when:**
- Teams can't deliver because ownership is fragmented
- Conway's Law is producing the wrong architecture
- Growth has created teams that are far too large or too small
- A team's mission has fundamentally changed and the current people/skills don't match

**Reorg is NOT warranted when:**
- You just want things to "feel" cleaner
- You have a performance problem that's really about people, not structure
- You're new and want to "put your stamp" on the org
- One person left and you're restructuring around the gap

---

## The IGA-Specific Team Design Challenge

### The Connector Problem

IGA has potentially hundreds of connectors (target systems). You can't have one team per connector. You need:

**Option A: Connector framework team + distributed connector ownership**
- Central team owns the framework, SDK, testing infrastructure
- Product teams or domain teams own individual connectors
- Platform provides the rails; others build on them

**Option B: Connector platform team owns all connectors**
- One team owns the framework AND all connectors
- Scales poorly beyond ~30 connectors
- But maintains consistency and quality

**Option C: Connector tiers**
- Tier 1 (top 20 most important): Dedicated team with deep ownership
- Tier 2 (next 50): Shared ownership with automated testing
- Tier 3 (remaining): Community/partner-maintained on your framework

Most IGA companies at scale end up at Option C. Your org design should anticipate this.

### The Hybrid Deployment Problem

IGA requires on-premises agents. This creates a team design question: who owns the agent lifecycle?

- If a separate team owns agents → coordination overhead with cloud platform team
- If one team owns both → extremely broad cognitive load
- If product teams own agents → platform loses control of a critical component

**The resolution:** Platform owns the agent FRAMEWORK and lifecycle infrastructure (updates, health monitoring, connectivity). Domain teams own what agents DO (specific connector logic). Split at the interface boundary.

---

## Hiring at Director Level

### What Changes About Hiring When You're a Director

| EM Hiring | Director Hiring |
|-----------|-----------------|
| You hire ICs into your team | You hire managers who hire ICs |
| Technical assessment dominates | Leadership assessment dominates |
| You're the decision-maker | You're the calibrator (your managers make IC hiring decisions) |
| Speed matters | Quality matters more (a bad manager affects 5-10 people) |
| One bad hire is recoverable | One bad manager hire cascades |

### The Manager Hiring Bar

A manager you hire should be someone you'd be comfortable NOT managing for 6 months. If you'd need to closely supervise them, they're not ready for this role at this company.

**Assessment dimensions:**
- Do they build good teams? (Ask for specific examples of teams they've built)
- Can they make hard decisions? (Performance management, trade-offs, firing)
- Do they communicate well upward? (You need reliable signal from them)
- Can they operate in ambiguity? (Growth stage = ambiguous)
- Are they self-aware? (Do they know their gaps and compensate?)

### Building a Diverse Team

At Director level, you're setting the composition of an entire organization. This is where diversity (thought, background, experience) compounds.

- Mix enterprise + growth-stage backgrounds (calibration from both sides)
- Mix deep specialists + generalists (both are needed)
- Mix tenured people + new hires (institutional memory + fresh eyes)
- Mix builders + operators (some people love creation, others love maintenance — both are essential)

---

## Chapter Summary

Org design at Director level is architectural work — your structure shapes your outcomes through Conway's Law. Optimize for team independence, align to value streams, size for cognitive load. Build incrementally: understand → hire managers first → formalize structure → scale. Managing managers is a fundamentally different skill from managing ICs — you coach judgment rather than observe execution. Reorganize only when structure actively prevents delivery, not for aesthetics.

**The end-state test:** Each team in your org can clearly answer: "What do we own? Who do we serve? How do we measure success? How do we interact with other teams?" If every team can answer these crisply, your org design is working.
