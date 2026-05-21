# Chapter 3: Developing Meaningful Service Level Indicators

> **Implementing Service Level Objectives** — Alex Hidalgo
> *User-Perspective Measurement, Measuring Many Things by Measuring Few, and Business Alignment*

This chapter is the practical heart of Part I. Hidalgo argues that SLIs are *more important than SLOs themselves* — because even without formal targets or error budgets, simply measuring your service from the user's perspective transforms how you think about reliability. He walks through the process of developing SLIs from first principles: starting with a simple request/response API, showing how six questions collapse into 1-2 measurements, then scaling to a complex retail website composed of many microservices. He closes with a powerful insight: your SLIs are probably already defined — just in different languages by different teams (user journeys, KPIs, interface tests).

## Table of Contents

- [Why SLIs Matter More Than SLOs](#why-slis-matter-more-than-slos)
- [What Meaningful SLIs Provide](#what-meaningful-slis-provide)
  - [Happier Users](#happier-users)
  - [Happier Engineers](#happier-engineers)
  - [A Happier Business](#a-happier-business)
- [Uptime vs. Availability vs. Reliability](#uptime-vs-availability-vs-reliability)
- [Developing SLIs: The Simple Service](#developing-slis-the-simple-service)
  - [Six Questions for a Request/Response API](#six-questions-for-a-requestresponse-api)
  - [Measuring Many Things by Measuring Only a Few](#measuring-many-things-by-measuring-only-a-few)
- [Developing SLIs: The Complex Service](#developing-slis-the-complex-service)
  - [Following the User Journey Through Components](#following-the-user-journey-through-components)
- [SLI Descriptions in Plain Language](#sli-descriptions-in-plain-language)
- [Business Alignment: SLIs Are User Journeys Are KPIs](#business-alignment-slis-are-user-journeys-are-kpis)

**Block types:** [Core Concept] [Worked Example] [Implementation Guide] [Common Pitfall] [Tool & Platform] [2025 Update] [Senior EM Application] [Template]

---

## Why SLIs Matter More Than SLOs

Hidalgo makes a bold claim and repeats it throughout:

> *"The single most important aspect of adopting an SLO-based approach to reliability doesn't even involve SLOs at all."*

Why SLIs rank higher:
- You can't have reasonable SLO targets without meaningful SLIs — the stack builds upward
- Even without SLOs or error budgets, user-perspective measurements are transformational
- SLIs can immediately improve alerting, incident response, and debugging
- They force you to think about users — which is valuable regardless of what you do with the data next

> *"Even if you never end up with SLO target percentages or decision making based upon error budgets, you can still think about your users."*

---

## What Meaningful SLIs Provide

### Happier Users

You're now measuring what users care about, not just what's easy to instrument. This shifts engineering attention toward user-impacting problems and away from internal metrics that may not matter.

### Happier Engineers

The key benefit for engineers: **you can stop alerting on everything else.**

> *"If you can develop meaningful SLIs, the only reason you have to wake someone up at 03:00 is when that SLI isn't performing correctly. It doesn't matter how many errors are in your logs, what latencies your database queries are currently experiencing, or how many of your jobs are currently crash-looping. If your service is still able to perform its job reliably as determined by comprehensive SLIs, then those are all problems that can wait until normal work hours."*

> **[Core Concept: SLIs as the Single Alerting Signal]**
>
> This is one of the most impactful practical outcomes of SLI adoption: reducing alert noise. Instead of alerting on dozens of infrastructure metrics (CPU, memory, disk, error logs, queue depth...), you alert on ONE thing: is the SLI degrading?
>
> The infrastructure metrics don't disappear — they become *diagnostic* tools used *after* an SLI-based alert fires. The hierarchy:
>
> ```
> SLI alert fires ("users are affected") → you investigate
>   → Dashboard shows SLI degrading
>     → You look at infrastructure metrics to find WHY
>       → CPU spike on database server is causing slow queries
>         → Fix the root cause
> ```
>
> This eliminates pages for infrastructure issues that *don't* affect users (a server at 90% CPU that's handling all requests fine) and catches issues that *do* affect users but don't show up in traditional metrics (a configuration error that returns 200 OK with incorrect data).

### A Happier Business

SLIs align engineering with product, business, and QA because they measure the same things those teams care about — just in different language. This creates cross-org alignment and enables reporting that leadership can actually use (Chapter 17).

---

## Uptime vs. Availability vs. Reliability

Hidalgo defines three commonly conflated terms:

| Term | Definition | Example |
|------|-----------|---------|
| **Uptime** | The time a service is actually *running* on a platform | Binary process is executing |
| **Availability** | The time a service is actually *able to respond* to user requests | Process is running AND accepting connections AND responding |
| **Reliability** | The time a service is actually *able to perform the duties it was designed to do* | Available AND returning correct results AND within acceptable latency AND in the right format |

A service can be *up* but not *available* (running but not accepting connections — maybe the port isn't bound). It can be *available* but not *reliable* (accepting connections but returning errors, or returning stale data, or responding too slowly).

> *"People often conflate reliability, availability, and uptime, even though they're all entirely different things."*

SLIs should measure **reliability** — the broadest and most user-relevant of the three.

---

## Developing SLIs: The Simple Service

### Six Questions for a Request/Response API

Hidalgo walks through a thought experiment: you have a simple request/response API. What do users need it to do?

| # | Question | What It Checks |
|---|----------|---------------|
| 1 | Is the service **up**? | Process is running |
| 2 | Is the service **available**? | Accepting connections from users |
| 3 | Is the service **responsive**? | Responding within acceptable time |
| 4 | Is it returning an acceptable number of **good responses** (not errors)? | Error rate is low enough |
| 5 | Are responses in the **correct format**? | Data format matches expectations (JSON, protobuf, etc.) |
| 6 | Is the **correct data** being returned? | Freshness, accuracy, relevance of payload |

### Measuring Many Things by Measuring Only a Few

Here's Hidalgo's key insight — you don't need six separate SLIs. The questions *nest*:

> *"If you can figure out a way to measure [correct data being returned], you're also measuring [correct format]. From a user's perspective, you can't possibly be receiving the correct data if the data isn't formatted in the way you expect it to be."*

The collapse:
- If correct data → then correct format → then good response → then service is available → then service is up
- Latency may need a separate measurement

**Result: 6 questions → 2 SLI measurements** (correctness + latency)

> **[Worked Example: The Collapse from Six to Two]**
>
> ```
> Questions:                           Measurements needed:
>
> 6. Correct data?    ─┐
> 5. Correct format?   │── Measure: "correct response received"    ─┐
> 4. Good responses?   │   (if data is correct, format and          │
> 2. Available?        │    response must also be correct;           ├─ SLI 1: Correctness
> 1. Up?             ─┘    if receiving responses, must be           │
>                           up and available)                        ─┘
>
> 3. Responsive?     ──── Measure: "response within threshold"     ── SLI 2: Latency
> ```
>
> This is the "measuring many things by measuring only a few" principle. By choosing the *highest-level* measurement (end-to-end correctness from the user's perspective), you implicitly cover all the lower-level concerns. The infrastructure can be on fire internally, but if users are getting correct responses quickly enough, the service is reliable.

> **[Implementation Guide: Start with These Two SLIs for Any API]**
>
> For any request/response service, you can get started with just two SLIs:
>
> **SLI 1 — Availability/Correctness:**
> ```
> good_requests / total_requests
>
> Where "good" = responded with correct status code (not 5xx)
>                AND correct data format
>                AND within correctness criteria
> ```
>
> **SLI 2 — Latency:**
> ```
> fast_requests / total_requests
>
> Where "fast" = response time ≤ threshold (e.g., 400ms)
> ```
>
> These two numbers give you a starting SLI that covers all six of Hidalgo's questions. It's not perfect — "correct status code" doesn't guarantee "correct data" — but it's a vastly better starting point than raw infrastructure metrics. Iterate from here.

---

## Developing SLIs: The Complex Service

Hidalgo scales up to a retail website with multiple microservices: load balancer → web app (multiple instances) → cache, database, user service, cart service, payment gateway → third-party payment vendor.

### Following the User Journey Through Components

Different user interactions follow different paths through the system:

| User Interaction | Components Traversed |
|-----------------|---------------------|
| Visit home page | Load balancer → web app → cache |
| Browse items | Load balancer → web app → database |
| Add/remove cart item | Load balancer → web app → cart service → cache → database |
| Edit shipping address | Load balancer → web app → user service → database |
| Purchase item | Load balancer → web app → payment gateway → third-party vendor |

Each path requires the SLI measurement to follow the *entire logical service path from start to finish* — not just one hop.

Hidalgo walks through the login flow specifically: the SLI should measure from "external request hits load balancer" to "user sees logged-in page rendered in browser" — not just "user service returns 200 to web app." The latter is a *component* metric; the former is a *user experience* metric.

> **[Common Pitfall: Measuring Components Instead of Journeys]**
>
> | What Teams Often Measure | What They Should Measure |
> |------------------------|------------------------|
> | Error rate between web app and user service | Can users actually log in end-to-end? |
> | Database query latency | Does the page load within the user's threshold? |
> | Cart service availability | Can users actually add items and see them persist? |
> | Payment gateway response time | Can users complete a purchase from click to confirmation? |
>
> Component metrics are *diagnostic* — they tell you where a problem is once you know there IS a problem. User journey SLIs are *detecting* — they tell you there IS a problem by measuring the user's actual experience.
>
> **The practical reality Hidalgo acknowledges:** Measuring complete user journeys end-to-end is hard. He explicitly says you don't have to perfectly mimic user interactions — approximations based on component metrics are often "more than good enough." The point is to *aim* for user perspective, even if your measurement is imperfect.

> **[2025 Update: Distributed Tracing Makes Journey-Based SLIs Practical]**
>
> When Hidalgo wrote in 2020, measuring end-to-end user journeys required significant custom instrumentation. By 2025:
>
> - **OpenTelemetry distributed tracing** makes it straightforward to follow a request across services and measure total journey duration and success/failure from entry to response
> - **Service mesh telemetry** (Istio, Linkerd) provides journey-level metrics without application code changes
> - **Real User Monitoring (RUM)** captures the *actual* user experience including browser rendering time — the truest SLI possible
> - **Synthetic monitoring with trace-based assertions** (Tracetest, Malabi) lets you write end-to-end tests that validate entire user journeys and produce SLI-compatible measurements
>
> The gap between "what Hidalgo recommends" and "what's practically achievable" has narrowed dramatically. Journey-based SLIs that were aspirational in 2020 are table stakes in 2025.

---

## SLI Descriptions in Plain Language

Hidalgo provides two example SLI descriptions:

**Simple API:**
> *"The 95th percentile of requests to our service will be responded to with the correct data within 400 ms."*

**Complex retail website (login):**
> *"When clients external to our network provide a valid username and password combination, the site will reload in a logged-in state."*

Both are:
- **Understandable by non-engineers** — no jargon, no technical implementation details
- **Binary** — results in "yes, this happened" or "no, it didn't"
- **User-perspective** — describes what the user experiences, not what the server does

> **[Template: Writing SLI Descriptions]**
>
> Pattern: `When [user action], [expected outcome] [within threshold]`
>
> Examples:
> - "When a user submits a search query, relevant results are displayed within 2 seconds"
> - "When an API client sends a valid request, a correct response is returned within 400ms"
> - "When a user initiates checkout, payment is processed and confirmation is displayed within 10 seconds"
> - "When an engineer triggers a deployment, the new version is serving traffic within 15 minutes"
> - "When a log event is ingested, it is searchable within 60 seconds"
>
> **The test:** Can your product manager understand this sentence? Can your VP? Can the on-call engineer at 3 AM use it to determine if there's a real problem? If yes to all three, it's a good SLI description.

---

## Business Alignment: SLIs Are User Journeys Are KPIs

Hidalgo's closing insight is one of the most strategic in the book:

> *"If you were to put that sentence [the SLI description] in front of a product manager, they might say: 'Sure, but that's not an SLI, that's a user journey.' ...And if you took that SLI description and put it in front of the business aspect of your organization, they might say: 'Sure, but that's not an SLI, that's a KPI.' ...If you described your SLI to your QA or test engineering team, they might respond with: 'We agree, but that's not an SLI, it's an interface test.'"*

| Team | What They Call It | What It Actually Is |
|------|------------------|-------------------|
| SRE/Engineering | SLI | User-perspective measurement |
| Product Management | User Journey | Same thing |
| Business/Analytics | KPI | Same thing |
| QA/Test Engineering | Interface Test | Same thing |

> *"Chances are that many people at your company or in your organization are already entirely aligned in terms of what aspects of your service need to be measured and how important those are to users. It's just likely that the language you've all been using doesn't line up exactly."*

> **[Senior EM Application: The Rosetta Stone for Cross-Org Alignment]**
>
> This is gold for a Senior EM trying to drive SLO adoption:
>
> 1. **Don't start from scratch.** Ask your product manager for their "user journeys" document. Ask QA for their "critical path tests." Ask business analytics for their "KPIs." You likely already have 80% of your SLI definitions — they're just in different formats and owned by different teams.
>
> 2. **Use shared language.** When presenting SLIs to product: "These are our user journeys, instrumented for continuous measurement." To leadership: "These are our KPIs, measured in real-time against targets." To QA: "These are our interface tests, running against production continuously." Same SLI, different framing.
>
> 3. **Create alignment, not duplication.** If product already tracks "login success rate" as a KPI and QA already tests "login flow" as an interface test, your SLI should be built *on the same measurement* — not a third, independent system. One measurement, multiple consumers (SLO dashboard, product analytics, QA reporting).
>
> 4. **Use this alignment to get buy-in.** When leadership asks "why are we investing in SLOs?", the answer is: "We're not building something new. We're connecting the user journeys that product already defined, the KPIs that business already tracks, and the tests that QA already runs into a unified system that lets us make data-driven reliability decisions. The pieces already exist — we're just connecting them."

> **[AI & Observability: AI-Assisted SLI Development]**
>
> AI tools in 2025 can accelerate the SLI development process Hidalgo describes:
>
> - **Auto-suggestion from traces:** OpenTelemetry trace data analyzed by ML to suggest "here are the most common user journeys through your system" — automatically identifies the paths Hidalgo maps manually
> - **SLI gap analysis:** AI correlates incident history with existing SLI coverage to identify "you had 12 incidents affecting checkout, but your SLIs only cover the browse and search journeys"
> - **Threshold recommendation:** ML analyzes historical latency distributions to suggest SLI thresholds — "Based on your P50 of 120ms and P99 of 800ms, a threshold of 500ms would classify 97.2% of requests as 'good'"
> - **Natural language SLI definition:** "Monitor whether users can successfully complete checkout" → AI generates the appropriate Prometheus query or Datadog SLO configuration
>
> These don't replace the human judgment Hidalgo emphasizes (understanding what users *actually* need), but they dramatically reduce the instrumentation effort that has historically been the bottleneck.

---

**Chapter 3 establishes:** SLIs are more important than SLOs. Start by asking what your users need, then identify the minimum measurements that cover all dimensions (measuring many things by measuring few). Write SLI descriptions in plain language that anyone can understand. Your SLIs likely already exist — as user journeys, KPIs, or interface tests — in other teams' documents. Connect them.

**Next: Chapter 4 — Choosing Good Service Level Objectives, where Hidalgo tackles the critical question of what percentage to target and the many trade-offs involved.**
