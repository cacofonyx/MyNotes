# Chapter 14: IGA for Regulated Industries

> *"Every industry needs IGA. But in financial services, healthcare, and government, the consequences of getting it wrong aren't just 'we got fined.' They're 'patients got harmed,' 'fraud went undetected,' or 'national security was compromised.'"*

---

## Why Industry-Specific IGA Matters

Generic IGA capabilities (lifecycle, certs, roles, SoD) exist in every platform. But regulated industries have:

| Dimension | Generic | Regulated Industry |
|-----------|---------|-------------------|
| Certification frequency | "Best practice: quarterly" | "SOX requires quarterly, MINIMUM" |
| Revocation speed | "Same day is good" | "HIPAA: immediate. Banking: within hours." |
| SoD rules | "Customize for your org" | "Industry-standard rule sets (e.g., SAP SoD for finance)" |
| Evidence requirements | "Keep logs" | "Produce specific evidence artifacts in prescribed formats" |
| Third-party access | "Manage it" | "Must be segregated, time-bound, monitored separately" |
| Audit frequency | "Annual" | "Continuous regulatory examination" |

---

## Financial Services

### Regulatory Landscape

| Regulation | Geography | Key Identity Requirements |
|-----------|-----------|--------------------------|
| SOX Section 404 | US (public companies) | Internal controls over financial reporting |
| GLBA | US | Customer data protection |
| PCI-DSS | Global (payment card) | Access control for cardholder data |
| DORA | EU (2025+) | Digital operational resilience |
| MAS-TRM | Singapore | Technology risk management |
| FCA/PRA | UK | Operational resilience |
| Basel III OpRisk | Global (banks) | Operational risk capital (identity incidents = operational risk) |

### What's Unique About Financial Services IGA

#### 1. SOX Compliance Is the Primary Driver

Every public financial institution runs quarterly SOX certification campaigns. Non-negotiable.

**What auditors check:**
- Segregation of duties in financial systems (SAP, Oracle EBS)
- Access reviews completed within required timeframes
- Terminated employee access revoked promptly
- Service account governance (shared accounts = audit finding)
- Elevated access to financial reporting systems

#### 2. Segregation of Duties at Extreme Granularity

Financial SoD rules are deep and industry-specific:

```
SAP SoD RULESET (PARTIAL — a real implementation has 300+ rules):

Accounts Payable:
├── Create Vendor (FK01) × Approve Payment (F-53) = CRITICAL
├── Post Invoice (FB60) × Release Payment (F110) = HIGH
├── Change Vendor Bank (FK02) × Approve Payment = CRITICAL
└── Goods Receipt (MIGO) × Invoice Verification (MIRO) = HIGH

General Ledger:
├── Post Journal Entry (FB01) × Approve Journal (FBRA) = HIGH
├── Park Document (FV50) × Post Parked Document (FBV0) = MEDIUM
└── Period Open/Close (OB52) × Post Journal = HIGH

Treasury:
├── Create Deal (FTR_CREATE) × Confirm Deal = CRITICAL
└── Value Date Change × Payment Release = HIGH
```

Banks and financial institutions may have 500+ SoD rules, many mandated by regulators.

#### 3. Service Account Governance

Financial regulators hate shared/service accounts because they break accountability:
- "Who ran that transaction?" "The service account." "WHO ran it?" "...we don't know."
- Regulators require: individual accountability for every financial transaction
- IGA must: track service account ownership, rotate credentials, ensure human behind every shared account

#### 4. Third-Party/Vendor Access

Banks work with thousands of vendors who access systems:
- Must be segregated from employee access
- Must be time-bound (contract end date = access end date)
- Must be monitored differently
- Must be certified more frequently (quarterly or even monthly for high-risk)

---

## Healthcare

### Regulatory Landscape

| Regulation | Geography | Key Identity Requirements |
|-----------|-----------|--------------------------|
| HIPAA | US | PHI access controls, minimum necessary |
| HITECH | US | Breach notification, enhanced enforcement |
| 21st Century Cures | US | Interoperability, information blocking |
| GDPR | EU | Patient data as personal data |
| PIPEDA | Canada | Health information protection |
| NHS DSPT | UK | Data security standards for health |

### What's Unique About Healthcare IGA

#### 1. Minimum Necessary Access (The HIPAA Mandate)

HIPAA requires: Every healthcare worker should have access ONLY to the patient information needed for their job. No more.

```
MINIMUM NECESSARY IN PRACTICE:

Cardiologist:
✅ Access to cardiology patient records
✅ Access to related test results
❌ Access to psychiatric records
❌ Access to records of patients not under their care

Billing Clerk:
✅ Access to billing information
✅ Access to procedure codes
❌ Access to clinical notes
❌ Access to mental health records

Emergency Physician:
✅ Access to ALL records (emergency override = "break glass")
📝 But every access is logged and must be justified post-hoc
```

