# Playbook: refactor

**Family:** Change
**Intent:** Reshape, same contract
**Profile:** `lite`

**Family:** Change
**Intent:** Reshape, public contract
**Profile:** `full`

**Not when:** sneaking a feature → `feature.md`.
**Basis:** Feathers characterization tests; Parnas isolate change.
**Skills:** `sdd-tdd`, `review.md`

Match the catalog row: same contract → `lite` + ADR why. Public contract change → `full` (specify v2 + migration ADR).

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). Read SPEC, ADRs, tests.
2. Characterization tests if no safety net.
3. Justify with a metric or risk. Classify internal vs architectural.
4. Internal (`lite`): ADR; no new SPEC; continue after ADR. Architectural (`full`): SPEC v2 + migration ADR + PLAN. **STOP G1** then TASKS **STOP G2**.
5. Tests green before and after. `sdd-tdd` if behavior could drift.
6. `review.md` + G3.
7. **Package.** `handover.md`.

## Reply

Type, ADR path, package or `full` gate.
