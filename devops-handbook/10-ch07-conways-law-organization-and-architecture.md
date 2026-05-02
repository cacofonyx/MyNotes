# Chapter 7: How to Design Our Organization and Architecture with Conway's Law in Mind

> **Part II -- Where to Start**

This chapter addresses one of the most consequential decisions in any DevOps transformation: how to organize teams and structure architecture so that they reinforce -- rather than undermine -- fast flow. Using Conway's Law as the governing principle, it demonstrates that organizational structure and software architecture are mirror images of each other. The chapter walks through organizational archetypes, the pathologies of over-functional orientation, the benefits of market-oriented teams, the importance of loosely coupled architectures, and the two-pizza team model. Two substantial case studies (Etsy's Sprouter and Target's API Enablement) illustrate how Conway's Law plays out in practice.

## Table of Contents

- [Conway's Law at Etsy (Sprouter)](#conways-law-at-etsy-sprouter)
- [Organizational Archetypes](#organizational-archetypes)
- [Problems Often Caused by Overly Functional Orientation ("Optimizing for Cost")](#problems-often-caused-by-overly-functional-orientation-optimizing-for-cost)
- [Enable Market-Oriented Teams ("Optimizing for Speed")](#enable-market-oriented-teams-optimizing-for-speed)
- [Making Functional Orientation Work](#making-functional-orientation-work)
- [Testing, Operations, and Security as Everyone's Job Every Day](#testing-operations-and-security-as-everyones-job-every-day)
- [Enable Every Team Member to Be a Generalist](#enable-every-team-member-to-be-a-generalist)
- [Fund Not Projects but Services and Products](#fund-not-projects-but-services-and-products)
- [Design Team Boundaries in Accordance with Conway's Law](#design-team-boundaries-in-accordance-with-conways-law)
- [Create Loosely Coupled Architectures to Enable Developer Productivity and Safety](#create-loosely-coupled-architectures-to-enable-developer-productivity-and-safety)
- [Keep Team Sizes Small (the "Two-Pizza Team" Rule)](#keep-team-sizes-small-the-two-pizza-team-rule)
  - [Case Study: Continuous Learning -- Team Topologies](#case-study-continuous-learning--team-topologies)
  - [Case Study: API Enablement at Target (2015)](#case-study-api-enablement-at-target-2015)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Organization and Architecture Design](#how-generative-ai-is-reshaping-organization-and-architecture-design)

---

## Conway's Law at Etsy (Sprouter)

The chapter opens with the origin and definition of Conway's Law, then immediately illustrates it through a detailed case study from Etsy.

> **[Deep Dive: Conway's Law -- Definition and Origin]**
>
> **Dr. Melvin Conway** performed a famous experiment in 1968 with a contract research organization of eight people commissioned to produce a COBOL and an ALGOL compiler. Five people were assigned to COBOL and three to ALGOL. The resulting COBOL compiler ran in five phases; the ALGOL compiler ran in three.
>
> Conway's Law states:
>
> *"Organizations which design systems ... are constrained to produce designs which are copies of the communication structures of these organizations. ... The larger an organization is, the less flexibility it has and the more pronounced the phenomenon."* -- Dr. Melvin Conway (1968)
>
> **Eric S. Raymond** crafted the now more famous simplified version in his Jargon File:
>
> *"The organization of the software and the organization of the software team will be congruent; commonly stated as 'if you have four groups working on a compiler, you'll get a 4-pass compiler.'"*
>
> The key implication: how we organize our teams has a **powerful effect on the software we produce** and our resulting architectural and production outcomes. Done poorly, Conway's Law creates tightly coupled teams that are all waiting on each other, where even small changes create potentially global, catastrophic consequences. Done well, it enables teams to work safely and independently.

**The Etsy Sprouter Story:**

Etsy's DevOps journey began in 2009. Their 2014 revenue was nearly $200 million, and the company had a successful IPO in 2015. The story centers on a technology called **Sprouter** (short for "stored procedure router"), originally developed in 2007.

- **What Sprouter was:** Sprouter sat between Etsy's front-end PHP application and its Postgres database, centralizing database access and hiding the database implementation from the application layer. It was designed to let developers write PHP while DBAs wrote SQL in Postgres, with Sprouter bridging the gap.

- **The problem it created:** Any new business functionality required the DBAs to write a new stored procedure. As Ross Snyder, a senior engineer at Etsy, described at Surge 2011: *"Every time developers wanted to add new functionality, they would need something from the DBAs, which often required them to wade through a ton of bureaucracy."*

  This meant developers had a **dependency on the DBA team** for any feature work. Work sat in queues, required meetings and coordination, and lead times ballooned. Sprouter created tight coupling between teams.

  Worse, stored procedures were also tightly coupled to Sprouter itself -- any stored procedure change required a Sprouter change. Sprouter became an ever-larger **single point of failure**. Snyder explained that almost every deployment caused a mini-outage.

- **Conway's Law explains both the problem and the solution:** Etsy initially had two teams (developers and DBAs) responsible for two architectural layers (application logic and stored procedures). Two teams, two layers -- as Conway's Law predicts. But Sprouter added a **third** layer, meaning that when business rules changed, three layers now needed updating (application, stored procedures, and Sprouter), requiring coordination across what effectively became three teams. The 2019 *State of DevOps Report* confirms that such coordination challenges increase lead times and cause reliability problems.

- **The fix:** In spring 2009, new CTO Chad Dickerson kicked off "the great Etsy cultural transformation," including a two-year effort to eliminate Sprouter. The team moved all business logic from the database layer into the application layer. They created a small team that wrote a **PHP ORM (object-relational mapping) layer**, enabling front-end developers to make calls directly to the database. This reduced the number of teams required to change business logic from **three teams down to one**.

  *"We started using the ORM for any new areas of the site and migrated small parts of our site from Sprouter to the ORM over time. It took us two years to migrate the entire site off of Sprouter."* -- Ross Snyder

- **Results:** Eliminating Sprouter removed the multi-team coordination overhead, decreased handoffs, significantly increased deployment speed and success, and improved site stability. Small teams could independently develop and deploy code. Developer productivity increased. Sprouter was finally removed from production and version control repositories, prompting Snyder to say: *"Wow, it felt good."*

> **[Insight]** The Etsy Sprouter story is a textbook illustration of how well-intentioned architectural decisions can create organizational dysfunction when Conway's Law is not considered. Sprouter was designed to help -- to decouple developers from database complexity. But by adding a third architectural layer, it added a third organizational dependency, turning a two-team coordination problem into a three-team coordination problem. The fix was not a reorganization of people but a simplification of architecture -- the ORM reduced the architectural layers, which automatically reduced the organizational coupling. This is the core lesson: architecture and organization are two sides of the same coin. You can intervene on either side, but the other will follow.

---

## Organizational Archetypes

The chapter introduces three primary types of organizational structures from the field of decision sciences (as defined by Dr. Roberto Fernandez):

| Archetype | Optimizes For | Structure | Characteristics |
|-----------|--------------|-----------|----------------|
| **Functional** | Expertise, division of labor, reducing cost | Tall hierarchical structures; people grouped by specialty | Centralizes expertise; enables career growth and skill development. Prevailing method for Operations (server admins, network admins, DBAs each in separate groups). |
| **Matrix** | Attempting to combine functional and market | Complex; individual contributors may report to two or more managers | Often achieves neither functional nor market goals. Frequently results in complicated reporting structures. |
| **Market** | Responding quickly to customer needs | Flat; composed of multiple cross-functional disciplines | May lead to redundancies. Each service team is simultaneously responsible for feature delivery and service support. Used by Amazon, Netflix. |

> **[Deep Dive: The Three Organizational Archetypes]**
>
> **Functional orientation** is the traditional IT model: server admins in one group, network admins in another, DBAs in a third. It optimizes for expertise and cost reduction through specialization. The downside is that any cross-cutting work (like a deployment) requires tickets, handoffs, and coordination across multiple groups.
>
> **Matrix orientation** attempts to get the best of both worlds by overlaying project/product lines on top of functional departments. In practice, it often creates confusion: people report to multiple managers, priorities conflict, and accountability is diffused. The book notes that many who work in or manage matrix organizations observe that they "often result in complicated organizational structures... sometimes achieving neither the goals of functional or market orientation."
>
> **Market orientation** organizes around the customer and the product. Teams are cross-functional, containing all the skills needed to deliver end-to-end value. This is how Amazon and Netflix operate -- each service team owns feature delivery AND service support. The tradeoff is potential redundancy (multiple teams may each have their own DBA, for instance), but the speed and autonomy gains typically outweigh the cost.

> **[2024+ Context: Team Topologies' Four Team Types]**
>
> Matthew Skelton and Manuel Pais's *Team Topologies* (2019) refined the market-oriented model into a more precise vocabulary, which is directly referenced later in this chapter:
>
> - **Stream-aligned teams:** The primary value-delivering unit. Owns a full slice of the business domain end-to-end. Analogous to the market-oriented team described here.
> - **Platform teams:** Build and maintain the self-service infrastructure and tooling that stream-aligned teams consume. Reduces cognitive load on stream-aligned teams.
> - **Enabling teams:** Contain specialists who help other teams acquire new capabilities (e.g., a DevOps Center of Excellence helping teams adopt CI/CD).
> - **Complicated-subsystem teams:** Own a subsystem so technically complex it requires deep specialist knowledge (e.g., a video codec team, a machine learning model team).
>
> The three **interaction modes** between teams are equally important:
> - **Collaboration:** Two teams work closely together for a defined period (high communication, temporary).
> - **X-as-a-Service:** One team provides a service that another consumes via an API or platform (low communication, scalable).
> - **Facilitating:** One team (usually an enabling team) helps another team learn or adopt a new capability.
>
> The **Inverse Conway Maneuver** -- deliberately designing your team structure to produce the architecture you want -- is the practical application of Conway's Law. Instead of letting your org chart accidentally dictate your architecture, you intentionally organize teams around the desired architectural boundaries. DORA's 2023 and 2024 research validates this: teams with low coordination overhead and clear ownership boundaries consistently show superior delivery performance.

---

## Problems Often Caused by Overly Functional Orientation ("Optimizing for Cost")

In traditional IT Operations organizations, functional orientation means teams organized by specialty: DBAs in one group, network admins in another, server admins in a third, and so on.

**Consequences:**

- **Long lead times:** Complex activities like large deployments require opening tickets with multiple groups and coordinating work handoffs. Work sits in long queues at every step.
- **Loss of context and motivation:** The person performing the work often has little visibility into how their work relates to value stream goals. As the book puts it, they think: *"I'm just configuring servers because someone told me to."* This places workers in a "creativity and motivation vacuum."
- **Competing priorities across value streams:** When each functional area serves multiple Development teams, all competing for scarce cycles, issues must be escalated to managers, directors, and eventually executives who can prioritize work against global organizational goals. These decisions must cascade back down to change local priorities -- slowing everyone else.
- **Net result of universal expediting:** When every team expedites their work, *every project ends up moving at the same slow crawl.*
- **Poor handoffs, rework, quality issues, bottlenecks, and delays:** The gridlock impedes important organizational goals, which often far outweigh the desire to reduce costs.

The book notes that centralized QA and Infosec functions face the same problem: they may work well enough for infrequent releases, but as deployment frequency increases, functionally oriented organizations have difficulty keeping up, especially when their work is manual.

> **[Insight]** The chapter's observation that "when every team expedites their work, every project ends up moving at the same slow crawl" is a direct consequence of Little's Law (WIP / Throughput = Lead Time). When every project is "priority one," nothing is truly prioritized. The WIP of the shared functional teams explodes, and lead times grow proportionally. The solution is not better prioritization but structural change: either embed the functional capability into the product team (market orientation) or provide it as a self-service platform. Both approaches eliminate the queue.

---

## Enable Market-Oriented Teams ("Optimizing for Speed")

To achieve DevOps outcomes, the book recommends reducing functional orientation and enabling market orientation so that many small teams can work **safely and independently**, quickly delivering value to the customer.

**In the extreme form:**
Market-oriented teams are responsible for the full lifecycle of their service -- feature development, testing, security, deployment, and production support -- from idea conception to retirement. They are cross-functional and independent, able to:
- Design and run user experiments
- Build and deliver new features
- Deploy and run their service in production
- Fix defects without manual dependencies on other teams

Amazon and Netflix use this model. Amazon touts it as one of the primary reasons behind their ability to move fast even as they grow.

**How to get there without a "big bang" reorg:**
The book explicitly advises against large, top-down reorganizations, which create disruption, fear, and paralysis. Instead:

1. **Embed functional engineers** (Ops, QA, Infosec) into each service team, OR
2. **Create a platform organization** that provides an automated technology platform where service teams can self-serve everything they need to test, deploy, monitor, and manage their services.

This enables each service team to deliver value without opening tickets with IT Operations, QA, or Infosec.

**Research support:** DORA's 2018 and 2019 *State of DevOps Reports* found that teams see superior performance in speed and stability when functional work like database change management, QA, and Infosec is integrated throughout the software delivery process.

![Figure 7.1: Functional vs. Market Orientation](../images/Fig7-1.jpg)
*Left: Functional orientation -- all work flows through centralized IT Operations. Right: Market orientation -- all product teams can deploy their loosely coupled components self-service into production. Source: Humble, Molesky, and O'Reilly, Lean Enterprise.*

> **[Deep Dive: The Inverse Conway Maneuver]**
>
> The concept of deliberately organizing teams to produce the desired architecture -- rather than letting accidental organizational structure dictate architecture -- is known as the **Inverse Conway Maneuver** (a term popularized by Thoughtworks' Technology Radar and expanded in *Team Topologies*).
>
> The logic is:
> 1. Conway's Law says your architecture will mirror your organization.
> 2. Therefore, if you want a particular architecture (e.g., loosely coupled microservices), you should organize your teams to mirror that architecture (e.g., small, autonomous teams each owning one service).
> 3. If you reorganize teams without changing architecture, or change architecture without reorganizing teams, you will create friction -- the two will pull toward alignment eventually, and the adjustment period will be painful.
>
> **Practical steps:**
> - Identify the desired architectural boundaries (bounded contexts, service boundaries).
> - Organize teams so that each team owns one or a small number of bounded contexts.
> - Ensure teams have all the skills they need to deliver end-to-end within their boundary.
> - Provide shared capabilities (CI/CD, observability, infrastructure) via a platform team rather than a functional silo.
>
> This is the organizing principle behind Amazon's two-pizza teams, Netflix's full-cycle developers, and Spotify's squads. It is not just a nice idea -- DORA research consistently shows that loosely coupled teams with clear ownership deliver better outcomes.

> **[2024+ Context: Platform Engineering]**
>
> The "platform organization" option described in this chapter has matured into the **Platform Engineering** movement. Rather than each product team reinventing deployment pipelines, observability, and infrastructure management, a dedicated platform team builds an **Internal Developer Platform (IDP)** that product teams consume via self-service.
>
> Key developments since the book's publication:
> - **Backstage** (Spotify, open-sourced 2020) became the de facto developer portal framework.
> - **CNCF Platforms White Paper** (2023) defined platform engineering principles.
> - **DORA 2023 and 2024 reports** found that well-built internal platforms correlate with higher delivery performance and lower burnout.
> - **Gartner** predicted that by 2026, 80% of software engineering organizations will establish platform teams.
>
> The platform team model resolves a tension in the market-oriented approach: not every product team can (or should) become expert in Kubernetes, observability, security scanning, and CI/CD. The platform team absorbs that cognitive load by providing golden paths -- opinionated, pre-configured workflows that embed best practices. Teams get the autonomy of market orientation with the expertise benefits of functional orientation.

---

## Making Functional Orientation Work

The chapter offers an important counterpoint: **it is possible to create effective, high-velocity organizations with functional orientation.** Cross-functional, market-oriented teams are one path to fast flow and reliability, but they are not the only path.

**Requirements for functional orientation to work:**
- Everyone in the value stream views customer and organizational outcomes as a **shared goal**, regardless of where they sit in the org chart.
- Service teams get what they need from Operations **reliably and quickly** (ideally on demand), and vice versa.
- A **high-trust culture** enables all departments to work together effectively.
- All work is **transparently prioritized** with sufficient **slack** in the system for high-priority work to be completed quickly.
- **Automated self-service platforms** build quality into the products everyone is building.

**Examples:** Many of the most admired DevOps organizations retain functional orientation of Operations, including **Etsy, Google, and GitHub**.

**The "Second Toyota Paradox":**

In the Lean manufacturing movement of the 1980s, researchers were puzzled by Toyota's functional orientation, which was at odds with the best practice of cross-functional, market-oriented teams. This was called "the second Toyota paradox."

Mike Rother wrote in *Toyota Kata*:

> *"As tempting as it seems, one cannot reorganize your way to continuous improvement and adaptiveness. What is decisive is not the form of the organization, but how people act and react. The roots of Toyota's success lie not in its organizational structures, but in developing capability and habits in its people. It surprises many people, in fact, to find that Toyota is largely organized in a traditional, functional-department style."*

> **[Insight]** This section is a crucial corrective to the simplistic narrative of "functional = bad, market = good." The Toyota example shows that organizational structure is necessary but not sufficient -- **culture, habits, and capabilities** matter more than boxes on an org chart. Etsy, Google, and GitHub all retained functional Operations teams and still achieved elite DevOps performance. The common thread is not structure but trust, transparency, and automated self-service. An organization that reorganizes into cross-functional teams but retains a low-trust, siloed culture will not see improvement. Conversely, a functionally organized team with high trust and self-service platforms can move very fast. The implication for practitioners: before reorganizing, ask whether the problem is really the structure or whether it is the culture, the communication patterns, or the lack of automation.

---

## Testing, Operations, and Security as Everyone's Job Every Day

In high-performing organizations, **quality, availability, and security are not the responsibility of individual departments** -- they are part of everyone's job every day.

What this looks like in practice:
- The most urgent problem of the day might be deploying a customer feature, fixing a Sev 1 production incident, reviewing a fellow engineer's change, applying emergency security patches, or making improvements so fellow engineers are more productive.

**Jody Mulkey, CTO at Ticketmaster**, on shared goals between Dev and Ops:

> *"For almost 25 years, I used an American football metaphor to describe Dev and Ops. You know, Ops is defense, who keeps the other team from scoring, and Dev is offense, trying to score goals. And one day, I realized how flawed this metaphor was, because they never all play on the field at the same time. They're not actually on the same team!"*
>
> *"The analogy I use now is that Ops are the offensive linemen, and Dev are the 'skill' positions (like the quarterback and wide receivers) whose job it is to move the ball down the field -- the job of Ops is to help make sure Dev has enough time to properly execute the plays."*

**Facebook's "shared pain" example (2009):**

During enormous growth in 2009, Facebook experienced significant problems related to code deployments. There was chronic firefighting and long hours. Pedro Canahuati, their director of production engineering, described a meeting full of Ops engineers where someone asked all people not working on an incident to close their laptops -- **and no one could.**

The most significant change they made: **all Facebook engineers, engineering managers, and architects rotated through on-call duty** for the services they built. This gave everyone visceral feedback on the upstream architectural and coding decisions they made, creating an enormous positive impact on downstream outcomes.

> **[Insight]** The Facebook on-call rotation is one of the most powerful feedback mechanisms described in the book. It connects directly to the Second Way (Feedback, Chapter 3): when the person who writes the code also gets paged at 3 AM when it breaks, the feedback loop is immediate and visceral. This practice eliminates the moral hazard of the "throw it over the wall" model, where developers never experience the consequences of poor coding or architectural decisions. Google's SRE model takes this further: if a service generates too many operational incidents, the SRE team can hand the pager back to the development team until reliability improves. This creates a powerful incentive to write production-quality code from the start.

---

## Enable Every Team Member to Be a Generalist

In extreme functional orientation, departments of specialists (network admins, storage admins, etc.) operate as what Dr. Spear calls *"sovereign states."* Any complex operational activity requires multiple handoffs and queues between infrastructure areas, lengthening lead times.

**The countermeasure:** Enable and encourage every team member to be a **generalist** by providing opportunities to learn all the skills necessary to build and run the systems they are responsible for, and by regularly rotating people through different roles.

The chapter introduces three staffing models:

| Model | Depth | Breadth | Effect |
|-------|-------|---------|--------|
| **"I-shaped" (Specialist)** | Deep expertise in one area | Very few skills in other areas | Creates bottlenecks quickly; insensitive to downstream waste; prevents planning flexibility |
| **"T-shaped" (Generalist)** | Deep expertise in one area | Broad skills across many areas | Can step up to remove bottlenecks; sensitive to downstream waste; helps make planning flexible |
| **"E-shaped"** | Deep expertise in a few areas | Experience across many areas; proven execution skills; always innovating | Almost limitless potential |

*Source: Scott Prugh, "Continuous Delivery," ScaledAgileFramework.com*

**Scott Prugh (CSG International)** on the transformation to generalist teams:

> *"By cross-training and growing engineering skills, generalists can do orders of magnitude more work than their specialist counterparts, and it also improves our overall flow of work by removing queues and wait time."*

On pushback from traditional managers:

> *"Traditional managers will often object to hiring engineers with generalist skill sets, arguing that they are more expensive and that 'I can hire two server administrators for every multi-skilled operations engineer.'"* -- But the business benefits of enabling faster flow are overwhelming.

**Growth mindset connection:** The chapter references Dr. Carol Dweck's concept of **fixed mindset** vs. **growth mindset**. When we value people merely for their existing skills rather than for their ability to acquire and deploy new skills, we reinforce the fixed mindset. A learning organization requires people who are willing to learn.

**Jason Cox, Director of Systems Engineering at Disney:**

> *"Inside of Operations, we had to change our hiring practices. We looked for people who had 'curiosity, courage, and candor,' who were not only capable of being generalists but also renegades. ... We want to promote positive disruption so our business doesn't get stuck and can move into the future."*

> **[Insight]** The E-shaped model is particularly worth noting because it resolves the false dichotomy between specialist and generalist. In practice, the most effective engineers have deep expertise in two or three areas (say, distributed systems and database internals) combined with working knowledge across the full stack. This allows them to make architectural decisions that account for downstream impact, to step in and unblock teammates across domain boundaries, and to identify integration problems that pure specialists would miss. The chapter's emphasis on generalists is not about making everyone mediocre at everything -- it is about ensuring that deep expertise does not come at the cost of tunnel vision.

---

## Fund Not Projects but Services and Products

The chapter advocates for **stable service teams with ongoing funding** to execute their own strategy and road map, rather than the traditional project-based funding model.

**Traditional model problems:**
- Development and Test teams are assigned to a "project" and reassigned when it is completed and funding runs out.
- Developers cannot see the long-term consequences of their decisions (a form of missing feedback).
- The funding model only values and pays for the earliest stages of the software life cycle -- which is the **least expensive part** for successful products or services.

> *"Every new application is like a free puppy. It's not the upfront capital cost that kills you. ... It's the ongoing maintenance and support."* -- John Lauderbach, VP of Information Technology at Roche Bros. Supermarkets

**Product-based funding model goals:**
- Value the achievement of **organizational and customer outcomes** (revenue, customer lifetime value, adoption rate) with the minimum of output (effort, time, lines of code).
- Contrast with project metrics: whether completed within budget, time, and scope.

> **[Insight]** The shift from project to product funding is one of the most consequential organizational changes the book advocates, and it is deeply connected to Conway's Law. Project funding creates transient teams that dissolve after delivery, ensuring no one is around to deal with the operational consequences of their decisions. Product funding creates stable teams with long-term ownership, which naturally incentivizes building for operability, reliability, and maintainability. This echoes the "you build it, you run it" principle from Amazon. It also connects to the American Airlines case study in Chapter 1, where the shift to product-based funding (giving product teams a set budget and OKRs) was described as "a huge accelerator" in their DevOps journey.

---

## Design Team Boundaries in Accordance with Conway's Law

As organizations grow, maintaining effective communication and coordination becomes the largest challenge. Creating and maintaining shared understanding and mutual trust becomes even more important. The second edition specifically notes that **remote, hybrid, and distributed work configurations** -- with team members stretched across offices, homes, time zones, and sometimes contractual boundaries -- have become common.

**Anti-patterns** that create poor outcomes (side effects of Conway's Law):
- Splitting teams by function (e.g., developers and testers in different locations or outsourcing testers entirely)
- Splitting teams by architectural layer (e.g., separate application and database teams)

These configurations require significant communication and coordination but still result in rework, disagreements, poor handoffs, and people sitting idle waiting for someone else.

**The ideal:** Software architecture should enable small teams to be independently productive, sufficiently decoupled so that work can be done without excessive or unnecessary communication and coordination.

> **[2024+ Context: DORA Findings on Loosely Coupled Teams]**
>
> The DORA 2023 *State of DevOps Report* introduced explicit measurement of **team independence** and **coordination overhead**. Key findings:
> - Teams that could develop, test, and deploy their services **without requiring coordination with other teams** had significantly better delivery performance across all four DORA metrics.
> - High coordination overhead (needing to synchronize with multiple teams for releases) was one of the strongest predictors of poor performance.
> - The 2024 report reinforced this by finding that **clear team ownership of services** (knowing exactly who owns what) correlated with both faster delivery and lower burnout.
>
> These findings provide empirical backing for the chapter's argument: team boundaries should be drawn to minimize cross-team dependencies. Conway's Law is not just a theoretical observation -- it is a measurable predictor of delivery performance.

---

## Create Loosely Coupled Architectures to Enable Developer Productivity and Safety

**Tightly coupled architecture consequences:**
- Small changes can result in large-scale failures.
- Anyone working in one part of the system must constantly coordinate with everyone in other parts.
- Complex, bureaucratic change management processes.
- Testing requires integrating changes with hundreds or thousands of other developers, often in scarce integration test environments that take weeks to obtain.
- Result: long lead times (weeks or months) and low developer productivity.

**Loosely coupled architecture benefits:**
- Small teams of developers can independently implement, test, and deploy code into production safely and quickly.
- Developer productivity is maintained and improved.
- Deployment outcomes improve.

> **[Deep Dive: Loosely Coupled Architectures, SOA, and Bounded Contexts]**
>
> The chapter identifies two key properties of architectures that enable independent deployment:
>
> **1. Loosely coupled services:** Services can be updated in production independently, without having to update other services. Services must be decoupled from other services and -- just as importantly -- from **shared databases** (although they can share a database service, provided they don't share common schemas).
>
> **2. Bounded contexts** (from Eric J. Evans's *Domain-Driven Design*): Developers should be able to understand and update the code of a service without knowing anything about the internals of its peer services. Services interact strictly through **APIs** and don't share data structures, database schemata, or other internal representations of objects. Bounded contexts ensure services are compartmentalized with well-defined interfaces, enabling easier testing.
>
> These properties are found in **service-oriented architectures (SOAs)** (first described in the 1990s) and in **microservices** (which build upon SOA principles). The **12-factor app** is a popular set of patterns for modern web architecture based on these principles.
>
> **Randy Shoup**, former Engineering Director for Google App Engine:
>
> *"Organizations with these types of service-oriented architectures, such as Google and Amazon, have incredible flexibility and scalability. These organizations have tens of thousands of developers where small teams can still be incredibly productive."*

> **[Insight]** The emphasis on not sharing databases deserves special attention. In many legacy organizations, the database is the hidden coupling mechanism -- dozens of services read from and write to the same tables, creating invisible dependencies that make independent deployment impossible. When Service A adds a column to a shared table, Service B's queries may break. This is why the bounded context pattern insists on data encapsulation: each service owns its data and exposes it only through APIs. Migrating from shared databases to service-owned data stores is one of the hardest parts of any microservices transition, but it is essential for achieving the independent deployability that this chapter advocates. The Etsy Sprouter story at the beginning of the chapter is essentially a database coupling problem.

---

## Keep Team Sizes Small (the "Two-Pizza Team" Rule)

Conway's Law encourages keeping team sizes small to reduce inter-team communication and keep each team's domain small and bounded.

**Amazon's two-pizza rule:** A team should only be as large as can be fed with two pizzas -- usually **five to ten people**. This was part of Amazon's transformation away from a monolithic codebase in 2002.

**Four important effects of small team size:**

1. **Clear, shared understanding:** As teams get larger, the communication required scales combinatorially. Small teams maintain shared mental models of their system.

2. **Limited growth rate:** By limiting team size, you limit the rate at which the system can evolve, helping the team maintain shared understanding.

3. **Decentralized power and autonomy:** Each two-pizza team (2PT) is as autonomous as possible. The team lead, working with executives, decides on a key business metric (the **fitness function**), which becomes the team's evaluation criteria. The team then acts autonomously to maximize that metric. (Netflix culture calls this *"highly aligned, loosely coupled."*)

4. **Leadership development:** Leading a two-pizza team gives employees leadership experience in an environment where failure does not have catastrophic consequences.

**Werner Vogels, Amazon CTO**, explained the advantages to Larry Dignan of Baseline (2005):

> *"Small teams are fast ... and don't get bogged down in so-called administrivia. ... Each group assigned to a particular business is completely responsible for it. ... The team scopes the fix, designs it, builds it, implements it and monitors its ongoing use. This way, technology programmers and architects get direct feedback from the business people who use their code or applications -- in regular meetings and informal conversations."*

An essential element of Amazon's strategy was the **link between organizational structure (two-pizza team) and architectural approach (SOA)**. The team structure and the architecture reinforced each other -- a deliberate application of Conway's Law.

---

### Case Study: Continuous Learning -- Team Topologies

In *Team Topologies: Organizing Business and Technology Teams for Fast Flow*, Matthew Skelton and Manuel Pais present team and organizational patterns to optimize software delivery. Their central theme aligns with this chapter: **good team designs reinforce good software delivery, and good software delivery reinforces more effective teams.**

**Best practices for teams:**

- **Trust and communication take time.** It takes at least three months for team members to reach high performance. Keep teams together at least a year to benefit from their work together.
- **Just-right sizing.** Eight is an ideal number (similar to the two-pizza team). 150 is an upper limit (citing Dunbar's number -- the number of people with whom one can maintain stable social relationships, per British anthropologist Robin Dunbar, 1990s).
- **Communication can be expensive.** Within-team communication is good, but any time teams have demands or constraints on other teams, it leads to queues, context switching, and overhead.

**Four types of teams:**

| Team Type | Purpose |
|-----------|---------|
| **Stream-aligned teams** | End-to-end team owning the full value stream. Similar to market orientation. |
| **Platform teams** | Create and support reusable technology (infrastructure, content management) often used by stream-aligned teams. May be a third party. |
| **Enabling teams** | Contain experts who help other teams improve (e.g., Center of Excellence). |
| **Complicated-subsystem teams** | Own a subcomponent so complex it requires specialist knowledge. |

The authors also touch on other team types such as **SRE (site reliability engineer)** and **service experience** teams.

> **[2024+ Context: Team Topologies Adoption and Evolution]**
>
> Since its 2019 publication, *Team Topologies* has become the most widely adopted framework for organizing technology teams. Key developments:
>
> - **DORA 2023 report** explicitly cited Team Topologies concepts (stream-aligned teams, platform teams) as correlating with high performance.
> - **Cognitive load** -- a central concept in Team Topologies -- has been validated as a key factor in team effectiveness. Teams overwhelmed by the cognitive load of their domain (too many services, too many technologies, too complex a domain) show degraded performance regardless of how skilled the individuals are.
> - **Platform Engineering** has emerged as the operational realization of the "platform team" concept, with dedicated conferences (PlatformCon), a CNCF working group, and tools (Backstage, Port, Kratix) built around the model.
> - The concept of **team APIs** (explicit documentation of how to interact with a team, what they provide, what they expect) has gained traction as a way to make Conway's Law deliberate rather than accidental.

---

### Case Study: API Enablement at Target (2015)

**Context:** Target is the sixth-largest US retailer, spending over $1 billion on technology annually.

**The problem:** Heather Mickman, a former director of development for Target, described the starting point:

> *"In the bad old days, it used to take ten different teams to provision a server at Target, and when things broke, we tended to stop making changes to prevent further issues, which of course makes everything worse."*

Core data (inventory, pricing, stores) was locked in legacy systems and mainframes. Multiple sources of truth existed between e-commerce and physical stores, owned by different teams with different data structures and priorities.

> *"The result was that if a new development team wanted to build something for our guests, it would take three to six months to build the integrations to get the data they needed. Worse, it would take another three to six months to do the manual testing to make sure they didn't break anything critical because of how many custom point-to-point integrations we had in a very tightly coupled system. Having to manage the interactions with the twenty to thirty different teams, along with all their dependencies, required lots of project managers because of all the coordination and handoffs. It meant that development was spending all their time waiting in queues instead of delivering results and getting stuff done."* -- Heather Mickman

This long lead time jeopardized critical business goals, such as integrating the supply chain operations of Target's physical stores and their e-commerce site.

**The solution:** In 2012, Mickman led the **API Enablement team** to enable development teams to "deliver new capabilities in days instead of months." The goal: any engineering team inside Target could get and store the data they needed (products, stores, operating hours, location, whether there was a Starbucks on-site, etc.) through APIs.

**Team selection and approach:**

> *"Because our team also needed to deliver capabilities in days, not months, I needed a team who could do the work, not give it to contractors -- we wanted people with kickass engineering skills, not people who knew how to manage contracts. And to make sure our work wasn't sitting in queue, we needed to own the entire stack, which meant that we took over the Ops requirements as well. ... We brought in many new tools to support continuous integration and continuous delivery. And because we knew that if we succeeded, we would have to scale with extremely high growth, we brought in new tools such as the Cassandra database and Kafka message broker. When we asked for permission, we were told no, but we did it anyway because we knew we needed it."*

**Results:**

| Metric | Before | After |
|--------|--------|-------|
| Time to build integrations | 3-6 months | Days |
| New business capabilities enabled | -- | 53 (including Ship to Store, Gift Registry, Instacart and Pinterest integrations) |
| API calls per month (2014) | -- | 1.5 billion |
| API calls per month (2015) | -- | 17 billion |
| APIs available | -- | 90+ |
| Deployments per week | -- | 80 |
| Digital sales growth (2014 holiday) | -- | +42% |
| Digital sales growth (Q2 2015) | -- | +32% |
| Black Friday 2015 in-store pickup orders | -- | 280,000+ |
| Stores fulfilling e-commerce orders (2015 goal) | 100 | 450 of 1,800 |

> *"The API Enablement team shows what a team of passionate change agents can do. And it helped set us up for the next stage, which is to expand DevOps across the entire technology organization."* -- Heather Mickman

> **[Insight]** The Target case study is a near-perfect illustration of every concept in this chapter working together:
>
> - **Conway's Law:** Twenty to thirty teams with custom point-to-point integrations produced a tightly coupled system that mirrored the organizational complexity. The API Enablement team, by owning the entire stack, could move independently.
> - **Market orientation:** The team was cross-functional, owning development AND operations. They explicitly rejected the functional model ("we took over the Ops requirements").
> - **Loosely coupled architecture:** APIs replaced custom point-to-point integrations, decoupling producers from consumers. Pinterest integration became "very easy, because we just provided them our APIs."
> - **Product funding:** The team had an ongoing mission ("deliver new capabilities in days"), not a project with an end date.
> - **Generalists:** Mickman sought "kickass engineering skills," not contract managers.
> - **Organizational courage:** They adopted Cassandra and Kafka despite being told no. This highlights that structural change often requires deliberate defiance of existing policies that were optimized for a different era.

---

## Conclusion

The chapter concludes that through the Etsy and Target case studies, we can see how architecture and organizational design can dramatically improve outcomes:

- **Done incorrectly:** Conway's Law will ensure poor outcomes, preventing safety and agility.
- **Done well:** The organization enables developers to safely and independently develop, test, and deploy value to the customer.

The relationship between organization and architecture is bidirectional and self-reinforcing. Teams must be designed with Conway's Law in mind so that the natural tendency of organizations to produce architectures that mirror their communication structures works in their favor, not against them.

---

## How Generative AI Is Reshaping Organization and Architecture Design

> **[GenAI + Chapter 7 Concepts]** Conway's Law, organizational archetypes, loosely coupled architecture, and team sizing are all being reshaped by the rise of Generative AI. Here is a concept-by-concept analysis:

### GenAI and Conway's Law

| Concept | Traditional View | With GenAI |
|---------|-----------------|------------|
| **Team communication overhead** | Scales combinatorially with team size; keep teams small | AI assistants can summarize cross-team discussions, translate between domain vocabularies, and reduce the cost of coordination -- potentially allowing slightly larger effective team sizes |
| **Bounded contexts** | Developers must understand their service without knowing peer internals | AI-powered code navigation and explanation tools (Copilot, Cursor, Cody) let developers quickly understand unfamiliar codebases, partially reducing the cost of crossing context boundaries |
| **Architecture mirroring org structure** | Immutable law | AI-generated code may not "belong" to any team in the traditional sense. Organizations must decide: does AI-generated code follow the same ownership model? Who is on-call for AI-written services? |
| **Functional vs. market orientation** | Choose one and optimize | AI may make functional orientation more viable by reducing queue times (AI can auto-provision infrastructure, auto-review security, auto-generate tests), blurring the distinction between "embedded specialist" and "self-service platform" |

### GenAI and Loosely Coupled Architecture

- **API design:** AI tools can generate API contracts, suggest bounded context boundaries from existing codebases, and auto-detect coupling violations (e.g., services sharing database schemas).
- **Migration from monolith to microservices:** AI-assisted code analysis can identify module boundaries, suggest decomposition strategies, and even generate the interface code for newly extracted services. Tools like Amazon Q and Google's Gemini Code Assist are being applied to legacy modernization.
- **Risk:** AI-generated code may inadvertently increase coupling if prompts are not carefully scoped. An AI assistant asked to "add a feature" without architectural context may take the path of least resistance (e.g., directly querying another service's database rather than calling its API).

### GenAI and Team Design

- **"AI as team member":** Some organizations are experimenting with treating AI coding agents as virtual team members, raising questions about team sizing (does the two-pizza rule change when one "member" is an AI that never sleeps?) and about cognitive load (AI can reduce individual cognitive load but may increase it if code quality requires constant review).
- **Enabling generalists:** AI dramatically lowers the barrier to working across the stack. A backend engineer can use AI assistance to write competent frontend code, and vice versa. This accelerates the I-shaped to T-shaped to E-shaped progression the chapter advocates.
- **Platform engineering amplified:** AI-powered platforms can go beyond golden paths to provide intelligent, context-aware guidance -- suggesting not just "how to deploy" but "what to monitor, how to test, and what architectural patterns to follow" based on the specific service being built.

### Key Takeaway

Conway's Law remains fully operative in the age of AI. AI changes the *cost* of communication and coordination, but it does not change the fundamental principle that organizational structure and architecture mirror each other. Organizations adopting AI must be intentional about how AI-generated artifacts fit into their team ownership and architectural boundary models -- or Conway's Law will produce the same accidental coupling it always has.

**Further reading:**
- [Team Topologies -- Key Concepts](https://teamtopologies.com/key-concepts) -- the four team types and three interaction modes
- [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/) -- principles of platform engineering
- [Martin Fowler on Bounded Contexts](https://martinfowler.com/bliki/BoundedContext.html) -- canonical explanation of the DDD concept
- [Inverse Conway Maneuver (Thoughtworks)](https://www.thoughtworks.com/radar/techniques/inverse-conway-maneuver) -- original Radar entry
- [DORA State of DevOps Reports](https://dora.dev/research/) -- annual research on team structure and delivery performance
- [Backstage by Spotify](https://backstage.io/) -- open-source developer portal for platform engineering
- [Domain-Driven Design Reference (Eric Evans)](https://www.domainlanguage.com/ddd/reference/) -- bounded context patterns
