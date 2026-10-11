# Module 6: Pre-Merge Blast Radius & `/pr` (Merge Danger)

*Source: Matt Pocock v1.3 (`/pr` lineage) via The Hype Kevin.*

### **6.1 Merge Danger**
Before drafting the PR, compute a **merge danger** assessment for the combined change set: how much can this merge break, and how confidently do we know it won't? Inputs:
*   **Blast radius** (§6.2) — the structural reach of the change.
*   **Test coverage delta** — new behavior covered? modified paths previously covered?
*   **Desk findings history** — tickets that failed desks (M5) once or twice carry elevated danger; double-failers that escalated to re-grilling carry the most.
*   **DAG position** — early unlocking tickets are high-danger (more downstream depends on them); leaf tickets are low.

### **6.2 Blast Radius Calculation**
1.  Diff surface: files touched, by type (interface/implementation/test/config/docs).
2.  Propagation: for each exported symbol changed, its inbound dependents (callers, implementers, subtype relations) — use the code graph, not grep optimism.
3.  Runtime surfaces: entry points (routes, jobs, CLI) reachable from the changed symbols.
4.  Classify: **contained** (private to the ticket's module), **local** (same subsystem callers), **global** (crosses a boundary or lands on a public entry point). Global-radius merges get a second Desk 2 pass before the PR leaves draft.

### **6.3 PR Draft Standard**
The PR is drafted automatically from pipeline artifacts — not rewritten from memory:
*   Title: the ticket's objective sentence.
*   Body: spec citations implemented, acceptance criteria with evidence links, Desk 1/Desk 2 verdicts, blast-radius classification, and the merge-danger rating with its inputs.
*   The reviewer of the PR reviews the ASSEMBLED evidence; nothing asks them to re-derive it.

### **6.4 Merge Gate Order**
Desk 1 PASS + Desk 2 PASS (M5) → blast radius computed (§6.2) → merge danger rated (§6.1) → PR drafted (§6.3) → human merge decision on global-radius or high-danger changes; contained/low-danger may merge on the standing policy the team has set. After merge: the ticket's M4 margin notes and desk findings hand off to `/retro` (M7).
