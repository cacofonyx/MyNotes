# Chapter 13: Architect for Low-Risk Releases

> **Part III -- The Technical Practices of Flow**

This chapter tackles the architecture dimension of DevOps, arguing that tightly coupled, monolithic architectures are the single largest structural barrier to safe, frequent deployments. It traces the evolutionary architecture journeys of Amazon, eBay, Blackboard, and others, presents the strangler fig application pattern as the primary migration strategy, and makes the case that architecture must evolve continuously to serve changing organizational goals. The DORA research data confirms that architecture is the largest contributor to continuous delivery capability.

## Table of Contents

- [Introduction: The Architectural Trap](#introduction-the-architectural-trap)
- [An Architecture that Enables Productivity, Testability, and Safety](#an-architecture-that-enables-productivity-testability-and-safety)
- [Architectural Archetypes: Monoliths vs. Microservices](#architectural-archetypes-monoliths-vs-microservices)
  - [Case Study: Evolutionary Architecture at Amazon (2002)](#case-study-evolutionary-architecture-at-amazon-2002)
- [Use the Strangler Fig Application Pattern to Safely Evolve Our Enterprise Architecture](#use-the-strangler-fig-application-pattern-to-safely-evolve-our-enterprise-architecture)
  - [Case Study: Strangler Fig Pattern at Blackboard Learn (2011)](#case-study-strangler-fig-pattern-at-blackboard-learn-2011)
  - [Case Study: Continuous Learning -- Architecture and DORA Research](#case-study-continuous-learning--architecture-and-dora-research)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Architectural Decisions for Low-Risk Releases](#how-generative-ai-is-reshaping-architectural-decisions-for-low-risk-releases)
  - [GenAI and Evolutionary Architecture](#genai-and-evolutionary-architecture)
  - [GenAI and the Strangler Fig Pattern](#genai-and-the-strangler-fig-pattern)
  - [GenAI and Microservices Operations](#genai-and-microservices-operations)
  - [The Meta-Question: Does AI Change the Architecture Principles, or Accelerate Them?](#the-meta-question-does-ai-change-the-architecture-principles-or-accelerate-them)

---

## Introduction: The Architectural Trap

The chapter opens with a powerful observation: **almost every well-known DevOps exemplar has had near-death experiences due to architectural problems.** LinkedIn, Google, eBay, Amazon, and Etsy all faced moments where their architecture nearly killed the organization before they were able to successfully migrate to something better.

This is framed as the principle of **evolutionary architecture**. Jez Humble observes that the architecture of "any successful product or organization will necessarily evolve over its life cycle."

Randy Shoup (Chief Engineer and Distinguished Architect at eBay 2004-2011, later at Google) provides a key quote:

> "Both eBay and Google are each on their fifth entire rewrite of their architecture from top to bottom." -- Randy Shoup

And the critical follow-up on hindsight:

> "Looking back with 20/20 hindsight, some technology [and architectural choices] look prescient and others look shortsighted. Each decision most likely best served the organizational goals at the time. If we had tried to implement the 1995 equivalent of micro-services out of the gate, we would have likely failed, collapsing under our own weight and probably taking the entire company with us." -- Randy Shoup

**eBay's full architectural evolution:**
1. Perl and files (v1, 1995)
2. C++ and Oracle (v2, 1997)
3. XSL and Java (v3, 2002)
4. Full-stack Java (v4, 2007)
5. Polyglot microservices (2013+)

**How eBay approached re-architecture:** When Shoup's team planned to move to full-stack Java in 2006, they did not attempt a full rewrite. They first ran a small pilot to prove they understood the problem, then sorted site pages by revenue produced and migrated highest-revenue areas first, stopping when the business return no longer justified the effort. This is textbook **evolutionary design**.

> **[Deep Dive: Evolutionary Architecture]**
>
> Evolutionary architecture is the idea that an architecture should be designed for change, not for permanence. The key principles:
>
> 1. **No architecture is "right" forever.** What serves you at 10 users will not serve you at 10 million. What helps you prototype fast will not help you deploy independently at scale.
> 2. **Fitness functions.** Neal Ford, Rebecca Parsons, and Patrick Kua formalized this in *Building Evolutionary Architectures* (2017): define automated "fitness functions" -- tests that evaluate whether the architecture still meets its goals (e.g., no circular dependencies, deployment independence, latency budgets). If the fitness function fails, the architecture needs to evolve.
> 3. **Incremental migration.** You never do a "big bang" rewrite. You migrate incrementally, proving each step with a pilot, measuring business value, and stopping when the return diminishes.
> 4. **The architecture serves the organization, not the other way around.** Architecture decisions should be driven by current organizational goals (time-to-market, scalability, team autonomy), not by theoretical purity.
>
> The eBay example is powerful because it shows five complete rewrites over ~20 years. Each was the "right" architecture for its era. The lesson is not "get it right the first time" but "build the muscle to evolve continuously."

**The symptoms of overly tight architecture** are described in detail:
- Every commit into trunk risks creating **global failures** (breaking everyone else's tests and functionality, or the entire site going down)
- Every small change requires **enormous communication and coordination** over days or weeks, plus approvals from any potentially affected group
- Deployments become problematic -- changes are batched together, complicating integration and testing, increasing failure likelihood
- Even small changes may require coordination with **hundreds or thousands** of developers, any of whom can create a catastrophic failure requiring weeks to fix
- The telltale quote: "My developers spend only 15% of their time coding -- the rest of their time is spent in meetings."
- A **self-reinforcing downward spiral**: fear of integration and deployment leads to deploying less frequently, which leads to larger batches, which leads to more risk, which leads to more fear

The chapter introduces the **Second Law of Architectural Thermodynamics** via Charles Betz (author of *Architecture and Patterns for IT*):

> "[IT project owners] are not held accountable for their contributions to overall system entropy." -- Charles Betz

In other words, reducing overall complexity and increasing productivity of all development teams is rarely the goal of any individual project. Each project optimizes locally, but the aggregate effect is increasing entropy and coupling.

> **[Insight]** The "15% coding time" symptom is one of the most powerful diagnostic signals in the chapter. If developers are spending the majority of their time in meetings, coordinating changes, and waiting for approvals rather than writing code, the root cause is almost always architectural, not organizational. You can restructure teams, improve meeting discipline, and add project managers -- but none of that addresses the underlying problem: changes in one area ripple unpredictably across the system, forcing coordination. The only real fix is architectural decoupling. This connects directly to Conway's Law (Chapter 7): the architecture constrains the org structure, and vice versa. You cannot have autonomous teams on a tightly coupled codebase.

> **[2024+ Context]** The "Second Law of Architectural Thermodynamics" has found a modern formalization in the concept of **architecture decision records (ADRs)** and **architectural fitness functions**. Organizations like Thoughtworks, Netflix, and Spotify now maintain explicit ADR logs and automated fitness functions (e.g., ArchUnit for Java, dependency-cruiser for JavaScript) that continuously test whether the architecture still meets its goals. The emergence of **modular monoliths** as a deliberate architectural choice (championed by Shopify and others) represents a nuanced response to the monolith-vs-microservices debate: you can get many of the modularity benefits without the operational complexity of distributed systems, provided you enforce module boundaries rigorously. This is essentially applying the "well-defined interfaces" principle from this chapter within a single deployable unit.

---

## An Architecture that Enables Productivity, Testability, and Safety

The chapter contrasts tightly coupled architecture (which impedes everyone) with **loosely coupled architecture with well-defined interfaces** that enforce how modules connect.

**Properties of the desired architecture:**
- Small, productive teams that can make small changes safely and independently
- Each service has a well-defined API
- Easier testing of services
- Creation of contracts and SLAs between teams
- Independent deployment

![Figure 13.1: Google Cloud Datastore](../images/Fig13-1.jpg)
*Source: Shoup, "From the Monolith to Micro-services."*

Randy Shoup describes how this works at Google:

> "This type of architecture has served Google extremely well -- for a service like Gmail, there's five or six other layers of services underneath it, each very focused on a very specific function. Each service is supported by a small team, who builds it and runs their functionality, with each group potentially making different technology choices. Another example is the Google Cloud Datastore service, which is one of the largest NoSQL services in the world -- and yet it is supported by a team of only about eight people, largely because it is based on layers upon layers of dependable services built upon each other." -- Randy Shoup

> "Organizations with these types of architectures, such as Google and Amazon, show how it can impact organizational structures, [creating] flexibility and scalability. These are both organizations with tens of thousands of developers, where small teams can still be incredibly productive." -- Randy Shoup

> **[Deep Dive: Bounded Contexts and Service Design]**
>
> The "well-defined interfaces" the chapter calls for have a precise vocabulary in Domain-Driven Design (DDD), which Eric Evans formalized in 2003. The key concept is the **bounded context**: a boundary within which a particular domain model is defined and applicable. Each bounded context has:
>
> - **Its own ubiquitous language** -- terms mean specific things within this context (e.g., "Order" means something different in the Fulfillment context vs. the Billing context)
> - **Explicit interfaces** at its boundaries -- context maps define how bounded contexts communicate (shared kernel, customer-supplier, anticorruption layer, etc.)
> - **Its own persistence** -- each bounded context owns its data and does not allow direct database access from outside
>
> The Google Cloud Datastore example (8 people supporting one of the largest NoSQL services in the world) works precisely because bounded contexts are enforced: each layer is a well-defined service with clear responsibilities and APIs. The team doesn't need to coordinate with hundreds of other teams because the boundaries are explicit and enforced.
>
> **Why this matters for DevOps:** If your service boundaries don't align with bounded contexts, you get "distributed monolith" -- all the operational complexity of microservices with none of the autonomy benefits. Changes still cascade across services because the domain boundaries are in the wrong places. Getting service boundaries right is arguably the hardest problem in microservices architecture.

> **[Insight]** The Google Cloud Datastore example -- one of the largest NoSQL services in the world supported by just eight people -- is the chapter's most striking data point. It demolishes the assumption that large-scale systems require large teams. The enabling factor is not superhuman engineers; it is layers of dependable, well-defined services that abstract away complexity. Each layer is a "standing on the shoulders of giants" moment. This is why platform engineering matters: the better the platform (shared infrastructure, common libraries, reliable lower-level services), the smaller the team needed at each higher level. Conversely, when every team has to build everything from scratch, team sizes balloon and coordination costs explode.

> **[2024+ Context]** The "layers upon layers of dependable services" pattern described here has evolved into what is now called **platform engineering**. The CNCF 2023 Platform Engineering Maturity Model describes a progression from ad-hoc shared infrastructure to fully self-service Internal Developer Platforms (IDPs). The key idea: platform teams build the reusable layers so that stream-aligned product teams can stay small and focused. Tools like Backstage (Spotify), Kratix, and Humanitec provide the scaffolding for building these platforms. The 8-person Google Cloud Datastore team is only possible because Google's internal platform (Borg, Bigtable, Spanner, etc.) handles infrastructure concerns. The lesson is not "use microservices" but "invest in platforms that allow small teams to operate large systems."

---

## Architectural Archetypes: Monoliths vs. Microservices

The chapter emphasizes that **monolithic architectures are not inherently bad** -- they are often the best choice early in a product life cycle.

> "There is no one perfect architecture for all products and all scales. Any architecture meets a particular set of goals or range of requirements and constraints, such as time to market, ease of developing functionality, scaling, etc. The functionality of any product or service will almost certainly evolve over time -- it should not be surprising that our architectural needs will change as well. What works at scale 1x rarely works at scale 10x or 100x." -- Randy Shoup

**Table 13.1: Architectural Archetypes**

| Archetype | Pros | Cons |
|-----------|------|------|
| **Monolithic v1** (all functionality in one application) | Simple at first; low interprocess latencies; single codebase, one deployment unit; resource efficient at small scales | Coordination overhead increases as team grows; poor enforcement of modularity; poor scaling; all-or-nothing deploy (downtime, failures); long build times |
| **Monolithic v2** (sets of monolithic tiers: front end, app server, database layer) | Simple at first; join queries are easy; single schema, deployment; resource efficient at small scales | Tendency for increased coupling over time; poor scaling and redundancy (all-or-nothing, vertical only); difficult to tune properly; all-or-nothing schema management |
| **Microservice** (modular, independent, graph relationship vs. tiers, isolated persistence) | Each unit is simple; independent scaling and performance; independent testing and deployment; can optimally tune performance (caching, replication, etc.) | Many cooperating units; many small repos; requires more sophisticated tooling and dependency management; network latencies |

The table makes clear that each archetype supports different evolutionary needs. A startup benefits from monolithic simplicity and speed. An organization with hundreds of teams benefits from microservice independence.

> **[Deep Dive: Microservices Architecture -- Benefits, Costs, and When to Use]**
>
> Microservices are not free. The chapter's table hints at the costs, but they deserve explicit treatment:
>
> **Benefits (the "why"):**
> - **Independent deployment:** Team A deploys without coordinating with Team B. This is the single biggest benefit -- it removes the coordination tax that kills velocity in large organizations.
> - **Independent scaling:** Scale the hot path (e.g., search) without scaling everything else.
> - **Technology heterogeneity:** Each service can use the best tool for the job (different languages, databases, frameworks).
> - **Fault isolation:** A failure in one service doesn't cascade to all services (if designed correctly with circuit breakers, bulkheads, etc.).
> - **Organizational alignment:** Small teams own small services end-to-end ("you build it, you run it").
>
> **Costs (the "what you pay"):**
> - **Distributed systems complexity:** Network failures, partial failures, eventual consistency, distributed transactions -- these are hard problems that don't exist in a monolith.
> - **Operational overhead:** Each service needs its own CI/CD pipeline, monitoring, alerting, logging, deployment infrastructure. Without strong platform engineering, this overhead scales linearly with the number of services.
> - **Testing complexity:** End-to-end testing across services is harder than testing a monolith. Contract testing (Pact, etc.) helps but adds tooling overhead.
> - **Debugging difficulty:** A request that flows through 15 services is vastly harder to debug than one that stays within a single process. Distributed tracing (Jaeger, Zipkin, OpenTelemetry) is essential but adds complexity.
> - **Data consistency:** Without a shared database, maintaining consistency across services requires patterns like sagas, event sourcing, or CQRS -- each with their own complexity.
>
> **When to use microservices:**
> - When your organization has multiple teams that need to deploy independently
> - When different parts of your system have different scaling requirements
> - When you have the platform engineering maturity to support many services
> - When the coordination cost of the monolith exceeds the operational cost of distributed services
>
> **When NOT to use microservices:**
> - Startups with small teams (< 20-30 developers)
> - When you don't yet understand your domain boundaries
> - When you lack the operational tooling (CI/CD, observability, service mesh) to manage many services
> - When you're doing it for resume-driven development rather than solving a real problem

> **[Insight]** The authors and Shoup are careful NOT to say "microservices are always better." The table is deliberately structured to show that monoliths have real advantages (simplicity, low latency, resource efficiency) that are lost when you move to microservices. The key insight is that architecture is a tool, not a religion. The "right" architecture depends on the organization's current scale, team size, and goals. Many organizations have made the mistake of jumping to microservices prematurely, creating what is often called a "distributed monolith" -- all the operational complexity of microservices with none of the autonomy benefits, because service boundaries were drawn incorrectly or because teams lack the tooling maturity to operate many services. The DevOps exemplars (eBay, Amazon, Twitter, LinkedIn) all started as monoliths and evolved to microservices only when the monolith became a bottleneck to organizational goals.

> **[2024+ Context]** Since this edition was published, the architecture discourse has evolved significantly:
>
> - **Modular monoliths** have gained credibility as a deliberate architectural choice, not just a stepping stone. Shopify runs one of the largest e-commerce platforms in the world on a modular monolith (enforced with Packwerk for Ruby). The idea: enforce module boundaries within a single deployable unit, getting most of the organizational benefits of microservices without the distributed systems tax. This aligns with the chapter's message that monoliths aren't inherently bad -- they just need enforced modularity.
> - **Cell-based architecture** (promoted by WSO2 and adopted by organizations like Netflix) organizes services into "cells" -- self-contained units that include multiple services, their data stores, and their communication infrastructure. Cells communicate through well-defined gateways. This is a layer of abstraction above microservices that reduces inter-service communication complexity.
> - **Service mesh** (Istio, Linkerd, Consul Connect) has matured to handle the cross-cutting concerns that make microservices operationally expensive: mTLS, traffic management, observability, retries, circuit breaking. By moving these concerns from application code to infrastructure, service mesh reduces the per-service operational overhead significantly.
> - **Kubernetes** has become the de facto platform for running microservices, providing service discovery, load balancing, rolling deployments, and self-healing. The rise of Kubernetes has lowered the barrier to operating many services, making the "operational overhead" cost in the table somewhat less prohibitive than when this chapter was written.

---

### Case Study: Evolutionary Architecture at Amazon (2002)

This is one of the most studied architecture transformations in technology history.

**The starting point:** Amazon.com started in 1996 as a monolithic application called **Obidos** -- a single web server talking to a backend database. Werner Vogels (Amazon CTO) describes it:

> "[Obidos] evolved to hold all the business logic, all the display logic, and all the functionality that Amazon eventually became famous for: similarities, recommendations, Listmania, reviews, etc." -- Werner Vogels (in interview with ACM Turing Award-winner Jim Gray)

**The problem:** As Obidos grew, it became tangled with complex sharing relationships. Individual pieces could not be scaled as needed.

> "Many things that you would like to see happening in a good software environment couldn't be done anymore; there were many complex pieces of software combined into a single system. It couldn't evolve anymore." -- Werner Vogels

**The architectural decision:**

> "We went through a period of serious introspection and concluded that a service-oriented architecture would give us the level of isolation that would allow us to build many software components rapidly and independently." -- Werner Vogels

**The transformation:** From 2001 to 2005, Amazon moved from a two-tier monolith to a fully distributed, decentralized services platform. Vogels notes they "were one of the first to take this approach."

**Three key lessons from the Amazon transformation:**

1. **Strict service orientation achieves isolation.** When applied rigorously, it gives you a level of ownership and control not previously possible.
2. **Prohibit direct database access by clients.** This makes scaling and reliability improvements to service state possible without involving clients. (This is essentially the bounded context principle -- each service owns its data.)
3. **Development and operational processes benefit from service orientation.** Each service has a team associated with it, completely responsible for the service from scoping to building to operating. ("You build it, you run it.")

**The results:**
- 2011: approximately **15,000 deployments per day**
- 2015: approximately **136,000 deployments per day**

> **[Insight]** Lesson 2 -- "prohibiting direct database access" -- is arguably the most important and most frequently violated architectural principle in the chapter. When Service A reads directly from Service B's database, you have created an invisible, undocumented coupling. Service B cannot change its schema, change its database technology, or scale its database without potentially breaking Service A. The database becomes a shared mutable state that ties the two services together as tightly as if they were in the same codebase. This is why the chapter emphasizes APIs so heavily: APIs are explicit, versioned, documented contracts. Database schemas are implicit, fragile, and difficult to evolve. Every organization I have seen struggle with microservices has this pattern somewhere: "well, we technically have separate services, but they all share a database." That is not microservices. That is a monolith deployed as multiple processes.

> **[Insight]** The leap from 15,000 to 136,000 deployments per day in four years (2011-2015) at Amazon is not just about speed -- it reflects the compounding effect of service-oriented architecture. Each new service added to the ecosystem is independently deployable, so the total deployment count grows roughly with the number of services times the deployment frequency of each. The architecture makes deployment scale sublinearly with organizational complexity rather than superlinearly (as it does in a monolith, where adding more developers makes deployment harder, not easier).

---

## Use the Strangler Fig Application Pattern to Safely Evolve Our Enterprise Architecture

This is the chapter's core prescriptive guidance: how to actually migrate from the architecture you have to the one you need.

**The term** "strangler fig application" was coined by **Martin Fowler in 2004**, inspired by strangler vines he saw in Australia:

> "They seed in the upper branches of a fig tree and gradually work their way down the tree until they root in the soil. Over many years they grow into fantastic and beautiful shapes, meanwhile strangling and killing the tree that was their host." -- Martin Fowler

> **[Deep Dive: The Strangler Fig Application Pattern]**
>
> The strangler fig pattern is the single most important migration strategy in the chapter. Here is how it works in practice:
>
> **Step 1: Identify the seam.** Find a piece of functionality in the monolith that can be extracted. Ideally, this is a bounded context with relatively few inbound and outbound dependencies.
>
> **Step 2: Place existing functionality behind an API.** Before extracting anything, create an API (or facade) in front of the existing functionality. All existing callers should now go through this API. The existing implementation behind the API remains unchanged.
>
> **Step 3: Implement new functionality in the new architecture.** When new features are needed in this area, build them in a new service using the desired architecture. The new service calls back to the old system through the API when it needs existing data or functionality.
>
> **Step 4: Incrementally migrate existing functionality.** Over time, migrate existing features from the old system to the new service. Each migration is a small, testable, reversible step.
>
> **Step 5: Retire the old implementation.** Eventually, all functionality has been migrated. The old code behind the API can be decommissioned.
>
> **Why this works:**
> - **No "big bang" cutover.** The old system and new system coexist, reducing risk.
> - **Reversibility.** If the new service has problems, traffic can be routed back to the old system.
> - **Incremental value.** Each extracted service delivers immediate benefits (independent deployment, better testing, team autonomy) without waiting for the entire migration to complete.
> - **Business-driven prioritization.** Migrate the highest-value areas first (as eBay did, sorting pages by revenue).
>
> **Common pitfalls:**
> - **Tightly coupling the new service to the old system.** If the new service connects directly to the old system's database, you have not achieved decoupling -- you have just moved the code.
> - **Trying to migrate too much at once.** The power of the pattern is in small, incremental steps.
> - **Replicating complexity instead of simplifying.** The chapter warns that existing business processes are often more complex than necessary due to the old system's idiosyncrasies. Migration is an opportunity to simplify, not just rewrite.
>
> **Related pattern -- Branching by Abstraction:** Coined by Paul Hammant, this technique creates an abstraction layer between the areas being changed, enabling evolutionary design while everyone works off trunk/master and practices continuous integration. It is the in-codebase equivalent of the strangler fig pattern.

**Key implementation principles:**

1. **Versioned APIs (immutable services).** When modifying a service, create a new API version rather than changing the existing one. This allows callers to migrate at their own pace and keeps the system loosely coupled.
2. **Client libraries with clean APIs.** If the services you call don't have cleanly defined APIs, build client libraries that hide the complexity of communicating with those systems.
3. **Don't just reproduce existing functionality.** Business processes are often more complex than necessary due to idiosyncrasies of existing systems. Research the user and re-engineer the process for a simpler design.

Martin Fowler underscores the risk of rewrites:

> "Much of my career has involved rewrites of critical systems. You would think such a thing is easy -- just make the new one do what the old one did. Yet they are always much more complex than they seem, and overflowing with risk. The big cut-over date looms, and the pressure is on. While new features (there are always new features) are liked, old stuff has to remain. Even old bugs often need to be added to the rewritten system." -- Martin Fowler

**Strategy for getting started:**
- Create quick wins and deliver early incremental value before continuing to iterate
- Up-front analysis to identify the **smallest possible piece of work** that will usefully achieve a business outcome using the new architecture

> **[Insight]** The Fowler quote about rewrites -- "even old bugs often need to be added to the rewritten system" -- captures a truth that every engineer who has attempted a major rewrite has learned the hard way. Legacy systems encode years of business logic, edge cases, workarounds, and implicit knowledge. A rewrite that doesn't account for these will break in production in ways the team never anticipated. The strangler fig pattern avoids this trap by keeping the old system running and migrating incrementally. You only need to understand and replicate the specific piece you are extracting, not the entire system at once. This is why the chapter recommends finding the "smallest possible piece of work" first -- it limits the blast radius of misunderstanding.

> **[2024+ Context]** The strangler fig pattern has been formalized in cloud migration frameworks. AWS's Migration Hub, Google Cloud's Migrate for Anthos, and Azure's App Service Migration Assistant all embed variations of the pattern. The rise of **API gateways** (Kong, Apigee, AWS API Gateway) and **service mesh ingress** (Istio Gateway, Envoy) has made Step 2 (placing functionality behind an API) significantly easier -- you can route traffic between old and new implementations at the infrastructure level without changing application code. **Feature flags** (LaunchDarkly, Split, Unleash) further enable the pattern by allowing gradual traffic shifting between old and new implementations with instant rollback capability. The combination of API gateway + feature flags + observability has made the strangler fig pattern operationally safer than ever before.

---

### Case Study: Strangler Fig Pattern at Blackboard Learn (2011)

**Company context:** Blackboard Inc. was a pioneer in educational technology with approximately $650 million in annual revenue in 2011. Their flagship product, Blackboard Learn, was packaged software installed and run on-premises at customer sites.

**The problem:** A legacy J2EE codebase dating back to 1997 (with fragments of Perl code still embedded). David Ashman, chief architect, describes the symptoms:

> "Our build, integration, and testing processes kept getting more and more complex and error prone. And the larger the product got, the longer our lead times and the worse the outcomes for our customers. To even get feedback from our integration process would require twenty-four to thirty-six hours." -- David Ashman

**The diagnostic evidence:**

Ashman used data from the source code repository going back to 2005 to make the problem visible.

![Figure 13.2: Blackboard Learn Code Repository: Before Building Blocks](../images/Fig13-2.jpg)
*Source: "DOES14 -- David Ashman -- Blackboard Learn -- Keep Your Head in the Clouds," YouTube video, DevOps Enterprise Summit 2014*

**Key observation from Figure 13.2:** The top graph shows lines of code continuing to increase, while the bottom graph shows code commits starting to decrease. The codebase was growing, but developers were making fewer changes -- objective evidence that the architecture was making it increasingly difficult to introduce changes.

> "To me, it said we needed to do something, otherwise the problems would keep getting worse, with no end in sight." -- David Ashman

**The solution: Building Blocks (2012)**

Ashman's team implemented a code re-architecting project using the **strangler fig pattern**. They created what they called **Building Blocks** -- separate modules decoupled from the monolithic codebase, accessed through fixed APIs. This allowed developers to:
- Work in separate modules with far more autonomy
- Avoid constantly communicating and coordinating with other teams
- Make mistakes that resulted in small, local failures instead of catastrophic global ones

**What happened when Building Blocks were available:**
- The size of the monolith source code repository began to **decrease** (developers moved code into Building Block modules)
- Every developer given a choice **preferred working in the Building Block codebase** where they had more autonomy, freedom, and safety

![Figure 13.3: Blackboard Learn Code Repository: After Building Blocks](../images/Fig13-3.jpg)
*Source: "DOES14 -- David Ashman -- Blackboard Learn -- Keep Your Head in the Clouds," YouTube video, DevOps Enterprise Summit 2014*

**Key observation from Figure 13.3:** Both lines of code and code commits grew exponentially in the Building Blocks repositories. The new architecture unlocked developer productivity that had been suppressed by the monolith.

> "Having developers work in the Building Blocks architecture made for impressive improvements in code modularity, allowing them to work with more independence and freedom. In combination with the updates to our build process, they also got faster, better feedback on their work, which meant better quality." -- David Ashman

> **[Insight]** The Blackboard case study contains one of the most underappreciated diagnostic techniques in the chapter: **plotting lines of code against code commits over time from version control data.** When LOC increases but commits decrease, it is an objective, non-debatable signal that the architecture is throttling developer productivity. This is data that every organization has access to (it lives in git) but almost nobody examines. If you are trying to build a case for re-architecture to your leadership, this graph is more persuasive than any theoretical argument. It says: "our developers are producing less output per person despite the codebase growing, and the trend is worsening." The Blackboard team used this data not just to justify the investment but to measure the success of the migration -- commits per developer increased dramatically in the Building Blocks architecture.

> **[Insight]** The observation that "every developer given a choice would work in the Building Block codebase" is a natural experiment in developer experience. Developers vote with their feet (or in this case, their commits). When given two architectures -- one tightly coupled with high coordination cost, one modular with autonomy -- 100% chose the modular path. This is not surprising, but it is powerful evidence. If your organization has pockets of modular architecture alongside the monolith, look at where developers prefer to work. That preference is a leading indicator of which architecture supports productivity and safety.

---

### Case Study: Continuous Learning -- Architecture and DORA Research

The **DORA and Puppet 2017 State of DevOps Report** found that **architecture was the largest contributor to continuous delivery.**

Key findings:
- Teams who scored highest on architectural capabilities could **complete their work independently** of other teams
- They could **change their systems without dependencies** on other teams
- These findings were echoed in the **2018 and 2019** State of DevOps Reports, confirming the continued importance of **loosely coupled architecture** for fast, low-friction deployment and release

> **[Insight]** This is perhaps the most important finding in the entire chapter: architecture, not tooling, not culture, not process, was the **largest** contributor to continuous delivery in the DORA research. This means that organizations investing heavily in CI/CD tooling, automated testing, and deployment pipelines -- while ignoring the architecture -- are optimizing a secondary factor. If services are tightly coupled, no amount of pipeline sophistication will enable independent, frequent deployment. The pipeline can only deliver value as fast as the architecture allows. This finding should be posted on the wall of every engineering leadership meeting room.

> **[2024+ Context]** The DORA findings about architecture have only grown stronger in subsequent research. The 2022 and 2023 DORA reports introduced "loosely coupled teams" as an explicit capability, noting that both loosely coupled architecture AND loosely coupled team structures are required. The Team Topologies framework (Skelton & Pais, 2019) provides the organizational complement: stream-aligned teams own services end-to-end, platform teams provide shared infrastructure, enabling teams reduce cognitive load, and complicated-subsystem teams handle deep specialization. The research shows you need both: loosely coupled architecture + loosely coupled team topology = elite delivery performance. One without the other delivers diminishing returns.

---

## Conclusion

The chapter concludes by reinforcing the central argument:

> "To a large extent, the architecture that our services operate within dictates how we test and deploy our code."

Because we are often stuck with architectures optimized for a different era or different organizational goals, **we must be able to safely migrate from one architecture to another.** The strangler fig pattern enables this incremental migration, and the case studies (eBay, Amazon, Blackboard) demonstrate that it works at vastly different scales and in different contexts.

The architecture must evolve to serve the current needs of the organization -- and the muscle to perform that evolution is as important as any specific architectural choice.

---

## How Generative AI Is Reshaping Architectural Decisions for Low-Risk Releases

> **[GenAI + DevOps]** Every concept in this chapter -- evolutionary architecture, the strangler fig pattern, monoliths vs. microservices, bounded contexts -- is being reshaped by Generative AI. Here is a concept-by-concept analysis:

### GenAI and Evolutionary Architecture

| Architectural Activity | Traditional | With GenAI |
|---|---|---|
| **Identifying extraction candidates** | Manual code analysis, tribal knowledge, architecture reviews | AI-powered static analysis tools (e.g., CodeScene, Codiumate) can analyze dependency graphs, coupling metrics, and change frequency to recommend which modules to extract first |
| **Defining service boundaries** | Domain workshops, event storming, expert judgment | AI can analyze codebases to suggest bounded context boundaries based on call patterns, data access patterns, and change coupling |
| **Fitness function creation** | Architects manually define and maintain architectural tests | AI can generate and update fitness functions based on architectural intent (e.g., "these two modules should never depend on each other") |
| **Migration planning** | Manual dependency analysis and sequencing | AI can model migration paths, estimate effort, and identify hidden dependencies that humans miss |

### GenAI and the Strangler Fig Pattern

- **API generation:** AI can automatically generate API facades (Step 2 of the pattern) by analyzing existing function signatures and call patterns in the monolith
- **Test generation for migration safety:** AI can generate comprehensive test suites that verify behavioral equivalence between old and new implementations -- the critical safety net for any strangler fig migration
- **Dependency discovery:** AI can crawl codebases to find hidden dependencies (database access, file system coupling, shared state) that would break during extraction -- dependencies that are invisible to manual analysis
- **Risk:** AI-generated code may introduce subtle behavioral differences during migration that are hard to detect. The "even old bugs often need to be added" problem (per Fowler) becomes harder when AI is generating the new implementation without full understanding of legacy business logic.

### GenAI and Microservices Operations

- **AI-powered service mesh:** AI agents that dynamically adjust traffic routing, circuit breaker thresholds, and retry policies based on real-time performance data
- **AI incident correlation:** When a request fails across 15 microservices, AI can correlate traces, logs, and metrics to identify the root cause in seconds rather than hours
- **AI architecture drift detection:** Continuous AI monitoring of actual service communication patterns vs. intended architecture, alerting when services develop unauthorized dependencies
- **Emerging pattern: "AI Architecture Guardian"** -- an always-on AI agent that monitors commits, pull requests, and deployments for architectural violations (e.g., direct database access across service boundaries, circular dependencies, coupling increases)

### The Meta-Question: Does AI Change the Architecture Principles, or Accelerate Them?

**The answer: accelerate, not change.** Loosely coupled architecture is still better than tightly coupled architecture. The strangler fig pattern is still safer than big bang rewrites. Evolutionary architecture is still necessary because requirements change. AI does not invalidate any of these principles -- it makes the gap between organizations that practice them and those that don't even wider.

The one area where AI may introduce genuinely new architectural patterns is in **AI-native services** -- services whose core logic is an AI model rather than deterministic code. These services have different testing, versioning, and deployment characteristics (model versions rather than code versions, probabilistic rather than deterministic behavior, data drift rather than code bugs). Architects will need to extend the principles in this chapter to accommodate these new service types.

**Further reading:**
- [Building Evolutionary Architectures (O'Reilly)](https://www.oreilly.com/library/view/building-evolutionary-architectures/9781492097532/) -- Neal Ford, Rebecca Parsons, Patrick Kua; the definitive guide to fitness functions and evolutionary architecture
- [Martin Fowler: Strangler Fig Application](https://martinfowler.com/bliki/StranglerFigApplication.html) -- the original 2004 article that coined the term
- [Sam Newman: Building Microservices, 2nd Edition](https://www.oreilly.com/library/view/building-microservices-2nd/9781492034018/) -- comprehensive guide to microservices architecture, including when NOT to use them
- [Team Topologies](https://teamtopologies.com/) -- the organizational counterpart to the architectural patterns in this chapter
- [Modular Monolith with DDD (GitHub)](https://github.com/kgrzybek/modular-monolith-with-ddd) -- reference implementation of the modular monolith approach as an alternative to premature microservices
- [CNCF Platform Engineering Maturity Model](https://tag-app-delivery.cncf.io/whitepapers/platform-eng-maturity-model/) -- framework for building the platform layers that enable small teams to own large services
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/) -- standard for distributed tracing across microservices, essential for the observability that makes microservices debuggable
