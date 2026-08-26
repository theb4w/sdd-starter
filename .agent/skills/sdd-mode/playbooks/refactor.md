# Playbook: refactor

**Gate profile:** internal → `lite` plus an ADR why. Architectural → `full`.
**When:** structure change; behavior preserved or contract migrated on purpose.
**Not when:** sneaking a feature → `feature.md`.
**Skills:** `sdd-tdd`

## Steps

1. Ensure `SDD/`. Read module SPEC, ADRs, tests.
2. If no safety net, add characterization tests before refactoring.
3. Justify with a metric or risk. Classify internal vs architectural.
4. Internal: ADR in `SDD/decisions/`; no new SPEC. Architectural: SPEC v2 + ADR of migration + PLAN. **STOP GATE 1** if `full`.
5. If `full`: TASKS, **STOP GATE 2**. If `lite`: no G2.
6. Tests green before and after. `sdd-tdd` for behavior that could drift.
7. **STOP GATE 3.** **STOP GATE 4.** `handover.md`.

## Reply

Type, why, ADR path, test evidence, waiting gate.
