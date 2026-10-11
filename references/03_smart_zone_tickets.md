# Module 3: Atomic Decomposition & The Smart Zone — `/to-tickets` DAG

*Source: Matt Pocock v1.3 (`/to-tickets` lineage) via The Hype Kevin. Token-budget verification engine: `../../kirby-context-audit/SKILL.md` (Smart Zone mode).*

### **3.1 The Smart Zone**
LLM output quality degrades as a single context grows: attention thins, hallucination rises, drift accumulates. The Smart Zone is the bounded token window in which a model reliably performs — small, self-contained tasks with clear inputs and verifiable outputs. Ticket sizing exists to keep EVERY implementation unit inside the zone. Operationally: if a ticket's brief (spec excerpt + glossary terms + acceptance criteria) plus its expected diff cannot fit a modest context with room to think, the ticket is too big — split it.

### **3.2 Tracer-Bullet Tickets**
Each ticket is a **tracer bullet**: a thin, end-to-end slice that produces a verifiable result (a passing test, a working endpoint, a rendered screen) — not a horizontal layer ("write all the types first"). A tracer bullet proves the path; subsequent tickets widen it.

### **3.3 The Ticket DAG**
Decompose the spec into tickets forming a **Directed Acyclic Graph** with explicit blocking edges:
*   Each ticket states: `requires: [ticket-ids]` and `unlocks: [ticket-ids]`.
*   No cycles — a cycle means the decomposition re-opened a decision; route the thread back to M1.
*   Parallelizable tickets (no edge between them) are marked — they can run in parallel clean-head builds (M4).

### **3.4 Ticket Contract (every ticket, no exceptions)**
1.  **Objective** — one sentence in glossary vocabulary.
2.  **Spec citations** — the numbered requirements this ticket implements (from M2 §2.3 items 3–4: behavioral requirements and edge-case dispositions).
3.  **Context manifest** — the exact files/docs the builder receives (M4's concealment depends on this being minimal and explicit).
4.  **Acceptance criteria** — copied from the spec, verbatim.
5.  **Out of scope** — what adjacent tickets own (prevents scope creep inside a clean head).
6.  **Sizing check** — the manifest + expected diff estimated against the Smart Zone budget; a fail here splits the ticket BEFORE it is queued.

### **3.5 Verification**
Before queuing, run `../../kirby-context-audit/SKILL.md` Smart Zone verification over each ticket's context manifest to confirm the budget holds with margin. Tickets failing the check are split and re-edged in the DAG.
