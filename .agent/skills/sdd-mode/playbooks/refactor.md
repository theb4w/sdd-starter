# Playbook: refactor

**Gate profile:** internal (no contract change) → `lite` plus an ADR that says why. Architectural (public contract, schema, dependency) → `full` and usually `multi-phase.md`.
**When:** change structure or shape; behavior preserved, or contract migrated on purpose.
**Not when:** sneaking a feature into a rename → `feature.md`.
**Principles:** backward-compat, prove-it-works, tdd-red-green, primary-source.
**Skills:** `sdd-tdd`
**Human prompt (pointer):** `prompts/REFACTOR.md`

## Steps

1. Read the module SPEC, ADRs that justified the current shape, and existing tests.
2. Measure coverage of the area. If there is no safety net, add characterization tests **before** the refactor (`sdd-tdd` RED on current behavior, which should already pass — here the “RED” is missing tests, not a bug). Do not refactor untested behavior.
3. Justify with a concrete metric or risk (complexity, a race, an upcoming feature). Classify internal vs architectural.
4. Internal: ADR if you are choosing a new pattern; TASKS short; no new SPEC. Architectural: SPEC v2 + ADR of migration + rollback + PLAN. **STOP GATE 1** if `full`.
5. If `full`: TASKS, then **STOP GATE 2**. If `lite`: no G2; keep the change small enough to review in G4.
6. Implement with tests green before and after. `sdd-tdd` for any behavior that could drift.
7. **STOP GATE 3** — same behaviors as before, on the real surface.
8. **STOP GATE 4.** `handover.md`.

## Reply

Type (internal/architectural), why, ADR path, test evidence before/after, waiting gate.
