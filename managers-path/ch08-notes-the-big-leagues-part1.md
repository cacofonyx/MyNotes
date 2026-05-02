# Chapter 8: The Big Leagues — Part 1

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

> "My job wasn't to be the smartest person in the room. It wasn't to be 'right.' Rather, my role was to help the team make the best possible decisions and help them implement them in a sustainable and efficient way." — James Turnbull

This chapter is about **senior executive leadership** — CTO, VP of Engineering, SVP, and their equivalents. Fournier acknowledges this level varies wildly by company, but focuses on the core skills and challenges that all senior technical leaders share.

For a Senior EM aiming at Director, this chapter shows what's two levels ahead — useful for understanding how your Director thinks and what THEIR job demands.

**Part 1 covers:** Senior leadership job description, Andy Grove's four tasks, leadership models, VP of Engineering, CTO.
**Part 2 covers:** Changing priorities, setting strategy, delivering bad news.
**Part 3 covers:** Senior peers, the echo effect, ruling with fear vs. guiding with trust, True North.

## Table of Contents — Part 1

- [The Senior Technical Leader](#the-senior-technical-leader)
- [Models for Thinking About Tech Senior Leadership](#models-for-thinking-about-tech-senior-leadership)
- [What's a VP of Engineering?](#whats-a-vp-of-engineering)
- [What's a CTO?](#whats-a-cto)
- [Ask the CTO: Where Do I Fit?](#ask-the-cto-where-do-i-fit)

**Block types in Part 1:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Senior EM vs. Director] [Mental Model] [Cross-Functional Play] [Go Deeper]

---

## The Senior Technical Leader

Fournier opens with what's expected of a senior technical leader. The core capabilities:

- **Making hard decisions without perfect information** and facing the consequences
- **Understanding the current business landscape** and seeing its potential futures
- **Planning months and years ahead** so the organization is positioned for those futures
- **Understanding organizational structure** and its impact on team effectiveness
- **Playing politics productively** — moving the organization and business forward
- **Working well with non-engineering peers** and seeking their perspectives
- **Disagreeing and committing** — supporting decisions you didn't agree with
- **Holding individuals and organizations accountable** for output

**Andy Grove's four management tasks** (from *High Output Management*):

1. **Information gathering/sharing** — synthesizing large quantities of information, identifying critical elements, sharing appropriately
2. **Nudging** — asking questions to remind people of commitments, keeping the organization on track without giving orders
3. **Decision making** — setting direction with conflicting perspectives and incomplete information. "If making decisions were easy, there would be much less need for managers"
4. **Role modeling** — showing company values through your behavior, showing up for commitments, setting the best example

> **[Insight]** Grove's framework is powerful because it reveals what senior leaders actually DO with their time. It's not coding. It's not even managing in the traditional sense. It's: absorbing information, gently steering, making calls under uncertainty, and being watched. That last one — role modeling — is the most underestimated. As a senior leader, you're always on stage. Every interaction is observed and interpreted. Your mood in a meeting, your reaction to bad news, your choice of which project to visit — all are signals that ripple through the organization.

> **[SRE Lens: Grove's Four Tasks for SRE Senior Leaders]**
>
> | Task | SRE Application |
> |------|----------------|
> | **Information gathering** | Read every P1 postmortem. Monitor SLO trends across the org. Attend skip-levels. Scan incident channels. Know the operational state of the business. |
> | **Nudging** | "Have we done the production readiness review for that new service?" "What's our plan for the upcoming traffic spike?" "How's the on-call burden looking this quarter?" |
> | **Decision making** | Error budget policy decisions. Build vs. buy for reliability tooling. How to allocate SRE headcount across product teams. When to mandate reliability work over feature work. |
> | **Role modeling** | Staying calm during incidents. Being data-driven in discussions. Treating product engineers as partners. Taking vacation. Admitting mistakes publicly. |

---

## Models for Thinking About Tech Senior Leadership

Fournier identifies seven roles that senior leadership can play, combined differently at different companies:

1. **R&D** — experimentation, research, new technology generation
2. **Technology strategy/visionary** — how tech grows the business; predicting technology evolution
3. **Organization** — structure, staffing plans, ensuring projects are staffed
4. **Execution** — making things get done; aligning roadmaps, resolving conflicts
5. **Face of technology, external** — conferences, recruiting, customer meetings
6. **Infrastructure and technical operations** — infrastructure, cost, security, scaling
7. **Business executive** — understanding the business, balancing development with business growth

Common combinations:
- **CTO or Head of Engineering:** Business executive + technology strategy + organization + execution
- **CTO/Chief Scientist:** R&D + technology strategy + external face
- **VP of Engineering:** Organization + execution + business executive
- **CTO/CIO:** Infrastructure + organization + execution

> **[Deep Dive: Where Does SRE Leadership Fit?]**
>
> SRE senior leadership often combines:
> - **Infrastructure and technical operations** (core)
> - **Organization and execution** (team management)
> - **Technology strategy** (reliability as competitive advantage)
> - **Business executive** (cost optimization, risk management)
>
> At smaller companies, the SRE Director or VP might report to the VP of Engineering and own "infrastructure + operations + organization." At larger companies, SRE might be its own VP-level function, especially if reliability is a core business differentiator.
>
> **The career question:** As an SRE senior leader, which combination matches your strengths and aspirations? If you love strategy and business impact, you might aim for a CTO-style role. If you love building organizations and execution, VP of Engineering is more natural. If you want to stay deeply technical, a VP of Infrastructure or Chief Architect role might suit you.

---

## What's a VP of Engineering?

Fournier describes the VP of Engineering as typically the top of the management career ladder for engineers. Key characteristics:

- **Strong "ground game"** — can drop into details and make things happen at a low level
- **Tracks several in-flight initiatives** and ensures they're going well
- **Handles significant management responsibility** — aligns development roadmap to hiring plan, runs hiring process, coaches management team
- **Organizational strategy** — sets goals, ensures business goals translate to achievable technology goals
- **Both big and detail-oriented** — hard to hire for because it requires both
- **Needs technical credibility** but may resist hard technical interviews for a mostly-management role

The people who excel: "Capable engineers who care deeply about their teams and prefer to stay out of the spotlight in favor of creating high-performing organizations. They're interested in the complexities of getting people to work together effectively."

> **[Interview Angle: "Do You Want to Be a VP of Engineering?"]**
>
> Fournier's description is a self-assessment tool:
> - Do you enjoy making engineering processes more efficient? ✓ VP path
> - Do you like having a broad view of work and prioritizing it? ✓ VP path
> - Are you fascinated by organizational structure? ✓ VP path
> - Are you good at partnering with product managers? ✓ VP path
> - Would you rather sit in a roadmap-planning meeting than an architecture review? ✓ VP path
>
> For SRE leaders specifically: the VP of Engineering path often means expanding beyond SRE into broader engineering leadership. The skills transfer well — operational thinking, systems debugging, cross-team coordination — but the scope change is significant.

---

## What's a CTO?

Fournier is blunt: **"CTO is not an engineering role... not the top of the technical ladder... not the natural progression engineers should strive to achieve."**

Her definition: **"The CTO should be the strategic technical executive the company needs in its current stage of evolution."**

Key elements:
- **"An executive first, a technologist second."** Must care about and understand the business.
- Must have a seat at the executive table and understand business challenges
- Identifies where "technology can be used to create new or bigger lines of business"
- Must "protect the technology team from becoming a pure execution arm for ideas"

Fournier warns about CTOs who give up all management responsibility: **"If you give up management, you're giving up the most important power you ever had over the business strategy."** A CTO without direct reports and without management authority is "at best at the mercy of influence... at worst a figurehead."

> **[Insight]** Fournier's most controversial take: the CTO who has no reports is powerless. This challenges the common "CTO as chief architect" model. Her argument is structural: without the ability to allocate people to problems, you can only influence, not direct. And influence without any structural power is fragile — it works only as long as everyone agrees with you. The moment there's a conflict between what you think is important technically and what a VP thinks is important organizationally, the VP wins because they control the people.

> **[SRE Lens: The SRE Leadership Analog]**
>
> The CTO vs. VP tension maps directly to a common SRE organizational question: should the most senior SRE leader be a "Chief Reliability Officer" (strategic, influencing) or a "VP of SRE" (managing, directing)?
>
> Fournier's framework suggests: without management authority over SRE teams, a strategic reliability leader has influence but no power. When a product VP says "ship now, fix reliability later," the CRO can argue but the VP controls the engineers. The VP of SRE who manages the SRE team can allocate people to the reliability work regardless.
>
> **For your career:** If you want to shape reliability strategy for an organization, make sure you have the management structure to back it up. Strategy without execution authority is just advice.

---

## Ask the CTO: Where Do I Fit?

Fournier offers a decision framework for CTO vs. VP of Engineering:

**CTO indicators:** Want to cofound, oversee architecture, understand business deeply, do external events/speaking, manage senior ICs, be willing to manage senior managers and engineers.

**VP indicators:** Enjoy managing people, enjoy process efficiency, like broad view and prioritizing work, fascinated by org structure, good at product partnership, willing to trade technical depth for organizational effectiveness.

Her advisor's wisdom: **"Wanting to be a CTO is like wanting to be married. Remember that it's not just the title, it's also the company and the people that matter."**

> **[Mental Model: Title as Job vs. Title as Identity]**
>
> Fournier is gently warning against title-chasing. The CTO title at a 20-person startup means "technical cofounder doing everything." The CTO title at a 10,000-person company means "business executive who happens to be technical." Same title, completely different jobs.
>
> **For Senior EMs eyeing Director:** Don't chase the title. Chase the work. If you enjoy the WORK of organizational leadership — developing managers, setting strategy, navigating cross-functional dynamics — the title will follow. If you only want the title for the status or compensation, you'll be miserable in the role.

---

*Continued in [Part 2](ch08-notes-the-big-leagues-part2.md): Changing priorities, setting strategy, delivering bad news.*
