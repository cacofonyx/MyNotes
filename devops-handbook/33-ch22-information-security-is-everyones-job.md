# Chapter 22: Information Security Is Everyone's Job Every Day

> **Part VI -- Integrating Information Security, Change Management, and Compliance**

This chapter is the cornerstone of Part VI and lays out the philosophy and practices for integrating information security into every stage of the DevOps value stream. Rather than treating Infosec as a gatekeeping silo that only appears at the end of a project, the chapter systematically describes how to embed security into iteration demos, defect tracking, shared source code repositories, the deployment pipeline, application and environment testing, the software supply chain, and production telemetry. It draws on case studies from Twitter, Etsy, the US Federal Government (18F), and Fannie Mae to show how organizations have made this shift -- and how breathtaking the results can be when security becomes everyone's daily work rather than a compliance checkbox.

---

## Table of Contents

- [Integrate Security into Development Iteration Demonstrations](#integrate-security-into-development-iteration-demonstrations)
- [Integrate Security into Defect Tracking and Post-Mortems](#integrate-security-into-defect-tracking-and-post-mortems)
- [Integrate Preventive Security Controls into Shared Source Code Repositories and Shared Services](#integrate-preventive-security-controls-into-shared-source-code-repositories-and-shared-services)
- [Integrate Security into Our Deployment Pipeline](#integrate-security-into-our-deployment-pipeline)
- [Ensure Security of the Application](#ensure-security-of-the-application)
  - [Case Study: Static Security Testing at Twitter (2009)](#case-study-static-security-testing-at-twitter-2009)
- [Ensure Security of Our Software Supply Chain](#ensure-security-of-our-software-supply-chain)
  - [Continuous Learning: Open-Source Dependencies and Supply Chain Security](#continuous-learning-open-source-dependencies-and-supply-chain-security)
- [Ensure Security of the Environment](#ensure-security-of-the-environment)
  - [Case Study: 18F Automating Compliance for the Federal Government with Compliance Masonry (2016)](#case-study-18f-automating-compliance-for-the-federal-government-with-compliance-masonry-2016)
- [Integrate Information Security into Production Telemetry](#integrate-information-security-into-production-telemetry)
  - [Creating Security Telemetry in Our Applications](#creating-security-telemetry-in-our-applications)
  - [Creating Security Telemetry in Our Environment](#creating-security-telemetry-in-our-environment)
  - [Case Study: Instrumenting the Environment at Etsy (2010)](#case-study-instrumenting-the-environment-at-etsy-2010)
- [Protect Our Deployment Pipeline](#protect-our-deployment-pipeline)
  - [Case Study: Shifting Security Left at Fannie Mae (2020)](#case-study-shifting-security-left-at-fannie-mae-2020)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Information Security in DevOps](#how-generative-ai-is-reshaping-information-security-in-devops)

---

## Integrate Security into Development Iteration Demonstrations

The chapter opens with a diagnosis of why Infosec is so often at odds with DevOps. James Wickett, co-creator of the Gauntlt security tool and organizer of DevOpsDays Austin, frames the structural problem:

> "One interpretation of DevOps is that it came from the need to enable developer's productivity, because as the number of developers grew, there weren't enough Ops people to handle all the resulting deployment work. This shortage is even worse in Infosec -- the ratio of engineers in Development, Operations, and Infosec in a typical technology organization is 100:10:1. When Infosec is that outnumbered, without automation and integrating information security into the daily work of Dev and Ops, Infosec can only do compliance checking, which is the opposite of security engineering -- and besides, it also makes everyone hate us."

The 100:10:1 ratio is the root cause. When a single Infosec engineer must cover the output of 100 developers and 10 operations staff, the only feasible strategy is compliance checking -- reviewing checklists at the end of a project rather than doing genuine security engineering throughout.

Wickett and Josh Corman (former CTO of Sonatype) coined the term **Rugged DevOps** to describe incorporating information security objectives into DevOps. The chapter traces this lineage back to *Visible Ops Security* by Gene Kim, Paul Love, and George Spafford, and to Dr. Tapabrata Pal's work at Capital One, where the team described their processes as **DevOpsSec**.

> **[Deep Dive: Shift-Left Security]**
>
> "Shift-left" means moving security activities earlier in the software development lifecycle -- from the end (where they traditionally occur as a gatekeeping review) to the beginning (where they can shape design decisions). The chapter's first recommendation -- invite Infosec to iteration demos -- is the simplest and most accessible form of shift-left. It requires no tooling, no automation, and no organizational restructuring. It simply asks: let Infosec see what is being built as it is being built. The payoff is that Infosec can provide guidance when there is "the most amount of time and freedom to make corrections," rather than delivering a 200-page PDF of vulnerabilities when the project is essentially complete and no one has time or budget to fix anything.

The key practice is **inviting Infosec to product demonstrations at the end of each development interval**. Justin Arbuckle, former Chief Architect at GE Capital, describes the practice they called "compliance by demonstration":

> "When it came to information security and compliance, we found that blockages at the end of the project as much more expensive than at the beginning -- and Infosec blockages were among the worst. 'Compliance by demonstration' became one of the rituals we used to shift all this complexity earlier in the process. . . . By having Infosec involved throughout the creation of any new capability, we were able to reduce our use of static checklists dramatically and rely more on using their expertise throughout the entire software development process."

Snehal Antani, former CIO of Enterprise Architecture at GE Capital Americas, described their top three key business measurements as "development velocity (i.e., speed of delivering features to market), failed customer interactions (i.e., outages, errors), and compliance response time (i.e., lead time from audit request to delivery of all quantitative and qualitative information required to fulfill the request)."

> **[Insight]** The inclusion of "compliance response time" as one of only three key business metrics is significant. It elevates compliance from a cost center to a first-class business measurement, alongside speed and reliability. This framing tells compliance teams that their work matters -- and it tells engineering teams that compliance efficiency is their responsibility too.

---

## Integrate Security into Defect Tracking and Post-Mortems

The traditional Infosec pattern is to store all security vulnerabilities in a GRC (governance, risk, and compliance) tool that only Infosec has access to. The DevOps alternative is to put security issues into the same work tracking system that Development and Operations use -- making the work visible and prioritizable alongside all other work.

Nick Galbreath, who headed Information Security at Etsy for many years, describes this approach:

> "We put all security issues into JIRA, which all engineers use in their daily work, and they were either 'P1' or 'P2,' meaning that they had to be fixed immediately or by the end of the week, even if the issue is only an internally facing application."

Galbreath also emphasizes the learning dimension:

> "Any time we had a security issue, we would conduct a post-mortem, because it would result in better educating our engineers on how to prevent it from happening again in the future, as well as a fantastic mechanism for transferring security knowledge to our engineering teams."

> **[Insight]** The choice to use only two priority levels (P1: fix immediately, P2: fix by end of week) is a deliberate design decision. It eliminates the paralysis that comes from complex priority matrices (P1 through P5, severity/priority grids) where security issues languish at P3 or P4 because they are never "urgent enough." With only two levels, every security issue is urgent. This sends a clear cultural signal: security is not optional, and security debt is not acceptable.

---

## Integrate Preventive Security Controls into Shared Source Code Repositories and Shared Services

Building on the shared source code repository concept from Chapter 20, this section describes how to add security-specific mechanisms and tools to that repository. The goal is to make it easy for any engineer to use pre-blessed, security-approved libraries and configurations.

> **[Deep Dive: Security as Code]**
>
> "Security as code" is the practice of defining and managing security policies, configurations, and controls through version-controlled code rather than through manual processes or documentation. When the chapter describes putting authentication libraries, encryption standards, and configuration hardening settings into the shared source code repository, it is describing security as code in its most practical form. The key insight is that version control is not just a storage mechanism -- it is an "omni-directional communication mechanism to keep all parties aware of changes being made." When a security-sensitive library is updated, the commit notification goes to everyone who needs to know. When a configuration hardening standard changes, the diff shows exactly what changed and why.

The chapter provides a concrete list of what should be in the shared repository:

- **Code libraries and their recommended configurations:** 2FA (two-factor authentication library), bcrypt password hashing, logging
- **Secret management tools:** Vault, sneaker, Keywhiz, credstash, Trousseau, Red October (with a note that all major cloud providers now operate cloud-based secret management systems as a good alternative)
- **OS packages and builds:** NTP for time syncing, secure versions of OpenSSL with correct configurations, OSSEC or Tripwire for file integrity monitoring, syslog configuration for centralized ELK stack logging

> **[Deep Dive: Secrets Management]**
>
> The chapter's mention of tools like Vault, Keywhiz, and credstash touches on one of the most critical and frequently mishandled areas of security engineering. Secrets -- database passwords, API keys, encryption keys, certificates -- must never be stored in source code, configuration files, or environment variables in plaintext. A mature secrets management strategy involves:
>
> 1. **Centralized secret storage** with encryption at rest and in transit (HashiCorp Vault, AWS Secrets Manager, Azure Key Vault, GCP Secret Manager)
> 2. **Dynamic secrets** that are generated on demand and expire automatically, eliminating long-lived credentials
> 3. **Secret rotation** -- automated periodic rotation of all credentials
> 4. **Audit logging** of all secret access for forensic and compliance purposes
> 5. **Least-privilege access** -- services only have access to the secrets they need
>
> The most common security breach vector in DevOps environments is leaked secrets: API keys committed to Git, database passwords hardcoded in Docker images, or cloud credentials left in CI/CD environment variables. Tools like git-secrets, truffleHog, and GitHub's built-in secret scanning can detect these before they reach production.

For container-based environments, the chapter adds an important supply chain note:

> "Now that Docker-based systems are ubiquitous, organizations should use a container registry to hold all base images. In order to secure the software supply chain, these source versions should be stored along with a secure hash of the image created. This hash must be validated whenever the image is used or deployed."

> **[2024+ Context: Supply Chain Security -- SLSA, Sigstore, and SBOM]**
>
> The chapter's advice to store secure hashes of container images has evolved into a comprehensive supply chain security framework:
>
> - **SLSA (Supply-chain Levels for Software Artifacts):** Developed by Google and adopted by the OpenSSF, SLSA provides four levels of increasing build integrity guarantees. At Level 3, the build process is fully defined in source, the build service is hardened, and there is cryptographic proof that the deployed artifact matches the tested artifact. SLSA addresses the exact threats illustrated by the SolarWinds and Codecov attacks described later in this chapter.
>
> - **Sigstore:** A project under the Linux Foundation that provides keyless signing and verification for software artifacts. Sigstore's components -- Cosign (container signing), Fulcio (certificate authority), and Rekor (transparency log) -- make it practical to sign every container image, binary, and SBOM without the operational burden of managing PGP keys.
>
> - **SBOM (Software Bill of Materials):** Executive Order 14028 (May 2021) directed US federal agencies to require SBOMs from software vendors. Standards like SPDX and CycloneDX define machine-readable formats for listing all components in a software product. SBOMs make the dependency analysis described in this chapter scalable and automated.
>
> - **OPA (Open Policy Agent) and Policy-as-Code:** Tools like OPA, Kyverno, and HashiCorp Sentinel allow organizations to define security policies (e.g., "no container image may be deployed without a verified signature" or "all base images must come from the approved registry") as code that is version-controlled, testable, and automatically enforced in the deployment pipeline.

---

## Integrate Security into Our Deployment Pipeline

The chapter contrasts the old model -- where a security review after development produced "hundreds of pages of vulnerabilities in a PDF" that went unaddressed due to deadline pressure -- with the DevOps approach of automating security tests to run alongside all other tests in the deployment pipeline.

> "Our goal is to provide both Dev and Ops with fast feedback on their work so that they are notified whenever they commit changes that are potentially insecure. By doing this, we enable them to quickly detect and correct security problems as part of their daily work, which enables learning and prevents future errors."

The chapter highlights **Gauntlt** as an exemplary tool designed to integrate into deployment pipelines. Gauntlt uses Gherkin syntax for security test scripts -- the same syntax developers use for unit and functional testing -- putting security testing in a framework developers are already familiar with.

![Jenkins Running Automated Security Testing](../images/Fig22-1.jpg)
*Figure 22.1: Jenkins Running Automated Security Testing. Source: James Wicket and Gareth Rushgrove, "Battle-tested code without the battle," Velocity 2014 conference presentation.*

> **[Deep Dive: DevSecOps]**
>
> DevSecOps is the practice of integrating security into every phase of the DevOps lifecycle -- not as an afterthought or a gate, but as a continuous, automated activity embedded in the pipeline. The term signals that security is not a separate discipline bolted onto DevOps but is intrinsic to it. Key principles of DevSecOps:
>
> 1. **Automation first:** Security tests run automatically on every commit, not periodically by a human.
> 2. **Developer ownership:** Developers are responsible for the security of their code, supported by tools and training from Infosec.
> 3. **Fast feedback:** Security findings are surfaced immediately, in the same tools developers already use, not in a separate PDF or GRC system.
> 4. **Continuous improvement:** Security defects trigger blameless post-mortems and result in new automated tests that prevent recurrence.
> 5. **Risk-based prioritization:** Not every security finding blocks the pipeline; teams agree on severity thresholds that balance speed with risk.
>
> The chapter's entire structure -- from iteration demos to pipeline integration to production telemetry -- describes the DevSecOps approach, even though it uses the older term "Rugged DevOps."

---

## Ensure Security of the Application

The chapter distinguishes between testing approaches:

- **Happy path testing:** Development's traditional focus -- validating positive logic flows where everything goes as expected
- **Sad path testing:** QA, Infosec, and fraud practitioners focus on what happens when things go wrong, especially security-related error conditions (sometimes called the **bad paths**)

The example given: an e-commerce site with a customer input form accepting credit card numbers. The sad and bad paths include SQL injections, buffer overruns, and other exploits that must be tested.

The chapter outlines four categories of security testing:

**Static analysis:** Testing in a non-runtime environment, ideally in the deployment pipeline. Tools inspect program code for all possible runtime behaviors, seeking coding flaws, back doors, and malicious code ("testing from the inside out"). Examples: Brakeman, Code Climate, searching for banned code functions (e.g., "exec()").

**Dynamic analysis:** Tests executed while a program is in operation, monitoring system memory, functional behavior, response time, and performance ("testing from the outside in"). Examples: Arachni, OWASP ZAP (Zed Attack Proxy). Automated penetration testing with tools like Nmap and Metasploit should also be included.

> **[Deep Dive: Dependency Scanning]**
>
> **Dependency scanning** is another type of static testing performed at build time inside the deployment pipeline. It inventories all dependencies for binaries and executables, ensuring they are free of vulnerabilities or malicious binaries. Examples: Gemnasium and bundler audit for Ruby, Maven for Java, OWASP Dependency-Check.
>
> Modern dependency scanning has evolved significantly since the book's examples. GitHub's Dependabot, Snyk, Grype, and Trivy can scan not just application dependencies but also container images, infrastructure-as-code templates, and even CI/CD pipeline configurations. The most mature organizations run dependency scanning at multiple points: at commit time (in the IDE), at build time (in the pipeline), at deploy time (scanning the final artifact), and continuously in production (detecting newly disclosed vulnerabilities in already-deployed components).

**Source code integrity and code signing:** All developers should have their own PGP key (managed via systems like keybase.io). All commits to version control should be signed. All packages created by the CI process should be signed, with their hash recorded in the centralized logging service.

The chapter also references OWASP's Cheat Sheet series, which covers:
- How to store passwords
- How to handle forgotten passwords
- How to handle logging
- How to prevent cross-site scripting (XSS) vulnerabilities

> **[Deep Dive: Threat Modeling]**
>
> While the chapter does not use the term "threat modeling" explicitly, the practices it describes -- identifying sad paths, bad paths, and security-specific error conditions -- are the practical outputs of threat modeling. Threat modeling is a structured process for identifying security threats and vulnerabilities early in the design phase. Common frameworks include:
>
> - **STRIDE** (Spoofing, Tampering, Repudiation, Information disclosure, Denial of service, Elevation of privilege) -- developed by Microsoft
> - **DREAD** (Damage, Reproducibility, Exploitability, Affected users, Discoverability) -- a risk-scoring model
> - **PASTA** (Process for Attack Simulation and Threat Analysis) -- a seven-step risk-centric methodology
> - **Attack Trees** -- visual representations of how a system can be attacked
>
> Threat modeling at the sprint level (reviewing each new feature or user story for security implications) is the most effective way to generate the sad/bad path test cases the chapter describes. Tools like OWASP Threat Dragon, Microsoft Threat Modeling Tool, and IriusRisk can help structure this process.

> **[2024+ Context: Zero Trust Architecture]**
>
> The chapter's emphasis on defense in depth -- static analysis, dynamic analysis, dependency scanning, code signing, environment hardening, and production telemetry -- aligns closely with the Zero Trust security model. Zero Trust, formalized in NIST SP 800-207, assumes that no user, device, or network is inherently trustworthy. Every access request must be authenticated, authorized, and continuously validated. In a DevOps context, Zero Trust manifests as:
>
> - **No implicit trust for CI/CD pipelines:** Each pipeline step authenticates to the next; credentials are scoped to the minimum necessary
> - **No implicit trust for container images:** Every image is verified against a signed digest before deployment
> - **No implicit trust for network traffic:** Service mesh (Istio, Linkerd) enforces mTLS between all services
> - **No implicit trust for human access:** Production access requires just-in-time (JIT) elevation with time-limited credentials and full audit logging
>
> NIST SP 800-207 (Zero Trust Architecture) and NIST SP 800-204 (Security Strategies for Microservices-based Application Systems) provide the authoritative frameworks for implementing these patterns.

---

### Case Study: Static Security Testing at Twitter (2009)

This is one of the chapter's most detailed case studies, tracing Twitter's security transformation from crisis to exemplar.

**The crisis:** Twitter experienced hyper-growth -- from 2.5 million to 10 million active users between January and March 2009 alone. During this period, two serious security breaches occurred:

1. **January 2009:** The @BarackObama Twitter account was hacked
2. **April 2009:** Administrative accounts were compromised through a brute-force dictionary attack

These breaches led to an **FTC consent order** requiring Twitter to:
- Designate employees responsible for their information security plan
- Identify reasonably foreseeable risks and create plans to address them
- Maintain the privacy of user information with verification and testing

The consent order had to be implemented within sixty days and enforced for **twenty years**.

**The team's approach:** Justin Collins, Alex Smolen, and Neil Matatall identified six key problems:

1. **Prevent security mistakes from being repeated** -- they were fixing the same defects over and over
2. **Integrate security objectives into existing developer tools** -- they could not generate a huge PDF report and email it; they needed to give developers the exact information needed to fix issues
3. **Preserve trust of Development** -- they needed to know when they sent false positives so they could fix the error and avoid wasting Development's time
4. **Maintain fast flow through Infosec through automation** -- even with automated scanning, manual work remained (waiting for scans, interpreting reports, finding responsible people)
5. **Make everything security related self-service, if possible** -- trusting that most people wanted to do the right thing
6. **Take a holistic approach** -- analysis from all angles: source code, production environment, customer experience

**The breakthrough:** During a company-wide hack week, the team integrated static code analysis into the Twitter build process using **Brakeman**, which scans Ruby on Rails applications for vulnerabilities. The goal was to integrate security scanning into the earliest stages of the Development process, not just at code commit.

**Results:** Over the years, Brakeman reduced the rate of vulnerabilities found by **60%**.

![Number of Brakeman Security Vulnerabilities Detected](../images/Fig22-2.jpg)
*Figure 22.2: Number of Brakeman Security Vulnerabilities Detected at Twitter. The spikes are usually associated with new releases of Brakeman that detect additional vulnerability categories.*

> **[Insight]** The Twitter case study illustrates a principle that appears throughout the DevOps Handbook: fast, automated feedback changes behavior. When developers write insecure code and find out about it six months later in a PDF, nothing changes. When they write insecure code and find out within minutes through a pipeline failure with a clear explanation and fix guidance, they learn. The 60% reduction in vulnerabilities was not primarily the result of catching more bugs -- it was the result of developers writing fewer bugs because they had internalized the security patterns through continuous feedback. This is the Third Way (continual learning and experimentation) applied to security.

---

## Ensure Security of Our Software Supply Chain

Josh Corman's observation frames this section:

> "We are no longer writing customized software -- instead, we assemble what we need from open source parts, which has become the software supply chain that we are very much reliant upon."

When organizations use open-source components, they inherit not just functionality but also any security vulnerabilities those components contain.

### Continuous Learning: Open-Source Dependencies and Supply Chain Security

The **2020 State of the Octoverse** report by Dr. Nicole Forsgren found the most frequent use of open-source dependencies in JavaScript (94%), Ruby (90%), and .NET (90%). The research also found that teams using automation to generate pull request patches for detected vulnerabilities accelerated their supply chain security **thirteen days sooner, or 1.4 times faster**, than those who did not.

The **2014 Verizon PCI Data Breach Investigation Report** found that ten CVEs accounted for almost **97% of the exploits** used in cardholder data breaches. Eight of those ten vulnerabilities were **over ten years old**.

The **2021 DBIR** confirmed this pattern: "One might think that more recent vulnerabilities would be more common. However, as we saw last year, it is actually the older vulnerabilities that are leading the way."

The **2019 Sonatype State of the Software Supply Chain Report** (co-authored by Dr. Stephen Magill and Gene Kim) analyzed Maven Central -- 4 million versions of 310,000 components serving over 146 billion download requests -- and found:

- **9%** of components had at least one vulnerability
- **47%** of components had at least one vulnerability when the component and all its transitives were analyzed
- The **median time to remediate** software vulnerabilities was **326 days**

![Time to Remediate vs. Time to Update Dependencies](../images/Fig22-3.jpg)
*Figure 22.3: Time to Remediate (TTR) vs. Time to Update Dependencies (TTU). Projects that update more frequently tend to remediate their security vulnerabilities faster. Source: Sonatype, 2019 Software Supply Chain Report.*

This correlation between update frequency and vulnerability remediation speed is why Jeremy Long, founder of OWASP Dependency Check, suggests that **the best security patching strategy is to remain current on all dependencies**. He speculates that "only 25% of organizations report vulnerabilities to users, and only 10% of vulnerabilities are reported as Common Vulnerabilities and Exposures (CVE)."

The report also found that "popularity" of a software project (GitHub stars, forks, Maven downloads) is **not correlated** with better security characteristics. This is problematic because many engineers select components based on popularity.

The 2019 study identified **five behavioral clusters** for open-source projects:

- **Small exemplar:** Small teams (1.6 devs), exemplary MTTU
- **Large exemplar:** Large teams (8.9 devs), exemplary MTTU, very likely foundation-supported, 11x more popular
- **Laggards:** Poor MTTU, high stale dependency count, more likely commercially supported
- **Features first:** Frequent releases but poor TTU, still reasonably popular
- **Cautious:** Good TTU but seldom completely up to date

![Five Behavioral Clusters for Open-Source Projects](../images/Fig22-4.jpg)
*Figure 22.4: Five Behavioral Clusters for Open-Source Projects. Source: Sonatype, 2019 Software Supply Chain Report.*

The **2020 State of the Software Supply Chain Report** compared high-performing vs. low-performing clusters and found dramatic differences:

**Confidence of Changes:**
- 15x more frequent deployments
- 4.9x less likely to have dependencies break application functionality
- 3.8x more likely to describe updating dependencies as easy

**Security of Components:**
- 26x faster detection and remediation of vulnerable OSS components
- 33x more likely to be confident that OSS dependencies are secure
- 4.6x more likely to be confident that OSS licenses are compliant
- 2.1x more likely to have access to newer OSS component versions

**Productivity:**
- 5.7x less time for developers to be productive when switching teams
- 26x less time to approve a new OSS dependency for use
- 1.5x more likely for employees to recommend their organization as a great place to work

The practices that explained the performance differences were:
- **77%** more likely to automate approval, management, and analysis of dependencies
- **59%** more likely to use software composition analysis (SCA) tools
- **28%** more likely to enforce governance policies in CI
- **56%** more likely to have centrally managed CI infrastructure
- **51%** more likely to maintain a centralized record of all deployed artifacts (supporting SBOM collection)
- **96%** more likely to be able to centrally scan all deployed artifacts

**Supply chain attacks -- SolarWinds and Codecov:**

The **2020 State of the Octoverse** showed vulnerability timelines: a vulnerability typically takes **218 weeks (just over four years)** before being disclosed; then 4.4 weeks for the community to release a fix; then 10 weeks to alert on the fix's availability; then one week for repos that apply the fix.

Two prominent recent breaches illustrate supply chain risks:

- **SolarWinds (spring 2020):** A malicious payload was added to an update to the SolarWinds Orion network management software, affecting over **18,000 customers**. The payload used privileged accounts to gain unauthorized access across corporate network infrastructure.

- **Codecov (April 2021):** A "CI poisoning attack" -- a malicious payload added to the Codecov docker image and bash uploader stole credentials from CI environments, impacting a significant number of their 29,000 customers.

> "Both of these attacks show how reliant organizations have become on automated updates, how any CI/CD pipeline can be compromised to insert malicious payloads, and how new risks can emerge as new development practices are adopted."

> **[2024+ Context: NIST and Modern Supply Chain Security]**
>
> The supply chain security landscape has been dramatically reshaped since the events described in this chapter:
>
> - **NIST SSDF (Secure Software Development Framework, SP 800-218):** Provides a core set of secure software development practices, designed to be integrated into any SDLC. It was updated in response to Executive Order 14028.
> - **NIST SP 800-161 Rev. 1 (Cybersecurity Supply Chain Risk Management):** Provides guidance for identifying, assessing, and mitigating supply chain risks.
> - **CISA Secure by Design:** The US Cybersecurity and Infrastructure Security Agency's initiative pushing software manufacturers to build security into products from the design phase -- exactly what this chapter advocates.
> - **OpenSSF (Open Source Security Foundation):** A cross-industry collaboration under the Linux Foundation working on securing open-source software. Projects include Scorecard (automated security health checks), SLSA (build integrity), Sigstore (artifact signing), and the Alpha-Omega Project (funding security improvements in critical open-source projects).
> - **EU Cyber Resilience Act (CRA):** Requires software products sold in the EU to meet cybersecurity requirements throughout their lifecycle, including vulnerability handling and SBOM provision.

---

## Ensure Security of the Environment

Even with known, good configurations created, monitoring controls must verify that all production instances match those known good states. The chapter describes two complementary approaches:

1. **Correctness testing ("as it should be"):** Automated tests to ensure configuration hardening, database security settings, key lengths, etc. are correctly applied. Tools include automated configuration management systems (Puppet, Chef, Ansible, Salt) and tools like ServerSpec and the Netflix Simian Army (Conformity Monkey, Security Monkey).

2. **Environment scanning ("as it actually is"):** Understanding actual environment state. Examples: Nmap to ensure only expected ports are open, Metasploit to ensure adequate hardening against known vulnerabilities. Outputs should go into the artifact repository and be compared with previous versions.

### Case Study: 18F Automating Compliance for the Federal Government with Compliance Masonry (2016)

**Context:** US Federal Government agencies were projected to spend nearly **$80 billion** on IT in 2016. To take any system from "dev complete" to "live in production" requires obtaining an **authority to operate (ATO)** from a designated approving authority (DAA). The governing documents number over **four thousand pages** of laws, policies, and regulations (FISMA, FedRAMP, FITARA). Even low-security systems require over **one hundred controls** to be implemented, documented, and tested. ATO approval typically takes **eight to fourteen months** after "dev complete."

Mike Bland explains 18F's origin: "18F was created within the General Services Administration to capitalize on the momentum generated by the Healthcare.gov recovery to reform how the government builds and buys software."

**Cloud.gov:** A platform-as-a-service built from open-source components running on AWS GovCloud. Cloud.gov handles operational concerns (logging, monitoring, alerting, service lifecycle management) and the bulk of compliance concerns. By running on this platform, a large majority of infrastructure and platform-level controls are handled automatically, leaving only application-layer controls for individual teams.

**Compliance Masonry:** A prototype tool for automating the creation of **system security plans (SSPs)** -- "comprehensive descriptions of the system's architecture, implemented controls, and general security posture . . . often incredibly complex, running several hundred pages in length." SSP data is stored in **machine-readable YAML** and automatically rendered into GitBooks and PDFs. The work is done in partnership with the **OpenControl** community and published as open source.

> **[Insight]** The 18F case study demonstrates a powerful pattern: solve the compliance problem once at the platform level so that every application team inherits the solution. Instead of each team independently documenting and testing 100+ controls, the platform handles 80% of them. This is the same "paved road" concept Fannie Mae's Chris Porter describes later in the chapter. The platform becomes a compliance multiplier -- the investment in building compliance into the platform pays dividends across every application that runs on it.

> **[2024+ Context: Policy-as-Code with OPA]**
>
> The machine-readable compliance approach pioneered by Compliance Masonry has evolved into a broader "policy-as-code" movement:
>
> - **Open Policy Agent (OPA):** A general-purpose policy engine that decouples policy decisions from applications. Policies are written in Rego, a declarative language. OPA is used across the CNCF ecosystem to enforce admission control in Kubernetes, authorization in microservices, and compliance rules in CI/CD pipelines.
> - **Kyverno:** A Kubernetes-native policy engine that uses YAML (no new language to learn) to define policies like "all containers must come from the approved registry" or "all pods must have resource limits."
> - **Conftest:** Uses OPA to test structured configuration data (Kubernetes manifests, Terraform plans, Dockerfiles) against policy, integrating directly into CI/CD pipelines.
> - **Compliance-as-Code Frameworks:** Tools like Chef InSpec, HashiCorp Sentinel, and AWS Config Rules allow compliance requirements to be expressed as executable tests that run continuously against live infrastructure.

---

## Integrate Information Security into Production Telemetry

Marcus Sachs observed in 2010:

> "Year after year, in the vast majority of cardholder data breaches, the organization detected the security breach months or quarters after the breach occurred. Worse, the way the breach was detected was not an internal monitoring control but was far more likely someone outside of the organization, usually a business partner or the customer who notices fraudulent transactions. One of the primary reasons for this is that no one in the organization was regularly reviewing the log files."

The chapter advocates integrating security telemetry into the same tools Development, QA, and Operations already use. By radiating how services are being attacked in production, the organization reinforces that everyone needs to think about security risks in their daily work.

### Creating Security Telemetry in Our Applications

Application-level telemetry for detecting problematic user behavior:
- Successful and unsuccessful user logins
- User password resets
- User email address resets
- User credit card changes

The ratio of unsuccessful login attempts to successful logins serves as an early indicator of brute-force attacks.

### Creating Security Telemetry in Our Environment

Environment-level telemetry for detecting unauthorized access:
- OS changes (in production and build infrastructure)
- Security group changes
- Changes to production configurations (OSSEC, Puppet, Chef, Tripwire, Kubernetes, network infrastructure, middleware)
- Cloud infrastructure changes (VPC, security groups, users and privileges)
- XSS attempts (cross-site scripting attacks)
- SQLi attempts (SQL injection attacks)
- Web server errors (4XX and 5XX errors)

### Case Study: Instrumenting the Environment at Etsy (2010)

**Context:** Nick Galbreath was director of engineering at Etsy, responsible for information security, fraud control, and privacy. He defined fraud as "when the system works incorrectly, allowing invalid or un-inspected input into the system, causing financial loss, data loss/theft, system downtime, vandalism, or an attack on another system."

Rather than creating a separate fraud control or information security department, Galbreath embedded those responsibilities throughout the DevOps value stream by creating security-related telemetry displayed alongside Dev and Ops metrics.

Three examples of security telemetry at Etsy:

1. **Abnormal production program terminations** (segmentation faults, core dumps): "Of particular concern was why certain processes kept dumping core across our entire production environment, triggered from traffic coming from the one IP address, over and over again. Of equal concern were those HTTP '500 Internal Server Errors.' These are indicators that a vulnerability was being exploited to gain unauthorized access to our systems, and that a patch needs to be urgently applied."

2. **Database syntax errors:** "We were always looking for database syntax errors inside our code -- these either enabled SQL injection attacks or were actual attacks in progress. For this reason, we had zero tolerance for database syntax errors in our code, because it remains one of the leading attack vectors used to compromise systems."

3. **Indications of SQL injection attacks:** "This was a ridiculously simple test -- we'd merely alert whenever 'UNION ALL' showed up in user-input fields, since it almost always indicates a SQL injection attack. We also added unit tests to make sure that this type of uncontrolled user input could never be allowed into our database queries."

![Developers See SQL Injection Attempts in Graphite at Etsy](../images/Fig22-5.jpg)
*Figure 22.5: Developers See SQL Injection Attempts in Graphite at Etsy. Source: Nick Galbreath, "DevOpsSec: Applying DevOps Principles to Security, DevOpsDays Austin 2012."*

Galbreath's observation about the transformative effect:

> "Nothing helps developers understand how hostile the operating environment is than seeing their code being attacked in real time."

> "One of the results of showing this graph was that developers realized that they were being attacked all the time! And that was awesome, because it changed how developers thought about the security of their code as they were writing the code."

> **[Insight]** The "UNION ALL" detection is a masterclass in pragmatic security engineering. It is not sophisticated. It is not a machine learning model or a complex WAF rule. It is a string match on two words. And it works, because SQL injection attacks overwhelmingly use that specific pattern. The lesson is that security telemetry does not need to be complex to be effective. Start with the simplest signal that detects the most common attack, make it visible, and iterate. Perfect is the enemy of deployed.

---

## Protect Our Deployment Pipeline

The CI/CD pipeline itself presents a new attack surface. Jonathan Claudius, former Senior Security Tester at TrustWave SpiderLabs, warns:

> "Continuous build and test servers are awesome, and I use them myself. But I started thinking about ways to use CI/CD as a way to inject malicious code. Which led to the question: Where would be a good place to hide malicious code? The answer was obvious: in the unit tests. No one actually looks at the unit tests, and they're run every time someone commits code to the repo."

Pipeline protection strategies include:

- **Harden CI servers** and ensure they can be reproduced in an automated manner, just like customer-facing production infrastructure
- **Review all changes** introduced into version control, either through pair programming at commit time or code review between commit and merge
- **Instrument the repository** to detect when test code contains suspicious API calls (e.g., unit tests accessing the file system or network), quarantining it and triggering immediate code review
- **Isolate every CI process** on its own container or VM, recreated from a known, good, verified base image at the start of every build
- **Ensure version control credentials** used by the CI system are read-only

### Case Study: Shifting Security Left at Fannie Mae (2020)

**Context:** Fannie Mae has a more than **$3 billion** balance sheet and helps finance approximately **one in four homes** in the US as of 2020. Safety and soundness is part of their mission, and they have a low risk tolerance.

Chris Porter (CISO) and Kimberly Johnson (EVP and COO) presented their evolution at the **2020 DevOps Enterprise Summit**. The transformation boiled down to two key changes: changing culture and changing how security communicated with Dev teams and integrated security tools.

**The old way:** Dev would hand off production-ready code. Security would conduct their own tests and send back a list of vulnerabilities for Dev to correct. It was inefficient and no one liked it.

**The new way -- shifting security left:**
1. Relinquished control over security tools, making them **self-service and API-based**
2. Integrated tools with **Jira and Jenkins**
3. Trained developers to run the tools and understand results
4. Changed nomenclature: instead of "vulnerabilities," they talked about **"defects"**
5. Fully integrated all security tests within the **CI/CD pipeline** so every code check-in triggered tests

Chris Porter describes the approach:

> "I call this the paved road. If you follow the paved road and you use the CI/CD pipeline, which has all the checks integrated into the pipeline, then it will be easier for you to deploy code."

This operated like an **Andon cord** -- if a test did not pass, it broke the line and had to be fixed before the line could continue. Not using the paved road meant "a much slower, bumpier journey."

Porter on the mindset shift:

> "A mindset change is needed from development and security. In the past, security's mindset had been to protect developers from themselves. But in a DevOps model, the work has moved to 'you build it, you own it.'"

Kimberly Johnson's summary of the business impact:

> "In the old way, with Dev handing off production-ready code to Security for testing, we had a major bottleneck in the throughput of the Security team. For large organizations that operate at scale, it can be really hard to find enough Security talent to continually test everything that is developed. Building the security tests into the development pipeline unlocked a lot more productivity for us and reduced our dependence on Security personnel for standard testing and routine deployments.
> In addition to reducing our reliance on the Information Security team, shifting left and automating our testing has yielded better business results. Our deployment frequency has increased by 25% in the last year, and our deployment failure rate has fallen by about the same amount. We are getting critical business changes into production much faster, with fewer errors, using fewer resources, and generating less rework. Moving to DevSecOps has been a win-win-win for us."

> **[Insight]** The nomenclature change -- from "vulnerabilities" to "defects" -- is a subtle but powerful cultural move. "Vulnerability" belongs to the security domain and carries an accusatory connotation (someone left a vulnerability in the code). "Defect" belongs to the engineering domain and carries a neutral, fixable connotation (the code has a defect, let us fix it). By changing the word, Fannie Mae reframed security issues as normal engineering work rather than special security problems, making developers more willing to engage with them.

---

## Conclusion

The chapter concludes:

> "Throughout this chapter, we have described ways to integrate information security objectives into all stages of our daily work. We do this by integrating security controls into the mechanisms we've already created, ensuring that all on-demand environments are also in a hardened, risk-reduced state -- by integrating security testing into the deployment pipeline and ensuring the creation of security telemetry in pre-production and production environments. By doing so, we enable developer and operational productivity to increase while simultaneously increasing our overall safety."

The pattern across every section is the same: take the DevOps practices already established (shared repos, deployment pipelines, telemetry, blameless post-mortems) and extend them with security-specific content. Security does not require a separate set of tools, processes, or organizational structures -- it requires the existing DevOps practices to be security-aware.

---

## How Generative AI Is Reshaping Information Security in DevOps

> **[GenAI + DevOps]**

Generative AI is transforming every layer of the security integration described in this chapter. Here is how the chapter's concepts map to AI-driven capabilities:

### GenAI and Security Testing Automation

| Security Area | Traditional | With GenAI |
|---|---|---|
| Static analysis | Rule-based scanners with predefined patterns | AI models detect novel vulnerability patterns, reduce false positives, explain findings in context |
| Dynamic analysis | Predefined attack payloads and test scripts | AI generates context-aware attack payloads tailored to the specific application |
| Dependency scanning | CVE database matching against dependency manifests | AI correlates vulnerability intelligence with actual usage patterns, prioritizing exploitable vulnerabilities over theoretical ones |
| Threat modeling | Manual workshops with security experts | AI generates threat models from architecture diagrams, code, and infrastructure definitions |
| Security code review | Rule-based linters and manual expert review | AI reviewers (GitHub Copilot code review, Amazon CodeGuru, Semgrep with AI) identify security anti-patterns in context |

### GenAI and Security Telemetry

- **AI-powered anomaly detection:** Instead of manually defining thresholds for login failures or SQL injection patterns (like Etsy's "UNION ALL" string match), AI models learn normal behavior patterns and flag deviations automatically
- **Natural language incident triage:** Security analysts can query telemetry in natural language -- "Show me all authentication failures from unusual geolocations in the last 24 hours" -- instead of writing complex queries
- **Automated incident response runbooks:** AI generates and executes response playbooks based on detected attack patterns

### GenAI and Supply Chain Security

- **AI-generated SBOMs:** Tools like Snyk and Sonatype use AI to identify dependencies that static analysis misses (dynamically loaded libraries, vendored code)
- **Vulnerability impact analysis:** AI determines whether a vulnerability in a dependency is actually reachable in the context of a specific application, dramatically reducing false positive remediation burden
- **AI-assisted patch generation:** Given a vulnerability and the affected code, AI can suggest or generate patches

### The Tension: AI as Both Shield and Sword

AI creates new security challenges even as it solves existing ones:

- **AI-generated code introduces new vulnerabilities:** Studies show AI coding assistants sometimes suggest insecure patterns (e.g., using deprecated cryptographic functions)
- **AI-powered social engineering:** Phishing and social engineering attacks become more sophisticated with AI-generated content
- **Prompt injection attacks:** AI-integrated pipelines may be vulnerable to prompt injection through malicious code comments or commit messages
- **Model supply chain risk:** AI models themselves become dependencies that must be secured, versioned, and audited

**Further reading:**
- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) -- security risks specific to AI/LLM-integrated applications
- [NIST AI Risk Management Framework (AI RMF)](https://www.nist.gov/artificial-intelligence) -- the emerging standard for AI governance
- [Semgrep AI](https://semgrep.dev/) -- AI-powered static analysis with security focus
- [Snyk AI Security](https://snyk.io/) -- AI-driven vulnerability detection and remediation
- [OpenSSF Scorecard](https://scorecard.dev/) -- automated security health checks for open-source projects
- [SLSA Framework](https://slsa.dev/) -- supply-chain integrity levels for software artifacts
- [Sigstore](https://www.sigstore.dev/) -- keyless signing and verification for software supply chain
- [EU AI Act](https://artificialintelligenceact.eu/) -- regulatory framework for AI systems
