# Chapter 15: SRE/Platform Engineering for IGA — Advanced

> *"Running an identity platform at scale is where SRE meets security meets compliance. The error budget math is different when a bug doesn't just show wrong data — it grants wrong access."*

---

## IGA in CI/CD: Identity-as-Code

### The Concept

Just as infrastructure has moved to IaC (Terraform, Pulumi), identity governance is moving toward declarative, version-controlled access definitions:

```
IDENTITY-AS-CODE PIPELINE:

┌────────────┐     ┌────────────┐     ┌────────────┐     ┌────────────┐
│ Developer  │     │ PR Review  │     │  IGA       │     │  Target    │
│ writes     │────▶│ (human +   │────▶│  Engine    │────▶│  Systems   │
│ access     │     │  automated │     │  applies   │     │  updated   │
│ definition │     │  checks)   │     │  changes   │     │            │
└────────────┘     └────────────┘     └────────────┘     └────────────┘

access-definitions/
├── roles/
│   ├── finance-analyst.yaml
│   ├── software-engineer.yaml
│   └── platform-sre.yaml
├── policies/
│   ├── sod-financial.yaml
│   └── sod-engineering.yaml
└── birthright/
    ├── engineering.yaml
    └── finance.yaml
```

### Example: Role Definition as Code

```yaml
# roles/platform-sre.yaml
apiVersion: iga/v1
kind: Role
metadata:
  name: platform-sre
  owner: platform-team-lead
  review-cycle: quarterly
spec:
  description: "Platform SRE team member with production access capabilities"
  eligibility:
    department: [Engineering]
    team: [Platform]
    title-contains: [SRE, "Site Reliability", "Platform Engineer"]
  entitlements:
    - system: aws
      access: platform-sre-role
      accounts: [prod, staging, dev]
    - system: kubernetes
      access: cluster-admin
      namespaces: [platform-*]
    - system: pagerduty
      access: platform-rotation
    - system: github
      access: platform-team
      permission: write
    - system: datadog
      access: platform-dashboards
  sod-exclusions:
    - cannot-hold-with: finance-admin
    - cannot-hold-with: hr-data-access
  time-bound:
    prod-access: on-call-only
```

### CI/CD Checks for Identity Changes

```
PR opened: "Add admin entitlement to contractor role"

Automated checks:
├── ✅ Schema validation (valid YAML, known fields)
├── ✅ SoD simulation (no new violations created)
├── ⚠️ Risk assessment: ELEVATED (admin access for contractors)
├── ❌ Policy check: FAILED — "Contractor roles cannot include 
│     admin-level entitlements per policy CP-003"
│
└── PR blocked. Requires security team override or policy exception.
```

### Benefits of Identity-as-Code

| Benefit | Explanation |
|---------|------------|
| Version control | Full history of role/policy changes (who, what, when, why) |
| Code review | Peer review for access changes (catches mistakes, ensures understanding) |
| Automated testing | SoD checks, policy validation before deployment |
| Reproducibility | Same definitions → same access state (no manual drift) |
| Audit trail | Git log IS the audit trail for governance decisions |
| Rollback | Bad change? `git revert` restores previous state |
| Self-service | Teams propose their own access changes via PR |

---

## Multi-Tenant Platform Operations

### Operating an IGA SaaS at Scale

Saviynt serves 500+ customers. Each is a tenant. Platform operations at this scale:

#### Tenant Isolation Tiers

```
┌─────────────────────────────────────────────────────────────────┐
│ ISOLATION TIER 1: Shared Multi-Tenant (Standard)                │
│ Most customers. Shared compute, isolated data.                   │
│ ┌────────┐ ┌────────┐ ┌────────┐ ┌────────┐                   │
│ │ Cust A │ │ Cust B │ │ Cust C │ │ Cust D │  ... 400+         │
│ └────────┘ └────────┘ └────────┘ └────────┘                   │
│ Shared: Compute, networking, base services                       │
│ Isolated: Data (DB schema/partition), config, encryption keys   │
├─────────────────────────────────────────────────────────────────┤
│ ISOLATION TIER 2: Dedicated Tenant (Premium)                     │
│ Large/regulated customers. Dedicated compute, separate DB.       │
│ ┌─────────────────────┐ ┌─────────────────────┐               │
│ │ Bank X (dedicated)  │ │ Gov Agency (dedicated)│               │
│ │ Own DB, own compute │ │ FedRAMP boundary     │               │
│ └─────────────────────┘ └─────────────────────┘               │
├─────────────────────────────────────────────────────────────────┤
│ ISOLATION TIER 3: Isolated Region                                │
│ Data residency requirements. Entire stack in specific geography. │
│ ┌───────────────┐ ┌───────────────┐ ┌───────────────┐         │
│ │ EU Region     │ │ US-Gov Region │ │ APAC Region   │         │
│ │ (Frankfurt)   │ │ (GovCloud)    │ │ (Sydney)      │         │
│ └───────────────┘ └───────────────┘ └───────────────┘         │
└─────────────────────────────────────────────────────────────────┘
```

