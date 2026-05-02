# Chapter 21: Reserve Time to Create Organizational Learning and Improvement

> **Part V — The Technical Practices of Continual Learning**

This chapter addresses the most practical and actionable dimension of the Third Way: deliberately reserving time for learning and improvement. While Chapter 19 established the cultural foundation (just culture, blameless retrospectives) and Chapter 20 provided the propagation mechanisms (ChatOps, shared repositories, codified standards), this chapter tackles the organizational discipline of actually allocating time for improvement work. Drawing from the Toyota Production System's improvement blitz (kaizen blitz), the chapter presents case studies from Target, Facebook, Google, Nationwide Insurance, and Capital One to demonstrate that organizations that dedicate structured time for paying down technical debt, teaching and learning, and community building consistently outperform those that treat improvement as something to do "when there's time" (which is never).

## Table of Contents

- [The Improvement Blitz (Kaizen Blitz)](#the-improvement-blitz-kaizen-blitz)
  - [Case Study: Thirty-Day Challenge at Target (2015)](#case-study-thirty-day-challenge-at-target-2015)
- [Institutionalize Rituals to Pay Down Technical Debt](#institutionalize-rituals-to-pay-down-technical-debt)
  - [Case Study: Facebook Hackathons and the HipHop Compiler](#case-study-facebook-hackathons-and-the-hiphop-compiler)
- [Enable Everyone to Teach and Learn](#enable-everyone-to-teach-and-learn)
  - [Teaching Thursday at Nationwide Insurance](#teaching-thursday-at-nationwide-insurance)
  - [Cross-Functional Skill Building](#cross-functional-skill-building)
  - [Case Study: ASREDS Learning Loop](#case-study-asreds-learning-loop)
- [Share Your Experiences from DevOps Conferences](#share-your-experiences-from-devops-conferences)
  - [DevOpsDays and DevOps Enterprise Summit](#devopsdays-and-devops-enterprise-summit)
  - [Case Study: Internal Technology Conferences at Nationwide, Capital One, and Target (2014)](#case-study-internal-technology-conferences-at-nationwide-capital-one-and-target-2014)
- [Create Community Structures to Spread Practices](#create-community-structures-to-spread-practices)
  - [Continuous Learning: DORA 2019 Findings on Community Structures](#continuous-learning-dora-2019-findings-on-community-structures)
  - [Case Study: Google's Testing Grouplet and Test Mercenaries](#case-study-googles-testing-grouplet-and-test-mercenaries)
    - [Testing on the Toilet (TotT)](#testing-on-the-toilet-tott)
    - [Test Certified (TC)](#test-certified-tc)
    - [Company-Wide Fixits](#company-wide-fixits)
- [Conclusion](#conclusion)
- [How Generative AI Is Reshaping Organizational Learning](#how-generative-ai-is-reshaping-organizational-learning)
  - [GenAI and Improvement Blitzes](#genai-and-improvement-blitzes)
  - [GenAI and Teaching/Learning](#genai-and-teachinglearning)
  - [GenAI and Community Structures](#genai-and-community-structures)
  - [The Meta-Question: Does AI Reduce the Need for Reserved Learning Time?](#the-meta-question-does-ai-reduce-the-need-for-reserved-learning-time)

---

## The Improvement Blitz (Kaizen Blitz)

The chapter opens with the Toyota Production System concept of the **improvement blitz** (or kaizen blitz) — "a dedicated and concentrated period of time to address a particular issue, often over the course of several days."

Dr. Steven Spear explains: **"blitzes often take this form: A group is gathered to focus intently on a process with problems. . . . The blitz lasts a few days, the objective is process improvement, and the means are the concentrated use of people from outside the process to advise those normally inside the process."**

The output of an improvement blitz is typically a new approach to solving a problem: new layouts of equipment, new means of conveying material and information, a more organized workspace, or standardized work. They may also leave behind a to-do list of changes to be made later.

> **[Deep Dive: Why Dedicated Time Matters — The Urgency Trap]**
>
> The need for dedicated, protected time for improvement work seems obvious, but it is constantly undermined by organizational dynamics. The pattern is universal:
>
> 1. Teams are fully loaded with feature work (100% utilization)
> 2. Technical debt accumulates because there is "no time" to address it
> 3. Technical debt slows down feature work, creating pressure to work harder
> 4. The team works harder on features, leaving even less time for improvement
> 5. Technical debt accumulates faster, feature velocity drops further
> 6. Goto step 3
>
> This is the "downward spiral" described in the book's introduction. The only way to break it is to **explicitly reserve time** for improvement work — not as a reward when there is slack, but as a non-negotiable investment.
>
> The analogy is physical maintenance: you do not wait until a bridge collapses to perform maintenance. You schedule regular inspections and repairs, accepting that the bridge will be partially closed during maintenance. Organizations that do not reserve time for technical improvement are operating bridges without maintenance schedules. The question is not whether the bridge will fail, but when.
>
> Research supports this: DORA consistently finds that teams that dedicate time to reducing technical debt have better delivery performance. The improvement time is not a cost — it is an investment with measurable returns in speed, stability, and team satisfaction.

### Case Study: Thirty-Day Challenge at Target (2015)

**Context:** Target's DevOps Dojo, also known as the Technology Innovation Center, occupies about eighteen thousand square feet of open office space where DevOps coaches help teams elevate their practice.

**The thirty-day challenge format:**
- Internal development teams come in for a month
- Work together with dedicated Dojo coaches and engineers
- Teams bring their actual work — the goal is to solve a real problem they have been struggling with
- Work in two-day sprints with planning, execution, and demos
- When complete, teams return to their lines of business with their solved problem and new learnings

Ross Clanton, former Director of Operations at Target: **"We currently have capacity to have eight teams doing 30-Day Challenges concurrently, so we are focused on the most strategic projects of the organization. So far, we've had some of our most critical capabilities come through the Dojo, including teams from Point Of Sale (POS), Inventory, Pricing, and Promotion."**

Ravi Pandey, a Target development manager: **"In the old days, we would have to wait six weeks to get a test environment. Now, we get it in minutes, and we're working side by side with Ops engineers who are helping us increase our productivity and building tooling for us to help us achieve our goals."**

Clanton: **"It is not uncommon for teams to achieve in days what would usually take them three to six months. So far, two hundred learners have come through the Dojo, having completed fourteen challenges."**

**Additional engagement models:**
- **Flash builds:** One- to three-day events focused on shipping an MVP or capability
- **Open labs:** Biweekly sessions where anyone can visit to talk to coaches, attend demos, or receive training

> **[Insight]** Target's Dojo model is notable for several reasons:
>
> 1. **Teams bring their real work.** This is not a training exercise disconnected from production. Teams solve actual problems they have been struggling with, which means the learning is immediately applicable and the business gets real value from the investment.
> 2. **The Dojo has dedicated, full-time staff.** This is not a volunteer or side-project effort. Target invested in permanent coaching capacity, signaling organizational commitment.
> 3. **The results are dramatic.** "Achieve in days what would usually take three to six months" is a 30-60x improvement in throughput. This kind of improvement is possible because the Dojo breaks teams out of their normal context — away from interruptions, meetings, and firefighting — and provides them with dedicated coaching and cross-functional support.
> 4. **The knowledge returns to the organization.** When teams go back to their lines of business, they bring their new practices with them — seeding improvement across the organization. This is the "local to global" mechanism from Chapter 20, implemented through people rather than through code.
>
> The Dojo model has been widely adopted. Similar programs exist at organizations including ING, Verizon, and Lowe's, often under names like "Engineering Excellence Lab," "DevOps Dojo," or "Platform Accelerator."

---

## Institutionalize Rituals to Pay Down Technical Debt

The chapter prescribes scheduling rituals that enforce the practice of reserving Dev and Ops time for improvement work. The easiest approach: **schedule day- or week-long improvement blitzes where everyone self-organizes to fix problems they care about — no feature work is allowed.**

Problems to address include: code, environment, architecture, tooling, and more. Teams span the entire value stream (Development, Operations, Infosec) and demonstrate their improvements to the rest of the company.

**Alternative terms for this practice:**
- Kaizen blitz / improvement blitz (Lean)
- Spring or fall cleanings
- Ticket queue inversion weeks
- Hack days / hackathons / 20% innovation time

> **[Deep Dive: Improvement Blitz vs. Hackathon — A Critical Distinction]**
>
> The chapter explicitly notes that "hack days" and "hackathons" sometimes focus on product innovation and prototyping new market ideas rather than improvement work, and worse, are often restricted to developers. The chapter's improvement blitz is deliberately different:
>
> | Dimension | Hackathon (as commonly practiced) | Improvement Blitz (as prescribed here) |
> |---|---|---|
> | **Focus** | New product ideas, prototypes | Fixing daily work problems, reducing technical debt |
> | **Participants** | Usually developers only | Dev, Ops, Infosec — entire value stream |
> | **Output** | Demos of prototypes (often never productionized) | Deployed improvements to actual systems |
> | **Measurement** | "Cool factor," audience voting | Reduction in unplanned work, faster deployments, fewer incidents |
> | **Motivation** | Innovation and fun | Reducing daily pain and frustration |
>
> Both have value, but they serve different purposes. The improvement blitz specifically targets the "downward spiral" of technical debt. Its power comes from empowering those closest to the work to identify and solve their own problems.

The chapter uses an evocative metaphor from Dr. Spear: a complex system is like a spider web, with intertwining strands constantly weakening and breaking. If the right combination breaks, the entire web collapses. **"No wonder then that spiders repair rips and tears in the web as they occur, not waiting for the failures to accumulate."**

> **[Insight]** The spider web metaphor perfectly captures why command-and-control management cannot solve the technical debt problem. In a complex system, the number of potential failure points is too large and too distributed for any centralized authority to track and prioritize. Only the people closest to the work — the engineers who feel the daily pain of workarounds, slow builds, flaky tests, and brittle infrastructure — know which "strands" are weakest. The improvement blitz empowers them to fix what they see, without requiring approval from a prioritization committee. This is a direct application of the Toyota Production System principle: the people doing the work are the best experts on improving the work.

### Case Study: Facebook Hackathons and the HipHop Compiler

Mark Zuckerberg describes Facebook's approach: **"Every few months we have a hackathon, where everyone builds prototypes for new ideas they have. At the end, the whole team gets together and looks at everything that has been built. Many of our most successful products came out of hackathons, including Timeline, chat, video, our mobile development framework and some of our most important infrastructure like the HipHop compiler."**

**The HipHop story in detail:**

In 2008, Facebook faced significant capacity problems with over one hundred million active users and rapid growth. During a hack day, **Haiping Zhao**, Senior Server Engineer, started experimenting with converting PHP code to compilable C++ code to increase infrastructure capacity.

Over the next two years, a small team built the **HipHop compiler**, converting all Facebook production services from interpreted PHP to compiled C++ binaries. HipHop enabled Facebook's platform to handle production loads **six times higher** than native PHP.

Drew Paroski, one of the engineers: **"There was a moment where, if HipHop hadn't been there, we would have been in hot water. We would probably have needed more machines to serve the site than we could have gotten in time. It was a Hail Mary pass that worked out."**

Later, Paroski and engineers Keith Adams and Jason Evans created the **HipHop Virtual Machine (HHVM)**, taking a just-in-time compilation approach. By 2012, HHVM had completely replaced the HipHop compiler in production, with nearly twenty engineers contributing.

> **[Insight]** The HipHop story is remarkable because it started as a hack day experiment and became a business-critical infrastructure project that arguably saved Facebook from a scaling crisis. This demonstrates the unpredictable value of improvement time: you cannot predict which hack day project will become a Hail Mary pass. But by creating regular opportunities for experimentation, you increase the probability of breakthrough improvements. The progression from hack day experiment to two-year project to twenty-engineer team to production replacement also shows a healthy maturation path: start small, prove value, get investment, scale up.

---

## Enable Everyone to Teach and Learn

A dynamic culture of learning creates conditions where everyone can not only learn but also teach, through traditional methods (classes, training) and experiential methods (conferences, workshops, mentoring).

### Teaching Thursday at Nationwide Insurance

Steve Farley, VP of Information Technology at Nationwide Insurance (five thousand technology professionals): **"Since 2011, we have been committed to create a culture of learning — part of that is something we call Teaching Thursday, where each week we create time for our associates to learn. For two hours, each associate is expected to teach or learn. The topics are whatever our associates want to learn about — some of them are on technology, on new software development or process improvement techniques, or even on how to better manage their career. The most valuable thing any associate can do is mentor or learn from other associates."**

> **[Insight]** Teaching Thursday at Nationwide is notable for its simplicity and scale: two hours per week, five thousand people, any topic. The math is compelling: 5,000 people x 2 hours/week x 50 weeks/year = 500,000 person-hours of learning per year. Even if only 10% of those hours produce meaningful skill transfer, that is 50,000 person-hours — the equivalent of 25 full-time employees doing nothing but training. And unlike external training, the knowledge is contextual (people teach what they actually use at Nationwide) and bidirectional (the teacher learns by preparing and presenting). The phrase "expected to teach or learn" is also important: it is not optional, and teaching is valued equally with learning.

### Cross-Functional Skill Building

The chapter emphasizes that certain skills are becoming increasingly needed by all engineers, not just developers:

- Version control
- Automated testing
- Deployment pipelines
- Configuration management
- Creating automation

Karthik Gaekwad, part of the National Instruments DevOps transformation: **"For Operations people who are trying to learn automation, it shouldn't be scary — just ask a friendly developer, because they would love to help."**

**Practical methods for cross-functional learning:**
- Joint code reviews that include both Dev and Ops
- Having Development show Operations how to authenticate, log in, and run automated tests
- Integrating new automated tests into deployment pipelines
- Sending test results to monitoring systems for earlier detection of component failures

### Case Study: ASREDS Learning Loop

The chapter introduces the **ASREDS Learning Loop** from *Sooner Safer Happier* (Smart et al., 2020) as a framework for preventing learning from becoming trapped in "learning bubbles" or silos.

**The problem:** When learnings become trapped in bubbles, knowledge is hidden and different teams unnecessarily struggle with similar issues, run similar experiments, develop the same antipatterns, and fail to use each other's learnings. Institutional knowledge is permanently lost when people leave.

**The ASREDS loop:**
1. **A**lign on a goal
2. **S**ense the context
3. **R**espond by designing one or more experiments
4. **E**xperiments — run them
5. **D**istill the results into insights and metrics
6. **S**hare the results by publishing learnings so others can pick them up again at the Sense stage

![Figure 21.1: The ASREDS Learning Loop](../images/Fig21-1.jpg)
*Source: Smart et al., Sooner Safer Happier: Antipatterns and Patterns for Business Agility (Portland, OR: IT Revolution, 2020)*

> **[Deep Dive: The ASREDS Loop as an Anti-Silo Mechanism]**
>
> The critical step in the ASREDS loop is **Share** — and specifically, the fact that sharing feeds back into **Sense** for other teams. This creates a virtuous cycle:
>
> 1. Team A aligns on a goal (e.g., reduce deployment time)
> 2. Team A senses their context (current deployment takes 45 minutes, bottleneck is integration testing)
> 3. Team A designs an experiment (parallelize test suites)
> 4. Team A runs the experiment (deployment time drops to 12 minutes)
> 5. Team A distills the results (parallelization works; specific configuration documented)
> 6. Team A shares the results (published to internal wiki, presented at community of practice meeting)
> 7. Team B, at the **Sense** step of their own loop, discovers Team A's results
> 8. Team B adapts and builds on Team A's experiment rather than starting from scratch
>
> Without the Share step, Team B would independently discover the same problem and run the same experiment — or worse, run a less effective experiment because they lack Team A's context. With the Share step, knowledge compounds across teams.
>
> The ASREDS loop is compatible with the improvement blitz (from earlier in this chapter) and the ChatOps/shared repository mechanisms (from Chapter 20). The loop provides the cognitive framework; the other practices provide the execution mechanisms.

> **[2024+ Context]** The ASREDS loop and similar learning frameworks have been operationalized through several modern approaches:
>
> - **Internal tech blogs and newsletters:** Companies like Netflix, Uber, Airbnb, and Stripe publish engineering blogs that serve a dual purpose: external brand building and internal knowledge sharing.
> - **Guilds and chapters** (Spotify model): Cross-team communities organized around specific topics (e.g., testing guild, data engineering chapter) that regularly share learnings.
> - **Engineering All-Hands with "show and tell":** Regular organization-wide meetings where teams present their recent improvements, failures, and learnings.
> - **Learning Management Systems (LMS):** Platforms like Pluralsight, LinkedIn Learning, and custom internal systems track and incentivize learning activities.

---

## Share Your Experiences from DevOps Conferences

The chapter advocates that organizations should encourage engineers to attend conferences, give talks, and when necessary, create and organize internal or external conferences.

### DevOpsDays and DevOps Enterprise Summit

Two conferences are highlighted:

- **DevOpsDays:** One of the most vibrant self-organized conference series, remaining free or nearly free, supported by practitioner communities and vendors. Many DevOps practices have been shared and promulgated at these events.
- **DevOps Enterprise Summit:** Created in 2014 for technology leaders to share experiences adopting DevOps in large, complex organizations. By 2021, fourteen conferences had been held with nearly one thousand talks from technology experts across almost every industry vertical.

> **[2024+ Context]** The DevOps conference landscape has evolved:
>
> - **DevOpsDays** continues to thrive with events in dozens of cities worldwide, maintaining its community-organized, practitioner-driven format.
> - **DevOps Enterprise Summit** has become a major venue for enterprise transformation stories, with virtual and in-person formats.
> - **SREcon** (USENIX): Focused specifically on site reliability engineering practices.
> - **KubeCon/CloudNativeCon:** The CNCF's flagship conference has become the largest cloud-native/DevOps conference.
> - **PlatformCon:** A newer conference focused specifically on platform engineering.
> - **Virtual/hybrid formats:** Post-2020, conferences increasingly offer virtual participation, making them accessible to organizations with limited travel budgets.

### Case Study: Internal Technology Conferences at Nationwide, Capital One, and Target (2014)

**Nationwide Insurance:**

Since 2005, Nationwide adopted Agile and Lean principles for their five thousand technology professionals. Steve Farley: **"Exciting technology conferences were starting to appear around that time, such as the Agile national conference. In 2011, the technology leadership at Nationwide agreed that we should create a technology conference, called TechCon. By holding this event, we wanted to create a better way to teach ourselves, as well as ensure that everything had a Nationwide context, as opposed to sending everyone to an external conference."**

**Capital One:**

One of the largest US banks ($298 billion in assets, $24 billion in revenue in 2015) held their first internal software engineering conference in 2015. The mission: promote sharing and collaboration, build relationships, and enable learning.

Conference details:
- Thirteen learning tracks and fifty-two sessions
- Over 1,200 internal employees attended
- An expo hall with twenty-eight booths where internal teams showcased their capabilities
- **No vendors** — deliberately keeping focus on Capital One goals

Dr. Tapabrata Pal: **"We even had an expo hall, where we had twenty-eight booths, where internal Capital One teams were showing off all the amazing capabilities they were working on. We even decided very deliberately that there would be no vendors there, because we wanted to keep the focus on Capital One goals."**

**Target:**

Heather Mickman and Ross Clanton held six internal DevOpsDays events since 2014, with over 975 followers in their internal technology community, modeled after DevOpsDays held at ING in Amsterdam in 2013.

After attending the DevOps Enterprise Summit in 2014, they held their own internal conference, inviting speakers from outside firms. Clanton: **"2015 was the year when we got executive attention and when we built up momentum. After that event, tons of people came up to us, asking how they could get involved and how they could help."**

> **[Deep Dive: Why Internal Conferences Are So Effective]**
>
> Internal technology conferences provide several unique benefits that external conferences cannot:
>
> 1. **Contextual relevance:** Every talk, demo, and discussion is about your organization's specific challenges, tools, and culture. There is no "that won't work here" reaction because the speaker is living in the same context.
> 2. **Cross-silo visibility:** In large organizations, teams often have no idea what other teams are building. An internal conference with an expo hall creates a "marketplace of ideas" where teams discover shared problems and potential collaborations.
> 3. **Leadership signaling:** When leadership sponsors and attends an internal conference, it sends a powerful signal that learning and sharing are valued. The Capital One decision to exclude vendors is particularly significant — it says "this is about us, not about selling."
> 4. **Speaker development:** Presenting at an internal conference is a safe stepping stone toward presenting at external conferences. It builds communication skills and confidence in a supportive environment.
> 5. **Community building:** The informal interactions (hallway conversations, expo booths, lunch discussions) create relationships across organizational boundaries that facilitate future collaboration and knowledge sharing.
>
> The Target story is especially instructive: after their internal conference, "tons of people came up to us, asking how they could get involved." This is the grassroots energy that drives lasting transformation — you cannot mandate enthusiasm, but you can create the conditions for it.

> **[Insight]** The progression from external conference attendance to internal conference creation follows a deliberate pattern: (1) send people to external conferences to learn new ideas, (2) have them share what they learned internally, (3) eventually create your own internal conference where the content is tailored to your context. This mirrors the local-to-global pattern of the entire chapter: external knowledge is imported, contextualized, and then propagated internally.

---

## Create Community Structures to Spread Practices

### Continuous Learning: DORA 2019 Findings on Community Structures

DORA's 2019 State of DevOps Report investigated how organizations spread DevOps and Agile practices. The analysis showed that **high performers favor strategies that create community structures at both low and high levels in the organization**, making them more sustainable and resilient to reorganizations and product changes.

**Top strategies employed by high performers:**
1. Communities of practice
2. Grassroots initiatives
3. Proof of concept as a template (the PoC gets reproduced elsewhere)
4. Proof of concept as a seed

> **[Insight]** The DORA finding that communities of practice and grassroots initiatives are the top strategies for high performers is a direct challenge to the "big bang" transformation approach. Many organizations attempt DevOps transformation through top-down mandates: "All teams will use CI/CD by Q4." The research shows that the most effective approach is bottom-up community building, where practitioners self-organize around shared interests and practices, and successful patterns are replicated organically. Top-down support (funding, time allocation, executive sponsorship) enables the grassroots movement, but does not replace it.

### Case Study: Google's Testing Grouplet and Test Mercenaries

The chapter continues the story (introduced earlier in the book) of how Google built a world-class automated testing culture starting in 2005, using dedicated improvement blitzes, internal coaches, and an internal certification program.

**Background:** Google had a 20% innovation time policy, enabling developers to spend roughly one day per week on a Google-related project outside their primary responsibility. Some engineers formed **grouplets** — ad hoc teams of like-minded engineers who pooled their 20% time for focused improvement blitzes.

A testing community of practice was formed by **Bharat Mediratta and Nick Lesiecki**, with the mission of driving automated testing adoption across Google. As Mike Bland described: **"There were no explicit constraints put upon us, either. And we took advantage of that."**

#### Testing on the Toilet (TotT)

One of their most famous mechanisms was **Testing on the Toilet (TotT)** — a weekly testing periodical published in **nearly every bathroom in nearly every Google office worldwide.**

Bland: **"The goal was to raise the degree of testing knowledge and sophistication throughout the company. It's doubtful an online-only publication would've involved people to the same degree."**

> **[Insight]** Testing on the Toilet is a masterclass in knowledge propagation design. By publishing in bathrooms, the Testing Grouplet guaranteed that their content would be read — you have a captive audience. The medium forced brevity (one page, one concept), making each edition focused and digestible. And the name itself created word-of-mouth marketing through humor. The underlying principle is serious: meet people where they are, not where you wish they were. If engineers are not reading your wiki, do not complain about adoption — find a channel they cannot avoid.

#### Test Certified (TC)

**Test Certified** provided a road map to improve automated testing practices. Bland describes it as designed to "hack the measurement-focused priorities of Google culture" and overcome the obstacle of not knowing where or how to start.

**Three levels:**
- **Level 1:** Quickly establish a baseline metric
- **Level 2:** Set a policy and reach an automated test coverage goal
- **Level 3:** Strive towards a long-term coverage goal

**Supporting roles:**
- **Test Certified Mentors:** Provided advice and guidance to any team that wanted help
- **Test Mercenaries:** A full-time team of internal coaches and consultants who worked hands-on with teams to improve testing practices and code quality

Bland was a leader of the testing grouplet from 2006 to 2007, and a member of the test mercenaries from 2007 to 2009.

Bland: **"It was our goal to get every team to TC Level 3, whether they were enrolled in our program or not. We also collaborated closely with the internal testing tools teams, providing feedback as we tackled testing challenges with the product teams. We were boots on the ground, applying the tools we built, and eventually, we were able to remove 'I don't have time to test' as a legitimate excuse."**

On the TC levels: **"The TC levels exploited the Google metrics-driven culture — the three levels of testing were something that people could discuss and brag about at performance review time. The Testing Grouplet eventually got funding for the Test Mercenaries, a staffed team of full-time internal consultants. This was an important step, because now management was fully onboard, not with edicts, but by actual funding."**

> **[Deep Dive: The Google Testing Grouplet as a Model for Internal Change]**
>
> The Testing Grouplet's approach contains a complete playbook for driving organizational change without formal authority:
>
> 1. **Start with volunteers and 20% time** — No budget, no authority, just passionate practitioners. This removes the "we need approval" barrier.
> 2. **Create visible, digestible content (TotT)** — Raise awareness and education across the entire organization through a channel people cannot ignore.
> 3. **Provide a clear path (TC Levels)** — Give teams a concrete, graduated road map so they know where to start and what "good" looks like at each stage.
> 4. **Offer hands-on help (Mentors)** — Advisory support for teams that want guidance but can do the work themselves.
> 5. **Deploy embedded coaches (Mercenaries)** — Full-time consultants who work alongside teams, applying tools and techniques to real code.
> 6. **Hack the culture (metrics, performance reviews)** — Align the improvement with existing incentive structures so that adoption becomes self-reinforcing.
> 7. **Get formal funding** — After demonstrating value, secure organizational commitment through budget allocation.
> 8. **Run company-wide events (Fixits)** — Create moments of collective energy that accelerate adoption.
>
> This progression — volunteer → content → path → mentors → coaches → culture → funding → events — is replicable in any organization for any practice change (not just testing).

#### Company-Wide Fixits

Another mechanism: company-wide **"fixit" improvement blitzes**. Bland describes fixits as **"when ordinary engineers with an idea and a sense of mission recruit all of Google engineering for one-day, intensive sprints of code reform and tool adoption."**

Bland organized four company-wide fixits, the last involving **more than one hundred volunteers in over twenty offices in thirteen countries.** He led the Fixit Grouplet from 2007 to 2008.

Bland's principle: **"provide focused missions at critical points in time to generate excitement and energy, which helps advance the state of the art. This will help the long-term culture change mission reach a new plateau with every big, visible effort."**

> **[Insight]** The fixit model is powerful because it creates a sense of collective mission. When one hundred volunteers in twenty offices and thirteen countries work on the same problem on the same day, it sends a message: this matters, and we are all in this together. The energy from a fixit carries forward long after the day ends — participants return to their teams with new skills, new relationships, and renewed motivation. This is the "punctuated equilibrium" model of change: long periods of gradual improvement, punctuated by intense events that shift the baseline.

---

## Conclusion

The chapter concludes that the rituals described help reinforce the culture that we are all lifelong learners and that **we value the improvement of daily work over daily work itself.** This is achieved by:

- Reserving time to pay down technical debt
- Creating community structures for mutual teaching and learning
- Sharing knowledge both inside and outside the organization

**"By having everyone help each other learn in our daily work, we out-learn the competition, helping us win in the marketplace. But also, we help each other achieve our full potential as human beings."**

> **[Insight]** The closing statement — "we help each other achieve our full potential as human beings" — is a fitting conclusion not just for this chapter but for the entire Part V. The Third Way is ultimately about creating organizations where people grow, learn, and thrive. The competitive advantage (winning in the marketplace) is a consequence of this, not the primary goal. Organizations that treat their engineers as learning machines to be optimized for output miss the point: the most productive engineers are the ones who are growing, challenged, supported, and engaged. The practices in Part V — just culture, blameless retrospectives, chaos engineering, shared knowledge, improvement blitzes, communities of practice — all serve this dual purpose: better systems AND better experiences for the people who build them.

---

## How Generative AI Is Reshaping Organizational Learning

> **[GenAI + Chapter 21 Concepts]** The practices in this chapter — improvement blitzes, teaching and learning, conferences, and community structures — are being augmented and in some cases transformed by Generative AI:

### GenAI and Improvement Blitzes

AI is changing the scope of what can be accomplished during dedicated improvement time:

| Improvement Task | Traditional (Hack Week) | With GenAI (Hack Week) |
|---|---|---|
| **Reduce tech debt** | Team manually refactors 2-3 modules | AI-assisted refactoring of 10-15 modules; AI identifies and generates fixes for code smells |
| **Improve test coverage** | Team writes tests for critical paths | AI generates test suites for entire modules, including edge cases; team reviews and refines |
| **Update documentation** | Team writes docs for undocumented systems | AI generates initial documentation from code analysis; team reviews for accuracy and completeness |
| **Fix security vulnerabilities** | Team triages and patches known CVEs | AI identifies vulnerable patterns across the codebase, generates patches, and creates PRs |
| **Standardize configurations** | Team manually aligns configs to standards | AI detects configuration drift and generates compliant configurations |

The net effect: improvement blitzes become 3-5x more productive, making the same time investment yield significantly more value.

### GenAI and Teaching/Learning

AI is augmenting the teaching and learning practices the chapter describes:

- **Personalized learning paths:** AI can assess an engineer's current skills and create a customized learning plan, matching them with relevant internal content, external courses, and mentors.
- **AI teaching assistants:** During Teaching Thursday-style events, AI can answer follow-up questions, provide additional examples, and help participants apply concepts to their specific codebase.
- **Automated skill gap analysis:** AI can analyze code review patterns, incident participation, and deployment metrics to identify skill gaps at the team and organizational level, informing the topics for learning events.
- **On-demand pairing:** AI coding assistants provide 24/7 "pair programming" that can teach new languages, frameworks, and patterns — supplementing (not replacing) the human mentoring the chapter advocates.

### GenAI and Community Structures

AI can strengthen the community of practice model:

- **Content curation:** AI can monitor internal and external sources to surface relevant content for each community of practice — "the testing guild might be interested in this new property-based testing framework that three teams adopted last quarter."
- **Pattern detection:** AI can analyze code across teams to identify where community of practice knowledge is being applied and where gaps exist — "15 teams have adopted the recommended testing patterns, but 8 teams are still using the deprecated approach."
- **Matchmaking:** AI can identify engineers with complementary skills and connect them for mentoring or collaboration — the algorithmic equivalent of hallway conversations at an internal conference.
- **Knowledge synthesis:** AI can synthesize discussions from community Slack channels, meeting notes, and presentations into searchable knowledge bases — preventing the loss of institutional knowledge that the ASREDS loop addresses.

### The Meta-Question: Does AI Reduce the Need for Reserved Learning Time?

No — it makes reserved learning time even more valuable. AI increases the productivity of improvement work (more tech debt reduced per hour), the effectiveness of teaching (more personalized, more accessible), and the reach of community structures (better knowledge propagation). But AI cannot create the organizational discipline of actually reserving the time. The hardest part of this chapter's prescription is not the mechanics of improvement blitzes or internal conferences — it is the organizational commitment to protect time from the relentless pressure of feature work.

If anything, AI raises the stakes: organizations that reserve time for learning will leverage AI to accelerate their improvement dramatically. Organizations that do not reserve time will find that AI generates more code faster, creating more technical debt faster, deepening the downward spiral.

The Toyota spider web metaphor applies: AI makes each individual strand repair faster and more effective, but the spider still needs to dedicate time to repairing the web.

**Further reading:**
- [Sooner Safer Happier (IT Revolution)](https://itrevolution.com/product/sooner-safer-happier/) — source of the ASREDS learning loop
- [Google Testing Blog](https://testing.googleblog.com/) — ongoing evolution of Google's testing culture
- [DevOpsDays](https://devopsdays.org/) — community-organized DevOps conferences worldwide
- [DevOps Enterprise Summit](https://events.itrevolution.com/) — enterprise DevOps experience reports
- [Spotify Engineering Culture (Video)](https://engineering.atspotify.com/) — the guild/chapter model for communities of practice
- [Target's DevOps Dojo Story (DOES Talk)](https://videos.itrevolution.com/) — detailed presentation of the Dojo model
- [DORA State of DevOps Reports](https://dora.dev/) — annual research on DevOps practices and performance
