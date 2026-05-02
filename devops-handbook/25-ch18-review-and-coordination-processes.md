# Chapter 18: Create Review and Coordination Processes to Increase Quality of Our Current Work

> **Part IV — The Technical Practices of Feedback**

This chapter shifts reliance away from periodic inspections and heavyweight approvals toward integrated peer review as part of daily work. It covers the dangers of overly controlling change processes, code review practices (pull requests, pair programming), coordination of changes, and cutting bureaucratic overhead — with case studies from GitHub, Google, Pivotal Labs, Adidas, and Target.

## Table of Contents

- [Peer Review at GitHub (2011)](#peer-review-at-github-2011)
- [The Dangers of Change Approval Processes](#the-dangers-of-change-approval-processes)
- [Potential Dangers of "Overly Controlling Changes"](#potential-dangers-of-overly-controlling-changes)
  - [Case Study: DORA Research on Change Approvals](#case-study-dora-research-on-change-approvals)
  - [Case Study: From Six-Eye Principle to Release at Scale at Adidas (2020)](#case-study-from-six-eye-principle-to-release-at-scale-at-adidas-2020)
- [Enable Coordination and Scheduling of Changes](#enable-coordination-and-scheduling-of-changes)
- [Enable Peer Review of Changes](#enable-peer-review-of-changes)
  - [Case Study: Code Reviews at Google (2010)](#case-study-code-reviews-at-google-2010)
  - [Potential Dangers of More Manual Testing and Change Freezes](#potential-dangers-of-more-manual-testing-and-change-freezes)
- [Enable Pair Programming to Improve All Our Changes](#enable-pair-programming-to-improve-all-our-changes)
  - [Case Study: Pair Programming at Pivotal Labs (2011)](#case-study-pair-programming-at-pivotal-labs-2011)
  - [Evaluating the Effectiveness of Pull Request Processes](#evaluating-the-effectiveness-of-pull-request-processes)
- [Fearlessly Cut Bureaucratic Processes](#fearlessly-cut-bureaucratic-processes)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Review and Coordination](#how-generative-ai-is-reshaping-review-and-coordination)

---

The chapter opens with **GitHub's peer review process** as a model: pull requests let engineers tell others about changes, review them, discuss modifications, and push follow-up commits. Engineers request "+1" or "+2" reviews and @mention specific reviewers.

![Figure 18.1: Comments and Suggestions on a GitHub Pull Request](../images/Fig18-1.jpg)
*Source: Scott Chacon, "GitHub Flow," ScottChacon.com, August 31, 2011.*

**GitHub Flow — five steps:**
1. Create a descriptively named branch off master (e.g., "new-oauth2-scopes")
2. Commit locally, regularly push to same-named remote branch
3. Open a pull request when feedback is needed or branch is ready for merge
4. Get desired reviews and approvals, then merge to master
5. Deploy merged changes to production

**Result:** In 2012, GitHub performed **12,602 deployments**. On their busiest day (after a company summit): 563 builds and 175 deployments, all through the pull request process.

> **[Deep Dive: The Pull Request as a DevOps Innovation]**
>
> The pull request is often taken for granted today, but it was a genuine innovation in workflow design. Before PRs, code review was typically either informal ("hey, look at this") or heavyweight (Gerrit-style mandatory approval queues). The PR combined several things into one artifact:
>
> - **A review request** — "please look at this change"
> - **A discussion thread** — context, questions, suggestions
> - **A deployment trigger** — merge to master = deploy
> - **An audit trail** — who changed what, who approved it, what was discussed
>
> This is why the PR became the unit of work in DevOps — it's simultaneously a quality gate, a communication tool, a deployment mechanism, and a compliance artifact. Every modern CI/CD system triggers off PR events.

---

## The Dangers of Change Approval Processes

**The Knight Capital failure:** A 15-minute deployment error caused $440 million in trading losses. The company was sold over the weekend to survive.

John Allspaw identified two counterfactual narratives:
1. **Change control failure** — better controls could have detected the risk
2. **Testing failure** — better testing could have identified the risk

**The surprising reality:** In low-trust, command-and-control cultures, adding more change controls and testing countermeasures often **increases** the likelihood of future problems.

> Gene Kim: "One of the most important moments of my professional career. This 'aha' moment was the result of a conversation in 2013 with John Allspaw and Jez Humble about the Knight Capital accident, making me question some of my core beliefs... especially having been trained as an auditor."

> **[Insight]** The Knight Capital analysis is one of the most important passages in the entire book. It challenges the deeply held belief that "more controls = more safety." The mechanism by which more controls create *less* safety: additional approval steps increase lead time → longer lead times increase batch sizes → larger batches increase risk → more failures → which trigger even more controls. It's the downward spiral from the Introduction, but applied specifically to change management. The escape route is the same: smaller batches, automated quality checks, and peer review close to the work — not more distant approvals.

---

## Potential Dangers of "Overly Controlling Changes"

Typical reactions to change control failures:
- Adding more questions to change request forms
- Requiring more authorizations (one more VP, one more board)
- Requiring more lead time for change approvals

**All of these add friction**, multiply steps and approvals, increase batch sizes and lead times — reducing the likelihood of successful outcomes.

> Toyota Production System core belief: "People closest to a problem typically know the most about it."

The further the distance between the change implementer and the change authorizer, the worse the outcome.

### Case Study: DORA Research on Change Approvals

DORA 2019 findings:
- **Lightweight change processes** (developers confident they can go from "submitted" to "accepted" for typical approvals) **contribute to high performance**
- **Heavyweight change processes** (external review board or senior manager required) have a **negative impact** on performance
- 2014 Puppet findings: high-performing teams relied more on **peer review** and less on external approval

> **[Deep Dive: What Should a Change Advisory Board Actually Do?]**
>
> The book explicitly states that change advisory boards serve an important role in **coordinating and governing** — but their job should NOT be to manually evaluate every change. ITIL does not mandate that practice.
>
> Consider the impossible predicament of a CAB member: review a complex change with hundreds of thousands of lines of code. Reading a 100-word description can't predict success. Scrutinizing thousands of lines of code is unlikely to reveal new insights. The engineers who work in the codebase daily are often surprised by side effects.
>
> **The modern CAB role:** Coordinate and sequence changes to avoid collisions, ensure risk-proportional review processes are in place, verify that automated gates are working — NOT individually approve each change. The CAB becomes a governance body that designs the system of controls, not a bottleneck that personally executes each control.

### Case Study: From Six-Eye Principle to Release at Scale at Adidas (2020)

**Context:** After experiencing five bad outages during peak sales in November 2020, Adidas was in crisis. They had 10x growth, 50% increase in digital revenue, 2-3x more visitors, 10x more technical traffic. 3,000 orders/minute, 11 billion touchpoints/day. 550 million lines of code, ~2,000 engineers.

**The nightmare:** Three VPs had to sit in a room approving every single change during the two-month peak sales period.

> "I can tell you the reality of how clueless at the end we were on some of the details." — Fernando Cornago, VP Digital Tech

**Their journey to "Release Fitness":**

1. Asked three stability questions: How do we detect interruptions fast? Fix them fast? Prevent them from reaching production?
2. Brought in ITIL and SRE practices
3. Discovered that "everything is connected" — interruptions crossed product boundaries
4. Developed **"%revenue bleed versus net sales"** KPI — measuring business impact of outages
5. Created **Release Fitness dashboard** checking three angles per release:
   - **System level:** How is my product doing?
   - **Value stream:** Upstream/downstream dependencies
   - **Environment:** Platform health, events (hype drop days), error budgets

**Implementation evolution:** Started as Excel spreadsheet (teams fill out before each release) → too tedious → automated dashboard giving clear go/no-go.

**Result:** Self-adjusting, self-regulating system. Strict release guidelines BUT automated checks and error budgets telling any developer if they can deploy. **No more three VPs in a room.** Massively reduced onboarding time for ~100 new engineers per month.

> **[Insight]** The Adidas case study is a perfect illustration of evolving from heavyweight to lightweight change management. Phase 1: crisis → humans in a room approving everything (doesn't scale). Phase 2: spreadsheet checklist (doesn't sustain). Phase 3: automated dashboard with error budgets (scales and self-regulates). The final state is not "no controls" — it's "automated, risk-proportional controls that enable fast flow." The error budget concept (from SRE) is the key innovation: teams have quantified allowance for risk, and the system automatically adjusts behavior when the budget is low.

> **[2024+ Context]** Adidas's "Release Fitness" approach has parallels in the broader **Platform Engineering** movement. Tools like **OpsLevel**, **Cortex**, and **Port** provide automated "service scorecards" that evaluate deployment readiness across multiple dimensions (test coverage, security scanning, documentation, dependency freshness). The DORA team's concept of **"capabilities"** that predict performance aligns with this: rather than checking a box on a form, verify that the capabilities (automated testing, monitoring, rollback) are actually in place. **Backstage** service catalog plugins can surface this information at deployment time.

---

## Enable Coordination and Scheduling of Changes

- **Loosely coupled architectures** reduce coordination needs — teams make changes with high autonomy
- Even in loosely coupled systems, hundreds of daily deploys may create collision risks (e.g., simultaneous A/B tests) → use **chat rooms** to announce changes and find collisions
- More tightly coupled architectures may need deliberate scheduling — representatives meet to **sequence changes** (not authorize them)
- Global infrastructure changes (core network switches) always carry higher risk → require technical countermeasures (redundancy, failover, testing, simulation)

---

## Enable Peer Review of Changes

Instead of external approval bodies, require **peer reviews** — engineers close to the work scrutinize changes. Applicable to application code, environments, servers, networking, databases.

**Review requirements should scale with risk:**
- Fellow engineer review for normal changes
- Subject matter expert (security, database) for higher-risk areas
- Multiple reviews ("+2") for business-critical components with poor test coverage

**Small batch sizes apply to reviews too:**

> "There is a non-linear relationship between the size of the change and the potential risk of integrating that change — when you go from a ten line code change to a one hundred line code, the risk of something going wrong is more than ten times higher." — Randy Shoup

> "Ask a programmer to review ten lines of code, he'll find ten issues. Ask him to do five hundred lines, and he'll say it looks good." — Giray Özil

**Code review guidelines:**
- Everyone must have their changes reviewed before committing to trunk
- Monitor commit stream of fellow team members for potential conflicts
- Define which changes qualify as high-risk requiring SME review
- Changes too large to reason about easily should be split into smaller changes

**Code review forms:** Pair programming, over-the-shoulder, email pass-around, tool-assisted (Gerrit, GitHub PRs)

> **[Deep Dive: The Non-Linear Risk of Change Size]**
>
> Shoup's observation deserves emphasis with a concrete illustration:
>
> | Change Size | Lines Changed | Review Effort | Defect Detection Rate | Risk |
> |-------------|--------------|---------------|----------------------|------|
> | Small | 10-50 lines | 10-15 minutes | High (~85%) | Low |
> | Medium | 50-200 lines | 30-60 minutes | Moderate (~60%) | Medium |
> | Large | 200-500 lines | 2-4 hours | Low (~40%) | High |
> | Very Large | 500+ lines | Days (often deferred) | Very Low (~20%) | Very High |
>
> The implication: PR size is one of the most actionable levers for improving code quality. Many teams set hard limits (e.g., <400 lines per PR) and invest in tooling that flags oversized PRs.

### Case Study: Code Reviews at Google (2010)

In 2016, Google's 25,000 developers committed **16,000 changes into trunk per workday**, plus 24,000 automated changes per day.

Mandatory code reviews cover:
- Code readability for languages (enforces style guide)
- Ownership assignments for code sub-trees
- Code transparency and contributions across teams

![Figure 18.2: Size of Change vs. Lead Time for Reviews at Google](../images/Fig18-2.jpg)
*Source: Ashish Kumar, "Development at the Speed and Scale of Google," QCon 2010.*

The chart shows: larger changes require longer review lead times. Upper-left data points = complex, risky changes requiring more deliberation.

**Randy Shoup's personal lesson:** Submitted a ~3,000-line change for review. The reviewer spent days going through it and said: "Please don't do that to me again." Shoup learned to make code reviews part of daily work in small increments.

### Potential Dangers of More Manual Testing and Change Freezes

When testing failures occur, the typical reaction is "do more testing." But if we're adding manual testing at the end of the project:
- Manual testing is slower and more tedious
- "Additional testing" takes significantly longer
- Deploying less frequently → batch size increases
- Larger batch sizes → change success rates go down, incidents and MTTR go up

**Instead:** Fully integrate testing into daily work as part of smooth, continual flow. Build in quality. Test, deploy, and release in ever smaller batch sizes.

> **[Insight]** Change freezes deserve special criticism. The logic seems sound: "Stop all changes during the critical period to reduce risk." But the data consistently shows that change freezes *increase* risk: they create a dam of accumulated changes that all flood out after the freeze ends, creating the largest, riskiest batch of the year. They also send the message that changes are inherently dangerous — reinforcing the fear culture the Third Way aims to eliminate. Adidas's story illustrates the evolution: from change freezes → to three VPs approving everything → to automated release fitness. Each step moved away from "stop changes" toward "make changes safe."

---

## Enable Pair Programming to Improve All Our Changes

Pair programming: two engineers at one workstation. One **drives** (writes code), the other **navigates** (reviews, considers strategic direction, catches problems). Skills transfer automatically.

Another pattern: one engineer writes the test, the other writes the implementation (reinforces TDD).

> "I can't help wondering if pair programming is nothing more than code review on steroids. The advantage of pair programming is its gripping immediacy: it is impossible to ignore the reviewer when he or she is sitting right next to you." — Jeff Atwood, co-founder of Stack Exchange

**Dr. Laurie Williams' 2001 study:**
- Paired programmers are **15% slower** than two independent individuals
- But "error-free" code increased from **70% to 85%**
- Since testing and debugging cost many times more than initial programming → net positive
- Pairs consider more design alternatives, arrive at simpler, more maintainable designs
- Catch design defects early
- **96%** of respondents enjoyed pair programming more than solo work

### Case Study: Pair Programming Replacing Broken Code Review at Pivotal Labs (2011)

**Elisabeth Hendrickson** (VP of Engineering, Pivotal) described how their Gerrit code review process was broken:
- Reviews took an **entire week**
- Only senior engineers could "+1" changes
- Senior engineers had many other responsibilities and "often didn't care as much about the fixes the more junior developers were working on"

> "The only people who had the ability to '+1' the changes were senior engineers... It created a terrible situation — while you were waiting for your changes to get reviewed, other developers were checking in their changes. So for a week, you would have to merge all their code changes onto your laptop, re-run all the tests..." — Hendrickson

**Solution:** Dismantled Gerrit code review entirely. Required pair programming instead. Reduced review time from **weeks to hours.**

> "Code reviews work fine in many organizations, but it requires a culture that values reviewing code as highly as it values writing the code in the first place." — Hendrickson

> **[Insight]** The Pivotal case study reveals a critical failure mode of code review: when reviewing is treated as a second-class activity. If reviewing code isn't valued (in terms of recognition, performance reviews, time allocation) as much as writing code, review queues grow, feedback slows, and the process degrades into rubber-stamping. Pair programming sidesteps this entirely because the review is embedded in the act of creation. The tradeoff is the 15% overhead — but as Williams showed, the defect reduction pays for itself many times over.

### Evaluating the Effectiveness of Pull Request Processes

**Ryan Tomayko** (CIO, co-founder of GitHub, co-inventor of the pull request) on what makes a good PR:

**Bad PR:** "Fixing issue #3616 and #3841." — No @mentions, no explanation, no context.

**Good PR elements:**
- Sufficient detail on **why** the change is being made
- **How** the change was made
- Identified **risks** and resulting **countermeasures**
- Good discussion enabled by context — additional risks pointed out, better implementation ideas, risk mitigation suggestions
- If something bad happens on deployment → added to PR with link to post-mortem
- Discussion without blame; candid conversation on preventing recurrence

> **[2024+ Context]** PR best practices have been formalized into tooling:
> - **PR templates** (GitHub, GitLab) enforce structure: what changed, why, testing done, risks
> - **PR size checkers** (Danger, PullApprove) warn when PRs exceed size thresholds
> - **CODEOWNERS files** auto-assign reviewers based on changed file paths
> - **Required status checks** ensure CI passes before merge
> - Google's research published in *Software Engineering at Google* (2020) found that code review is one of the most impactful quality practices — but only when review cycle time is kept under 24 hours. Beyond that, the value degrades rapidly.

---

## Fearlessly Cut Bureaucratic Processes

> "A great metric to publish widely is how many meetings and work tickets are mandatory to perform a release — the goal is to relentlessly reduce the effort required." — Adrian Cockcroft

**Examples:**
- **Capital One "Got Goo?"** — dedicated team removing tools, processes, and approvals that impede work (Dr. Tapabrata Pal)
- **Disney "Join the Rebellion"** — program to remove toil and obstacles from daily work (Jason Cox)
- **Target TEAP-LARB dismantling** — Heather Mickman investigated why the technology approval process existed. Applied the "five whys." Discovered **no one knew** why it existed, beyond a vague notion of governance after some forgotten disaster. Mickman took responsibility for her technology choices and dismantled the process. Cassandra was successfully introduced and widely adopted. She received the **"Lifetime Achievement Award for removing barriers to get technology work done."**

> **[Insight]** The Target TEAP-LARB story is included for a specific reason: it illustrates that many approval processes in large organizations are **zombie processes** — they were created in response to a specific incident, but the incident has been forgotten, the context has changed, and the process lives on purely through inertia. Mickman's "five whys" approach is the recommended diagnostic: keep asking "why does this process exist?" until you either find a compelling current reason (keep it) or discover that no one remembers (remove it). Every organization has TEAP-LARBs hiding in their value stream.

---

## Conclusion

> John Allspaw, to a newly hired junior engineer asking permission to deploy a small HTML change: "I don't know, is it? Did you have someone review your change? Do you know who the best person to ask is for changes of this type? Did you do everything you absolutely could to assure yourself that this change operates in production as designed? If you did, then don't ask me — just make the change!"

Creating conditions where change implementers **fully own the quality of their changes** is essential to high-trust, generative culture. Not "no controls" — but controls through peer review, automated testing, and telemetry rather than distant approval boards.

---

## How Generative AI Is Reshaping Review and Coordination

> **[GenAI + DevOps]**

**AI-Assisted Code Review:** AI tools (GitHub Copilot code review, CodeRabbit, Sourcery, Amazon CodeGuru) can perform automated first-pass code reviews — catching style violations, potential bugs, security issues, and performance problems before a human reviewer sees the code. This addresses the Pivotal Labs problem: the queue for human review shrinks because AI handles the mechanical review, freeing humans for the judgment-intensive review.

**AI-Generated PR Descriptions:** AI can auto-generate PR descriptions from diffs — the "why" and "what" that Tomayko says good PRs need. This lowers the barrier to well-documented PRs, especially for less experienced engineers.

**AI and Change Risk Assessment:** AI can analyze the risk profile of a change (files touched, test coverage, blast radius, historical failure patterns for similar changes) and route it to the appropriate review level — small, well-tested changes get lightweight review, while large changes to critical paths get extra scrutiny. This implements risk-proportional review automatically.

**AI and Pair Programming:** AI coding assistants (Copilot, Claude, Cursor) function as an always-available pair programming partner — the "navigator" that reviews code as it's written, suggests alternatives, and catches defects in real-time. Dr. Williams' finding that pairing increases error-free code from 70% to 85% may be further improved with AI as the constant navigator.

**The key tension:** AI can handle mechanical review (syntax, style, known patterns) but cannot yet evaluate architectural appropriateness, business logic correctness, or organizational context. Human peer review remains essential for judgment calls. The most effective model is **AI + Human** — AI as first pass, human for judgment.

**Further reading:**
- [Google Engineering Practices — Code Review](https://google.github.io/eng-practices/review/) — Google's public code review guidelines
- [GitHub Copilot Code Review](https://github.blog/changelog/2024-10-29-copilot-code-review-in-github-com-public-preview/) — AI-assisted review in PRs
- [Conventional Comments](https://conventionalcomments.org/) — structured format for review feedback
- [Software Engineering at Google — Code Review Chapter](https://abseil.io/resources/swe-book/html/ch09.html) — comprehensive treatment of review at scale
