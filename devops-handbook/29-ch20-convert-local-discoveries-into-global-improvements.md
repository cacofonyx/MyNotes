# Chapter 20: Convert Local Discoveries into Global Improvements

> **Part V — The Technical Practices of Continual Learning**

This chapter addresses one of the most critical challenges in large organizations: ensuring that knowledge, improvements, and discoveries made by one team are propagated across the entire organization. While Chapter 19 focused on creating a culture where learning from failure is safe and encouraged, this chapter provides the specific mechanisms — technical and organizational — for multiplying the effect of those learnings. The practices range from ChatOps and shared source code repositories to codified non-functional requirements and deliberate technology standardization. The overarching goal is that everyone doing work benefits from the cumulative experience of the organization.

## Table of Contents

- [The Knowledge Propagation Problem](#the-knowledge-propagation-problem)
- [Use Chat Rooms and Chat Bots to Automate and Capture Organizational Knowledge](#use-chat-rooms-and-chat-bots-to-automate-and-capture-organizational-knowledge)
  - [Hubot at GitHub](#hubot-at-github)
- [Automate Standardized Processes in Software for Reuse](#automate-standardized-processes-in-software-for-reuse)
  - [ArchOps at GE Capital](#archops-at-ge-capital)
- [Create a Single, Shared Source Code Repository for Our Entire Organization](#create-a-single-shared-source-code-repository-for-our-entire-organization)
  - [Google's Monorepo](#googles-monorepo)
  - [Case Study: Continuous Learning — Code Maintainability (DORA 2019)](#case-study-continuous-learning--code-maintainability-dora-2019)
  - [The Library Ownership Model](#the-library-ownership-model)
  - [The Java Struts Anti-Pattern](#the-java-struts-anti-pattern)
  - [Software Supply Chain Security](#software-supply-chain-security)
- [Spread Knowledge by Using Automated Tests as Documentation and Communities of Practice](#spread-knowledge-by-using-automated-tests-as-documentation-and-communities-of-practice)
- [Design for Operations through Codified Non-Functional Requirements](#design-for-operations-through-codified-non-functional-requirements)
- [Build Reusable Operations User Stories into Development](#build-reusable-operations-user-stories-into-development)
- [Ensure Technology Choices Help Achieve Organizational Goals](#ensure-technology-choices-help-achieve-organizational-goals)
  - [Cloud Computing and Self-Service Platforms](#cloud-computing-and-self-service-platforms)
  - [Case Study: Standardizing a New Technology Stack at Etsy (2010)](#case-study-standardizing-a-new-technology-stack-at-etsy-2010)
  - [Case Study: Crowdsourcing Technology Governance at Target (2018)](#case-study-crowdsourcing-technology-governance-at-target-2018)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Knowledge Propagation](#how-generative-ai-is-reshaping-knowledge-propagation)
  - [GenAI and ChatOps Evolution](#genai-and-chatops-evolution)
  - [GenAI and Shared Code Repositories](#genai-and-shared-code-repositories)
  - [GenAI and Non-Functional Requirements](#genai-and-non-functional-requirements)
  - [GenAI and Technology Governance](#genai-and-technology-governance)
  - [The Meta-Question: Does AI Make Knowledge Propagation Automatic?](#the-meta-question-does-ai-make-knowledge-propagation-automatic)

---

## The Knowledge Propagation Problem

The chapter opens by framing the challenge. In Chapter 19, we created a safe learning culture through blameless retrospectives and failure injection. In this chapter, we create mechanisms to ensure those learnings are not trapped within the team that generated them but are propagated globally throughout the organization.

The goal is to "elevate the state of the practice of the entire organization so that everyone doing work benefits from the cumulative experience of the organization."

> **[Insight]** Knowledge propagation is the difference between an organization where every team makes the same mistakes independently and an organization where each mistake is made only once. In a 500-person engineering organization with 50 teams, a failure to propagate knowledge means the same problem is potentially solved (or suffered through) 50 times. With effective propagation, it is solved once, and 49 teams benefit without ever encountering it. The leverage is enormous — and it is one of the key mechanisms behind the performance gap between elite and low-performing organizations identified in the DORA research.

---

## Use Chat Rooms and Chat Bots to Automate and Capture Organizational Knowledge

The chapter describes how chat rooms can be used not just for communication but as a mechanism for transparency, knowledge capture, and automation. This technique was pioneered in the **ChatOps** journey at GitHub.

The goal was to put automation tools "into the middle of the conversation in their chat rooms, helping create transparency and documentation of their work."

Jesse Newland, a systems engineer at GitHub, explains: **"Even when you're new to the team, you can look in the chat logs and see how everything is done. It's as if you were pair-programming with them all the time."**

**Benefits of performing work through automation in chat rooms:**
- Everyone sees everything that is happening
- Engineers, on their first day, can see what daily work looks like and how it is performed
- People are more apt to ask for help when they see others helping each other
- Rapid organizational learning is enabled and accumulated

**Key advantage over email:** Chat rooms inherently record and make all communications public. Emails are private by default, and the information in them cannot easily be discovered or propagated.

> **[Deep Dive: ChatOps as a Knowledge Capture System]**
>
> ChatOps is often described as "automation in chat," but its deeper value is as a knowledge capture system. Consider the difference:
>
> - **Without ChatOps:** An engineer SSHes into a server, runs some commands, fixes a problem, maybe writes a note in a ticket. The knowledge of what was done and why lives in one person's head and possibly one ticket.
> - **With ChatOps:** The engineer types `@hubot deploy owl to production` in a shared channel. Everyone sees the command, the output, and the context (the preceding discussion about why the deploy was needed). The knowledge is automatically captured, timestamped, searchable, and visible to future team members.
>
> This is not just a convenience — it fundamentally changes the rate of organizational learning. New engineers can read chat history to understand not just *what* was done but *why* it was done, *what was discussed before the decision*, and *what the outcome was*. This rich contextual knowledge is exactly what is lost when work is performed in isolation.

### Hubot at GitHub

GitHub created **Hubot**, a software application that interacted with the Ops team in their chat rooms. All Operations staff at GitHub worked remotely — no two engineers were in the same city. As Mark Imbriaco, former VP of Operations, recalls: **"There was no physical watercooler at GitHub. The chat room was the water cooler."**

Hubot was integrated with automation technologies including Puppet, Capistrano, Jenkins, resque, and graphme. Actions performed through Hubot included:
- Checking health of services
- Puppet pushes or code deployments to production
- Muting alerts during maintenance
- Pulling up smoke test logs when deployments failed
- Taking production servers out of rotation
- Reverting to master for production front-end services
- Even apologizing to on-call engineers

**Example chat exchange:**
> *@sr: @jnewland, how do you get that list of big repos? disk_hogs or something?*
> *@jnewland: /disk-hogs*

Newland observed that questions like "How is that deploy going?" or "Are you deploying that or should I?" or "How does the load look?" were rarely asked anymore — the information was visible to everyone in the chat room.

The most important result, according to Newland: **Ops work became more humane** as engineers were enabled to discover problems and help each other quickly and easily.

> **[Insight]** The word "humane" is worth pausing on. Newland did not say the most important result was faster deployments or fewer incidents — he said it was making Ops work more humane. When Operations engineers work in isolation (SSHing into servers alone at 3 AM), the work is lonely, stressful, and error-prone. When the same work is visible in a shared chat room, other people can see you struggling, offer help, catch mistakes, and share the cognitive load. This human element of ChatOps is often undervalued relative to the automation benefits, but it directly supports the just culture described in Chapter 19.

> **[2024+ Context]** The ChatOps paradigm has evolved significantly since GitHub's Hubot:
>
> - **Slack and Microsoft Teams** have become the dominant platforms, replacing IRC. Slack's workflow builder and app ecosystem have made ChatOps accessible without custom bot development.
> - **Modern incident management tools** (Incident.io, Rootly, FireHydrant, PagerDuty) are built as Slack-native applications, bringing the entire incident lifecycle into the chat room — from declaration to triage to resolution to retrospective.
> - **GitOps and deployment bots:** Tools like ArgoCD, Flux, and GitHub Actions post deployment status to Slack channels. PR-based workflows make deployments visible in the same chat context.
> - **The "AI teammate" pattern:** AI assistants in Slack (e.g., Anthropic's Claude, OpenAI's ChatGPT integrations) can answer questions about infrastructure, suggest runbook steps during incidents, and help with on-call triage — extending the ChatOps model from "automation in chat" to "intelligence in chat."
>
> The core principle remains unchanged: performing work in a shared, visible, searchable context multiplies organizational learning.

---

## Automate Standardized Processes in Software for Reuse

The chapter identifies a common anti-pattern: codifying standards and processes in prose, stored in Word documents uploaded "somewhere." The result is predictable — engineers building new applications do not know the documents exist, or do not have time to implement them, leading to fragile, insecure, and unmaintainable applications.

**The prescription:** Instead of putting expertise into Word documents, transform standards and processes into **executable form** that makes them easier to reuse. Put them into a centralized source code repository, making the tool available for everyone to search and use.

### ArchOps at GE Capital

Justin Arbuckle, chief architect at GE Capital in 2013, needed to create a mechanism for teams to comply with policy across "national, regional, and industry regulations across dozens of regulatory frameworks, spanning thousands of applications running on tens of thousands of servers in tens of data centers."

The mechanism they created was called **ArchOps**, which **"enabled our engineers to be builders, not bricklayers. By putting our design standards into automated blueprints that were able to be used easily by anyone, we achieved consistency as a byproduct."**

Arbuckle concluded: **"the actual compliance of an organization is in direct proportion to the degree to which its policies are expressed as code."**

> **[Deep Dive: Policy as Code — The Compliance Revolution]**
>
> Arbuckle's statement — "compliance is in direct proportion to the degree to which policies are expressed as code" — is one of the most important insights in this chapter. It reframes compliance from a human oversight problem to an engineering automation problem.
>
> **Traditional compliance:** Write policies in documents. Train people to follow them. Audit periodically. Find violations months later. Remediate painfully.
>
> **Policy as code:** Express policies in machine-executable form (Open Policy Agent, Sentinel, Kyverno, etc.). Enforce them automatically in the deployment pipeline. Violations are caught at build time, not audit time. Compliance is continuous, not periodic.
>
> Examples:
> - "All containers must run as non-root" → OPA/Gatekeeper policy enforced at Kubernetes admission
> - "All S3 buckets must be encrypted" → Terraform Sentinel policy enforced at `terraform plan`
> - "All services must have health checks" → CI pipeline check that fails builds without health endpoints
> - "All dependencies must be from approved registries" → Package manager configuration enforced by policy
>
> When the compliant path is also the easiest path (because it is automated and self-service), compliance becomes a natural byproduct of doing work — not an overhead imposed on top of it.

> **[2024+ Context]** Policy as code has become a mature discipline:
>
> - **Open Policy Agent (OPA):** The CNCF graduated project has become the de facto standard for policy as code, used for Kubernetes admission control, API authorization, Terraform compliance, and more.
> - **Kyverno:** A Kubernetes-native policy engine that uses YAML (instead of Rego, OPA's language) for policy definitions, lowering the barrier to adoption.
> - **HashiCorp Sentinel:** Policy as code framework for Terraform, Vault, Consul, and Nomad.
> - **Supply chain security policies:** SLSA (Supply-chain Levels for Software Artifacts), Sigstore, and in-toto provide frameworks for expressing and enforcing software supply chain policies as code.

---

## Create a Single, Shared Source Code Repository for Our Entire Organization

The chapter presents the shared source code repository as one of the most powerful mechanisms for converting local discoveries into global improvements. When anything in the repository is updated (e.g., a shared library), it rapidly and automatically propagates to every service that uses it through each team's deployment pipeline.

### Google's Monorepo

Google is cited as one of the largest examples. By 2015, Google had:
- A single shared source code repository
- Over one billion files
- Over two billion lines of code
- Used by every one of their twenty-five thousand engineers
- Spanning every Google property (Search, Maps, Docs, Calendar, Gmail, YouTube)

Rachel Potvin, Google engineering manager: engineers can leverage "a wealth of libraries" because **"almost everything has already been done."**

Eran Messeri, Google Developer Infrastructure group: one advantage of using a single repository is that it allows users to easily access all code in its most up-to-date form **without the need for coordination.**

**What goes into the shared repository (beyond source code):**
- Configuration standards for libraries, infrastructure, and environments (Chef, Puppet, or Ansible scripts)
- Deployment tools
- Testing standards and tools, including security
- Deployment pipeline tools
- Monitoring and analysis tools
- Tutorials and standards

Randy Shoup describes: **"the most powerful mechanism for preventing failures at Google is the single code repository. Whenever someone checks in anything into the repo, it results in a new build, which always uses the latest version of everything."**

Tom Limoncelli, co-author of *The Practice of Cloud System Administration*: **"You can write a tool exactly once and have it be usable for all projects. You have 100% accurate knowledge of who depends on a library; therefore, you can refactor it and be 100% sure of who will be affected and who needs to test for breakage. I could probably list one hundred more examples. I can't express in words how much of a competitive advantage this is for Google."**

> **[Deep Dive: Monorepo vs. Polyrepo — The Tradeoffs]**
>
> Google's monorepo approach is not universally applicable. Understanding the tradeoffs is important:
>
> **Monorepo advantages:**
> - Single version of truth for all code
> - Atomic cross-project changes (refactor a library and all consumers in one commit)
> - 100% visibility into who depends on what
> - Simplified tooling (one build system, one CI system, one code search)
> - Easier code reuse and discovery
>
> **Monorepo challenges:**
> - Requires massive investment in custom tooling (build systems, code review, CI) at scale
> - Google, Meta, and Microsoft have each built custom version control and build systems for this purpose
> - Can create tight coupling if not carefully managed
> - Access control is more complex (not all engineers should see all code)
>
> **Polyrepo advantages:**
> - Each team has full autonomy over their repository
> - Standard tooling (Git, GitHub/GitLab) works out of the box
> - Clearer ownership boundaries
> - Simpler access control
>
> **Polyrepo challenges:**
> - Cross-cutting changes require coordinating across multiple repositories
> - Dependency management becomes complex (which version of library X does service Y use?)
> - Code discovery is harder (is there already a library for this?)
> - "Diamond dependency" problems
>
> The key insight from the chapter is not "use a monorepo" but rather "ensure knowledge propagates." If you use a polyrepo approach, you need other mechanisms (shared package registries, internal developer portals, automated dependency updates) to achieve the same knowledge propagation that a monorepo provides structurally.

### Case Study: Continuous Learning -- Code Maintainability (DORA 2019)

Based on Rachel Potvin's expertise at Google, DORA's 2019 State of DevOps Report identified **code maintainability** as a key construct for continuous delivery success.

The report found: **"Teams that manage code maintainability well have systems and tools that make it easy for developers to change code maintained by other teams, find examples in the codebase, reuse other people's code, as well as add, upgrade, and migrate to new versions of dependencies without breaking their code."**

These systems and tools contribute to continuous delivery **and** help decrease technical debt, which in turn improves productivity.

### The Library Ownership Model

At Google, every library has an **owner** responsible for:
- Ensuring the library compiles and passes tests for all projects that depend on it (like a "real-world librarian")
- Migrating each project from one version to the next

This ownership model is critical: it means there is always a single person or team accountable for the health and evolution of each shared component.

### The Java Struts Anti-Pattern

The chapter describes a real-world organization running **eighty-one different versions** of the Java Struts framework in production. All but one had critical security vulnerabilities, and maintaining all versions created significant operational burden. The variance made upgrading risky and unsafe, which discouraged developers from upgrading — creating a vicious cycle.

The single source repository with automated testing solves this by ensuring teams can migrate to new versions safely and confidently.

> **[Insight]** The Java Struts example is a perfect illustration of how local optimization (each team choosing the version that works for them) creates global dysfunction (81 versions, 80 with known vulnerabilities, enormous maintenance burden). This is the same tension between team autonomy and organizational coherence that appears throughout the book. The solution is not to eliminate team autonomy (which kills innovation) but to provide shared infrastructure that makes the right thing the easy thing — a single repository with a single current version, automated migration, and comprehensive testing.

### Software Supply Chain Security

The chapter notes that dependencies must be drawn from within the organization's source control or package repository to prevent attacks through the "software supply chain" from compromising systems.

> **[2024+ Context]** Software supply chain security has become a top-tier concern since this chapter was written:
>
> - **SolarWinds attack (2020):** Demonstrated that compromising a software build pipeline can provide access to thousands of downstream organizations.
> - **Log4Shell (2021):** A critical vulnerability in the widely-used Log4j library showed how a single transitive dependency can expose entire organizations.
> - **SLSA framework:** Supply-chain Levels for Software Artifacts provides a graduated security framework for software supply chains.
> - **Sigstore:** Open-source project for signing, verifying, and protecting software supply chains.
> - **SBOM requirements:** Software Bill of Materials is now required by US Executive Order 14028 for software sold to the federal government.
> - **Dependency management tools:** Dependabot (GitHub), Renovate, Snyk, and Socket.dev provide automated dependency scanning, vulnerability detection, and upgrade automation.
>
> The chapter's prescription of a single shared repository with controlled dependencies has become a security imperative, not just a productivity benefit.

---

## Spread Knowledge by Using Automated Tests as Documentation and Communities of Practice

When shared libraries are used across the organization, automated tests serve a dual purpose: ensuring quality **and** documenting how to use the library.

With test-driven development (TDD), automated tests become a **living, up-to-date specification** of the system. Any engineer wishing to understand how to use a system can look at the test suite to find working examples of the API.

**Organizational structure for knowledge propagation:**
- Each library should have a **single owner or team** representing where expertise resides
- Only one version should be allowed in production, ensuring production leverages the best collective knowledge
- The library owner is responsible for safely migrating groups from one version to the next
- Create **discussion groups or chat rooms** for each library or service, so anyone with questions can get responses from other users

> **[Insight]** The idea that automated tests are documentation is profound and underappreciated. Traditional documentation (READMEs, wikis, API docs) rots over time — it is written once and gradually diverges from the actual behavior of the code. Automated tests, by contrast, are verified every time the CI pipeline runs. If the test says "calling createUser with these parameters returns a 201 status and this JSON body," that statement is verified to be true as of the last successful build. Tests cannot lie (assuming they are well-written and actually run). This makes the test suite the most reliable documentation in the entire organization.

---

## Design for Operations through Codified Non-Functional Requirements

When Development follows their work downstream and participates in production incident resolution, applications become increasingly better designed for Operations. The chapter identifies a set of **non-functional requirements** that should be integrated into all production services:

- Sufficient production telemetry in applications and environments
- The ability to accurately track dependencies
- Services that are resilient and degrade gracefully
- Forward and backward compatibility between versions
- The ability to archive data to manage production data set size
- The ability to easily search and understand log messages across services
- The ability to trace requests from users through multiple services
- Simple, centralized runtime configuration using feature flags, etc.

> **[Deep Dive: Non-Functional Requirements as Organizational Knowledge]**
>
> Each of these non-functional requirements represents accumulated organizational wisdom about what it takes to run a production service reliably. Consider the history behind each:
>
> - **"Sufficient production telemetry"** — learned from incidents where teams were "troubleshooting blind" (like the CSG outage in Chapter 19)
> - **"Accurately track dependencies"** — learned from cascade failures where no one knew which upstream service was causing the problem
> - **"Resilient and degrade gracefully"** — learned from total outages caused by a single failing component (the Netflix lesson)
> - **"Forward and backward compatibility"** — learned from deployments that could not be rolled back because database schema changes were irreversible
> - **"Trace requests through multiple services"** — learned from debugging distributed systems where a user's request touched 15 services
>
> By codifying these requirements, the organization ensures that each new service starts with the collective wisdom of every previous service's operational experience. This is the "local to global" mechanism in its most concrete form.

> **[2024+ Context]** Non-functional requirements have been formalized through several modern frameworks:
>
> - **OpenTelemetry:** Provides a standard for instrumenting applications with traces, metrics, and logs — addressing the telemetry, dependency tracking, and request tracing requirements simultaneously.
> - **Production readiness reviews:** Formalized at Google (SRE Book, Chapter 32), these reviews ensure services meet operational requirements before launch.
> - **Backstage scorecards:** Spotify's developer portal allows organizations to define and track compliance with non-functional requirements across all services.
> - **Platform engineering "golden paths":** Internal developer platforms encode non-functional requirements into templates, so new services are born compliant.

---

## Build Reusable Operations User Stories into Development

For Operations work that cannot be fully automated or made self-service, the goal is to make recurring work as repeatable and deterministic as possible through standardization, automation, and documentation.

Instead of manually building servers according to checklists, automate as much as possible, including post-installation configuration management. Where steps cannot be automated (e.g., physically racking a server), define handoffs as clearly as possible.

Tools like **Terraform** automate provisioning and configuration of cloud infrastructure. Ad hoc changes can be captured in ticketing systems (JIRA, ServiceNow), with infrastructure configuration changes captured in version control and applied automatically — a paradigm known as **infrastructure-as-code** or **GitOps**.

**The goal:** For all recurring Ops work, know: what work is required, who is needed, what the steps are, and how long it takes. Example: "We know a high-availability rollout takes fourteen steps, requiring work from four different teams, and the last five times we performed this it took an average of three days."

By creating well-defined "Ops user stories," recurring Operations work becomes visible alongside Development work, enabling better planning and more repeatable outcomes.

> **[Insight]** The concept of "Ops user stories" is a powerful bridge between Development and Operations. By expressing Ops work in the same format as Dev work (user stories in a backlog), it becomes visible, plannable, and prioritizable alongside feature work. This addresses a common complaint from Ops teams: "All our work is invisible — leadership only sees what Dev ships." When Ops work is expressed as user stories with story points and velocity tracking, its volume and value become visible to everyone.

---

## Ensure Technology Choices Help Achieve Organizational Goals

While service-oriented architectures allow small teams to build services in whatever language or framework suits them, this autonomy can create problems when expertise for a critical service resides in only one team, creating a bottleneck.

**The diagnostic:** If a list of technologies that Operations will support does not exist, go through production infrastructure and services to find which ones are creating disproportionate failure demand and unplanned work.

**Technologies to identify and address:**
- Those that impede or slow down flow of work
- Those that disproportionately create high levels of unplanned work
- Those that disproportionately create large numbers of support requests
- Those most inconsistent with desired architectural outcomes (throughput, stability, security, reliability, business continuity)

### Cloud Computing and Self-Service Platforms

The goal is to create infrastructure platforms where users (including development teams) can self-service operations without raising tickets or sending emails. This aligns with NIST's five essential characteristics of cloud computing:

1. **On-demand self-service:** Automatically provision computing resources without human interaction
2. **Broad network access:** Accessible through heterogeneous platforms
3. **Resource pooling:** Multi-tenant model with dynamic resource assignment
4. **Rapid elasticity:** Elastically provision and release resources on demand
5. **Measured service:** Automatically control, optimize, and report resource use

**DORA finding:** Only 29% of respondents using cloud infrastructure agreed they met all five NIST characteristics. But elite performers were **twenty-four times more likely** to have met all essential cloud characteristics compared to low performers.

> **[Insight]** The 24x gap between elite and low performers in meeting cloud characteristics is one of the most striking findings cited in this chapter. It demonstrates that "being in the cloud" is not the same as "getting value from the cloud." Many organizations lift-and-shift on-premises workloads to cloud VMs without adopting cloud-native practices (auto-scaling, self-service provisioning, managed services). They pay cloud bills without getting cloud benefits. The five NIST characteristics provide a concrete checklist for assessing whether your cloud adoption is delivering real value.

### Case Study: Standardizing a New Technology Stack at Etsy (2010)

After a nearly disastrous 2010 peak holiday season, Etsy decided to massively reduce the number of technologies in production, choosing a few the entire organization could fully support.

**Decision:** Migrate the entire platform to **PHP and MySQL**. This was a **philosophical decision, not a technological one** — they wanted both Dev and Ops to understand the full stack so everyone could contribute to a single platform and read, rewrite, and fix each other's code.

**Technologies retired:** lighttpd, Postgres, MongoDB, Scala, CoffeeScript, Python, and many others.

**The MongoDB lesson:** Dan McKinley, a developer who introduced MongoDB at Etsy in 2010, wrote that all benefits of a schema-less database were negated by operational problems: logging, graphing, monitoring, production telemetry, backups, restoration, and numerous other issues. The result was abandoning MongoDB and porting to the already-supported MySQL infrastructure.

Michael Rembetsy, Etsy's Director of Operations: **"We retired some great technologies, taking them entirely out of production."**

> **[Deep Dive: The Hidden Cost of Technology Diversity]**
>
> The Etsy case study is controversial because it appears to argue against innovation. But the real lesson is about understanding total cost of ownership:
>
> **Visible costs of a new technology:**
> - Developer time to build the feature
> - Training time to learn the technology
>
> **Hidden costs (often discovered only after production deployment):**
> - Monitoring integration (does our monitoring system support this database?)
> - Logging integration (do our log aggregation tools parse this format?)
> - Backup and restoration procedures (has anyone tested restoring this database type?)
> - Security patching (who is responsible for tracking and applying patches?)
> - On-call support (can the on-call engineer debug problems at 3 AM?)
> - Incident response (do our runbooks cover this technology?)
> - Hiring (can we find enough engineers who know this technology?)
>
> At Etsy's scale, the hidden costs overwhelmed the visible benefits. The decision to standardize on PHP and MySQL was not a judgment that those technologies were superior — it was a judgment that the operational efficiency of having a fully-supported, well-understood stack outweighed the theoretical benefits of using the "best" technology for each use case.
>
> This is a judgment call that each organization must make for itself, and the answer depends on scale, maturity, and operational capabilities.

### Case Study: Crowdsourcing Technology Governance at Target (2018)

**Background:** Target previously had an **Architectural Review Board (ARB)** — a centralized group that met regularly to make tool decisions for all product teams. This was neither efficient nor effective.

**The solution:** Dan Cundiff and Jason Walker created **recommend_tech**, a repository in GitHub featuring a simple list of technology choices organized by domain (collaboration tools, application frameworks, caching, datastores, etc.).

**How it works:**
- Each technology is listed as **recommended**, **limited use**, or **do not use**
- Each file shows why that technology has its disposition and how to use it
- Full history showing how decisions were made is available in the repo
- Each disposition has a **half-life** — a directional waypoint for teams to understand the possibility of a shift
- **Anyone at Target** can open a pull request to suggest changes, new technologies, etc.
- Everyone can comment and discuss benefits or risks
- When a PR is merged, the technology choice is "strongly recommended and loosely held until the next pattern emerges"

**Key principles:**
- **Accessible:** Everyone can contribute
- **Transparent:** Everyone can see
- **Flexible:** Easy to change
- **Cultural:** Community-driven

**For changes with a "steep cost"** (e.g., changing cloud providers, decommissioning a data center), the CIO is brought into the process. Any engineer can pitch their idea directly to the CIO and senior leaders.

> **[Deep Dive: Governance vs. Guidance — A Spectrum]**
>
> The Target case study illustrates a fundamental shift in how technology governance works:
>
> | Dimension | Traditional Governance (ARB) | Crowdsourced Guidance (recommend_tech) |
> |---|---|---|
> | **Decision maker** | Centralized committee | Community with escalation path |
> | **Speed** | Weeks to months (committee meetings) | Days (PR review and merge) |
> | **Transparency** | Decisions communicated after the fact | Full discussion history in Git |
> | **Input** | Limited to committee members | Open to all engineers |
> | **Enforcement** | Mandatory (tollgates) | Advisory (guardrails) |
> | **Adaptability** | Slow (requires committee reconvening) | Fast (any engineer can propose a change) |
> | **Context** | Often lost (meeting minutes, if any) | Preserved in Git history |
>
> The key insight is that **guidance with transparency is more effective than governance without it**. When engineers understand *why* a technology choice was made (because the reasoning is in the Git history), they are more likely to follow it voluntarily than when a committee decree arrives without context.

> **[2024+ Context]** The recommend_tech pattern has inspired similar approaches at many organizations:
>
> - **Tech Radar:** Thoughtworks' Tech Radar format (Adopt, Trial, Assess, Hold) has been adopted internally by many organizations, sometimes managed as code in Git repositories.
> - **Backstage TechDocs and Tech Radar plugin:** Spotify's Backstage supports custom Tech Radar visualizations and documentation, making technology guidance discoverable through the developer portal.
> - **ADRs (Architecture Decision Records):** The practice of recording architectural decisions as versioned documents (in Git, alongside code) has become widespread, providing the same "full history" benefit that recommend_tech offers.
> - **Platform engineering:** The emergence of platform teams has created an organizational home for technology guidance, where the platform team maintains the "golden path" and recommended technologies while still allowing teams to diverge when justified.

---

## Conclusion

The chapter concludes that the techniques described enable every new learning to be incorporated into the collective knowledge of the organization. This is done through:
- Actively and widely communicating new knowledge (chat rooms)
- Technology such as architecture as code
- Shared source code repositories
- Technology standardization

By doing this, "we elevate the state of the practice of not only Dev and Ops but also the entire organization, so everyone who performs work does so with the cumulative experience of the entire organization."

> **[Insight]** The chapter's mechanisms can be placed on a spectrum from low-friction/low-structure to high-friction/high-structure:
>
> 1. **Chat rooms** (lowest friction) — Knowledge is shared as a byproduct of doing work. No extra effort required.
> 2. **Shared source code repositories** — Knowledge is encoded in code. Requires engineering discipline but propagates automatically.
> 3. **Codified non-functional requirements** — Knowledge is encoded in standards. Requires organizational agreement but ensures consistency.
> 4. **Technology standardization** (highest structure) — Knowledge is encoded in organizational policy. Requires governance but maximizes operational efficiency.
>
> The most effective organizations use all four, applying the appropriate mechanism to the appropriate type of knowledge. Not every learning needs to become a policy, but every policy should be discoverable and understandable.

---

## How Generative AI Is Reshaping Knowledge Propagation

> **[GenAI + Chapter 20 Concepts]** The core challenge of this chapter — converting local knowledge into globally accessible knowledge — is the exact problem that Generative AI is uniquely positioned to address. Here is how:

### GenAI and ChatOps Evolution

The ChatOps model (automation in chat) is evolving into **"AI teammates in chat"**:

- **AI-powered incident response:** During an incident, an AI assistant in Slack can automatically pull relevant runbooks, suggest diagnostic commands, surface similar past incidents, and draft customer communications — all within the shared chat context.
- **Conversational knowledge retrieval:** Instead of searching wikis or post-mortem databases, engineers can ask an AI assistant, "What happened the last time the payment service had elevated error rates?" and get a synthesized answer from multiple sources.
- **Automated context capture:** AI can summarize long incident threads into structured incident reports, capturing knowledge that would otherwise be lost in chat noise.

### GenAI and Shared Code Repositories

AI is augmenting the shared repository model:

- **AI-powered code search:** Instead of keyword search across the monorepo, AI can understand intent — "find the library that handles rate limiting for gRPC services" — and return relevant results even if the code does not use those exact terms.
- **Automated library recommendations:** AI can suggest existing shared libraries when a developer starts writing code that duplicates existing functionality — "it looks like you're implementing retry logic; the resilience library in /shared/lib/resilience already provides this with circuit breakers and exponential backoff."
- **Automated dependency updates:** AI can analyze changelogs, breaking changes, and migration guides to generate pull requests that upgrade dependencies across the organization — the library ownership model described in this chapter, automated.

### GenAI and Non-Functional Requirements

- **Automated compliance checking:** AI can analyze a service's codebase and flag non-functional requirement gaps — "this service does not implement health checks, does not emit OpenTelemetry traces, and has no circuit breakers."
- **Scaffolding and golden paths:** AI can generate service templates that are pre-configured with all required non-functional requirements, customized for the specific use case.

### GenAI and Technology Governance

- **AI-assisted decision analysis:** When an engineer proposes a new technology, AI can analyze the existing technology landscape, identify similar tools already in use, assess compatibility with existing infrastructure, and surface risks — providing data-driven input to the governance discussion.
- **Automated Tech Radar updates:** AI can analyze dependency trends, community activity, security vulnerability patterns, and internal usage to suggest technology disposition changes.

### The Meta-Question: Does AI Make Knowledge Propagation Automatic?

Partially. AI dramatically reduces the friction of knowledge discovery and application. But the foundational practices in this chapter remain essential:

- **Knowledge must be captured before AI can surface it.** If retrospectives are not written, AI has nothing to search. If standards are not codified, AI has nothing to recommend.
- **Knowledge must be structured to be useful.** A well-organized shared repository with clear ownership is more valuable to AI than a disorganized wiki with stale, contradictory information.
- **Human judgment remains essential.** AI can suggest that a library exists for a given problem, but the engineer must decide whether it fits their specific context. AI can surface similar past incidents, but the team must interpret the relevance.

AI is a force multiplier on the knowledge propagation mechanisms described in this chapter — but those mechanisms must exist first.

**Further reading:**
- [Backstage by Spotify](https://backstage.io/) — open-source developer portal for knowledge discovery and service catalog
- [OpenTelemetry](https://opentelemetry.io/) — standard for production telemetry (traces, metrics, logs)
- [Open Policy Agent](https://www.openpolicyagent.org/) — policy as code framework
- [SLSA Framework](https://slsa.dev/) — supply chain security framework
- [ADR GitHub Organization](https://adr.github.io/) — Architecture Decision Records standards and tools
- [Thoughtworks Tech Radar](https://www.thoughtworks.com/radar) — model for technology governance visualization
- [Google SRE Book — Production Readiness Reviews](https://sre.google/sre-book/evolving-sre-engagement-model/) — formalized non-functional requirement reviews
