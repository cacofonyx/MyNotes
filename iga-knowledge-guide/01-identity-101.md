# Chapter 01: Identity 101

> *"Identity is the new perimeter."* — Every security vendor since 2019, but they're not wrong.

---

## What Is Digital Identity?

A digital identity is the collection of attributes that represent a person (or system, or service) in the digital world. Think of it as the answer to three questions:

1. **Who are you?** (Identity)
2. **How do you prove it?** (Authentication)
3. **What are you allowed to do?** (Authorization)

### Physical World Analogy

| Physical World | Digital World |
|---------------|---------------|
| Your face / passport | Username, employee ID, digital certificate |
| Showing your ID at the door | Authentication (password, MFA, biometric) |
| Your badge level / key card zones | Authorization (roles, permissions, entitlements) |
| Building security checking your badge hasn't expired | Access certification / continuous verification |
| HR onboarding giving you a badge | Identity provisioning |
| HR collecting your badge on last day | De-provisioning |

---

## The Identity Ecosystem: A Map

The identity and security world has multiple overlapping domains. Here's how they relate:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    IDENTITY & ACCESS MANAGEMENT (IAM)                │
│                    The broadest umbrella term                        │
│                                                                     │
│  ┌───────────────────────┐  ┌──────────────────────────────────┐   │
│  │         IGA           │  │              AM                   │   │
│  │  Identity Governance  │  │       Access Management           │   │
│  │  & Administration     │  │  (SSO, Federation, MFA)           │   │
│  │                       │  │                                    │   │
│  │  - Who has what       │  │  - How you log in                  │   │
│  │  - Should they have it│  │  - Session management              │   │
│  │  - Prove it to auditor│  │  - Okta, Azure AD, Ping            │   │
│  └───────────────────────┘  └──────────────────────────────────┘   │
│                                                                     │
│  ┌───────────────────────┐  ┌──────────────────────────────────┐   │
│  │         PAM           │  │             CIEM                  │   │
│  │  Privileged Access    │  │  Cloud Infrastructure             │   │
│  │  Management           │  │  Entitlement Management           │   │
│  │                       │  │                                    │   │
│  │  - Admin/root access  │  │  - Cloud permissions specifically  │   │
│  │  - Vault, session rec │  │  - AWS IAM, Azure RBAC, GCP IAM   │   │
│  │  - CyberArk, BeyondT  │  │  - Overprivileged cloud identities│   │
│  └───────────────────────┘  └──────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### The Key Distinctions

| Domain | Core Question | Example Products |
|--------|--------------|-----------------|
| **IAM** (umbrella) | Everything about digital identity | Broad category |
| **AM** (Access Management) | "How do users authenticate and get sessions?" | Okta, Azure AD, Ping Identity, ForgeRock |
| **IGA** (Identity Governance) | "Who has what access, should they, and can we prove it?" | Saviynt, SailPoint, One Identity |
| **PAM** (Privileged Access) | "How do we control and monitor admin access?" | CyberArk, BeyondTrust, Delinea |
| **CIEM** (Cloud Entitlements) | "Who has what in AWS/Azure/GCP?" | Ermetic, CloudKnox (now Microsoft), Saviynt |

### Where IGA Sits — The Governance Layer

Think of it this way:
- **AM** handles the front door (login)
- **PAM** handles the vault (admin access)
- **CIEM** handles cloud permissions
- **IGA** is the **governance layer over ALL of them** — it asks "should this access exist?" and proves the answer to auditors

IGA doesn't replace AM or PAM. It governs them. It's the system that says:
- "This person was hired → provision them in AD, Okta, AWS, SAP"
- "This person changed roles → adjust their permissions across all systems"
- "This person left → revoke everything, everywhere, NOW"
- "Auditor asks 'who can approve payments over $10K?' → here's the certified answer"

---

## Authentication vs. Authorization: The Core Split

These get confused constantly. Clear distinction:

### Authentication (AuthN)

**Question:** "Are you who you claim to be?"

**Mechanisms:**
- Something you know (password)
- Something you have (phone, hardware key)
- Something you are (fingerprint, face)
- Somewhere you are (IP, geolocation)

**Example:** You type your password and tap your YubiKey. System confirms: "Yes, this is sree@company.com."

### Authorization (AuthZ)

**Question:** "Now that we know who you are, what can you do?"

**Mechanisms:**
- Role-Based Access Control (RBAC) — you have role X, role X includes permissions A, B, C
- Attribute-Based Access Control (ABAC) — your department + location + clearance level determines access
- Policy-Based Access Control (PBAC) — rules engine evaluates context dynamically

**Example:** You're authenticated as sree@company.com. But can you access the production database? The payroll system? The board deck? That's authorization.

### IGA Is Primarily About Authorization Governance

IGA cares less about HOW you logged in and more about WHAT you can access once you're in. Specifically:
- Is your access appropriate for your role?
- Was it properly approved?
- Is it still needed?
- Can we prove all of the above to an auditor?

---

## Identity Lifecycle: The Core Pattern

Every person in an organization goes through a lifecycle. IGA manages the identity implications at each stage:

