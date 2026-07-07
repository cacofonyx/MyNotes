# Chapter 07: Access Certifications & Reviews

> *"Certification is IGA's garbage collection. Without it, access accumulates until it becomes a breach waiting to happen."*

---

## Why Certifications Exist

Access is easy to grant. Access is hard to remove. Over time:
- People accumulate permissions they no longer need
- Roles evolve but old access stays
- Project-based access outlives the project
- Nobody notices until an audit (or an incident)

Certification is the periodic process of asking: **"Does this person still need this access? Prove it."**

It exists because auditors require EVIDENCE that someone REVIEWED access and made a conscious decision to keep or revoke it. "We think it's fine" isn't good enough. You need: "Manager Jane Doe reviewed access for her 12 direct reports on 2024-03-15 and confirmed/revoked each item."

---

## The Certification Campaign Lifecycle

```
┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐   ┌──────────┐
│  Define  │──▶│  Launch  │──▶│  Review  │──▶│ Execute  │──▶│  Report  │
│  Campaign│   │  Campaign│   │  Period  │   │  Actions │   │  Results │
└──────────┘   └──────────┘   └──────────┘   └──────────┘   └──────────┘
                                    │
                          ┌─────────┴─────────┐
                          │  Reviewers see     │
                          │  their items and   │
                          │  decide:           │
                          │  ✅ Certify (keep) │
                          │  ❌ Revoke         │
                          │  ↗️ Reassign       │
                          └───────────────────┘
```

### Step 1: Define Campaign

**Scope:** What's being reviewed?
- "All access for Finance department" (org-scoped)
- "All users of SAP" (application-scoped)
- "All high-risk entitlements" (risk-scoped)
- "Access for User X who changed roles" (event-triggered)

**Reviewers:** Who reviews?
- Manager reviews all their direct reports' access
- Application owner reviews all users of their app
- Security team reviews high-risk items only

**Timeline:**
- Start date
- Duration (typically 2-4 weeks)
- Escalation if not completed by deadline
- Default action on expiry (auto-revoke? escalate? extend?)

### Step 2: Launch Campaign

IGA system:
1. Generates line items (every user × every entitlement in scope)
2. Assigns items to reviewers
3. Sends notifications ("You have 147 items to review by March 30")
4. Opens the review interface

### Step 3: Review Period

Reviewers log in and see something like:

```
┌─────────────────────────────────────────────────────────────────┐
│ ACCESS CERTIFICATION: Q1 2025 Finance Team Review               │
│ Due: March 30, 2025 │ Progress: 43/147 items reviewed          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│ EMPLOYEE: Maria Chen (Senior Analyst → Promoted to Manager)     │
│ ┌───────────────────────────────────────────────────────────┐   │
│ │ Entitlement              │ Risk │ Recommendation │ Decision│   │
│ ├───────────────────────────┼──────┼────────────────┼─────────│   │
│ │ SAP FI - Post Journal    │ High │ ⚠️ SoD Risk   │ [    ]  │   │
│ │ SAP AP - Approve Payment │ High │ ⚠️ SoD Risk   │ [    ]  │   │
│ │ SharePoint - Finance Docs│ Low  │ ✅ Keep        │ [    ]  │   │
│ │ AWS - Dev Read Only      │ Med  │ ❓ Unused 90d  │ [    ]  │   │
│ │ Tableau - Finance Dash   │ Low  │ ✅ Keep        │ [    ]  │   │
│ └───────────────────────────────────────────────────────────┘   │
│                                                                  │
│ EMPLOYEE: Raj Patel (Software Engineer)                         │
│ ┌───────────────────────────┐                                   │
│ │ ...                        │                                   │
│ └───────────────────────────┘                                   │
└─────────────────────────────────────────────────────────────────┘
```

For each line item, reviewer decides:
- **Certify** (keep) — "Yes, they still need this"
- **Revoke** — "No, remove this access"
- **Reassign** — "I can't decide, send to someone else"

### Step 4: Execute Actions

After review closes:
- Certified items: No action needed (access remains)
- Revoked items: Provisioning engine removes access from target systems
- Unreviewed items: Default action (configurable — often auto-revoke or escalate)

### Step 5: Report Results

Generate compliance evidence:
- Campaign completion percentage
- Items certified vs. revoked
- Reviewers who completed on time vs. late
- Risk reduction achieved
- Evidence package for auditors

---

## Types of Certification

### Manager Certification

| Aspect | Details |
|--------|---------|
| **Scope** | All access for a manager's direct reports |
| **Reviewer** | The manager |
| **Frequency** | Quarterly (SOX), semi-annual (HIPAA) |
| **Volume** | 10-50 reports × 20-50 entitlements each = 200-2,500 items |
| **Challenge** | Managers don't understand technical entitlements |

