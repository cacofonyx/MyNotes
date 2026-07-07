# Chapter 08: Role Engineering & Mining

> *"Role engineering is the art of abstracting complexity. Done well, it simplifies governance. Done poorly, it creates a new kind of chaos."*

---

## The Role Concept

A **role** is a named bundle of entitlements assigned as a unit. Instead of managing 30 individual permissions per person, you manage one role assignment.

```
WITHOUT ROLES:                          WITH ROLES:
User → Entitlement 1                    User → "Finance Analyst" Role
User → Entitlement 2                            │
User → Entitlement 3                            ├→ Entitlement 1
User → Entitlement 4                            ├→ Entitlement 2
...                                             ├→ Entitlement 3
User → Entitlement 30                           ├→ ...
                                                └→ Entitlement 30
(30 assignments to manage)              (1 assignment to manage)
```

### Why This Matters at Scale

| Metric | Without Roles | With Roles |
|--------|--------------|------------|
| Assignments to manage (10K users × 30 entitlements) | 300,000 | 10,000 (role assignments) |
| Certification items per manager (20 reports) | 600 | 20 (role-level certs) |
| Provisioning on role change | Manual per entitlement | Swap one role |
| SoD analysis complexity | Entitlement × entitlement | Role × role |
| Audit explanation | Per-entitlement justification | "They're in this role because they're a Finance Analyst" |

---

## Types of Roles

### Business Roles

Map to organizational functions — what a person DOES:

| Business Role | Who Gets It | What It Contains |
|-------------|-------------|-----------------|
| Finance Analyst | Anyone titled "Finance Analyst" | SAP FI read, reporting tools, budget system |
| Software Engineer | Engineering team members | GitHub, CI/CD, dev AWS account, Jira |
| HR Business Partner | HR team | Workday admin, benefits system, comp tools |
| Sales Rep | Sales team | Salesforce, CPQ, contract tool |

**Assigned based on:** Job title, department, business function

### Technical Roles

Map to system-level permission bundles — HOW access is granted:

| Technical Role | What It Represents | Where It Applies |
|---------------|-------------------|-----------------|
| SAP-FI-Postings | Can post financial documents | SAP only |
| AWS-Dev-ReadOnly | Read access to dev AWS account | AWS only |
| AD-Finance-Group | Member of Finance AD security group | Active Directory only |

**Assigned based on:** Needed by business roles or specific requests

### Composite/Hierarchical Roles

Roles built from other roles:

```
"Senior Finance Analyst" (Composite Role)
├── "Finance Analyst" (Business Role)
│   ├── SAP-FI-Read
│   ├── Tableau-Finance
│   └── Budget-System-User
├── "Financial Reporting" (Business Role)
│   ├── SAP-FI-Postings
│   └── Consolidation-Tool
└── Additional: Audit-Committee-Viewer
```

### Organizational Roles

Based on org attributes, not job function:

| Org Role | Trigger | Grants |
|----------|---------|--------|
| US Employee | Location = US | Benefits portal, US payroll access |
| Remote Worker | Work location = remote | VPN access, virtual desktop |
| Austin Office | Office = Austin | Building access, local printer, parking system |
| Contractor | Employment type = contractor | Time tracking, limited network |

---

## Role Engineering: Building Roles

### Top-Down Approach (Design)

Start from business requirements and work down to entitlements:

