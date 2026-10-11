# Kirby Pocock Workflow - Dispatcher

This skill orchestrates Matt Pocock's v1.3 spec-driven engineering assembly line (mattpocock/skills): a pre-coding alignment pipeline that eliminates the **Silent Guess** — the industry-wide failure where an LLM, given an ambiguous task, silently makes assumptions and codes in the dark instead of asking. Long prompts cannot fix this: developers cannot foresee the decision tree in the fog. The pipeline instead forces ambiguity out BEFORE code exists, isolates every build to the model's "Smart Zone", and gates merges through two adversarial review desks.

**Runtime complement:** `../../kirby-helix-workflow/SKILL.md` owns deterministic runtime gates (`<gates>`, exit-code test traps) and dual-tier `learnings.md` memory. This skill owns the conversational specification, ticket DAG, and clean-head build lifecycle. Route between them per Module 7 §7.4.

## 📚 Module Index
- **Module 1: The Grilling Protocol & Domain Glossary** -> Read `./01_grilling_and_glossary.md`
- **Module 2: The Specification Anchor (`/to-spec` synthesis rules)** -> Read `./02_to_spec_protocol.md`
- **Module 3: Atomic Decomposition & The Smart Zone (`/to-tickets` DAG)** -> Read `./03_smart_zone_tickets.md`
- **Module 4: Clean-Head Isolated Builds** -> Read `./04_clean_head_isolated_builds.md`
- **Module 5: The Two-Desk Code Review** -> Read `./05_two_desk_review.md`
- **Module 6: Pre-Merge Blast Radius & `/pr` (Merge Danger)** -> Read `./06_pr_and_merge_danger.md`
- **Module 7: The Deterministic Feedback Loop (`/retro`)** -> Read `./07_retro_deterministic_loops.md`

## Pipeline (strict order)
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

## When to Use
- An ambiguous feature request would otherwise be coded from silent assumptions (M1 first — always).
- You need to formalize ubiquitous language before a multi-ticket build (`GLOSSARY.md`, ADRs — M1).
- You are compiling interview decisions into an authoritative spec without feature hallucination (M2).
- You are decomposing a spec into tracer-bullet tickets sized for bounded token windows (M3).
- You are running ticket builds in isolated contexts/git worktrees with standards concealed from the builder (M4).
- You are reviewing code against the ticket (Desk 1) and against repo invariants (Desk 2 — executed via `../../kirby-open-code-review/SKILL.md`) (M5).
- You are computing merge danger / blast radius before a PR (M6).
- You are converting post-implementation friction into deterministic linters, hooks, or memory rules (M7 — with `../../kirby-helix-workflow/SKILL.md` runtime gates).

## When NOT to Use
- Deterministic runtime enforcement (test traps, exit-code gates) — `../../kirby-helix-workflow/SKILL.md`.
- Verifying context windows stay within token budgets — `../../kirby-context-audit/SKILL.md` (invoked BY M3/M4, not duplicated).
- Trivial single-file changes with zero ambiguity — pipeline cost exceeds risk; grill only what is in the fog.
