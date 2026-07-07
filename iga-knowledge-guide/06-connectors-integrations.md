# Chapter 06: Connectors & Integrations

> *"An IGA platform is only as good as its connectors. You can have the most beautiful governance engine in the world — if it can't reliably talk to AD, SAP, and AWS, it's useless."*

---

## What Is a Connector?

A connector is the integration layer between the IGA platform and a target system. It translates IGA operations (create account, grant permission, revoke access, read current state) into the specific protocol and API the target system understands.

```
┌──────────┐         ┌──────────────┐         ┌──────────────┐
│  IGA     │  IGA    │  Connector   │  Target  │   Target     │
│  Engine  │  API    │              │  Protocol│   System     │
│          │────────▶│  - Translate │─────────▶│              │
│  "Create │         │  - Error     │          │   (AD, AWS,  │
│  account │         │    handling  │          │    SAP, ...)  │
│  for     │         │  - Retry     │          │              │
│  Maria"  │◀────────│  - Mapping   │◀─────────│              │
│          │  Result │              │  Response│              │
└──────────┘         └──────────────┘         └──────────────┘
```

### What a Connector Does

| Operation | Description | Example |
|-----------|------------|---------|
| **Account Creation** | Create a new identity in target system | Create AD user, create AWS IAM user |
| **Account Modification** | Change attributes on existing account | Update email, change group membership |
| **Account Disable/Enable** | Suspend or reactivate an account | Disable AD account on leave |
| **Account Deletion** | Remove account entirely | Delete AWS IAM user on termination |
| **Entitlement Grant** | Add specific permission | Add to AD group, attach AWS policy |
| **Entitlement Revoke** | Remove specific permission | Remove from AD group, detach policy |
| **Import (Read)** | Pull current state from target | Read all accounts and their permissions |
| **Reconciliation** | Compare IGA state with target state | Find orphaned accounts, drift |

---

## Integration Patterns

### Pattern 1: Direct API Integration (Cloud-to-Cloud)

```
Saviynt (Cloud) ←──REST/SCIM/GraphQL──→ Target SaaS (Cloud)
```

**Used for:** SaaS applications, cloud providers
**Examples:** AWS IAM API, Azure Graph API, Salesforce REST API, Okta SCIM
**Pros:** No agents needed, real-time, cloud-native
**Cons:** Subject to API rate limits, API changes break connectors

### Pattern 2: Agent/Gateway (Cloud-to-On-Prem)

```
Saviynt (Cloud) ←──Outbound HTTPS──→ Agent (Customer DMZ) ←──LDAP/JDBC──→ On-Prem System
```

**Used for:** On-premises systems not directly reachable from cloud
**Examples:** Active Directory, on-prem SAP, Oracle EBS, mainframes
**Pros:** No inbound firewall rules, secure tunnel
**Cons:** Agent maintenance, another component to monitor, network dependency

### Pattern 3: SCIM (Standard Protocol)

```
Saviynt ←──SCIM 2.0──→ Any SCIM-compliant app
```

**SCIM** (System for Cross-domain Identity Management): Industry standard for identity provisioning. REST-based, JSON payloads, defined operations (Create, Read, Update, Delete, Search).

**Used for:** SaaS apps that support SCIM (growing list: Slack, GitHub, Zoom, etc.)
**Pros:** Standard protocol, predictable behavior, vendor-neutral
**Cons:** Not all apps support it fully, SCIM spec has ambiguities

### Pattern 4: ITSM Ticket-Based (Manual Fulfillment)

```
Saviynt ──creates ticket──→ ServiceNow/Jira ──human fulfills──→ Target System
```

