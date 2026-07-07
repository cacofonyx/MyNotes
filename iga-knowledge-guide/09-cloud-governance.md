# Chapter 09: Cloud Governance (CPAM + CIEM)

> *"Cloud didn't just add more systems to govern. It fundamentally changed the nature of identity — ephemeral compute, infinite permissions, machine identities outnumbering humans 10:1."*

---

## Why Cloud Broke Traditional IGA

Traditional IGA was designed for a world where:
- Identities are humans
- Systems are finite and known
- Permissions are coarse (access/no-access)
- Lifecycle is months to years
- Changes are infrequent

Cloud reality:

| Traditional | Cloud |
|------------|-------|
| Hundreds of systems | Thousands of services per cloud account |
| Coarse permissions | AWS alone: 15,000+ unique IAM actions |
| Human identities | Machine identities outnumber humans 10:1 |
| Static accounts | Ephemeral (containers, serverless — minutes of lifespan) |
| Change = planned event | Continuous change (infrastructure-as-code, CI/CD) |
| Central IT controls | Every developer can create IAM resources |
| One auth boundary | Multi-cloud + hybrid = fragmented identity planes |

### The Permission Explosion

```
ON-PREM (circa 2010):
- 50 applications
- ~500 unique entitlements
- Manageable in spreadsheets (barely)

CLOUD (today):
- AWS: 15,000+ IAM actions across 300+ services
- Azure: 8,000+ unique permissions
- GCP: 5,000+ IAM permissions
- Per cloud account/subscription/project: multiply by number of environments
- Per application WITHIN cloud: custom IAM policies compound

A single org might have: 50,000+ effective unique permissions to govern
```

### The Machine Identity Problem

Traditional IGA focuses on humans. In cloud:

```
Identity Distribution in a Typical Cloud-Native Org:

Humans:     ████████  (~10%)
            (Employees, contractors)

Machines:   ████████████████████████████████████████████████  (~90%)
            (Service accounts, IAM roles, API keys, 
             Lambda execution roles, K8s service accounts,
             CI/CD pipeline identities, workload identities)
```

Each machine identity has permissions. Each can be compromised. Most are never reviewed, never rotated, never certified.

---

## CIEM: Cloud Infrastructure Entitlement Management

### What CIEM Does

CIEM answers: **"What can every identity (human + machine) actually DO across our cloud environments?"**

Not just "who has access to AWS" but "which specific API calls can they make, on which resources, under what conditions."

### Key CIEM Capabilities

#### 1. Multi-Cloud Visibility

```
┌─────────────────────────────────────────────────────┐
│                    CIEM Platform                      │
│                                                      │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐       │
│  │    AWS    │  │   Azure   │  │    GCP    │       │
│  │           │  │           │  │           │       │
│  │ IAM Users │  │ Entra ID  │  │ IAM       │       │
│  │ IAM Roles │  │ App Regs  │  │ Service   │       │
│  │ Policies  │  │ RBAC      │  │ Accounts  │       │
│  │ SCPs      │  │ Cond.Acc  │  │ Workload  │       │
│  │ Resource  │  │ PIM       │  │ Identity  │       │
│  │  Policies │  │ Custom    │  │ Custom    │       │
│  └───────────┘  └───────────┘  └───────────┘       │
│         │              │              │              │
│         └──────────────┼──────────────┘              │
│                        │                             │
│              ┌─────────┴─────────┐                   │
│              │ Unified View:     │                   │
│              │ "Who can do what  │                   │
│              │  across ALL clouds"│                   │
│              └───────────────────┘                   │
└─────────────────────────────────────────────────────┘
```

#### 2. Effective Permission Analysis

Cloud permissions are LAYERED. The effective permission is the intersection of multiple policies:

```
AWS Example:

Identity Policy (attached to user/role)
    ∩ (intersect with)
Resource Policy (on the S3 bucket, Lambda, etc.)
    ∩ (intersect with)
Organization SCP (Service Control Policy - guardrails)
    ∩ (intersect with)
Permission Boundary (if set)
    = Effective Permission (what they can actually do)
```

