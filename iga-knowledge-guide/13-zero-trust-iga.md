# Chapter 13: Zero Trust & IGA Convergence

> *"Zero Trust isn't a product. It's an architecture principle. And IGA provides one of its most critical inputs: continuous knowledge of who should have access to what."*

---

## Zero Trust in 60 Seconds

**Old model (perimeter-based):**
- "Inside the network = trusted"
- VPN + firewall = security
- Once you're in, you can access most things

**Zero Trust model:**
- "Never trust, always verify"
- Every access request is authenticated and authorized, regardless of network location
- Least privilege, always. No implicit trust.

```
PERIMETER MODEL:                    ZERO TRUST MODEL:
┌──────────────────────┐            ┌──────────────────────┐
│     "Trusted" Zone    │            │  Nothing is trusted   │
│                       │            │                       │
│  VPN → You're in!    │            │  Every request:       │
│  Access everything   │            │  - Who are you?       │
│                       │            │  - What device?       │
│                       │            │  - What's the context?│
│  Firewall = moat     │            │  - Should you STILL   │
│                       │            │    have this access?  │
└──────────────────────┘            └──────────────────────┘
```

### Zero Trust Core Principles

| Principle | Meaning |
|-----------|---------|
| **Verify explicitly** | Always authenticate and authorize based on all available data points |
| **Least privilege** | Limit access to just what's needed, just when needed |
| **Assume breach** | Minimize blast radius, segment access, verify end-to-end |

---

## Where IGA Fits in Zero Trust

Zero Trust is an ARCHITECTURE. It needs multiple components working together:

```
┌─────────────────────────────────────────────────────────────────────┐
│                     ZERO TRUST ARCHITECTURE                           │
│                                                                      │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐   │
│  │  Identity  │  │   Device   │  │  Network   │  │ Application│   │
│  │  Security  │  │   Trust    │  │  Segment.  │  │  Security  │   │
│  │            │  │            │  │            │  │            │   │
│  │ IGA ← HERE│  │ MDM/EDR    │  │ Micro-seg  │  │ App-level  │   │
│  │ AM/SSO    │  │ Device     │  │ SASE       │  │ authZ      │   │
│  │ PAM       │  │ posture    │  │ ZTNA       │  │ API gw     │   │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘   │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                    POLICY ENGINE                               │   │
│  │  Combines signals from all pillars to make access decisions   │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                    OBSERVABILITY                               │   │
│  │  Continuous monitoring, analytics, threat detection            │   │
│  └──────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

### IGA's Role in Zero Trust

IGA provides the **KNOWLEDGE** layer that Zero Trust needs:

| Zero Trust Question | IGA Provides the Answer |
|--------------------|------------------------|
| "Should this identity have this access?" | Access governance (certs, reviews, policies) |
| "What's the minimum access they need?" | Role engineering + right-sizing |
| "Has this access been reviewed recently?" | Certification records |
| "Does this access violate separation rules?" | SoD policy enforcement |
| "Is this identity still valid?" | Lifecycle management (is the person still employed?) |
| "What's the risk of this access grant?" | Risk scoring |

Without IGA, Zero Trust doesn't know what "appropriate access" looks like. It can enforce access decisions — but it needs IGA to INFORM those decisions.

---

## From Periodic to Continuous: The IGA Shift

### Traditional IGA: Periodic Governance

```
Q1 Cert → [3 months of no governance] → Q2 Cert → [3 months] → Q3 Cert

Problems:
- Between certs, access drift goes undetected
- 3-month-old certification ≠ current state
- By the time you review, damage may already be done
```

### Zero Trust IGA: Continuous Governance

```
═══════════════════════════ CONTINUOUS MONITORING ═══════════════════════
  │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │ │
  Event-driven reviews:
  - Role change → immediate review
  - Unused access 30 days → alert
  - Anomalous usage → investigate
  - New SoD conflict → block
  - Risk score increase → re-certify
  
  Periodic certs still exist (audit requirement) but are CONFIRMATIONS
  of continuous governance, not the primary control.
