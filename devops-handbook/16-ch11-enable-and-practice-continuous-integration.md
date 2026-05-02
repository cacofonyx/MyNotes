# Chapter 11: Enable and Practice Continuous Integration

> **Part III — The Technical Practices of Flow**

This chapter tackles the most controversial practice in the DevOps toolkit: continuous integration and trunk-based development. Where Chapter 10 built the automated testing safety net, Chapter 11 applies it to the thorniest human-workflow problem in software engineering -- how multiple developers share a codebase without descending into "merge hell." The chapter makes a data-backed argument that optimizing for **team productivity** (trunk-based development with daily commits) consistently outperforms optimizing for **individual productivity** (long-lived feature branches). Two detailed case studies (HP LaserJet Firmware and Bazaarvoice) provide compelling evidence at radically different scales, and DORA research validates the practices empirically.

## Table of Contents

- [HP's LaserJet Firmware (2014)](#hps-laserjet-firmware-2014)
- [Small Batch Development and What Happens When We Commit Code to Trunk Infrequently](#small-batch-development-and-what-happens-when-we-commit-code-to-trunk-infrequently)
- [Adopt Trunk-Based Development Practices](#adopt-trunk-based-development-practices)
  - [Case Study: Continuous Integration at Bazaarvoice (2012)](#case-study-continuous-integration-at-bazaarvoice-2012)
  - [DORA Research on Trunk-Based Development](#dora-research-on-trunk-based-development)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Continuous Integration](#how-generative-ai-is-reshaping-continuous-integration)

---

## HP's LaserJet Firmware (2014)

**Context:** Gary Gruver was the director of engineering for HP's LaserJet Firmware division, building firmware for all HP scanners, printers, and multifunction devices. The team: **400 developers distributed across the US, Brazil, and India.**

**The problem:** Despite the team's size, they were moving far too slowly. For years, they could not deliver new features as quickly as the business needed.

> "Marketing would come to us with a million ideas to dazzle our customer, and we'd just tell them, 'Out of your list, pick the two things you'd like to get in the next six to twelve months.'" -- Gary Gruver

**Quantifying the waste:** Only **two firmware releases per year**, with the majority of time spent porting code to support new products. Gruver estimated only **5% of developer time** was spent creating new features. The remaining 95% broke down as:

| Activity | % of Developer Time | Nature of Activity |
|----------|-------------------|-------------------|
| Detailed planning | 20% | Overhead (poor throughput misattributed to faulty estimation, leading to demands for more detailed estimates) |
| Porting code (on separate branches) | 25% | Rework / technical debt |
| Integrating code between branches | 10% | Rework / merge overhead |
| Manual testing | 15% | Manual labor (no automation) |
| **New features** | **5%** | **Actual value creation** |

> **[Deep Dive: The 5% Feature Time Problem]**
>
> This breakdown is staggering but not unusual. Consider what it means: for every $1 million spent on this 400-person team, only $50,000 went toward creating customer value. The other $950,000 was overhead, rework, and manual labor.
>
> **Why the 20% "detailed planning" is particularly revealing:** The poor throughput and high lead times were misattributed to faulty estimation, so management asked for more detailed estimates. This is a classic organizational anti-pattern: when the system is broken, the response is to add more process (more planning, more documentation, more estimation) rather than fix the system. More detailed planning does not increase throughput -- it adds overhead to an already overloaded system. The correct diagnosis was that the problem was technical (branching strategy, lack of automation, architecture), not managerial (insufficient planning).
>
> **The compound effect of branch-based development:**
> - 25% porting code across branches + 10% integrating branches = **35% of total time spent on branch management**
> - This is the direct, measurable cost of not doing trunk-based development
> - With trunk-based development, this 35% drops to near zero, because there is one codebase supporting all products

**The goal:** Increase time spent on innovation and new functionality by a **factor of ten** (from 5% to 50%). The strategy:

1. **Continuous integration and trunk-based development**
2. **Significant investment in test automation**
3. **Creation of a hardware simulator** so tests could run on a virtual platform
4. **Reproduction of test failures on developer workstations**
5. **New architecture** to support running all printers off a common build and release

**The architectural transformation:** Before, each product line required a new code branch, with each model having unique firmware built with capabilities defined at compile time (using `#define` and `#ifdef` flags). The new architecture had:
- All developers working in a **common code base**
- A **single firmware release** supporting all LaserJet models built off trunk
- Printer capabilities established at **runtime** via XML configuration files (not compile-time flags)

**Four years later -- the results:**
- **One codebase** supporting all **24 HP LaserJet product lines** developed on trunk
- Developers who thought "it would never work" could not imagine going back
- Several engineers who later left HP called to report how backward development was elsewhere, noting how difficult it is to be effective without continuous integration feedback

**The testing investment:**

> "Without automated testing, continuous integration is the fastest way to get a big pile of junk that never compiles or runs correctly." -- Gary Gruver

- Full manual testing cycle originally required **six weeks**
- Team built **2,000 printer simulators** on **six racks of servers** (constructed in six weeks)
- Created a culture that **halted all work** when the deployment pipeline broke (Andon cord from Chapter 10)

**Testing cadence:**
- Unit tests: ran on developer workstations in minutes
- Three levels of automated testing on every commit and every 2 and 4 hours
- Full regression testing every 24 hours

**Productivity metrics:**

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Builds per day | 1 | 10-15 | 10-15x increase |
| Commits per day | ~20 (via a "build boss") | 100+ (by individual developers) | 5x increase |
| Lines of code changed/added daily | Not tracked | 75,000-100,000 | -- |
| Regression test time | 6 weeks | 1 day | 42x faster |

**Business results:**

| Metric | Change |
|--------|--------|
| Time spent on innovation/new features | 5% --> 40% (**8x increase**) |
| Overall development costs | **Reduced ~40%** |
| Programs under development | **Increased ~140%** |
| Development cost per program | **Decreased 78%** |

> **[Deep Dive: The HP LaserJet ROI Calculation]**
>
> Let's work through the economics. Assume a fully loaded cost of $150,000/year per developer for 400 developers:
>
> - **Annual team cost:** 400 x $150K = $60 million/year
> - **Before: Feature development spend:** 5% x $60M = $3M/year on new features
> - **After: Feature development spend:** 40% x $60M x 0.6 (40% cost reduction) = $14.4M/year on new features
> - **Net increase in feature investment:** $14.4M - $3M = **$11.4M/year** -- nearly a 5x increase in value-creating work
> - **Simultaneously, total costs dropped 40%:** $60M --> $36M/year, saving $24M/year
>
> The total economic impact is approximately **$35M/year in combined savings and additional feature investment** -- and this doesn't account for the revenue impact of shipping 140% more products. This is why the book calls continuous integration "one of the most critical practices" -- the ROI is extraordinary.

> **[Insight]** The HP LaserJet case study is uniquely powerful because it is not a web application, not a cloud service, and not a startup. It is **embedded firmware** for physical hardware -- the domain where people most often say "continuous integration can't work for us." If 400 firmware developers across three countries can do trunk-based development on a codebase that runs physical printers, the argument that your web application is "too complex" for continuous integration is difficult to sustain. The key enablers were: (1) architectural change to support a single codebase, (2) simulators that let tests run without physical hardware, and (3) cultural change to halt work on pipeline failures. All three were necessary; none alone was sufficient.

> **[2024+ Context]** Gary Gruver has continued to advocate for these practices through his books (*Start and Scaling DevOps in the Enterprise*, *Engineering the Digital Transformation*) and consulting work. His framework has been applied across diverse industries, from automotive (where firmware faces similar challenges) to financial services. The embedded/firmware world has continued to evolve: CI/CD for embedded systems is now supported by tools like PlatformIO, QEMU-based emulators, and hardware-in-the-loop (HIL) testing platforms. The pattern -- simulate hardware to enable automated testing, then do trunk-based development -- has become standard practice in automotive (AUTOSAR), aerospace, and IoT.

---

## Small Batch Development and What Happens When We Commit Code to Trunk Infrequently

**The spectrum of branching strategies** (from Jeff Atwood, founder of Stack Overflow):

- **Optimize for individual productivity:** Every developer works in their own private branch. Nobody can disrupt anyone else's work, but merging becomes a nightmare. "Every person's work has to be painstakingly merged with everyone else's work to see even the smallest part of the complete system."
- **Optimize for team productivity:** Everyone works in the same common area (trunk). Commits are simple, but each commit can break the project and bring all progress to a screeching halt.

**The mathematical reality:** The effort required to merge branches back together **increases exponentially** as the number of branches increases.

**The problems of long-lived feature branches:**
1. **Merge hell:** Conflicting changes require manual resolution, often involving multiple developers
2. **Delayed feedback:** Instead of continuous performance testing against a fully integrated system, testing happens only at the end
3. **Cascading impact:** As code production rate increases and more developers are added, the probability of any change impacting someone else increases
4. **Reluctance to refactor:** When merging is difficult, developers become less motivated to improve and refactor code, because refactoring is more likely to cause rework for everyone else. Developers avoid modifying code with dependencies throughout the codebase -- which is tragically where the highest payoffs often are

> **[Deep Dive: The Exponential Merge Problem -- A Concrete Example]**
>
> Consider a team of 5 developers, each working on a feature branch for 2 weeks before merging:
>
> **Week 1:** Each developer changes ~500 lines across ~20 files
> **Week 2:** Each developer changes ~500 more lines, now 1,000 lines each
>
> **Merge day arrives:**
> - Developer A merges first: 1,000 lines, straightforward
> - Developer B merges: 1,000 lines, but 3 files conflict with A's changes. 30 minutes to resolve.
> - Developer C merges: 1,000 lines, 5 files conflict with A+B's merged code. 2 hours to resolve.
> - Developer D merges: 1,000 lines, 8 files conflict with A+B+C. 4 hours, requires help from B.
> - Developer E merges: 1,000 lines, 12 files conflict with A+B+C+D. Full day, breaks 3 tests.
>
> **Total merge overhead:** ~1.5 developer-days, plus broken tests that take another day to fix.
> **Total with daily commits to trunk:** Each developer merges ~100 lines/day, conflicts are 1-2 files at most, resolved in minutes. Total overhead: ~30 minutes/day for the whole team.
>
> **The scaling problem:** With 5 developers and 2-week branches, merge overhead is painful but manageable. With 50 developers and 2-week branches, merge day is a multi-day crisis. With 400 developers (like HP LaserJet), it is simply impossible -- which is why they could only ship twice a year.

**Ward Cunningham's definition of technical debt:**

> "When we do not aggressively refactor our codebase, it becomes more difficult to make changes and to maintain over time, slowing down the rate at which we can add new features."

> **[Insight]** The connection between branching strategy and technical debt is profound and underappreciated. When merging is painful, developers avoid refactoring. When developers avoid refactoring, technical debt accumulates. When technical debt accumulates, the codebase becomes harder to change. When the codebase is harder to change, developers create longer-lived branches to isolate their work. This creates a vicious cycle: **long-lived branches --> fear of merging --> no refactoring --> more technical debt --> longer-lived branches.** Trunk-based development breaks this cycle by making merging trivially easy, which removes the barrier to continuous refactoring, which keeps technical debt under control.

---

## Adopt Trunk-Based Development Practices

**The practice:** All developers check their code into trunk **at least once per day**. This reduces batch size to the work performed by the entire team in a single day. The more frequently developers check in, the smaller the batch and the closer to the theoretical ideal of single-piece flow.

**Benefits of frequent trunk commits:**
- All automated tests run on the software system as a whole after every change
- Alerts when a change breaks another part of the application or interferes with another developer's work
- Merge problems are detected when small and corrected quickly

**Gated commits:** The deployment pipeline can be configured to reject any commits that take the system out of a deployable state. The pipeline first confirms that the submitted change will successfully merge, build as expected, and pass all automated tests before actually being merged into trunk. If not, the developer is notified, allowing corrections without impacting anyone else.

**What daily commits force:**
- Breaking work into smaller chunks while keeping trunk in a working, releasable state
- Version control becomes a communication mechanism -- everyone understands the system state, the pipeline health, and can help when things break

**The updated definition of "done":**

> "At the end of each development interval, we must have integrated, tested, working, and potentially shippable code, demonstrated in a production-like environment, **created from trunk using a one-click process, and validated with automated tests.**"

**Eliminating the stabilization phase:** By keeping code in a deployable state continuously, we eliminate the common practice of having a separate test and stabilization phase at the end of the project.

> **[Deep Dive: Trunk-Based Development -- Common Objections and Responses]**
>
> Trunk-based development is, as the text says, "likely the most controversial practice discussed in this book." Here are the most common objections and evidence-based responses:
>
> | Objection | Response |
> |-----------|----------|
> | "We need feature branches to prevent incomplete features from reaching production" | Use **feature flags/toggles** (Chapter 12) to hide incomplete features in production code. The code is in trunk, but the feature is not visible to users. |
> | "Our code reviews require branches and pull requests" | Use **pair programming** (no review queue) or **short-lived branches** (<1 day) with rapid review. Google's approach: code is reviewed *before* it enters trunk, not on long-lived branches. |
> | "Trunk-based dev means no isolation -- one bad commit breaks everyone" | This is exactly what **gated commits** and **fast automated tests** prevent. A bad commit is either rejected by the gate or immediately visible and fixable. |
> | "Our team is too large for everyone to commit to trunk" | Google has 30,000+ developers committing to a single monorepo. Scale is not the issue; testing infrastructure and architectural decoupling are. |
> | "We need branches for release management" | Use **release branches** cut from trunk (never the other way around). These are short-lived and receive only cherry-picked fixes. Development always happens on trunk. |
> | "Our regulators require branch-based change control" | The deployment pipeline provides complete audit trails. Every commit is tested, every deployment is traceable. This typically *exceeds* the evidence provided by manual branch-based processes. |
>
> **The empirical evidence is clear:** DORA research shows that trunk-based development predicts higher throughput, better stability, and better availability. The objections are real concerns, but each has a well-tested solution.

> **[2024+ Context]** Trunk-based development has gained significant ground since this book was written, but the debate continues:
>
> - **Google's research** (published in *Software Engineering at Google*, 2020) provides extensive documentation of their trunk-based monorepo approach, serving as the largest-scale proof point
> - **Meta (Facebook)** also uses a trunk-based monorepo approach for their primary codebase
> - **The "short-lived feature branches" compromise** has become the most common middle ground: branches that live for hours or at most 1-2 days, reviewed quickly, and merged to trunk. GitHub Flow and GitLab Flow embody this approach.
> - **Stacking tools** (Graphite, ghstack, spr) enable developers to work on dependent changes as a series of small, reviewable, independently mergeable commits -- getting the isolation benefits of branches with the integration benefits of trunk-based development
> - **The research keeps accumulating:** The 2022 and 2023 DORA reports continued to validate that teams with trunk-based development (or very short-lived branches) have better delivery performance. A 2024 study by LinearB found that teams with branch lifetimes under 24 hours had 3x fewer production incidents than teams with branch lifetimes over 5 days.

---

### Case Study: Continuous Integration at Bazaarvoice (2012)

**Context:** Ernest Mueller, who had previously helped engineer the DevOps transformation at National Instruments, joined Bazaarvoice in 2012. Bazaarvoice supplied customer-generated content (reviews, ratings) for thousands of retailers (Best Buy, Nike, Walmart). At the time: $120 million in revenue, preparing for IPO.

**The application:** The Bazaarvoice Conversations application -- a monolithic Java application:
- ~5 million lines of code (dating back to 2006)
- ~15,000 files
- Running on 1,200 servers across four data centers and multiple cloud providers

**The trigger:** The team had switched to Agile with two-week sprints and wanted to increase release frequency from their ten-week production release schedule.

**The first attempt (January 2012):**

> "It didn't go well. It caused massive chaos, with forty-four production incidents filed by our customers. The major reaction from management was basically 'Let's not ever do that again.'" -- Ernest Mueller

**Root cause analysis -- three core problems:**
1. **Lack of test automation** made any level of testing during two-week intervals inadequate
2. **Version control branching strategy** allowed developers to check in new code right up to the production release
3. **Microservice teams** performing independent releases were causing issues during monolith releases

**The six-week fix:** Mueller concluded the monolithic Conversations deployment needed continuous integration. For six weeks, **developers stopped doing feature work** to focus on:
- Writing automated testing suites (unit tests in JUnit, regression tests in Selenium)
- Getting a deployment pipeline running in TeamCity

> "By running these tests all the time, we felt like we could make changes with some level of safety. And most importantly, we could immediately find when someone broke something, as opposed to discovering it only after it's in production." -- Ernest Mueller

**The branching model change:** Switched to a trunk/branch release model:
- Every two weeks, a new dedicated release branch was created
- **No new commits** allowed to the release branch unless emergency (all changes through a sign-off process)
- The branch went through QA, then was promoted to production

**The dramatic improvement:**

| Release | Date | Customer Incidents | Notes |
|---------|------|-------------------|-------|
| Pre-CI attempt | January 2012 | **44** | "Massive chaos" |
| First CI release | March 6, 2012 | **5** | 5 days late |
| Second CI release | March 22, 2012 | **1** | On time |
| Third CI release | April 5, 2012 | **0** | On time |

**From 44 incidents to zero in three months.**

**Scaling further:**

> "We had such success with releases every two weeks, we went to weekly releases, which required almost no changes from the engineering teams. Because releases became so routine, it was as simple as doubling the number of releases on the calendar and releasing when the calendar told us to. Seriously, it was almost a non-event."

Mueller noted that the majority of changes required to move to weekly releases were in **customer service and marketing teams** (changing processes like weekly customer emails), not in engineering.

**Subsequent improvements:**
- Testing time reduced from **3+ hours to less than 1 hour**
- Environments reduced from four to three (Dev, Test, Production -- eliminated Staging)
- Moved toward full continuous delivery with fast, one-click deployments

> **[Deep Dive: The Feature Freeze as Investment]**
>
> The six-week feature freeze at Bazaarvoice deserves special attention. Management was asked to stop all feature work for six weeks -- during an IPO year -- to invest in testing and CI infrastructure. This required significant courage and organizational alignment.
>
> **The ROI calculation:**
> - **Cost of the freeze:** 6 weeks of feature development lost (assume 50 developers x 6 weeks = 300 developer-weeks)
> - **Cost of the January incident:** 44 customer incidents at a company serving Best Buy, Nike, and Walmart, during IPO preparation (reputation damage, customer trust, engineering firefighting time)
> - **Ongoing cost of the old model:** 10-week release cycles meant features waited 2.5 months to reach customers; each failed release required weeks of stabilization
> - **Return on the freeze:** Within 3 months, zero-incident releases. Within 6 months, weekly releases. Testing time reduced 67%. One fewer environment to maintain.
>
> **The lesson:** A short, focused investment in infrastructure (testing, CI, pipeline) pays for itself many times over. But it requires making the cost of the current state visible. The 44-incident January release made the cost undeniable. Without that crisis, the investment might never have been approved. This is a common pattern: organizations often need a catalyst (a major incident, a visible failure) to justify investing in foundations.

> **[Insight]** The observation that moving from biweekly to weekly releases was "almost a non-event" is one of the most telling details in the entire case study. It demonstrates a fundamental principle: **the hardest part of increasing release frequency is going from infrequent to frequent -- not from frequent to more frequent.** Once the infrastructure, testing, and cultural practices are in place, increasing frequency is just a calendar change. This is because the underlying capability (reliable, automated, one-click deployment) is the same whether you use it once a week or once a day. The investment is in the capability; the frequency is just how often you exercise it.

---

### DORA Research on Trunk-Based Development

The 2014-2019 State of DevOps Reports provide empirical backing for continuous integration and trunk-based development.

**Key findings from the 2016 and 2017 reports:** Trunk-based development predicts higher throughput, better stability, and better availability when teams follow these practices:
- Have **three or fewer active branches** in the application's code repository
- **Merge branches to trunk at least daily**
- **Don't have code freezes or integration phases**

**Beyond delivery metrics:** DORA's research shows that continuous integration and trunk-based development contribute to **higher job satisfaction and lower rates of burnout**.

> **[Deep Dive: Why Three or Fewer Branches?]**
>
> The "three or fewer active branches" guideline is specific and measurable. Here is the reasoning:
>
> | Active Branches | Merge Complexity | Typical Use |
> |----------------|-----------------|-------------|
> | **1 (trunk only)** | None | Pure trunk-based development (Google-style) |
> | **2-3** | Low | Trunk + 1-2 short-lived release branches or short-lived feature branches |
> | **4-10** | Medium | Multiple feature branches or team branches; merge conflicts become common |
> | **10+** | High | Long-lived feature branches, team branches, release branches; integration becomes a project |
>
> The research does not say "zero branches." It acknowledges that a small number of short-lived branches (e.g., a release branch for the current release, a hotfix branch) is compatible with high performance. What it says is that **more than three active branches** is a reliable predictor of poor delivery performance. The branches themselves are not the problem -- it is the *delay in integration* they represent.

> **[Insight]** The burnout finding is significant and often overlooked. Why would branching strategy affect burnout? Because long-lived branches create unpredictable, stressful merge events. Developers dread "merge day" because they know it will be painful, time-consuming, and may undo days of their work. Trunk-based development replaces this periodic stress with small, routine integrations that are individually painless. The psychological difference between "I merge daily and it takes 5 minutes" and "I merge monthly and it takes 3 days of conflict resolution" is enormous -- even if the total time spent merging is similar, the unpredictability and concentration of pain in the branch model causes disproportionate stress.

---

## Conclusion

This chapter established:

1. **The case for continuous integration** -- two detailed case studies (HP LaserJet, Bazaarvoice) showing transformative results across different scales, technologies, and industries
2. **The problem with long-lived branches** -- exponential merge complexity, delayed feedback, reluctance to refactor, accumulated technical debt
3. **Trunk-based development** -- all developers commit to trunk at least daily, with gated commits and fast automated tests as safety mechanisms
4. **The updated definition of "done"** -- code must be integrated, tested, working, demonstrated in a production-like environment, created from trunk with one-click, and validated with automated tests
5. **Empirical validation** -- DORA research confirming trunk-based development predicts better delivery performance and lower burnout

The chapter sets the stage for Chapter 12, which covers automating the deployment process and enabling low-risk releases -- the final step in turning continuous integration into continuous delivery.

---

## How Generative AI Is Reshaping Continuous Integration

> **[GenAI + Chapter 11 Concepts]** Continuous integration and trunk-based development are being enhanced by GenAI in several ways:

**AI-Powered Code Review:**
- **GitHub Copilot code review**, **CodeRabbit**, and **Sourcery** provide instant automated review of pull requests, identifying bugs, style issues, and potential improvements
- AI review does not replace human review for design decisions and architectural choices, but it dramatically reduces the time human reviewers spend on mechanical issues
- **Impact on trunk-based development:** By reducing the time PRs spend waiting for review (the primary bottleneck in branch-based workflows), AI review makes short-lived branches viable even for teams without pair programming
- **Tools:** GitHub Copilot, CodeRabbit, Sourcery, Amazon CodeGuru

**AI Merge Conflict Resolution:**
- LLMs can analyze the semantic intent of conflicting changes and suggest resolutions
- For simple conflicts (formatting, import ordering, non-overlapping logic), AI can resolve automatically
- For complex conflicts (overlapping business logic), AI can present options with explanations
- **Impact:** Reduces the primary pain point of frequent integration, making trunk-based development less intimidating

**AI-Assisted Small Batch Development:**
- AI can help decompose large features into small, independently mergeable increments
- AI can suggest feature flag boundaries for incomplete work
- AI can analyze a large changeset and recommend how to split it into smaller, safer commits
- **The pattern:** "AI decomposition advisor" that helps developers practice the small-batch discipline that trunk-based development requires

**AI CI Pipeline Triage:**
- When CI fails, AI analyzes the error, correlates it with the commit diff, and suggests a fix
- AI can distinguish between "your code broke the build" and "the build infrastructure has an issue"
- AI can auto-fix common CI failures (dependency version conflicts, formatting issues, simple test failures)
- **Tools:** Trunk.io, Buildkite's AI features, GitHub Actions error analysis

**AI and the HP LaserJet Problem:**
- The HP LaserJet case study's core innovation was architectural: replacing compile-time flags with runtime configuration. Modern AI can help with this pattern:
  - AI can identify feature flags and compile-time conditionals in a codebase and suggest runtime alternatives
  - AI can generate the configuration schema for runtime feature selection
  - AI can help design the test matrix for a multi-product codebase

**The Meta-Insight:** AI does not change the fundamental argument of this chapter -- that optimizing for team productivity (trunk-based development) outperforms optimizing for individual productivity (long-lived branches). But AI reduces the friction of trunk-based development in three ways: faster code review (shorter branch lifetimes), smarter conflict resolution (less merge pain), and automated CI triage (faster return to green). In doing so, AI makes the already-strong case for continuous integration even stronger.

**Further reading:**
- [Trunk-Based Development](https://trunkbaseddevelopment.com/) -- comprehensive reference site by Paul Hammant
- [Google's Monorepo Paper](https://research.google/pubs/pub45424/) -- "Why Google Stores Billions of Lines of Code in a Single Repository"
- [DORA Research on Trunk-Based Development](https://dora.dev/capabilities/trunk-based-development/) -- detailed findings
- [Graphite](https://graphite.dev/) -- stacking tool for trunk-based development with code review
- [Gary Gruver's Books](https://garygruver.com/) -- *Start and Scaling DevOps in the Enterprise* and *Engineering the Digital Transformation*
- [Ship / Show / Ask](https://martinfowler.com/articles/ship-show-ask.html) -- a branching model that balances trunk-based development with code review
