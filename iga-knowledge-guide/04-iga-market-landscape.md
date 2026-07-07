# Chapter 04: The IGA Market Landscape

> *"The IGA market is in a generational shift — from on-prem monoliths to cloud-native platforms. Companies that made the leap early are winning. Those that didn't are scrambling."*

---

## Market Overview

IGA is a ~$8-10B market (2024) growing at ~15% CAGR. Driven by:
- Regulatory pressure (never decreasing)
- Cloud migration (creating new governance gaps)
- Remote work (dissolving perimeter-based security)
- Identity-centric attacks (80%+ of breaches involve compromised credentials)

---

## The Major Players

### Tier 1: Market Leaders

#### SailPoint

**Founded:** 2005, Austin TX. **Public:** NYSE (SAIL) 2017, taken private by Thoma Bravo 2022 (~$6.9B), re-IPO'd 2024.

**Architecture:** Originally on-prem (IdentityIQ). Built cloud product (IdentityNow, now "Identity Security Cloud") as separate platform.

**Strengths:**
- Largest installed base in IGA
- Deep enterprise relationships
- Strong partner ecosystem
- Identity Security Platform (broader than just IGA)

**Weaknesses:**
- Two-product strategy (IdentityIQ vs Identity Security Cloud) creates migration pain for existing customers
- Cloud platform built later, playing catch-up on cloud-native architecture
- Heavy professional services dependency

**Positioning:** Incumbent market leader. Strong with Fortune 500. "Identity security" framing (broader than governance alone).

#### Saviynt

**Founded:** 2010, Los Angeles. **Private** (growth equity from investors including AB Vista Equity).

**Architecture:** Cloud-native from ground up. Single converged platform — EIC (Enterprise Identity Cloud).

**Strengths:**
- True cloud-native multi-tenant architecture (not lift-and-shift)
- Converged platform: IGA + CPAM + Application GRC + Data Governance in one
- Strong in cloud governance (AWS, Azure, GCP native understanding)
- Faster deployment timeline vs. legacy vendors
- FedRAMP authorized (government market access)

**Weaknesses:**
- Smaller market share than SailPoint (growing rapidly but from smaller base)
- Less deep in some legacy on-prem connector ecosystems (SAP, mainframe)
- Brand recognition still building in some geographies

**Positioning:** Cloud-native challenger. Convergence play (one platform vs. many tools). "Born in the cloud" narrative.

#### Microsoft (Entra ID Governance)

**Launched:** 2022 (rebranding Azure AD + adding governance features)

**Architecture:** Native Azure. Tightly integrated with Microsoft ecosystem.

**Strengths:**
- Already in every Microsoft shop (zero deployment for basic features)
- Deep Azure/M365 integration
- Bundling economics (part of E5 license)
- Massive R&D budget

**Weaknesses:**
- IGA capabilities still maturing vs. dedicated vendors
- Weak for non-Microsoft ecosystems (SAP, AWS, legacy apps)
- Not a dedicated IGA focus — it's a feature, not a platform
- Limited advanced governance (SoD, role mining less mature)

**Positioning:** "Good enough" for Microsoft-only shops. Threat to dedicated IGA vendors via bundling, but not yet a replacement for complex environments.

---

### Tier 2: Established Players

| Vendor | Key Facts | Differentiation |
|--------|-----------|-----------------|
| **One Identity** (Quest/Clearlake) | On-prem legacy (Identity Manager). Trying cloud pivot. | Strong in AD-heavy environments |
| **Omada** | Danish, European focus. Cloud-native. | Strong in mid-market European companies. GDPR-first design |
| **CyberArk** (acquired Zilla Security 2024) | PAM leader entering IGA space | PAM+IGA convergence from PAM side |
| **IBM** (Security Verify Governance) | Legacy player. Declining market presence | Still in large IBM shops, but losing deals |
| **Oracle** (Identity Governance) | Legacy on-prem. Part of Oracle stack | Captive Oracle ERP customer base |
| **RSA** (Governance & Lifecycle) | Legacy, declining. Formerly EMC/Dell | Minimal new customer acquisition |

---

### Tier 3: Emerging / Niche

