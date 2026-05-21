# Chapter 9: Dual Reporting

> **High Output Management** — Andrew S. Grove
> *Matrix Management, Peer Groups, and the Multi-Plane Organization*

Chapter 8 established that hybrid organizations are inevitable. Chapter 9 explains the *mechanism* that makes them work: **dual reporting** — the practice of having people report to two supervisors simultaneously, one providing mission-oriented direction and another providing functional/technical supervision. Grove traces Intel's accidental discovery of this practice through the mundane question of "who should plant security report to?" and extends it to the multi-plane organizational model that enables know-how managers to multiply their leverage.

The chapter also introduces **peer group decision-making**, **corporate culture as a coordination mechanism**, and **transitory teams** — all of which are essential to the functioning of modern tech organizations.

## Table of Contents

- [The Origin: Where Should Plant Security Report?](#the-origin-where-should-plant-security-report)
- [Why Dual Reporting Is Necessary](#why-dual-reporting-is-necessary)
- [Peer Groups as Supervisors](#peer-groups-as-supervisors)
- [Trust and Corporate Culture](#trust-and-corporate-culture)
- [Making the Hybrid Work: The Controller Example](#making-the-hybrid-work-the-controller-example)
- [The Two-Plane (Multi-Plane) Organization](#the-two-plane-multi-plane-organization)
- [Transitory Teams](#transitory-teams)

**Block types:** [Core Concept] [Senior EM Application] [SRE Lens] [Modern Lens] [Anti-Pattern] [Mental Model] [Practical Toolkit]

---

## The Origin: Where Should Plant Security Report?

Grove tells the origin story: at a staff meeting, Intel struggled to decide who should supervise security personnel at remote plants.

**Option A — report to the local plant manager:** He's physically present and can monitor daily performance. But he's an engineer who knows nothing about security standards.

**Option B — report to the corporate security manager at HQ:** He's the expert who sets standards and hired them. But he's not at the plant and wouldn't know if they showed up late.

The solution: **report jointly to both.** The corporate security manager specifies *how* the job should be done (functional supervision). The local plant manager monitors *how well* it's being performed day-to-day (mission-oriented supervision).

> *"Could an employee in fact have two bosses? The answer was a tentative 'yes,' and the culture of joint reporting relationships, dual reporting, was born. It was a slow, laborious birth."*

---

## Why Dual Reporting Is Necessary

Grove traces why single reporting inevitably fails in large organizations. A superstar salesman gets promoted to sales manager, then regional manager (now supervising application engineers he doesn't understand technically), then general manager (now supervising manufacturing with zero manufacturing background).

The general manager can supervise the *general* aspects of his manufacturing manager's job, but has no competence to evaluate the *technical* work. Yet going fully functional (having all manufacturing managers report to a senior manufacturing executive) destroys the mission-oriented unit's ability to coordinate across functions.

> *"We want the immediacy and the operating priorities coming from the general manager as well as a technical supervisory relationship. The solution is dual reporting."*

> **[SRE Lens: The Embedded SRE's Dual Report Is Exactly This]**
>
> The embedded SRE model is a textbook application of Grove's dual reporting:
>
> | Supervisor | What They Provide | Grove's Term |
> |-----------|-------------------|-------------|
> | **Product team's EM** (mission-oriented) | Day-to-day priorities, sprint planning, team dynamics, product context | Mission-oriented supervision |
> | **SRE manager / SRE guild lead** (functional) | Technical standards, SRE practices, career development, peer community, on-call standards | Functional/technical supervision |
>
> **Without dual reporting:** An embedded SRE who only reports to the product EM gradually loses SRE discipline — they become a general engineer who occasionally does reliability work. Standards drift across teams. No SRE career path exists.
>
> **With dual reporting:** The SRE maintains both product context (from the product EM) and technical excellence (from the SRE functional supervisor). This is exactly what Grove describes with the controller example: the division general manager provides mission priorities, the finance organization provides professional standards and career development.
>
> **The practical implementation:** The embedded SRE's performance review is co-authored by both supervisors. The product EM evaluates operational impact and team contribution. The SRE manager evaluates technical depth, adherence to reliability standards, and growth in the SRE craft. Neither alone has the full picture.

---

## Peer Groups as Supervisors

Grove describes a natural emergence: manufacturing managers from different divisions, each reporting to general managers with non-manufacturing backgrounds, start meeting informally. They realize they share common technical problems. The informal meetings become regular. Eventually a formal council of manufacturing peers forms.

> *"In effect, they now have supervision that a general manager competent in manufacturing could have given them, but that supervision is being exercised by a* peer group."

This is dual reporting where one "supervisor" is actually a group of peers rather than a single individual.

> **[Core Concept: Voluntary Surrender of Individual Decision-Making]**
>
> For peer groups to function as supervisors, individual members must accept constraints on their autonomy:
>
> *"Being a member means you no longer have complete freedom of individual action, because you must go along with the decisions of your peers in most instances."*
>
> Grove's vacation analogy: traveling with another couple means less individual freedom but more fun. Similarly, joining a peer coordination group means accepting peer decisions in exchange for better outcomes that no individual could achieve alone.
>
> **For SRE:** SRE guilds, architecture review boards, and reliability councils all work this way. When the SRE guild decides on a standard monitoring stack, individual team leads give up the freedom to choose their own tools in exchange for consistency, shared expertise, and reduced maintenance burden. The voluntary surrender only works if the peer group produces better outcomes than individual action — otherwise, members will defect.

---

## Trust and Corporate Culture

> *"Trust in no way relates to an organizational principle but is instead an aspect of the corporate culture."*

Dual reporting introduces ambiguity — which most people dislike. Making it work requires **cultural trust**: confidence that the system, despite its ambiguity, produces fair outcomes and that peers and supervisors will act in good faith.

> *"It's not because Intel loved ambiguity that we became a hybrid organization. We have tried everything else, and while other models may have been less ambiguous, they simply didn't work. Hybrid organizations and the accompanying dual reporting principle, like a democracy, are not great in and of themselves. They just happen to be the best way for any business to be organized."*

> **[Anti-Pattern: Dual Reporting Without Cultural Trust]**
>
> Dual reporting degenerates when trust is absent:
>
> - **The "two bosses" complaint:** Without trust, employees feel pulled between competing demands and freeze. "My product EM wants me to ship features, my SRE manager wants me to fix reliability — who do I listen to?"
> - **Grade shopping:** The employee takes their problem to whichever supervisor is more likely to give the answer they want.
> - **Accountability vacuum:** When something goes wrong, each supervisor assumes the other was responsible. "I thought your side was handling that."
>
> **The fix is not to eliminate dual reporting** (which also eliminates the hybrid's benefits). The fix is to build the cultural trust that makes it work: clear expectation-setting between both supervisors, joint performance evaluation, and explicit protocols for resolving conflicts when the two supervisors disagree.

---

## Making the Hybrid Work: The Controller Example

Grove illustrates with an Intel controller who serves a business division:

- **Mission-oriented supervision (divisional GM):** Tells the controller which business problems to focus on, sets priorities based on division strategy
- **Functional supervision (finance organization):** Ensures the controller uses proper methods and practices, provides training, supervises technical quality, manages career progression within finance

The advertising example follows the same pattern: divisional marketing managers control their messaging (mission), but a peer coordinating body (chaired by the corporate merchandising manager) selects the agency, defines brand standards, and negotiates volume ad buys (functional).

> **[Modern Lens: Dual Reporting in Modern Tech — Everywhere, Even When Unnamed]**
>
> Dual reporting is pervasive in modern tech organizations, even when not called by that name:
>
> | Role | Mission-Oriented Report | Functional Report |
> |------|------------------------|-------------------|
> | **Embedded SRE** | Product team EM | SRE chapter/guild lead |
> | **Security engineer on a product team** | Product team EM | CISO / security org |
> | **Data engineer supporting a product** | Product analytics lead | Data engineering platform team |
> | **Design system engineer** | Product team using the components | Design systems team |
> | **Tech lead** | EM (people management, team priorities) | Staff/Principal engineer (technical direction, architecture) |
>
> The pattern is universal: whenever a specialist is embedded in a cross-functional team, dual reporting exists implicitly. The question is whether it's *managed* (clear expectations from both sides) or *accidental* (confusion, conflicting priorities, no one owns career development).

---

## The Two-Plane (Multi-Plane) Organization

Grove introduces a powerful mental model: people operate on multiple organizational planes simultaneously. Cindy, the process engineer, works 80% of her time in her plant (Plane 1: operating hierarchy) and 20% in a cross-plant coordinating group (Plane 2: coordination hierarchy).

These planes have separate org charts, separate hierarchies, and sometimes *reversed* authority relationships. Grove gives a personal example: as Intel's president, he serves on a strategic planning group chaired by a division controller. In the operating plane, he outranks the controller. In the planning plane, the controller leads him.

> *"The multi-plane organization enables me to serve as a foot soldier rather than as a general when appropriate and useful."*

**The leverage multiplication:** Cindy's knowledge in Plane 1 affects one plant. Through Plane 2 (the coordinating group), it affects ALL plants. The two-plane structure is how know-how managers multiply their leverage across the organization.

> **[Senior EM Application: Your Planes]**
>
> As a Senior EM, you likely operate on 3-4 planes:
>
> | Plane | Your Role | Your "Supervisor" | Your Leverage |
> |-------|----------|-------------------|---------------|
> | **Plane 1: Operating** | Manager of 2-4 SRE/engineering teams | Your Director | Direct supervision of your teams |
> | **Plane 2: Architecture** | Member of architecture review board | Board chair (often a Principal Engineer) | Influence on cross-org technical decisions |
> | **Plane 3: SRE Guild** | Chapter lead or active member | Guild lead (may be your peer or junior!) | Setting reliability standards across all product teams |
> | **Plane 4: Incident Response** | Escalation point during P1 incidents | Incident commander (could be anyone on rotation) | Cross-org coordination during crises |
>
> Each plane has its own hierarchy, and your authority is different in each. In Plane 1, you're the leader. In Plane 4, the IC leads and you're a contributor. This flexibility is what Grove says makes organizations work — *if* you accept the ambiguity.

---

## Transitory Teams

Grove closes by noting that many multi-plane groups are **temporary** — task forces, working groups, and informal problem-solving collectives that form for a purpose and dissolve when it's accomplished.

> *"The more varied the nature of the problems we face and the more rapidly things change around us, the more we have to rely on such specially composed* transitory teams *to cope with matters."*

In fast-moving industries (like semiconductors, like software): *"we can't possibly shift formal organization fast enough to keep up with the pace of advancing technology."*

The skills needed — dual reporting, peer group decision-making — are the same whether the group is permanent or transitory. And the binding force is **cultural values as a mode of control** — the topic of Chapter 10.

> **[SRE Lens: Incident Response Teams Are Transitory Teams]**
>
> The purest transitory team in SRE is the **incident response team**: assembled ad hoc from whoever is needed (on-call, subject-matter experts, incident commander), works intensely on a specific problem, and dissolves when the incident is resolved. It operates on a different plane from the operating org, has its own hierarchy (IC leads, regardless of org-chart seniority), and requires exactly the dual-reporting skills Grove describes.
>
> Other SRE transitory teams:
> - **Migration task force** — assembled to execute a specific platform migration, dissolved when complete
> - **Reliability improvement sprint** — cross-team engineers pulled together for a focused reliability push, returned to their teams after
> - **Post-incident review group** — assembled for a deep-dive investigation, dissolved after the report is published
> - **Vendor evaluation team** — assembled to evaluate and select a new observability/monitoring tool, dissolved after the decision
>
> Grove's insight: the *formal* org chart can't change fast enough to handle these needs. Transitory teams are the fast, flexible response mechanism that operates alongside the formal structure.

---

**Chapter 9 establishes:** Dual reporting is the mechanism that makes hybrid organizations work. People can (and should) report to both a mission-oriented supervisor and a functional supervisor. Peer groups can serve as functional supervisors. Multi-plane organizations let people operate in different roles and hierarchies simultaneously. Transitory teams handle fast-changing problems that formal structures can't keep up with. All of it requires trust and shared corporate culture.

**Next: Chapter 10 — Modes of Control, where Grove addresses what governs behavior in organizations when formal rules aren't enough.**
