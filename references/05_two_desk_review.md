# Module 5: The Two-Desk Code Review

*Source: Matt Pocock v1.3 via The Hype Kevin. Desk 2's automated execution engine: `../../kirby-open-code-review/SKILL.md`.*

### **5.1 Why Two Desks**
A single review pass conflates two orthogonal questions and drops whichever it runs out of attention for. The pipeline decouples review into two **parallel, adversarial desks** with non-overlapping mandates:

| Desk | Question | Inputs | Blind to |
|---|---|---|---|
| **Desk 1 — Spec Review** | "Did the code actually build what the ticket asked for?" | Ticket contract (M3 §3.4), spec citations, acceptance-criteria evidence, the diff | Repo conventions, style, architecture opinions |
| **Desk 2 — Standards Review** | "Does the code satisfy repo architectural invariants, test coverage, and conventions?" | The diff, the repo's standards/lint rules, test suite | The spec and the ticket's intent |

Each desk must be able to fail the ticket independently. A pass requires BOTH.

### **5.2 Desk 1 Protocol (Spec)**
1.  Read the ticket contract and its spec citations FIRST, the diff second — judgment anchors to the ask, not the implementation's polish.
2.  Walk each acceptance criterion; locate the code + evidence satisfying it. Any criterion without visible satisfaction = FAIL with the criterion named.
3.  Hunt scope drift: diff hunks implementing anything outside the contract (including the M4 margin notes' adjacent fixes, which should not be present) = FAIL.
4.  Ambiguity discovered here (spec silent on what the diff does) routes to M1 — Desk 1 does not adjudicate spec meaning.

### **5.3 Desk 2 Protocol (Standards)**
1.  Execute the automated review pass via `../../kirby-open-code-review/SKILL.md` (ocr CLI) as the primary instrument; the human/agent reviewer adjudicates its findings.
2.  Check the diff against repo invariants: architecture boundaries, error-handling patterns, test coverage for new behavior, naming per `GLOSSARY.md` (a code symbol contradicting the glossary is a defect), and the deterministic rules accumulated by M7 retros.
3.  Desk 2 never sends the ticket back for "better ideas" — only for invariant violations. Taste debates are retro material, not review blocks.

### **5.4 Fail Loop**
A desk FAIL returns the ticket to a fresh clean head (M4) with the review findings appended to the context manifest — the original builder's session is not resurrected. Two consecutive Desk 1 failures on the same criterion escalate to M1: the spec or the ticket is wrong, not the builder. Two consecutive Desk 2 failures on the same invariant escalate to retro (M7): the invariant is either not machine-enforceable yet (make it a linter/hook) or is genuinely contestable (taste debate — retire or reword it); a third clean head would just repeat the collision.