**Used for:** Legacy systems with no API, mainframes, custom applications
**Pros:** Works for anything (human can do what API can't)
**Cons:** Slow, error-prone, no automatic verification, audit gap

### Pattern 5: Database Direct

```
Saviynt Agent ←──JDBC/ODBC──→ Target System's Database
```

**Used for:** Custom applications with no API but accessible database
**Pros:** Can work when nothing else does
**Cons:** Fragile (schema changes break it), bypasses application logic, risky

---

## The Connector Ecosystem

### Categories of Target Systems

| Category | Examples | Typical Protocol | Volume |
|----------|---------|-----------------|--------|
| **Directories** | AD, Azure AD, LDAP | LDAP, Graph API | Highest (everyone has one) |
| **Cloud Providers** | AWS, Azure, GCP | REST APIs | Growing fast |
| **ERP** | SAP, Oracle EBS, Workday | RFC, REST, SOAP | Complex (deep entitlements) |
| **SaaS** | Salesforce, ServiceNow, Slack | REST, SCIM | High volume, simpler |
| **Databases** | Oracle DB, SQL Server, PostgreSQL | JDBC | Common for DBA access |
| **DevOps** | GitHub, GitLab, Jenkins | REST | Growing (dev access governance) |
| **Custom Apps** | Internal tools | Varies (REST, DB, ticket) | Long tail problem |
| **Mainframe** | IBM z/OS, RACF, Top Secret | Terminal emulation, APIs | Legacy but critical |
| **PAM** | CyberArk, HashiCorp Vault | REST | Integration point |
| **Cloud Data** | Snowflake, Databricks | REST | Emerging |

### The Long Tail Problem

```
Distribution of connector usage:

# of       │
customers  │
using      │████
connector  │████████
           │████████████
           │████████████████
           │████████████████████████
           │████████████████████████████████████████████████
           └───────────────────────────────────────────────────
            AD  Azure AWS SAP  SF  SNOW  ... ... ... [200+ more]

Top 10 connectors: used by 80% of customers
Long tail (190+): each used by < 5% of customers
```

**The challenge:** You need deep investment in the top 10 (AD, Azure AD, AWS, SAP, Salesforce, ServiceNow, etc.) AND breadth across 200+ others. Quality can't drop off for the long tail — that one customer relying on the mainframe connector cares about it deeply.

---

## Connector Operations in Detail

### Import (Full and Incremental)

**Full Import:** Read ALL accounts and entitlements from target system. Used for initial setup and periodic reconciliation.

```
Target System → [All 50,000 accounts + entitlements] → IGA Identity Warehouse
```

- Expensive (high API volume, large data transfer)
- Typically scheduled off-peak (nightly, weekly)
- Required for reconciliation accuracy

**Incremental Import:** Read only CHANGES since last import.

```
Target System → [237 accounts changed in last hour] → IGA Identity Warehouse
```

- Efficient (minimal data)
- Near-real-time freshness
- Depends on target system supporting change detection (delta queries, webhooks, changelogs)

### Provisioning (Write Operations)

The IGA engine decides "grant X to user Y." The connector executes it.

**Critical properties:**

| Property | Why It Matters |
|----------|---------------|
| **Idempotent** | Retrying shouldn't create duplicates |
| **Atomic** | Either fully succeed or fully fail (no half-provisioned states) |
| **Auditable** | Every operation logged with timestamp, operator, result |
| **Reversible** | Can undo if needed (revoke what was granted) |
| **Timeout-safe** | Know when to give up and retry vs. wait |

### Reconciliation

Compare what IGA THINKS with what ACTUALLY exists:

```
┌─────────────────┐         ┌─────────────────┐
│ IGA Expected    │         │ Target Actual   │
│ State           │         │ State           │
│                 │         │                 │
│ User A: Groups  │         │ User A: Groups  │
│  [G1, G2, G3]  │    ≠    │  [G1, G2, G4]  │ ← Drift!
│                 │         │                 │
│ User B: Exists  │         │ User B: Exists  │ ← OK
│                 │         │                 │
│ User C: Exists  │         │ User C: Missing │ ← Gap!
│                 │         │                 │
│ (no User D)     │         │ User D: Exists  │ ← Orphan!
└─────────────────┘         └─────────────────┘
```

**Reconciliation outcomes:**

| Situation | Meaning | Action |
|-----------|---------|--------|
| Match | IGA and target agree | Nothing — good |
| Drift | Different permissions than expected | Flag for review, auto-correct, or alert |
| Gap | IGA says should exist, target says no | Re-provision or investigate |
| Orphan | Target has account IGA doesn't know about | Flag for review, disable, or correlate |

---

## What Goes Wrong: Connector Failure Modes

### 1. Connection Failures

**Symptoms:** Timeout, refused connection, auth failure
**Causes:** Network issues, credential rotation, firewall changes, target system down
**Impact:** Provisioning queues up, new hires blocked, de-provisioning delayed

### 2. Schema Changes

**Symptoms:** Operations fail with "invalid attribute" or unexpected responses
**Causes:** Target system upgraded, API versioned, fields renamed
**Impact:** Silent failures (operations appear to succeed but data is wrong)

### 3. Rate Limiting

**Symptoms:** HTTP 429 errors, throttled operations
**Causes:** Target system rate limits exceeded (especially during full imports or bulk provisioning)
**Impact:** Import takes 10x longer, provisioning delayed

### 4. Partial Failures

**Symptoms:** Some operations succeed, others fail in a batch
**Causes:** Data validation errors, duplicate conflicts, permission issues
**Impact:** Inconsistent state — some access granted, some not

### 5. Stale Data

**Symptoms:** IGA shows access that doesn't actually exist (or vice versa)
**Causes:** Reconciliation not running frequently enough, incremental import missing changes
**Impact:** False confidence in access state, audit findings

### 6. Connector Bugs

**Symptoms:** Wrong mapping, duplicated accounts, incorrect attribute values
**Causes:** Logic errors in connector code, edge cases in target system behavior
**Impact:** Security risk (wrong access), operational issues (broken accounts)

---

## Connector Architecture at Saviynt

### REST-Based Connector Framework

Saviynt provides a configurable connector framework where many connectors are built via configuration (JSON-based job definitions) rather than custom code:

```json
{
  "connection": {
    "url": "https://api.target.com",
    "authType": "OAuth2",
    "clientId": "...",
    "tokenEndpoint": "..."
  },
  "accountImport": {
    "endpoint": "/users",
    "pagination": "offset",
    "mapping": {
      "accountName": "$.username",
      "displayName": "$.profile.name",
      "status": "$.active"
    }
  },
  "createAccount": {
    "endpoint": "/users",
    "method": "POST",
    "body": {
      "username": "${user.accountName}",
      "email": "${user.email}"
    }
  }
}
```

**Benefits:**
- Faster connector development (configuration, not code)
- Consistent behavior across connectors
- Easier testing and validation
- Customer-modifiable for custom systems

### Pre-Built vs. Custom Connectors

| Type | Description | Count |
|------|------------|-------|
| **Out-of-box** | Fully built, tested, supported by Saviynt | 200+ |
| **Configurable REST** | Customer configures JSON for their REST API | Unlimited |
| **Custom development** | Built by SI/partner for unique systems | As needed |

---

## Integration Beyond Connectors

### HR System Integration (Source)

```
HRIS (Workday, SuccessFactors, BambooHR)
                │
                │ Identity feed (new hires, changes, terminations)
                ▼
        ┌──────────────┐
        │ Saviynt EIC  │
        │              │
        │ Creates/     │
        │ Updates/     │
        │ Disables     │
        │ identities   │
        └──────┬───────┘
               │ Provisions to target systems
               ▼
    AD, AWS, SAP, Salesforce, ...
```

HRIS is the **authoritative source** — it TELLS IGA what to do (new hire, role change, termination). IGA then ACTS on target systems.

### ITSM Integration (Workflow)

```
Access Request → IGA Workflow → (optional) ITSM Ticket → Provisioning
                                    │
                                    └→ For visibility, change management, 
                                       or manual fulfillment
```

ServiceNow, Jira Service Management — IGA can create tickets for:
- Audit trail in ITSM
- Manual fulfillment (systems without API)
- Change management compliance

### SIEM Integration (Security)

```
IGA Events → SIEM (Splunk, Sentinel, etc.)

Events include:
- High-risk access granted
- SoD violation detected
- Orphaned account found
- Certification failed
- Privileged access activated
```

Security team monitors IGA events alongside other security signals.

---

> **🔧 Platform Engineering Lens**
>
> Connectors are the **most reliability-sensitive component** of an IGA platform. They're your "external dependencies" — and you don't control them.
>
> **SRE patterns that apply directly:**
>
> | SRE Concept | Connector Application |
> |-------------|----------------------|
> | Circuit breaker | If target system is down, stop hammering it. Queue operations. |
> | Retry with backoff | Transient failures (429, 503) should retry, not fail permanently |
> | Bulkhead | One failing connector shouldn't impact others |
> | Health checks | Proactive detection of connector issues before users notice |
> | SLIs/SLOs | Provisioning success rate, latency per connector |
> | Error budgets | How much connector failure is acceptable before escalation? |
> | Observability | Per-connector metrics: latency, error rate, queue depth |
> | Chaos testing | What happens when AWS API is down for 2 hours? |
>
> **The connector platform is essentially a managed integration layer** — similar to API gateway challenges but with the added complexity of:
> - 200+ distinct protocols and systems
> - Each with unique failure modes
> - Each owned by different customer teams
> - No control over target system behavior
>
> This is where your platform engineering skills translate most directly to the IGA domain.

---

## Self-Test Questions

1. What's the difference between a connector's import operation and reconciliation? Why do you need both?
2. Why might you use a SCIM connector vs. a custom REST connector?
3. What are the three integration patterns for reaching on-prem systems from a cloud IGA platform?
4. Name three connector failure modes and their business impact.
5. Why is the "long tail" of connectors a product and engineering challenge?
6. How would you design monitoring for a connector platform supporting 200+ integration types?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Connector** | Integration component between IGA and target system |
| **Target System** | Any application/infrastructure IGA governs access to |
| **SCIM** | System for Cross-domain Identity Management — standard provisioning protocol |
| **Full Import** | Reading all accounts/entitlements from target (expensive, comprehensive) |
| **Incremental Import** | Reading only changes since last import (efficient, frequent) |
| **Reconciliation** | Comparing IGA expected state with actual target state |
| **Orphaned Account** | Account in target system with no corresponding IGA identity |
| **Drift** | Difference between expected and actual entitlement state |
| **Agent/Gateway** | On-prem component enabling cloud IGA to reach on-prem systems |
| **Provisioning** | Write operation: creating/modifying/deleting access in target system |
| **Idempotent** | Operation that can be retried without creating duplicates |
| **Authoritative Source** | System that drives identity creation (usually HRIS) |
