# High Output Management — Andy Grove

Detailed, self-contained notes on *High Output Management* (1983, updated 1995) by Andrew S. Grove, co-founder and CEO of Intel.

These notes are written for a **Senior Engineering Manager in SRE** targeting Director-level growth. Each chapter includes Grove's original context and key quotes, deep interpretations, modern applications (DevOps, platform engineering, SLOs), SRE-specific lens, AI/automation impact, practical toolkits, and references to related frameworks and books.

## Notes

### Front Matter
| File | Topic |
|------|-------|
| [Foreword](foreword-notes.md) | Ben Horowitz's 2015 foreword — Grove the person, the output equation preview, the optimism paradox |
| [Introduction](introduction-notes.md) | Grove's 1995 update — globalization, the information revolution, the micro CEO, managing your own career |

### Part I — The Breakfast Factory (Production)
| File | Topic |
|------|-------|
| [Ch1 Part 1](ch01-notes-basics-of-production-part1.md) | Limiting step, time offsets, three production operations, capacity trade-offs, SLOs as the production triad, incident response as production flow |
| [Ch1 Part 2](ch01-notes-basics-of-production-part2.md) | Continuous operations, three inspection types, inventory and opportunity at risk, adding value, lowest-value-stage detection, criminal justice system example |
| [Ch2 Part 1](ch02-notes-managing-the-breakfast-factory-part1.md) | Five daily indicators, paired indicators, black box model, leading/linearity/trend/stagger indicators, build-to-order vs. build-to-forecast |
| [Ch2 Part 2](ch02-notes-managing-the-breakfast-factory-part2.md) | Gate vs. monitor inspections, the embassy visa factory, productivity, introduction of leverage, work simplification |

### Part II — Management Is a Team Game (Leverage)
| File | Topic |
|------|-------|
| [Ch3 Part 1](ch03-notes-managerial-leverage-part1.md) | Manager's output equation, Grove's day, five managerial activities (information-gathering, giving, decisions, nudging, role modeling) |
| [Ch3 Part 2](ch03-notes-managerial-leverage-part2.md) | Leverage equation, high-leverage activities, negative leverage (waffling, meddling, depression), delegation |
| [Ch3 Part 3](ch03-notes-managerial-leverage-part3.md) | Time management as production (batching, calendar as factory, slack, project inventory), 6-8 span of control, interruptions |
| [Ch4](ch04-notes-meetings.md) | Process-oriented meetings (1-1s, staff, operation reviews), mission-oriented meetings, the 80/20 rule |
| [Ch5](ch05-notes-decisions.md) | Free discussion → clear decision → full support, peer-group syndrome, peer-plus-one, the six questions framework |
| [Ch6](ch06-notes-planning.md) | Three-step planning (demand, status, gap), today's gap is yesterday's failure, MBO/OKRs, the Columbus case study |

### Part III — Team of Teams (Organization)
| File | Topic |
|------|-------|
| [Ch7](ch07-notes-breakfast-factory-goes-national.md) | Centralization vs. decentralization dilemma, scaling the breakfast factory nationally |
| [Ch8](ch08-notes-hybrid-organizations.md) | Mission-oriented vs. functional orgs, Grove's Law (all large orgs become hybrids), platform teams as functional groups |
| [Ch9](ch09-notes-dual-reporting.md) | Matrix management, peer groups as supervisors, multi-plane organizations, transitory teams |
| [Ch10](ch10-notes-modes-of-control.md) | Free-market forces, contractual obligations, cultural values, the CUA factor |

### Part IV — The Players (Individual Performance)
| File | Topic |
|------|-------|
| [Ch11](ch11-notes-the-sports-analogy.md) | Can't vs. won't diagnostic, Maslow's hierarchy, self-actualization, competence vs. achievement driven, the manager as coach |
| [Ch12](ch12-notes-task-relevant-maturity.md) | No single best management style, TRM per task not per person, structured → communicating → monitoring |
| [Ch13 Part 1](ch13-notes-performance-appraisal-part1.md) | Why reviews are highest-leverage feedback, output vs. internal measures, time offsets, the potential trap |
| [Ch13 Part 2](ch13-notes-performance-appraisal-part2.md) | Three L's (level, listen, leave yourself out), mixed/blast/ace reviews, five stages of problem-resolution |
| [Ch14](ch14-notes-two-difficult-tasks.md) | Interviewing (four information categories), retaining a valued employee who wants to quit |
| [Ch15](ch15-notes-compensation.md) | Money as measure vs. motivator, merit vs. experience pay, Peter Principle, recycling |
| [Ch16](ch16-notes-why-training-is-the-bosss-job.md) | Training as highest-leverage activity, the 17:1 leverage ratio, the manager as teacher |

### Epilogue
| File | Topic |
|------|-------|
| [One More Thing](epilogue-notes-one-more-thing.md) | Grove's scored action assignments — 100 points to become a better manager |

## Block Types

Each chapter uses a consistent set of annotation blocks:

| Block | Purpose |
|-------|---------|
| **[Core Concept]** | Grove's original idea with the "why" |
| **[Modern Lens]** | How the concept evolved since 1983 |
| **[Grove vs. Modern]** | What holds up, what changed |
| **[Senior EM Application]** | Applying the concept at the Senior EM / Director-track level |
| **[SRE Lens]** | Reliability engineering-specific application |
| **[Production Thinking]** | Mapping factory concepts to software/SRE |
| **[Practical Toolkit]** | Concrete techniques, templates, and metrics |
| **[Metrics That Matter]** | Specific numbers to track with healthy ranges |
| **[AI & Automation]** | How AI changes the calculus |
| **[Anti-Pattern]** | Common ways teams get this wrong |
| **[Scenario]** | Realistic worked examples |
| **[Mental Model]** | Related frameworks from other thinkers |
| **[Go Deeper]** | Books, talks, and papers for further learning |

## Key Equations from the Book

**Manager's output** = output of his organization + output of neighboring organizations under his influence

**Managerial output** = L1 x A1 + L2 x A2 + ... (where L = leverage, A = activity)

**Productivity** = output / labor

**Training leverage** = 12 hours invested / 200 hours gained = 17:1 (at 1% improvement across 10 people)

## The Book in One Paragraph

A manager's output is the output of their organization. To maximize that output, apply production principles (find the limiting step, plan backward, inspect at the lowest-value stage), choose high-leverage activities (training, 1-1s, decisions — not status meetings), build hybrid organizations that balance responsiveness with efficiency, and elicit peak individual performance through motivation (create racetracks for self-actualization) and training (the boss's job, not HR's). When someone isn't performing, diagnose: can't do it (train) or won't do it (motivate). Adjust your management style to their task-relevant maturity, not their seniority. Deliver honest performance feedback — it's the highest-leverage form of task-relevant feedback you have. And never forget: today's gap represents a failure of planning sometime in the past.
