# Module 1: The Grilling Protocol & Domain Glossary

*Source: Matt Pocock v1.3 agent skills framework (`/grill-with-docs` lineage) via The Hype Kevin's analysis.*

### **1.1 Purpose**
Grilling is a stateful, rigorous pre-coding interview that eliminates the Silent Guess. The agent systematically interrogates the user on edge cases, state transitions, and business logic **before any code is written**. A worked example: implementing a "Pause" subscription button seems trivial until grilling surfaces the edge case of what happens to already-packaged items — the exact ambiguity an ungrilled LLM would silently resolve (wrongly).

### **1.2 The Interview Loop**
1.  Read the task + all project docs (`AGENTS.md`, READMEs, existing code in the touched area) BEFORE the first question.
2.  Ask one question at a time, each naming a concrete scenario ("What happens to X when Y?"), never abstract ("How should it work?").
3.  Classify each answer on receipt:
    *   **Settled by discussion** — record the decision verbatim in the decision log.
    *   **Requires a spike** — a technical unknown that discussion cannot settle (behavior of a library, feasibility of an approach); branch a small time-boxed prototype, record its result as the decision evidence.
    *   **Out of scope** — explicitly parked; parking is a decision too.
4.  Continue until every state transition, error path, and business rule in the task's blast radius has an explicit disposition. The exit criterion is "no unasked question a reviewer could still ask".

### **1.3 GLOSSARY.md — Ubiquitous Language**
*   Maintain `GLOSSARY.md` under repo root: **one word for one thing** (domain-driven ubiquitous language).
*   Every entry: term, definition, and the code symbol that implements it. If two terms name one thing, merge them and record the alias; if one term means two things, split it — this is a grilling finding, not an editing choice.
*   The glossary is load-bearing downstream: tickets (M3) and Desk 1 review (M5) quote glossary terms; a ticket using a term not in the glossary is a defect.

### **1.4 Architecture Decision Records**
Decisions with structural consequences (state ownership, data flow, library choice) become ADRs: context, options considered, decision, consequences. Spikes' outcomes attach to the ADR as evidence. ADRs are immutable once accepted — superseding requires a new ADR that references the old.

### **1.5 Output Contract**
Grilling terminates into `/to-spec` (M2) carrying: the decision log (verbatim dispositions), `GLOSSARY.md` deltas, spike results, ADRs, the parked/out-of-scope list, and the **grilling checklist delta** — new default questions added to the standing checklist by this round (fed back by M7 §7.3 retros; the checklist ensures the question gets asked by default next time). Nothing in the contract may be paraphrased from memory — the spec compiler consumes recorded decisions only.
