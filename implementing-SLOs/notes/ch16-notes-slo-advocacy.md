# Chapter 16: SLO Advocacy

> **Implementing Service Level Objectives** — Daria Barteneva, Eva Parish
> *Crawl-Walk-Run Framework, Organizational Scaling, Training Programs, and Handling Resistance*

This chapter is a practitioner's guide to scaling SLO adoption beyond a single team. Barteneva and Parish describe a methodical Crawl-Walk-Run framework that takes an organization from "one team is experimenting" to "SLOs are how we make reliability decisions everywhere." The chapter is rich with specific artifacts (elevator pitches, training curricula, FAQ documents) and addresses the human challenges head-on: resistance to change, overloaded teams, and role confusion about who owns reliability. Their core insight is that organizational adoption is a marketing and education problem, not a technology problem.

This chapter is for anyone who has proven SLOs work for their team and now needs to convince 10, 50, or 200 other teams to adopt them.

## Table of Contents

- [The Crawl-Walk-Run Framework](#the-crawl-walk-run-framework)
- [Crawl Phase: Foundation](#crawl-phase-foundation)
  - [Research and Positioning](#research-and-positioning)
  - [The Elevator Pitch](#the-elevator-pitch)
  - [Documentation Suite](#documentation-suite)
  - [Training Program](#training-program)
  - [The Pilot](#the-pilot)
- [Walk Phase: Early Scaling](#walk-phase-early-scaling)
  - [White-Glove Assistance](#white-glove-assistance)
  - [Case Study Library](#case-study-library)
  - [Scaling Training](#scaling-training)
- [Run Phase: Organization-Wide Adoption](#run-phase-organization-wide-adoption)
- [Handling Challenges](#handling-challenges)

**Block types:** [Core Concept] [Implementation Guide] [Worked Example] [Common Pitfall] [Senior EM Application] [2025 Update] [Production Thinking] [Organizational Reality] [Template]

---

## The Crawl-Walk-Run Framework

> **[Core Concept: Organizational Adoption in Three Phases]**
>
> | Phase | Duration | Focus | Success Criteria |
> |---|---|---|---|
> | **Crawl** | 2-4 months | Research, build materials, pilot with one team | One team successfully using SLOs for decisions; materials ready for next teams |
> | **Walk** | 4-8 months | Assist early adopters, build case studies, scale training | 5-10 teams adopted; repeatable process established; quantified benefits |
> | **Run** | Ongoing | Community of practice, continuous improvement, organizational default | SLOs are expected for all production services; self-service adoption; culture |
>
> **Why phases matter:** Attempting to jump from "nobody uses SLOs" to "everyone must adopt SLOs by Q4" fails every time. Each phase builds the foundation for the next:
> - Crawl produces the materials and proof points
> - Walk produces the case studies and trained advocates
> - Run produces the self-sustaining culture

---

## Crawl Phase: Foundation

### Research and Positioning

> **[Implementation Guide: Understanding Your Organization Before Pitching]**
>
> Before advocating, understand the landscape:
>
> - **Current reliability practices:** How does the org currently measure/manage reliability? What's working? What's painful?
> - **Decision-making patterns:** How are reliability investments currently prioritized? Who holds authority?
> - **Cultural readiness:** Is there appetite for process change? Where is the pain sharpest?
> - **Existing vocabulary:** Does the org already use SLO-adjacent terms? (SLAs, uptime percentages, incident severity)
>
> **The positioning insight:** Frame SLOs not as "a new thing we need to do" but as "a better answer to problems we already have." The problems exist — you're offering a more systematic solution.

### The Elevator Pitch

> **[Template: Two Elevator Pitches — Engineers vs. Executives]**
>
> **For engineers (30 seconds):**
> "SLOs give us a budget for how much unreliability is acceptable. When we're within budget, we ship freely. When we're out of budget, we focus on reliability. It replaces the 'ops vs. dev' argument with data. No more guessing whether it's safe to deploy."
>
> **For executives (30 seconds):**
> "SLOs translate reliability into business terms. Instead of 'we had 3 P1 incidents this quarter' — which means different things to everyone — we say 'we consumed 85% of our reliability budget, leaving 15% margin before users are impacted enough to churn.' It connects engineering investment to customer experience with a number everyone can understand."
>
> **Why different pitches:** Engineers care about autonomy and reduced toil. Executives care about risk, customer impact, and investment efficiency. Same SLO framework, different value propositions.

### Documentation Suite

> **[Implementation Guide: The Five Documents You Need Before Starting]**
>
> Barteneva and Parish identify specific documents to prepare during crawl:
>
> | Document | Length | Audience | Purpose |
> |---|---|---|---|
> | **One-page strategy** | 1 page | Leadership | Why SLOs, what we're proposing, expected outcomes, timeline |
> | **SLO explainer** | 2 pages | All engineers | What SLOs are, how they work, how they differ from SLAs, with one example |
> | **FAQ** | 2-3 pages | Everyone | Answers to common objections and questions (living document, grows over time) |
> | **Step-by-step guide** | 3-5 pages | Teams adopting SLOs | Practical guide: how to choose SLIs, set targets, configure alerting, create dashboards |
> | **Use case document** | 1-2 pages per case | Adjacent teams | "Here's how Team X used SLOs to solve Problem Y" — becomes the case study library |
>
> **The key insight:** These documents are written ONCE and reused for every subsequent team's adoption. The investment in crawl phase documentation pays dividends throughout walk and run.

### Training Program

> **[Implementation Guide: Two Training Formats]**
>
> | Format | Duration | Content | Outcome |
> |---|---|---|---|
> | **Overview talk** | 30 minutes | What SLOs are, why they matter, one example, Q&A | Audience understands the concept and sees relevance to their work |
> | **Hands-on workshop** | 2-3 hours | Define SLIs for a real service, set initial targets, build a dashboard, configure one alert | Team leaves with a working (if preliminary) SLO for their service |
>
> **The overview talk** is for awareness. **The workshop** is for adoption. You need both — the overview creates interest, the workshop converts interest into action.
>
> **Workshop structure:**
> 1. (15 min) Brief recap of SLO concepts
> 2. (30 min) Identify user journeys for the team's service
> 3. (30 min) Define SLIs for 2-3 key journeys
> 4. (20 min) Set initial SLO targets based on historical data
> 5. (30 min) Build a basic dashboard (using existing tooling)
> 6. (15 min) Configure one fast-burn alert
> 7. (10 min) Set review date and next steps

### The Pilot

> **[Senior EM Application: Selecting the Pilot Team]**
>
> The pilot team selection determines whether your SLO initiative succeeds or fails:
>
> | Select for... | Avoid... |
> |---|---|
> | A team with an engaged lead who's interested in trying something new | A team forced to participate by mandate |
> | A service with clear users and measurable reliability | A service with ambiguous purpose or no observability |
> | A team with moderate reliability pain (something to improve) | A team in crisis (no bandwidth for new process) or a team with no issues (no motivation) |
> | A team whose success would be visible to adjacent teams | A team isolated from the rest of the org (success won't spread) |
>
> **The pilot goal is not perfection** — it's producing a credible story: "We tried SLOs. Here's what we learned. Here's the decision they helped us make. Here's what we'd do differently."

---

## Walk Phase: Early Scaling

### White-Glove Assistance

> **[Production Thinking: Hands-On Help for Early Adopters]**
>
> The first 5-10 teams after the pilot need active assistance:
>
> - **Join their sprint planning** to help identify where SLO data should influence decisions
> - **Pair on SLI definition** — the hardest step for teams without experience
> - **Review their targets** before they go live (catch obvious errors)
> - **Be available for questions** — dedicated Slack channel, office hours
> - **Celebrate their first SLO-driven decision** — make it visible to the org
>
> **Why white-glove matters:** Teams adopting SLOs without guidance will make the same mistakes your pilot team made. Your job in walk phase is to compress their learning curve from months to weeks.
>
> **The scaling limit:** You can personally assist ~5-10 teams. Beyond that, you need to scale through documentation, tooling, and trained advocates.

### Case Study Library

> **[Organizational Reality: Stories Beat Theory Every Time]**
>
> Barteneva and Parish emphasize that case studies from your own organization are 10x more persuasive than external examples:
>
> | External example | Internal case study |
> |---|---|
> | "Google uses SLOs" | "Team X used SLOs to reduce their incident rate by 40%" |
> | "The SRE book says..." | "When our checkout SLO was violated last month, the error budget policy gave the team permission to pause features and fix the retry logic" |
> | "Best practice is..." | "Here's the dashboard Team Y built. Here's the decision it helped them make last sprint." |
>
> **Case study format:**
> - **Situation:** What was the team's reliability challenge before SLOs?
> - **Action:** How did they implement SLOs? What did they measure?
> - **Result:** What decision did SLOs enable? What improved?
> - **Quote:** One sentence from the team lead about the experience
>
> Build 3-5 case studies during the walk phase. They become your primary sales tool for the run phase.

### Scaling Training

> **[Implementation Guide: Growing the Trainer Pool]**
>
> You cannot be the only person delivering SLO training. Scale by:
>
> 1. **Document your training materials** thoroughly (slides, facilitator notes, workshop guides)
> 2. **Identify 2-3 champions from early adopter teams** who grasped the concepts quickly
> 3. **Co-deliver training with them** (they observe you, then you observe them)
> 4. **Certify them to deliver independently** after 2-3 co-deliveries
> 5. **Establish office hours** where any champion can answer questions
>
> **The office hours pattern:** Weekly 30-minute open session. Anyone can bring SLO questions. Champions rotate hosting. Low commitment, high accessibility. These sessions surface FAQ additions and common stumbling blocks.

---

## Run Phase: Organization-Wide Adoption

> **[Core Concept: From Advocacy to Infrastructure]**
>
> In the run phase, SLOs transition from "something we're promoting" to "how we work." The advocacy shifts from persuasion to infrastructure:
>
> | Walk Phase (Advocacy) | Run Phase (Infrastructure) |
> |---|---|
> | Convincing teams to adopt SLOs | Providing tools that make SLOs easy to adopt |
> | Personal assistance for each team | Self-service guides and templates |
> | Case studies to prove value | Organizational expectation that production services have SLOs |
> | Training workshops | Onboarding curriculum includes SLOs |
> | Champions as volunteers | SLO expertise embedded in platform team |
>
> **Run phase activities:**
> - **Community of practice:** Regular (monthly/quarterly) cross-team SLO review meetings where teams share learnings
> - **SLO reviews:** Formal periodic assessments of SLO health across the portfolio
> - **Quality-of-service reviews:** Deep dives into services with chronic SLO issues
> - **Continuous improvement:** Platform team iterates on tooling based on team feedback
> - **Case study sharing:** New case studies continue to emerge and are shared org-wide

> **[2025 Update: Platform Engineering Makes Run Phase Easier]**
>
> By 2025, the platform engineering movement provides natural infrastructure for run-phase SLO adoption:
>
> - **Service templates** (golden paths) include pre-configured SLO dashboards and alerts from day one
> - **Service scorecards** (Cortex, OpsLevel, Backstage Soundcheck) include "has SLOs defined" as a readiness criterion
> - **Developer portals** surface SLO status alongside deployment and ownership information
> - **GitOps workflows** enable SLO-as-code: teams define SLOs in YAML, CI/CD deploys the configuration
>
> The shift: in 2020, you had to convince teams to add SLOs. In 2025, the platform includes SLOs by default — teams have to actively opt out.

---

## Handling Challenges

> **[Organizational Reality: Three Common Resistance Patterns]**
>
> Barteneva and Parish identify recurring challenges:
>
> **1. Role Misunderstanding**
>
> "That's an SRE thing, not my job."
>
> **Response:** SLOs are owned by service teams, not SRE. SRE provides the framework and tooling; the service team defines what reliability means for their users and decides how to invest. Reframe: "You already own reliability for your service — SLOs just give you better tools to manage it."
>
> **2. Change Resistance**
>
> "We've been doing fine without this. Why change?"
>
> **Response:** Don't argue against their current success. Instead, identify a specific pain point they have (incident arguments, unclear priorities, unreliable deployments) and show how SLOs address that specific pain. "Helping by showing" — don't tell them they have a problem, show them the data that reveals it.
>
> **3. Overloaded Teams**
>
> "We don't have bandwidth for another initiative."
>
> **Response:** This is often legitimate, not resistance. Offer:
> - A minimal implementation (1 SLI, 1 target, 30 minutes of setup)
> - To do the initial configuration for them (white-glove)
> - To defer until next quarter when their project completes
> - To frame it as *reducing* their work long-term (fewer false alerts, less time in incident arguments)
>
> Never force adoption on an overwhelmed team. They'll implement poorly, have a bad experience, and become vocal opponents.

> **[Worked Example: "Helping by Showing"]**
>
> **Scenario:** A team insists they don't need SLOs. Their service "is fine."
>
> **The approach:**
> 1. Ask to shadow their incident response for one month (observing, not interfering)
> 2. Track: number of incidents, time-to-detect, time-to-mitigate, was the incident user-impacting or not?
> 3. At the end of the month, present the data:
>    - "You had 4 incidents. 2 were user-impacting. Detection averaged 8 minutes."
>    - "If you had an SLO with burn-rate alerting, detection would have been ~2 minutes for the first incident — catching it before the second."
>    - "Here's what that would look like for your service specifically."
> 4. Don't push. Let the data speak. Offer to help if they're interested.
>
> This approach respects the team's autonomy while providing evidence they can't dismiss. It's slower than mandating adoption but produces genuine buy-in.

> **[Senior EM Application: The Advocacy Burnout Risk]**
>
> SLO advocacy is emotionally draining. Barteneva and Parish acknowledge this:
>
> - You'll repeat the same pitch dozens of times
> - Some teams will resist no matter what you do
> - Progress feels slow when you're in it
> - Champions burn out if they're doing it alone alongside their day job
>
> **Mitigation:**
> - Track adoption metrics (teams adopted, decisions influenced) — celebrate progress
> - Rotate advocacy responsibility among champions
> - Accept that 100% adoption isn't necessary — even 60-70% creates a strong culture
> - Budget your advocacy time explicitly (20% of your role, not 100%)
> - Celebrate wins publicly — both for the adopting team and for the advocates

> **[Common Pitfall: Mandating Without Supporting]**
>
> The fastest way to kill SLO adoption: a VP sends an email saying "all teams must have SLOs by Q3" without providing training, tooling, or support.
>
> **What happens:**
> - Teams create SLOs to check a compliance box
> - SLIs are poorly chosen (whatever's easiest to measure, not what matters)
> - Targets are arbitrary (copy-paste "99.9%" from a blog post)
> - No one uses the SLOs for decisions
> - After the mandate is "met," SLOs are never updated
> - Organization concludes "SLOs don't work for us"
>
> **The fix:** Mandates only work when accompanied by enablement. For every mandate, provide: training (30-min overview + workshop for each team), tooling (self-service SLO creation), support (office hours, champions), and a reasonable timeline (6+ months for full adoption).

---

**Chapter 16 establishes:** Scaling SLO adoption requires a deliberate Crawl-Walk-Run approach. Crawl phase builds the foundation (research, materials, pilot). Walk phase scales through white-glove assistance, case studies, and expanding the trainer pool. Run phase transitions from advocacy to infrastructure — making SLOs the default through platform tooling and organizational expectation. Internal case studies are far more persuasive than external examples. Resistance comes in three forms (role misunderstanding, change resistance, overloaded teams) — each requiring a different response. Mandates without enablement produce compliance theater. "Helping by showing" — demonstrating value through data rather than arguments — creates genuine buy-in.

**Next: Chapter 17 — Reliability Reporting (Alex Hidalgo), covering why traditional incident metrics (counts, severity, MTTX) fail as reliability measures and how SLO-based reporting provides actionable, human-understandable reliability communication.**