```
Step 1: Identify job functions            Step 2: Define access needs
┌──────────────────────┐                  ┌──────────────────────┐
│ Job Title: Finance   │                  │ What does a Finance  │
│ Analyst              │                  │ Analyst need?        │
│                      │                  │                      │
│ Department: Finance  │  ───────────▶    │ - Read financials    │
│ Level: Individual    │                  │ - Run reports        │
│ Contributor          │                  │ - Access budget tool │
└──────────────────────┘                  └──────────────────────┘

Step 3: Map to entitlements               Step 4: Create role
┌──────────────────────┐                  ┌──────────────────────┐
│ SAP: FI_READ access  │                  │ Role: Finance_Analyst│
│ Tableau: Finance     │                  │                      │
│   workspace viewer   │  ───────────▶    │ Contains:            │
│ BudgetApp: User role │                  │ - SAP_FI_READ        │
│ SharePoint: Finance  │                  │ - TABLEAU_FIN_VIEW   │
│   site reader        │                  │ - BUDGET_USER        │
└──────────────────────┘                  │ - SP_FINANCE_READ    │
                                          └──────────────────────┘
```

**Advantages:**
- Clean, intentional design
- Aligned with business understanding
- Easy to explain to auditors

**Disadvantages:**
- Theoretical — may miss what people actually need
- Time-consuming (requires business input for every role)
- Can be out-of-date before it's finished

### Bottom-Up Approach (Mining)

Start from actual access data and discover patterns:

```
Step 1: Gather actual access data
┌────────────────────────────────────────────────┐
│ User A (Finance Analyst): SAP_FI, TABLEAU, SP  │
│ User B (Finance Analyst): SAP_FI, TABLEAU, SP  │
│ User C (Finance Analyst): SAP_FI, TABLEAU, SP, BUDGET │
│ User D (Finance Analyst): SAP_FI, TABLEAU      │
└────────────────────────────────────────────────┘

Step 2: Find clusters (role mining algorithm)
┌────────────────────────────────────────────────┐
│ Pattern found: 90% of Finance Analysts have    │
│ {SAP_FI, TABLEAU, SP}                          │
│                                                │
│ Proposed role: "Finance Analyst Base"           │
│ Coverage: 90% of target population             │
└────────────────────────────────────────────────┘

Step 3: Validate with business owners
┌────────────────────────────────────────────────┐
│ "Does this make sense as a role?"              │
│ "Should BUDGET be included (30% have it)?"     │
│ "Is User D missing SP access by mistake?"     │
└────────────────────────────────────────────────┘
```

**Advantages:**
- Reflects reality (what people actually use)
- Data-driven, faster to start
- Identifies gaps and outliers

**Disadvantages:**
- Codifies bad habits (accumulated access ≠ needed access)
- Noisy data (edge cases, historical artifacts)
- Requires cleanup AFTER mining (not just accept raw output)

### Hybrid Approach (Reality)

Most successful role engineering combines both:

1. **Mine** to discover patterns and cluster similar access
2. **Validate** with business to confirm patterns make sense
3. **Design** refinements — add missing pieces, remove inappropriate items
4. **Iterate** — roles aren't static, review and adjust quarterly

---

## Role Mining: How It Works

### The Algorithm (Conceptual)

Given a matrix of Users × Entitlements:

```
         E1  E2  E3  E4  E5  E6  E7  E8
User A:   1   1   1   0   0   0   0   0
User B:   1   1   1   0   0   0   0   0
User C:   1   1   1   1   0   0   0   0
User D:   0   0   0   0   1   1   1   0
User E:   0   0   0   0   1   1   1   1
User F:   0   0   0   0   1   1   1   0
```

**Step 1:** Find frequent entitlement combinations
- {E1, E2, E3} appears in 3 users (A, B, C)
- {E5, E6, E7} appears in 3 users (D, E, F)

**Step 2:** Propose roles
- Role 1: {E1, E2, E3} — covers Users A, B, C
- Role 2: {E5, E6, E7} — covers Users D, E, F

**Step 3:** Handle outliers
- User C has E4 extra (exception or add to role?)
- User E has E8 extra (exception or separate role?)

### Mining Parameters

| Parameter | Trade-off |
|-----------|----------|
| **Minimum support** (min users with pattern) | Low = more roles found, some noisy. High = only major patterns. |
| **Minimum confidence** (% of role users who have all items) | Low = roles cover more people but less precise. High = tight roles but more exceptions. |
| **Maximum role size** | Small = granular, many roles. Large = fewer roles, more complex each. |