```

### What Continuous Governance Looks Like

| Signal | Action | Timeframe |
|--------|--------|-----------|
| Person changes role | Re-evaluate all access | Within hours |
| Access unused 30 days | Alert manager, suggest revoke | Daily check |
| Risk score increases | Trigger targeted review | Real-time |
| SoD rule added/changed | Scan all access against new rule | Within hours |
| New vulnerability in target system | Review who has access to affected system | Immediate |
| Peer leaves company | Review shared service accounts/delegations | Same day |
| External threat intel (credential leak) | Force re-authentication + access review | Immediate |

---

## Adaptive Access: Context-Aware Decisions

### The Model

Zero Trust + IGA together enable ADAPTIVE access decisions — not binary (allow/deny) but contextual:

```
ACCESS REQUEST EVALUATION:

┌──────────────────────────────────────────────────┐
│                                                   │
│  Identity ──────────┐                             │
│  (who you are,      │                             │
│   your role,        │                             │
│   your risk score)  │                             │
│                     ├──▶ POLICY ENGINE ──▶ DECISION│
│  Context ───────────┤                             │
│  (device, location, │    Possible outcomes:       │
│   time, behavior)   │    ✅ Allow (full access)    │
│                     │    ⚡ Allow (restricted)     │
│  Request ───────────┘    🔒 Allow (monitored)     │
│  (what access,           ⏰ Allow (time-limited)  │
│   why needed)            ❌ Deny                  │
│                          🔐 Require step-up auth  │
│                                                   │
└──────────────────────────────────────────────────┘
```

### Scenario: Same Person, Different Contexts

```
Maria requests access to customer database:

Context 1: Monday 10 AM, corporate laptop, Austin office, normal behavior
→ DECISION: Allow (full access, normal)

Context 2: Saturday 2 AM, personal device, foreign IP, first time this hour
→ DECISION: Require step-up auth (MFA) + allow restricted (read-only) + enable monitoring

Context 3: Same as 2, but Maria's risk score spiked yesterday (flagged by ML)
→ DECISION: Deny + alert security team + require investigation before re-enable
```

### IGA's Input to Adaptive Decisions

| IGA Data Point | How It Informs Adaptive Access |
|---------------|-------------------------------|
| Risk score | Higher risk → stricter access controls |
| Last certification date | Stale certification → require re-review |
| Peer comparison | Access that peers don't have → higher scrutiny |
| Usage patterns | Unused access → reduce scope |
| SoD status | Existing violations → deny additional access |
| Employment status | Contractor nearing end date → restrict new grants |

---

## Identity-First Security Architecture

### The Emerging Model

Organizations moving to "identity-first" security:

```
OLD SECURITY MODEL:                     IDENTITY-FIRST MODEL:
┌────────────────────────┐              ┌────────────────────────┐
│ Network is primary     │              │ Identity is primary     │
│ control plane          │              │ control plane           │
│                        │              │                         │
│ 1. Protect the network │              │ 1. Know all identities  │
│ 2. Control network     │              │ 2. Govern all access    │
│    access              │              │ 3. Monitor all behavior │
│ 3. Add identity        │              │ 4. Use network as ONE   │
│    on top (maybe)      │              │    signal (not primary) │
└────────────────────────┘              └────────────────────────┘
```

### Why Identity Becomes Primary

1. **No perimeter to defend:** Cloud, remote work, SaaS — there IS no network boundary
2. **Credentials are #1 attack vector:** 80%+ of breaches involve compromised credentials
3. **Data moves:** It's in AWS, Azure, SaaS apps, APIs — network-centric controls can't follow it
4. **Machine identities dominate:** APIs call APIs. Services call services. Network = irrelevant for service-to-service access.

### IGA as the Foundation

```
IDENTITY-FIRST SECURITY STACK:

┌───────────────────────────────────────────────────────┐
│  LAYER 4: Threat Detection & Response                  │
│  (ITDR, UEBA, SOC)                                    │
├───────────────────────────────────────────────────────┤
│  LAYER 3: Access Enforcement                           │
│  (SSO, ZTNA, conditional access, PAM)                 │
├───────────────────────────────────────────────────────┤
│  LAYER 2: Access Governance ← IGA IS THIS LAYER      │
│  (What access should exist, policies, reviews)        │
├───────────────────────────────────────────────────────┤
│  LAYER 1: Identity Foundation                          │
│  (Directory, lifecycle, identity data quality)         │
└───────────────────────────────────────────────────────┘
```

IGA sits at Layer 2 — the GOVERNANCE layer that informs enforcement (Layer 3) and detection (Layer 4). Without good governance, enforcement doesn't know what's right, and detection doesn't know what's wrong.

---

## ITDR: Identity Threat Detection & Response

### What Is ITDR?

A newer category (Gartner coined ~2022) focused specifically on detecting and responding to identity-based threats:
- Credential theft
- Identity impersonation
- Privilege escalation
- Lateral movement via identity compromise
- Golden ticket / golden SAML attacks

### IGA + ITDR Integration

```
IGA provides:                    ITDR provides:
┌────────────────────────┐      ┌────────────────────────┐
│ - Who should have what │      │ - Who is doing what    │
│ - What's normal access │      │ - What's anomalous     │
│ - What's over-provisiond│  ←──▶  │ - What looks like      │
│ - What violates policy │      │   an attack            │
│ - What's unused        │      │ - What needs response  │
└────────────────────────┘      └────────────────────────┘
        │                               │
        └───────── Together ────────────┘
                     │
        "This behavior is anomalous AND
         this identity is over-provisioned
         AND this access wasn't recently certified
         → HIGH CONFIDENCE THREAT"
```

---

## Implementing Zero Trust with IGA: A Practical Roadmap

### Maturity Stages

| Stage | Description | IGA Actions |
|-------|-------------|-------------|
| **Stage 1** | Basic hygiene | Lifecycle automation, quarterly certs, basic RBAC |
| **Stage 2** | Visibility | Full entitlement mapping, reconciliation, peer analysis |
| **Stage 3** | Least privilege | Right-sizing, SoD enforcement, unused access removal |
| **Stage 4** | Continuous | Event-driven certs, real-time risk scoring, adaptive access |
| **Stage 5** | Autonomous | AI-driven governance, self-healing, predictive |

Most enterprises are at Stage 1-2. Leading organizations are at Stage 3-4. Stage 5 is aspirational.

---

> **🔧 Platform Engineering Lens**
>
> Zero Trust architecture maps directly to platform engineering patterns:
>
> | Zero Trust Concept | Platform Engineering Equivalent |
> |-------------------|-------------------------------|
> | Never trust, always verify | No implicit trust between services (mTLS, service mesh) |
> | Least privilege | Pod security, RBAC, network policies — minimum permissions |
> | Continuous verification | Health checks, continuous deployment verification |
> | Micro-segmentation | Namespace isolation, network policies, service mesh |
> | Context-aware decisions | Adaptive scaling, feature flags, progressive delivery |
>
> **The insight for your role:** Platform engineering teams are already implementing Zero Trust principles for INFRASTRUCTURE (service mesh, pod security, network policies). IGA extends these same principles to HUMAN access. The philosophy is identical — the implementation layers are different.
>
> Your platform team likely already has opinions about: mTLS everywhere, principle of least privilege for service accounts, workload identity, and continuous verification. Those same opinions apply to human access governance. IGA is the tool that implements them.

---

## Self-Test Questions

1. What are the three core principles of Zero Trust? How does IGA serve each one?
2. What's the difference between periodic governance (traditional IGA) and continuous governance (Zero Trust IGA)?
3. How does "adaptive access" differ from binary allow/deny decisions? What data does it need from IGA?
4. What is ITDR and how does it complement IGA?
5. In an "identity-first" security architecture, where does IGA sit and why is it foundational?
6. How would you explain the connection between Zero Trust and your existing platform engineering work to a peer?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **Zero Trust** | Security model: never trust implicitly, always verify explicitly |
| **Continuous Governance** | Always-on access evaluation vs. periodic batch review |
| **Adaptive Access** | Context-aware access decisions (not binary allow/deny) |
| **ITDR** | Identity Threat Detection & Response — detecting identity-based attacks |
| **ZTNA** | Zero Trust Network Access — network access based on identity + context |
| **Micro-segmentation** | Dividing network into small zones with independent access controls |
| **Least Privilege** | Providing minimum access needed for the task, nothing more |
| **Identity-First Security** | Architecture where identity (not network) is the primary control plane |
| **Step-up Authentication** | Requiring additional verification when risk is elevated |
| **Blast Radius** | Scope of damage if a credential is compromised |
| **Assume Breach** | Design principle: plan as if attackers are already inside |