#### Noisy Neighbor Patterns Specific to IGA

| Pattern | Example | Mitigation |
|---------|---------|-----------|
| **Cert campaign spike** | Customer A launches SOX cert → 50K items to process | Per-tenant compute quotas, priority queues |
| **Full reconciliation** | Customer B runs full import on 200 connectors simultaneously | Rate limiting per tenant at connector layer |
| **Report generation** | Customer C generates massive compliance report | Async report generation, dedicated compute |
| **Bulk provisioning** | Customer D onboards 5000 new hires (acquisition) | Queue depth limits, burst capacity |

#### Fair-Share Scheduling

```
PROVISIONING QUEUE (shared):

Priority:
├── P0: De-provisioning (security — always first)
├── P1: Real-time provisioning (user waiting)
├── P2: Bulk provisioning (batch, can wait)
└── P3: Scheduled operations (reports, recon)

Per-tenant fairness:
├── Each tenant gets baseline throughput guarantee
├── Burst above baseline: best-effort, shared pool
└── Hard cap: no tenant can consume >X% of shared capacity
```

---

## Capacity Planning for Certification Campaigns

### The Burst Problem in Detail

Certification is the #1 capacity planning challenge for IGA platforms:

```
QUARTERLY PATTERN (many customers certify in same window):

        │ Peak: 5x steady state
Load    │     ╭────╮
        │    ╱      ╲
        │   ╱        ╲    ╭────╮
        │──╱──────────╲──╱────╲──── Steady state
        │                         
        └──────────────────────────── Time
           Jan 15-Feb 15         Apr 15-May 15
           (Q4 SOX certs)        (Q1 SOX certs)

Multiple customers certify in same window because SOX deadlines
are industry-synchronized (calendar quarter boundaries).
```

### Capacity Model

```
Variables:
- T = number of tenants launching certs this quarter (~40% of base)
- U = average items per cert campaign (varies: 1K - 500K)
- C = concurrent reviewers per tenant during peak
- R = review submission rate (items/sec/reviewer)
- P = provisioning burst on cert close (revocations)

Peak sizing:
- UI/API tier: T × C × request_rate = peak requests/sec
- Database: T × U items × read_pattern = query load
- Provisioning: T × revocation_rate on cert close = burst writes
- Background jobs: T × notification_volume = email/Slack load
```

### Pre-Campaign Checklist (Operational)

Before major certification windows:
1. Scale compute tier to anticipated peak
2. Pre-warm caches for frequently accessed tenant data
3. Verify database connection pool sizing
4. Confirm connector capacity for post-campaign revocations
5. Alert thresholds adjusted (normal alerting during cert is noisy)
6. On-call briefed on expected load patterns
7. Customer success notified of maintenance windows to avoid

---

## Chaos Engineering for Identity

### Why It's Needed

IGA failures have security implications. You need confidence that:
- Connector failures don't leave accounts unrevoked
- Database failures don't result in wrong access decisions
- Queue failures don't silently drop provisioning operations
- Network partitions don't create inconsistent state between IGA and targets

### IGA-Specific Chaos Experiments

| Experiment | What You Test | What You Expect |
|-----------|--------------|-----------------|
| Kill connector X | Impact on provisioning for that target | Operations queue, retry on recovery, no data loss |
| Slow database 10x | Certification UI performance | Graceful degradation, timeout handling, no cascading failure |
| Drop provisioning queue messages | Provisioning reliability | Reconciliation catches gaps, alerts fire |
| Inject stale token for target system | Connector auth failure handling | Re-auth triggered, operations retried |
| Simulate target system returning wrong data | Import data quality | Validation catches anomalies, doesn't blindly import |
| Kill AI recommendation service | Certification without AI | Graceful fallback (show items without recommendations) |
| Partition between cert engine and provisioning | Post-cert revocation | Eventual consistency, revocations execute when partition heals |