| Vendor | Focus |
|--------|-------|
| **Zilla Security** (now CyberArk) | AI-first IGA for SaaS applications |
| **Veza** | Authorization graph platform — next-gen approach to access visibility |
| **ConductorOne** | Developer-friendly access management, PLG motion |
| **Opal** | Developer-centric access platform, infrastructure-as-code approach |
| **Cerby** | Unmanaged/shadow SaaS governance |
| **Authomize** (now Delinea) | Identity threat detection |

---

## The Analyst View

### Gartner Magic Quadrant (IGA)

Gartner evaluates IGA vendors on:
- Completeness of Vision (x-axis)
- Ability to Execute (y-axis)

**2024 positioning (approximate):**
```
                    High Ability to Execute
                           │
          Leaders          │         Leaders
       (SailPoint)         │        (Saviynt)
                           │
    ───────────────────────┼───────────────────────
                           │
       Niche Players       │       Visionaries
       (IBM, One Identity) │       (Omada, Veza)
                           │
                    Low Ability to Execute

        ← Less Complete Vision    More Complete Vision →
```

### KuppingerCole Leadership Compass

European analyst firm. Rates on: Product, Innovation, Market presence.

- Saviynt: "Overall Leader" designation (strong across all axes)
- SailPoint: Strong on market presence, product
- Microsoft: Rising fast on market presence (bundling advantage)

---

## The Generational Shift: On-Prem → Cloud-Native

### Why This Matters

The IGA market is mid-transition. Legacy vendors (SailPoint IdentityIQ, Oracle, IBM) built their platforms in the 2005-2015 era. On-premises. Java monoliths. 12-18 month deployments.

Cloud-native platforms (Saviynt EIC, SailPoint Identity Security Cloud) are architecturally different:

| Dimension | Legacy On-Prem | Cloud-Native |
|-----------|---------------|--------------|
| Deployment | Customer data center, 12-18 months | SaaS, weeks to months |
| Updates | Annual major versions, painful upgrade | Continuous delivery, always current |
| Architecture | Monolith, single-tenant | Microservices, multi-tenant |
| Scaling | Hardware procurement | Elastic cloud scaling |
| Cost model | CapEx (license + infrastructure) | OpEx (subscription) |
| Integration | Agent-based, on-prem connectors | API-first, cloud-to-cloud |
| AI/ML | Difficult to add (data siloed) | Natural fit (centralized data, compute) |
| Time-to-value | 12-24 months | 3-6 months |

### The Migration Challenge

~60% of enterprise IGA deployments are still on-prem (2024). Migration to cloud is happening but:
- Enterprises move slowly (risk aversion, existing investment)
- Customizations on legacy platforms don't translate directly
- Data migration is complex (years of history, policies, roles)
- This creates opportunity for cloud-native vendors to win competitive replacements

---

## Market Dynamics: What Drives Competition

### 1. Platform Convergence vs. Best-of-Breed