---

## The Role Explosion Problem

### What Goes Wrong

Bad role management leads to exponential role growth:

```
Year 1:  50 roles     (clean, intentional)
Year 2:  200 roles    (some exceptions became roles)
Year 3:  800 roles    (every unique combination got a role)
Year 5:  3,000 roles  (one role per person, essentially)
```

**Causes:**
- "I need everything in Role X plus one more thing" → new role
- "Create a role for this team of 3 people" → role with 3 members
- "Nobody wants to change existing roles (might break something)" → only additions
- "Contractor needs subset of Employee role" → new role for each variant
- Regional variants: "Finance Analyst - US" "Finance Analyst - EU" "Finance Analyst - APAC"

### When You Know You Have a Problem

- More roles than people in some departments
- Average role has <5 members
- Nobody can explain what half the roles are for
- New hire provisioning requires 8+ role assignments
- Role names are incomprehensible ("FIN_US_SR_V2_2023_MOD")

### How to Prevent / Fix

| Strategy | How |
|----------|-----|
| **80/20 rule** | Roles cover 80% of access. Remaining 20% = individual entitlement requests |
| **Role ownership** | Every role has an owner responsible for relevance and cleanup |
| **Periodic pruning** | Roles with <3 members get reviewed for deletion quarterly |
| **Composition over creation** | Need Role A + extra? Assign Role A + individual entitlement, don't make Role A-Prime |
| **Governance on role creation** | Creating a new role requires justification, min member threshold |
| **Sunset dates** | Project-based roles get expiration dates |

---

## Birthright Access: The Automatic Baseline

### What It Is

Birthright access = the set of roles/entitlements automatically granted when someone JOINS based on their attributes. No request needed.

### How It's Defined

```
IF (Department = Finance) AND (Level = Individual Contributor)
THEN auto-assign: "Finance Analyst" role

IF (Department = Engineering) AND (Title contains "Software Engineer")
THEN auto-assign: "Software Engineer" role

IF (Location = Austin) AND (Employment Type = FTE)
THEN auto-assign: "Austin Office" org role
```

### Birthright Design Principles

| Principle | Explanation |
|-----------|------------|
| **Minimum necessary** | Only what EVERYONE in that segment needs on Day 1 |
| **Well-tested** | Auto-provisioning failures = blocked new hires |
| **Conservative** | Better to grant less automatically, allow requests for more |
| **Role-based, not individual** | Should apply to all people matching criteria |
| **Quickly grantable** | All entitlements in birthright roles must be auto-provisionable (no manual steps) |

### Birthright vs. Request-Based

```
Total Access a Person Has:
┌───────────────────────────────────────────────────┐
│                                                    │
│  ┌──────────────────┐  ┌────────────────────────┐ │
│  │   BIRTHRIGHT      │  │   REQUEST-BASED        │ │
│  │   (Automatic)     │  │   (Approved)           │ │
│  │                   │  │                        │ │
│  │  - Base tools     │  │  - Project access      │ │
│  │  - Team access    │  │  - Special permissions │ │
│  │  - Standard apps  │  │  - Cross-team collab   │ │
│  │                   │  │  - Temporary access    │ │
│  │  ~60-70% of       │  │  ~30-40% of total     │ │
│  │  total access     │  │  access               │ │
│  └──────────────────┘  └────────────────────────┘ │
│                                                    │
└───────────────────────────────────────────────────┘
```

---

## Entitlement Analytics

### Peer Group Analysis

"What access do people LIKE YOU have?"

```
Target User: Maria (Finance Analyst, Austin, IC)

Peers (same title/dept/location):
- 95% have SAP_FI_READ         → Expected (include in role)
- 95% have TABLEAU_FINANCE     → Expected (include in role)
- 90% have SHAREPOINT_FINANCE  → Expected (include in role)
- 40% have BUDGET_TOOL         → Common but not universal (optional?)
- 5% have SAP_FI_ADMIN         → Outlier (investigate - likely over-provisioned)

Maria has: SAP_FI_ADMIN ← She's an outlier. Flag for review.
```

