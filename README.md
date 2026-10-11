# Kirby Pocock Workflow

[![Kirby Skills Collection](https://img.shields.io/badge/Kirby_Skills-Collection-blue?style=flat-square&logo=github)](https://github.com/markkirby125/kirby-skills-collection)

You hand an AI coding agent an ambiguous feature request. It does not ask questions. It silently guesses — picks an interpretation, codes in the dark, and hands you back something plausible-looking that is wrong in a way you will not discover until production. You tried writing longer prompts; that failed, because you cannot foresee the decision tree in the fog any better than the model can.

**This is the Silent Guess, and it is the default behavior of every LLM given an underspecified task.**

**The Solution:** The `kirby-pocock-workflow` skill installs Matt Pocock's spec-driven engineering assembly line — a rigorous pre-coding alignment pipeline where ambiguity is eliminated before any code exists, tickets are isolated to the model's "Smart Zone", and implementation is gated through two independent adversarial review desks plus a deterministic retrospective that converts every failure into a machine-enforced rule so it cannot recur.

The worked example from the source material: a "Pause subscription" button looks trivial until grilling surfaces the edge case of already-packaged items — exactly the ambiguity an ungrilled agent silently resolves, wrongly.

## What's Inside

- **Module 1 — The Grilling Protocol & Domain Glossary:** a stateful pre-coding interview (one concrete scenario per question), discussion-vs-spike decision routing, `GLOSSARY.md` ubiquitous language ("one word for one thing"), and immutable ADRs.
- **Module 2 — The Specification Anchor:** `/to-spec` synthesis rules — the spec records agreed decisions with citations and is **forbidden from inventing features**; discovered gaps stop compilation and emit new grilling questions.
- **Module 3 — Atomic Decomposition & The Smart Zone:** tracer-bullet tickets in a DAG with explicit blocking edges, sized to bounded token windows; the context-audit Smart Zone gate verifies every manifest before queueing.
- **Module 4 — Clean-Head Isolated Builds:** one fresh context (or git worktree) per ticket, coding standards concealed from the builder so 100% of attention lands on the functional spec, and a hard data-not-directives boundary against prompt injection through ingested docs.
- **Module 5 — The Two-Desk Code Review:** Desk 1 asks "did the code build what the ticket asked?" (blind to conventions); Desk 2 asks "does it satisfy repo invariants?" (blind to intent) — executed automatically via `kirby-open-code-review`. Both must pass; neither can overrule the other's domain.
- **Module 6 — Pre-Merge Blast Radius & `/pr`:** merge-danger rating from blast radius, coverage delta, desk history, and DAG position; PRs drafted from pipeline artifacts, never from memory.
- **Module 7 — The Deterministic Feedback Loop:** `/retro` converts friction into linters, hooks, grilling-checklist questions, or runtime gates (`kirby-helix-workflow`) — every constraint verified to actually fire before the item closes.

## Pipeline

```
Grilling + Glossary + Spikes (M1)
        ▼
/to-spec — immutable spec (M2)
        ▼
/to-tickets — Smart Zone DAG (M3)
        ▼
Clean-head isolated builds, one per ticket (M4)
        ▼
Two-desk review: Desk 1 Spec │ Desk 2 Standards (M5)
        ▼
/pr — merge danger + blast radius (M6)
        ▼
merge ─── /retro — deterministic feedback loops (M7)
```

## Ecosystem Integration

- `kirby-helix-workflow` — the deterministic runtime sibling: Helix owns `<gates>`, exit-code test traps, and dual-tier `learnings.md` memory; this skill owns the conversational spec, ticket DAG, and build lifecycle. Retro items with runtime form are implemented as Helix gates.
- `kirby-open-code-review` — the automated Desk 2 engine (ocr CLI over the ticket branch).
- `kirby-context-audit` — the Smart Zone verification instrument (60%-of-window budget, SPLIT verdicts).

## 🪄 The Magic Prompt

Copy and paste this into any AI coding app (Cursor, Windsurf, Claude Code, Grok, Kimi, Reasonix):

```markdown
@agent Install the Kirby Pocock Workflow skill from: https://github.com/markkirby125/kirby-pocock-workflow
1. Read `SKILL.md` and `references/` from the repository.
2. Place into your environment's skills/rules directory preserving the dispatcher structure.
3. Confirm when installation is complete.
```

## Manual Installation

- **Cursor**: Save `SKILL.md` to `.cursor/rules/kirby-pocock-workflow.mdc` and copy `references/`
- **Windsurf**: Save `SKILL.md` to `.windsurfrules` and copy `references/`
- **Antigravity / agents dir**: Clone this repository directly into `~/.agents/skills/kirby-pocock-workflow`

## Requirements

- Git ≥ 2.41 (worktree isolation per ticket).
- Optional but recommended: the `ocr` CLI from [open-code-review](https://github.com/alibaba/open-code-review) for automated Desk 2, and the `kirby-helix-workflow` skill for runtime gate enforcement.
- Upstream companion skills by Matt Pocock (`/grill-with-docs`, `/to-spec`, `/to-tickets`) document the original command surface; this skill packages the full pipeline doctrine for the Kirby library.

## Tech Stack

- **Format**: Markdown / YAML (Hollow Shell skill)
- **Compatibility**: Antigravity, Claude Code, Cursor, Windsurf, Grok, Kimi, Reasonix
- **Tested**: `tests/test_new_skills_oct2026.py` in the [kirby-skills](https://github.com/markkirby125/kirby-skills) monorepo (36 tests: structure, routing, real worktree isolation, DAG cycle detection, Smart Zone sizing, no-hallucination gate, glossary reconciliation)

---

## Repo Details

* **Repository**: [https://github.com/markkirby125/kirby-pocock-workflow](https://github.com/markkirby125/kirby-pocock-workflow)
* **Parent Collection**: [kirby-skills](https://github.com/markkirby125/kirby-skills)
* **Master Directory**: [kirby-skills-collection](https://github.com/markkirby125/kirby-skills-collection)
* **Category**: Workflow / Agent Ops
* **Skill Author**: William Fitzpatrick (Kirby Skills Library)
* **Source Video**: "Ship like the best engineers: Matt Pocock's AI workflow" — The Hype Kevin
* **Direct Video URL**: https://youtu.be/Q3uuE2adUT8
* **Upstream Framework**: [mattpocock/skills](https://github.com/mattpocock/skills) v1.3 (Matt Pocock)

## Attribution & Provenance

* **Original Framework Author**: Matt Pocock — the v1.3 agent-skills framework: Grilling, GLOSSARY.md, spikes, `/to-spec`, `/to-tickets` (Smart Zone), clean-head builds, two-desk review, `/pr` merge danger, and `/retro` deterministic loops.
* **Source Analysis**: The Hype Kevin's walkthrough of the v1.3 release, from which this skill's pipeline order, desk separation, and Smart Zone doctrine are documented.
* **Kirby Extensions**: the data-not-directives ingestion boundary (M4), the Desk 2 double-fail escalation to retro (M5), threshold reconciliation notes, and the Helix handoff contract (M7).
