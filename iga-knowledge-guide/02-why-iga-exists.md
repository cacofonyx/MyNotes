# Chapter 02: Why IGA Exists

> *"Nobody buys IGA because they want IGA. They buy it because an auditor said 'prove it' and they couldn't."*

---

## The Origin Story: Compliance Made This Market

IGA didn't emerge because engineers thought "we should govern identity better." It emerged because:

1. **Massive corporate fraud** (Enron, WorldCom, 2001-2002)
2. **Government said "never again"** (Sarbanes-Oxley Act, 2002)
3. **Auditors started asking** "who has access to financial systems and can you prove appropriate controls?"
4. **Companies couldn't answer** → scrambled to build/buy tools
5. **A market was born** (first IGA products ~2003-2005)

The fundamental question IGA answers for auditors:

> **"Who has access to what, who approved it, and is it still appropriate?"**

If you can't answer this question across all your systems within hours (not weeks), you have a governance problem.

---

## The Compliance Drivers

### SOX (Sarbanes-Oxley Act, 2002)

**Applies to:** All US publicly traded companies

**What it requires (identity-relevant parts):**
- Section 302: CEO/CFO must certify financial reports are accurate
- Section 404: Companies must maintain internal controls over financial reporting
- **Identity implication:** Must prove that access to financial systems is controlled, reviewed, and appropriate. Must demonstrate segregation of duties.

**What auditors check:**
- Who can post journal entries?
- Can the same person create AND approve purchase orders? (SoD violation)
- Are access reviews happening quarterly?
- When someone leaves finance, is their SAP access revoked immediately?

**Failure consequence:** Material weakness finding → stock price impact, SEC scrutiny, potential criminal liability for executives.

### HIPAA (Health Insurance Portability and Accountability Act, 1996)

**Applies to:** Healthcare organizations, anyone handling PHI (Protected Health Information)

**What it requires:**
- Minimum necessary access (only access what you need for your job)
- Audit trails of who accessed what patient data
- Regular access reviews
- Immediate revocation when access is no longer needed

**Identity implication:** Must prove that a billing clerk can't access clinical records, that a nurse in cardiology can't access psychiatry records, that a departed employee can't access anything.

**Failure consequence:** Fines up to $1.5M per violation category per year. Breach notification requirements. Reputational devastation.

### GDPR (General Data Protection Regulation, 2018)

**Applies to:** Anyone handling EU citizen data (which is basically everyone)

