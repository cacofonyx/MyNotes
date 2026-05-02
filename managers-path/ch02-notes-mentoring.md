# Chapter 2: Mentoring

> **The Manager's Path** — Camille Fournier
> *A Guide for Tech Leaders Navigating Growth and Change*

Fournier positions mentoring as the **first act of people management** — often unofficial, often unplanned, but foundational. This chapter covers mentoring interns, new hires, and technical/career mentoring, and introduces the "Alpha Geek" anti-pattern. For a Senior EM, the chapter matters in two ways: (1) you design and oversee mentoring programs for your teams, and (2) the three core skills Fournier identifies (listening, communicating, calibrating) are the same skills you use daily at scale.

## Table of Contents

- [The Importance of Mentoring to Junior Team Members](#the-importance-of-mentoring-to-junior-team-members)
- [Being a Mentor](#being-a-mentor)
  - [Mentoring an Intern](#mentoring-an-intern)
    - [Listen Carefully](#listen-carefully)
    - [Clearly Communicate](#clearly-communicate)
    - [Calibrate Your Response](#calibrate-your-response)
  - [Ask the CTO: Mentoring a Summer Intern](#ask-the-cto-mentoring-a-summer-intern)
  - [Mentoring a New Hire](#mentoring-a-new-hire)
  - [Technical or Career Mentoring](#technical-or-career-mentoring)
- [Good Manager, Bad Manager: The Alpha Geek](#good-manager-bad-manager-the-alpha-geek)
- [Tips for the Manager of a Mentor](#tips-for-the-manager-of-a-mentor)
- [Key Takeaways for the Mentor](#key-takeaways-for-the-mentor)
  - [Be Curious and Open-Minded](#be-curious-and-open-minded)
  - [Listen and Speak Their Language](#listen-and-speak-their-language)
  - [Make Connections](#make-connections)
- [Assessing Your Own Experience](#assessing-your-own-experience)
- [Quarterly Ritual: Mentoring Health Check](#quarterly-ritual-mentoring-health-check)
- [Peer Reflection Prompt](#peer-reflection-prompt)
- [How GenAI Is Reshaping Mentoring](#how-genai-is-reshaping-mentoring)

**Block types in this chapter:** [Deep Dive] [Insight] [SRE Lens] [Interview Angle] [Leader's Playbook] [Anti-Pattern] [Script] [Scenario] [Senior EM vs. Director] [Red Flags] [Mental Model] [The Shadow Side] [Go Deeper] [Influence Without Authority] [Cross-Functional Play] [Quarterly Ritual] [Peer Reflection Prompt]

---

## The Importance of Mentoring to Junior Team Members

Mentors are commonly assigned to junior team members — new hires, interns. In healthy organizations, it's an opportunity for both parties: the mentor practices having responsibility for another person; the mentee gets focused, individual attention.

**Fournier's personal anecdote:** Her first serious mentoring experience was as an intern at Sun Microsystems, working on JVM tools. Her mentor Kevin, a senior engineer, "made time for me. Instead of showing me a desk and leaving me to figure out what exactly I needed to do, Kevin took the time to discuss projects with me, to sit with me at the whiteboard, to go through the code together. I knew what I was expected to get done, and when I got stuck, I could ask him for help."

> "That summer was critical for my development as a software engineer, because under his guidance I began to see that I could actually do real-world work and that I was capable of being a productive employee."

> **[Insight]** Fournier's Kevin anecdote reveals what makes mentoring powerful: it's not the knowledge transfer — it's the **confidence transfer**. Kevin didn't just teach Fournier technical skills; he showed her she was "capable of being a productive employee." For a Senior EM, this reframes what you're optimizing for when you design mentoring programs. The question isn't "Did the mentee learn X technology?" — it's "Did the mentee come out believing they can contribute meaningfully here?" That belief is what drives retention, engagement, and long-term performance.

---

## Being a Mentor

Fournier frames mentoring as a **safe way to practice management**. "It's unlikely that you'll get fired for being a bad mentor." The worst outcomes: (a) the mentee drains your coding time, or (b) you do such a poor job that good talent has a bad experience and doesn't join or leaves early.

She warns against the bad mentor archetypes: those who "ignore their charges, waste their time with trivial projects, or, worst of all, intimidate and belittle them out of ever wanting to join the organization."

> **[SRE Lens]** SRE teams have a particular mentoring challenge: the on-call component. A new SRE hire isn't just learning code and systems — they're learning how to respond under pressure, how to triage ambiguous production alerts at 2 AM, how to communicate during an incident. Mentoring in SRE needs to explicitly include **operational apprenticeship**: shadow on-call shifts, co-handling incidents with the mentor driving and explaining their reasoning, and progressive responsibility (primary on-call only after the mentor judges readiness, not after a fixed calendar date).

### Mentoring an Intern

Fournier identifies three core management skills that mentoring an intern develops:

#### Listen Carefully

> "Listening is the first and most basic skill of managing people. Listening is a precursor to empathy, which is one of the core skills of a quality manager."

Listening means more than hearing words — it's interpreting body language, tone, whether they're looking you in the eye, smiling, frowning, sighing. "These small signals give you a clue as to whether he feels understood or not."

Key practices:
- Be prepared to say anything complex a few times, in different ways
- If you don't understand something, repeat the question differently and let them correct you
- Use whiteboards to draw diagrams
- Remember you're in a position of power — the mentee is probably nervous, trying not to look stupid, and may not ask questions even when confused

> "The odds of you spending all of your time answering questions are slim compared to the odds that your intern will go off in the absolute wrong direction because he didn't ask enough questions."

> **[Deep Dive: Active Listening as a Senior EM]**
>
> Fournier's listening advice is written for first-time mentors, but the skill only becomes more critical — and more difficult — at senior levels. As a Senior EM:
>
> **The challenge scales:** You're no longer listening to one mentee — you're listening to multiple managers, tech leads, and senior ICs, each with their own communication style. Some are direct, some hint, some avoid conflict, some catastrophize. You need to calibrate your listening per person.
>
> **The power dynamic intensifies:** When you were a mentor, the intern knew you were senior. Now, as a Senior EM, people filter what they tell you even more aggressively. "Everything is fine" might mean "I'm drowning but afraid to look weak." "It's a minor issue" might mean "this is a ticking bomb I don't want to escalate."
>
> **Practical technique — The Three Levels of Listening** (from Co-Active Coaching):
> - **Level 1 (Internal):** You're listening to your own thoughts. "What should I say next?" — This is where most managers default.
> - **Level 2 (Focused):** You're fully focused on the other person's words, tone, and meaning. You're tracking what they're saying AND what they're not saying.
> - **Level 3 (Global):** You're sensing the emotional energy in the room. Is this person anxious? Relieved? Holding something back? The room itself has information.
>
> Most managers operate at Level 1. The goal is to spend most 1-1 time at Level 2 and shift to Level 3 when something feels off.
>
> **[Go Deeper]** *The Coaching Habit* (Bungay Stanier) Chapter 1: "The Kickstart Question" — the art of asking "What's on your mind?" and actually listening to the answer.

#### Clearly Communicate

If the intern asks too many questions without researching first, that's an opportunity to communicate expectations: tell them you expect self-research before asking. Ask them to explain a piece of code. Point them to documentation.

The value of breaking projects into milestones upfront: "You've taken on some of the harder thinking up front."

Walk through the breakdown with the intern: "Does it make sense to him? Listen to his questions and answer them."

> **[Mental Model: Delegation as Teaching — The "Tell, Show, Do, Review" Ladder]**
>
> Fournier describes breaking down an intern's project into milestones. This is actually a specific instance of a broader teaching framework:
>
> | Stage | What the Manager Does | When to Use |
> |-------|----------------------|-------------|
> | **Tell** | Explain what needs to be done and why | Brand new to the task, never done anything similar |
> | **Show** | Demonstrate while they watch. Walk through an example together. | They understand the theory but have never seen it done |
> | **Do** | They do it while you observe and give real-time guidance | They've seen it but haven't tried it. First attempt. |
> | **Review** | They do it independently, you review the output | They've done it once or twice, building confidence |
> | **Delegate** | They own it. You check in periodically on outcomes. | Proven competence. Trust established. |
>
> **For SRE:** This ladder applies perfectly to incident response training. Tell (explain the incident process), Show (run an incident with them observing), Do (let them drive an incident with you co-piloting), Review (they run incidents independently, you debrief after), Delegate (they're the incident commander, you're not in the room).

#### Calibrate Your Response

The intern may far outstrip expectations, struggle with simple tasks, produce fast but low quality work, or work very slowly for overly perfect output. "In the first few weeks, you're learning the frequency that you need to check in with him to provide the right adjustments."

> **[Insight]** These three skills — **listen, communicate, calibrate** — are presented as intern mentoring basics, but they are the ENTIRE job of management at every level. A Senior EM listens to their managers and teams, communicates priorities and expectations, and calibrates their involvement based on each person's needs. The only thing that changes with seniority is the *scale* and *stakes*, not the skills themselves. If you can't do these three things well, no amount of strategic thinking or org design will save you.

### Ask the CTO: Mentoring a Summer Intern

Fournier's practical checklist:

1. **Prepare for arrival.** Desk, computer, system access — all ready on day one. "There's nothing worse than showing up for your big job with nowhere to sit and no access to the systems."

2. **Have a project.** Something specific but not urgent, relevant to the team, completable by an entry-level engineer in ~half the internship duration (10-week internship → 5-week project). "Your internship program is not a way for you to get extra work done; it's a way for you to identify and attract talent."

3. **Plan a final presentation.** Gives the intern exposure, sets a clear finish line, and helps you evaluate whether to make a full-time offer. "Interns who feel like the company appreciated their work are the ones most likely to come back after they graduate."

> **[Leader's Playbook: Designing Your Team's Intern/New Grad Program]**
>
> As a Senior EM, you don't mentor interns yourself — but you design the system:
>
> 1. **Pre-select mentors deliberately.** Not whoever has the lightest sprint load. Choose people you want to develop as future leaders — mentoring is their first leadership experience. (Fournier makes this point explicitly later in the chapter.)
> 2. **Create a project bank.** Maintain a running list of 5-10 "intern-worthy" projects per team: bounded, meaningful, not on the critical path. Review quarterly.
> 3. **Structured check-ins.** Don't just assign the mentor and hope. Schedule a midpoint check with the mentor: "How is it going? What challenges?" And a separate 1-1 with the intern: "Are you getting what you need?"
> 4. **For SRE specifically:** Intern projects that work well: building an internal tool (dashboard, CLI utility, automation script), improving documentation for a system, implementing a chaos experiment under guidance, contributing to the observability platform. Projects that DON'T work: anything on-call-related, anything touching production directly, anything where failure would page someone.

---

### Mentoring a New Hire

Fournier contrasts two personal experiences:

**Bad:** Her first job out of college at "BigTechCo" — manager showed her to her office and left her alone. She didn't know how to ask for help, got discouraged, and went to grad school.

**Good:** First job after grad school — set up with a mentor who encouraged questions, did pair programming, helped her learn the codebase. "I was productive within days, and learned more in the first few months of that job than I had learned in the entire time I worked at BigTechCo."

> "I credit this almost entirely to the mentoring I got when I started."

**Key differences from intern mentoring:**
- The relationship goes on longer
- Focus is on onboarding: helping the person adjust to company life effectively
- Building *both* the mentor's and mentee's network of contacts

**Fresh eyes as a gift:** "It can be hard to remember what it was like to experience your world for the first time." New hires surface **unspoken rules** that veterans don't even notice — vacation norms, how long to struggle before asking for help, jargon. "Unspoken rules don't just make it harder for new people to join, they can also make it harder for you to do your job well."

**Onboarding documents:** Effective teams have step-by-step guides for dev environment setup, tracking systems, tools. "Mentoring a new hire by helping her work through the documents, and having her modify those documents with any surprises she encounters during onboarding, provides a powerful message of commitment."

**Network building:** "Companies are full of human networks that exist to transmit knowledge and information quickly. Bringing this person into some of your networks will help her get up to speed faster."

> "Even if you have absolutely no interest in management, it's very difficult to build a career at any company with multiple teams without building a strong network of trusted people."

> **[Anti-Pattern: The "Sink or Swim" SRE Onboarding]**
>
> SRE teams are especially prone to the BigTechCo mistake Fournier describes. The justification sounds reasonable: "We hire senior people. They should be able to figure it out." The new SRE is handed a laptop, pointed to a wiki (that's 40% outdated), and added to the on-call rotation in 4-6 weeks whether they're ready or not.
>
> **What happens:** The new hire spends their first month in a state of low-grade anxiety. They can find the code but don't understand the *why* behind architectural decisions. They're on-call for systems they've never seen in production. Their first incident is terrifying and they feel incompetent. Within 6-12 months, they're either performing below potential (because they built a fragmented mental model) or they've left.
>
> **The fix — SRE Onboarding Ladder:**
> - **Week 1-2:** Paired with a mentor for system walkthroughs. Not "read the docs" — actual live walkthroughs of production systems with the mentor explaining history, gotchas, and tribal knowledge.
> - **Week 3-4:** Shadow on-call. Sit with the on-call engineer during their shift. Join incident bridges as an observer. Ask questions afterward.
> - **Week 5-6:** Reverse-shadow: new hire is "primary" on-call with the mentor as active backup who reviews every decision. Mentor is in the room, not just on the phone.
> - **Week 7-8:** Solo on-call with mentor on secondary/backup. Mentor debriefs after the shift.
> - **The document improvement principle** from Fournier applies perfectly: every new SRE should improve at least 3 runbooks during onboarding. This teaches them AND improves the system.

> **[Scenario: The New Hire Who's "Too Senior" for Onboarding]**
>
> You hire a Staff SRE from Google. They've built planet-scale systems. Your team is excited. You assign them a mentor and a structured onboarding plan. In the first week, they push back: "I appreciate this, but I've been doing SRE for 12 years. I don't need someone holding my hand. Just point me to the code and I'll figure it out."
>
> **The temptation:** Defer to their seniority and skip the structure.
>
> **The right move:** Apply Task-Relevant Maturity (from Ch1). They have high TRM for SRE practices generally, but **zero TRM for your specific systems, your team's culture, your incident process, your unspoken rules.** Frame it this way:
>
> *"I have no doubt about your technical skills — that's why we hired you. The onboarding isn't about whether you can do SRE. It's about learning the 200 things that are specific to us that nobody writes down — the service that looks healthy but falls over under load on Fridays, the team in Platform that you need to talk to before touching the database layer, the way our incident process actually works vs. what the wiki says. Your mentor knows all of this, and the fastest way to absorb it is to lean into the onboarding, not skip it. I've seen senior people who skip it take 6 months to get fully productive. I've seen senior people who embrace it get fully productive in 6 weeks."*

> **[Senior EM vs. Director: Onboarding Responsibility]**
>
> | Dimension | Senior EM | Director |
> |-----------|-----------|----------|
> | **What you own** | The onboarding experience for your teams — content, mentors, timeline, quality | The onboarding *system* for the org — standard processes, mentor training, feedback loops |
> | **Who you onboard personally** | Your direct reports (managers, TLs) — you ARE their onboarding mentor | Your direct reports (Senior EMs) + you set the tone for how the org treats new people |
> | **Quality signal** | Time-to-productivity for new hires on your teams | Retention rate at 6 months and 12 months across the org |
> | **Improvement cycle** | Review onboarding feedback after each new hire | Quarterly review of onboarding NPS, time-to-first-commit, time-to-first-on-call |

---

### Technical or Career Mentoring

Fournier is brief here — this type is "usually not directly related to the path of management."

**Best mentoring relationships:** Evolve naturally in the context of larger work. A senior engineer mentoring a junior on the team — they work on problems together. Senior gets better code from the mentee; junior gets hands-on instruction. "This type of mentoring is usually not a formal relationship and may be an expected part of the job for senior engineers."

**Formal cross-team programs:** "Often an ambiguous obligation for both the mentor and the mentee." Can enhance networks but frequently fail because there's no structure or guidance.

**When you are a mentor:** Be explicit about expectations (prepared questions, time commitment). Be honest with your answers — "There's no point in being a mentor to a relative stranger if you can't at least use that professional distance to offer him the kind of candid advice that he may not get from his manager or coworkers." It's also OK to say no.

**When you are a mentee:** Come prepared. "You owe it to this person not to waste her time." Consider whether you actually need a mentor or a "friend, therapist, or coach."

> **[Insight]** Fournier's distinction between mentoring, friendship, therapy, and coaching is deceptively important. Many mentoring relationships fail because the mentee actually needs something different:
>
> | What You Need | What It Looks Like | Who Provides It |
> |--------------|-------------------|----------------|
> | **Mentoring** | "How do I navigate the promotion process at this company?" | Someone who's done it, ideally in the same org |
> | **Coaching** | "I know I should delegate more, but something holds me back" | A trained coach who helps you uncover your own answers |
> | **Sponsorship** | "I need someone to advocate for me in rooms I'm not in" | A senior leader who stakes their credibility on your behalf |
> | **Friendship** | "I need someone to vent to who understands this industry" | A peer at another company, a former colleague |
> | **Therapy** | "Work anxiety is affecting my sleep and relationships" | A licensed professional |
>
> As a Senior EM, you need ALL of these, not just mentoring. And when your reports say "I want a mentor," probe what they actually need — it might be one of the other four.

> **[Cross-Functional Play: Mentoring Across the SRE↔Product Boundary]**
>
> Some of the most valuable mentoring relationships cross functional boundaries. Consider:
> - Pair a senior SRE with a product engineer as mutual mentors. The SRE teaches operational thinking; the product engineer teaches product/customer empathy.
> - Have an SRE join a product team's design review as a "reliability mentor" — not to gate, but to teach the team how to think about failure modes.
> - Encourage your SREs to mentor product engineers on observability, and have product engineers mentor SREs on user behavior and business metrics.
>
> These cross-boundary relationships reduce the "us vs. them" dynamic that plagues SRE↔Product interactions and build the shared understanding that makes collaboration natural.

---

## Good Manager, Bad Manager: The Alpha Geek

This is one of the most memorable sections in the book — Fournier's portrait of a common and destructive archetype.

**The Alpha Geek profile:**
- Driven to be the best engineer on the team
- Always has the right answer, solves all hard problems
- Values intelligence and technical skill above all other traits
- Believes technical superiority should determine who makes decisions
- Can't deal with dissent, easily threatened by anyone who might upstage her
- "Tries to create a culture of excellence, but ends up creating a culture of fear"

**At their best:** Inspirational to younger developers. Deep knowledge of systems. Can design great systems. "Alpha geeks have a lot to teach you, if they want to."

**At their worst:** "Can't let anyone else get any glory without claiming some of it for themselves." Origin of all good ideas, had no part in bad ideas. "Gleefully point out your ignorance." Rigid about how things should be done. Hides information to maintain their edge. "Absolutely hate it when they have to take direction from anyone they don't respect intellectually."

**The mentoring connection:** The alpha geek habit starts showing up when engineers first become mentors. Fournier offers a self-diagnostic:

> "Do you view yourself as an engineer who does not pull any punches and always says exactly what you think? Are you eagerly seeking out the gotcha, hunting for mistakes, reluctant to admit that someone else has had a good idea or has written good code?"

**Management implications:** "Alpha geeks make absolutely terrible managers, unless they can learn to let go of their identity as the smartest person in the room."

> "If you're ever in the position to promote people to management, be very, very careful in giving your alpha geeks team management positions, and keep a close eye on the impact they have in that role."

> **[Deep Dive: The Alpha Geek in SRE — An Especially Dangerous Variant]**
>
> SRE attracts alpha geeks more than most disciplines because the work rewards deep technical knowledge, quick diagnosis under pressure, and being "right" about system behavior. The SRE alpha geek is the person who:
>
> - During incidents, takes over from junior on-call engineers instead of coaching them
> - Writes post-mortems that subtly blame others ("if the deployment process had been followed correctly...")
> - Dismisses new tooling or approaches with "that won't work at our scale" without evaluation
> - Gatekeeps access to production systems because "only I understand this well enough"
> - Makes other engineers feel stupid for not knowing the history of a system that was built 5 years ago
>
> **Why it's especially dangerous in SRE:** SRE culture values technical depth and war stories. An alpha geek in SRE can disguise their behavior as "high standards" and "operational rigor." But the damage is real: junior engineers stop participating in incident response, knowledge stays siloed in the alpha geek's head (single point of failure!), and the team's bus factor drops to 1.
>
> **The paradox:** The alpha geek often IS your most technically skilled person. You need their knowledge. You can't afford to lose them. But you also can't let them poison the team culture.

> **[Script: Coaching an Alpha Geek Report]**
>
> Your most senior SRE is technically brilliant but creating a fear-based team dynamic. In your 1-1:
>
> *"I want to talk about something I've been observing, and I'm raising it because I think it's holding the team back from where we both want it to be.*
>
> *You have the deepest technical knowledge on this team — that's not in question. But I've noticed a pattern: when someone proposes an approach in design review, you tend to immediately point out why it won't work, before exploring what might be good about it. Last week, [junior SRE] proposed a monitoring approach and you said 'that's naive — it won't scale past 10K requests.' He stopped contributing for the rest of the meeting.*
>
> *Here's what concerns me: we need [junior SRE] and others to develop their own judgment. If they never get to propose ideas and learn from the outcome, they'll never grow. And we can't afford to have all of our system knowledge in one person's head — that's a reliability risk.*
>
> *I'm not asking you to lower your standards. I'm asking you to change your approach. Instead of 'that won't work,' try 'What happens at 10K requests per second? Walk me through it.' You'll get the same quality outcome, but the junior engineer will learn through your question instead of shutting down from your statement.*
>
> *Can we try that for the next month and see how it changes the dynamic?"*
>
> **Why this works:** Ties the behavior to a shared goal (team growth), acknowledges their value, frames the change as a technique upgrade rather than a character flaw, and proposes a time-boxed experiment.

> **[The Shadow Side: Technical Excellence Becomes Technical Gatekeeping]**
>
> Every Senior EM values technical excellence — it's what drew us to engineering in the first place. The shadow side: your standards become a weapon.
>
> **How to tell the difference:**
> - **Technical excellence:** "Let's think through the failure modes before we commit to this design." → Opens discussion, invites others.
> - **Technical gatekeeping:** "This design is clearly wrong. Let me show you how to do it properly." → Shuts down discussion, asserts dominance.
>
> - **Technical excellence:** "I'd like to see more test coverage on this critical path. Here are some edge cases to consider." → Specific, actionable, constructive.
> - **Technical gatekeeping:** "This isn't production-ready. You clearly don't understand how this system works." → Vague, demeaning, personal.
>
> **The self-test:** After you give technical feedback, does the other person walk away more capable and more confident? Or do they walk away diminished and dependent on you? The first is excellence; the second is gatekeeping.

> **[Interview Angle]**
>
> A very common Director/Senior EM interview question: "Tell me about a time you managed a brilliant but difficult engineer."
>
> **Strong answer structure:**
> 1. **Context:** "I had a Staff SRE who was the most technically capable person on the team — they'd designed our core monitoring platform — but they were creating a culture where junior engineers were afraid to contribute."
> 2. **Diagnosis:** "I realized the issue wasn't their technical standards — those were appropriate. It was their *delivery*. They equated being right with being blunt, and didn't see the impact."
> 3. **Action:** "I used SBI feedback in a 1-1, with specific examples. I acknowledged their value, then proposed a concrete behavior change: asking questions instead of making declarations."
> 4. **Result:** "Over two months, the dynamic shifted. The Staff SRE actually started enjoying helping juniors grow. Our incident participation from junior engineers doubled."
> 5. **The nuance:** "I was prepared for it not to work. I had a plan B — restructuring responsibilities to limit their direct interaction with juniors while preserving their technical impact. But it didn't come to that."

---

## Tips for the Manager of a Mentor

This section is directly relevant to you as a Senior EM.

**"What you measure, you improve."** When assigning a mentor, figure out what you're hoping to achieve and find the person who can meet those goals.

**Common failures of mentoring programs:**
- Mentor and mentee given no guidance beyond "you've been matched"
- If the mentor isn't engaged or is too busy → disappointment for mentee
- If the mentee doesn't know how to ask for help → "forced socializing and a waste of time"

**Treat mentoring as real work:**
- Recognize it's an additional responsibility — mentor's productivity may slow during the period
- Don't assign someone already on a time-sensitive project
- "Look for someone that you believe can succeed in the role, and who wants to distinguish herself beyond her coding ability"

**Three pitfalls Fournier calls out:**

1. **Viewing mentoring as low-status "emotional labor"** — Dismissing it as less important than writing code. "Emotional labor is often dismissed as less important work... I'm not suggesting that you should pay people extra money to serve as mentors, but they need to be recognized for the work they put in."

2. **Assuming "like" must mentor "like"** — Don't default to women mentoring women, PoC mentoring PoC only. "As a woman in tech, I personally get tired of the only mentoring being focused around lines of diversity." Match the best mentor for the *situation*, not the demographic.

3. **Failing to use mentoring as a leadership development opportunity** — "Use this opportunity to reward and train future leaders on your team."

> **[Insight]** The "emotional labor" callout is important and often missed by engineering managers. In most eng orgs, the people who mentor, onboard, organize team events, and do "glue work" (Tanya Reilly's term) are disproportionately women and underrepresented minorities. If you reward only "hard technical output" in performance reviews, you're systematically penalizing the people who make your team functional. As a Senior EM, **explicitly recognize mentoring in performance evaluations**. Make it a first-class contribution, not an unspoken expectation.

> **[Leader's Playbook: Setting Up Mentoring Relationships That Actually Work]**
>
> 1. **Define the goal** before matching people. Is it onboarding speed? Cultural integration? Technical skill building? Career growth? Different goals require different mentors.
> 2. **Brief both parties.** Give the mentor explicit expectations: "Meet weekly for 30 min, focus on X, check in with me at midpoint." Give the mentee permission to ask for what they need.
> 3. **Check in at the midpoint.** Ask both independently: "Is this working? What would make it better?" Adjust or rematch if needed.
> 4. **Recognize the mentor publicly** at the end: "Alex did an outstanding job mentoring our new hire — they were productive in half the usual ramp-up time."
> 5. **Limit tenure.** Mentoring relationships should have a defined end point (3 months for onboarding, the summer for interns). Open-ended mandated mentoring becomes stale.

> **[Mental Model: The Dreyfus Model of Skill Acquisition — Matching Mentor to Mentee]**
>
> The Dreyfus model describes five stages of skill development:
>
> | Stage | Characteristics | What They Need from a Mentor |
> |-------|----------------|------------------------------|
> | **Novice** | Follows rules rigidly, needs clear instructions | "Here is exactly what to do and how" — structured guidance |
> | **Advanced Beginner** | Can handle simple tasks, starts to see patterns | "Here's why we do it this way" — context and reasoning |
> | **Competent** | Can plan their own work, handles routine situations | "What do you think you should do?" — coached independence |
> | **Proficient** | Sees the big picture, knows when rules don't apply | "Let me challenge your approach" — debate and refinement |
> | **Expert** | Operates on intuition, transcends rules | Doesn't need a mentor — needs a sparring partner or a coach |
>
> **The matching principle:** A mentor should be 1-2 stages above the mentee — close enough to remember the mentee's challenges, far enough ahead to guide effectively. An Expert mentoring a Novice is often a bad pairing — the Expert has internalized so much that they can't explain their reasoning in terms the Novice can understand. A Competent person mentoring a Novice is often ideal.
>
> **For SRE:** An SRE who's been on-call for a year (Competent) is often a better incident response mentor for a new hire (Novice) than a Staff SRE who's been doing it for a decade (Expert). The one-year person still remembers the fear and confusion of their first page.

---

## Key Takeaways for the Mentor

### Be Curious and Open-Minded

> "When we close our minds and stop learning, we start to lose the most valuable skill for maintaining and growing a successful technical career."

Mentoring provides "a great opportunity to cultivate curiosity and see the world through fresh eyes." New people asking questions can surface hidden patterns and assumptions worth questioning.

> "While many people think creativity is about seeing new things, it's also about seeing patterns that are hidden to others."

> **[SRE Lens]** In SRE, the "fresh eyes" phenomenon is extremely powerful during onboarding. A new SRE will ask "Why does this service have three different monitoring systems?" or "Why is this runbook 47 steps long?" — questions that veterans stopped asking years ago because the answer was "historical reasons." These questions are gold. They're pointing at technical debt, operational complexity, and toil that the team has normalized. Build a practice of capturing new hire questions and turning them into improvement backlog items.

### Listen and Speak Their Language

> "Senior engineers can develop bad habits, and one of the worst is the tendency to lecture and debate with anyone who does not understand them or who disagrees with what they are saying."

To work with a newcomer, "you must be able to listen and communicate in a way that person can understand, even if you have to try several times to get it right."

### Make Connections

> "Your career ultimately succeeds or fails on the strength of your network."

> "Don't abuse the mentoring relationship... your career is long and the tech world can be very small, so treat the other person well."

> **[Influence Without Authority: Mentoring as Strategic Network Building]**
>
> Fournier frames networking as career self-interest, but there's a deeper play for Senior EMs: **mentoring creates future allies across the organization.**
>
> The junior SRE you mentor today might become a Staff engineer on a product team in 3 years — and when you need that team to prioritize reliability work, you have a trusted relationship. The new hire you onboard well might become a manager on another team — and when you need cross-team collaboration, the trust is already there.
>
> This isn't manipulation — it's building the organizational fabric that makes everything else possible. Directors who have deep, trust-based relationships across the org can move mountains. Directors who only have relationships within their own org struggle to influence anything.

---

## Assessing Your Own Experience

Fournier's self-reflection questions:
- Does your company have an internship program? Can you mentor an intern?
- How does your company think about onboarding? Do you assign mentors?
- Have you had a great mentor? What made them great?
- Have you had a mentoring relationship that didn't work? What lessons can you apply?

---

## Quarterly Ritual: Mentoring Health Check

> **[Quarterly Ritual]**
>
> **Monthly (quick pulse):**
> - [ ] Every new hire in the last 3 months has an assigned mentor who is actively meeting with them
> - [ ] No one has been added to on-call rotation without completing the onboarding ladder
> - [ ] I've checked in with at least one mentor-mentee pair to see how it's going
>
> **Quarterly (the audit):**
> - [ ] Review time-to-productivity for recent hires. Is it improving, stable, or degrading?
> - [ ] Review 6-month retention rate. Are new hires staying?
> - [ ] Review mentor feedback: Are mentors feeling supported, or overwhelmed and unrecognized?
> - [ ] Check: Is mentoring work reflected in performance reviews for those who do it?
> - [ ] Review onboarding docs: When were they last updated? (If >6 months ago, assign the next new hire to update them.)
> - [ ] Am I personally mentoring or sponsoring at least one person? (Your own development requires it too.)
>
> **Annually:**
> - [ ] Review the full onboarding experience end-to-end. Do a "new hire experience audit" — walk through the first 30 days as if you were new. Where does it break?
> - [ ] Evaluate whether your team has alpha geek dynamics. Ask skip-level: "Do you feel comfortable proposing ideas that disagree with the most senior person on your team?"

---

## Peer Reflection Prompt

> **[Peer Reflection Prompt]**
>
> 1. **"Who mentored you into the leader you are today? Have you told them?"** Seriously — go send that message. Mentoring is largely thankless work, and hearing the impact years later is one of the most powerful things a mentor can experience. And reflecting on what they did will clarify what you should be doing for others.
>
> 2. **"Do you have any alpha geek tendencies yourself?"** Be honest. The alpha geek is seductive because it's rooted in a real strength (technical excellence). Before you could diagnose it in others, you need to rule it out in yourself. Ask a trusted peer: "Have you ever seen me shut someone down in a meeting? Claim credit I shouldn't have? Gatekeep knowledge?" Their answer might surprise you.
>
> 3. **"How many people on your team could you lose tomorrow and the team would still function?"** If the answer is "there are one or two people who, if they left, everything would fall apart" — those people are single points of failure, and the solution is mentoring. Knowledge that exists in only one head is an operational risk, not a competitive advantage. What's your plan to spread that knowledge?
>
> 4. **"When was the last time you were genuinely taught something by someone more junior than you?"** Fournier says mentoring is a two-way street — the mentor learns from the mentee's fresh perspective. If you can't remember the last time a junior person changed your mind or taught you something, you may have stopped listening.

---

## How GenAI Is Reshaping Mentoring

> **[GenAI + Management]**

**AI as a "first responder" mentor:** New hires increasingly use AI tools (ChatGPT, Copilot, internal AI assistants) as their first source for questions — "How do I set up the dev environment?" "What does this error mean?" "Where's the documentation for X?" This reduces the trivial question burden on human mentors, freeing them for the higher-value mentoring: context, culture, judgment, relationships.

**AI and onboarding documentation:** AI can help maintain onboarding docs — detecting when linked resources are broken, identifying gaps based on common new hire questions, even generating first drafts of walkthroughs from code and config files. Fournier's principle that "new hires should update onboarding docs" still applies — but AI can accelerate the update process.

**AI and the Alpha Geek:** AI levels the playing field in one important way — junior engineers with good AI-assisted research skills can now arrive at technical answers faster, reducing the alpha geek's information advantage. This shifts the alpha geek's value from "having the answers" to "having the judgment" — which is a healthier dynamic. But alpha geeks who feel threatened by this shift may become even more defensive.

**AI doesn't replace human mentoring:** AI can answer "how does this system work?" It cannot answer "what's the unspoken political dynamic between our team and the platform team?" or "is this a company where I should advocate loudly for promotion, or wait to be noticed?" The human, contextual, cultural dimensions of mentoring are irreplaceable and become MORE valuable as AI handles the technical Q&A.

**The risk:** Over-reliance on AI for onboarding creates engineers who know the *what* but not the *why*. They can get code working but don't understand the history, the tradeoffs, the cultural context. Human mentoring bridges that gap.

**Further reading:**
- [*The Coaching Habit* by Michael Bungay Stanier](https://boxofcrayons.com/the-coaching-habit-book/) — transforms your mentoring conversations from advice-giving to question-asking
- [Tanya Reilly, "Being Glue"](https://noidea.dog/glue) — essential reading on the "emotional labor" problem Fournier raises, and how to value it
- [*Thanks for the Feedback* by Stone & Heen](https://www.penguinrandomhouse.com/books/313485/thanks-for-the-feedback-by-douglas-stone-and-sheila-heen/) — the mentee's perspective on receiving and using feedback effectively
- [Google re:Work — Onboarding](https://rework.withgoogle.com/guides/hiring-shape-the-candidate-experience/) — data-driven onboarding practices
- [*An Elegant Puzzle* by Will Larson](https://press.stripe.com/an-elegant-puzzle) — Chapter on "Onboarding" for systems-level thinking about new hire experience
- [SRE Onboarding at LinkedIn](https://engineering.linkedin.com/blog/topic/sre) — practical example of SRE-specific onboarding at scale
