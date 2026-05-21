# Foreword and Preface

> **Implementing Service Level Objectives** — Alex Hidalgo
> *Foreword by David N. Blank-Edelman (Cofounder of SREcon)*

## Foreword

David Blank-Edelman frames the entire book in a single sentence: *"Reliability is a conversation."* It's a conversation with infrastructure, systems, services, complexity, colleagues, and users. SLIs and SLOs are tools for having *better* conversations — not scripts that dictate exactly what to say, but guidance that helps you navigate reliability discussions more effectively.

Two pieces of "soggy news":
1. SLIs and SLOs are easy in theory, harder in practice
2. They never finish — the conversation is ongoing

The good news: this book helps you mine the gold.

## Preface

### The Molly Story — The Book's Thesis in a Haircut

Hidalgo opens with a story that captures the entire philosophy. His hair stylist Molly started her career obsessing over perfection — spending an hour on a 30-minute men's cut to make everything perfectly symmetrical. The result: stressed stylist, frustrated waiting clients, no happier customers.

Her breakthrough: she realized *"trying to be perfect didn't really do much for anyone involved."* When she relaxed her standards to "incredibly good" instead of "technically perfect," **everyone was happier**: shorter waits for clients, more tips for her, better reviews for the shop. *"Every human involved was happier when perfection wasn't being aimed for."*

> *"Learn from Molly. The primary philosophies that are covered in this book are lessons she learned organically from her own business: nothing is perfect all the time, and it turns out that people don't actually expect things to be."*

This is the SLO philosophy distilled: measure what your users actually need, target "good enough" rather than "perfect," and everyone — users, engineers, business — ends up happier.

### How to Read This Book

The book has three parts:

| Part | Focus | Reading |
|------|-------|---------|
| **I. SLO Development** (Ch 1-5) | Concepts, philosophies, definitions — what the components are, how to use them, why they work | Mandatory reading, in order |
| **II. SLO Implementation** (Ch 6-12) | Practical — alerting math, dashboards, probability/statistics, worked examples, new services, data reliability | Read in any order based on your needs |
| **III. SLO Culture** (Ch 13-17) | Adoption — organizational buy-in, when to change SLOs, discoverability, advocacy, reporting | Read in any order |

Hidalgo emphasizes: this is all **only a model**. SLOs are an approach, not magic. They enable better discussions and data-driven decisions. There is no one-size-fits-all.

> **[Core Concept: "It's Only a Model"]**
>
> This is Hidalgo's most important disclaimer and it applies to every chapter: SLOs are a model of reality, not reality itself. The map is not the territory. Your SLI might not perfectly capture user experience. Your SLO target might be wrong. Your error budget window might be suboptimal. All of that is fine — imperfect models that drive better decisions are infinitely more useful than no model at all, or than a perfect model that nobody uses.
>
> The book repeatedly returns to this: iterate, don't perfect. Start, don't plan endlessly. An SLI that's "pretty good" is better than spending 6 months designing the "right" SLI.

> **[Senior EM Application: The "Molly" Pitch for Leadership]**
>
> When you need to explain SLOs to non-technical leadership, tell the Molly story:
>
> "We're like a hair stylist spending an hour on a 30-minute cut. Our users don't need us to be perfect — they need us to be reliably good. We're exhausting our engineers chasing the last 0.01% of reliability that users don't notice. SLOs let us define 'good enough,' measure whether we're achieving it, and redirect the saved effort toward things that actually make users happier — like new features and faster response times. Everyone involved ends up better off."
>
> Leadership doesn't need to understand error budget math. They need to understand the economics of "good enough."