### Application Certification

| Aspect | Details |
|--------|---------|
| **Scope** | All users who have access to a specific application |
| **Reviewer** | Application owner or data steward |
| **Frequency** | Semi-annually or annually |
| **Volume** | Could be thousands of users for popular apps |
| **Challenge** | App owners know the app but not all the users |

### Entitlement Certification

| Aspect | Details |
|--------|---------|
| **Scope** | All users with a specific high-risk entitlement |
| **Reviewer** | Security team or risk owner |
| **Frequency** | Event-triggered or quarterly |
| **Volume** | Usually smaller (focused on high-risk) |
| **Challenge** | Requires deep understanding of what the entitlement allows |

### Micro-Certification

| Aspect | Details |
|--------|---------|
| **Scope** | Single access item at point of change |
| **Reviewer** | Manager or relevant owner |
| **Frequency** | Real-time (triggered by event) |
| **Volume** | One item at a time |
| **Challenge** | Interrupts workflow; needs to be fast |

**Example:** Employee changes roles. IGA detects they have access that doesn't match new role. Sends micro-cert to new manager: "Maria has SAP FI access from her previous role. Should she keep it?"

---

## The Rubber-Stamp Problem (And Solutions)

### The Problem

Industry data consistently shows:
- ~90-95% of certification decisions are "Certify" (keep)
- Average review time per item: 3-5 seconds
- Reviewers click "approve all" to clear their queue

**Why this happens:**
1. **Volume overload:** 500 items to review? Ain't nobody reading each one.
2. **Incomprehensible names:** "SAP_FI_BUKRS_1000_F-02" means nothing to a manager
3. **Risk asymmetry:** Revoking access → angry employee, broken workflow. Keeping access → invisible risk.
4. **No consequence:** Nobody gets penalized for over-certifying. Under-certifying creates immediate pain.
5. **Time pressure:** "Complete by Friday or escalation to your VP"

### Solutions in Modern IGA

#### 1. Risk-Based Certification

Don't review everything equally. Focus human attention on HIGH RISK items:

```
Total access items: 10,000
├── Low risk (auto-certify): 7,000 (no human review needed)
├── Medium risk (light review): 2,000 (summary view, one-click)
└── High risk (deep review): 1,000 (forced justification required)
```

**How risk is calculated:**
- Entitlement sensitivity (admin access = high risk)
- User risk profile (new hire, contractor, excessive access)
- Usage patterns (unused for 90+ days = flag)
- SoD implications (contributing to a toxic combination)

#### 2. AI Recommendations

IGA suggests decisions based on:
- Peer comparison: "No one else in this role has this access" → suggest revoke
- Usage analytics: "This permission hasn't been used in 180 days" → suggest revoke
- Historical patterns: "This access was granted for a project that ended" → suggest revoke
- Context: "Just promoted to manager" → suggest keep management entitlements

#### 3. Plain Language Translation

Instead of: `SAP_FI_BUKRS_1000_T-CODE_FB01`
Show: `"Can post financial journal entries in SAP Finance (Company Code 1000)"`

**Impact:** Reviewer can actually understand what they're approving.

#### 4. Contextual Information

Show the reviewer:
- When access was granted and by whom
- Last time it was actually used
- Whether peers in the same role have it
- Business justification from original request
- Risk score with explanation

#### 5. Micro-Certifications (Continuous)

Instead of quarterly batch (500 items at once), review access at the MOMENT it becomes questionable:
- Role change → review carried-over access immediately
- 90 days unused → ping manager for quick decision
- New SoD rule → flag affected users immediately

---

## Campaign Orchestration at Scale

### Enterprise Reality

A large company running quarterly SOX certification:
- 50,000 employees
- Average 30 entitlements each = 1.5M line items
- 5,000 managers as reviewers
- 4-week review window
- Hundreds of applications in scope

### Operational Challenges

| Challenge | Details |
|-----------|---------|
| **Reviewer load distribution** | Some managers have 3 reports (easy), some have 40 (overwhelming) |
| **Delegation** | VP is on vacation during cert window — who reviews their team? |
| **Escalation** | 20% of reviewers haven't started with 3 days left — what do you do? |
| **Partial completion** | Manager reviewed 80% of items, ran out of time — what happens to the rest? |
| **Contested revocations** | User disagrees with revocation — appeal process? |
| **Timing** | Running cert during quarter-end when Finance is busiest = resistance |
| **Scope creep** | "Can we add 3 more apps to this campaign?" mid-flight |

