# Chapter 10: Modes of Control

> **High Output Management** — Andrew S. Grove
> *Free-Market Forces, Contractual Obligations, Cultural Values, and the CUA Factor*

Grove shifts from organizational structure (Chapters 7-9) to a deeper question: **what actually governs behavior in organizations?** He identifies three modes of control — free-market forces, contractual obligations, and cultural values — and provides a framework (the CUA factor) for determining which mode is most appropriate in any given situation. This chapter explains why culture matters to performance (not just to morale) and why the "right" control mode depends on the nature of the work and the motivation of the people doing it.

## Table of Contents

- [Three Modes of Control](#three-modes-of-control)
  - [Free-Market Forces](#free-market-forces)
  - [Contractual Obligations](#contractual-obligations)
  - [Cultural Values](#cultural-values)
- [The CUA Factor: Choosing the Right Mode](#the-cua-factor-choosing-the-right-mode)
  - [The Four Quadrants](#the-four-quadrants)
  - [The New Employee Progression](#the-new-employee-progression)
  - [The Outside Senior Hire Problem](#the-outside-senior-hire-problem)
- [Modes of Control at Work: Everything Mixed Together](#modes-of-control-at-work-everything-mixed-together)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Mental Model] [Anti-Pattern] [Modern Lens] [Scenario]

---

## Three Modes of Control

Grove uses a vivid everyday sequence to introduce the three modes:

1. **Buying tires** — you choose based purely on self-interest (best tires, lowest price). No relationship with the dealer matters. This is **free-market forces**.

2. **Stopping at a red light** — you don't think about it. It's a law (a social contract). Everyone agreed to follow the rule. Police enforce it. This is **contractual obligations**.

3. **Stopping to help at an accident** — you forget self-interest and rules. You expose yourself to danger to help strangers. This is **cultural values** — concern for the group overrides personal interest.

### Free-Market Forces

Based on **price**. Two parties exchange goods/services, each maximizing self-interest. No oversight needed. Extremely efficient *when the value of what's being exchanged is clearly defined.*

Limitation: works for commodities (tires, cloud compute, office supplies) but fails when value is ambiguous. How much is one engineer's contribution to a team project worth? The free market can't answer that.

### Contractual Obligations

When free-market pricing is impractical, parties enter **contracts**: "I'll pay you a salary, you agree to do a type of work to certain standards. I get the right to monitor and evaluate your performance." Rules, policies, and procedures are all forms of contractual obligation.

Requires **overhead** to monitor and enforce — just as traffic laws require police. Without enforcement, contracts degrade.

### Cultural Values

When the environment changes faster than rules can be updated, or when situations are too ambiguous for contracts to cover, behavior is governed by **shared values, objectives, and methods**:

> *"Its most important characteristic is that the interest of the larger group to which an individual belongs takes precedence over the interest of the individual himself."*

Requires **trust**: *"you are surrendering to the group your ability to protect yourself."* Trust develops only through *"a great deal of common, shared experience."*

Management's role: develop cultural values through **articulation** (stating values explicitly) and, more importantly, through **example** (behaving consistently with stated values — Grove's role modeling from Chapter 3).

> **[Core Concept: The Three Modes and Management's Role in Each]**
>
> | Mode | What Governs Behavior | Management's Role | Overhead |
> |------|----------------------|-------------------|----------|
> | **Free market** | Self-interest and price signals | None — the market self-regulates | Zero |
> | **Contractual** | Rules, policies, agreements, monitoring | Set rules, monitor adherence, evaluate performance, enforce | High — requires monitoring systems |
> | **Cultural values** | Shared values, trust, group interest | Articulate values and model them through behavior | Low in steady state — but high initial investment to build |
>
> **Grove's warning:** There's a temptation to idealize cultural values because they sound "nice." But they're not always the right mode. Buying tires via cultural values (paying whatever the dealer asks because you trust him) is inefficient. Enforcing traffic laws via cultural values alone (hoping everyone stops at red lights) would fail. The right answer depends on context.

---

## The CUA Factor: Choosing the Right Mode

Grove introduces the **CUA factor** — a composite measure of an environment's **Complexity, Uncertainty, and Ambiguity**:

- **Complex:** Many interacting parts, difficult to predict (Cindy's process engineering environment)
- **Uncertain:** Unclear whether resources, decisions, or outcomes will materialize (Bruce waiting for headcount approval)
- **Ambiguous:** Unclear who's in charge, what the priorities are, or which "end is up" (Mike, the transportation supervisor who quit)

### The Four Quadrants

| | **Low CUA** (clear, structured) | **High CUA** (complex, ambiguous) |
|--|--------------------------------|----------------------------------|
| **Self-interest motivation** | **Free market** — buy tires, negotiate vendor contracts | **Chaos** — every man for himself on a sinking ship. No mode works. |
| **Group-interest motivation** | **Contractual** — follow the rules, stop at red lights | **Cultural values** — help at the accident scene, make judgments based on shared principles |

### The New Employee Progression

Grove maps this to career development:

1. **New hire** — motivated primarily by self-interest (job security, learning, proving themselves). Give them a **clearly structured job with low CUA** — contractual mode works fine.
2. **Growing employee** — starts caring about the team, shares experiences with peers. Can handle **more complexity and ambiguity** — cultural mode starts working.
3. **Experienced veteran** — deeply shares values and methods of the organization. Thrives in **high-CUA environments** where judgment, not rules, governs decisions.

> *"This is why promotion from within tends to be the approach favored by corporations with strong corporate cultures."*

### The Outside Senior Hire Problem

> *"What do we do when for some reason we have to hire a senior person from outside the company?"*

The outside hire enters with **high self-interest** (proving themselves, no shared history) but is immediately given a **high-CUA job** (leading a team in trouble — that's why you went outside). They're in the chaos quadrant.

> *"All we can do is cross our fingers and hope she quickly forgets self-interest and just as quickly gets on top of her job to reduce her CUA factor."*

> **[SRE Lens: Modes of Control in SRE Operations]**
>
> All three modes coexist in SRE work:
>
> | Activity | Mode | Why This Mode |
> |----------|------|--------------|
> | **Choosing a monitoring vendor** | Free market | Evaluate features, pricing, support. Self-interest: get the best tool for the money. |
> | **Following the deployment process** | Contractual | CI/CD pipeline enforces gates. Change management policies define what's allowed. Monitoring enforces SLOs. |
> | **Deciding whether to wake someone at 3 AM for a borderline alert** | Cultural values | No rule covers every edge case. The on-call engineer uses judgment based on team norms: "We err on the side of paging because customer impact matters more than engineer sleep." |
> | **Helping a sister team during their P1 when you're not on-call** | Cultural values | No contract requires this. You do it because the culture says "we help each other during incidents." |
> | **Deciding what to work on during a slow on-call week** | Cultural values | No checklist covers this. Your team's culture determines whether you pick up tech debt, improve runbooks, or browse Reddit. |
>
> **The SRE cultural values that matter most:**
> - **Blameless postmortems** — cultural value, not a rule. You can't contractually mandate intellectual honesty.
> - **Err toward customer impact over engineer convenience** — this drives decisions about alert sensitivity, deployment timing, and on-call response.
> - **Shared ownership** ("not my service" is unacceptable) — cultural value that prevents the tragedy of the commons in shared infrastructure.
> - **Invest in automation over manual work** — cultural value that fights the natural human preference for familiar toil over unfamiliar automation.
>
> **Where contractual mode applies in SRE:** SLOs, error budget policies, on-call rotation schedules, escalation paths, deployment requirements. These are codified rules with monitoring and enforcement. They exist because cultural values alone aren't sufficient for critical safety-related behavior — you need both.

> **[Senior EM Application: The CUA Factor for Your Teams]**
>
> Use Grove's CUA framework to diagnose why certain parts of your organization struggle:
>
> | Symptom | Likely CUA Problem | Fix |
> |---------|-------------------|-----|
> | New engineers are lost and unproductive for months | High CUA for someone with no shared experience → they're in the chaos quadrant | Reduce CUA: structured onboarding, clear first tasks, assigned mentors (move them from cultural to contractual mode) |
> | Senior engineers resist new processes | They built their methods through years of shared experience (cultural mode) and now you're imposing new contractual obligations | Involve them in designing the new process (preserve cultural ownership) rather than mandating it (pure contractual) |
> | Teams fight over shared resources (compute, platform team time) | Free-market mode operating where contractual or cultural mode should | Establish allocation policies (contractual) or shared planning processes (cultural) instead of letting teams compete |
> | Outside senior hire is struggling 6 months in | High self-interest + high CUA = chaos quadrant (Grove's exact prediction) | Actively reduce CUA: give them a specific, scoped mission; pair them with a cultural guide; don't expect them to absorb values by osmosis |

> **[Modern Lens: DevOps Culture as Grove's Cultural Values Mode]**
>
> The DevOps movement — particularly the "Third Way" (culture of experimentation and learning) from *The DevOps Handbook* — is fundamentally about shifting engineering organizations from contractual mode to cultural values mode:
>
> | Traditional IT (Contractual) | DevOps/SRE (Cultural Values) |
> |----------------------------|------------------------------|
> | Change Advisory Board *approves* deployments | Engineers *decide* when to deploy based on canary signals and SLO health |
> | Incident response follows a *documented procedure* | IC uses *judgment* based on shared incident management values |
> | Security review is a *gate* before production | Security is a *shared responsibility* embedded in every engineer's work |
> | On-call is a *contractual obligation* (you're scheduled, you respond) | On-call is a *cultural commitment* (you own your service's reliability because you care about the customer) |
>
> The shift works only when the CUA factor is managed. You can't jump from contractual to cultural overnight — it requires the "common, shared experience" that Grove says is the foundation of trust. This is why DevOps transformations take years, not months, and why they fail when leadership tries to impose a "DevOps culture" by mandate (contractual) rather than building it through shared practice (cultural).

---

## Modes of Control at Work: Everything Mixed Together

Grove illustrates how all three modes coexist in daily work. Bob, a marketing supervisor:
- **Buys lunch** in the cafeteria → free market (he chooses what to buy and what to pay)
- **Shows up to work** → contractual (salary in exchange for effort)
- **Participates in strategic planning** beyond his regular job → cultural values (he contributes because he believes the company needs his input)

In Barbara's sales training program:
- **Buying binder materials** → free market (lowest price for required quality)
- **The training program itself** → contractual (salespeople *expect* regular training, even without a formal mandate)
- **Coordinating messages across divisions** → cultural values (divisions sacrifice self-interest for coherent customer communication)

Grove closes with a cautionary tale: marketing managers created sales contests (commissions, prizes for pushing specific products), which governed sales behavior through **free-market forces**. Then they complained that salespeople were "only governed by self-interest." But the managers themselves created that dynamic by using the market mode! If they wanted cultural behavior (balanced product promotion for the company's benefit), they needed cultural mechanisms, not financial incentives.

> **[Anti-Pattern: Using the Wrong Mode of Control]**
>
> | Situation | Wrong Mode Used | Why It Fails | Right Mode |
> |-----------|----------------|-------------|------------|
> | Wanting blameless postmortems | Contractual ("policy says no blame") | People follow the letter but not the spirit; passive-aggressive blame still happens | Cultural values — leaders model blamelessness; shared experience builds trust |
> | Wanting engineers to reduce toil | Cultural ("we value automation") | Without enforcement, toil reduction gets deprioritized in favor of shinier projects | Contractual — track toil %, set hard threshold (Google's 50% rule), enforce |
> | Wanting cross-team collaboration | Contractual ("teams must file cross-team requests through this ticketing system") | Creates bureaucratic overhead; teams game the system or route around it | Cultural — build relationships through embedded engineers, shared on-call, joint postmortems |
> | Wanting cost optimization | Cultural ("we should all be mindful of cloud costs") | Nobody's self-interest is served by spending time on cost optimization | Free market — teams have cloud budgets and keep savings (incentive alignment) |

---

**Chapter 10 establishes:** Behavior is controlled by three modes — free market, contractual, cultural values. The CUA factor (complexity, uncertainty, ambiguity) determines which mode is appropriate. Cultural values work best in high-CUA environments but require trust built through shared experience. Most work environments use all three modes simultaneously. The manager's job is to identify and apply the most appropriate mode for each situation.

**Next: Chapter 11 — The Sports Analogy, which opens Part IV (The Players) and addresses individual motivation and peak performance.**
