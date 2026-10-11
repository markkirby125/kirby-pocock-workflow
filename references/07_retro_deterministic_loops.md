# Module 7: The Deterministic Feedback Loop — `/retro`

*Source: Matt Pocock v1.3 (`/retro` lineage) via The Hype Kevin. Runtime enforcement sibling: `../../kirby-helix-workflow/SKILL.md`.*

### **7.1 Purpose**
The retro converts session friction and failures into **deterministic environment constraints** — linters, pre-commit hooks, or immutable memory rules — so an error that happened once cannot silently recur. A retro that produces only "we'll be careful next time" has failed; feelings are inputs, not outputs.

### **7.2 Inputs**
Every merge (M6) feeds the retro: builder margin notes (M4 §4.5 — ambiguities hit, adjacent issues seen), Desk 1/Desk 2 findings and their categories, escalation events (tickets that went back to grilling), and any mid-build Silent Guess caught late.

### **7.3 Root-Cause Conversion Rules**
For each friction item, classify and convert:

| Root cause | Deterministic conversion |
|---|---|
| A convention Desk 2 caught repeatedly | Linter rule or hook check (the convention leaves human judgment permanently) |
| An ambiguity that reached the builder | Grilling checklist addition (M1) — the question gets asked next time by default |
| A spec gap discovered downstream | Spec synthesis guard (M2) — the gap-detection pattern that missed it |
| An environment/tooling failure | Pinned dependency, CI check, or setup script fix |
| A repeated human mistake | Pre-commit hook or immutable memory rule (never a reminder to "remember") |

### **7.4 Helix Handoff**
Where the conversion is a **runtime gate** (test trap, exit-code enforcement, `<gates>` block) rather than a static check, implement it in `../../kirby-helix-workflow/SKILL.md`'s deterministic gate system and record the lesson in its dual-tier `learnings.md`. Static checks (linters, hooks) live in this repo's tooling directly. Division: **Pocock retro decides WHAT the constraint is; Helix implements the runtime form of it.**

### **7.5 Loop Closure Verification**
A retro item is closed only when its constraint demonstrably fires: test the linter against a reproduction, confirm the hook blocks a bad commit, confirm the grilling checklist contains the new question. Unfired constraints are open items carried to the next retro — plus a meta-retro question about why the constraint wasn't wired.