### Usage Analytics

"Is this access actually USED?"

```
Entitlement: AWS-Prod-ReadOnly
Granted to: Maria Chen
Granted: 2023-06-15
Last used: 2023-07-02 (14 months ago)

→ Recommendation: Revoke (unused for 14 months)
```

### Outlier Detection

Finding people who have MORE or DIFFERENT access than their peers:

```
Finance Analysts average: 15 entitlements
Maria Chen: 47 entitlements ← 3x average = outlier

Extra entitlements include:
- 12 from previous role (Software Engineer) — never removed
- 8 from a project that ended 6 months ago
- 5 admin entitlements that ICs shouldn't have

→ Trigger: Review with manager, likely revoke 25+ items
```

---

## Role Lifecycle

Roles aren't static. They have their own lifecycle:

```
┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐
│  Design  │──▶ │  Review  │──▶ │  Active  │──▶ │  Retire  │
│  & Test  │    │ & Approve│    │  & Maint │    │          │
└──────────┘    └──────────┘    └──────────┘    └──────────┘
     │                │               │               │
     │                │               │               │
 - Define scope   - Business      - Monitor       - Phase out
 - Map entitlements  owner signs    usage         - Migrate users
 - Test provisioning off          - Adjust        - Archive
 - Validate SoD   - Security      entitlements   - Document
                    review        - Handle           why retired
                                   exceptions
```

---

> **🔧 Platform Engineering Lens**
>
> Role management is essentially **configuration management for access.** The same problems exist:
>
> | Infrastructure Config Problem | Role Management Equivalent |
> |------------------------------|---------------------------|
> | Configuration drift | Roles diverge from intended state over time |
> | Snowflake servers | Unique roles per person (defeats purpose of roles) |
> | Config sprawl | Thousands of roles nobody understands |
> | No owner | Orphaned roles (exist but nobody maintains them) |
> | No testing | New role assignments breaking things (SoD violations) |
> | Manual changes | Ad-hoc role modifications without governance |
>
> **If you think of roles as "infrastructure-as-code for access":**
> - Roles should be version-controlled (change history, who modified, why)
> - Role changes should be tested (SoD simulation before deployment)
> - Roles should have owners (like services have on-call)
> - Unused roles should be garbage-collected (like unused infrastructure)
> - Role assignment should be declarative ("this person SHOULD have these roles" → system converges)
>
> The future of role management looks increasingly like GitOps for identity.

---

## Self-Test Questions

1. What's the difference between a business role and a technical role? Give an example of each.
2. When would you use top-down role design vs. bottom-up role mining? What are the risks of each?
3. What is "role explosion" and what causes it? How do you prevent it?
4. What's birthright access and how does it differ from request-based access?
5. How does peer group analysis help identify over-provisioned users?
6. Why do roles need a lifecycle (not just "create once and forget")?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Role** | Named bundle of entitlements assigned as a unit |
| **Business Role** | Role aligned to a job function (e.g., "Finance Analyst") |
| **Technical Role** | Role aligned to system permissions (e.g., "SAP-FI-Read") |
| **Role Mining** | Discovering role patterns from existing access data |
| **Role Engineering** | Designing roles from business requirements |
| **Role Explosion** | Uncontrolled growth of roles making them unmanageable |
| **Birthright Access** | Access automatically granted based on attributes at hire |
| **Peer Group** | Set of similar users for comparison (same role/dept/level) |
| **Outlier** | User with significantly different access than their peer group |
| **Entitlement Analytics** | Data analysis of access patterns, usage, and anomalies |
| **Composition** | Building complex roles from simpler roles |
| **Role Owner** | Person accountable for a role's correctness and relevance |