CIEM must calculate this intersection to answer: "Can User X delete this S3 bucket?" The answer depends on ALL layers.

#### 3. Overprivileged Identity Detection

The #1 cloud security problem: identities have far more permissions than they use.

```
Granted Permissions:      ████████████████████████████████  (100%)
Actually Used:            ████████  (25%)
Overprivileged Gap:              ████████████████████████  (75% unnecessary)
```

**Industry stat:** Average cloud identity uses <5% of granted permissions. The remaining 95% is attack surface.

**CIEM detects:**
- Unused permissions (granted but never exercised)
- Unused identities (service accounts that haven't authenticated in 90 days)
- Overly broad policies ("*" permissions, admin access)
- Cross-account access that shouldn't exist

#### 4. Right-Sizing Recommendations

"This Lambda function has AdministratorAccess but only ever calls S3:GetObject and DynamoDB:Query."

CIEM recommends: Replace AdministratorAccess with a least-privilege policy containing only the 2 actions actually used.

---

## CPAM: Cloud Privileged Access Management

### What CPAM Does

CPAM manages **elevated/privileged access** to cloud environments. "Admin access when you need it, only for as long as you need it."

### The Problem CPAM Solves

Traditional approach:
- Cloud admins have standing privileged access (always-on admin)
- If their credentials are compromised → attacker has full admin immediately
- No time-bound limitation
- Audit shows "admin access granted 3 years ago, used daily" — can't distinguish legitimate use from compromise

CPAM approach:
- Nobody has standing admin access
- When admin access needed → request through CPAM
- Granted Just-in-Time (JIT), expires automatically
- Session recorded, actions logged
- Anomalous usage detected in real-time

### Just-in-Time (JIT) Access Pattern

```
Normal State:           Request Phase:          Active Phase:        Expiry:
┌───────────┐          ┌───────────┐          ┌───────────┐       ┌───────────┐
│ Engineer  │          │ Engineer  │          │ Engineer  │       │ Engineer  │
│           │          │           │          │           │       │           │
│ Perms:    │          │ "I need   │          │ Perms:    │       │ Perms:    │
│ READ-ONLY │          │  admin for│          │ READ-ONLY │       │ READ-ONLY │
│           │          │  2 hours" │          │ + ADMIN   │       │           │
│           │          │           │          │ (2hr TTL) │       │ (back to  │
└───────────┘          └───────────┘          └───────────┘       │  normal)  │
                             │                      │              └───────────┘
                             ▼                      ▼
                       ┌──────────┐          ┌──────────┐
                       │ Approve  │          │ Session  │
                       │ (auto or │          │ recorded │
                       │  manual) │          │ Actions  │
                       └──────────┘          │ logged   │
                                             └──────────┘
```

### CPAM vs Traditional PAM

| Aspect | Traditional PAM (CyberArk) | CPAM (Saviynt) |
|--------|---------------------------|----------------|
| Designed for | Data center, on-prem servers | Cloud environments |
| Identity model | Shared accounts (root, admin) | Federated, individual cloud identities |
| Vault concept | Store passwords in vault, check out | No passwords — assume cloud IAM roles |
| Session type | SSH/RDP to a server | Cloud console, API calls, CLI |
| Scale | Hundreds of privileged accounts | Thousands of cloud roles/identities |
| Ephemeral | No — vault persists | Yes — access exists only during session |
| Multi-cloud | Bolted on | Native (AWS + Azure + GCP in one view) |

### CPAM Key Capabilities

| Capability | Description |
|-----------|-------------|
| **JIT Elevation** | Grant admin permissions temporarily with auto-expiry |
| **Zero Standing Privileges** | No permanent admin access — all JIT |
| **Session Recording** | Record what admin does during elevated session |
| **Multi-cloud Support** | Same workflow for AWS, Azure, GCP |
| **Approval Workflows** | Configurable: auto-approve for low-risk, manual for high-risk |
| **Anomaly Detection** | Flag unusual admin behavior during session |
| **Emergency Access** | Break-glass procedures for incidents (fast-track approval) |

---

## Cloud Governance Challenges

### Challenge 1: Shadow Cloud

Developers create cloud resources (and IAM policies) without governance awareness:
- New IAM roles created in CI/CD pipelines
- Service accounts proliferating
- Cross-account trust relationships added ad-hoc
- API keys generated and never rotated

**IGA approach:** Continuous discovery. Scan cloud environments for new identities/permissions that weren't provisioned through IGA. Flag for review.

### Challenge 2: Infrastructure-as-Code (IaC) Permissions

Terraform, CloudFormation, Pulumi create IAM resources. How do you govern that?

```
Developer writes Terraform:
  resource "aws_iam_role" "my_service_role" {
    assume_role_policy = ... (too broad?)
    inline_policy = ... (admin access?)
  }

Deploy pipeline executes it → new IAM role exists in AWS

Question: Did anyone review whether this role is appropriate?
          Does it violate least privilege?
          Does it create SoD issues?
```

**Emerging answer:** IGA/CIEM integration with CI/CD — scan IaC templates BEFORE deployment for overly permissive policies. "Shift left" for identity governance.

### Challenge 3: Kubernetes Identity

Kubernetes has its own identity layer:
- Service accounts (K8s internal)
- RBAC roles and role bindings
- Workload identity mapping to cloud IAM
- Namespace-level isolation

```
┌─────────────────────────────────────────────┐
│           Kubernetes Cluster                 │
│                                              │
│  ┌──────────┐    ┌──────────────────────┐   │
│  │ Pod      │    │ K8s Service Account  │   │
│  │ (workload)│───▶│ (K8s identity)       │   │
│  └──────────┘    └──────────┬───────────┘   │
│                              │               │
│                              │ Workload      │
│                              │ Identity      │
│                              ▼               │
│                   ┌────────────────────┐     │
│                   │ Cloud IAM Role     │     │
│                   │ (AWS/Azure/GCP)    │     │
│                   └────────────────────┘     │
└─────────────────────────────────────────────┘

Governance question: Which pods can assume which cloud roles?
                     Is that mapping appropriate?
                     Who approved it?
```

### Challenge 4: Multi-Cloud Correlation

Same human has identities across multiple clouds. Without correlation:
- AWS: admin in 3 accounts
- Azure: contributor in 5 subscriptions  
- GCP: owner of 2 projects

Each cloud manages its own IAM. Nobody has the unified view until CIEM correlates them.

### Challenge 5: Ephemeral Identities

Serverless functions, containers, spot instances — identities that exist for minutes:
- Lambda function executes for 30 seconds with IAM role
- Container runs for 4 hours then terminates
- Spot instance lives for 2 hours

Traditional IGA lifecycle (joiner/mover/leaver) doesn't map. These identities are born and die faster than any review cycle.

---

## Saviynt's Cloud Governance Approach

### Unified Model

```
┌─────────────────────────────────────────────────────────┐
│                Saviynt EIC Platform                       │
│                                                          │
│  ┌─────────────────────────────────────────────────────┐│
│  │              Identity Warehouse                      ││
│  │  Human: employees, contractors                       ││
│  │  Machine: service accounts, IAM roles, workloads    ││
│  │  Cloud: AWS roles, Azure SPs, GCP SAs               ││
│  │  All correlated to same governance model             ││
│  └─────────────────────────────────────────────────────┘│
│                                                          │
│  ┌──────────┐ ┌──────────┐ ┌──────────────────────────┐│
│  │   IGA    │ │   CPAM   │ │        CIEM              ││
│  │          │ │          │ │  Effective permissions    ││
│  │ Lifecycle│ │ JIT      │ │  Right-sizing            ││
│  │ Certs    │ │ Elevation│ │  Anomaly detection       ││
│  │ Roles    │ │ Sessions │ │  Drift monitoring        ││
│  │ SoD      │ │ Recording│ │  Multi-cloud correlation ││
│  └──────────┘ └──────────┘ └──────────────────────────┘│
└─────────────────────────────────────────────────────────┘
```

**The convergence advantage:** Same policy engine governs human IGA access AND cloud privileged access AND cloud entitlement posture. Single risk score incorporating all three views.

---

## Cloud Governance Maturity Model

| Level | Description | What It Looks Like |
|-------|-------------|-------------------|
| **1: Blind** | No visibility into cloud identities/permissions | "How many IAM roles do we have?" "No idea." |
| **2: Visible** | Can see what exists but no governance | Dashboard showing cloud identities, no action taken |
| **3: Monitored** | Alerts on dangerous patterns | "New admin role created" triggers notification |
| **4: Governed** | Policies enforced, violations blocked | Overprivileged identity can't be created without approval |
| **5: Optimized** | Continuous right-sizing, JIT everywhere, minimal standing privilege | Least privilege is the default, exceptions are temporary and audited |

Most organizations are at Level 1-2. The market opportunity is moving them to 4-5.

---

> **🔧 Platform Engineering Lens**
>
> Cloud governance is where your expertise is DIRECTLY applicable:
>
> **You live in this world already:**
> - You manage Kubernetes clusters → you understand service accounts, RBAC, workload identity
> - You write Terraform → you know how IAM policies get created in CI/CD
> - You manage cloud accounts → you've dealt with IAM policy complexity
> - You've probably given developers too-broad permissions "to unblock them" → you understand the pressure
>
> **Platform engineering opportunities in cloud governance:**
> - **Golden paths for IAM:** Pre-approved, least-privilege IAM templates developers can use
> - **Policy-as-code:** OPA/Rego policies checking IAM before deployment
> - **Self-service with guardrails:** Developers request cloud access through platform portal, auto-granted within policy bounds
> - **Observability for identity:** Monitoring permission usage, detecting drift, alerting on anomalies
> - **Developer education:** Making least-privilege EASY, not just mandated
>
> **The key insight:** Cloud governance shouldn't be a gate that slows developers. It should be a PLATFORM CAPABILITY that makes least-privilege the path of least resistance. That's a platform engineering challenge, not just a security tooling challenge.

---

## Self-Test Questions

1. Why can't traditional IGA (designed for on-prem) handle cloud permissions effectively?
2. What's the difference between CIEM and CPAM? How do they complement each other?
3. Explain "effective permissions" in AWS — why can't you just look at the IAM policy attached to a user?
4. What is Just-in-Time (JIT) access and why is it better than standing privileged access?
5. Why are machine identities a bigger governance challenge in cloud than humans?
6. How would you apply platform engineering thinking to make cloud governance developer-friendly?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **CIEM** | Cloud Infrastructure Entitlement Management — visibility + governance of cloud permissions |
| **CPAM** | Cloud Privileged Access Management — JIT admin access for cloud |
| **JIT Access** | Just-in-Time — permissions granted temporarily and auto-expire |
| **Zero Standing Privileges** | No permanent admin access exists; all elevated access is JIT |
| **Effective Permissions** | Actual permissions after all policy layers are evaluated |
| **Right-Sizing** | Reducing permissions to only what's actually used |
| **Overprivileged** | Having more permissions than needed (attack surface) |
| **Machine Identity** | Non-human identity (service account, IAM role, workload) |
| **Cross-Account Trust** | IAM relationship allowing one cloud account to access another |
| **Permission Boundary** | AWS concept limiting maximum possible permissions |
| **SCP** | Service Control Policy — organization-wide permission guardrails in AWS |
| **Workload Identity** | Cloud identity assigned to a running workload (pod, function) |
| **Shadow Cloud** | Cloud resources created outside governance processes |
