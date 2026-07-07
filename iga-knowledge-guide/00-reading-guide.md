# Chapter 00: Reading Guide & Learning Path

> *You're an engineer learning a new domain. This isn't a textbook — it's a map.*

---

## Who This Is For

You're a Platform Engineering or SRE leader who:
- Has zero IGA background (and that's fine — this builds from scratch)
- Thinks in systems, APIs, reliability, and platforms
- Is joining (or has joined) Saviynt and needs domain depth
- Wants to speak credibly about identity governance without faking it

---

## How This Guide Is Structured

### Three Parts, One Arc

```
Part I: Foundations        →  "What is this space and why does it exist?"
Part II: Intermediate     →  "How does it actually work in practice?"
Part III: Advanced        →  "Where is it going and how do I lead here?"
```

Each part assumes you've read (or at least skimmed) the previous one. But individual chapters are designed to be self-contained enough for reference use later.

### Reading Modes

**Mode 1: Sequential (Recommended for first pass)**
Read front to back. Takes 4-5 weeks at ~1 chapter per day-and-a-half. Deepest understanding.

**Mode 2: Sprint (Need domain literacy fast)**
- Week 1: Ch 01 → 02 → 03 (core concepts)
- Week 2: Ch 05 → 06 → 10 (Saviynt-specific + platform lens)
- Done. Revisit other chapters as conversations surface topics.

**Mode 3: Reference (After first pass)**
Use the chapter table in README.md. Jump to what you need before a meeting, conversation, or decision.

---

## How Each Chapter Works

Every chapter follows the same structure:

| Section | Purpose |
|---------|---------|
| Opening quote/hook | Anchor the chapter's core idea |
| Core content | The actual knowledge, built incrementally |
| Real-world scenarios | Concrete examples — "at a company like X, this looks like..." |
| Saviynt angle | Where relevant: how this maps to Saviynt specifically |
| SRE/Platform lens | Callout box connecting the topic to your existing mental models |
| Self-test questions | If you can answer these, you've got it |
| Key terms | Quick reference glossary |

### SRE/Platform Lens Boxes

These look like:

> **🔧 Platform Engineering Lens**
>
> How this topic connects to reliability, observability, developer experience, or platform thinking. Your bridge from "new domain" to "I already know something analogous."

They appear throughout — not just in the dedicated SRE chapters (10, 15). The goal: you never feel like IGA is some alien domain. It's systems. You know systems.

---

## What You DON'T Need Before Starting

- ❌ Security certifications
- ❌ Prior identity/access management experience
- ❌ Knowledge of compliance frameworks
- ❌ Saviynt product experience
- ❌ Enterprise IT background

## What Helps (But Isn't Required)

- ✅ General understanding of cloud infrastructure (AWS/Azure/GCP)
- ✅ Familiarity with APIs, microservices, distributed systems
- ✅ Knowing what SLOs, SLIs, and error budgets are
- ✅ Having managed or built a platform team

---

## Chapter-by-Chapter Overview

### Part I: Foundations (Beginner)

| # | Chapter | What You'll Learn |
|---|---------|-------------------|
| 01 | **Identity 101** | The entire identity ecosystem mapped: digital identity, authentication vs authorization, IAM vs IGA vs PAM vs CIEM. Where IGA sits in the security stack. Physical-world analogies. Why "just use Active Directory" isn't enough. The identity lifecycle (joiner/mover/leaver) introduced with concrete scenarios. |
| 02 | **Why IGA Exists** | The origin story: corporate fraud → SOX → an industry was born. Every major compliance driver (SOX, HIPAA, GDPR, SOC 2, PCI-DSS) explained with what auditors actually check. The five problems IGA solves: privilege creep, orphaned accounts, SoD violations, audit preparedness, speed-vs-control tension. The cost of failure (financial, operational, reputational). Why NOW — trends making IGA more critical. |
| 03 | **Core IGA Capabilities** | The five pillars: identity lifecycle management, access request & approval, access certification, role management, and segregation of duties. Each explained with workflows, diagrams, and end-to-end scenarios. How the provisioning engine works underneath. Reconciliation explained (IGA's "eventual consistency" problem). |
| 04 | **The IGA Market Landscape** | Tier 1-3 vendors profiled (SailPoint, Saviynt, Microsoft, CyberArk, Omada, Veza, Opal, ConductorOne). Analyst positioning (Gartner MQ, KuppingerCole). The generational shift from on-prem to cloud-native. Market dynamics: convergence vs best-of-breed, cloud governance as wedge, AI as differentiator, developer experience as emerging battlefield. How enterprises evaluate and switch IGA vendors. |

### Part II: Intermediate

| # | Chapter | What You'll Learn |
|---|---------|-------------------|
| 05 | **Saviynt's Architecture & Differentiators** | Enterprise Identity Cloud (EIC) deep-dive. The four pillars: IGA, CPAM, AAG, DSAG — what each does and why they're in one platform. What "cloud-native" actually means architecturally (multi-tenant, microservices, continuous delivery). Multi-tenancy model: what's shared vs isolated. Key technical components (identity warehouse, connector framework, policy engine, workflow engine, risk engine). Competitive positioning vs SailPoint, CyberArk, Microsoft. FedRAMP as a moat. |
| 06 | **Connectors & Integrations** | How IGA talks to 200+ target systems. Five integration patterns (direct API, agent/gateway, SCIM, ticket-based, database direct). The connector ecosystem by category (directories, cloud, ERP, SaaS, DevOps, mainframe). Connector operations: import (full/incremental), provisioning, reconciliation. Six failure modes and their business impact. Saviynt's REST-based connector framework. HRIS, ITSM, and SIEM integration patterns. The long-tail problem. |
| 07 | **Access Certifications & Reviews** | Campaign lifecycle end-to-end: define → launch → review → execute → report. Four certification types (manager, application, entitlement, micro). The rubber-stamp problem — why 90% of decisions are "approve" and five solutions (risk-based, AI recommendations, plain language, contextual info, micro-certs). Campaign orchestration at scale (50K employees, 5K reviewers). Metrics that distinguish real governance from checkbox compliance. Anti-patterns. |
| 08 | **Role Engineering & Mining** | Why roles exist (combinatorial explosion without them). Four role types (business, technical, organizational, composite). Top-down design vs bottom-up mining — algorithms, trade-offs, hybrid approach. The role explosion problem: causes, symptoms, prevention. Birthright access design principles. Entitlement analytics: peer group analysis, usage analytics, outlier detection. Role lifecycle management. |
| 09 | **Cloud Governance (CPAM + CIEM)** | Why cloud broke traditional IGA (permission explosion, machine identities, ephemeral compute). CIEM deep-dive: multi-cloud visibility, effective permission analysis, overprivileged detection, right-sizing. CPAM deep-dive: Just-in-Time access, zero standing privileges, session recording, break-glass. Five cloud governance challenges: shadow cloud, IaC permissions, Kubernetes identity, multi-cloud correlation, ephemeral identities. Maturity model (blind → optimized). |
| 10 | **SRE/Platform Engineering for IGA — Foundations** | IGA as a platform product (two-layer customer model). Why reliability bar is higher than typical SaaS. SLIs and SLOs specific to identity (provisioning latency, de-provisioning speed, reconciliation freshness, connector health). Error budgets in IGA context. Four observability pillars applied (metrics, logs, traces, alerts). IGA-specific incident types. Identity incident vs security incident distinction. Capacity planning for burst workloads. Deployment risks unique to IGA. |

### Part III: Advanced

| # | Chapter | What You'll Learn |
|---|---------|-------------------|
| 11 | **GenAI Revolution in IGA — Current State** | What IGA used ML for BEFORE GenAI (anomaly detection, risk scoring, role mining). What GenAI adds (the step change: explanation, accessibility, natural language). Six capabilities shipping TODAY: natural language access requests, intelligent certification recommendations, conversational admin copilot, natural language policy authoring, auto-classification of requests, anomaly explanation. What works well vs what's still hype. Implementation challenges: training data quality, hallucination risk, explainability for auditors, bias. |
| 12 | **GenAI + IGA — Future Scope** | Seven future capabilities with detailed scenarios: autonomous access governance, behavioral LLM threat detection, self-healing identity posture, conversational access requests, policy-as-prompt, synthetic identity testing, agentic IGA. The trajectory from "AI assists" → "AI acts, humans supervise" → "AI governs, humans audit." Risks: over-trust, adversarial manipulation, regulatory lag, opacity, monoculture. New infrastructure platform teams must build (model serving, vector stores, guardrails, evaluation pipelines). |
| 13 | **Zero Trust & IGA Convergence** | Zero Trust principles and how IGA serves each one. IGA's role as the "knowledge layer" for Zero Trust. Shift from periodic to continuous governance. Adaptive access: context-aware decisions (not binary allow/deny). Identity-first security architecture (identity as primary control plane, not network). ITDR (Identity Threat Detection & Response) and how it complements IGA. Practical maturity roadmap from basic hygiene to autonomous. |
| 14 | **IGA for Regulated Industries** | Financial services: SOX deep-dive, extreme SoD granularity (SAP transaction-level), service account governance, third-party vendor access. Healthcare: HIPAA minimum necessary, break-glass access pattern, role complexity, patient record segregation. Government: security clearances, FedRAMP requirements, cross-domain (classified) access, personnel category separation. Cross-industry patterns: evidence-first design, tiered governance, regulatory mapping, continuous monitoring. |
| 15 | **SRE/Platform Engineering for IGA — Advanced** | Identity-as-Code (declarative access via CI/CD with examples). Multi-tenant platform operations (isolation tiers, noisy neighbor patterns, fair-share scheduling). Capacity planning for certification campaigns (burst modeling, pre-campaign ops checklist). Chaos engineering for identity (experiments + why extra care needed). Developer experience golden paths for access (CLI, instant patterns). Advanced SLOs (composite, per-tenant). Incident playbooks (mass de-provisioning failure, wrong access granted). Platform engineering maturity model for IGA. |
| 16 | **The Business of IGA** | How IGA is sold (timeline, deal sizes, pricing models). Buyer personas and what each values (CISO, VP Identity, GRC Director, CTO). Competitive dynamics (Saviynt vs SailPoint, vs Microsoft — dimension by dimension). Revenue models and growth metrics (ARR, NDR, churn). TCO arguments (cloud-native vs on-prem). ROI quantification. Market trends: consolidation, compliance-as-a-service, identity security category expansion, developer-led adoption, AI as differentiator. How engineering decisions map to business outcomes. |

---

## Vocabulary Survival Kit

Before Chapter 1, here are 10 terms you'll see everywhere. Rough definitions — each gets proper treatment in later chapters.

| Term | Quick Definition |
|------|-----------------|
| **IGA** | Identity Governance & Administration — managing who has access to what, and proving it's correct |
| **Entitlement** | A specific permission or access right (e.g., "can read S3 bucket X") |
| **Provisioning** | Actually creating/granting access in a target system |
| **De-provisioning** | Removing access — harder than it sounds at scale |
| **Access Certification** | Periodic review: "Does this person still need this access?" |
| **Segregation of Duties (SoD)** | Preventing toxic combinations (e.g., same person can't create AND approve payments) |
| **Connector** | Integration between IGA and a target system (AD, SAP, AWS, etc.) |
| **Joiner/Mover/Leaver** | The lifecycle: employee joins, changes role, leaves. Each triggers access changes |
| **Role** | Bundle of entitlements assigned together (e.g., "Finance Analyst" role grants X, Y, Z) |
| **PAM** | Privileged Access Management — managing admin/root access specifically |

---

## Suggested Cadence

| Time Available | Approach |
|---------------|----------|
| 30 min/day | One chapter section per day. Complete guide in ~6 weeks |
| 1 hr/day | One chapter per day. Complete in ~2.5 weeks |
| Intensive (onboarding week) | 2-3 chapters per day. Foundations in 2 days, full guide in a week |

---

## How to Know You're "Getting It"

After each Part, you should be able to:

**After Part I:**
- Explain IGA to a non-technical executive in 2 minutes
- Describe why compliance drives IGA purchases
- Name the top 3-4 vendors and what differentiates them

**After Part II:**
- Describe Saviynt's architecture at a whiteboard
- Explain what a connector does and why it breaks
- Articulate what SRE means for an identity platform
- Understand what certification campaigns are and why they're painful

**After Part III:**
- Discuss GenAI's impact on IGA (separating real from hype)
- Articulate a platform engineering vision for IGA
- Speak to business/commercial context around identity governance
- Understand where the industry is heading in 3-5 years

---

## One More Thing

This guide is written with a specific bias: **IGA is infrastructure.** It's a platform. It has reliability concerns, scaling challenges, developer experience problems, and operational overhead. Many people in this industry think about it as "GRC tooling" (governance, risk, compliance). That's valid. But your lens — platform engineering — is increasingly the RIGHT lens for modern IGA. Cloud-native, API-first, developer-friendly governance is where the market is heading. You're not late to this domain. You're arriving at exactly the right time with exactly the right background.