### The Blast Radius Concern

```
CHAOS TESTING IN IGA = EXTREME CARE:

General SaaS chaos: "If we inject latency, users see slow page loads."
IGA chaos: "If we inject failures, access might be granted that shouldn't be,
            or revocations might not execute, creating security exposure."

Rules:
1. NEVER chaos test in production on provisioning paths (security risk)
2. Staging environment with synthetic tenants
3. Even in staging: verify no access state corruption after experiment
4. Read-only chaos (inject read failures) safer than write-path chaos
5. Always have kill switch to immediately stop experiment
```

---

## Developer Experience for Access

### The Problem

Traditional IGA interfaces are designed for IT admins and compliance teams. Developers hate them:
- Complex portals
- Cryptic entitlement names
- Slow approval workflows
- No integration with developer tools (CLI, IDE, Slack)

### Golden Paths for Developer Access

```
INSTEAD OF:                              GOLDEN PATH:
1. Open IGA portal                       1. Developer runs:
2. Navigate to "Access Request"             $ saviynt access request \
3. Search 10,000 items for                      --system aws \
   "AWS production"                              --account prod \
4. Fill out justification form                   --role read-only \
5. Wait 3 days for approval                      --duration 4h \
6. Get access                                    --reason "debugging INC-4521"
                                         2. Auto-approved (matches policy:
                                            read-only + time-bound + incident ref)
                                         3. Access in 30 seconds
                                         4. Auto-expires in 4 hours
```

### Platform Engineering Approach to Developer Access

| Principle | Application |
|-----------|------------|
| **Self-service** | Developers can get access without filing tickets |
| **API-first** | CLI, SDK, Slack bot — not just web portal |
| **Paved roads** | Pre-defined access patterns that are pre-approved |
| **Fast feedback** | Know in seconds if request will be approved (not days) |
| **Temporary by default** | All developer access has expiration |
| **Integrated** | Works with developer tools (kubectl plugin, Terraform provider) |

### Access Patterns That Should Be Instant

| Pattern | Why It Should Be Fast | How |
|---------|----------------------|-----|
| Read-only access to non-prod | Low risk, high frequency | Auto-approve policy |
| Time-bound prod access during incident | Time-critical, justified | Incident reference validates, auto-grant |
| Same access as teammate (onboarding) | Pre-approved via role | Birthright role assignment |
| Debug access to your own service | Ownership justifies | Service ownership lookup + auto-grant |

---

## SLIs/SLOs at Advanced Maturity

### Beyond Basics: Composite SLOs

Simple SLIs (from Chapter 10) are individual metrics. Advanced SLOs compose them:

```
COMPOSITE SLO: "Access Governance Health"

Components:
├── Provisioning Success: 99.5% of operations succeed within SLA
├── Reconciliation Coverage: 100% of connectors reconciled within 24h  
├── Data Freshness: 95% of identity changes reflected within 1 hour
├── Certification Availability: 99.9% during campaign windows
└── Security Posture: De-provisioning latency < 1 hour (p99)

Composite score: Weighted average (security gets 2x weight)
Status: GREEN / YELLOW / RED
```

### Per-Tenant SLOs

Different customers may have different SLOs based on tier:

| Tier | API Availability | Provisioning Latency | Support Response |
|------|-----------------|---------------------|------------------|
| Enterprise | 99.95% | p95 < 5 min | 15 min for P1 |
| Standard | 99.9% | p95 < 15 min | 1 hour for P1 |
| Starter | 99.5% | p95 < 60 min | 4 hours for P1 |

### SLOs That Matter Most (Ranked)

1. **De-provisioning latency** — Security exposure grows every minute
2. **Provisioning correctness** — Wrong access granted = incident
3. **API availability** — Customer integration depends on it
4. **Certification availability during campaigns** — Compliance deadlines don't move
5. **Data freshness** — Stale data = wrong governance decisions

---

## Incident Management: Identity-Specific Playbooks

### Playbook: Mass De-Provisioning Failure

