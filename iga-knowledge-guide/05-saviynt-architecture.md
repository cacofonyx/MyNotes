# Chapter 05: Saviynt's Architecture & Differentiators

> *"Saviynt's bet: identity governance, privileged access, cloud security, and application governance belong in ONE platform, not four separate tools stitched together."*

---

## Enterprise Identity Cloud (EIC): The Big Picture

Saviynt's platform is called **Enterprise Identity Cloud (EIC)**. It's a converged identity security platform with four major solution areas on a single architecture:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    ENTERPRISE IDENTITY CLOUD (EIC)                    │
│                                                                      │
│  ┌──────────────┐ ┌──────────────┐ ┌──────────────┐ ┌────────────┐ │
│  │     IGA      │ │    CPAM      │ │     AAG      │ │    DSAG    │ │
│  │   Identity   │ │    Cloud     │ │  Application │ │    Data    │ │
│  │  Governance  │ │  Privileged  │ │    Access    │ │  Security  │ │
│  │    & Admin   │ │   Access     │ │  Governance  │ │  Access    │ │
│  │              │ │   Mgmt       │ │              │ │  Govern.   │ │
│  └──────────────┘ └──────────────┘ └──────────────┘ └────────────┘ │
│         │                │                 │               │         │
│  ┌──────┴────────────────┴─────────────────┴───────────────┴──────┐ │
│  │                    COMMON PLATFORM LAYER                        │ │
│  │  Identity Warehouse │ Policy Engine │ Analytics │ Connectors   │ │
│  │  Workflow Engine │ Risk Engine │ Audit/Reporting │ APIs         │ │
│  └────────────────────────────────────────────────────────────────┘ │
│                                                                      │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │                    CLOUD INFRASTRUCTURE                         │ │
│  │           Multi-tenant │ AWS/Azure hosted │ Elastic             │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

## The Four Solution Pillars

### 1. IGA (Identity Governance & Administration)

Core IGA capabilities (everything from Chapter 03):
- Identity lifecycle management
- Access request & approval workflows
- Access certifications
- Role management & mining
- SoD policy enforcement
- Provisioning & reconciliation

**Saviynt-specific:**
- "Intelligent Identity" — AI-assisted recommendations throughout
- Control Center for unified dashboards
- Out-of-the-box compliance controls (SOX, HIPAA, etc.)

### 2. CPAM (Cloud Privileged Access Management)

Privileged access for cloud environments:
- Just-in-Time (JIT) privileged access to cloud consoles
- Session recording and monitoring
- Ephemeral credentials (no standing privileges)
- Multi-cloud support (AWS, Azure, GCP)
- Kubernetes RBAC governance

**Why it's in the same platform as IGA:**
- Same identity = same governance
- Privileged access is just "higher-risk access" — same lifecycle, same certification, same SoD
- Eliminates gap between "who has regular access" (IGA) and "who has admin access" (PAM)

**Competitor comparison:** CyberArk has PAM and is adding IGA. Saviynt has IGA and includes PAM. Different starting points converging to same destination.

### 3. AAG (Application Access Governance)

Fine-grained governance WITHIN applications (not just to applications):
- SAP transaction code level governance
- Salesforce permission set analysis
- ERP role management
- Intra-application SoD (e.g., SAP SoD at transaction code level)

**Why this matters:**
- Standard IGA says "Person X has access to SAP"
- AAG says "Person X can execute transaction codes FB01 (post document), FK01 (create vendor), and ME21N (create purchase order) — and the combination of FK01 + FB01 is an SoD violation"

**Depth vs breadth:** IGA governs access TO 500 applications. AAG governs access WITHIN the most critical applications (SAP, Oracle EBS, etc.) at granular level.

### 4. DSAG (Data Security Access Governance)

Governance of access to sensitive DATA (not just applications):
- Who can access PII, PHI, financial data
- Database-level access governance
- Cloud data platform governance (Snowflake, Databricks)
- Unstructured data governance (SharePoint, file shares)

**The insight:** Traditional IGA governs application access. But the real risk is data access. You might have "SAP access" but the question is "can you see salary data in SAP?"

---

## Architecture: What "Cloud-Native" Actually Means

### Multi-Tenant SaaS

| Architecture Decision | What It Means | Why It Matters |
|----------------------|---------------|----------------|
| Multi-tenant | All customers share infrastructure (isolated at data layer) | Economics, faster updates, operational efficiency |
| SaaS-only | No on-prem deployment option | Consistent platform, no version fragmentation |
| Continuous deployment | Updates ship without customer action | Always current, no painful upgrades |
| API-first | Everything accessible via APIs | Extensible, automatable |
| Microservices | Components scale independently | Elasticity per workload type |
| Event-driven | Async processing for heavy workloads | Certification campaigns don't block provisioning |

### Contrast with Legacy Architecture

