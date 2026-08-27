# Playbook: refactor

**Gate profile:** internal → `lite` + ADR why. Architectural → `full` (contract change is specify v2).
**When:** structure change; behavior preserved or contract migrated on purpose.
**Not when:** sneaking a feature → `feature.md`.
**Basis:** Feathers characterization tests; Parnas isolate change.
**Skills:** `sdd-tdd`, `review.md`

## Steps

1. Ensure `SDD/`. Read SPEC, ADRs, tests.
2. Characterization tests if no safety net.
3. Justify with a metric or risk. Classify internal vs architectural.
4. Internal: ADR; no new SPEC. Architectural: SPEC v2 + migration ADR + PLAN. `full`: **STOP G1** then TASKS **STOP G2**. `lite`: continue after ADR.
5. Tests green before and after. `sdd-tdd` if behavior could drift.
6. `review.md` + G3.
7. **Package.** `handover.md`.

## Reply

Type, ADR path, package or `full` gate.