**What it requires (identity-relevant parts):**
- Data minimization (don't access more than you need)
- Purpose limitation (access only for stated purpose)
- Right to be forgotten (can you prove you've removed access to someone's data?)
- Accountability (prove you're doing all of the above)

**Identity implication:** Must demonstrate that only authorized personnel access personal data, and that access is limited to what's necessary for their role.

**Failure consequence:** Fines up to 4% of global annual revenue or €20M, whichever is higher. (Meta was fined €1.2B in 2023.)

### SOC 2 (Service Organization Control 2)

**Applies to:** Any company providing services to other companies (SaaS, cloud providers — like Saviynt itself)

**What it requires:**
- Trust principles: Security, Availability, Processing Integrity, Confidentiality, Privacy
- Demonstrated controls around access management
- Evidence of regular access reviews
- Logical access controls documented and tested

**Identity implication:** Your customers' auditors will ask you (as a SaaS provider) to prove YOUR access governance is solid. If you're Saviynt, your platform helps customers with THEIR compliance — but you also need to demonstrate your own.

**Failure consequence:** Lose SOC 2 certification → enterprise customers can't buy from you → revenue impact.

### Other Frameworks

| Framework | Sector | Identity Relevance |
|-----------|--------|-------------------|
| PCI-DSS | Payment card data | Access control to cardholder data environment |
| FedRAMP | US Government cloud | Strict identity controls for gov systems |
| NIST 800-53 | US Federal | Comprehensive access control requirements |
| ISO 27001 | Global | Access management as core control domain |
| GLBA | Financial services | Customer data protection |
| CCPA/CPRA | California privacy | Data access governance |

---

## The Five Problems IGA Solves

### Problem 1: Access Accumulation (Privilege Creep)

**What happens without IGA:**
- Person joins as junior analyst → gets access to 5 systems
- Gets promoted to senior analyst → gets access to 3 more systems (but keeps original 5)
- Moves to a different team → gets new team access (but keeps ALL previous access)
- After 5 years: has access to 40+ systems, needs maybe 12

**Why it's dangerous:** Each unnecessary access is an attack surface. If their credentials are compromised, attacker gets everything they accumulated.

**What IGA does:** Detects access that doesn't match current role. Triggers review. Automates removal of unnecessary entitlements during role changes.

### Problem 2: Orphaned Accounts

**What happens without IGA:**
- Employee leaves on Friday
- IT gets notified Monday (maybe)
- AD account disabled Tuesday
- But their AWS IAM user? Still active.
- Their Salesforce account? Still active.
- Their admin access to the legacy billing system? Who even knows about that one.

**The stat:** Average enterprise has 40% more identities in target systems than active employees.

**What IGA does:** Reconciliation — continuously compares "who should have access" (HR source of truth) with "who actually has access" (target systems). Flags orphaned accounts. Automates removal.

### Problem 3: Segregation of Duties (SoD) Violations

**What SoD means:** Certain access combinations are toxic — one person should NEVER hold both:

| Permission A | Permission B | Why Toxic |
|-------------|-------------|-----------|
| Create vendor | Approve payment | Could create fake vendor, pay themselves |
| Write code | Deploy to production | Could deploy malicious code unchecked |
| Create employee | Approve payroll | Could create ghost employee, collect salary |
| Modify price list | Approve orders | Could give unauthorized discounts |

**What happens without IGA:** These violations hide in complexity. Person A has 50 entitlements across 10 systems. Person B has 60 across 12 systems. Manually checking all combinations? At scale, impossible.

**What IGA does:** Maintains SoD policy rules. Checks EVERY access request against violations. Blocks or escalates. Continuously scans existing access for violations that crept in.

### Problem 4: Audit Preparedness

**What happens without IGA:**
- Audit comes quarterly
- Team spends 3-6 WEEKS gathering evidence manually
- Pull reports from 20+ systems
- Compile into spreadsheets
- Hope nothing is missing
- Auditor finds gaps anyway

**What IGA does:** Continuous audit trail. Every access grant, approval, certification, revocation — logged with who, what, when, why. Auditor asks a question → answer in minutes, not weeks.

### Problem 5: Speed vs. Control

**The tension:**
- Business wants: "New hire productive on Day 1"
- Security wants: "No access without proper approval and review"
- Without IGA: You get one or the other. Fast = risky. Controlled = slow.

**What IGA does:** Automation resolves the tension. Birthright access provisioned automatically (fast) based on pre-approved role definitions (controlled). Requests for additional access follow automated workflows (fast enough) with proper approvals logged (controlled).

---

## The Cost of Getting It Wrong

### Financial

| Incident | Cost |
|----------|------|
| Average data breach (2024) | $4.88M (IBM Cost of Data Breach Report) |
| SOX material weakness | Stock price drop 5-10% on disclosure |
| HIPAA violation (single incident) | $100K - $1.5M in fines |
| GDPR violation | Up to 4% global revenue |
| Failed audit remediation | $500K - $2M in emergency consulting |

### Operational

- Audit prep consuming 6-8 weeks of team time per quarter
- New hire waiting 3-5 days for access (lost productivity × headcount × every hire)
- Security incidents from over-provisioned accounts
- Manual access reviews consuming manager time (often rubber-stamped = useless)

### Reputational

- Breach disclosure → customer trust erosion
- Regulatory action → public record
- Failed audit → board-level conversation, potential leadership changes

---

## Why NOW: The Trends Making IGA More Critical

### 1. Cloud Explosion
- On-prem: 10-20 systems to govern
- Cloud-native org: 200+ SaaS apps, multiple cloud providers, thousands of cloud entitlements
- Scale of the problem multiplied 10x in a decade

### 2. Remote/Hybrid Work
- No physical perimeter to fall back on
- Access from anywhere = identity IS the perimeter
- BYOD, contractor workforce, partner access

### 3. Regulatory Acceleration
- New regulations every year (DORA in EU, state privacy laws in US)
- Existing regulations getting stricter enforcement
- Cross-border complexity increasing

### 4. Zero Trust Architecture
- "Never trust, always verify" requires knowing WHO has WHAT access at ALL times
- IGA provides the foundation for Zero Trust access decisions

### 5. AI & Automation
- Attack surface growing faster than security teams
- Manual governance can't scale
- AI-assisted IGA becoming table stakes (more in Ch 11-12)

---

## How Companies Buy IGA (The Sales Motion)

Understanding why companies buy helps you understand what they value:

| Buyer Trigger | What They're Really Saying |
|--------------|---------------------------|
| "We failed an audit" | Emergency. Need to fix NOW. Price insensitive. |
| "Audit is coming in 6 months" | Proactive but urgent. Compliance-first buyer. |
| "Our current IGA tool is end-of-life" | Replacement cycle. Feature comparison shopping. |
| "We're moving to cloud, current tool is on-prem" | Modernization. Architecture matters more than features. |
| "We have no IGA at all" | Greenfield. Usually triggered by growth (IPO-bound, enterprise customers demanding SOC 2) |
| "We need to reduce access-related risk" | Security-first buyer. Harder to quantify ROI. |

**The pattern:** Compliance is the #1 purchase trigger. Security is #2. Efficiency/productivity is a nice-to-have that helps justify budget but rarely drives the initial purchase.

---

> **🔧 Platform Engineering Lens**
>
> IGA exists because of an **observability gap in the access layer.** Organizations couldn't answer basic questions about their access state. Sound familiar?
>
> This is the same pattern as:
> - "Which services are running in production?" → Service catalog
> - "What's the latency of service X?" → Observability platform
> - "Who deployed what, when?" → Deployment tracking
> - **"Who has access to what, and should they?"** → IGA
>
> The platform engineering insight: IGA is an **observability + control plane for identity.** It provides the visibility (who has what) and the actuators (grant/revoke) that allow governance at scale. Without it, you're flying blind on one of your most critical security dimensions.

---

## Self-Test Questions

1. Name three compliance frameworks that drive IGA purchases. What's the common thread?
2. What is "privilege creep" and why can't you solve it with manual processes at scale?
3. Why is "Mover" (role change) often harder than "Joiner" or "Leaver" from an access perspective?
4. What's a Segregation of Duties violation? Give an example of a toxic access combination.
5. If a company has never had IGA, what's the most likely trigger for them to buy it?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **SOX** | Sarbanes-Oxley Act — US law requiring internal controls over financial reporting |
| **HIPAA** | Health Insurance Portability and Accountability Act — US healthcare data protection |
| **GDPR** | General Data Protection Regulation — EU privacy law with global reach |
| **SOC 2** | Audit framework for service organizations proving security controls |
| **SoD** | Segregation of Duties — preventing toxic permission combinations |
| **Privilege Creep** | Gradual accumulation of unnecessary access over time |
| **Orphaned Account** | Active account in a system for a person who no longer needs it |
| **Material Weakness** | Audit finding indicating a significant control deficiency |
| **Access Certification** | Periodic review confirming access is still appropriate |
| **Reconciliation** | Comparing expected access state with actual access state across systems |
| **Birthright Access** | Minimum access automatically granted based on role at hire |
