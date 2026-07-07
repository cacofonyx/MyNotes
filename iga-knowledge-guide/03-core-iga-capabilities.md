# Chapter 03: Core IGA Capabilities

> *"IGA is deceptively simple in concept — manage who has access to what. It's ferociously complex in execution."*

---

## The Five Pillars of IGA

Every IGA platform (Saviynt, SailPoint, or otherwise) provides some version of these five capabilities:

```
┌─────────────────────────────────────────────────────────────────┐
│                        IGA PLATFORM                              │
│                                                                  │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────┐ ┌──────┐ │
│  │ Identity  │ │  Access   │ │  Access   │ │  Role │ │ SoD  │ │
│  │ Lifecycle │ │ Request & │ │ Certifi-  │ │ Mgmt  │ │Policy│ │
│  │ Mgmt      │ │ Approval  │ │ cation    │ │       │ │      │ │
│  └───────────┘ └───────────┘ └───────────┘ └───────┘ └──────┘ │
│       │              │              │            │         │     │
│       ▼              ▼              ▼            ▼         ▼     │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │              CONNECTORS (to target systems)                  ││
│  │    AD, Azure, AWS, SAP, Salesforce, ServiceNow, ...         ││
│  └─────────────────────────────────────────────────────────────┘│
└─────────────────────────────────────────────────────────────────┘
```

---

## Pillar 1: Identity Lifecycle Management

### What It Is

Automating the entire lifecycle of an identity — from creation to deletion — driven by events in authoritative sources (usually HR systems).

### The Trigger Pattern

```
HR System Event  →  IGA Detects Change  →  IGA Executes Actions  →  Target Systems Updated
```

### Joiner (New Hire)

**Trigger:** New record appears in HR system (Workday, SuccessFactors, BambooHR)

**IGA Actions:**
1. Create identity record in IGA
2. Determine birthright access based on:
   - Job title
   - Department
   - Location
   - Manager
   - Employment type (FTE vs contractor)
3. Provision accounts across target systems:
   - Create AD account
   - Create email
   - Add to appropriate groups
   - Create accounts in role-specific applications
4. Notify manager, IT, new hire
5. Log everything for audit trail

**Example scenario:**
> New hire: Maria, Software Engineer, Platform Team, Austin office
> 
> Birthright access auto-provisioned:
> - AD account + standard groups
> - Email (Google Workspace)
> - GitHub (platform-team org, engineering teams)
> - Jira (Engineering project)
> - AWS (read-only dev account)
> - PagerDuty (Platform team rotation)
> - Slack (general + platform-engineering channels)
> 
> All provisioned before Day 1. Zero tickets filed.

### Mover (Role Change)

**Trigger:** Change in HR record — new title, department, manager, or location

**IGA Actions:**
1. Detect what changed
2. Determine new birthright access for new role
3. **Grant** new access needed
4. **Flag** access that no longer aligns with new role
5. Either auto-revoke (if policy allows) or trigger certification for manager review
6. Check SoD: does new access + retained access create violations?

**Why Mover is hardest:**
- Joiner: provisioning from nothing → clear target state
- Leaver: revoke everything → clear target state
- Mover: partial change → requires comparing old state vs new state, deciding what stays and what goes. Often involves judgment calls.

**The accumulation problem:** Without IGA, Movers almost never lose access. They only gain. After 3 role changes, a person has access for 4 roles worth of permissions.

### Leaver (Departure)

**Trigger:** Termination date in HR system (or immediate termination event)

