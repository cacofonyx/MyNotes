# Chapter 1: Agile, Continuous Delivery, and the Three Ways

> **Part I — The Three Ways**

This chapter lays the theoretical foundation for the entire book. It introduces the concept of value streams (borrowed from Lean Manufacturing), defines the technology value stream, establishes key metrics (lead time, process time, %C/A), and presents the Three Ways — the overarching principles from which all DevOps behaviors and patterns are derived.

## Table of Contents

- [The Manufacturing Value Stream](#the-manufacturing-value-stream)
- [The Technology Value Stream](#the-technology-value-stream)
  - [Focus on Deployment Lead Time](#focus-on-deployment-lead-time)
    - [Defining Lead Time vs. Processing Time](#defining-lead-time-vs-processing-time)
    - [The Common Scenario: Deployment Lead Times Requiring Months](#the-common-scenario-deployment-lead-times-requiring-months)
    - [Our DevOps Ideal: Deployment Lead Times of Minutes](#our-devops-ideal-deployment-lead-times-of-minutes)
  - [Observing "%C/A" as a Measure of Rework](#observing-ca-as-a-measure-of-rework)
  - [Case Study: Flow Metrics — Continuous Learning](#case-study-flow-metrics--continuous-learning)
- [The Three Ways: The Principles Underpinning DevOps](#the-three-ways-the-principles-underpinning-devops)
  - [The First Way: Flow (Left-to-Right)](#the-first-way-flow-left-to-right)
  - [The Second Way: Feedback (Right-to-Left)](#the-second-way-feedback-right-to-left)
  - [The Third Way: Continual Learning and Experimentation](#the-third-way-continual-learning-and-experimentation)
  - [Research Support for the Three Ways](#research-support-for-the-three-ways)
  - [Case Study: American Airlines' DevOps Journey (Part 1)](#case-study-american-airlines-devops-journey-part-1--new-to-second-edition-2020)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping the Three Ways and Value Streams](#how-generative-ai-is-reshaping-the-three-ways-and-value-streams)
  - [GenAI and the Technology Value Stream](#genai-and-the-technology-value-stream)
  - [GenAI and the Three Metrics](#genai-and-the-three-metrics)
  - [GenAI Applied to Each of the Three Ways](#genai-applied-to-each-of-the-three-ways)
  - [The Meta-Question: Is AI Changing the Three Ways, or Accelerating Them?](#the-meta-question-is-ai-changing-the-three-ways-or-accelerating-them)

---

## The Manufacturing Value Stream

**Core concept:** A value stream is "the sequence of activities an organization undertakes to deliver upon a customer request," or "the sequence of activities required to design, produce, and deliver a good or service to a customer, including the dual flows of information and material." — Karen Martin and Mike Osterling, *Value Stream Mapping*

- In manufacturing, the value stream is easy to see: it starts when a customer order is received and raw materials hit the plant floor.
- To achieve fast, predictable lead times, manufacturing uses:
  - **Small batch sizes**
  - **Reducing work in process (WIP)**
  - **Preventing rework** — defects must not pass to downstream work centers
  - **Constantly optimizing for global goals** (not local optimization)

> **[Deep Dive: The Four Lean Techniques Explained]**
>
> These four techniques reappear throughout the entire book. Understanding them deeply here pays dividends for every subsequent chapter:
>
> **1. Small batch sizes:** Instead of processing 100 widgets (or 100 features) at once, process 1 or 5 at a time. Counterintuitively, this *increases* throughput because: (a) defects are caught immediately rather than contaminating the entire batch, (b) each batch completes faster so value reaches the customer sooner, (c) if customer needs change mid-process, less work is wasted. In software: think "one commit, one deploy" vs. "6 months of features in one release." A useful mental model: imagine stuffing, sealing, and stamping 100 envelopes. The "big batch" approach (stuff all 100, then seal all 100, then stamp all 100) feels efficient but is slower and riskier than doing each envelope end-to-end — if you discover the address labels are wrong, you've wasted effort on all 100.
>
> **2. Reducing WIP (Work in Process):** WIP is the number of things actively being worked on simultaneously. Little's Law (a mathematical proof, not just a guideline) states: **Lead Time = WIP ÷ Throughput.** This means that for a given throughput, the *only* way to reduce lead time is to reduce WIP. If your team has a throughput of 5 features per week, having 20 features in progress means each one takes 4 weeks. Reducing WIP to 10 means each one takes 2 weeks — without anyone working faster. In practice: limit the number of open feature branches, limit the number of PRs in review, limit the number of cards in your "In Progress" column.
>
> **3. Preventing rework:** In manufacturing, if a defective part passes to the next station, it creates waste at *every downstream station* that processes it. The cost of fixing a defect grows exponentially the further it travels. In software: a bug caught in a developer's IDE costs seconds to fix. The same bug caught in code review costs minutes. In integration testing, hours. In production with customers affected, days or weeks — plus trust damage. The DevOps pipeline is designed to catch defects as early as possible: linting, unit tests, integration tests, canary deploys.
>
> **4. Optimizing for global goals:** Local optimization (making one stage faster) often hurts global performance. A classic example: if Dev produces features twice as fast but Ops can't deploy them, you've just doubled the WIP sitting between stages — increasing lead time per Little's Law. The Theory of Constraints teaches that improving anything *other than the bottleneck* is an illusion of progress. Global optimization means finding and relieving the bottleneck first.

> **[Insight]** The value stream concept is fundamental because it forces you to think end-to-end rather than locally. Most organizations optimize individual stages (faster coding, faster testing, faster approval) without realizing that 80%+ of total lead time is typically spent *waiting between stages*, not in the stages themselves. Value stream mapping makes this queue time visible for the first time — and for many teams, it's a shock to see that a "2-week feature" spent 2 days being worked on and 12 days sitting in queues.

---

## The Technology Value Stream

The same principles from manufacturing apply to technology/knowledge work. In DevOps, the **technology value stream** is defined as: **the process required to convert a business hypothesis into a technology-enabled service or feature that delivers value to the customer.**

- **Input:** A business objective, concept, idea, or hypothesis — starts when accepted into Development's committed backlog.
- **Process:** Idea → user stories / feature spec → code implementation → checked into version control → integrated and tested with the rest of the system.
- **Key insight:** Value is created only when services are running in production. So we must deliver fast flow AND ensure deployments don't cause chaos (outages, impairments, security/compliance failures).

> **[Insight]** "Value is created only when our services are running in production" is a deceptively simple statement with radical implications. It means that a feature branch sitting in a pull request is *zero value*. Code merged to main but not deployed is *zero value*. A completed sprint that hasn't reached customers is *zero value*. This reframes the entire team's definition of "done" — work isn't done when it's coded, reviewed, or merged. It's done when a customer is benefiting from it. Every stage between "committed code" and "running in production" is, from a Lean perspective, waste to be minimized.

### Focus on Deployment Lead Time

The book's primary focus is on **deployment lead time** — a subset of the full value stream:
- **Starts:** When any engineer (Dev, QA, Ops, Infosec) checks a change into version control.
- **Ends:** When that change is successfully running in production, providing value and generating feedback/telemetry.

**Two phases of work:**

| Phase | Analogous To | Characteristics |
|-------|-------------|-----------------|
| Design & Development | Lean Product Development | Highly variable, uncertain, creative, may never be repeated |
| Testing, Deployment & Operations | Lean Manufacturing | Predictable, mechanistic, minimized variability, short lead times, near zero defects |

**Goal:** Instead of large batches processed sequentially (waterfall / long-lived feature branches), have testing, deployment, and operations happening **simultaneously** with design/development. Achieved by working in small batches and building quality into every part of the value stream.

> Note: With techniques such as test-driven development, testing occurs even before the first line of code is written.

> **[Insight]** The two-phase distinction is important for setting expectations. The first phase (design/development) will always have inherent uncertainty — you can't assembly-line creative problem-solving. But the second phase (testing/deployment/operations) *can and should* be made predictable and repeatable. Many organizations make the mistake of treating the second phase as if it's also inherently unpredictable ("deployments are always risky") — when in reality, deployment unpredictability is a *solvable engineering problem*, not a fact of life. The entire deployment pipeline (Part III of this book) exists to make phase two as boring and reliable as an assembly line.

#### Defining Lead Time vs. Processing Time

Two key measures from the Lean community:

- **Lead time:** Clock starts when request is made → ends when fulfilled. *This is what the customer experiences.*
- **Process time** (a.k.a. touch time / task time): Clock starts when work actually begins → ends when complete. Omits queue/wait time.

![Figure 1.1: Lead Time vs. Process Time of a Deployment Operation](../images/Fig1-1.jpg)

> **[Deep Dive: A Worked Example of Lead Time vs. Process Time]**
>
> Consider a typical feature request flowing through a value stream:
>
> | Stage | Queue Time (Waiting) | Process Time (Working) |
> |-------|---------------------|----------------------|
> | In backlog before picked up | 5 days | — |
> | Development | — | 2 days |
> | Waiting for code review | 1.5 days | — |
> | Code review | — | 2 hours |
> | Waiting for test environment | 3 days | — |
> | QA testing | — | 1 day |
> | Waiting for change approval | 2 days | — |
> | Deployment | — | 1 hour |
> | **Totals** | **~11.5 days** | **~3.1 days** |
>
> **Total lead time:** ~14.6 days. **Total process time:** ~3.1 days.
>
> **Process efficiency:** 3.1 / 14.6 = **21%**. Meaning 79% of the time, the feature was sitting idle, waiting. And this is a *generous* example — many organizations see process efficiency below 10%.
>
> **The DevOps interventions at each wait state:**
> - Backlog wait → smaller batches, WIP limits (pull only what you can finish)
> - Code review wait → pair programming (no review queue), or async review culture with <4hr SLA
> - Test environment wait → ephemeral on-demand environments (cloud, containers)
> - Approval wait → automated compliance checks, risk-proportional approvals
> - Each intervention targets the *queue*, not the processing step — because that's where the time is.

**Key insight:** The proportion of process time to lead time is an important efficiency measure. Achieving fast flow almost always requires **reducing time work spends waiting in queues.**

> **[Insight]** In most technology organizations, process time (hands-on-keyboard time) is a tiny fraction of lead time — often less than 10-20%. The rest is queue time: waiting for code review, waiting for a test environment, waiting for approval, waiting for the deployment window. This means that the biggest gains in lead time come not from making people work faster, but from **eliminating wait states**. Automated testing eliminates the wait for QA. Self-service environments eliminate the wait for infrastructure. Trunk-based development eliminates the wait for merge resolution. This is why the DevOps approach focuses on pipeline automation and organizational design rather than individual productivity.

> **[2024+ Context]** The concept of "developer wait time" has become formalized as **Developer Experience (DevEx)**. Research by Michaela Greiler, Margaret-Anne Storey, and Abi Noda (2023) identified three core dimensions: **feedback loops** (how fast developers get information about their work), **cognitive load** (how much developers must learn and remember), and **flow state** (how often developers get interrupted). Organizations like Spotify, Google, and Netflix now have dedicated DevEx or Developer Productivity teams whose entire mission is reducing these wait states. The SPACE framework (Forsgren et al., 2021) provides a measurement model. If Figure 1.1 quantifies the problem, DevEx is the emerging discipline dedicated to solving it systematically.

> The book favors "process time" over "cycle time" to avoid confusion, following Martin and Osterling: "cycle time has several definitions synonymous with processing time and pace or frequency of output."

#### The Common Scenario: Deployment Lead Times Requiring Months

Many organizations, especially large ones with tightly coupled monolithic systems, face deployment lead times of months. Common symptoms:
- Scarce integration test environments
- Long test and production environment lead times
- High reliance on manual testing
- Multiple required approval processes

**What happens:** Heroics required at every stage. Nothing works at end of project when merging all changes together — code doesn't build, tests fail. Fixing each problem requires days/weeks of investigation. Poor customer outcomes.

![Figure 1.2: A Technology Value Stream with a Deployment Lead Time of Three Months](../images/Fig1-2.jpg)
*Source: Damon Edwards, "DevOps Kaizen," 2015*

> **[Insight]** The "big bang merge" problem described here is a direct consequence of large batch sizes. When ten developers work on separate feature branches for three months and then merge simultaneously, the combinatorial complexity of integration is enormous — any of those branches might conflict with any other. The fix isn't better merge tooling; it's *not diverging in the first place*. This is the argument for trunk-based development and continuous integration (Chapter 11): by integrating small changes frequently (daily or more), you keep the merge problem trivially small.

#### Our DevOps Ideal: Deployment Lead Times of Minutes

In the DevOps ideal:
- Developers receive **fast, constant feedback** on their work.
- They can quickly and independently **implement, integrate, validate, and deploy** code to production.
- Achieved by continually checking **small code changes** into version control, performing **automated and exploratory testing**, and deploying to production.
- High confidence changes work as designed; problems quickly detected and corrected.

**Architectural requirement:** Modular, well-encapsulated, loosely coupled architecture — small teams work with high autonomy, failures are small and contained, no global disruptions.

**Result:** Deployment lead time measured in minutes (worst case: hours).

![Figure 1.3: A Technology Value Stream with a Lead Time of Minutes](../images/Fig1-3.jpg)

> **[Insight]** Notice the phrase "independently implement, integrate, validate, and deploy." The word "independently" is carrying enormous weight. It implies that team A can deploy without coordinating with teams B, C, and D — no shared deployment windows, no cross-team integration testing, no "release trains." This level of independence requires both a loosely coupled architecture (so changes don't cascade across services) and a robust automated testing pipeline (so each team can validate their changes in isolation). When organizations say "we can't do DevOps because we have a monolith," what they really mean is "our architecture doesn't permit independent deployment." Chapter 13 addresses how to architect for this.

> **[2024+ Context]** *Team Topologies* (Skelton & Pais, 2019) gave this "independent deployment" concept a precise organizational vocabulary. Their model defines **stream-aligned teams** as the primary value-delivering unit — each owning a slice of the business domain end-to-end, able to build, test, and deploy independently. **Platform teams** provide the self-service infrastructure that makes this independence possible. The DORA 2023 report explicitly validated this: teams with low "coordination overhead" (a Team Topologies concept) had significantly better delivery performance. So the "modular, loosely coupled architecture" the authors call for here has a direct organizational counterpart: loosely coupled *teams* with well-defined interaction modes. Architecture and org design must evolve together — you can't have one without the other (which is Conway's Law, covered in Chapter 7).

---

### Observing "%C/A" as a Measure of Rework

The **third key metric** (alongside lead time and process time): **Percent Complete and Accurate (%C/A)** — reflects quality of output at each step in the value stream.

> "%C/A can be obtained by asking downstream customers what percentage of the time they receive work that is 'usable as is,' meaning that they can do their work without having to correct the information that was provided, add missing information that should have been supplied, or clarify information that should have and could have been clearer." — Karen Martin and Mike Osterling

> **[Deep Dive: How to Measure %C/A in Practice]**
>
> Imagine mapping %C/A at each handoff in a software delivery value stream:
>
> | Handoff | %C/A | Common Rework Required |
> |---------|------|----------------------|
> | Product → Dev | 60% | Ambiguous acceptance criteria, missing edge cases, unclear priorities |
> | Dev → Code Review | 75% | Missing tests, style violations, unclear commit messages |
> | Code Review → QA | 70% | Works on dev machine but not in test environment, missing test data setup |
> | QA → Ops (Deploy) | 50% | No deployment runbook, missing config for production, unclear rollback procedure |
> | Ops → Customer | 90% | Feature doesn't match what customer actually needed (a product problem, not a technical one) |
>
> **How to read this:** The QA → Ops handoff at 50% is the biggest quality bottleneck. Half the time, Ops can't deploy what they receive without going back to ask questions or fix things. This is where you'd focus improvement first.
>
> **How to collect it:** Simply ask the receiving team: "What percentage of work items that come to you are complete and usable without needing corrections?" You can do this informally in a retrospective, or formally by tracking "returned" or "rejected" items. The number doesn't need to be precise — even a rough estimate reveals where the biggest quality gaps are.
>
> **The compound effect:** If each stage has 80% %C/A across 5 stages, the end-to-end probability of a work item flowing through without any rework is 0.8⁵ = **33%**. Two-thirds of all work items hit at least one rework loop. This is why seemingly "small" quality problems at each stage create enormous systemic waste.

> **[Insight]** %C/A is a powerful metric because it measures quality from the *receiver's* perspective, not the sender's. A development team might consider a feature "done" and throw it over the wall to QA, but if QA has to send it back 40% of the time for missing test cases, unclear requirements, or broken builds, the %C/A is only 60%. Tracking this at each handoff in the value stream reveals exactly where rework is being generated — and rework is one of the largest hidden sources of waste. In practice, low %C/A at a particular handoff usually signals a missing feedback loop: the upstream team doesn't know what "good" looks like from the downstream perspective.

---

### Case Study: Flow Metrics — Continuous Learning

When measuring end-to-end value stream performance, **avoid proxy metrics** (lines of code committed, deployment frequency alone) — these reveal local optimizations but don't link to business outcomes like revenue.

**Flow metrics** (from Dr. Mik Kersten, *Project to Product*) make software delivery as visible as widgets on a production line:

| Flow Metric | Definition | What It Reveals |
|-------------|-----------|-----------------|
| **Flow Velocity** | Number of flow items completed in a set time period | Whether value delivery is accelerating |
| **Flow Efficiency** | Proportion of active work time to total elapsed time | Inefficiencies like long wait times; whether upstream work is in wait state |
| **Flow Time** | Time for a unit of business value to move through the value stream (features, defects, risks, debts) | Whether time-to-value is getting shorter |
| **Flow Load** | Number of active or waiting flow items in a value stream (similar to WIP) | Whether demand outweighs capacity; high load → reduced velocity or increased flow time |
| **Flow Distribution** | Proportion of each flow item type in a value stream | Helps adjust mix to maximize business value delivered |

> **[Insight]** Flow distribution is often the most eye-opening metric for leadership. When teams visualize what proportion of their work is features (new value) vs. defects (fixing past mistakes) vs. debt (paying down shortcuts) vs. risk (security/compliance), the typical finding is that new feature work is a much smaller share than anyone assumed — often 20-30%. The rest is "keeping the lights on." This directly connects to the downward spiral from the Introduction: as technical debt accumulates, the share of time spent on features shrinks, making it harder to deliver value, which leads to more pressure, which leads to more shortcuts, which leads to more debt. Flow distribution makes this dynamic visible and quantifiable for executive stakeholders.

> **[2024+ Context]** Kersten's Flow Framework has gained significant enterprise adoption since *Project to Product* was published. Tools like Planview Tasktop (now Planview Viz), Jellyfish, LinearB, and others now automate the collection of flow metrics by integrating with Jira, GitHub, GitLab, and CI/CD pipelines. The key evolution: organizations are now **correlating flow metrics with business outcomes** — e.g., "teams with flow efficiency >40% ship features that generate 2x more revenue." This closes the loop the book hints at: connecting technical delivery metrics to business value. The DORA 2024 report also began incorporating "value delivery" as a concept beyond the original four metrics, acknowledging that speed and stability alone don't guarantee business impact.

---

## The Three Ways: The Principles Underpinning DevOps

Presented originally in *The Phoenix Project*, the Three Ways are the set of principles from which **all observed DevOps behaviors and patterns are derived.**

![Figure 1.4: The Three Ways](../images/Fig1-4.jpg)
*Source: Gene Kim, "The Three Ways: The Principles Underpinning DevOps," ITRevolution.com, August 22, 2012*

> **[Deep Dive: The Three Ways as a System]**
>
> The Three Ways are not a menu to pick from — they are a **layered system** where each builds on the previous:
>
> ```
> Third Way: Continual Learning & Experimentation
>    ↑ requires
> Second Way: Fast Feedback (Right-to-Left)
>    ↑ requires
> First Way: Fast Flow (Left-to-Right)
>    ↑ requires
> Foundation: Visible work, version control, automated builds
> ```
>
> **Why this ordering matters:**
> - You can't get meaningful feedback (Second Way) on code that takes 3 months to deploy. The feedback is so delayed it's useless — the developer has moved on, the context is lost, and the link between cause and effect has faded. You need fast flow *first* so that feedback arrives while it's still actionable.
> - You can't build a learning culture (Third Way) without feedback loops. Organizational learning requires data about what's working and what isn't. Without production telemetry, deployment metrics, and customer feedback flowing back quickly, there's nothing concrete to learn from — just opinions and blame.
> - This explains a common failure mode: organizations try to implement blameless post-mortems (Third Way) while still deploying quarterly (broken First Way) with no production monitoring (broken Second Way). The post-mortems devolve into vague discussions because there's no data, no fast experiments, and no way to verify if improvements actually worked.
>
> **A useful analogy:** The Three Ways are like the scientific method applied to software delivery. The First Way (Flow) is conducting the experiment quickly. The Second Way (Feedback) is measuring the results. The Third Way (Learning) is forming and testing new hypotheses based on what you measured. Skip any step and you don't have science — you have guessing.

> **[Insight]** The Three Ways are presented as a hierarchy by design. You must establish Flow (First Way) before Feedback (Second Way) becomes effective, and you need both before Continual Learning (Third Way) can take hold. This isn't just theoretical — it reflects practical dependency. Fast feedback on code quality is meaningless if you can't deploy that code. Organizational learning is hollow if you don't have the feedback loops to learn from. When organizations struggle with DevOps adoption, it's often because they're trying to do Third Way activities (blameless post-mortems, improvement kata) without having established the First Way foundations (deployment pipeline, small batches). The book's structure follows this ordering for a reason.

### The First Way: Flow (Left-to-Right)

**Enables fast left-to-right flow** of work from Development → Operations → Customer.

To maximize flow:
- Make work **visible**
- Reduce **batch sizes** and intervals of work
- Build in quality — **prevent defects** from passing downstream
- Constantly optimize for **global goals**

**Benefits of speeding up flow:**
- Reduced lead time for internal/customer requests (especially code deployment)
- Increased quality of work AND throughput
- Boosted ability to innovate and out-experiment the competition

**Resulting practices:**
- Continuous build, integration, test, and deployment processes
- Creating environments on demand
- Limiting work in process (WIP)
- Building systems and organizations that are safe to change

> **[Insight]** "Make work visible" comes first for a reason. You cannot optimize what you cannot see. In manufacturing, work is physical — you can literally see inventory piling up on the factory floor. In technology, work is invisible — it lives in ticketing systems, code branches, email threads, and people's heads. Making it visible (through kanban boards, value stream maps, deployment dashboards) is the prerequisite for every other improvement. Many teams discover that simply making their work visible — without changing anything else — leads to immediate improvements, because people naturally start addressing the bottlenecks they can now see.

> **[2024+ Context]** The "make work visible" principle has spawned an entire category of engineering intelligence tools. Platforms like Backstage (Spotify's open-source developer portal), OpsLevel, Port, and Cortex provide a "single pane of glass" showing service ownership, deployment status, SLO compliance, and dependency maps. **DORA dashboards** (built into tools like Sleuth, LinearB, Faros AI, and natively in GitLab/GitHub) make the four key metrics visible in real-time. The next frontier is **AI-powered visibility**: tools that automatically detect bottlenecks, predict deployment risks, and surface anomalies in flow metrics — moving from "see the work" to "the system alerts you to where the work is stuck." The principle is unchanged; the tooling has caught up to the ambition.

### The Second Way: Feedback (Right-to-Left)

**Enables fast and constant feedback** from right to left at all stages of the value stream.

Requirements:
- **Amplify feedback** to prevent problems from recurring
- Enable **faster detection and recovery**
- Create **quality at the source**
- Generate/embed knowledge where it is needed

**Key principle:** See problems as they occur → **swarm them** until effective countermeasures are in place → continually shorten and amplify feedback loops.

**Result:** Ever-safer systems of work where problems are found and fixed long before catastrophic failure. Maximizes opportunities for organizational learning and improvement.

> **[Insight]** "Swarming" is a term borrowed from Toyota's *andon cord* practice — when a line worker detects a defect, they pull a cord that stops the entire production line until the problem is fixed. This seems wasteful (stopping the whole line for one defect?) but it's actually the opposite: it prevents the defect from propagating downstream where it becomes exponentially more expensive to fix. In software, the equivalent is stopping to fix a broken build immediately rather than working around it. The 2018 *Accelerate* research confirmed this: teams that stop and fix problems immediately (rather than scheduling them for later) have significantly better delivery performance. The short-term "waste" of stopping is dwarfed by the long-term waste of propagated defects.

> **[2024+ Context]** Modern observability platforms (Datadog, Grafana, Honeycomb, Lightstep/ServiceNow Cloud Observability) have made the Second Way's feedback loops dramatically faster and richer than what was practical when this book was written. **OpenTelemetry** (now the second-most active CNCF project after Kubernetes) has standardized how applications emit traces, metrics, and logs — making it possible to instrument once and send telemetry anywhere. The emerging concept of **Observability 2.0** (championed by Charity Majors at Honeycomb) argues for moving beyond traditional monitoring (dashboards of known-unknowns) to high-cardinality event analysis that lets you ask arbitrary questions about production behavior — finding *unknown-unknowns*. This is the Second Way's "amplify feedback" taken to its logical conclusion: not just faster alerts on known problems, but the ability to explore production behavior in real-time to discover problems you didn't know to look for.

### The Third Way: Continual Learning and Experimentation

**Enables creation of a generative, high-trust culture** that supports dynamic, disciplined, and scientific approach to experimentation and risk-taking.

Key elements:
- Facilitates **organizational learning** from both successes AND failures
- By shortening/amplifying feedback loops → ever-safer systems of work → better able to take risks and experiment → **learn faster than competition**
- Design systems of work to **multiply effects of new knowledge**: transform **local discoveries into global improvements**
- Anyone performing work does so with the **cumulative and collective experience** of everyone in the organization

> **[Insight]** "Local discoveries into global improvements" is a deceptively ambitious goal. In practice, it means that when one team discovers a better way to do database migrations, that knowledge doesn't stay locked in that team — it becomes a shared library, a platform capability, or a documented practice that every team benefits from. This is the organizational equivalent of compound interest: each improvement makes every future improvement slightly easier. The mechanisms for this (shared code libraries, internal tools platforms, internal tech talks, post-mortem repositories) are detailed in Part V. Without these mechanisms, organizations experience the frustrating pattern where the same problem is solved differently by ten different teams, and the same mistake is made independently across the organization.

> **[2024+ Context]** The "local to global" mechanism has found its most powerful modern expression in **Internal Developer Platforms (IDPs)** and **golden paths**. When a platform team encodes best practices into a self-service template (e.g., "create a new microservice" that automatically includes CI/CD, observability, security scanning, and SLO monitoring), every team that uses that template benefits from the accumulated wisdom baked into it. Backstage (Spotify), `create-react-app`-style scaffolding, and Kubernetes Operators all embody this: local discoveries codified into reusable, self-service capabilities. **AI is accelerating this further** — AI coding assistants trained on internal codebases (via retrieval-augmented generation or fine-tuning) can suggest patterns and solutions from across the organization, making "the cumulative and collective experience of everyone" more accessible than ever before. The Third Way's vision of organizational learning is becoming technically feasible at a scale the authors likely couldn't have imagined.

### Research Support for the Three Ways

The Three Ways are backed by research, not just theory:

- **Six-year study** led by co-author Dr. Nicole Forsgren (2014–2019 State of DevOps Reports, with Puppet/DORA, published in *Accelerate: The Science of Lean and DevOps*).
- Combining capabilities from all Three Ways leads to **superior outcomes for both organizations and people.**
- **Elite performers** ship software faster and more reliably, contributing to revenue, market share, and customer satisfaction.
- Elite performers are **twice as likely** to meet or exceed organizational performance goals.
- Adopting these practices shows **decreased burnout and deployment pain.**

---

### Case Study: American Airlines' DevOps Journey (Part 1) — New to Second Edition (2020)

**Context:** American Airlines started at "the very bottom, at the very beginning" — Maya Leibman, EVP and CIO, speaking at DevOps Enterprise Summit-London 2020.

**Overcoming excuses:** Early DevOps examples came from digital-native companies (Netflix, Spotify) — easy to discount ("they were born in the cloud"). But when traditional enterprises (Target, Nordstrom, Starbucks) adopted DevOps, American Airlines had no excuses left.

> **[Insight]** This "excuse pattern" is universal and worth recognizing. Every industry has its version: "We're different because we're regulated / we have legacy systems / we're not a tech company / our scale is different." The progression of DevOps adoption from digital natives (Netflix, Google) → large tech companies (Amazon, Microsoft) → traditional enterprises (Target, Nordstrom) → heavily regulated industries (banks, airlines, healthcare) systematically demolished each excuse. American Airlines is included in this book precisely because they represent the "hardest case" — a century-old, heavily regulated, safety-critical industry with massive legacy systems. If they can do it, the excuse cupboard is bare.

**Getting started — five steps:**
1. Setting concrete goals
2. Formalizing their toolchain
3. Bringing in coaches and mentors from outside the company
4. Experimenting and automating
5. Conducting immersive practical training (learn while doing)

**Ultimate goal:** Deliver value faster.

> "There were so many times when a business counterpart would bring something to the table, a new idea, and they'd say, 'Oh this is what we want to do but it's going to take IT six months or a year to get it done.' And those experiences just killed me. So the impetus behind this was really 'how do we not be the long tent pole.' We knew there was a better way of working that would help us achieve that." — Maya Leibman

**Metrics they chose to measure:**
- Deployment frequency
- Deployment cycle time
- Change failure rate
- Development cycle time
- Number of incidents
- Mean time to recover (MTTR)

> **[Insight]** Notice that their metrics are almost exactly the DORA four key metrics (deployment frequency, lead time, change failure rate, MTTR) plus two additional ones (development cycle time and number of incidents). This isn't a coincidence — the DORA metrics have become the de facto standard because research shows they are predictive of both technical performance and organizational outcomes. Starting with these metrics is a proven playbook. The value isn't just in the numbers themselves but in making them visible: teams can't argue about whether they're improving when the dashboard shows deployment frequency going from monthly to weekly.

**Early wins:** Value stream mapping helped team members understand end-to-end processes → inspired motivation → built energy around attacking and improving issues. Also conducted immersive learning across IT.

**Question 2: "Finance, friend or foe?"**

The finance approval process was cumbersome:
- No projects approved without Finance involvement
- Projects approved but no headcount added (no other priorities stopped)
- Equal scrutiny regardless of size or risk
- Equal scrutiny even for top corporate priorities with no question of being done
- Projects often completed before approved

> "I used to describe it as a process that's designed to make you give up." — Leibman

> **[Insight]** This finance approval pattern is one of the most common organizational anti-patterns in large enterprises, and it's worth pausing on. The approval process was originally designed to control risk, but it evolved into a bottleneck that applied uniform friction regardless of risk level — a $10K experiment got the same scrutiny as a $10M initiative. This is a classic case of what the Theory of Constraints calls a "policy constraint" — a human-created rule that becomes the bottleneck, as opposed to a physical or technical constraint. The solution wasn't to bypass Finance but to redesign the process so that scrutiny was proportional to risk. This pattern applies to many approval gates in the technology value stream (change advisory boards, security reviews, architecture reviews): the goal isn't to eliminate oversight but to make it risk-proportional and fast.

**Solution:** Cost mapping exercise — assigned all costs to products, including run costs. IT could see where money was actually invested; Finance gained visibility needed to trust there wasn't large waste.

**Experimentation:** Finance gave four product teams a set budget for the year. Teams defined OKRs and used budget for top priorities. Allowed testing before rollout, focused on accountability and outcomes. Finance gained even more visibility. Success → scaled new model across all products → new funding process.

![Figure 1.5: American Airlines' DevOps Transformation Journey](../images/Fig1-5.jpg)
*Source: With permission of Ross Clanton*

> "This was a huge accelerator in our journey." — Leibman

**Question 3: "How do we know what the score is?"**

Evolution over three years:
- **Year 1 (Inputs):** Learning about Agile/DevOps, focusing on products, cloud, security
- **Year 2 (Outputs):** Measuring deployment frequency, MTTR, etc.
- **Year 3 (Outcomes):** Focused on actual business outcomes: make money, improve Ops, increase LTR (loyalty/long-term revenue), reduce cost

> "In year one, one of our objectives was X% of people are going to go to Agile training. That really represents an input. In year two...the objectives sort of changed to X% of teams are going to up their agile maturity from this level to this level. And by the time we got to year three, agile wasn't even an objective anymore. We realized the inputs and outputs are great, we have to measure them, but ultimately we have to be focused on the outcome." — Leibman

> **[Insight]** The **Inputs → Outputs → Outcomes** progression is a maturity model in itself and a useful diagnostic. If your organization is measuring "number of people trained" or "percentage of teams using Jira," you're in Year 1. If you're measuring deployment frequency and MTTR, you're in Year 2. If you're measuring revenue impact, customer satisfaction, and market share, you're in Year 3. Most organizations get stuck in Year 1 or 2. The leap to Year 3 is hard because it requires connecting technical metrics to business metrics — which requires product thinking, not just engineering thinking. Leibman's observation that "agile wasn't even an objective anymore" by Year 3 is telling: the practices become invisible infrastructure, like electricity — you don't measure how much electricity you use as a goal, you measure what you accomplished with it.

> **[2024+ Context]** American Airlines' journey has continued. By 2023, they reported significant improvements in deployment frequency and cycle time at subsequent DevOps Enterprise Summit conferences. Their experience has become a reference case for the broader airline/transportation industry. More broadly, the Inputs→Outputs→Outcomes maturity progression maps well to a pattern seen across many enterprise DevOps transformations: Year 1 is about building capability and literacy, Year 2 is about measuring operational effectiveness, and Year 3+ is about connecting engineering to business strategy. Organizations in the "Year 3+" phase increasingly use **OKR frameworks** (Objectives and Key Results) to explicitly link engineering outcomes to business goals — e.g., "reduce checkout latency by 200ms" connects to "increase conversion rate by 2%." Tools like Jellyfish and Faros AI now automate this engineering-to-business alignment.

**Question 4: "What's a product?"** — Fleshing out taxonomy proved one of the most challenging moments. Many opinions, no single right answer. Decision: just get started, put something on paper, organize around it, fix as they learned.

> **[Insight]** "Just get started, put something on paper, fix it as you learn" is the improvement kata in action — and it applies not just to product taxonomy but to every aspect of a DevOps transformation. Teams that wait for the perfect organizational structure, the perfect pipeline, or the perfect metrics framework before starting will never start. The authors include this detail to normalize the messiness of real transformation: American Airlines didn't have it figured out from day one. They iterated. This is the Third Way applied to the transformation itself.

**Question 5: "Does this feel way bigger than DevOps?"** — The journey expanded beyond just DevOps. (Continued later in the book.)

**How this case illustrates the Three Ways:**
- **First Way (Flow):** Value stream mapping to optimize flow
- **Second Way (Feedback):** Selecting outcomes to measure → establish fast feedback
- **Third Way (Learning):** Immersive learning experiences → culture of continual learning and experimentation

---

## Conclusion

This chapter established:
1. **Value streams** — the concept, applied to both manufacturing and technology
2. **Lead time** — as one of the key measures of effectiveness for both manufacturing and technology value streams
3. **The Three Ways** — high-level principles underpinning all of DevOps:
   - **First Way: Flow** — fast left-to-right flow (detailed in next chapter, practices in Part III)
   - **Second Way: Feedback** — fast right-to-left feedback
   - **Third Way: Continual Learning and Experimentation** — generative, high-trust culture

> Note: Going forward in the book, "engineer" refers to anyone working in the value stream, not just developers.

---

## How Generative AI Is Reshaping the Three Ways and Value Streams

> **[GenAI + Chapter 1 Concepts]** Every concept in this chapter — value streams, lead time, %C/A, and the Three Ways — is being actively reshaped by Generative AI. Here's a concept-by-concept breakdown:

### GenAI and the Technology Value Stream

The value stream ("business hypothesis → technology-enabled service → value to customer") now has AI actors at multiple stages:

| Value Stream Stage | Traditional | With GenAI |
|---|---|---|
| **Idea → Spec** | PM writes user stories | AI helps draft specs from rough intent; AI analyzes customer data to suggest features |
| **Spec → Code** | Developer writes code | AI pair-programmer generates code from specs; developer reviews and refines |
| **Code → Tested** | Developer/QA write tests | AI generates test cases, including edge cases; AI identifies untested code paths |
| **Tested → Deployed** | Pipeline runs, human approves | AI analyzes deployment risk, auto-approves low-risk changes, flags high-risk ones |
| **Deployed → Value** | Users adopt, telemetry collected | AI analyzes user behavior patterns, auto-generates A/B test hypotheses |

**The critical implication:** AI compresses *process time* at each stage but does nothing about *queue time between stages* — unless you also redesign the flow. Organizations that adopt AI coding tools without fixing their pipeline will produce more code that waits longer. The book's emphasis on lead time over process time becomes even more relevant.

### GenAI and the Three Metrics

- **Lead time:** AI can shrink process time dramatically, but lead time only improves if queue time also shrinks. AI-powered auto-review, auto-testing, and auto-deployment are needed for lead time gains — not just AI-powered coding.
- **Process time:** This is where GenAI has the most immediate impact. Studies show 30-55% faster task completion with AI coding assistants. But per this chapter, process time is already the minority of lead time.
- **%C/A:** AI-assisted code review, AI-generated tests, and AI-powered security scanning can improve the quality of handoffs — reducing rework. But AI-generated code itself may have lower %C/A if not properly reviewed (AI hallucinations, subtle bugs, security vulnerabilities).

### GenAI Applied to Each of the Three Ways

**First Way (Flow) + AI:**
- AI-powered code generation and test generation accelerate the flow of individual work items
- AI can auto-triage and auto-fix pipeline failures, reducing the "broken build" bottleneck
- **Risk:** More code produced faster can flood the pipeline if WIP limits aren't enforced — violating the very flow principles this chapter advocates
- **Emerging pattern:** "AI-native CI/CD" where the pipeline itself uses AI to decide test scope, deployment strategy, and rollback criteria

**Second Way (Feedback) + AI:**
- AI anomaly detection in production telemetry (going beyond threshold-based alerts to pattern recognition)
- AI-generated incident summaries and root cause hypotheses during outages
- AI-powered "explain this error" tools that translate cryptic stack traces into actionable insights
- **Emerging pattern:** "AI SRE" agents that monitor production, detect anomalies, correlate across services, and draft incident response plans — compressing the feedback loop from hours to minutes

**Third Way (Continual Learning) + AI:**
- AI that analyzes post-mortem databases to surface recurring patterns across teams
- AI that synthesizes knowledge from internal wikis, Slack, and code repositories to answer "has anyone solved this before?"
- AI-powered onboarding that gives new engineers access to organizational knowledge on day one
- **Emerging pattern:** "Organizational memory AI" — systems that capture and redistribute institutional knowledge, making the Third Way's "cumulative and collective experience" searchable and queryable

### The Meta-Question: Is AI Changing the Three Ways, or Accelerating Them?

The honest answer: **accelerating, not changing.** The principles in this chapter remain fully valid. Small batches are still better than large batches. Fast feedback still beats slow feedback. Learning cultures still outperform blame cultures. AI doesn't invalidate any of this — it makes the *gap* between organizations that practice these principles and those that don't *even wider*. An organization with strong DevOps foundations gets a force multiplier from AI. An organization without them gets faster production of the same chaos.

**Further reading:**
- [Google SRE Book (free online)](https://sre.google/sre-book/table-of-contents/) — the operational practices that complement the Three Ways, especially the Second Way
- [DORA's Quick Check](https://dora.dev/quickcheck/) — free assessment tool to measure your team against the four key metrics
- [Team Topologies — Key Concepts](https://teamtopologies.com/key-concepts) — organizational design patterns for the "loosely coupled teams" this chapter advocates
- [OpenTelemetry Documentation](https://opentelemetry.io/docs/) — the standard for implementing the Second Way's telemetry and feedback loops
- [Backstage by Spotify](https://backstage.io/) — open-source developer portal implementing the "make work visible" principle of the First Way
- [The SPACE Framework Paper](https://queue.acm.org/detail.cfm?id=3454124) — measuring developer productivity beyond just delivery metrics