```
TRIGGER: >10 de-provisioning operations stuck for >30 minutes

ASSESS:
├── How many terminated users are affected?
├── What systems still have their access?
├── Is this one connector or many?
└── Are these involuntary terminations (security-critical)?

IMMEDIATE (Severity: P1):
├── 1. Identify affected target systems
├── 2. Manually disable accounts in highest-risk systems first
│      (production, financial systems, customer data)
├── 3. Fix root cause (connector, queue, auth issue)
└── 4. Process backlog in priority order

COMMUNICATIONS:
├── Internal: Security team (exposure window)
├── Customer: "X users' de-provisioning delayed by Y minutes"
└── Compliance: May need to document as control failure

POST-INCIDENT:
├── Calculate security exposure window
├── Verify no unauthorized access occurred during window
├── Document for audit
└── Improve: monitoring, alerting, fallback procedures
```

### Playbook: Wrong Access Granted

```
TRIGGER: Provisioning granted access that violates policy/SoD

ASSESS:
├── What access was incorrectly granted?
├── To how many users?
├── For how long has incorrect access existed?
└── Has incorrect access been exercised?

IMMEDIATE (Severity: P1 Security):
├── 1. REVOKE incorrect access immediately
├── 2. Check audit logs: was incorrect access used?
├── 3. If used: escalate to security incident
├── 4. Identify root cause (policy engine bug? connector mapping error?)
└── 5. Scan for same bug pattern across other tenants

COMMUNICATIONS:
├── Security team: immediate (potential breach)
├── Customer: required disclosure (their security posture was weakened)
├── Compliance: control failure documentation
└── Legal: if customer data accessed via incorrect grant

POST-INCIDENT:
├── Full RCA with timeline
├── Impact assessment: was incorrect access exploited?
├── Fix: code fix + regression test
├── Verification: reconciliation across all affected tenants
```

---

## The Platform Engineering Maturity Model for IGA

| Level | Characteristics | Metrics |
|-------|----------------|---------|
| **1: Reactive** | Firefighting, manual operations, no SLOs | MTTR measured in hours, no error budgets |
| **2: Foundational** | Basic SLOs, monitoring, incident process | SLOs defined, MTTR < 1 hour, some automation |
| **3: Proactive** | Capacity planning, chaos testing, developer self-service | Error budgets tracked, <1 incident/month |
| **4: Predictive** | AI-assisted operations, self-healing, zero-touch deployment | MTTR < 15 min, automated scaling, zero manual toil |
| **5: Autonomous** | Platform manages itself, humans handle exceptions | Near-zero incidents, continuous optimization |

---

> **🔧 Platform Engineering Lens**
>
> This entire chapter IS the platform lens. The key takeaways:
>
> 1. **Identity-as-Code is coming** — your platform should support declarative access definitions with CI/CD integration. This is a competitive differentiator.
>
> 2. **Multi-tenant operations at this scale require mature platform engineering** — fair scheduling, isolation, burst handling. It's a distributed systems challenge with security constraints.
>
> 3. **Developer experience for access is a platform product** — not an afterthought. Self-service, API-first, integrated with developer tools.
>
> 4. **Incident playbooks for identity are DIFFERENT** — the wrong reflex (restart the service) might not apply when the issue is "wrong access was granted." Think security-first, then availability.
>
> 5. **The maturity journey** is the same as any platform team, but the CONSTRAINTS are different (security, compliance, correctness-over-speed). Let those constraints shape your priorities, not resist them.

---

## Self-Test Questions

1. What is "Identity-as-Code" and how does it benefit governance? What's needed to implement it?
2. How do noisy neighbor problems manifest differently in an IGA SaaS vs. generic SaaS?
3. Why must chaos engineering for IGA be more careful than general chaos engineering?
4. How would you design a "golden path" for developer access that's both fast AND governed?
5. What's different about incident response when the incident is "wrong access granted" vs. "service slow"?
6. Rank the SLOs for an identity platform by criticality. Defend your ranking.

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Identity-as-Code** | Declarative, version-controlled access definitions managed via CI/CD |
| **Golden Path** | Pre-approved, fast-track access pattern for common requests |
| **Fair-Share Scheduling** | Ensuring no single tenant monopolizes shared resources |
| **Chaos Engineering** | Intentionally injecting failures to test system resilience |
| **Blast Radius** | Scope of impact from a failure or incident |
| **Composite SLO** | SLO combining multiple SLIs into unified health score |
| **Per-Tenant SLO** | Different reliability targets for different customer tiers |
| **Break-glass (ops)** | Emergency procedure bypassing normal process for critical remediation |
| **Security Exposure Window** | Time during which unauthorized access exists unremediated |
| **Toil** | Repetitive manual operational work that could be automated |