```
LEGACY (SailPoint IIQ, Oracle OIG):          CLOUD-NATIVE (Saviynt EIC):
┌──────────────────────┐                     ┌──────────────────────────┐
│  Customer Data Center │                     │   Saviynt Cloud (AWS)    │
│                       │                     │                          │
│  ┌────────────────┐  │                     │  ┌─────┐ ┌─────┐ ┌────┐│
│  │  IGA Monolith  │  │                     │  │Svc A│ │Svc B│ │Svc C││
│  │  (Java, all-   │  │                     │  └──┬──┘ └──┬──┘ └──┬─┘│
│  │   in-one)      │  │                     │     │       │       │   │
│  │                │  │                     │  ┌──┴───────┴───────┴─┐ │
│  │  - Own DB      │  │                     │  │  Shared Platform    │ │
│  │  - Own app     │  │                     │  │  (DB, Queue, Cache) │ │
│  │  - Own infra   │  │                     │  └────────────────────┘ │
│  └────────────────┘  │                     │                          │
│                       │                     │  All customers on same   │
│  Customer manages     │                     │  version, always current │
│  everything: patches, │                     └──────────────────────────┘
│  upgrades, scaling    │
└──────────────────────┘
```

### The Multi-Tenancy Model

```
┌─────────────────────────────────────────────────────────┐
│              SAVIYNT EIC (Shared Compute)                 │
│                                                          │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐              │
│  │Tenant A  │  │Tenant B  │  │Tenant C  │  ... 500+    │
│  │(Customer)│  │(Customer)│  │(Customer)│  tenants      │
│  │          │  │          │  │          │              │
│  │ Data: 🔒 │  │ Data: 🔒 │  │ Data: 🔒 │  Isolated    │
│  └──────────┘  └──────────┘  └──────────┘              │
│                                                          │
│  Shared: Compute, Workflow Engine, Connectors            │
│  Isolated: Data, Configuration, Policies                 │
└─────────────────────────────────────────────────────────┘
```

**Tenant isolation guarantees:**
- Data isolation: Each customer's identity data strictly separated
- Configuration isolation: Policies, roles, workflows are per-tenant
- Compute fairness: Noisy neighbor protections (one customer's cert campaign can't starve another)
- Compliance isolation: Some tenants in specific regions (data residency requirements)

---

## Key Technical Components

### Identity Warehouse

Central repository of ALL identity data:
- User records from all authoritative sources
- Entitlement data from all target systems
- Historical access data (who had what, when)
- Relationship mappings (user → account → entitlement → role → application)

**Think of it as:** The materialized view of identity state across the entire enterprise.

### Connector Framework

~200+ pre-built connectors to target systems. Architecture:

```
┌───────────┐     ┌───────────────┐     ┌──────────────┐
│  Saviynt  │────▶│   Connector   │────▶│   Target     │
│  Engine   │     │   (REST/SCIM/ │     │   System     │
│           │◀────│    LDAP/DB)   │◀────│   (AD/AWS/   │
└───────────┘     └───────────────┘     │    SAP/...)  │
                                         └──────────────┘
    Read/Write         Protocol            Actual system
    operations        translation           with accounts
```

More detail in Chapter 06.

### Policy Engine

Evaluates rules across all governance decisions:
- SoD policies
- Risk scoring
- Approval routing logic
- Certification scoping
- Compliance mappings

### Workflow Engine

Orchestrates multi-step processes:
- Access request → approval → provisioning → notification
- Lifecycle events → multiple system actions
- Certification campaigns → reviewer assignment → decision → action

### Risk Engine

Calculates and maintains risk scores:
- Per identity (user risk)
- Per entitlement (how dangerous is this permission)
- Per application (criticality rating)
- Composite risk (user + entitlement + application context)

Used for: Risk-based certifications, prioritized reviews, intelligent recommendations.

### Analytics & Reporting

- Out-of-the-box compliance reports (SOX, HIPAA, etc.)
- Custom dashboards
- Access intelligence (peer analysis, usage patterns)
- Audit evidence generation

---

## Saviynt's Differentiators (vs. Competition)

### 1. True Convergence

| Capability | Saviynt | SailPoint | CyberArk | Microsoft |
|-----------|---------|-----------|----------|-----------|
| IGA | ✅ Full | ✅ Full | ❌ (adding via Zilla) | ⚠️ Basic |
| PAM (Cloud) | ✅ Full | ⚠️ Partner/basic | ✅ Full (their core) | ⚠️ Basic |
| Application GRC | ✅ Full | ⚠️ Limited | ❌ | ❌ |
| Data Governance | ✅ Growing | ❌ | ❌ | ⚠️ Purview (separate) |

**The convergence argument:** One policy engine, one risk score, one identity warehouse, one audit trail — across ALL of IGA, PAM, app governance, and data governance. No integration gaps.

### 2. Cloud-Native Architecture

- Built on cloud from Day 1 (not migrated)
- No "legacy version" requiring migration support
- All customers on same version (no fragmentation)
- Elastic scaling for burst workloads (certification campaigns)

### 3. Cloud Governance Depth

