# The Manager's Path — Leadership Operating Manual

Notes on **The Manager's Path** by Camille Fournier, tailored for **SRE leadership** (Senior EM → Director track).

Not a book summary. A leadership operating manual with 18 block types: actionable playbooks, scripts, scenarios, interview angles, mental models, anti-patterns, and SRE-specific adaptations.

## Chapters

| # | Chapter | File(s) | Lines |
|---|---------|---------|-------|
| 1 | Management 101 | `ch01-notes-management-101.md` | 652 |
| 2 | Mentoring | `ch02-notes-mentoring.md` | 463 |
| 3 | Tech Lead | `ch03-notes-tech-lead.md` | 391 |
| 4 | Managing People | `ch04-notes-managing-people.md` | 444 |
| 5 | Managing a Team | `ch05-notes-managing-a-team-part{1,2,3}.md` | 1,317 |
| 6 | Managing Multiple Teams | `ch06-notes-managing-multiple-teams-part{1,2}.md` | 521 |
| 7 | Managing Managers | `ch07-notes-managing-managers-part{1,2,3}.md` | 657 |
| 8 | The Big Leagues | `ch08-notes-the-big-leagues-part{1,2,3}.md` | 570 |
| 9 | Bootstrapping Culture | `ch09-notes-bootstrapping-culture-part{1,2}.md` | 384 |
| 10 | Conclusion | `ch10-notes-conclusion.md` | 79 |
| | **Total** | **18 files** | **5,478** |

## Merging Split Chapters

Parts can be concatenated into single files:

```bash
cd TMP/notes
cat ch05-notes-managing-a-team-part{1,2,3}.md > ch05-notes-managing-a-team.md
cat ch06-notes-managing-multiple-teams-part{1,2}.md > ch06-notes-managing-multiple-teams.md
cat ch07-notes-managing-managers-part{1,2,3}.md > ch07-notes-managing-managers.md
cat ch08-notes-the-big-leagues-part{1,2,3}.md > ch08-notes-the-big-leagues.md
cat ch09-notes-bootstrapping-culture-part{1,2}.md > ch09-notes-bootstrapping-culture.md
```

Note: The merging to be done manually. Not just as concatenating files mentioned above.

## Block Types

| Block | Purpose |
|-------|---------|
| `[Deep Dive]` | Concrete how-to tactics |
| `[Insight]` | What Fournier really means |
| `[SRE Lens]` | SRE leadership application |
| `[Interview Angle]` | EM/Director interview prep |
| `[Leader's Playbook]` | Step-by-step actions |
| `[Anti-Pattern]` | What failure looks like |
| `[Script]` | Actual words to say |
| `[Scenario]` | SRE situational walkthroughs |
| `[Senior EM vs. Director]` | Level comparison tables |
| `[Mental Model]` | Named thinking frameworks |
| `[The Shadow Side]` | When strengths become liabilities |
| `[Red Flags]` | Early warning signals |
| `[Cross-Functional Play]` | Working with Product, Security, etc. |
| `[Influence Without Authority]` | Impact outside your org |
| `[First 90 Days]` | New role playbook |
| `[Go Deeper]` | Book/resource references |
| `[Quarterly Ritual]` | Management operating cadence |
| `[Peer Reflection Prompt]` | Self-examination questions |