**IGA Actions:**
1. Immediately disable all authentication (prevent login)
2. Revoke active sessions where possible
3. Begin systematic de-provisioning across all systems
4. Transfer ownership of shared resources (files, groups, etc.)
5. Archive identity record (don't delete — auditors need history)
6. Generate evidence report for compliance

**Time-critical aspect:** For involuntary termination, this often needs to happen within minutes, not hours. An angry ex-employee with active admin credentials is a threat scenario every CISO fears.

**The long tail:** Some systems don't support immediate revocation. Local accounts, API keys, service accounts tied to a person — these are the ones that slip through.

---

## Pillar 2: Access Request & Approval

### What It Is

A structured workflow for requesting, approving, and provisioning access beyond birthright. Think "shopping cart for permissions."

### The Flow

```
User Requests  →  Policies Evaluated  →  Approval Routing  →  Provisioning  →  Granted
     │                   │                      │                   │
     │                   ▼                      ▼                   │
     │            ┌─────────────┐       ┌────────────┐             │
     │            │ SoD Check   │       │ Manager    │             │
     │            │ Risk Score  │       │ App Owner  │             │
     │            │ Auto-deny?  │       │ Security   │             │
     │            └─────────────┘       │ Auto-approve│            │
     │                                  └────────────┘             │
     └─────────────────────────────────────────────────────────────┘
                         Audit Trail (every step logged)
```

### What Makes This Non-Trivial

**1. The catalog problem:** Users need to FIND the right access to request. Enterprise might have 10,000+ entitlements. How do you present that? Searchable catalog? Role-based recommendations? "People like you also have..."?

**2. Approval routing:** Who approves?
- Direct manager? (Common, but often rubber-stamps)
- Application owner? (Knows context, but becomes bottleneck)
- Security team? (For high-risk access only — otherwise they'd do nothing else)
- Auto-approve? (For low-risk, pre-defined bundles)

**3. SoD enforcement at request time:** Before even routing for approval, check: "If we grant this, does it create a toxic combination with existing access?" If yes → block or escalate.

**4. Time-bound access:** Not all access should be permanent. "I need prod DB access for 2 hours to debug an incident" → grant with automatic expiration.

**5. Provisioning execution:** Approval is meaningless if the actual account/permission isn't created in the target system. This depends on connectors (Ch 06).

### Real-World Scenario

> Engineer needs access to a production AWS account for an incident response.
>
> 1. Opens IGA portal → searches "AWS prod account"
> 2. Finds "AWS-Production-ReadOnly" entitlement
> 3. Submits request with justification: "Incident INC-4521 — need to check CloudWatch logs"
> 4. IGA checks: No SoD violations. Risk score: medium.
> 5. Routes to: Team lead (auto-approve path for time-bound read-only)
> 6. Team lead approves via Slack integration
> 7. IGA provisions AWS IAM role via connector
> 8. Access granted with 4-hour expiration
> 9. 4 hours later: access automatically revoked
> 10. Full audit trail: who, what, when, why, who approved, when expired

---

## Pillar 3: Access Certification (Access Reviews)

### What It Is

Periodic campaigns where reviewers (usually managers or app owners) confirm: "Yes, this person still needs this access" or "No, revoke it."

### Why It Exists

Access accumulates. People get access for a project, project ends, access remains. Certification is the periodic cleanup — the garbage collection of the identity world.

### How a Certification Campaign Works

```
Campaign Created → Reviewers Assigned → Review Period Opens → Decisions Made → Actions Executed
     │                    │                      │                    │              │
     │                    ▼                      ▼                    ▼              ▼
     │           Manager or          "Keep" or "Revoke"       Approved items    Revoked items
     │           App Owner           for each line item       stay as-is        de-provisioned
     │                                                                          
     └──→ Scope: "All access for Finance department" or "All users of SAP"
```

### Types of Certification

| Type | What's Reviewed | Who Reviews | When |
|------|----------------|-------------|------|
| **Manager certification** | All access for their direct reports | Manager | Quarterly |
| **Application certification** | All users of a specific application | App owner | Semi-annually |
| **Entitlement certification** | Everyone with a specific permission | Risk owner | Event-triggered |
| **Micro-certification** | Single access decision at point of change | Manager | Real-time |

### The Rubber-Stamp Problem

**The dirty secret of IGA:** ~90% of certification decisions are "Approve." This is a well-documented problem. Why?

- Managers don't understand the entitlements they're reviewing (cryptic names like "SAP_FI_01_POST")
- Reviewing 200 line items is tedious → click "approve all"
- No consequence for over-approving; risk of revoking something needed = angry team member

**Modern IGA solutions (including Saviynt) address this with:**
- Risk-based certification: Only surface high-risk items for human review
- AI-recommended decisions: "This access is unused for 90 days — recommend revoke"
- Peer comparison: "No one else in this role has this access"
- Plain-language descriptions: Translate "SAP_FI_01_POST" → "Can post journal entries in SAP Finance"
- Micro-certifications: Review at moment of change, not batch quarterly

---

## Pillar 4: Role Management (RBAC)

### What It Is

Organizing access into logical bundles (roles) that can be assigned as a unit, rather than managing individual entitlements per person.

### Why Roles Exist

**Without roles:**
- 10,000 employees × 50 average entitlements = 500,000 individual access assignments to manage
- Each managed individually = operational nightmare

**With roles:**
- 200 roles, each bundling 10-30 entitlements
- Assign role → person gets all associated entitlements
- Manage at role level, not individual level

### Types of Roles

| Role Type | Definition | Example |
|-----------|-----------|---------|
| **Business role** | Maps to a job function | "Finance Analyst," "Software Engineer" |
| **Technical role** | Maps to a system permission bundle | "SAP-AP-User," "AWS-Dev-ReadOnly" |
| **Organizational role** | Maps to org position | "Austin Office Employee," "APAC Region" |
| **Composite role** | Combines multiple roles | "Senior Finance Analyst" = "Finance Analyst" + "Financial Reporting" |

### Role Engineering: Top-Down vs. Bottom-Up

**Top-down (Role Design):**
1. Look at org chart and job descriptions
2. Define what each job function needs
3. Create roles mapped to functions
4. Assign people to roles

**Problem:** Theoretical. Misses reality of how access actually works.

**Bottom-up (Role Mining):**
1. Look at what access people actually HAVE
2. Find clusters of common entitlements
3. Propose roles based on observed patterns
4. Validate with business owners

**Problem:** Codifies bad habits. If everyone accumulated too much access, mining just formalizes the mess.

**Reality:** You need both. Mine to discover patterns, then curate/clean from the top. Iterative process, never "done."

### The Role Explosion Problem

Bad role engineering leads to:
- Thousands of roles (some with 1-2 people assigned)
- Overlapping roles nobody understands
- "One more role" created for every exception
- Maintenance nightmare — who owns these 3,000 roles?

**Good role engineering:**
- Aims for 80% coverage with birthright roles
- Uses entitlement-level requests for the remaining 20%
- Regularly prunes unused roles
- Clear ownership per role

---

## Pillar 5: Segregation of Duties (SoD) Policy

### What It Is

Rules that define which combinations of access are prohibited, and enforcement mechanisms to prevent or detect violations.

### The Logic

```
IF person has [Permission A] AND [Permission B]
THEN → SoD Violation
ACTION → Block / Alert / Require exception approval
```

### SoD in Practice

**Preventive SoD:** Block the violation BEFORE it happens
- User requests access → SoD check runs → violation detected → request denied (or escalated)
- Role change triggers → new role would create conflict → flag for review

**Detective SoD:** Find violations that already exist
- Periodic scan of all access assignments
- Compare against SoD ruleset
- Surface violations for remediation
- Report for auditors

### Building SoD Rules

| Area | Toxic Combination | Business Risk |
|------|-------------------|--------------|
| Finance | Create vendor + Approve payment | Fraud — fictitious vendor payments |
| Finance | Modify price list + Process orders | Revenue manipulation |
| HR/Payroll | Create employee + Run payroll | Ghost employee fraud |
| IT | Write code + Deploy to production | Malicious code deployment |
| Procurement | Create PO + Receive goods | Theft via fake receipts |
| Banking | Initiate wire + Approve wire | Unauthorized fund transfer |

### SoD Complexity at Scale

For an enterprise SAP environment alone:
- 300+ SoD rules covering financial processes
- Each rule checking combinations across multiple transaction codes
- Thousands of users to check
- Rules interact (fixing one violation might create another)
- Exceptions exist (small team where someone MUST hold both — compensating controls required)

**Why automation is non-negotiable:** Checking 300 rules × 10,000 users × 50 entitlements each = billions of combinations. No human team can do this manually.

---

## How the Five Pillars Work Together

A single scenario touching all five:

> **Scenario:** Finance department reorganization at a bank.
>
> 1. **Lifecycle:** HR updates 200 people's departments/titles in Workday
> 2. **Role Management:** IGA maps new titles to new roles, identifies birthright changes
> 3. **SoD Policy:** Before applying new roles, checks for violations — finds 12 cases where new role + existing access = conflict
> 4. **Access Request:** For the 12 conflicts, routes to compliance team for exception or remediation decisions
> 5. **Certification:** Triggers micro-certification for affected managers: "Your team's access is changing — review these items"
>
> All automated. All logged. All auditable. Without IGA, this takes weeks of spreadsheet work and manual coordination.

---

## The Provisioning Engine

Underneath all five pillars is the provisioning engine — the component that ACTUALLY creates or removes access in target systems.

### How Provisioning Works

```
IGA Decision         →    Provisioning Engine    →    Target System
("Grant role X")          (translate + execute)       (AD/AWS/SAP/etc.)

                    ┌──────────────────────────┐
                    │   Provisioning Engine     │
                    │                           │
                    │  - Queue management       │
                    │  - Retry logic            │
                    │  - Conflict resolution    │
                    │  - Status tracking        │
                    │  - Rollback capability    │
                    │  - Reconciliation         │
                    └──────────────────────────┘
```

### Provisioning Patterns

| Pattern | Description | Use Case |
|---------|------------|----------|
| **Automated** | IGA directly creates/modifies account in target | Standard provisioning |
| **Ticket-based** | IGA creates ticket in ITSM (ServiceNow) for manual execution | Legacy systems without API |
| **Approval-gated** | Provisioning waits for human approval at target system level | High-security environments |
| **Just-in-Time** | Access created only when needed, expires automatically | Privileged access, cloud |

### Reconciliation: Trust But Verify

Provisioning isn't reliable unless you verify. Reconciliation is the continuous comparison:

```
What IGA THINKS exists  vs.  What ACTUALLY exists in target system
         │                              │
         └──────── Differences ─────────┘
                       │
              ┌────────┴────────┐
              │                 │
         Orphan found      Missing account
    (exists in target,    (IGA says it should
     IGA doesn't know)    exist, target says no)
              │                 │
              ▼                 ▼
         Flag/remove       Re-provision or
                          investigate
```

---

> **🔧 Platform Engineering Lens**
>
> The provisioning engine is where IGA meets your world directly. It's a **distributed workflow system** with:
> - **Async processing** (target systems respond at different speeds)
> - **Retry semantics** (connector timeouts, target system downtime)
> - **Idempotency requirements** (retrying a provision shouldn't create duplicates)
> - **Reconciliation loops** (eventual consistency between IGA and targets)
> - **Queue depth as a leading indicator** (provisioning backlog = new hires blocked)
>
> This is a system you'd design SLIs for:
> - Provisioning latency (p50, p95, p99)
> - Provisioning success rate
> - Reconciliation drift (% of accounts that don't match expected state)
> - De-provisioning time-to-complete (security-critical)
>
> If you think "this sounds like a message-driven microservice with eventual consistency guarantees" — yes, exactly.

---

## Self-Test Questions

1. Name the five pillars of IGA. How does each one interact with the others?
2. Why is the "Mover" lifecycle event harder than Joiner or Leaver?
3. What's the "rubber-stamp problem" in access certification? How do modern platforms address it?
4. Explain the difference between preventive and detective SoD controls.
5. What is reconciliation and why is it necessary even if your provisioning engine works perfectly?
6. If a CEO asks "why can't we just use spreadsheets for access reviews?" — what's your answer?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Identity Lifecycle** | The full arc of an identity: creation → changes → deletion |
| **Birthright Access** | Access automatically granted based on attributes (role, dept, location) |
| **Access Request** | Formal request for additional access beyond birthright |
| **Approval Workflow** | Routing logic determining who approves access requests |
| **Access Certification** | Periodic review confirming access is still appropriate |
| **Campaign** | A scheduled, scoped certification event (e.g., "Q3 Finance Review") |
| **RBAC** | Role-Based Access Control — permissions assigned via roles, not individually |
| **Role Mining** | Discovering role patterns from existing access data (bottom-up) |
| **Role Engineering** | Designing roles from business requirements (top-down) |
| **SoD Rule** | Definition of a prohibited access combination |
| **Compensating Control** | Alternative safeguard when SoD exception is granted |
| **Provisioning** | Actually creating/modifying accounts in target systems |
| **Reconciliation** | Comparing IGA's expected state with actual state in target systems |
| **Orphaned Account** | Account existing in target system with no corresponding active identity |
