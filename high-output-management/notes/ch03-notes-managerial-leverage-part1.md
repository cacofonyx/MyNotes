# Chapter 3: Managerial Leverage — Part 1

> **High Output Management** — Andrew S. Grove
> *The Manager's Output Equation and the Five Managerial Activities*

This is the most important chapter in the book. Everything before it was preparation — building a production vocabulary that Grove now applies to the work of managers themselves. The central question: **What is a manager's output?** Most managers answer with activities (making decisions, giving direction, allocating resources). Grove says those are inputs, not outputs. The output of a manager is the output of the organizations under their supervision or influence. From this definition, Grove derives the concept of **managerial leverage** — the ratio of output to activity — and shows how a manager can maximize their impact by choosing high-leverage activities and avoiding negative-leverage ones.

This chapter is split into three parts:
- **Part 1** (this file): The manager's output equation, Grove's day, and the five managerial activities
- **Part 2**: The leverage equation, high-leverage activities, negative leverage, and delegation
- **Part 3**: Time management via production principles, span of control, and interruptions

## Table of Contents

- [What Is a Manager's Output?](#what-is-a-managers-output)
  - [The Output Equation](#the-output-equation)
  - [Output vs. Activity — The Distinction That Matters](#output-vs-activity--the-distinction-that-matters)
  - [The Know-How Manager as Middle Manager](#the-know-how-manager-as-middle-manager)
- [A Day from Grove's Life](#a-day-from-groves-life)
  - [The Raw Data: What Grove Actually Did](#the-raw-data-what-grove-actually-did)
  - [Patterns in the Chaos](#patterns-in-the-chaos)
- [The Five Managerial Activities](#the-five-managerial-activities)
  - [1. Information-Gathering](#1-information-gathering)
  - [2. Information-Giving](#2-information-giving)
  - [3. Decision-Making](#3-decision-making)
  - [4. Nudging](#4-nudging)
  - [5. Being a Role Model](#5-being-a-role-model)

**Block types:** [Core Concept] [Modern Lens] [Senior EM Application] [SRE Lens] [Production Thinking] [Practical Toolkit] [Anti-Pattern] [Mental Model] [AI & Automation] [Scenario]

---

## What Is a Manager's Output?

Grove opens by asking a group of middle managers what a manager's output is. Their answers:

> judgments and opinions... direction... allocation of resources... mistakes detected... personnel trained and subordinates developed... courses taught... products planned... commitments negotiated

Grove's response: *"Do these things really constitute the output of a manager? I don't think so. They are instead activities, or descriptions of what managers do as they try to create a final result, or output."*

### The Output Equation

Then Grove states the equation that defines the entire book:

> **A manager's output = The output of his organization + The output of the neighboring organizations under his influence**

If a manager runs a wafer fabrication plant, her output is completed silicon wafers. If he supervises a design group, his output is completed designs. If she's a high school principal, her output is educated students. The manager's *activities* (meetings, emails, decisions) are not the output — they are the means by which output is achieved.

> *"A manager can do his 'own' job, his individual work, and do it well, but that does not constitute his output. If the manager has a group of people reporting to him or a circle of people influenced by him, the manager's output must be measured by the output created by his subordinates and associates."*

Grove draws an analogy: *"A coach or a quarterback alone does not score touchdowns and win games. Entire teams with their participation and guidance and direction do. League standings are kept by team, not by individual."*

> **[Core Concept: The Output Equation — The Foundation of Everything]**
>
> This equation is deceptively simple but its implications are profound:
>
> 1. **Your personal work is not your output.** The strategy doc you wrote, the architecture review you led, the incident you triaged — none of these are your output *as a manager*. They are activities. Your output is what your *organization produced* as a result.
>
> 2. **You have two levers:** direct supervision (your teams) and influence (neighboring teams). Most managers focus on the first and neglect the second. But for a Senior EM, the influence lever can be more powerful — aligning with product teams, sharing practices with other engineering orgs, influencing architecture decisions across the company.
>
> 3. **It forces accountability for outcomes, not effort.** You can work 80-hour weeks and attend every meeting, but if your teams aren't producing, your managerial output is low. Conversely, a manager who works 40 hours but whose teams ship reliably and consistently has high output.
>
> 4. **It applies to non-managers too.** Grove explicitly extends this to "know-how managers" — anyone who influences the work of others through expertise. A Staff engineer who shapes architecture decisions across 5 teams has output = the combined impact on those teams.

> **[Senior EM Application: Your Output Equation]**
>
> As a Senior EM managing 2-4 teams (say 15-30 engineers), your output equation is:
>
> ```
> Your output = Output of Team A + Output of Team B + Output of Team C
>             + Influence on Product Org + Influence on Platform Team
>             + Influence on Engineering-wide practices
> ```
>
> **Direct supervision output examples:**
> - Features shipped by your teams
> - Reliability improvements (SLO compliance, incident reduction)
> - Engineer development (promotions, skill growth)
> - Process improvements (faster delivery, reduced toil)
>
> **Influence output examples:**
> - Product team improved their reliability practices because of your advocacy
> - Other engineering orgs adopted the SLO framework you pioneered
> - Architecture review board made better decisions because of your input
> - Company-wide incident response improved because of the process you proposed
>
> **The diagnostic test:** At the end of each quarter, can you point to specific outputs from *each* of your teams AND specific improvements in neighboring organizations that happened because of your influence? If the influence column is empty, you're under-leveraging half of your output equation.

### The Know-How Manager as Middle Manager

Grove broadens the definition of "manager" to include anyone who influences others' work:

> *"Individual contributors who gather and disseminate know-how and information should also be seen as middle managers, because they exert great power within the organization."*

He gives the example of Cindy, an engineer who both supervises an engineering group in one plant AND serves on an advisory body that establishes standards for all plants. In the first role, her output is her plant's output. In the second, her output is the output improvement across ALL plants that her standards enable.

> **[Modern Lens: Staff+ Engineers and the Influence Output]**
>
> Grove's "know-how manager" concept maps perfectly to the modern Staff+/Principal engineer path. These engineers don't manage teams but produce enormous organizational output through influence:
>
> | Activity (What They Do) | Output (What They Produce) |
> |------------------------|---------------------------|
> | Write an architecture RFC | Multiple teams adopt a better approach — multiplied output |
> | Review design docs across teams | Higher quality designs, fewer costly mistakes caught late |
> | Establish coding standards | Consistency across codebase, faster onboarding for new engineers |
> | Mentor a senior engineer on system design | That engineer designs better systems for years to come |
> | Participate in architecture review board | Better org-wide technical decisions |
>
> The output equation for a Staff engineer: **their personal code output + the output improvement of every team they influence.** A Staff engineer who writes no code but whose architecture guidance improves the output of 5 teams by 10% each has more output than a Staff engineer who writes brilliant code alone.

---

## A Day from Grove's Life

Grove lays out an actual day from his schedule as Intel's president. This is one of the most revealing sections of the book because it shows what executive management *actually looks like* — and it's messier than any framework suggests.

### The Raw Data: What Grove Actually Did

| Time | Activity | Type |
|------|----------|------|
| 8:00-8:30 | Met with manager who resigned — listened to reasons, encouraged him to talk to other managers about a career change, decided to follow up personally | Information-gathering, Nudging, Decision-making |
| 8:00-8:30 | Phone call from competitor — ostensibly about industry meeting, actually mutual intelligence gathering about business conditions | Information-gathering |
| 8:30-9:00 | Read morning mail — scribbled messages: encouragement, disapproval, exhortations, denied a project request | Information-gathering, Nudging, Decision-making |
| 9:00-12:00 | Executive Staff Meeting — reviewed orders/shipments, set planning priorities, reviewed faltering marketing program, reviewed manufacturing cycle time reduction | Information-gathering, Decision-making, Nudging |
| 12:00-1:00 | Lunch in cafeteria — sat with training org, heard complaints about senior manager participation in foreign training, noted follow-up needed | Information-gathering, Nudging |
| 1:00-2:00 | Meeting on product quality problem — gathered information on status and corrective action, concurred with decision to resume shipment | Information-gathering, Decision-making |
| 2:00-4:00 | Lecture at employee orientation — gave presentation to ~200 new employees about company history, objectives, values; answered questions | Information-giving, Role modeling |
| 4:00-4:45 | Returned phone calls — denied a compensation request, decided to hold a meeting about new site organization | Decision-making |
| 4:45-5:00 | Met with assistant — reviewed requests for upcoming week, decided which to attend | Decision-making |
| 5:00-6:15 | Read afternoon mail and progress reports — information-gathering with nudging annotations | Information-gathering, Nudging |

### Patterns in the Chaos

Grove's self-assessment:

> *"When you look at what happened, you won't see any obvious patterns. I dealt with things in seemingly random fashion."*

His wife observed that it looked like her day managing a household. Grove agrees:

> *"My day always ends when I'm tired and ready to go home, not when I'm done. I am never done. Like a housewife's, a manager's work is never done."*

Two critical observations emerge:

1. **~25 separate activities** in one day — mostly information-gathering and giving, with decision-making and nudging mixed in
2. **~Two thirds of the day spent in meetings** — but before you're horrified, Grove asks: *"which of the activities — information-gathering, information-giving, decision-making, nudging, and being a role model — could I have performed outside a meeting? The answer is practically none."*

> **[Core Concept: Meetings Are a Medium, Not an Activity]**
>
> This is one of the most important reframes in the book:
>
> *"Meetings provide an occasion for managerial activities. Getting together with others is not, of course, an activity — it is a* medium. *You as a manager can do your work in a meeting, in a memo, or through a loudspeaker for that matter. But you must choose the most effective medium for what you want to accomplish, and that is the one that gives you the greatest leverage."*
>
> Meetings are not inherently good or bad. The question is not "how many meetings do I have?" but "are my meetings the highest-leverage medium for the activities I need to perform?" Sometimes a meeting is the highest-leverage choice (complex decisions requiring multiple perspectives). Sometimes a Slack message is (quick information sharing). Sometimes a document is (broadcasting information to many people asynchronously).
>
> **The Senior EM trap:** Either hating all meetings ("I spend too much time in meetings, I can't get anything done") or accepting all meetings passively. Both are wrong. The right approach: for every meeting on your calendar, ask "what activity am I performing in this meeting, and is a meeting the highest-leverage medium for it?" Cancel the ones where the answer is no.

> **[SRE Lens: An SRE Senior EM's Day Through Grove's Lens]**
>
> If you tracked a day in your life as a Senior EM in SRE, it might look like:
>
> | Time | Activity | Grove's Classification |
> |------|----------|----------------------|
> | 8:00 | Check SLO dashboards, incident overnight summary | **Information-gathering** |
> | 8:30 | 1-1 with TL — discuss career growth, upcoming architecture decision | **Information-gathering + Nudging** |
> | 9:00 | Incident review for yesterday's P2 | **Information-gathering + Decision-making** (action items) |
> | 10:00 | Cross-functional sync with Product EM — negotiate priorities | **Nudging + Information-giving** |
> | 11:00 | Architecture review for new service | **Decision-making + Information-gathering** |
> | 12:00 | Lunch with platform team engineer — hear concerns about migration timeline | **Information-gathering** |
> | 1:00 | Sprint planning for Team B | **Information-gathering** (as observer) |
> | 2:00 | Write quarterly reliability report for Director | **Information-giving** |
> | 3:00 | 1-1 with SRE manager — coaching on how to handle underperformer | **Nudging + Role modeling** |
> | 4:00 | Email triage — respond to headcount request, approve PTO, review RFC comment | **Decision-making + Nudging** |
> | 5:00 | Read team's recent postmortems | **Information-gathering** |
>
> **Notice:** Like Grove, ~70% of the day is meetings. The question isn't "too many meetings?" but "are these the right activities for my output equation?"

---

## The Five Managerial Activities

From his day, Grove identifies five types of managerial activity. Every managerial action falls into one of these categories:

### 1. Information-Gathering

This is what Grove spends the most time on. He collects information through:

- **Standard reports and memos** — structured, regular, but not timely
- **Ad hoc conversations** — with people inside and outside the company
- **Customer complaints** — both external and internal
- **Competitor intelligence** — even a casual phone call yields signal
- **Walking around** — visiting parts of the organization (extremely efficient but underutilized)

Grove's most important observation about information:

> *"The information most useful to me, and I suspect most useful to all managers, comes from quick, often casual verbal exchanges. This usually reaches a manager much faster than anything written down. And usually the more timely the information, the more valuable it is."*

Then a surprising statement about written reports:

> *"Reports are more a* medium *of* self-discipline *than a way to communicate information.* Writing *the report is important; reading it often is not."*

The process of writing forces precision. The report itself is less valuable than the thinking it required. Grove extends this to annual planning and capital authorization: *"the preparation of an annual plan is in itself the end, not the resulting bound volume."*

> **[Core Concept: The Information Hierarchy]**
>
> Grove describes an information hierarchy from most timely to most thorough:
>
> | Level | Analogy | Timeliness | Depth | Example |
> |-------|---------|-----------|-------|---------|
> | **Verbal exchanges** | Newspaper headline | Immediate | Shallow, possibly inaccurate | "I heard the migration is having issues" |
> | **Detailed conversations** | Newspaper article | Hours to days | Moderate depth | 1-1 where the TL explains what's actually happening |
> | **Written reports** | News magazine | Days to weeks | Deep, precise, but stale | The quarterly reliability report with full data |
>
> *"Each level in your information hierarchy is important, and you can rely on none alone."*
>
> Sources should be **complementary and redundant** — redundancy lets you verify what you've learned. This is exactly the Swiss Cheese model applied to information quality: no single source is reliable alone, but layered together they give a complete picture.

> **[Senior EM Application: Walking Around in a Remote World]**
>
> Grove describes "walking around" as *"an especially efficient way to get information, much neglected by most managers."* A two-minute conversation in a hallway achieves what would take a 30-minute scheduled meeting.
>
> **In the remote/hybrid era, the equivalent is:**
> - **Lurking in Slack channels** — read your teams' public channels. The casual conversations reveal team health, confusion, frustration, and wins that you'd never see in a 1-1.
> - **Joining standup async** — read the standup bot posts without attending the meeting. Information-gathering with zero disruption.
> - **Dropping into engineering Slack threads** — when an interesting technical discussion is happening, add a brief comment or question. This is the virtual equivalent of stopping by someone's desk.
> - **Reviewing PRs occasionally** — not to gate, but to gather information about code quality, review dynamics, and engineering approach.
> - **Reading incident channels in real-time** — during an incident, the #incident channel gives you more timely and accurate information than any post-incident report.
>
> **The key insight:** Information-gathering in a remote world requires *deliberate effort*. In an office, information comes to you naturally (hallway conversations, overheard discussions, body language). Remote, you have to seek it out. Budget time daily for this — it's not overhead, it's your most important managerial activity.

> **[AI & Automation: AI as Information-Gathering Accelerator]**
>
> Grove spent the majority of his day gathering information. AI is fundamentally changing the economics of this activity:
>
> | Information-Gathering Activity | Traditional | AI-Augmented |
> |-------------------------------|-------------|-------------|
> | Reading reports | Read each one, extract key points | AI summarizes key points, flags anomalies, highlights changes from last period |
> | Monitoring dashboards | Check each dashboard, spot trends | AI monitors continuously, alerts only on meaningful deviations |
> | Reading Slack channels | Skim channels, try to spot important threads | AI summarizes daily activity, highlights threads needing attention |
> | Reviewing postmortems | Read each one, extract patterns | AI correlates across postmortems, identifies systemic patterns |
> | Competitive intelligence | Talk to people, read industry news | AI aggregates and summarizes industry signals |
>
> **The danger:** AI makes information-gathering faster, but Grove says the value of information comes from the *judgment* applied to it. An AI summary of a postmortem is useful; but the insight that "this is the third time the same team has had a database connection pool issue, which means we have a training problem, not a code problem" requires human judgment. AI accelerates the gathering; humans must still do the interpreting.

### 2. Information-Giving

Managers are not just information consumers — they're transmitters. Grove emphasizes that beyond relaying facts, a manager must communicate *"objectives, priorities, and preferences as they bear on the way certain tasks are approached."*

This matters because:

> *"Only if the manager imparts these will his subordinates know how to make decisions themselves that will be acceptable to the manager, their supervisor. Thus, transmitting objectives and preferred approaches constitutes a key to successful delegation."*

### 3. Decision-Making

Grove distinguishes between *making* decisions and *participating in* them:

> *"For every time that happens, we* participate *in the making of many, many others, and we do that in a variety of ways. We provide factual inputs or just offer opinions, we debate the pros and cons of alternatives and thereby force a better decision to emerge, we review decisions made or about to be made by others, encourage or discourage them, ratify or veto them."*

Two types of decisions:
- **Forward-looking** — capital allocation, strategic planning, resource commitment
- **Responsive** — reacting to a developing problem or crisis (technical or people)

### 4. Nudging

Grove identifies a category of action that most management books miss entirely:

> *"You often do things at the office designed to influence events slightly... you may be advocating a preferred course of action, but you are not issuing an instruction or a command. Yet you're doing something stronger than merely conveying information. Let's call it 'nudging' because through it you nudge an individual or a meeting in the direction you would like."*

> *"In reality, for every unambiguous decision we make, we probably nudge things a dozen times."*

> **[Core Concept: Nudging — The Most Underrated Managerial Activity]**
>
> Nudging is where most of a manager's actual influence happens. It's the annotation on a report, the question in a meeting that redirects thinking, the suggestion to "talk to so-and-so about that," the raised eyebrow when someone proposes something questionable.
>
> **For Senior EMs, nudging looks like:**
> - Asking a leading question in an architecture review: "Have we considered what happens if the primary database fails?" — not a decision, but it forces the team to think about failure modes
> - Sending a Slack message to a TL: "I noticed Team B had a similar problem last quarter — might be worth comparing notes" — not a command, but it creates a connection
> - Cc'ing your director on a message about a risk: you're not escalating, but you're making the risk visible
> - Saying in a sprint planning: "This feels like a lot of scope for two weeks" — you're not overruling the team, but you're signaling concern
>
> **Why nudging matters more than decisions at senior levels:** The higher you go, the less you should be making direct decisions for your teams. But you're *constantly* nudging — shaping how people think about problems, what they prioritize, who they collaborate with, and which risks they take seriously. Nudging is how you scale your judgment across multiple teams without micromanaging.

### 5. Being a Role Model

> *"While we move about, doing what we regard as our jobs, we are* role models *for people in our organization... no single managerial activity can be said to constitute leadership, and nothing leads as well as example."*

> *"Values and behavioral norms are simply not transmitted easily by talk or memo, but are conveyed very effectively by doing and doing* visibly."

Grove gives pointed examples of negative role modeling: an insurance agent who makes personal calls on company time, a lawyer who returns from lunch drunk. The message: your *behavior* communicates values more powerfully than your *words*.

Then the most important statement about time:

> *"A great deal of a manager's work has to do with allocating resources: manpower, money, and capital. But the single most important resource that we allocate from one day to the next is our own time... How you handle your own time is, in my view, the single most important aspect of being a role model and leader."*

> **[SRE Lens: Role Modeling in SRE Culture]**
>
> What you do as a Senior EM *is* the SRE culture, whether you intend it or not:
>
> | What You Do | What It Signals |
> |------------|----------------|
> | You personally participate in incident response when a P1 hits | "Incidents matter enough for senior leadership to engage" |
> | You skip postmortems because you're "too busy" | "Postmortems are bureaucratic overhead, not valuable" |
> | You stay calm during incidents, focus on mitigation, ask clarifying questions | "Blameless response is the standard" |
> | You berate someone during an incident for "causing" the outage | "We blame people here" — no one will raise problems early again |
> | You take PTO and actually disconnect | "Work-life balance is real, not performative" |
> | You cancel 1-1s every other week for "more important" meetings | "Your direct reports are less important than whatever else is on your calendar" |
> | You respond to Slack at 11pm | "You should be available 24/7" — even if you say otherwise |
>
> Grove's point: you don't get to choose whether you're a role model. You already are. The only choice is what you model.

---

**Part 1 covered:** The output equation (manager's output = team output + influence output), Grove's day as a detailed case study, and the five managerial activities (information-gathering, information-giving, decision-making, nudging, role modeling).

**Part 2 covers:** The leverage equation (Output = L1×A1 + L2×A2 + ...), three types of high-leverage activities, negative leverage (depression, waffling, meddling), and delegation as leverage.

**Part 3 covers:** Time management via production principles (batching, calendar as production tool, slack, inventory of projects), span of control (6-8 rule), and managing interruptions.
