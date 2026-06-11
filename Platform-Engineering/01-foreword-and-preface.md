# Foreword and Preface

## Foreword — Nicole Forsgren, PhD

The foreword is written by **Nicole Forsgren** — lead author of *Accelerate*, creator of the DORA metrics, and Partner Research Manager at Microsoft. Her endorsement signals that this book sits in the lineage of the DevOps/DORA research tradition, extending it into the platform engineering space.

Forsgren frames platform engineering as "a crucial foundation for boosting agility, speeding up time to market, and enhancing overall product quality." She notes a "glaring lack of resources" guiding organizations through this work — this book fills that gap.

She highlights specific chapters she found valuable:
- **Chapter 4** — breakdown of roles and responsibilities, interview strategies, engineering ladders
- **Chapter 5** — why platforms should be treated as products (discovery, roadmaps, migration plans)
- **Chapter 10** — the power-interest grid for evaluating workplace dynamics and stakeholder management

> **[Comparison: The DORA → Platform Engineering Lineage]**
>
> Forsgren's involvement is meaningful context. The intellectual lineage runs: Lean Manufacturing → DevOps (The Phoenix Project, DevOps Handbook) → DORA Metrics (Accelerate) → Platform Engineering (this book). Each builds on the previous:
> - DevOps said "break down silos between dev and ops"
> - DORA proved that certain capabilities (CI/CD, trunk-based dev, monitoring) predict organizational performance
> - Platform Engineering says "here's how to *structurally provide* those capabilities at scale, as products, so teams don't each have to build them independently"
>
> Forsgren's endorsement confirms this positioning: platform engineering isn't a departure from DevOps/DORA — it's the organizational mechanism for delivering DORA capabilities at scale.

---

## Preface — A Note from Camille

Camille Fournier (author of *The Manager's Path*) shares the origin story. In 2017, she became head of platform engineering and met co-author Ian Nowland, freshly arrived from Amazon/AWS. Together, they turned around a platform organization from the reputation of "builds what they think is fun without concern for customer needs or stability" into "a mature, well-operated, customer-focused platform team."

**What each author brought:**
- **Ian (from Amazon/AWS):** Six-pagers for design and planning, hiring systems engineers, stronger operational practices, skepticism about user-level networking
- **Camille:** Product management focus, decisive leadership, goal setting, willingness to change things in pursuit of organizational excellence

The key confession in the preface — and it's honest in a way that sets the book's tone:

> *"The truth is that most platform engineering teams we hear about have that same reputation... building tech for the fun of it, without care for who needs it, and often without even the operational maturity that such critical work deserves. And this is because doing platform engineering is hard!"*

The authors frame the core challenges bluntly:
- Now that we know about product management, we have no excuse to keep building things just because they seem fun
- We can't hide behind planning challenges to excuse inability to execute
- If we want to provide critical systems, we must care about operational stability

---

## Who This Book Is For

Three audiences, in order of specificity:

1. **Platform engineering leaders** — senior engineers, architects, product/program/engineering managers in organizations that engineer and operate platforms. They understand intuitively that platforms aren't just cloud automation, but lack a clearer definition and practices.

2. **Broader technology leadership** — CTOs, SVPs, "product engineering" leaders who ask questions like:
   - "Why is the platform organization so big when we also have AWS?"
   - "Why does our platform have all this headcount but still move so slowly?"
   - "Why didn't our adoption of [cloud/SRE/developer experience] solve this?"

3. **Anyone interested in making platform engineering work** — startups wondering when to start, big companies transitioning from infrastructure to platform engineering, or anywhere in between.

> **[Organizational Reality: The Questions Leadership Asks]**
>
> Those three leadership questions are worth internalizing because they reflect the default skepticism platform teams face from product engineering leaders. If you run a platform team, you will eventually need to answer all three convincingly:
>
> - "Why so big when we have AWS?" → Because AWS gives you primitives, not products. Someone has to turn those primitives into something your developers can actually use without becoming part-time cloud engineers. (Chapter 1's swamp argument)
> - "Why so much headcount but slow?" → Possibly because you're running a feature shop, not a platform. You're doing the same work 50 teams would do, just centrally — instead of building automation that eliminates the work. (Chapter 1's Stage 2 vs Stage 3)
> - "Why didn't cloud/SRE/DevEx solve this?" → Because those are ingredients, not the meal. You need the organizational discipline of *product thinking applied to infrastructure* to turn capabilities into coherent platforms. (Chapter 2's four pillars)

---

## How to Read This Book

The book has three parts:

| Part | Chapters | Focus |
|------|----------|-------|
| **I. The What and Why** | Ch 1–2 | What platform engineering is, why it matters, the four pillars |
| **II. Practices** | Ch 3–10 | The "how" — detailed advice on getting started, teams, product thinking, operations, planning, architecture, migrations, stakeholders |
| **III. What Does Success Look Like?** | Ch 11–14 | Stories of success (often partial success), what good outcomes look like |

The authors note that Part II "is the meat of the book" — eight chapters of detailed practical advice. They explicitly say this book is **not** about underpinning technologies — it's about organizational practices needed to succeed.

---

## Key Context from Acknowledgments

The book was technically reviewed by **Tanya Reilly** (author of *The Staff Engineer's Path*), **Niall Murphy** (co-editor of the Google SRE book), **James Turnbull** (DevOps pioneer, contributes to Chapter 3), and several other industry practitioners. This review team signals the book's positioning at the intersection of SRE, staff engineering, and DevOps leadership.