**Convergence thesis (Saviynt's bet):**
- Customers want ONE platform for IGA + PAM + Cloud Governance + Data Governance
- Reduces integration complexity, unified policy, single pane of glass
- "Why buy 4 tools when 1 does all four?"

**Best-of-breed thesis (historical model):**
- CyberArk for PAM
- SailPoint for IGA
- Ermetic for CIEM
- Each does its thing best

**Market verdict:** Convergence is winning. Customers tired of integration tax between point solutions. But best-of-breed still wins for organizations with highly specific needs in one area.

### 2. Cloud Governance as Wedge

Cloud created new identity problems that legacy IGA couldn't handle:
- Thousands of cloud entitlements (AWS alone has 10,000+ unique permissions)
- Ephemeral compute (serverless, containers — identity lifecycle is minutes, not months)
- Multi-cloud sprawl (AWS + Azure + GCP = 3× the complexity)

Saviynt and others used cloud governance (CPAM/CIEM) as a wedge to enter accounts dominated by legacy IGA. "Your SailPoint can't govern your AWS environment? We can."

### 3. AI as Differentiator

Every IGA vendor now claims AI capabilities. Reality varies:
- **Table stakes:** Analytics dashboards, basic anomaly flags
- **Meaningful:** Risk-based certifications, intelligent recommendations, auto-classification
- **Leading edge:** Natural language policy, autonomous governance decisions, behavioral analysis

More in Chapters 11-12.

### 4. Developer Experience (DX) as Emerging Battlefield

New entrants (Opal, ConductorOne, Veza) are attacking from a DX angle:
- "IGA is built for compliance teams. What about developers?"
- Infrastructure-as-code for access policies
- API-first, GitOps-friendly
- Self-service access without portal overhead

This matters because engineering teams are increasingly a key persona, not just auditors.

---

## How Enterprise Customers Evaluate IGA

When a company is buying IGA, here's what the evaluation typically covers:

| Criterion | Weight | What They Check |
|-----------|--------|-----------------|
| Core IGA capabilities | High | Lifecycle, certs, request, roles, SoD |
| Connector coverage | High | "Do you connect to the 50 systems we have?" |
| Cloud governance | Growing | AWS/Azure/GCP native capabilities |
| Time to deploy | Medium-High | Months, not years |
| Total cost of ownership | High | License + implementation + ongoing |
| Compliance coverage | High | SOX, HIPAA, specific frameworks |
| Architecture (SaaS vs on-prem) | Growing | Multi-tenant cloud preferred |
| AI/ML capabilities | Growing | Beyond buzzwords — what's real? |
| Vendor stability | Medium | Funding, leadership, roadmap credibility |
| Professional services | Medium | Quality of implementation partners |
| UI/UX | Growing | End-user experience for requests, manager experience for certs |

---

## Competitive Displacement Patterns

How vendor switches typically happen:

| From | To | Why |
|------|-----|-----|
| IBM/Oracle IGA | SailPoint or Saviynt | End-of-life / end-of-support. Legacy pain. |
| SailPoint IdentityIQ (on-prem) | Saviynt EIC | Cloud migration. Faster time-to-value. Convergence. |
| No IGA (manual) | Any vendor | Audit failure or IPO/growth triggering compliance need |
| Multiple point tools | Saviynt (converged) | Consolidation play — one vendor instead of 4 |
| Microsoft Entra (basic) | Dedicated IGA | Outgrowing basic capabilities, non-Microsoft ecosystem needs |

---

> **🔧 Platform Engineering Lens**
>
> The market dynamics here mirror platform vs. toolchain debates in engineering:
> - **Convergence vs best-of-breed** = Kubernetes (converged platform) vs. hand-picked tools per concern
> - **Cloud-native vs lift-and-shift** = The same argument you've made about infrastructure platforms
> - **Developer experience** = The same fight you've had about making infrastructure self-service
>
> As a platform leader at Saviynt, you're positioned at the intersection of these trends:
> - Building the reliable infrastructure that powers convergence
> - Ensuring the cloud-native architecture actually delivers on its promises (multi-tenancy, elastic scaling, continuous delivery)
> - Potentially championing developer experience as a differentiator
>
> Understanding the competitive landscape helps you prioritize: "If we're losing deals because connector X is unreliable, that's a platform reliability problem with direct revenue impact."

---

## Self-Test Questions

1. What are the top 3 IGA vendors by market presence? What differentiates each?
2. Why is "cloud-native" a meaningful architectural distinction, not just marketing? Name 3 concrete advantages.
3. What is the "convergence" thesis in IGA? Which vendors are betting on it?
4. Why might a company switch from SailPoint IdentityIQ to Saviynt? What's the pitch?
5. How does Microsoft's entry (Entra ID Governance) threaten dedicated IGA vendors? Where does it fall short?
6. What do emerging players like Veza and Opal represent? What market need are they addressing?

---

## Key Terms

| Term | Definition |
|------|-----------|
| **EIC** | Enterprise Identity Cloud — Saviynt's platform |
| **IdentityIQ** | SailPoint's on-premises IGA product |
| **Identity Security Cloud** | SailPoint's SaaS IGA product |
| **Entra ID Governance** | Microsoft's cloud IGA offering (part of Entra suite) |
| **Magic Quadrant** | Gartner's vendor evaluation framework (Leaders, Visionaries, Niche, Challengers) |
| **CPAM** | Cloud Privileged Access Management — PAM for cloud environments |
| **Convergence** | Strategy of combining IGA + PAM + CIEM + more into one platform |
| **Best-of-Breed** | Strategy of picking the best specialized tool for each function |
| **TCO** | Total Cost of Ownership — license + implementation + maintenance + operations |
| **FedRAMP** | Federal Risk and Authorization Management Program — US gov cloud certification |
| **Time-to-Value** | Duration from purchase to productive use |