### Campaign Scheduling

```
         Jan    Feb    Mar    Apr    May    Jun    Jul    Aug    Sep    Oct    Nov    Dec
SOX:     |←── Campaign ──→|                |←── Campaign ──→|
HIPAA:                          |←── Campaign ──→|                          |←── Campaign ──→|
SOD:     [spot]     [spot]     [spot]     [spot]     [spot]     [spot]     [spot]     [spot]
Micro:   ════════════════════════════════ continuous ═════════════════════════════════════════
```

---

## Certification Metrics

### What Good Looks Like

| Metric | Target | Red Flag |
|--------|--------|----------|
| Campaign completion rate | >95% | <80% (reviewers not engaging) |
| On-time completion | >85% | <60% (deadline not respected) |
| Revocation rate | 5-15% | <2% (rubber stamping) or >30% (poor provisioning) |
| Average review time per item | 10-30 seconds | <3 sec (not reading) or >5 min (UI problem) |
| Items per reviewer | <300 | >500 (reviewer fatigue) |
| Escalation rate | <10% | >20% (scope or assignment problems) |
| Time to execute revocations | <48 hours | >1 week (provisioning issues) |

### Audit Evidence Package

What auditors want to see from a completed certification:
1. Campaign definition (scope, timeline, criteria)
2. Reviewer assignments (who was responsible for what)
3. Completion evidence (all items reviewed, timestamps)
4. Decision breakdown (certified vs. revoked, with justifications)
5. Action evidence (revocations actually executed in target systems)
6. Exception documentation (any extensions, reassignments, overrides)

---

## Certification Anti-Patterns

| Anti-Pattern | Problem | Better Approach |
|-------------|---------|-----------------|
| "Certify everything annually" | Too infrequent, too massive | Risk-based frequency (high risk = quarterly, low = annual) |
| "Every manager reviews all" | Volume overwhelms | AI pre-filter, show only questionable items |
| "Binary: keep or revoke" | No nuance | Add "time-bound extension" option |
| "One massive campaign" | All-or-nothing | Split by department, stagger over weeks |
| "Blame managers for not completing" | Wrong root cause | Reduce volume, improve UX, provide recommendations |
| "Default to keep on expiry" | Defeats purpose | Default to revoke (or at minimum, escalate) |

---

> **🔧 Platform Engineering Lens**
>
> Certification campaigns are your **burst workload pattern.** Think Black Friday for e-commerce:
>
> - **Quarterly SOX cert launches** = sudden spike in concurrent users (5,000 managers hitting the platform in Week 1)
> - **Action execution** = burst of provisioning operations (thousands of revocations on campaign close)
> - **Deadline pressure** = the system MUST be available during the 4-week window (downtime = missed compliance deadline)
>
> **Platform engineering concerns:**
> - **Capacity planning:** Can the system handle 5,000 concurrent reviewers doing full-page loads of 300 items each?
> - **Job scheduling:** Post-campaign revocations hitting all connectors simultaneously
> - **SLOs during campaigns:** Latency matters more here (reviewer waiting 10 seconds for page load × 300 items = frustration → rubber stamping)
> - **Progress tracking:** Campaign dashboard showing real-time completion metrics (a monitoring problem)
> - **Notification infrastructure:** Thousands of emails/Slack messages for reminders and escalations
>
> If certification engine goes down during SOX cert window = compliance incident = board-level escalation. Plan accordingly.

---

## Self-Test Questions

1. What's the difference between a manager certification and an application certification? When would you use each?
2. Why do ~90% of certification decisions end up as "certify"? Name three reasons.
3. How does risk-based certification reduce rubber-stamping?
4. What happens to items that aren't reviewed when a campaign deadline expires?
5. What metrics would you track to know if your certification program is actually working (vs. just checkbox compliance)?
6. Why is micro-certification better than quarterly batch certification for security? Why do companies still do batch?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Certification Campaign** | Organized, time-bound review of access across a defined scope |
| **Certify (decision)** | Reviewer confirms access should remain |
| **Revoke (decision)** | Reviewer removes access |
| **Rubber-stamping** | Approving all items without genuine review |
| **Micro-certification** | Single-item certification triggered by an event (not batch) |
| **Risk-based certification** | Focusing human review on high-risk items, auto-certifying low-risk |
| **Campaign scope** | The set of users/entitlements included in a certification |
| **Reviewer** | Person responsible for certifying or revoking access (usually manager or app owner) |
| **Escalation** | Action taken when reviewer hasn't completed by deadline |
| **Completion rate** | Percentage of campaign items reviewed before deadline |
| **Revocation rate** | Percentage of items revoked (vs. certified) |
