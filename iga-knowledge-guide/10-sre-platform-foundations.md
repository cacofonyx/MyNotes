# Chapter 10: SRE/Platform Engineering for IGA — Foundations

> *"An IGA platform IS infrastructure. It has SLOs, incidents, capacity concerns, and on-call — just like any production system. Except when it's down, people can't start their jobs and security gaps grow silently."*

---

## IGA as a Platform Product

### Who Are Your Customers?

As a Platform/SRE team at an IGA company (like Saviynt), you have TWO layers of customers:

```
┌─────────────────────────────────────────────────────────────────┐
│ LAYER 1: External Customers (Enterprises using Saviynt)          │
│                                                                  │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐    │
│  │ Customer A     │  │ Customer B     │  │ Customer C     │    │
│  │ (Bank, 50K     │  │ (Healthcare,   │  │ (Tech co,      │    │
│  │  employees)    │  │  20K employees)│  │  5K employees) │    │
│  └────────────────┘  └────────────────┘  └────────────────┘    │
│                                                                  │
│  Their users: Security teams, IT admins, managers doing certs,  │
│  end users requesting access, auditors pulling reports           │
└────────────────────────────────────────────────────┬────────────┘
                                                     │
┌────────────────────────────────────────────────────┼────────────┐
│ LAYER 2: Internal Teams (Saviynt engineering)      │            │
│                                                    ▼            │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐    │
│  │ Product Teams  │  │ Connector Team │  │ Data/AI Team   │    │
│  │ (build IGA     │  │ (integrations) │  │ (analytics,    │    │
│  │  features)     │  │                │  │  ML models)    │    │
│  └────────────────┘  └────────────────┘  └────────────────┘    │
│                                                                  │
│  They need: reliable infrastructure, CI/CD, observability,      │
│  development environments, deployment pipelines                  │
└─────────────────────────────────────────────────────────────────┘
```

### The Unique Reliability Bar

IGA platform reliability is different from typical SaaS:

| Typical SaaS | IGA Platform |
|-------------|--------------|
| User can't view dashboard → inconvenience | User can't log in to work → lost productivity ($$$) |
| Feature bug → wrong data shown | Provisioning bug → wrong access granted (security incident) |
| Downtime → users wait | Downtime during cert window → compliance deadline missed |
| Data breach → your data exposed | Data breach → ALL customers' identity data exposed |
| Outage → revenue impact | Outage → new hires can't start + terminations can't be processed (security risk) |

---

## SLIs and SLOs for an Identity Platform

### Defining SLIs (What to Measure)

| SLI | What It Measures | Why It Matters |
|-----|-----------------|----------------|
| **Provisioning latency** | Time from approval to access granted in target system | New hire waiting time, security of JIT access |
| **Provisioning success rate** | % of provisioning operations that succeed on first attempt | Reliability of the core function |
| **De-provisioning latency** | Time from termination event to ALL access revoked | Security exposure window |
| **Reconciliation freshness** | Time since last successful reconciliation per connector | How stale is our understanding of actual state |
| **API availability** | % of successful API responses (non-5xx) | Integration reliability for customers |
| **Certification page load time** | Latency for certification UI during campaigns | Reviewer experience (slow UI → rubber-stamping) |
| **Connector health** | % of connectors in healthy state (passing health checks) | Integration reliability |
| **Import success rate** | % of scheduled imports that complete without error | Data freshness and accuracy |

### Example SLOs

| Service | SLO | Budget Period | Rationale |
|---------|-----|--------------|-----------|
| Provisioning (standard) | 99% complete within 15 minutes | Monthly | New hire experience |
| Provisioning (de-provision) | 99.9% complete within 1 hour | Monthly | Security criticality |
| API availability | 99.95% uptime | Monthly | Enterprise SaaS expectation |
| Certification UI | p95 page load < 3 seconds | During campaigns | Reviewer experience |
| Connector health (top 10) | 99.9% healthy | Weekly | Core integration reliability |
| Reconciliation | Every connector reconciled within 24 hours | Daily | Data accuracy |

