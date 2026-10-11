# Module 2: The Specification Anchor — `/to-spec` Protocol

*Source: Matt Pocock v1.3 (`/to-spec` lineage) via The Hype Kevin.*

### **2.1 The Immutable Spec**
`/to-spec` compiles the grilling record (M1 output contract) into a single authoritative specification — an issue or document that later stages treat as ground truth. Two properties define it:
*   **Immutable once ratified:** downstream stages never edit the spec to match discovered convenience; a spec change re-enters through a new grilling round for the affected decision, then re-compiles.
*   **Complete:** every state transition, error path, business rule, and parked item from M1 appears with its disposition. Ratification requires the user's explicit confirmation that the spec matches their intent.

### **2.2 Synthesis Rules (The No-Hallucination Contract)**
1.  **Record agreed decisions only.** The spec is forbidden from inventing features, requirements, or constraints that no grilling decision supports. If synthesis reveals a gap (a state transition nobody dispositioned), the spec STOPS and emits the gap as new grilling questions — it does not paper over the hole.
2.  **Cite or quote:** every spec statement traces to a decision-log entry, glossary term, ADR, or spike result. Uncited statements are deleted on sight.
3.  **Ubiquitous language enforced:** spec vocabulary is `GLOSSARY.md` vocabulary verbatim.
4.  **No implementation detail:** the spec states WHAT and the business rules, never HOW. Technology choices appear only where they were themselves grilling decisions (ADRs).

### **2.3 Spec Structure**
1.  **Problem & scope** (with the parked/out-of-scope list from M1).
2.  **Definitions** (glossary delta).
3.  **Behavioral requirements** — numbered, each with its citation.
4.  **Edge cases & error paths** — each with its disposition.
5.  **Decisions record** — ADR references.
6.  **Acceptance criteria** — derived 1:1 from the above; nothing new appears here either.

### **2.4 Handoff**
The ratified spec becomes the sole input to `/to-tickets` (M3). Ambiguity discovered during decomposition routes BACK through M1 for that thread — never resolved by the ticket author.
