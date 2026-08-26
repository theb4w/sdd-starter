# Playbook: bug-fix

**Gate profile:** `lite` (G3, G4). Behavior/architecture change → reclassify.
**When:** a defect to reproduce, root-cause, and fix.
**Not when:** missing unspecified functionality → `feature.md` or `user-story.md`.
**Skills:** `sdd-tdd`

## Steps

1. Ensure `SDD/`. Read `SDD/INDEX.md`, module SPEC if any, latest `SDD/handovers/`.
2. Reproduce on the matching surface. A bug you cannot reproduce, you cannot prove fixed.
3. Root cause: expected (cite `SDD/modules/SPEC_*` or current behavior) vs actual vs why.
4. Classify: (a) stay here; (b) SPEC wrong → CLARIFY + update SPEC; (c) architectural → `refactor.md`.
5. **sdd-tdd:** RED on the repro, minimum fix, GREEN.
6. Do not ship “might help” without evidence.
7. **STOP GATE 3** — same surface as step 2.
8. **STOP GATE 4** — `fix(...): ...`.
9. Optional `handover.md`.

## Reply

Root cause, fix, RED/GREEN evidence, G3, `SDD/` paths touched.
