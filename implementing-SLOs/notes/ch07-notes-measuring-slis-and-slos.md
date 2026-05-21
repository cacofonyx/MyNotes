# Chapter 7: Measuring SLIs and SLOs

> **Implementing Service Level Objectives** — Ben Sigelman
> *Design Goals, Infrastructure Choices, and Implementation Patterns*

This chapter bridges philosophy and practice. Ben Sigelman (co-creator of Dapper and OpenTelemetry, founder of Lightstep/now ServiceNow Cloud Observability) provides a deeply technical guide to *actually implementing* SLI/SLO measurement infrastructure. He covers six design goals that should guide any implementation, describes the common observability machinery available (metrics, logs, traces), walks through implementation patterns for common-case SLIs, and discusses the general case of complex services.

This chapter assumes you've chosen *what* to measure (Chapters 1-3) and *what target* to set (Chapter 4). Now: *how* do you build the measurement system?

## Table of Contents

- [Six Design Goals for SLO Implementation](#six-design-goals-for-slo-implementation)
- [Common Machinery](#common-machinery)
  - [Centralized Time Series (Metrics)](#centralized-time-series-metrics)
  - [Structured Logging](#structured-logging)
  - [Distributed Tracing](#distributed-tracing)
- [Implementing Common-Case SLIs](#implementing-common-case-slis)
  - [Availability SLIs](#availability-slis)
  - [Latency SLIs](#latency-slis)
  - [Correctness SLIs](#correctness-slis)
- [The General Case: Complex Services](#the-general-case-complex-services)
- [Practical Considerations](#practical-considerations)

**Block types:** [Core Concept] [Implementation Guide] [Tool & Platform] [Common Pitfall] [2025 Update] [AI & Observability] [Template] [Senior EM Application]

---

## Six Design Goals for SLO Implementation

Sigelman identifies six properties that any good SLO measurement system should have:

| Design Goal | What It Means | Why It Matters |
|------------|---------------|----------------|
| **Flexible targets** | Operators can adjust thresholds, success criteria, and windows without code changes or deploys | SLOs must evolve; if changing a target requires a deploy, nobody will iterate |
| **Testable targets** | Can backtest proposed SLOs against historical data | You should never set a threshold without knowing how often it would have fired historically |
| **Freshness** | Time from real-world event to SLO reflection is minimized | For alerting: freshness must be seconds. For reporting: minutes/hours are fine. Match freshness to use case. |
| **Cost** | Implementation cost is bounded and predictable | Data engineering for org-wide SLOs can be significant, especially for high-throughput services. Plan ahead. |
| **Reliability** | SLO infrastructure is itself highly available | SLO infrastructure should be among the *most* reliable software you run. Unreliable SLO measurement = unreliable decisions. |
| **Organizational constraints** | Comply with data residency, vendor lock-in policies, and regulatory requirements | Especially in regulated industries or large orgs with data silo policies. Discover constraints EARLY. |

> **[Core Concept: "SLO Infrastructure Must Have SLOs of Its Own"]**
>
> Sigelman makes a crucial point: if your SLO measurement system is unreliable, your error budget calculations are wrong, your alerts don't fire, and your decisions are based on bad data. The monitoring system must be more reliable than the systems it monitors.
>
> If SLO infrastructure is unavailable for 30 minutes: exclude that period from SLO compliance calculations rather than counting it as "unknown" (which could falsely indicate compliance or violation).

> **[Common Pitfall: Backtesting Neglect]**
>
> One of Sigelman's most practical design goals: **testable targets.** You should never deploy a new SLO or alerting threshold without first asking "how would this have behaved over the last 30 days?"
>
> Without backtesting:
> - You set a latency threshold → it fires 200 times in the first week → alert fatigue → team mutes it
> - You set an error budget → it's violated on day 1 because the target was too ambitious → immediate loss of credibility
>
> With backtesting:
> - "At 500ms threshold, this would have fired 3 times last month — reasonable"
> - "At 99.9% target over 30 days, we would have violated 2 of the last 6 months — too strict for now, starting at 99.5%"

---

## Common Machinery

Sigelman describes three categories of observability infrastructure, each with different strengths for SLO measurement:

### Centralized Time Series (Metrics)

The most common foundation for SLIs. Pre-aggregated numerical data collected at regular intervals.

**Strengths for SLOs:** High compression, cheap at scale, native support for rates/percentiles/aggregations, purpose-built for dashboards and alerting.

**Weaknesses:** Low cardinality (can't easily break down by individual user, request ID, etc.), pre-aggregation loses detail, retroactive re-analysis is limited.

**Tools:** Prometheus, Datadog, Grafana Mimir, Google Cloud Monitoring, CloudWatch Metrics

### Structured Logging

Individual event records with rich context. Each log entry represents one request/event with full details.

**Strengths for SLOs:** High cardinality (can filter by user, endpoint, region, etc.), retroactive analysis is easy (just re-query), can answer "why" not just "what."

**Weaknesses:** Expensive at scale (every event stored individually), slower to query for aggregations, requires more compute for real-time SLI calculation.

**Tools:** Splunk, Elasticsearch/OpenSearch, Datadog Logs, Google Cloud Logging, Honeycomb

### Distributed Tracing

End-to-end request traces showing how a single request flows across services.

**Strengths for SLOs:** Perfect for journey-based SLIs (Ch3's ideal), shows causality across services, measures true end-to-end latency.

**Weaknesses:** Sampling required at high traffic (not all requests traced), complex instrumentation, newer/less mature tooling ecosystem.

**Tools:** OpenTelemetry (the standard), Jaeger, Zipkin, Datadog APM, Honeycomb, Grafana Tempo

> **[2025 Update: The Observability Landscape Has Consolidated]**
>
> When Sigelman wrote in 2020, the observability space was fragmented. By 2025:
>
> | 2020 State | 2025 State |
> |-----------|------------|
> | Metrics, logs, and traces as separate pillars with separate tools | **OpenTelemetry** unifies all three under one SDK, one collector, one format |
> | Choosing between Prometheus OR Datadog OR Cloud Monitoring | Multi-backend architectures common: OTel Collector sends to Prometheus for metrics AND Jaeger for traces AND Loki for logs |
> | Tracing required manual instrumentation | OTel auto-instrumentation for all major languages — trace generation with zero code changes |
> | SLO calculation required custom code | Native SLO features in Datadog, Grafana Cloud, Google Cloud, Nobl9 — click-to-create SLOs from existing metrics |
> | High cost of storing everything | eBPF-based observability (Pixie, Groundcover) provides kernel-level telemetry without per-event storage cost |
>
> **The practical implication:** If you're implementing SLOs today, start with OpenTelemetry instrumentation + a platform that natively supports SLO calculation. The "build from scratch on Prometheus recording rules" approach from 2020 still works but is no longer the lowest-effort path.

> **[Tool & Platform: Choosing Your SLI Data Source]**
>
> | SLI Type | Best Data Source | Why |
> |---------|-----------------|-----|
> | **Availability** (% of requests without errors) | Metrics (counters at load balancer or application) | High throughput, cheap, real-time |
> | **Latency** (% of requests under threshold) | Metrics (histograms) or Traces (span duration) | Histograms for aggregates; traces for per-request detail |
> | **Correctness** (% of responses with correct data) | Structured logs or Traces with payload inspection | Requires event-level detail to determine correctness |
> | **Freshness** (% of data within age threshold) | Custom probes or structured logs | Often requires synthetic measurement or timestamp comparison |
> | **End-to-end user journey** | Distributed traces or RUM | Only traces/RUM capture the full user-perspective journey across services |

---

## Implementing Common-Case SLIs

### Availability SLIs

The simplest SLI: ratio of successful responses to total responses.

```
availability_sli = requests_without_error / total_requests
```

**Where to measure:** As close to the user as possible.
- Best: Load balancer access logs (captures all requests, including those that never reach your app)
- Good: Application-level response codes
- Acceptable: Internal service-to-service error rates

**What counts as "error":**
- HTTP 5xx → always an error (server-side failure)
- HTTP 4xx → usually NOT counted (client error, not your reliability)
- HTTP 429 → debatable (rate limiting protects the service but denies user request)
- Timeout → error from user's perspective even if server thinks nothing went wrong

### Latency SLIs

Ratio of "fast enough" requests to total requests.

```
latency_sli = requests_under_threshold / total_requests
```

**Key decisions:**
- What threshold? (From user research and historical percentile analysis — Ch4)
- What percentile? (P95? P99? Multiple?)
- Where to measure? (Client-side includes network; server-side is what you control)

**Histogram-based implementation:** Most metrics systems support histograms that pre-bucket latency values, making it easy to calculate "% under threshold" without storing every individual request.

### Correctness SLIs

The hardest to implement. Requires some way to verify that the response content is *correct*, not just successful.

Approaches:
- **Semantic checks in the application** — application-level validation that response makes sense
- **Probe-based verification** — synthetic requests with known expected answers
- **Data comparison** — compare response data against source of truth
- **User feedback signals** — error reports, retry behavior, abandonment

---

## The General Case: Complex Services

For complex multi-service systems, Sigelman notes that the common-case patterns (availability, latency) rarely capture the full reliability picture. You need:

1. **Multi-signal SLIs** — combining availability AND latency AND correctness into a composite signal
2. **Journey-level measurement** — tracing a request across multiple services
3. **Synthetic + real traffic** — synthetics for coverage during low-traffic periods, real traffic for accuracy during peak

The key trade-off: **coverage vs. accuracy.** Synthetic probes give you guaranteed coverage (they run even when no real traffic exists) but may not represent real user behavior. Real-traffic measurement is maximally accurate but has gaps during quiet periods.

---

## Practical Considerations

Sigelman closes with real-world implementation advice:

- **Start with what you have.** Don't build new infrastructure before implementing SLOs on existing metrics.
- **Use existing high-availability infrastructure.** Don't put SLO calculations on a cron job that nobody monitors.
- **Plan for organizational constraints early.** Data residency, vendor policies, and regulatory requirements will constrain your choices. Discover them before you're 3 months into implementation.
- **Cost will surprise you.** High-cardinality SLI data (individual request correctness) can be expensive at scale. Budget for it or accept lower-fidelity measurement.
- **Freshness requirements drive architecture.** If you need sub-minute freshness for alerting, your data pipeline must be streaming, not batch.

> **[Senior EM Application: The "Start with What You Have" Principle]**
>
> Sigelman's most practical advice: don't let perfect infrastructure prevent you from starting.
>
> | If you have... | You can immediately measure... |
> |---------------|-------------------------------|
> | Load balancer logs | Availability SLI (success/error rates) |
> | Application metrics with histograms | Latency SLI (% under threshold) |
> | Distributed tracing (even sampling) | Journey-level SLIs with some approximation |
> | Only basic uptime monitoring | Start there. Binary up/down → availability percentage. Iterate. |
>
> You don't need OpenTelemetry, Nobl9, and a custom data pipeline to start. You need one metric, one threshold, and the willingness to observe it for a month. Everything else is iteration.

> **[AI & Observability: AI for SLI Implementation (2025)]**
>
> AI is reducing the implementation burden Sigelman describes:
>
> - **Auto-instrumentation:** OTel auto-instrumentation + AI-suggested metric selection means less custom code
> - **Threshold suggestion:** ML analyzes historical latency distributions and suggests optimal thresholds
> - **Anomaly-based SLIs:** Instead of fixed thresholds, ML learns "normal" and flags deviations — adapts automatically to service changes
> - **SLI validation:** AI compares SLI signal with incident history to validate: "Your SLI would have caught 85% of past incidents. Here's what it misses."
> - **Cost estimation:** AI projects data volume and storage costs for proposed SLI implementations before you commit resources

---

**Chapter 7 establishes:** SLO implementation needs six design goals (flexible, testable, fresh, cost-effective, reliable, constraint-aware). Use existing observability infrastructure (metrics for availability/latency, logs for correctness, traces for journeys). Start with what you have. Don't let perfect be the enemy of good. SLO infrastructure must itself be highly reliable.

**Next: Chapter 8 — SLO Monitoring and Alerting (Niall Murphy), covering burn-rate alerting, multiwindow alerts, and the alerting philosophy that makes error budgets operationally useful.**