Deep native understanding of cloud IAM:
- AWS IAM policies, roles, SCPs
- Azure RBAC, PIM, conditional access
- GCP IAM, organization policies
- Cross-cloud identity correlation

**Not just "connect to AWS" but "understand what IAM:PassRole means and why it's dangerous."**

### 4. FedRAMP Authorization

Certified for US government workloads. Significant barrier to entry — requires years of security assessment. Locks out competitors without it from ~$200B federal IT market.

### 5. Time-to-Value

Typical deployment timelines:
- Legacy IGA (IdentityIQ): 12-18 months to production
- Saviynt EIC: 3-6 months to production (for comparable scope)
- Difference driven by: SaaS (no infra), pre-built connectors, out-of-box analytics

---

## Deployment Model

### Standard Deployment

```
Customer Environment                     Saviynt Cloud
┌─────────────────────┐                 ┌─────────────────┐
│                      │                 │                  │
│  On-prem systems     │◀── Secure ────▶│  Saviynt EIC     │
│  (AD, SAP, Oracle)   │   Connection    │  (SaaS)          │
│                      │   (Agent-based) │                  │
│  Cloud systems       │◀── Direct ────▶│                  │
│  (AWS, Azure, SaaS)  │   API          │                  │
│                      │                 │                  │
│  HR System           │───── Feed ────▶│  (Source of       │
│  (Workday, etc.)     │                 │   truth)         │
└─────────────────────┘                 └─────────────────┘
```

**For on-prem systems:** Agent/gateway deployed in customer network, connects outbound to Saviynt cloud. No inbound firewall rules needed.

**For cloud/SaaS systems:** Direct API connectivity. Cloud-to-cloud.

**For HR feeds:** Scheduled or event-driven import of identity data from HRIS.

---

## Where Platform Engineering Fits

As a Platform/SRE leader at Saviynt, your scope likely touches:

| Area | Platform Engineering Concern |
|------|------------------------------|
| Multi-tenant infrastructure | Isolation, fair scheduling, resource limits, noisy neighbor |
| Connector reliability | Uptime, retry semantics, circuit breaking, monitoring |
| Provisioning pipeline | Queue management, latency SLOs, failure recovery |
| Data pipeline (identity warehouse) | Freshness, reconciliation accuracy, scale |
| Certification campaign engine | Burst workload handling, deadline management |
| API platform | Rate limiting, versioning, developer experience |
| Security posture | The IGA vendor must be MORE secure than customers (they trust you with their identity data) |
| Deployment pipeline | Continuous delivery to multi-tenant SaaS safely |
| Observability | Tenant-level metrics, cross-tenant aggregates, alerting |

---

> **🔧 Platform Engineering Lens**
>
> Saviynt's architecture is a **multi-tenant platform engineering challenge** with some unique twists:
>
> **What's familiar:**
> - Multi-tenant SaaS with isolation requirements (like any PaaS)
> - Microservices with async communication (standard patterns)
> - CI/CD to production multiple times per week
> - Observability, alerting, incident response
>
> **What's unique to IGA:**
> - **Security is existential:** If Saviynt is breached, attackers potentially get the keys to EVERY customer's identity infrastructure. The security bar is higher than typical SaaS.
> - **Correctness over speed:** A provisioning bug that grants wrong access = security incident at customer. This isn't a "show wrong data" bug — it's "gave someone access to production they shouldn't have."
> - **Burst patterns:** Certification campaigns create massive burst workloads (quarterly SOX certs = spike). Not steady-state traffic.
> - **Regulatory requirements on the platform itself:** FedRAMP, SOC 2, ISO 27001 for Saviynt's own infrastructure. Your platform work has compliance implications.

---

## Self-Test Questions

1. What are the four solution pillars of Saviynt EIC? How do they differ from each other?
2. What does "convergence" mean in Saviynt's strategy? Why is it better than buying separate tools?
3. How does multi-tenancy work? What's shared vs. isolated between customers?
4. Why is FedRAMP authorization a competitive moat?
5. If you're explaining Saviynt's architecture to a peer platform engineer, what are the 3 most interesting/unique aspects?
6. What makes IGA platform security concerns different from a typical SaaS product?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **EIC** | Enterprise Identity Cloud — Saviynt's converged platform |
| **CPAM** | Cloud Privileged Access Management — JIT privileged access for cloud |
| **AAG** | Application Access Governance — fine-grained intra-app governance |
| **DSAG** | Data Security Access Governance — access to sensitive data |
| **Identity Warehouse** | Central repository of all identity and entitlement data |
| **Connector** | Integration component linking EIC to a target system |
| **Multi-tenant** | Architecture where multiple customers share compute, isolated at data layer |
| **Tenant** | A single customer's isolated environment within the shared platform |
| **FedRAMP** | US government security certification for cloud services |
| **Noisy Neighbor** | One tenant's workload impacting another's performance |
| **JIT Access** | Just-in-Time — access granted only when needed, auto-expires |
