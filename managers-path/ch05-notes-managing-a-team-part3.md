# Chapter 5: Managing a Team — Part 3

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

**Part 3 covers:** Team cohesion destroyers (brilliant jerk, noncommunicator, disrespectful employee), advanced project management, joining a small team, assessing your experience, closing rituals.
See [Part 1](ch05-notes-managing-a-team-part1.md) for: staying technical, debugging dysfunctional teams, the shield, managing former peers.
See [Part 2](ch05-notes-managing-a-team-part2.md) for: driving good decisions, conflict management.

## Table of Contents — Part 3

- [Challenging Situations: Team Cohesion Destroyers](#challenging-situations-team-cohesion-destroyers)
  - [The Brilliant Jerk](#the-brilliant-jerk)
  - [The Noncommunicator](#the-noncommunicator)
  - [The Employee Who Lacks Respect](#the-employee-who-lacks-respect)
- [Advanced Project Management](#advanced-project-management)
  - [Project Management Rules of Thumb](#project-management-rules-of-thumb)
- [Ask the CTO: Joining a Small Team](#ask-the-cto-joining-a-small-team)
- [Assessing Your Own Experience](#assessing-your-own-experience)
- [Quarterly Ritual: Team System Health (Part 3)](#quarterly-ritual-team-system-health-part-3)
- [Peer Reflection Prompt (Part 3)](#peer-reflection-prompt-part-3)
- [How GenAI Is Reshaping Team Management](#how-genai-is-reshaping-team-management)

**Block types in Part 3:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Cross-Functional Play] [First 90 Days] [Go Deeper] [Quarterly Ritual] [Peer Reflection Prompt]

---

## Challenging Situations: Team Cohesion Destroyers

Fournier opens this section by defining the real goal of team building: **psychological safety** — "a team whose members are willing to take risks and make mistakes in front of one another." This isn't about pizza parties; it's the underpinning of a successful team.

She recommends building relatedness: knowing people as humans, asking about their lives, letting them share what they're comfortable sharing. "This is more than empty small talk; it fosters relatedness, the sense of people as individuals and not just anonymous cogs."

On "culture fit" hiring: she acknowledges it "can have some unwanted consequences, such as discrimination" but comes from a wise place — "Teams that are friendly are happier, gel faster, and tend to produce better results."

Toxic employees are problematic specifically because they "make it hard for the rest of the team to feel safe around them." They destroy the psychological safety that makes teams effective.

> **[Mental Model: Psychological Safety (Amy Edmondson)]**
>
> Edmondson's research at Harvard identified psychological safety as the #1 predictor of high-performing teams — ahead of skills, resources, or structure. Google's Project Aristotle famously confirmed this.
>
> **What psychological safety IS:**
> - Team members feel safe to take interpersonal risks
> - People admit mistakes without fear of punishment
> - Questions are welcomed, not seen as weakness
> - Disagreement is productive, not threatening
> - Failure leads to learning, not blame
>
> **What it is NOT:**
> - Niceness (it actually requires candor)
> - Lower standards (high standards + safety = growth)
> - Guaranteed comfort (uncomfortable conversations happen — but safely)
>
> **For SRE teams specifically:** Psychological safety is directly tied to incident response quality. If your junior engineer is afraid to speak up during an incident because the senior engineer will dismiss them, you will miss signals. If your on-call engineer is afraid to escalate because they'll be seen as "not handling it," incidents get worse. If your team doesn't feel safe admitting they don't understand a system, knowledge gaps persist until they cause outages.
>
> **The blameless postmortem is a psychological safety practice.** It exists not because blame is morally wrong, but because blame prevents learning. If people are afraid of punishment, they hide information. If they hide information, you can't improve the system.
>
> **[Go Deeper]** Amy Edmondson, *The Fearless Organization.* Also: Google's re:Work Project Aristotle findings (free online).

### The Brilliant Jerk

Fournier's most detailed toxic employee profile. The brilliant jerk:
- Produces "individually outsized results"
- Is "so ego-driven that she creates a mixture of fear and dislike in almost everyone around her"
- Has been "rewarded for a very long time for her brilliance, and she clings to it like a life raft"
- "Bullies with her intellect, cutting down dissenting voices... ignoring those she believes are not her equal"
- "Letting her frustration with anything she sees as stupid seep out openly"

Fournier is blunt: **"The best way to avoid brilliant jerk syndrome is to simply not hire one."** Once hired, getting rid of them "takes a level of management confidence that I think is uncommon." They will "fight you tooth and nail on all feedback" and "if she doesn't see her behavior as a problem, she won't change it."

Her practical advice for managing one: **"Simply and openly refuse to tolerate bad behavior."** This is one case where "praise in public, criticize in private" may be inverted — if behavior is visibly impacting the team, address it in the moment: *"Please do not speak to people that way; it is disrespectful."*

Critical caveats:
- Keep your own reaction neutral — "If you seem emotional, it may undermine you"
- Only use public correction for behavior detrimental to the whole group
- If they're undermining you personally, discuss in private
- Priority order: protect the team > protect individuals > protect yourself

> **[Deep Dive: The Cost Accounting of Brilliant Jerks]**
>
> The reason brilliant jerks persist is because managers do bad math. They calculate the brilliant jerk's *visible* output — code shipped, problems solved, technical decisions made — and compare it to the *invisible* cost — talent who leaves, ideas that are never shared, junior engineers who stagnate, psychological safety that erodes.
>
> **Attempt an honest accounting:**
>
> | Visible Value | Hidden Cost |
> |---------------|-------------|
> | Ships 2x the code of peers | 3 engineers left in the past year citing "team culture" — recruiting + onboarding cost: ~$300K each |
> | Makes fast technical decisions | Those decisions are unquestioned because people are afraid to push back — some are wrong and only discovered in production |
> | Solves hard problems others can't | Junior engineers learn to stay silent, stunting their growth and reducing the team's future capacity |
> | Brings deep domain knowledge | That knowledge is hoarded, creating a single point of failure |
> | "Gets things done" | Everyone else is 20% less productive due to the hostile environment |
>
> When you do the full accounting, brilliant jerks are almost always net negative. The challenge is that the value is concentrated and visible, while the cost is distributed and invisible.

> **[SRE Lens: The Brilliant Jerk in Incident Response]**
>
> SRE teams are particularly vulnerable to brilliant jerks because incident response rewards fast, decisive, technically deep individuals — and brilliant jerks often shine brightest during incidents. They diagnose faster, they know the systems deeper, they push the fix.
>
> **The hidden cost in SRE:**
> - During incidents, their dominance shuts down other voices. The junior engineer who noticed the correlation between the deployment and the latency spike doesn't speak up because last time they were told "that's not relevant." That correlation WAS the root cause.
> - Postmortems become the brilliant jerk's performance review — they narrate the incident from their perspective, and no one challenges it. Systemic issues that require admitting uncertainty are glossed over.
> - On-call engineers afraid to escalate to the brilliant jerk let incidents run longer rather than face the dismissive response.
> - The brilliant jerk accumulates tribal knowledge because no one wants to pair with them, creating catastrophic bus factor risk.
>
> **The SRE-specific intervention:** Establish incident protocols that explicitly distribute voice. "Before we escalate, I want to hear from everyone on the bridge — what are you each seeing?" Make it structural, not personal, so no one person can dominate.

> **[Script: Addressing Brilliant Jerk Behavior in the Moment]**
>
> In a design review, your senior engineer sighs audibly when a mid-level engineer presents their approach, then says: "This is fundamentally wrong. Did you even read the documentation on how this system works?"
>
> **In the room, calmly:**
> *"Let's pause. Alex, I can see you have concerns about the approach — I want to hear them. But the way that came across was dismissive, and I need us to keep this a space where everyone can present ideas without being shut down. Can you rephrase your concern as a specific technical question?"*
>
> **In the follow-up 1-1:**
> *"I want to revisit what happened in the design review. When you said 'did you even read the documentation,' here's what I observed: Maya went quiet for the rest of the meeting, and no one else volunteered alternative approaches after that moment. You may have been right that the approach had issues — but the way you raised it prevented us from having a productive technical discussion.*
>
> *This is a pattern I've seen before. You have strong technical instincts, and I value that. But the impact of how you share them is reducing the team's overall output. I need you to find ways to challenge ideas without dismissing the person presenting them. 'I have a concern about X — can you walk me through how you'd handle Y?' gets you the same outcome without the collateral damage.*
>
> *I want to be direct: this is a requirement for your role, not a suggestion. If I continue to see this pattern, it will affect your performance evaluation and your career progression here. How can I help you work on this?"*

> **[Interview Angle]**
>
> "Tell me about a time you dealt with a difficult team member" — the brilliant jerk scenario is the strongest possible answer for a Senior EM/Director candidate.
>
> **Strong answer demonstrates:**
> - You recognized the hidden cost, not just the visible value
> - You addressed it directly — not passively hoped it would improve
> - You gave clear feedback with specific examples
> - You set a deadline for change
> - You were prepared to follow through (PIP, termination, or transfer)
> - You protected the team throughout the process
>
> **Weak answer:** "They were so productive that I worked around the personality issues." This tells the interviewer you'll tolerate toxic behavior.

### The Noncommunicator

Fournier's second toxic type: the person who hides information from everyone — manager, teammates, product manager. "Prefers to work in secret and unveil a magical project when everything is done and perfect." May revert others' commits or take their tickets. Doesn't want code review or design review.

Root causes: fear (of being found lacking, of unwanted work), or disrespect for the manager and desire for more autonomy.

Fournier says: "Nip this information-hiding habit in the bud as soon as possible." Address the root cause — if it's fear, check whether the team culture is harsh. If the team is treating this person as an outsider, decide whether to fix the team culture or move the individual.

> **[SRE Lens: The Noncommunicator During Incidents]**
>
> In SRE, noncommunicators are dangerous during incidents. The engineer who quietly fixes a problem without telling anyone denies the team the chance to learn. The on-call who resolves an incident without documenting it means the next person will face the same problem blind.
>
> **SRE-specific manifestations:**
> - Making production changes without announcing in the incident channel
> - Closing incidents without writing postmortems
> - Building automation that only they understand
> - Fixing problems silently during on-call and reporting "quiet week"
>
> **The fix:** Make communication a non-negotiable part of the operational process. Every production change gets announced. Every incident gets a postmortem, even minor ones. On-call handoffs include a written summary. These aren't bureaucracy — they're safety practices, like a pilot's checklist. Frame it that way: "In SRE, undocumented work is unfinished work."

> **[Anti-Pattern: The Lone Wolf Hero]**
>
> A variant of the noncommunicator specific to SRE: the engineer who resolves incidents single-handedly, dramatically, at 3 AM — and loves doing it. They don't involve others because they're faster alone. They don't document because they'll "remember." They don't improve systems because the heroics feel good.
>
> **Why this is destructive:**
> - Bus factor of 1 for critical institutional knowledge
> - Other team members never develop incident response skills
> - Systemic problems never get fixed because the hero patches over them each time
> - The hero burns out — they always do — and the team is suddenly helpless
>
> **The fix:** Require pair incident response for all P1/P2 incidents. The hero can lead, but someone else must be involved, learning, and documenting. Celebrate the postmortem as much as the fix. Explicitly value "incidents prevented" over "incidents heroically resolved."

### The Employee Who Lacks Respect

Fournier's shortest toxic employee section, because the advice is straightforward: if someone doesn't respect you or their teammates, ask directly whether they want to be on the team. If yes, lay out expectations clearly. If no, start the process to move them.

**"You can't have a person working for you who doesn't respect you, or doesn't respect your team. It will eat away at the cohesion of the rest of the team as they wonder whether that person is right in not respecting you."**

> **[Insight]** Fournier doesn't spend many words here because the situation is actually simple, even though it feels hard. The difficulty isn't intellectual — it's emotional. You know you need to address it. You're afraid. That's the entire story. Reread her advice from the conflict section: "Don't be afraid."
>
> The nuance for Senior EMs: at your level, "lack of respect" sometimes manifests as a report who constantly second-guesses you to *your* reports (undermining your authority), or who goes around you to your director. This is more insidious than open disrespect because it can look like "just being proactive." Address it directly: "I've noticed you've been raising concerns with [my director] before discussing them with me. I want to understand what's driving that — is there something about how I'm handling things that makes you feel you can't come to me first?"

---

## Advanced Project Management

Fournier acknowledges this might seem like a step back from the "big picture" management topics, but argues that engineering managers own estimation and planning in ways that matter.

"The organization will expect you to be capable of doing both off-the-cuff estimation and more concrete project planning."

### Project Management Rules of Thumb

**Rule 1: None of this is a replacement for agile project management.**

Fournier clarifies her role: she's not talking about sprint-level planning (that's the team's process). She's talking about **the larger picture — accomplishments measured in months — where higher-level planning is needed.**

> **[Senior EM vs. Director: Planning Scope]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **Planning horizon** | This quarter: what will we ship? Next quarter: what should we prepare for? | This year: what are the strategic bets? Next year: what capabilities do we need? |
> | **Estimation role** | Provides estimates for your team's work; pushes back on unrealistic commitments | Aggregates estimates across teams; makes resource allocation decisions |
> | **Scope management** | Cuts scope within projects to hit deadlines | Cuts entire projects or deprioritizes team-level initiatives to fit organizational capacity |
> | **Stakeholder communication** | Communicates timeline/risks to product partner and your director | Communicates portfolio-level progress to VP/exec, manages expectations across multiple stakeholders |

**Rule 2: You have 10 productive engineering weeks per engineer per quarter.**

13 weeks per quarter, but vacations, meetings, review season, production outages, and onboarding consume the rest. "Don't expect to get more than 10 weeks' worth of focused effort." Q1 is typically most productive; Q4 least.

> **[SRE Lens: It's Even Less for SRE Teams]**
>
> Fournier's 10-week estimate is for product engineering. For SRE teams, the math is worse:
>
> - 13 weeks per quarter, per engineer
> - Minus 3 weeks (vacations, meetings, reviews) = 10 weeks (Fournier's baseline)
> - Minus 2 weeks for on-call primary rotation (assuming 6-person rotation, ~2 weeks/quarter per person)
> - Minus 1 week for incident response during non-on-call time (postmortems, follow-ups, helping on-call)
> - Minus 1 week for cross-team support requests ("can you help us with...?")
> - **= approximately 6 productive project weeks per engineer per quarter**
>
> If you plan SRE project work at 10 weeks per person, you'll miss every commitment. Plan at 6, and add the 20% sustainability buffer on top of that.
>
> **The math your leadership needs to see:**
> - 5 SRE engineers × 6 project weeks = 30 engineer-weeks of project capacity per quarter
> - NOT 5 × 13 = 65, which is what a naive calculation produces
> - The gap between 30 and 65 is where unrealistic expectations live

**Rule 3: Budget 20% of time for generic sustaining engineering work.**

Testing, debugging, legacy code cleanup, platform migrations. "If you make this a habit, you can use it to tackle some of the midsize legacy code every quarter." In the worst case, it serves as slack for unexpected delays. But "if you fill the schedule to 100% with feature development, expect that the feature development will quickly slow down as a result of this overscheduling."

> **[Leader's Playbook: The Capacity Planning Template]**
>
> For a quarterly planning conversation, present team capacity like this:
>
> **Team: SRE Platform (5 engineers)**
>
> | Category | Weeks/Quarter (per person) | Total Team Weeks | % |
> |----------|---------------------------|-----------------|---|
> | On-call + incident response | 3 | 15 | 23% |
> | Sustainability (toil reduction, upgrades, debt) | 1.5 | 7.5 | 12% |
> | Cross-team support + meetings + overhead | 2.5 | 12.5 | 19% |
> | **Available for project work** | **6** | **30** | **46%** |
>
> "We have 30 engineer-weeks of project capacity this quarter. Here are the projects we can commit to within that budget, prioritized by impact."
>
> **Why this works:** It makes invisible work visible. Leadership can see that the team isn't "only" working on 2 projects with 5 people — they're supporting 15 services on-call, reducing toil, and handling cross-team requests, PLUS doing 2 projects. The conversation shifts from "why aren't you doing more?" to "given your constraints, are these the right 2 projects?"

**Rule 4: As you approach deadlines, it is your job to say no.**

You partner with tech lead and product to figure out "what 'must-haves' are not actually must-haves." You say no to both sides: push engineers toward pragmatic solutions when they want perfection, and push product toward simpler features when they want everything.

> **[Script: Saying No to Scope Near a Deadline]**
>
> Two weeks before a deadline. Product wants to add "just one more feature." Your tech lead says the team can do it "if we work weekends."
>
> To the product manager:
> *"I understand this feature is important, and I want to find a way to include it. But we're two weeks from our deadline, and adding this feature creates risk to the features we've already committed to — features your stakeholders are expecting. Here's what I can offer: we ship the committed scope on time, and I'll prioritize this feature as the first item next sprint. That gives us the quality we need without jeopardizing the deadline."*
>
> To the tech lead:
> *"I appreciate the team's willingness to push, and I don't want to waste that energy. But 'if we work weekends' is a warning sign, not a plan. If we burn the team out for this addition, we pay for it in the next sprint — slower velocity, lower morale, maybe someone calling in sick. Let's ship what we have and come back fresh."*

**Rule 5: Use the doubling rule for quick estimates, but push for planning time for longer tasks.**

"Whenever asked for an estimate, take your guess and double it." Good for off-the-cuff requests. For projects longer than a couple of weeks, double it AND request planning time before committing.

**Rule 6: Be selective about what you bring to the team to estimate.**

"It's distracting and stressful for engineers to have a manager who's constantly asking them for random project estimates." Handle uncertainty yourself. Don't be a telephone relaying estimation requests. Establish a teamwide process for discussing new work.

> **[Anti-Pattern: The Estimation Telephone]**
>
> Your VP asks your director: "How long to build feature X?" Director asks you. You walk to your tech lead's desk: "Hey, quick question — how long to build feature X?" Tech lead gives a gut feeling: "Maybe 3 weeks?" You relay back: "3 weeks." Director tells VP: "3 weeks." VP commits to a customer. The actual work takes 8 weeks.
>
> **What went wrong:** A gut-feeling estimate passed through a chain of people, each of whom heard a number without context and assumed it was more precise than it was. Nobody asked clarifying questions. Nobody added buffer. Nobody identified unknowns.
>
> **The fix:** When asked for an estimate, don't relay the question. Either give YOUR informed estimate based on your knowledge of the team and systems ("Off the top of my head, I'd estimate 4-8 weeks. I need 2 days of planning time to refine that.") or push back on premature commitment ("I can give you a range now, or a reliable estimate after a day of planning. Which do you need?").

> **[Mental Model: The Cone of Uncertainty]**
>
> Software estimation error follows a predictable pattern: early estimates are wildly inaccurate, and accuracy improves as you learn more about the work.
>
> - **Concept stage:** Estimates range 0.25x to 4x actual
> - **After initial design:** 0.5x to 2x
> - **After detailed design:** 0.67x to 1.5x
> - **After implementation starts:** 0.8x to 1.25x
>
> **Implication for managers:** When your VP asks "how long?" at the concept stage, the honest answer is: "Between 3 weeks and 6 months — I literally cannot tell you yet." You need to educate stakeholders about this reality and negotiate planning time to narrow the cone before committing.
>
> **The Senior EM skill:** Learn to give estimates as ranges with confidence levels. "I'm 80% confident this is 4-8 weeks. I'm 50% confident it's 3-5 weeks." This communicates the uncertainty honestly without sounding evasive.
>
> **[Go Deeper]** Steve McConnell, *Software Estimation: Demystifying the Black Art.* The cone of uncertainty is covered in Chapter 4.

---

## Ask the CTO: Joining a Small Team

A new manager hired from outside asks how to approach their first weeks managing a team of 5 where they know neither the people nor the technology.

Fournier's advice:
1. Get someone to walk you through systems, architecture, testing, and release process
2. Go through the normal developer onboarding if one exists
3. Spend time getting comfortable in the codebase — watch code reviews and pull requests
4. **Plan to work on at least a couple of features in your first 60 days** — take a specced feature, add it, pair with engineers, get your code reviewed
5. Perform a release, do an on-call rotation or support stint
6. Accept that management onboarding will be slower because of the technical ramp — "This slowdown is worth it"

"By getting to know the code, the processes for writing code, and the tools and systems your team use for their day-to-day, you will gain the understanding necessary for managing the team, and the technical credibility necessary for them to see you as a capable leader."

> **[First 90 Days: Joining as an External SRE Manager]**
>
> Fournier's advice plus SRE-specific additions:
>
> **Week 1-2: Orient**
> - [ ] Developer onboarding: check out code, set up local environment, deploy to staging
> - [ ] Meet every report 1-1. Ask Fournier's rapport questions (Ch4) + "What's the biggest operational risk we're not addressing?"
> - [ ] Get a systems architecture walkthrough. Draw the dependency map. Identify the systems you're on-call for.
> - [ ] Review the last 3 months of incidents. Read every P1/P2 postmortem.
> - [ ] Shadow an on-call shift. See what the on-call experience actually feels like.
>
> **Week 3-4: Participate**
> - [ ] Take a specced feature or bug fix and implement it. Get code reviewed by the team.
> - [ ] Perform a production deployment. Feel the deploy process firsthand.
> - [ ] Attend (or run) a postmortem. Observe the team's incident review culture.
> - [ ] Meet cross-functional partners: product managers, dependent team leads, security, platform.
>
> **Week 5-8: Diagnose**
> - [ ] Map the operational landscape: SLOs, error budgets, on-call burden, toil inventory
> - [ ] Identify the top 3 reliability risks (often obvious from incident patterns)
> - [ ] Assess team dynamics: who's strong, who's struggling, where are the collaboration gaps?
> - [ ] Start your management cadence: 1-1 schedule, team meeting rhythm, skip-levels if applicable
>
> **Week 9-12: Act**
> - [ ] Present your initial assessment to your director: "Here's what I've found, here's what I think matters, here's my plan"
> - [ ] Tackle one quick win that builds credibility (fix the most painful operational process, resolve a chronic toil item)
> - [ ] Set or refine team goals. Make sure the team understands the "why."
> - [ ] Solicit feedback: "What's one thing I should do differently?"
>
> **The meta-principle:** Your team will be watching to see whether you're a "real" technical leader or a "management tourist." Shipping code, doing on-call, and reading postmortems are how you earn their trust. Don't skip these because you're "too busy managing."

---

## Assessing Your Own Experience

Fournier closes with self-reflection questions. For each, I've added the Senior EM interpretation:

**"What are your new responsibilities now that you're the manager of a team? What tasks have you stopped doing or handed off?"**

> **[Insight]** This question targets a common failure: managers who add responsibilities without letting go of old ones, until they're doing two jobs badly. At the Senior EM level, the question becomes: what tech lead or individual contributor work are you still holding onto that should belong to someone else? Every task you refuse to let go of is a development opportunity you're denying someone on your team.

**"How well do you feel you know the day-to-day challenges of writing, deploying, and supporting code on your team?"**

> **[SRE Lens]** For SRE managers, expand this: Do you know what the on-call experience actually feels like? When was the last time you were paged? Do you know how long it takes to deploy a change to your team's systems? Do you know which runbooks are outdated? If you can't answer these, you've drifted too far from operational reality.

**"How often does your team mark work as completed?"**

> Cadence of completion = cadence of psychological reward. If your team goes months without marking something "done," morale will suffer, even if they're making progress.

**"When was the last time you wrote a feature, debugged a problem, or paired with a member of your team?"**

> At Senior EM level, "paired with a member of your team" is the most relevant variant. You probably shouldn't be writing features, but you should be close enough to pair occasionally.

**"Are there one or two team members who cause the bulk of negativity? What is your plan?"**

> If you can name them but don't have a plan, reread the conflict section.

**"Do your team members seem engaged with one another?"**

> Fournier's pizza test: would they stick around and socialize, or race out the door?

**"How does your team make decisions? Do you have a process for assigning decision-making responsibility?"**

> If the answer is "I make all the decisions" or "nobody knows who decides," you have a problem. See Part 2's RACI framework.

**"When was the last time you reviewed a completed project to see if it had achieved its goals?"**

> If "never," start now. See Part 2's outcome review playbook.

**"How well does your team understand why they are working on their current projects?"**

> This is the shield test. If your team can't answer "why," you're either over-shielding (no context) or under-communicating.

**"When was the last time you cut scope on a project? What did you use to determine which pieces to cut?"**

> If you've never cut scope, either you're extremely lucky or you're not managing deadlines actively enough.

---

## Quarterly Ritual: Team System Health (Part 3)

> **[Quarterly Ritual]**
>
> This complements the Part 1 quarterly ritual. Part 1 covers technical health, shipping, drama, workload, shielding, and collaboration. This covers decisions, conflict, toxicity, and project management.
>
> **Decision-Making Health:**
> - [ ] Does my team have a clear process for how decisions are made? Can every team member describe it?
> - [ ] Am I making decisions I should be delegating? Am I delegating decisions I should be making?
> - [ ] When was the last time I reviewed the outcome of a completed project? Did we learn from it?
> - [ ] Is my team data-driven? Can they point to data that influenced their last significant decision?
>
> **Conflict Health:**
> - [ ] Is there a conflict I'm aware of that I haven't addressed? How long has it been simmering?
> - [ ] Am I being kind (honest, specific, direct) or nice (vague, comfortable, unhelpful)?
> - [ ] Do I have any reports who are surprised by their performance feedback? If so, I'm not giving feedback frequently enough.
> - [ ] Am I tougher on other teams than on my own? (Check the displaced conflict anti-pattern.)
>
> **Toxicity Health:**
> - [ ] Is there anyone on my team who makes others feel unsafe? Do I have evidence?
> - [ ] Have I addressed it, or am I hoping it resolves itself?
> - [ ] Is anyone on my team hoarding information or working in isolation?
> - [ ] Does every team member feel respected — by me and by their teammates?
>
> **Project Management Health:**
> - [ ] Am I planning capacity realistically (10 weeks/quarter, minus on-call, minus sustainability)?
> - [ ] When was the last time I said "no" to a project or scope request?
> - [ ] Am I shielding my team from estimation churn, or am I relaying every estimation request?
> - [ ] Do my stakeholders understand the difference between an off-the-cuff guess and a committed estimate?

---

## Peer Reflection Prompt (Part 3)

> **[Peer Reflection Prompt]**
>
> 1. **"Think about the last project your team estimated. How far off was the estimate from reality? Now think about WHY it was off. Was the estimate wrong, or did the scope change? Did you adjust expectations when you saw it going off-track, or did you stay silent and hope?"** Most estimation failures are actually communication failures — the estimate was probably a range that got flattened into a single number, or scope crept without anyone recalculating.
>
> 2. **"Do you have a brilliant jerk on your team right now? If your immediate answer is 'no,' think harder. Sometimes brilliant jerks are people we like — the abrasiveness comes out only with people they don't respect, and you might not be seeing it."** Ask your skip-levels. Ask the most junior people on the team. The brilliant jerk's behavior is often invisible to the manager and devastating to everyone else.
>
> 3. **"When was the last time you made a decision that was unpopular with your team? How did you handle it? Did you explain your reasoning, or did you just make the call? Did you check in afterward to see how people felt about it?"** If you can't remember making an unpopular decision, either you have extraordinary alignment — or you're avoiding the hard calls.
>
> 4. **"If your team's capacity was cut in half tomorrow — you lose half your engineers — which projects would you keep and which would you drop? The ones you'd keep are your actual priorities. Does that match what your team is currently spending their time on?"** This thought experiment often reveals that teams are spreading themselves too thin across too many "important" projects, rather than focusing on the truly critical few.

---

## How GenAI Is Reshaping Team Management

> **[GenAI + Team Management]**

The team management challenges Fournier describes — staying technical, debugging dysfunction, shielding appropriately, managing conflict, dealing with toxic employees — are fundamentally human. But GenAI is changing the terrain.

**AI and Staying Technical:** AI coding assistants (Copilot, Claude Code, Cursor) are raising the bar for what "staying technical" means. When an engineering manager can use AI to prototype, review code, or understand unfamiliar systems, the excuse "I don't have time to be technical" weakens. Conversely, AI makes engineers more productive — which means teams ship more, which means managers need to keep pace with faster execution cycles.

**AI and Project Estimation:** AI is beginning to help with estimation — analyzing historical velocity data, identifying patterns in project complexity, flagging scope creep risks. But the hard part of estimation (understanding humans, predicting unknowns, managing stakeholder expectations) remains entirely human.

**AI and Team Dynamics:** AI tools can analyze communication patterns (Slack activity, PR review patterns, meeting participation) to surface signals about team health — isolation, overwork, communication silos. These are supplements to managerial observation, not replacements. The conversation about someone's behavior change still needs to happen human-to-human.

**AI and the Brilliant Jerk Problem:** As AI makes individual technical output less differentiating (everyone's more productive with AI), the "brilliant" part of the brilliant jerk becomes less valuable. The cost of the "jerk" part stays the same. AI may actually make it EASIER to address brilliant jerks because the team's technical output doesn't drop as much when one person is managed out — AI closes the productivity gap.

**The meta-question:** As AI handles more routine technical and administrative work, managers have fewer excuses for avoiding the uncomfortable, uniquely human aspects of their job: difficult conversations, conflict resolution, career development, team culture building. AI gives you time back — the question is whether you'll use it for the hard work of management or fill it with more comfortable technical work.

**Further reading for Chapter 5:**
- [*The Fearless Organization* by Amy Edmondson](https://fearlessorganization.com/) — the definitive work on psychological safety
- [*The Goal* by Eliyahu Goldratt](https://www.goodreads.com/book/show/113934.The_Goal) — Theory of Constraints applied to operations, directly relevant to "not shipping" diagnosis
- [*Turn the Ship Around!* by L. David Marquet](https://www.goodreads.com/book/show/16158601-turn-the-ship-around) — leader-leader model for pushing decision authority down
- [*Crucial Conversations* by Patterson et al.](https://www.goodreads.com/book/show/15014.Crucial_Conversations) — practical framework for high-stakes, high-emotion conversations
- [*Software Estimation: Demystifying the Black Art* by Steve McConnell](https://www.goodreads.com/book/show/93891.Software_Estimation) — the most rigorous treatment of estimation in software
- [*Wardley Maps* by Simon Wardley](https://medium.com/wardleymaps) — strategic situational awareness framework (free online)
- [*An Elegant Puzzle* by Will Larson, Ch. 5](https://press.stripe.com/an-elegant-puzzle) — covers team sizing, organizational design, and managing technical quality
- [Google's Project Aristotle](https://rework.withgoogle.com/guides/understanding-team-effectiveness/) — data-driven research on team effectiveness and psychological safety
- [*Accelerate* by Forsgren, Humble, Kim](https://www.goodreads.com/book/show/35747076-accelerate) — DORA metrics research connecting deployment practices to team performance