```
┌──────────┐     ┌──────────┐     ┌──────────┐     ┌──────────┐
│  JOINER  │ ──→ │  MOVER   │ ──→ │  MOVER   │ ──→ │  LEAVER  │
│          │     │          │     │          │     │          │
│ Day 1    │     │ Promoted │     │ Transfer │     │ Last day │
│ Hire     │     │ New role │     │ New dept │     │ Resign   │
└──────────┘     └──────────┘     └──────────┘     └──────────┘
     │                │                │                │
     ▼                ▼                ▼                ▼
 Grant base       Add new          Remove old       Revoke ALL
 access          access           access +         access NOW
 (birthright)    (role change)    add new          (time-critical)
```

### Joiner (Day 1)

New hire starts. They need:
- Email account
- Laptop enrollment
- Access to HR systems
- Team-specific tools (Jira, GitHub, Slack channels)
- Maybe cloud console access

**IGA's job:** Automatically provision all "birthright" access based on role, department, location. No tickets. No waiting.

### Mover (Role Change)

Person gets promoted, transfers departments, or takes on a new project.

**IGA's job:** 
- Grant new access needed for new role
- **Remove** access no longer needed (this is where most orgs fail — access accumulates)
- Detect toxic combinations (e.g., now they can both create AND approve purchase orders — SoD violation)

### Leaver (Last Day)

Person resigns, is terminated, or contract ends.

**IGA's job:**
- Revoke ALL access across ALL systems within minutes (not days)
- Disable accounts, not just lock them
- Prove to auditors that access was revoked (audit trail)

**The scary stat:** Industry research shows ~30% of employees retain access to at least one system after leaving an organization. This is the problem IGA exists to solve.

---

## Why "Just Use AD" Isn't Enough

Many engineers first think: "We have Active Directory / Okta / Azure AD. Isn't that identity management?"

Yes, but only for a subset:

| Capability | AD/Okta/Azure AD | IGA |
|-----------|-----------------|-----|
| User directory | ✅ | Uses it as source |
| Authentication (SSO) | ✅ | Not its job |
| Basic group membership | ✅ | Too coarse |
| Fine-grained entitlements | ❌ | ✅ |
| Access certification | ❌ | ✅ |
| SoD policy enforcement | ❌ | ✅ |
| Cross-system governance | ❌ (single system) | ✅ (hundreds of systems) |
| Compliance reporting | Basic | ✅ Purpose-built |
| Automated lifecycle | Basic | ✅ Complex workflows |
| Role mining/analytics | ❌ | ✅ |

The gap: AD tells you "sree is in the Finance group." IGA tells you "sree has 47 entitlements across 12 systems, 3 of which violate SoD policy, 2 of which haven't been used in 90 days, and all of which were certified by their manager last quarter."

---

## Scale: Why This Is a Real Problem

For a small company (50 people, 10 apps), you can manage access manually. Someone joins, IT creates accounts. Someone leaves, IT disables them. Manageable.

Now scale:

| Dimension | Small Co | Enterprise | Why IGA Is Needed |
|-----------|----------|-----------|-------------------|
| Employees | 50 | 50,000 | Can't manually manage 50K × N systems |
| Applications | 10 | 500+ | Each with its own permission model |
| Entitlements per person | 5-10 | 50-200 | Combinatorial explosion |
| Role changes per year | Few | Thousands | Each needs access adjustments |
| Compliance requirements | Minimal | SOX, HIPAA, etc. | Must prove governance to auditors |
| Audit frequency | Never | Quarterly/continuous | Need automated evidence |

At enterprise scale, without IGA:
- People accumulate access like barnacles (never revoked, always added)
- Nobody knows who has access to what
- Audit preparation takes months of manual spreadsheet work
- SoD violations hide in the complexity
- Departed employees retain access for weeks or months

---

> **🔧 Platform Engineering Lens**
>
> Think of IGA as an **internal platform** that serves security/compliance teams the same way your infrastructure platform serves developers. It has:
> - **APIs** (connectors to target systems)
> - **Workflows** (provisioning, certification, request/approval)
> - **SLOs** (provisioning latency, revocation speed, certification completion rates)
> - **Consumers** (security team, compliance team, auditors, end users requesting access)
> - **Reliability concerns** (if provisioning is down, new hires can't work; if de-provisioning is down, security risk accumulates)
>
> Your instinct to think about this as infrastructure — not just a "governance tool" — is the right instinct.

---

## Self-Test Questions

1. What's the difference between authentication and authorization? Which does IGA primarily govern?
2. If someone asks "why can't we just use Azure AD for identity governance?" — what are the 3 key gaps?
3. What are the three stages of the identity lifecycle (Joiner/Mover/Leaver)? Which is hardest to get right and why?
4. How is IGA different from PAM? From CIEM? Where do they overlap?
5. Why does access management at scale require automation — what breaks when you try to do it manually?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Digital Identity** | Collection of attributes representing a person/system digitally |
| **Authentication (AuthN)** | Verifying someone IS who they claim to be |
| **Authorization (AuthZ)** | Determining what a verified identity is ALLOWED to do |
| **IAM** | Identity & Access Management — the broadest umbrella |
| **IGA** | Identity Governance & Administration — governance of who-has-what |
| **AM** | Access Management — SSO, login, session management |
| **PAM** | Privileged Access Management — admin/root access control |
| **CIEM** | Cloud Infrastructure Entitlement Management — cloud permissions |
| **Provisioning** | Creating accounts and granting access in target systems |
| **De-provisioning** | Removing access when no longer needed |
| **Birthright Access** | Access automatically granted based on role/dept at hire |
| **Entitlement** | A specific, granular permission (e.g., "read access to S3 bucket X") |
