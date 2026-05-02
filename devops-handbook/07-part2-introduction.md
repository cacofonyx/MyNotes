# Part II: Introduction — Where to Start

> **Part II — Where to Start**

Part II of *The DevOps Handbook* shifts from the theoretical foundations of Part I (the Three Ways) to the practical question every organization faces: **where do we actually begin a DevOps transformation?** This introduction frames the five core concerns that the following chapters address, providing a roadmap for moving from "we understand DevOps principles" to "we are actively transforming a specific value stream."

## Table of Contents

- [The Central Questions](#the-central-questions)
- [The Five Primary Focuses](#the-five-primary-focuses)
  - [Selecting Which Value Streams to Start With](#selecting-which-value-streams-to-start-with)
  - [Understanding the Work in Our Candidate Value Streams](#understanding-the-work-in-our-candidate-value-streams)
  - [Designing Our Organization and Architecture with Conway's Law](#designing-our-organization-and-architecture-with-conways-law)
  - [Enabling Market-Oriented Outcomes](#enabling-market-oriented-outcomes)
  - [Protecting and Enabling Our Teams](#protecting-and-enabling-our-teams)
- [Embracing Uncertainty](#embracing-uncertainty)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping "Where to Start"](#how-generative-ai-is-reshaping-where-to-start)
  - [GenAI and Value Stream Selection](#genai-and-value-stream-selection)
  - [GenAI and Organizational Design](#genai-and-organizational-design)
  - [GenAI and Transformation Planning](#genai-and-transformation-planning)

---

## The Central Questions

The introduction opens with four interrelated questions that define the scope of Part II:

1. **Where** do we start a DevOps transformation in our organization?
2. **Who** needs to be involved?
3. **How** should we organize our teams?
4. How do we **protect their work capacity** and **maximize their chances of success**?

These questions are deceptively simple. In practice, they force organizations to confront deeply embedded assumptions about team structure, funding models, governance processes, and the relationship between business strategy and technology execution. Part II provides structured frameworks for answering each one.

> **[Insight]** These four questions mirror a pattern seen in any complex change initiative: scope (where), stakeholders (who), structure (how to organize), and sustainability (how to protect and grow). The order matters. You must select the right scope before identifying stakeholders, because the value stream you choose determines who is involved. You must know who is involved before designing the team structure, because the existing relationships and skills of the people constrain what structures are feasible. And you must have a viable structure before you can protect and enable the team, because protection mechanisms (dedicated time, separate physical or virtual space, executive air cover) must be tailored to the specific organizational context. Skipping any step leads to the common failure modes: transforming "everywhere at once" (wrong scope), leaving out critical stakeholders (wrong people), imposing a structure that doesn't fit (wrong design), or starving the initiative of resources (no protection).

---

## The Five Primary Focuses

The introduction identifies five primary areas that Part II's chapters will address:

### Selecting Which Value Streams to Start With

The first step is evaluating the value streams across the organization and choosing the right one to begin the transformation. This involves assessing greenfield vs. brownfield services, systems of engagement vs. systems of record, and the risk/reward balance of each candidate. The goal is to pick a starting point that maximizes the probability of early success while minimizing organizational disruption.

> **[Deep Dive: Why "Where to Start" Is the Highest-Leverage Decision]**
>
> The choice of initial value stream has a cascading effect on every subsequent decision:
>
> | Starting Choice | Consequence |
> |----------------|-------------|
> | **Too ambitious** (core revenue system, massive monolith) | High risk of failure, long time to first win, potential to discredit the entire initiative |
> | **Too trivial** (internal tool nobody cares about) | Easy win but no credibility — leadership dismisses it as irrelevant |
> | **Right-sized** (meaningful business impact, sympathetic team, manageable scope) | Quick wins build credibility, lessons learned transfer to harder problems |
>
> The "Goldilocks zone" for a starting value stream has three properties: (1) it matters enough that success will be noticed, (2) the team is willing and capable, and (3) the technical complexity is manageable within a 3-6 month horizon. This is why the book devotes an entire chapter (Chapter 5) to this decision.

### Understanding the Work in Our Candidate Value Streams

Once a value stream is selected, the next step is to deeply understand how work actually flows through it. This means identifying all the steps, handoffs, wait times, and rework loops — typically through value stream mapping exercises. The goal is to make the invisible work visible so that improvement efforts target the real bottlenecks, not the perceived ones.

### Designing Our Organization and Architecture with Conway's Law

Conway's Law states that organizations design systems that mirror their own communication structures. Part II addresses how to design both the organizational structure and the technical architecture in concert, so that teams can work independently and deliver value without excessive coordination overhead.

> **[2024+ Context]** Conway's Law has been formalized and operationalized through *Team Topologies* (Skelton & Pais, 2019), which provides four fundamental team types (stream-aligned, enabling, complicated-subsystem, and platform) and three interaction modes (collaboration, X-as-a-Service, facilitating). The DORA 2023 and 2024 reports found strong correlations between Team Topologies-style organizational design and high delivery performance. Organizations that align their team boundaries to their architecture boundaries — and vice versa — consistently outperform those that don't. This makes the "design our organization and architecture" focus area arguably the most consequential of the five, because getting it wrong creates structural impediments that no amount of tooling or process improvement can overcome.

### Enabling Market-Oriented Outcomes

Rather than organizing around technology functions (a "Dev team" and an "Ops team"), Part II advocates organizing around market-oriented outcomes — enabling cross-functional collaboration throughout the entire value stream. This means breaking down silos so that the people building, testing, deploying, and operating a service all share accountability for delivering value to the customer.

### Protecting and Enabling Our Teams

Transformation teams need protection from the gravitational pull of daily operations. This means dedicated time allocations, executive sponsorship, and organizational structures that shield the transformation effort from being consumed by urgent-but-not-important work.

> **[Insight]** The five focuses form a logical sequence: **Select** (where) -> **Understand** (what work) -> **Design** (how to organize) -> **Enable** (cross-functional collaboration) -> **Protect** (sustainability). Each step depends on the previous one. You cannot design the right team structure (step 3) without first understanding the work (step 2), because the work determines what skills and roles are needed. You cannot protect the team (step 5) without first enabling cross-functional collaboration (step 4), because a team that is organizationally isolated from the functions it depends on will be blocked regardless of how much "protection" it has. This sequence is the blueprint for the chapters that follow.

---

## Embracing Uncertainty

The introduction closes with an honest acknowledgment:

> "Beginning any transformation is full of uncertainty — we are charting a journey to an ideal end state but where virtually all the intermediate steps are unknown."

This is a critical framing statement. The authors are telling readers to expect ambiguity and to embrace an iterative, experimental approach rather than seeking a detailed, step-by-step plan. The chapters that follow provide "a thought process to guide your decisions, provide actionable steps you can take, and illustrate case studies as examples" — not a rigid prescription.

> **[Deep Dive: The Transformation as a Value Stream Itself]**
>
> There is an elegant recursion here: the DevOps transformation *itself* should follow DevOps principles. Just as the technology value stream benefits from small batches, fast feedback, and continual learning, so does the transformation initiative:
>
> | DevOps Principle | Applied to the Transformation |
> |-----------------|-------------------------------|
> | **Small batch sizes** | Start with one value stream, not the whole organization |
> | **Fast feedback** | Set short iteration cycles (2-4 weeks), measure progress, adjust |
> | **Make work visible** | Track transformation goals on a visible board, not in someone's head |
> | **Reduce WIP** | Don't run five transformation initiatives simultaneously |
> | **Continual learning** | Treat each iteration as an experiment; document what worked and what didn't |
>
> This is why the introduction emphasizes that "virtually all the intermediate steps are unknown." The authors are not being vague — they are applying the Third Way (continual learning and experimentation) to the transformation itself. You cannot plan a transformation in advance any more than you can plan a product in advance. You discover the right approach through disciplined experimentation.

> **[Insight]** The "uncertainty" framing is also a subtle warning against a common organizational pattern: the "transformation plan." Many organizations respond to a DevOps mandate by producing a detailed 18-month plan with Gantt charts, milestones, and resource allocations — essentially applying waterfall thinking to the transformation itself. This plan gives leadership a false sense of control but almost never survives contact with reality. The alternative, which Part II advocates, is to have a clear direction (the ideal end state) and a disciplined process for iterating toward it (select, understand, design, enable, protect, experiment, learn, repeat). The plan is the process, not the document.

> **[2024+ Context]** The concept of "transformation as product" has gained significant traction since this edition was published. Organizations like Adidas, ING, and Capital One now treat their DevOps/platform engineering transformations as products with their own product managers, backlogs, and user research (where the "users" are internal engineering teams). The Platform Engineering community (platformengineering.org) has formalized this: an Internal Developer Platform (IDP) is a product, and the platform team applies product thinking — user interviews, MVPs, iteration, metrics — to building and evolving it. This is the natural extension of the "transformation as value stream" idea: if the transformation is a value stream, then the output of that value stream (the platform, the practices, the tooling) is a product that serves internal customers. The CNCF Platforms White Paper (2023) codified this further, recommending that platform teams treat developers as customers and measure platform adoption, satisfaction, and impact on delivery metrics.

---

## Conclusion

Part II's introduction is deliberately brief — it is a signpost, not a destination. Its value lies in three things:

1. **Framing the right questions:** Where, who, how to organize, and how to protect. These four questions structure everything that follows.
2. **Identifying the five focus areas:** Select, understand, design, enable, protect. These map directly to the subsequent chapters.
3. **Setting expectations:** The transformation will be uncertain, iterative, and experimental. There is no master plan. There is a disciplined process for discovering the right path.

The introduction prepares the reader for the shift from theory (Part I) to action (Part II) by making clear that action does not mean abandoning the principles — it means applying them, starting with the transformation itself.

---

## How Generative AI Is Reshaping "Where to Start"

> **[GenAI + Part II Introduction Concepts]** The five focus areas identified in this introduction — selecting a value stream, understanding the work, designing org/architecture, enabling collaboration, and protecting teams — are all being influenced by Generative AI in ways that are worth examining.

### GenAI and Value Stream Selection

AI-powered engineering intelligence platforms (Jellyfish, LinearB, Faros AI, Pluralsight Flow) can now analyze data from Jira, GitHub, CI/CD systems, and incident management tools to automatically identify candidate value streams for transformation. Instead of relying solely on qualitative assessment ("which team seems most receptive?"), organizations can use quantitative signals:

- Which value streams have the highest deployment lead times?
- Which have the most rework (lowest %C/A equivalent)?
- Which have the greatest gap between team throughput and business demand?

This data-driven approach to value stream selection reduces the risk of choosing the wrong starting point and makes the case for transformation more compelling to skeptical stakeholders.

### GenAI and Organizational Design

AI tools can now analyze communication patterns (from Slack, email, meeting calendars) to map actual organizational topology — revealing the *de facto* communication structure rather than the *de jure* org chart. This is Conway's Law made measurable. Tools like DX (formerly Plandek) and Waydev can identify:

- Which teams are tightly coupled (high coordination overhead)?
- Where are the communication bottlenecks?
- Which teams operate most independently?

This data directly informs the organizational design decisions that Part II's chapters address, providing an empirical foundation for what has traditionally been a judgment-based exercise.

### GenAI and Transformation Planning

Perhaps the most transformative application: AI can help organizations iterate faster on their transformation plans by:

- **Analyzing retrospective data** across teams to identify common impediments and successful patterns
- **Generating experiment hypotheses** based on value stream metrics ("teams with >3 day code review wait times might benefit from pair programming — here are 5 teams matching that pattern")
- **Predicting transformation resistance** by analyzing sentiment in team communications and survey data
- **Synthesizing lessons learned** across multiple transformation initiatives within the same organization

The "uncertainty" the authors acknowledge becomes more manageable when AI can process the signals from early experiments and suggest course corrections faster than manual analysis allows.

**Further reading:**
- [Team Topologies — Key Concepts](https://teamtopologies.com/key-concepts) — organizational design patterns that operationalize Part II's "design our organization and architecture" focus
- [CNCF Platforms White Paper](https://tag-app-delivery.cncf.io/whitepapers/platforms/) — treating the transformation output (the platform) as a product
- [Platform Engineering Community](https://platformengineering.org/) — community and resources for teams building Internal Developer Platforms
- [DORA Quick Check](https://dora.dev/quickcheck/) — free tool to measure current state before selecting a transformation starting point
- [Value Stream Management Consortium](https://www.vsmconsortium.org/) — resources for value stream identification and mapping
