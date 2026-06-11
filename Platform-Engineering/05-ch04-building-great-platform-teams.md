# Chapter 4: Building Great Platform Teams

> **Part II — Platform Engineering Practices**

> *"It's not DNS. There's no way it's DNS. It was DNS."* — SSBroski

The DNS joke opens this chapter because it perfectly captures the staffing challenge of platform teams: DNS is nearly 40 years old and seems like it should be well-understood, yet it still causes complex failures regularly. It takes expertise not just to debug those failures, but to avoid creating new ones. Platform teams face the same dynamic — they build abstractions over complex systems to enable productivity, but if they aren't staffed with people who deeply understand those systems, they create operational problems that are far more expensive to fix than they were to prevent.

This chapter is about the people: who you need, what roles exist, how to hire them, how to recognize their work, and how to create a culture where diverse engineering skills work together instead of pulling in opposite directions. The central argument: **great platform teams require a deliberate mix of software engineers and systems engineers**, and most organizations are biased toward one or the other — creating teams that are strong builders but weak operators (or vice versa).

## Table of Contents

- [The Risks of Single-Focus Platform Teams](#the-risks-of-single-focus-platform-teams)
  - [Too Much Systems Focus](#too-much-systems-focus)
  - [Too Much Development Focus](#too-much-development-focus)
- [The Four Roles of Platform Engineers](#the-four-roles-of-platform-engineers)
  - [Software Engineers](#software-engineers)
  - [Systems Engineers](#systems-engineers)
  - [Reliability Engineers](#reliability-engineers)
  - [Systems Specialists](#systems-specialists)
- [Hiring and Recognizing Engineers in All Roles](#hiring-and-recognizing-engineers-in-all-roles)
  - [Titles, Level Matrices, and Interviews](#titles-level-matrices-and-interviews)
  - [The Platform Software Engineer Interview](#the-platform-software-engineer-interview)
  - [Interview for Customer Empathy](#interview-for-customer-empathy)
- [What Makes a Great Platform Engineering Manager?](#what-makes-a-great-platform-engineering-manager)
- [Other Roles on a Platform Team](#other-roles-on-a-platform-team)
- [Creating a Platform Engineering Team Culture (Case Study)](#creating-a-platform-engineering-team-culture-case-study)
- [Wrapping Up](#wrapping-up)

**Block types:** [Core Concept] [Deep Dive] [Anti-Pattern] [Worked Example] [Organizational Reality] [SRE/Production Lens] [Comparison] [AI Impact]

---

## The Risks of Single-Focus Platform Teams

Before presenting their model for balanced teams, the authors paint vivid portraits of what happens when teams are staffed with only one type of engineer. These are deliberately extreme characterizations — not all teams will match perfectly — but they describe failure patterns that are immediately recognizable to anyone who's worked in the space.

### Too Much Systems Focus

**The team profile:** Heavily populated by people from infrastructure, DevOps, SRE, and systems engineering backgrounds. Most have CS degrees but few have written significant code within large software systems.

**What they do well:** These teams are operationally excellent. They know their systems inside and out, including the underlying dependencies. When Asia goes down at 2 a.m., not only is the US team on it, but their leadership is awake and ready to help. Incident reviews are done by next day, with quick mitigations already in production and longer-term fixes planned. They are reliable, hardworking, and detail-oriented about operations.

**What they do badly:** The code they write is mostly automation, templating, and one-off tools. They aren't building better abstractions to manage complexity or working on architectural improvements to solve operational problems for good. Faced with system flaws they can't change through software, they reach for **rules and processes** — cataloged in meticulous wikis. Users constantly violate these rules, frustrating both sides. To make progress, the team relies on project managers to harass customer engineers into doing one-off work that the platform team can't streamline through software.

**Why they're stuck:** Their hiring process emphasizes deep system knowledge found in books and manual pages — "they might as well hang a sign over the door saying 'no software engineers need apply.'" They justify this as "what we need operationally" and "we can't afford to train anyone with this workload." The technical filter becomes a cultural filter. Generalist software engineers — exactly the type who could build better abstractions — stay away. The only SWEs they can hire are new grads, who leave after a year due to lack of mentorship. The churn reinforces the team's belief that systems aren't appealing to software engineers — when really it's the *culture* that drives them off.

### Too Much Development Focus

**The team profile:** Full of career software engineers and software engineering managers. They love writing code. They have CS degrees and extensive software experience, but usually very little of it involved developing platforms or infrastructure.

**What they do well:** These teams are builders. They think big about "golden paths," "vNext," and "next-gen" platforms. They nerd out on architecture and technology choices. They're innovative and fearless about tackling unsolved problems. And they're not wrong about what's possible — if they had infinite time.

**What they do badly:** They treat existing systems as what systems consultant Carla Geisser calls **"haunted graveyards"** — curiosities to be carefully poked, not systems to be understood. They view any effort on the old system as "throwaway work" distracting from building the new system faster. They're too optimistic in estimates. Operational problems fester. The 2 a.m. page? You'll have to call the on-call multiple times before they respond. Their manager will be upset you thought waking them would help.

**Why they're stuck:** The industry has spent 20 years viewing "shipping new code" as the most valuable thing software engineers do — heavily tied to compensation and promotions. This bias extends to managers who rose by writing code. They can't imagine hiring someone titled "software engineer" who can't solve algorithm problems on a whiteboard, regardless of other abilities. They view systems-focused engineers as doing "not real engineering" — someone who should be on a different team, doing automation and grunt work so the "real" engineers can focus on code. Unless the platform is massive, nobody wants that job.

> **[Core Concept: The Single-Focus Trap — Why Balance Is Hard]**
>
> The authors present these two failure modes not as hypotheticals but as the *default outcome* of how the industry is organized. Most engineering organizations naturally produce one of these two team types, because:
>
> 1. **Hiring reproduces culture.** Teams hire people who are similar to themselves. A systems-heavy team's interview process selects for more systems people. A dev-heavy team's interview selects for more developers. The bias compounds over time.
>
> 2. **Recognition reinforces focus.** If your company promotes for "lines of code shipped," systems engineers leave. If your company promotes for "uptime achieved," software engineers building v2 don't get promoted. People optimize for what gets rewarded.
>
> 3. **Organizational expectations lock you in.** The rest of the company expects "that infra team" to keep infrastructure running (systems focus) or expects "that dev team" to ship new features (development focus). Changing the team's mission requires changing everyone else's expectations — which is much harder than just hiring differently.
>
> **The escape:** Deliberately hire for the *opposite* of your current team's strength. If you're systems-heavy, your next 2-3 hires should be strong software engineers. If you're dev-heavy, your next hires should be experienced systems people. This feels uncomfortable because the new hires "don't fit" the existing culture — but that's exactly the point. You're building a *new* culture.

> **[Comparison: Manager's Path Connection]**
>
> Camille Fournier's earlier book *The Manager's Path* discusses how engineering managers shape team culture through hiring, recognition, and what they personally model. This chapter is the platform-specific application of those principles: the manager's job is to deliberately create a culture that values both building AND operating — even when the industry's default incentive structures pull in one direction.

---

## The Four Roles of Platform Engineers

To unstick single-focus teams, you need to equally value both software development and systems work. The authors propose four distinct roles:

| Role | Focus | What They Do |
|------|-------|-------------|
| **Software Engineer** | Building platform software | Write code that creates abstractions over complex systems. Drawn to understanding systems, comfortable on-call, ship deliberately. |
| **Systems Engineer** | Broad systems generalist | Automation, infrastructure integration, scaling, reliability config. Use broad systems knowledge to resolve deep issues involving both platform code and underlying dependencies. |
| **Reliability Engineer** | Focused on reliability practices | Incident management, SLOs, chaos engineering, production readiness reviews, postmortems, operational meetings. "How do we make everyone a little better?" |
| **Systems Specialist** | Deep expertise in specific area | Kernel engineer, networking engineer, performance engineer, storage engineer. Game-changing at scale, but hire only when need is clear. |

### Software Engineers

Platform software engineers are different from typical "backend" software engineers on application teams in three specific ways:

**1. They are drawn to understanding systems.** Not just completing features for end users, but thinking about how their code fits into the ecosystem of software, hardware, and networking. They read library source code. They're curious about failure patterns at the edges. They want to understand how their code actually runs in production.

How to spot them: *"Even when they're not paged, they will engage during incidents and make remediation much faster."*

**2. They are comfortable being on call for business-critical systems.** Not just willing — *effective* at it. Many engineers enjoy poring over system details intellectually but struggle at 2 a.m. under pressure. The causes vary (Unix skills, communication under pressure, comfort with ambiguity), but the result is the same: some engineers who love systems *design* are not suited to systems *operation*.

**3. They are comfortable shipping at a deliberate pace.** Platform teams don't move at startup speed. There are large costs to mistakes — operational risk and the risk of getting stuck supporting expensive features. An engineer strongly motivated by novelty and fast-turnaround feature building likely won't be a great fit for a mature platform team. (Chapter 8 notes these "pioneers" are better suited to early-stage platforms.)

> **[Organizational Reality: Finding Platform Software Engineers]**
>
> The authors acknowledge these engineers are rare because the industry hasn't trained for them. The standard software engineering career path emphasizes feature velocity, algorithm optimization, and system design for *applications*. Platform engineering needs engineers who combine software skills with systems curiosity AND operational comfort.
>
> **Where to find them:**
> - Watch who engages in incidents voluntarily (internal signal)
> - In behavioral interviews, ask about the largest incident they helped resolve — probe for whether they were genuinely significant in resolution
> - Look for engineers who have operated systems they built (not just built and handed off)
> - Former SREs who want to build more but haven't lost their operational instincts
>
> **What to avoid:** Engineers who are excited about platform architecture *in theory* but have never been on call, never debugged a production system under pressure, and have never dealt with the slow grind of maintaining something others depend on. They'll build beautiful v2 systems that create operational nightmares.

### Systems Engineers

The broad systems generalist — what many companies call a DevOps engineer, though the authors prefer not to use that name (because in a platform engineering culture, *everyone* should think in terms of product features, not just automation or reliability).

These engineers aren't world experts in any one area (performance, Linux, networking) but understand a lot more about how different systems work together than most software engineers. Their strength: resolving deep issues that span the platform codebase AND underlying dependencies. Software engineers often leave such issues languishing for months because they lack the systems knowledge to make progress.

**Why broad over specialized:**
1. Specialization takes years — hard to hire systems engineers who aren't already senior
2. Strong systems engineers feel pressure to specialize for promotions — you lose their valuable breadth
3. You don't want too many specialists, but you always need broad systems engineers

### Reliability Engineers

Not all "SRE" work. The authors distinguish: reliability engineers are those who want their role focused *specifically* on reliability practices, versus the broader systems engineer role that also encompasses support, efficiency, security, performance, and features.

What they excel at: high-impact incident management, SLO consulting, chaos engineering, game days, production readiness reviews, rigorous postmortems, operational meetings. They ask *"How do we make everyone a little bit better?"* — a social-technical question.

The authors recommend rotating reliability engineers in and out of platform teams to keep their skills current. Otherwise they risk being seen as "talkers who have never done it."

### Systems Specialists

Kernel engineers, networking engineers, performance engineers, storage engineers. Game-changing at scale — but the authors strongly advise waiting to hire them until the need is clear. Keep the bar high.

> **[Anti-Pattern: The Overspecialized Team]**
>
> The authors give a telling example: a developer tools team staffed entirely with version control experts. Instead of fixing the biggest user problem (lack of user-friendly tooling), they spent all their time refining interfaces to the version control system — because that's what specialists find interesting.
>
> Another anti-pattern: **"specialist as internal evangelist."** They imagine spending time contributing to OSS of no immediate company value, speaking at conferences, and researching obscure offerings. "Evangelism is a full-time role for SaaS vendors — when an engineer tries to make a full-time role of it internally without having much to show for their expertise, they tend to struggle for credibility."

---

## Hiring and Recognizing Engineers in All Roles

### Titles, Level Matrices, and Interviews

The authors present a practical framework:

| Role | Title | Interview | Level Matrix |
|------|-------|-----------|-------------|
| **Software Engineer** | Prefer "software engineer." Allow "platform software engineer" only if unavoidable. | Custom behavioral interview for platform fit | Company-wide software engineering ladder |
| **Systems Engineer** | Allow specialized (e.g., "DevOps engineer") | Same as SWE but more flexibility on coding; design covers systems breadth | Shared across all 3 systems roles |
| **Reliability Engineer** | Allow specialized (e.g., "SRE") | Same as systems eng; design covers SRE depth | Same as above |
| **Systems Specialist** | Allow per-role (e.g., "kernel engineer," "performance engineer") | Same as SWE; design covers their specialization | Same as above |

**Key principles:**

**Allow role-specific titles** — forcing a kernel engineer to be titled "SRE" because that's your level matrix demeans their depth and confuses peers. Titles indicate specific roles. But don't let everyone choose arbitrary titles either — create a new title only for substantial role differences.

**Avoid creating a new "platform software engineer" level matrix.** Standard SWE ladders emphasize shipping new code, which platform engineers do more slowly (because the systems they work on are more critical). The temptation is to create a separate ladder. Resist this — multiple similar ladders are expensive to maintain. Instead, specify level criteria in terms of *outcomes achieved* rather than *methods used*. "This engineer increased deployment reliability from 95% to 99.9%" is level-appropriate regardless of whether they wrote 50k lines or 5k lines of code.

**Create at most one level matrix for all systems roles** — not three. Because systems engineers don't churn out code at the same rate, they often get hired at too-junior levels or fail to get promoted. One shared systems ladder (like Meta's Production Engineer or Amazon's Systems Development Engineer) accommodates all three systems roles without creating confusing proliferation.

> **[Organizational Reality: Getting Systems Engineers Promoted]**
>
> The authors acknowledge this is a constant battle. Common failure modes:
> - A 10-year veteran of planet-scale systems gets offered a non-senior level "since they can't solve coding problems like a senior engineer"
> - Promotion committees struggle with engineers who wrote "only a thousand lines of code" in a year
> - Staff-level engineers who haven't "led building a new system" get blocked — because the panel equates leverage with new code
>
> **The workaround:** Find people outside platform engineering, at the next level up, who will attest "this person's impact is just as high as mine." Bringing individual cases forward forces the organization to adjust criteria. Over time, this builds evidence for systemic change.
>
> **Evidence for promotion cases** (from Diego Quiroga, Microsoft):
> - Tools, dashboards, or wikis they created (especially widely adopted ones)
> - Quality of customer interactions (clarity, depth, responsiveness)
> - Contribution to ticket resolution (volume AND complexity)
> - Involvement in postmortems, coaching other teams, proposing solutions
>
> Back these up with feedback from people on the receiving end. Prompt for feedback that speaks to both impact AND technical expertise needed.

### The Platform Software Engineer Interview

The authors recommend a specific interview structure designed for platform engineering — different from the standard "application software engineer" pipeline that many companies use:

1. **One traditional coding interview** — algorithm with naive/brute-force approach that can be optimized. Evaluate not just the optimal solution but also bookkeeping: error handling, edge cases, testing.

2. **One systems-aware coding interview** — may take 20 minutes to get code correct, but generates 30+ minutes of discussion about underlying assumptions: testing strategy, observability, what changes at scale (e.g., "what if inputs don't fit in memory?").

3. **One design interview focused on designing a platform** — not an application. (Key difference: application design asks "which platforms do I combine?" Platform design asks "how do I build the platform itself?")

4. **One inverted design interview** — candidate dives deep into something real they have designed and built. Tests depth of actual experience vs. theoretical knowledge.

5. **One behavioral/values interview** — focused on operational experience, ability to lead under conflict, and customer empathy.

**For systems roles:** Same outline, but with more flexibility on coding (offer a take-home coding problem + in-person discussion rather than live whiteboard). The authors insist on keeping *some* coding assessment even for systems roles — "there are many people who can't actually create code in existing production systems, including a lot of people whose resumes would make you think otherwise."

### Interview for Customer Empathy

The authors observed platform organizations developing "abrasive relationships" with their largest user groups — engineers treating users' problems with contempt while those users struggled with platform-caused issues.

This isn't just about "don't hire jerks." It also includes defensive behavior: touchiness around criticism, sighing and finger-pointing at the past, outbursts of "you users are lucky to have us." And sometimes the *user* is the difficult one — handling difficult users while supporting a system you didn't create takes maturity.

**Recommended screening questions:**
- "Tell me about a time when you helped one of your users understand the system."
- "Tell me about a time when you used customer feedback to change the direction of what you were building."
- "How do you understand your users in order to figure out whether a new feature is applicable to them?"

The authors note: *"Customer implies obligations; users are just some schmucks."* They prefer "customer empathy" over "user empathy" because it sets a higher bar for the relationship.

> **[AI Impact: AI Changing Platform Engineering Roles]**
>
> AI coding assistants are shifting the balance between "writing code" and "understanding systems" in platform engineering roles:
>
> **For software engineers on platform teams:**
> - AI handles more of the code generation, making the *systems understanding* and *operational judgment* aspects of the role even more important
> - The ability to evaluate AI-generated code for correctness in complex system contexts (concurrency, distributed systems, failure modes) becomes a critical skill
> - "Shipping deliberately" matters more than ever — AI can generate code fast, but understanding whether that code is safe to deploy to a platform serving 200 teams requires human judgment
>
> **For systems engineers:**
> - AI-powered troubleshooting (log analysis, correlation, pattern matching) amplifies their diagnostic abilities
> - But the broad systems intuition — "this failure pattern looks like a network partition, not a code bug" — remains human judgment that AI can't reliably replicate
>
> **For hiring:**
> - Interview processes may need updating: if AI can solve traditional coding problems, the differentiator becomes "can this person evaluate and debug AI-generated code in a systems context?"
> - The behavioral/customer-empathy interview becomes relatively MORE important as technical assessments get disrupted by AI
>
> **Net effect:** AI doesn't eliminate the need for platform engineering roles. It shifts the value from "can write code" (increasingly automated) toward "understands systems deeply enough to make safe decisions" (irreplaceable human judgment). The systems-curious, operationally comfortable, customer-empathetic profile the authors describe becomes *more* important, not less.

---

## What Makes a Great Platform Engineering Manager?

Three characteristics distinguish successful platform engineering managers:

### 1. Experience Operating Platforms

Platform engineering involves operational complexity that managers from application backgrounds don't appreciate. Underlying systems have "ill-defined boundaries" — a problem in one area can cascade in surprising ways. It takes humility and patience to manage a team slowly addressing systemic issues.

**Failure mode #1:** A software engineering leader without operational experience encourages the mindset that the solution is "one brilliant engineering fix away." For every brilliant fix that works, the authors have seen 10 that failed and compounded operational problems.

**Failure mode #2:** Hiring a good manager from a customer organization. Upsides: established manager, fast customer empathy, organizational relationships. Risks: they come from less operational complexity, may think underlying problems are "easy to solve," may view existing engineers as "doing things wrong" — alienating the strongest team members.

### 2. Experience on Big, Long-Running Projects

Managers used to "move fast and break things" get frustrated by platform engineering's slower pace. When many teams depend on your platform, changes must be made carefully. A multi-month migration without downtime is fundamentally different work from shipping a new feature daily.

Great platform leaders can both take criticism about slow delivery AND justify why the pace is right given the business criticality, complexity, and risk. They resist the temptation to "churn the team's focus by looking for quick fixes to regain face" under stakeholder pressure.

### 3. Attention to Detail

The most successful managers transitioning from application engineering to platform engineering are "detail-oriented sticklers who found motivation in doing project and process management personally."

Managers from infra backgrounds already know which details matter. Managers from application backgrounds need to track many details until they build instincts — which can feel like micromanagement. The authors' take: "if the options are 'my leader asks micromanaging questions to understand trade-offs' and 'my leader misses crucial details in making decisions that impact me,' most engineers will grudgingly prefer the former."

> **[SRE/Production Lens: The Platform Manager's Operational Instinct]**
>
> What "experience operating platforms" actually means in practice:
>
> - **Understanding cascading failures:** A platform manager needs to know that "just deploy the fix" at 2 a.m. might make things worse. They need the instinct for "let's mitigate first, fix properly later."
> - **Knowing when NOT to ship:** Application managers are trained that blocking deploys is a failure. Platform managers sometimes need to say "we're not shipping this Thursday because the risk profile has changed."
> - **Prioritizing operational hygiene:** Valuing the engineer who spent a week cleaning up alert noise (invisible work) as much as the engineer who built a new feature (visible work).
> - **Patience with systemic issues:** Some platform problems take 6 months to fix properly. A manager who demands quarterly "wins" will force shortcuts that create new problems.
>
> The authors from Chapter 1's SRE critique resurfaces here: they're not anti-SRE-practices, they just want those practices embedded in a manager who ALSO has product sense and software development appreciation.

---

## Other Roles on a Platform Team

### Product Managers

Good platform PMs are exceptionally hard to find. Most PM orgs tie value to revenue and external customers — few PMs have experience with internal platforms. Risk: PMs who bring a "business obsession" mindset may prioritize customer-visible features at the expense of reliability and developer productivity. One engineer's experience: *"Why is it so bad if engineers get interrupted every 10 minutes and can't deliver on anything else, as long as the customer is happy?"* — a startup mindset that's dysfunctional on a platform team.

**The authors' solution:** Turn to product-minded people from engineering or technical program backgrounds. For every PM with formal PM experience, they've worked with two who transitioned from engineering. It's a gamble that often pays off — but you still need *some* experienced PMs to train and calibrate the newbies.

**When you can't hire PMs:** The best fallback is staff engineers — specifically the ~25% who are "strong two-way communicators invested in doing what is right for the business." They listen to customers, internalize feedback, and look for incremental solutions even when it takes them away from building their ideal system.

### Project Managers / Technical Program Managers

The authors acknowledge TPMs are "the most vilified role in engineering organizations" — but argue the problem is usually the conditions they're asked to deliver in, not the role itself. When executives don't prioritize properly, TPMs are forced into brute-force cross-org execution (which feels like "harassing people for updates").

Advice: hire PMs first. Use EMs and tech leads for small-medium projects. Bring in TPMs only for broad, execution-focused projects that genuinely need 100% of someone's time. Find TPMs comfortable with your company's current processes — not ones who'll spend their first year trying to recreate big-company processes that don't exist.

### Developer Advocates, Technical Writers, Support Engineers

Only needed at very large scale (1000+ engineer orgs). Before that, engineers and PMs should perform these functions. Push back against "not my job" attitudes — and make sure this work gets recognized even if it's not in the level matrix.

---

## Creating a Platform Engineering Team Culture (Case Study)

The authors present a real case study of merging two teams with divergent cultures:

**The situation:** A compute platform based on complex OSS. Two teams:
- A **development team** of software engineers (mostly recent PhDs in systems-related fields, hired via standard SWE interviews with no screening for operational skills or customer empathy)
- A separate **SRE team** (small, mostly newcomers, hired into a different org)

**The development team's strengths:** Innovative, fearless about unsolved problems, knocked down technical barriers, delivered advances. Created solutions nobody in the OSS community had achieved.

**The development team's weaknesses:** Operational instability in new systems. Preferred to solve problems via "new build" rather than understanding and fixing existing infrastructure. Stuck in "pioneer mode." Customers unclear on delivery timelines. The separate SRE team made it worse — developers viewed reliability as "SRE's problem."

**The fix:**

1. **Merged the teams** under a manager from the SRE side with strong operational experience, long-running project skills, and stakeholder management ability
2. Balanced the team with people who wanted to build new things, people happy to scale and operate existing things, and people focused on customer communication
3. Moved from "one engineer, one feature" model to a **roadmap model** with consolidated priorities
4. Over ~6 months, stabilized operationally
5. Added a PM for product management — carefully ensuring tech leads still felt heard and EMs not undermined

**The cost:** Lost some innovative research-focused developers who preferred the old model. Mostly moved them to more appropriate roles — but lost a couple of good engineers who ended up "stuck on the wrong team." Cultural change has real personnel costs.

**The culture challenge:** The broader company culture valued "collaboratively building innovative things." The platform team needed a *different* culture — one that balanced innovation with stability, reliability, and usability. Platform teams typically develop slightly more conservative cultures than product engineering counterparts. This is fine — but leaders must watch for "us versus them" mindsets. "When your pride in running highly reliable systems turns into scorn at product teams who keep shipping broken code, you risk destroying the customer empathy that is so important."

> **[Organizational Reality: Cultural Change Has Real Costs]**
>
> The authors are refreshingly honest about what culture change actually means:
> - You will lose people. Some excellent engineers don't fit the new culture and will leave (or need to be moved).
> - It takes months, not weeks. The case study mentions ~6 months for operational stabilization — and cultural change takes longer.
> - You can't please everyone. "Pioneer" engineers who thrive in chaos won't be happy when the team stabilizes and slows down. That's a feature, not a bug — but it feels like a loss.
> - The broader org resists. Platform culture often differs from company culture. You need to be explicit about why yours is different while still respecting the broader values.
>
> **The key leadership move:** Recognize and reward different roles and skill sets. Talk about how they contribute to the whole. Take time to appreciate partner teams. If you only celebrate the person who built the new system (dev focus) and not the person who kept the old system running (ops focus), you'll recreate the imbalance you just fixed.

---

## Wrapping Up

The chapter's core argument: **platform teams fail when they're defined by what the team can produce (based on their skills) rather than what customers need.** A systems-heavy team builds great operations but can't build software abstractions. A dev-heavy team builds great software but can't operate it reliably. Both produce platforms shaped by team composition rather than user requirements.

The fix: deliberate diversity of skills and roles, supported by:
- Hiring processes that accommodate all four roles
- Level matrices that recognize non-code impact
- Managers with operational experience AND product sense
- Cultural investment in valuing different types of contributions equally

Without this foundation, the rest of the book's advice (product thinking, operational practices, stakeholder management) can't take root. You need the right people, recognized for the right work, led by the right managers — and only then can you build great platforms.