#### 2. Break-Glass Access

Healthcare has a unique pattern: In emergencies, a clinician might NEED access they don't normally have (patient arrives unconscious, their regular doctor isn't available).

```
BREAK-GLASS FLOW:

Normal: Doctor can only access their own patients' records

Emergency:
1. Doctor invokes "break glass" (emergency access override)
2. IGA GRANTS immediate access to patient record
3. Doctor provides care
4. AFTER THE FACT: Audit triggers
   - Why was break-glass invoked?
   - Was the access appropriate?
   - Was there a legitimate emergency?
5. If inappropriate → privacy violation → consequences

IGA's role: Enable break-glass instantly BUT ensure every 
            invocation is audited, justified, and reviewed.
```

#### 3. Role Complexity

Healthcare roles are uniquely complex:
- Same person might be: Doctor (clinical access) + Researcher (research data access) + Administrator (management access) + Teacher (student record access)
- Temporary privileges: On-call rotation, visiting physician, covering colleague
- Location-based: Access changes based on which department/floor/facility

#### 4. Patient Consent and Record Segregation

Some records have extra protection:
- Mental health records (restricted even from other clinicians)
- Substance abuse treatment (42 CFR Part 2 — federal protection)
- HIV/STI records (state-specific laws)
- VIP/celebrity patients (media protection)

IGA must enforce these WITHIN the EHR system, not just at the system access level.

---

## Government / Public Sector

### Regulatory Landscape

| Framework | Geography | Key Identity Requirements |
|----------|-----------|--------------------------|
| FedRAMP | US Federal | Cloud service security (IGA vendor must be certified) |
| NIST 800-53 | US Federal | Comprehensive security control catalog |
| FISMA | US Federal | Federal information security |
| CMMC | US DoD supply chain | Cybersecurity maturity |
| IL2-IL6 | US DoD | Impact levels for data classification |
| Protective Marking | UK (Official, Secret, Top Secret) | Classification-based access |
| Security clearances | Most countries | Personnel security = access eligibility |

### What's Unique About Government IGA

#### 1. Security Clearances as Access Prerequisite

Government access isn't just role-based. It's clearance-based:

```
ACCESS DECISION MATRIX:

To access a system, you need:
1. Appropriate security clearance (Secret, Top Secret, etc.)
   AND
2. Need-to-know for that specific information
   AND
3. Formal access approval for that specific system
   AND
4. Current training certifications (annual cybersecurity training)
   AND
5. Citizenship requirement (some systems US-citizen-only)

IGA must enforce ALL of these as AND conditions, not just role-based access.
```

#### 2. FedRAMP Requirements for IGA Vendors

If you're Saviynt selling to US government:
- Platform MUST be FedRAMP authorized
- Data must reside in authorized regions
- Specific security controls must be implemented and audited
- Continuous monitoring (not just point-in-time assessment)
- Incident reporting to government within specific timeframes

FedRAMP authorization takes 1-2+ years and significant investment. Once achieved, it's a major competitive moat.

#### 3. Cross-Domain Access (Classified Environments)

Government often has multiple classification levels:
- Unclassified systems
- Confidential systems
- Secret systems
- Top Secret systems
- Compartmented (TS/SCI) systems

IGA must prevent "spillage" (classified data or access leaking to lower classification):
- A person with Secret clearance cannot access Top Secret system
- A system at one level cannot exchange identity data with a higher level
- Cross-domain access requires specific approvals and controls

#### 4. Separation of Personnel Categories

| Category | Access Rules |
|----------|-------------|
| Government employees | Full access to government systems per clearance |
| Contractors (cleared) | Limited to contract scope, must be separately governed |
| Contractors (uncleared) | Unclassified systems only, escorted access to facilities |
| Foreign nationals | Severely restricted, special handling |
| Partners (allied nations) | Governed by international agreements, compartmented |

---

## Cross-Industry Patterns

Despite industry differences, some patterns are universal in regulated environments:

### Pattern 1: Evidence-First Design

```
Every governance decision must produce EVIDENCE:

WHO made the decision?
WHAT was decided? (certify/revoke/grant/deny)
WHEN was it decided?
WHY? (justification, business case)
WHAT HAPPENED? (action executed, system affected)
WAS IT VERIFIED? (reconciliation confirming actual state matches decision)
```

### Pattern 2: Tiered Governance

Not all access is equal. Regulate proportionally:

| Tier | Access Type | Governance Level |
|------|------------|-----------------|
| **Tier 1** (Critical) | Admin access, financial systems, PII/PHI | Quarterly cert, multi-approval, session monitoring |
| **Tier 2** (Standard) | Business applications, team tools | Semi-annual cert, manager approval |
| **Tier 3** (Low Risk) | Read-only, public info, basic tools | Annual cert, auto-approve with policy |

### Pattern 3: Regulatory Mapping

IGA must map controls to specific regulatory requirements:

```
Saviynt Control: "Quarterly access certification"
Maps to:
├── SOX 404: Internal control testing
├── HIPAA: Access review requirement
├── PCI-DSS 7.1: Access control procedures
├── NIST 800-53 AC-2: Account management
└── ISO 27001 A.9.2.5: Review of user access rights

One control → multiple frameworks satisfied.
One IGA campaign → multiple audit requirements met.
```

### Pattern 4: Continuous Monitoring vs. Point-in-Time

Regulators moving from annual audits to continuous oversight:
- Banking: Real-time transaction monitoring
- Healthcare: Continuous privacy monitoring
- Government: Continuous authorization (vs. 3-year reinvestigation cycles)

IGA must support CONTINUOUS evidence generation, not just quarterly snapshots.

---

## Compliance Automation

### What Saviynt (and similar) Provides

| Compliance Need | Platform Capability |
|----------------|---------------------|
| "Show all SOX controls" | Pre-built SOX control mapping, evidence reports |
| "Run quarterly certification" | Campaign orchestration, deadline enforcement |
| "Prove SoD enforcement" | SoD rule library, violation reports, exception tracking |
| "Show terminated employee access revocation time" | De-provisioning SLA reporting |
| "Map access to regulations" | Multi-framework compliance dashboards |
| "Demonstrate least privilege" | Right-sizing analytics, unused access reports |
| "Show audit trail for any access decision" | Full event log with search/export |

### Pre-Built Compliance Content

Vendors like Saviynt provide out-of-box compliance content:
- SOX SoD rule packs (300+ rules for SAP, Oracle)
- HIPAA control mappings
- PCI-DSS evidence templates
- FedRAMP control evidence collection
- Industry-specific report templates

This is a differentiator: customers don't have to BUILD their compliance program from scratch.

---

> **🔧 Platform Engineering Lens**
>
> For a platform team at an IGA company serving regulated industries:
>
> **Your infrastructure has compliance implications:**
> - Where data resides matters (FedRAMP, GDPR data residency)
> - How long logs are retained matters (7+ years for SOX)
> - How encryption is implemented matters (FIPS 140-2 for government)
> - How deployments are tracked matters (change management audits)
>
> **What this means practically:**
> - Your deployment pipeline IS a compliance control (audited for change management)
> - Your log retention IS a compliance obligation (not just operational)
> - Your disaster recovery IS a regulatory requirement (not just business continuity)
> - Your incident response IS a compliance activity (with reporting obligations)
>
> **Multi-region challenges:**
> - EU customer data must stay in EU (GDPR)
> - US government data must stay in US (FedRAMP)
> - Some customers need data isolation beyond multi-tenancy (dedicated tenancy)
> - Your platform architecture needs to support all of these deployment models
>
> The platform team isn't just building reliable infrastructure. You're building **auditable, compliant, evidence-generating** infrastructure. Every operational decision you make has downstream compliance implications.

---

## Self-Test Questions

1. Why does financial services need different SoD rules than generic IGA? Give an example.
2. What is "break-glass" access in healthcare and why can't you block it?
3. How does FedRAMP authorization function as a competitive moat for IGA vendors?
4. What's the difference between role-based access (enterprise) and clearance-based access (government)?
5. What does "continuous monitoring" mean for compliance, and how does it differ from annual audits?
6. How does your platform engineering work change when infrastructure decisions have compliance implications?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **SOX 404** | Section requiring internal controls over financial reporting |
| **HIPAA** | US healthcare privacy law governing PHI access |
| **FedRAMP** | US government cloud security authorization |
| **PCI-DSS** | Payment card data security standard |
| **DORA** | EU Digital Operational Resilience Act (financial services) |
| **Break-Glass** | Emergency access override in healthcare |
| **Minimum Necessary** | HIPAA principle: access only what your job requires |
| **SoD Rule Pack** | Pre-built set of segregation of duties rules for a specific system |
| **Security Clearance** | Government personnel vetting determining access eligibility |
| **Impact Level (IL)** | DoD data sensitivity classification determining hosting requirements |
| **Continuous Authorization** | Ongoing security assessment vs. point-in-time |
| **Data Residency** | Requirement that data remains in specific geographic locations |
| **FIPS 140-2** | US government standard for cryptographic modules |
