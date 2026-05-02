# Chapter 5: Managing a Team — Part 2

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 2 covers:** How to drive good decisions and conflict management (the Good Manager, Bad Manager section).
See [Part 1](ch05-notes-managing-a-team-part1.md) for: staying technical, debugging dysfunctional teams, the shield, managing former peers.
See [Part 3](ch05-notes-managing-a-team-part3.md) for: team cohesion destroyers, advanced project management, joining a small team, chapter assessment.

## Table of Contents — Part 2

- [How to Drive Good Decisions](#how-to-drive-good-decisions)
  - [Create a Data-Driven Team Culture](#create-a-data-driven-team-culture)
  - [Flex Your Own Product Muscles](#flex-your-own-product-muscles)
  - [Look into the Future](#look-into-the-future)
  - [Review the Outcome of Your Decisions and Projects](#review-the-outcome-of-your-decisions-and-projects)
  - [Run Retrospectives for the Processes and Day-to-Day](#run-retrospectives-for-the-processes-and-day-to-day)
- [Good Manager, Bad Manager: Conflict Avoider, Conflict Tamer](#good-manager-bad-manager-conflict-avoider-conflict-tamer)
  - [The Dos and Don'ts of Managing Conflict](#the-dos-and-donts-of-managing-conflict)

**Block types in Part 2:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [Influence Without Authority] [Go Deeper]

---

## How to Drive Good Decisions

Fournier sets up the decision-making landscape: the product manager owns the product roadmap, the tech lead owns technical details, but **the engineering manager is accountable for progress through both.** "The nature of leadership is that, while you may only have the authority to guide decisions rather than dictate them, you'll still be judged by how well those decisions turn out."

> **[Insight]** This is one of the most important sentences in the book. Read it again: *you'll be judged by how well those decisions turn out.* Not by how well you facilitated the process. Not by how inclusive you were. Not by how much consensus you built. By the *outcome.* This is the uncomfortable truth of management: you're accountable for results you don't fully control. The product manager makes a bad market call — your team builds the wrong thing — you're on the hook. The tech lead picks an architecture that doesn't scale — you're on the hook. This isn't fair, but it's real. The implication: you must be engaged enough in both product and technical decisions to influence them, even when you don't own them. Passive managers who "let the experts decide" often end up accountable for decisions they never examined.

> **[Senior EM vs. Director: Decision-Making Scope]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Product decisions** | Partners with one PM; influences scope and priorities for your teams | Partners with product leadership; influences strategy across multiple product areas |
> | **Technical decisions** | Guides architecture for your teams; holds TLs accountable | Sets technical direction across teams; approves major architectural bets |
> | **People decisions** | Hiring, firing, promotion for your direct reports | Organizational design, headcount allocation, succession planning |
> | **Resource decisions** | Manages capacity within your teams | Allocates resources across teams; makes build-vs-buy-vs-partner decisions |
> | **What you're judged on** | Team execution: did you ship what you committed to? | Organizational outcomes: did the right things get built, by the right teams, at the right time? |

### Create a Data-Driven Team Culture

Fournier recommends augmenting the product/business data that product managers already use with **engineering efficiency and quality data:**
- Time it takes to complete features
- Time spent dealing with outages
- Number of bugs found in QA or after releases

These data points can justify both product and technical decisions.

> **[SRE Lens: The Data Advantage SRE Managers Have]**
>
> SRE teams sit on a goldmine of decision-making data that most feature teams don't have:
>
> - **Incident data:** Frequency, severity, MTTR, root cause categories, affected services. This tells you where to invest in reliability.
> - **SLO/SLI data:** Which services are burning error budget? Which are comfortably within bounds? This tells you where reliability investment is needed vs. wasted.
> - **On-call burden data:** Pages per rotation, after-hours pages, time-to-acknowledge, escalation rate. This tells you about team health and operational quality.
> - **Toil metrics:** What percentage of team time goes to repetitive manual work? Which tasks are most common? This tells you where automation has the highest ROI.
> - **Deployment metrics (DORA):** Deployment frequency, lead time, change failure rate, MTTR. This tells you about the health of the entire engineering pipeline.
> - **Cost data:** Infrastructure spend per service, cost-per-request, capacity utilization. This tells you about efficiency.
>
> **The Senior EM move:** Don't just collect this data — *use it to influence decisions.* When product wants to launch a new feature on a service that's already burning its error budget, the data makes the case: "This service has had 3 SLO violations in the last quarter. Adding load from this feature will increase incident risk. Let's invest 2 sprints in stability first, then launch the feature on solid ground."
>
> **The Director move:** Aggregate this data across teams to tell organizational stories. "Our top 3 incident-producing services account for 60% of all on-call burden. Targeted investment in these 3 services would free up the equivalent of 2 full-time engineers for project work across the org."

> **[Leader's Playbook: Building a Data-Driven Decision Culture]**
>
> 1. **Start with a team dashboard.** One page, visible to everyone: deployment frequency, incident count, SLO status, sprint completion rate, on-call burden. Update weekly. If you can't build a dashboard, a shared spreadsheet works.
> 2. **Reference data in every planning conversation.** "Last quarter, we spent 30% of capacity on incident response. This quarter, I want that to be 20%. Here's how." Data should be a natural part of the conversation, not a special presentation.
> 3. **Make data part of project proposals.** When someone proposes a project, require: what problem does this solve? How do we measure success? What does the data currently show? What should the data show after?
> 4. **Review data together.** Monthly team meeting: review the dashboard, discuss trends, identify anomalies. This builds shared awareness and shared language.
> 5. **Celebrate data-driven wins.** "We invested in the deployment pipeline last quarter. Result: deployment time went from 4 hours to 20 minutes, and deployment frequency increased from weekly to daily."
>
> **What NOT to do:** Don't weaponize data. Data should inform decisions, not punish people. "Your sprint velocity dropped 20% — what's wrong with you?" is toxic. "Our velocity dropped 20% — let's understand why and whether it matters" is healthy.

### Flex Your Own Product Muscles

Fournier argues that engineering managers should develop product sense: understand your customer, whether that's an external user, internal engineers using your tools, or a support team. **"Taking the time to develop customer empathy is important because you'll need to give your engineers context for their work."**

Customer empathy also helps you figure out "which areas of the technology have the greatest direct impact on your customers, and that understanding will guide where you invest engineering effort."

> **[SRE Lens: Who Is Your Customer?]**
>
> SRE teams often struggle with this question because they have multiple customers:
>
> - **End users** (indirectly) — they experience the reliability your team enables
> - **Product engineering teams** — they use your platform, tools, and on-call support
> - **The business** — they depend on uptime for revenue
> - **Your own team** — internal tooling quality affects their productivity and happiness
>
> **The mistake:** Treating "the system" as your customer instead of the humans who depend on the system. An SRE team that obsesses over uptime numbers without understanding *which* downtime matters to *which* customers will optimize for the wrong things.
>
> **Practical customer empathy for SRE:**
> - Talk to customer support. Ask: "What reliability problems do customers complain about most?" The answer is rarely what you'd expect from looking at dashboards alone.
> - Shadow a product engineer for a day. Feel their deployment experience, their debugging workflow, their interaction with your tools.
> - Read customer-facing incident communications. Do they accurately represent what happened? Does the tone match the impact?
> - Attend a product team's sprint demo. See what they're building and how it depends on your infrastructure.

> **[Cross-Functional Play: Product Sense as a Career Accelerator]**
>
> For a Senior EM aiming at Director, product sense is a differentiator. Most SRE managers can articulate technical strategy. Far fewer can articulate how their technical strategy connects to business outcomes.
>
> **The test:** Can you explain your team's current top project to the VP of Product in language they care about? Not "we're migrating from Prometheus to Thanos for better multi-cluster aggregation" but "we're improving our monitoring infrastructure so product teams can detect and fix customer-impacting issues 3x faster, which directly supports the customer experience goals in this quarter's OKRs."
>
> If you can't make that translation, your product muscles need work.

### Look into the Future

Fournier says you need to "think two steps ahead, from a product and technology perspective." Understanding where the product roadmap is heading helps you guide the technical roadmap. She gives examples: rewriting checkout to support new payment types, moving to a new framework to support streaming data.

> **[Deep Dive: Two Steps Ahead in SRE]**
>
> For SRE managers, "looking into the future" means:
>
> **Product-informed reliability planning:**
> - If the product team is planning a 10x user growth initiative, you need to be capacity planning NOW — not after the launch.
> - If the company is expanding to new geographic regions, you need to understand data residency and latency requirements months before the feature work starts.
> - If a major new feature will change traffic patterns (e.g., real-time streaming instead of batch), your monitoring and scaling assumptions need to evolve.
>
> **Technology trend awareness:**
> - Is your company moving to Kubernetes? Your team needs container expertise before the migration, not during.
> - Is the industry shifting to platform engineering models? How does that affect SRE's role and value proposition?
> - Are AI/ML workloads growing? They have fundamentally different reliability characteristics (GPU dependencies, model serving latency, data pipeline failures).
>
> **The actionable habit:** Every quarter, have a "what's coming" conversation with your product counterpart and your peer engineering managers. Ask: "What's on your roadmap for next quarter that might change our operational landscape?" Then plan accordingly.

> **[Mental Model: Wardley Mapping for Technical Strategy]**
>
> Simon Wardley's mapping framework helps you think about where to invest by plotting components along an evolution axis:
>
> - **Genesis** → **Custom-Built** → **Product** → **Commodity**
>
> Components at different stages need different management:
> - **Genesis** (novel, uncertain): Your experimental new observability approach. Invest in exploration, tolerate failure.
> - **Custom-Built** (differentiated, but known): Your bespoke deployment pipeline. Invest in quality, but question whether it should stay custom.
> - **Product** (available from vendors): Monitoring tools, incident management platforms. Evaluate build-vs-buy seriously.
> - **Commodity** (utility, undifferentiated): Compute, storage, DNS. Don't invest engineering effort here — use cloud services.
>
> **For SRE managers:** Map your team's systems along this axis. Are you spending engineering time on commodity problems? Are you building custom solutions where a product would suffice? This framework helps you make "where to invest" decisions that Fournier describes.
>
> **[Go Deeper]** Simon Wardley's *Wardley Maps* (free online book) and his video talks on YouTube.

### Review the Outcome of Your Decisions and Projects

Fournier advocates for a habit most teams skip: **going back and checking whether your hypotheses were right.** Did the rewrite make the team faster? Did the new feature change customer behavior as predicted? What did A/B tests reveal?

> **[Anti-Pattern: Ship It and Forget It]**
>
> Your team completes a 3-month reliability project: a complete rewrite of the alerting pipeline. The team is relieved it's done. The product manager has a backlog of features waiting. Everyone moves on to the next thing.
>
> Six months later, someone asks: "Did the alerting rewrite actually improve things?" No one knows. No one measured. The dashboard that was supposed to track improvement was never built. The team has a vague sense that "things are better" but no data.
>
> **Why this matters:** Without outcome review, you can't learn. Was the rewrite the right investment? Or would targeted fixes have achieved 80% of the benefit at 20% of the cost? Without data, you'll keep making the same investment decisions — maybe right, maybe wrong — without ever improving your judgment.
>
> **The fix:** Before starting any significant project, define the success criteria and how you'll measure them. After the project ships, schedule a 30-day and 90-day review. Put it on the calendar during planning, not after shipping.

> **[Leader's Playbook: The Project Outcome Review]**
>
> **Before the project (define during planning):**
> - What hypothesis are we testing? ("Rewriting the alerting pipeline will reduce MTTD from 12 minutes to under 5 minutes")
> - How will we measure it? ("MTTD metric from incident tracker, averaged over 90 days post-launch vs. 90 days pre-launch")
> - What's the expected timeline for results? ("Full impact visible after 90 days of data")
>
> **30 days after shipping:**
> - Are we seeing early signals in the right direction?
> - Any unexpected side effects?
> - Anything we need to adjust?
>
> **90 days after shipping:**
> - Did we hit our success criteria?
> - What was the actual cost vs. estimated cost?
> - What did we learn that changes how we'd approach a similar project?
> - Share findings with the team and stakeholders.
>
> **The meta-benefit:** Over time, outcome reviews calibrate your estimation instincts. You learn which types of projects consistently deliver value and which don't. This is how you develop the strategic judgment that differentiates a Director from a Senior EM.

### Run Retrospectives for the Processes and Day-to-Day

Fournier recommends regular process retrospectives (whether you use agile or not) to detect patterns in how the team operates: "Is the team feeling good about how they get requirements? Do they feel good about the code quality?"

She describes this as "more subjective than gathering data about the team's health, but it's arguably even more valuable than many objective measures, because it comes from the things the team itself is noticing."

> **[SRE Lens: Retros Beyond Sprint Retros]**
>
> SRE teams should run retros at multiple cadences:
>
> **Sprint/iteration retro (every 2 weeks):** Standard agile retro for project work. What went well, what didn't, what to change.
>
> **On-call retro (every rotation or monthly):** Separate from sprint retro. Focused on: incident trends, on-call burden, tooling pain points, runbook gaps. The on-call engineer who just finished rotation leads.
>
> **Quarterly reliability review:** Step back and look at the bigger picture. SLO trends, incident patterns, toil metrics, team capacity allocation. Are we investing in the right things?
>
> **Post-incident reviews (per incident):** Already standard in SRE. But ensure these feed into the broader retro — individual incident learnings should aggregate into systemic improvements.
>
> **The common failure:** Running retros but never acting on the outcomes. If the same action item appears in 3 consecutive retros, you have a credibility problem. Either fix it or explain why it can't be fixed right now.

> **[Interview Angle]**
>
> "How do you make decisions as a manager?" is a common Director-level interview question. Fournier's four pillars — data-driven culture, product sense, future thinking, outcome review — give you a complete framework.
>
> Strong answer structure:
> - **Data:** "I ensure our decisions are grounded in data — team metrics, customer data, operational signals. For example, when deciding between two projects last quarter, I used incident trend data to show that one would have 3x the customer impact."
> - **Product sense:** "I develop a deep understanding of our customers and how our technical work connects to their experience. I regularly talk to [product managers / support teams / end users]."
> - **Forward-looking:** "I think two quarters ahead. I work closely with product leadership to understand where the roadmap is going, so our technical investments are ahead of demand rather than reactive."
> - **Outcome review:** "I close the loop on every significant project. We define success criteria upfront and measure outcomes at 30 and 90 days. This has calibrated my team's estimation accuracy significantly."
>
> **Director-level elevation:** Add "I've built these as team practices, not just personal habits. My teams run outcome reviews and data-driven planning without me driving it."

---

## Good Manager, Bad Manager: Conflict Avoider, Conflict Tamer

Fournier tells two contrasting stories:

**Jason (conflict avoider):** His team is overworked. Charles has been working on a pet project for months while the team needs him on the rewrite. Instead of addressing it directly, Jason calls a team vote — the team predictably votes to drop Charles's project. Charles is blindsided. Jason also never says no to new projects and doesn't ask for more people. "Jason is cool, everyone agrees, but it is so hard to get him to actually act on resolving conflicts or making difficult decisions."

**Lydia (conflict tamer):** Same situation — overworked team, someone on a pet project. She tells Charles directly that priorities have changed and the team needs him. "Charles is unhappy, and Lydia doesn't enjoy this conversation, but she knows that as the manager of the team, she's responsible for making sure they're focused on the most important projects." She also makes sure the team understands WHY they took on a big project, guides them through technology disagreements using structured feedback, and pushes for more people.

> **[Insight]** Jason and Lydia illustrate Fournier's sharpest management insight in this chapter: **democracy is not leadership.** Jason's voting approach FEELS empowering and fair. But it's actually an abdication. He used the team to deliver a message he was too afraid to deliver himself, and the result was crueler than a direct conversation would have been — Charles was publicly voted down by his own teammates. Lydia's direct conversation was uncomfortable but respectful. She treated Charles as an adult, explained the situation, and made the call. The team describes her as "tough but fair" — the highest compliment a manager can receive.

> **[Mental Model: The RACI for Decisions]**
>
> Fournier's Jason/Lydia contrast reveals a common confusion about decision-making roles. The RACI framework clarifies:
>
> - **R (Responsible):** Does the work. (Charles — implements the rewrite)
> - **A (Accountable):** Makes the final call. (Lydia — decides what the team works on)
> - **C (Consulted):** Provides input before the decision. (The team — shares perspective on priorities)
> - **I (Informed):** Told about the decision after it's made. (Stakeholders — learn the new plan)
>
> **Jason's mistake:** He put the team in the A role (voting = deciding) when it should have been his. The team should have been C (consulted for input), and he should have been A (made the call, owned the consequence).
>
> **When voting IS appropriate:** Low-stakes, reversible decisions where the team genuinely has equal stake and expertise. "Should our team retro be Monday or Friday?" "Which conference should we submit a talk to?" NOT: "Should we cancel a colleague's project?"

> **[Scenario: The SRE Priority Conflict]**
>
> Your SRE team of 6 supports 3 product teams. Product Team A has a critical launch in 4 weeks and wants dedicated SRE support. Product Team B has an ongoing reliability problem with incident rate 3x the target. Product Team C wants to onboard a new service. You don't have capacity for all three.
>
> **The Jason approach (conflict avoidance):**
> You try to do all three. You tell each product team "we'll try our best." You don't communicate the tradeoff. Two engineers burn out trying to context-switch between all three. The launch is poorly supported, the reliability problem persists, and the onboarding drags on for months. All three product teams are frustrated.
>
> **The Lydia approach (conflict taming):**
> You assess the situation, make a call, and communicate it directly:
>
> *"Here's our situation: we have 3 requests and capacity for 1.5 of them. Here's how I'm prioritizing:*
>
> *Priority 1: Product Team B's reliability problem. Incident rate is 3x target, and every incident costs us [X hours] and the business [$Y]. Two engineers on this for 4 weeks.*
>
> *Priority 2: Product Team A's launch. One engineer embedded with the team for launch support, focused on monitoring, rollback plan, and load testing. This is leaner than what they asked for, but it covers the critical risk.*
>
> *Priority 3 (deferred): Product Team C's onboarding. We'll start this after the launch and reliability work complete. I've communicated a revised timeline to them.*
>
> *I know this means saying 'not yet' to Team C and 'less than you wanted' to Team A. I've explained the tradeoffs to both teams. If anyone disagrees with this prioritization, I want to hear it now — but I've made this call based on risk and impact, and I'm confident it's the right one."*
>
> **Why this works:** Clear prioritization, transparent reasoning, direct communication, willingness to take heat for the decision.

> **[The Shadow Side: Conflict Taming Becomes Authoritarianism]**
>
> Lydia's approach — make the call, communicate directly, own the decision — is clearly better than Jason's. But the shadow side of decisive leadership is authoritarianism: making every decision yourself, shutting down dissent, and framing decisiveness as a virtue that excuses not listening.
>
> **How it manifests:**
> - You make decisions before consulting anyone, then "communicate" them as fait accompli
> - When team members push back, you interpret it as "not being aligned" rather than legitimate disagreement
> - You develop a reputation for being "decisive" — but your team stops offering input because they know the decision is already made
> - You move fast, but your team feels no ownership of the direction
>
> **The test:** After you make a decision, ask: "Did I consult the people who had relevant information before deciding? Could someone on my team have changed my mind with the right argument?" If the answer to both is no, you've crossed from decisive to autocratic.
>
> **Fournier's balance:** Lydia *consults* the team ("guides them through their disagreements... by following a structure for presenting options and soliciting feedback") AND makes the call when needed. She doesn't abdicate like Jason, but she doesn't dictate either.

### The Dos and Don'ts of Managing Conflict

Fournier provides a detailed list of conflict management principles. Here they are with commentary:

**Don't rely exclusively on consensus or voting.** Consensus requires that everyone has equal stake, equal knowledge, and is impartial. These conditions "are rarely met on teams where each person has different levels of expertise and different roles." The Charles vote was "downright cruel" — don't outsource hard conversations to group processes.

**Do set up clear processes to depersonalize decisions.** When allowing group decisions, establish shared standards: goals, risks, questions to answer. Assign decision ownership clearly. "Make it clear which members of the team should be consulted for feedback and who needs to be informed."

> **[Leader's Playbook: A Decision-Making Framework for Your Team]**
>
> Building on Fournier's advice, establish this for your team:
>
> **For every significant decision, define:**
> 1. **Decision owner:** Who makes the final call? (Usually one person, not a committee)
> 2. **Consulted parties:** Who has expertise or stake and should provide input? By when?
> 3. **Decision criteria:** What factors should be weighed? (Customer impact? Cost? Time? Technical risk?)
> 4. **Deadline:** When must this be decided? (Prevents analysis paralysis)
> 5. **Communication plan:** Who needs to know the outcome, and how?
>
> **For SRE-specific decisions, common templates:**
> - **Technology choice (e.g., new monitoring tool):** Decision owner = tech lead. Consulted = team (via RFC + time-boxed feedback period). Criteria = operability, cost, integration, learning curve. Deadline = 2 weeks from RFC.
> - **Priority change (e.g., shifting to reliability work):** Decision owner = you (the EM). Consulted = tech lead + product partners. Criteria = risk, customer impact, team capacity. Deadline = within the sprint.
> - **On-call policy change:** Decision owner = you. Consulted = the entire team (this affects everyone's quality of life). Criteria = fairness, burden distribution, coverage. Deadline = decided within 1 week, implemented next rotation.

**Don't turn a blind eye to simmering issues.** "If you're giving negative feedback in the course of a performance review, it shouldn't be a major surprise to your employee." If you learn about problems only during review season from peer feedback, "that's not a good sign. It's probably an indication that you are not paying attention."

**Do address issues without courting drama.** Key questions: "Is this an ongoing problem? Is it something you've personally noticed? Is this something many people on the team are struggling with? Is there a power dynamic or potential bias at play?" The goal is resolving team effectiveness problems, not becoming the team's therapist.

> **[Red Flags: You're Avoiding Conflict]**
>
> - You know about a problem between two team members and your plan is "let's see if it resolves itself"
> - You've given vague feedback ("maybe think about being more collaborative") instead of specific ("in yesterday's meeting, you interrupted Priya three times — that needs to stop")
> - You learn about issues for the first time during performance reviews
> - You have a team member whose behavior is a known problem, and your response has been "they're just like that"
> - You find yourself complaining about a team member to your manager or peers but haven't addressed it with the person directly
> - When two team members disagree, you avoid the room rather than facilitating resolution

**Don't take it out on other teams.** Fournier identifies an ironic pattern: conflict-avoidant managers INTERNALLY often become aggressive EXTERNALLY. They overidentify with their team and blame other teams for problems. She quotes a manager who realized: *"I was not telling my people the 10% of things they needed to be improving because I was afraid they would miss the message about the 90% of things that were good, and so I took that desire for accountability out on other teams."*

> **[Insight]** This is a devastatingly accurate observation. Watch for it in yourself. If you find yourself being more aggressive with other teams' managers than you are with your own team about their issues, you may be displacing internal conflict avoidance onto external targets. The other teams become a safe outlet for the accountability you're afraid to exercise at home. In SRE, this shows up as the team that's harsh in incident reviews toward other teams' code quality but soft on their own operational gaps.

**Do remember to be kind.** Fournier draws a critical distinction: **nice vs. kind.** "Nice is the language of polite society... But as a manager, you will have relationships that go deeper, and it's more important to be kind." Kind = telling someone they're not ready for promotion AND showing them what they need to do. Unkind = leading them on with "maybe" and watching them fail.

> **[Script: Being Kind, Not Nice]**
>
> Your senior SRE has been asking about promotion to Staff for 6 months. They're not ready — strong technically but weak on cross-team influence and mentorship. The "nice" response keeps deferring: "Keep doing what you're doing, we'll see next cycle."
>
> The kind response:
>
> *"I want to have an honest conversation about Staff promotion. You're one of the strongest technical engineers on the team — your incident response skills and system design work are genuinely Staff-level. But the Staff role at our company also requires demonstrated cross-team influence and developing others. Those are areas where I don't see enough evidence yet.*
>
> *Specifically: in the last two quarters, your work has been almost entirely within our team's boundary. For Staff, I need to see you driving technical decisions that affect other teams — like the observability standards work, or the cross-service SLO framework. And I need to see you actively mentoring — not just answering questions when asked, but proactively coaching someone on a skill they're developing.*
>
> *Here's what I'd like to propose: let's identify 2-3 specific opportunities in the next quarter for you to build evidence in these areas. I'll help create the opportunities. In 3 months, we'll reassess. Does this feel fair?"*
>
> **Why this is kind:** The person now knows exactly where they stand, what the gap is, and what to do about it. The "nice" alternative — vague encouragement — would waste another 6 months of their career.

**Don't be afraid.** "Conflict avoidance often arises from fear. We're scared of the responsibility of making the decision. We're afraid of seeming too demanding. We're afraid people will quit if we give them uncomfortable feedback."

**Do get curious.** Combat fear by interrogating your own motives: "Am I pushing this decision to the team because they really are the best people to decide, or am I just afraid that if I make an unpopular but necessary decision people will be mad at me?"

> **[Mental Model: The Avoidance Tax]**
>
> Every conflict you avoid doesn't disappear — it compounds. Think of it as technical debt for humans:
>
> - **Week 1:** Small interpersonal friction. 5-minute conversation to address. You avoid it.
> - **Month 1:** Friction has become a pattern. Other team members notice. Now it's a 30-minute conversation with specific examples needed.
> - **Month 3:** The affected person is disengaged. Others are resentful that you haven't acted. Now it's a formal performance conversation.
> - **Month 6:** The best team members have quietly started interviewing elsewhere because the culture feels broken. Now it's a retention crisis.
>
> **The avoidance tax:** Every week you delay, the cost of addressing the conflict increases. The 5-minute conversation in Week 1 would have cost you some discomfort. The retention crisis in Month 6 costs you months of recruiting, onboarding, and lost institutional knowledge.
>
> **For Senior EMs:** You pay the avoidance tax not just on your own conflicts but on your managers' conflicts too. If you see one of your managers avoiding a difficult conversation with their report, and you avoid telling them they need to have it... that's compound avoidance tax. The interest rate is brutal.

> **[Influence Without Authority: Managing Conflict Across Team Boundaries]**
>
> Fournier focuses on intra-team conflict, but SRE managers frequently face cross-team conflict where you have no authority over the other party.
>
> **Common SRE cross-team conflicts:**
> - A product team keeps deploying on Friday afternoons, causing weekend incidents for your on-call
> - A platform team changed an API without notice, causing cascading failures
> - A peer manager's team is chronically late on deliverables your team depends on
>
> **The conflict tamer's approach (adapted for cross-team):**
>
> 1. **Assume good intent first.** Maybe they don't know about the impact. Start with information sharing, not accusation.
> 2. **Use data, not emotion.** "Your Friday deployments correlated with 4 of our last 6 weekend incidents" is factual. "Your team keeps ruining our weekends" is adversarial.
> 3. **Propose a structural fix.** "What if we establish a deployment freeze after 2 PM on Fridays?" is better than "stop deploying on Fridays."
> 4. **Involve shared leadership only if needed.** Escalate with a problem brief and proposed solution, not a complaint.
> 5. **Don't weaponize incidents.** Using postmortems to assign blame to other teams destroys cross-team trust. Focus on systemic fixes, not finger-pointing.

---

*Continued in [Part 3](ch05-notes-managing-a-team-part3.md): Team Cohesion Destroyers, Advanced Project Management, Joining a Small Team, Chapter Assessment.*