### Error Budgets in IGA Context

```
SLO: 99.95% API availability = 21.6 minutes downtime per month allowed

Error Budget Tracking:
┌────────────────────────────────────────────────────────────────┐
│ Month: March 2025                                              │
│ Budget: 21.6 minutes                                           │
│ Consumed: 8.3 minutes (incident on March 12)                   │
│ Remaining: 13.3 minutes                                        │
│ Status: ✅ Healthy                                              │
├────────────────────────────────────────────────────────────────┤
│ If budget exhausted:                                           │
│ → Freeze deployments (except security patches)                 │
│ → Focus on reliability improvements                            │
│ → Post-mortem required for next budget violation               │
└────────────────────────────────────────────────────────────────┘
```

**Special consideration:** During certification campaign windows, you might tighten SLOs or treat any incident as higher severity (because the compliance deadline doesn't move).

---

## Observability for IGA

### The Four Pillars Applied

#### 1. Metrics

| Category | Key Metrics |
|----------|-------------|
| **Provisioning** | Queue depth, processing rate, success/fail rate, latency histogram |
| **Connectors** | Per-connector: health, error rate, latency, last successful operation |
| **Certifications** | Campaign progress, reviewer completion rate, items processed/second |
| **Infrastructure** | CPU, memory, disk, network per service. Pod counts. DB connections. |
| **Business** | Active tenants, operations per tenant, peak concurrent users |

#### 2. Logs

| What to Log | Why |
|-------------|-----|
| Every provisioning operation | Audit trail + debugging |
| Every connector communication | Diagnosing integration failures |
| Authentication/authorization decisions | Security + debugging access issues |
| Configuration changes | Change tracking |
| Campaign lifecycle events | Compliance evidence |

**Structured logging is essential.** Every log entry should include: tenant_id, correlation_id, user_id, operation, target_system, result, duration.

#### 3. Traces

Critical trace spans for IGA:
```
Access Request Trace:
├── UI: Request submitted (50ms)
├── Policy Engine: SoD check (200ms)
├── Policy Engine: Risk scoring (100ms)
├── Workflow: Route to approver (30ms)
├── [Wait: Human approval] (hours/days — not traced)
├── Workflow: Approval received (20ms)
├── Provisioning: Queue operation (10ms)
├── Provisioning: Execute on target (varies: 200ms - 60s)
│   ├── Connector: Authenticate to target (500ms)
│   ├── Connector: Create account (2s)
│   └── Connector: Verify creation (1s)
└── Notification: Send confirmation (100ms)
```

#### 4. Alerts

| Alert | Severity | Condition |
|-------|----------|-----------|
| Provisioning queue depth > threshold | P2 | New operations not being processed |
| Connector X unhealthy > 15 min | P2/P3 | Integration failure affecting customers |
| De-provisioning backlog > 0 for > 30 min | P1 | Security exposure growing |
| API error rate > 1% for 5 min | P2 | Platform degradation |
| Certification campaign at risk (deadline approaching, <80% complete) | P3 | Compliance risk |
| Reconciliation hasn't run for connector X in 48 hours | P3 | Data staleness |
| Tenant provisioning success rate < 95% | P2 | Customer impact |

---

## Incident Patterns in IGA

### IGA-Specific Incident Types

| Incident Type | Impact | Severity Logic |
|---------------|--------|---------------|
| **Provisioning pipeline down** | New hires can't access systems | P1 if during active provisioning hours |
| **De-provisioning stuck** | Terminated employees retain access | P1 always (security) |
| **Certification platform down** | Reviewers can't complete certs | P1 if within 48h of deadline, else P2 |
| **Connector failure (single)** | One target system not synced | P2/P3 depending on customer impact |
| **Connector failure (widespread)** | Multiple connectors down | P1 (platform-level issue) |
| **Reconciliation drift detected** | IGA state doesn't match reality | P2 (investigate: drift = potential incident) |
| **Data corruption** | Identity records incorrect | P1 (wrong access decisions being made) |
| **Performance degradation** | Slow UI, slow provisioning | P2 if affects certification campaigns |

### Identity Incident vs. Security Incident

Important distinction:

| Type | Example | Response |
|------|---------|----------|
| **Identity incident** | Provisioning pipeline slow, connector timeout | Standard incident response: fix, restore |
| **Security incident** | Wrong access granted, unauthorized identity created, breach detected | Security response: contain, investigate, notify |

Sometimes an identity incident IS a security incident:
- De-provisioning failed → terminated employee still has access → security exposure
- Reconciliation finds unknown admin account → potential breach

### On-Call Considerations

IGA on-call is different from typical SaaS on-call:

**Time-sensitivity patterns:**
- Terminations: Must process immediately (security)
- New hire provisioning: Business hours critical
- Certification deadlines: Fixed, non-negotiable
- Connector health: Varies by customer criticality

**Escalation paths:**
- Security concern? → Security team immediately
- Customer compliance deadline at risk? → Customer Success + Engineering leadership
- Data integrity question? → Don't guess. Escalate before taking action.

---

## Capacity Planning for IGA

### Workload Patterns

IGA traffic is NOT steady-state. It has predictable bursts:

```
Platform Load Over Time:

     │
Load │    ┌──┐
     │    │  │     Cert            ┌──┐
     │    │  │     Campaign        │  │     Cert
     │    │  │                     │  │     Campaign
     │ ┌──┤  ├──┐              ┌──┤  ├──┐
     │ │  │  │  │              │  │  │  │
     │ │  │  │  │  ┌──┐       │  │  │  │
     │─┤  │  │  ├──┤  ├───────┤  │  │  ├──
     │ │  │  │  │  │  │       │  │  │  │
     └─┴──┴──┴──┴──┴──┴───────┴──┴──┴──┴───── Time
       Mon-Fri         Steady    Mon-Fri
       (prov)          state     (prov)
       ↑                         ↑
       Quarterly SOX cert launch
```

### Key Burst Events

| Event | Load Pattern | Planning |
|-------|-------------|----------|
| **Certification campaign launch** | Spike: 5,000+ managers access platform in days 1-3 | Pre-scale. Cache warm. |
| **Quarter start** (new hires) | Provisioning burst: 200+ new hires same week | Queue capacity, connector rate limits |
| **Mass termination event** (layoff) | De-provisioning burst: hundreds in hours | Security priority + capacity |
| **Full reconciliation** | Heavy reads against all connectors | Off-peak scheduling, rate limit management |
| **End of cert window** | Rushed reviewers + bulk actions | Peak concurrent users, revocation burst |

### Multi-Tenant Capacity

Unique challenge: you don't control customer behavior timing.
- Customer A launches cert campaign Monday
- Customer B launches cert campaign Monday too (coincidence)
- Noisy neighbor: Customer A's import job consuming connector resources

**Solutions:**
- Per-tenant resource quotas
- Priority queues (paid tier gets priority?)
- Scheduling intelligence (suggest non-peak windows for heavy operations)
- Elastic scaling with per-tenant caps
- Fair-share scheduling for shared resources (connectors)

---

## Deployment Considerations

### Continuous Delivery for Multi-Tenant SaaS

```
Code Change → CI → Tests → Canary (5% of tenants) → Gradual Rollout → Full Release
                                    │
                                    ▼
                           Monitor for:
                           - Error rate increase
                           - Latency increase
                           - Provisioning failures
                           - Customer-reported issues
                           │
                           ├── Green? → Continue rollout
                           └── Red? → Rollback automatically
```

**IGA-specific deployment risks:**

| Risk | Why It's Worse for IGA |
|------|------------------------|
| Provisioning logic bug | Might grant WRONG access (security incident, not just bug) |
| Connector regression | Silent failure = access not revoked (security) |
| Policy engine change | Might approve access that should be denied |
| Data migration error | Corrupted identity data = governance decisions on wrong info |

**Deployment guardrails:**
- Never deploy during active certification campaigns (agree per-customer)
- Canary must include provisioning validation (synthetic operations)
- Rollback must be < 5 minutes
- Feature flags for governance logic (don't flip policy behavior on all tenants at once)

---

## The SRE/Platform Team's Scope at an IGA Company

### What You Likely Own

| Domain | Responsibilities |
|--------|-----------------|
| **Infrastructure** | Cloud infra, Kubernetes, databases, networking |
| **Platform services** | Shared services: queuing, caching, storage, observability |
| **Reliability** | SLOs, error budgets, incident response, postmortems |
| **CI/CD** | Build pipelines, deployment automation, environment management |
| **Developer experience** | Dev environments, tooling, inner-loop productivity |
| **Security posture** | Infrastructure security, secrets management, compliance controls |
| **Scalability** | Capacity planning, performance, multi-tenant efficiency |

### What You Interface With

| Team | Your Touchpoint |
|------|----------------|
| Product engineering | They build features on your platform |
| Connector team | They build integrations that depend on your networking + reliability |
| Data/AI team | They need compute + data pipelines |
| Security team | They set requirements you implement |
| SRE/DevOps (customer-facing) | They manage customer deployments/onboarding |
| Customer Success | They escalate reliability issues to you |

---

> **🔧 Platform Engineering Lens**
>
> This chapter IS your lens. The key mental model shifts for IGA-specific platform engineering:
>
> 1. **Correctness > availability.** In most SaaS, showing stale data is acceptable (eventual consistency). In IGA, showing wrong access state or executing wrong provisioning is a **security incident**. Plan accordingly.
>
> 2. **Burst tolerance is critical.** Unlike steady-state APIs, IGA has predictable (certification campaigns) and unpredictable (mass terminations) bursts. Design for them.
>
> 3. **The blast radius of bugs is higher.** A bug that affects provisioning logic doesn't just break a feature — it might GRANT ACCESS that shouldn't be granted, across hundreds of customers simultaneously.
>
> 4. **Compliance is a first-class engineering concern.** Your infrastructure decisions have audit implications. Your deployment processes need to satisfy SOC 2 controls. Your incident response has compliance reporting obligations.
>
> 5. **Multi-tenancy with hostile isolation requirements.** Tenants are enterprise security teams who may be COMPETITORS with each other. Data leakage between tenants isn't just a bug — it's a breach of trust that could kill the company.

---

## Self-Test Questions

1. What makes IGA reliability requirements different from a typical SaaS application?
2. Name three SLIs specific to an identity platform (not generic SaaS SLIs).
3. Why would you treat a de-provisioning failure as a P1 security incident rather than a P2 operational incident?
4. What are the predictable burst workload patterns in IGA? How do you plan for them?
5. Why is correctness sometimes more important than availability for an IGA platform?
6. What deployment risks are unique to an IGA platform vs. generic SaaS?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **SLI** | Service Level Indicator — a quantitative measure of service behavior |
| **SLO** | Service Level Objective — target value for an SLI |
| **Error Budget** | Allowed unreliability (1 - SLO) before action triggers |
| **Multi-tenant** | Architecture where many customers share infrastructure |
| **Noisy Neighbor** | One tenant's workload degrading another's experience |
| **Canary Deployment** | Rolling change to small % of traffic first to detect problems |
| **Provisioning Pipeline** | The system that processes access grant/revoke operations |
| **Blast Radius** | Scope of impact if something goes wrong |
| **Burst Workload** | Short-duration traffic spikes (e.g., cert campaign launch) |
| **Reconciliation Freshness** | How recently the system verified actual vs. expected state |
