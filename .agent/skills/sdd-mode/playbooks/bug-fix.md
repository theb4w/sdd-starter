# Playbook: bug-fix

**Gate profile:** `lite` (package includes G3). Reclassify if intended behavior or architecture must change.
**When:** a defect to reproduce, root-cause, and fix.
**Not when:** missing unspecified functionality → `feature.md` or `user-story.md`.
**Basis:** reproduce then root-cause; TDD. No G1/G2.
**Skills:** `sdd-tdd`, `review.md`

## Steps

1. Ensure `SDD/`. Read INDEX, SPEC if any, latest handover.
2. Reproduce on the matching surface.
3. Root cause: expected vs actual vs why.
4. Classify: (a) stay; (b) SPEC wrong → CLARIFY; (c) architectural → `refactor.md`.
5. `sdd-tdd`: RED on the repro, minimum fix, GREEN.
6. No “might help” without evidence.
7. `review.md`.
8. G3 = same surface as step 2.
9. **Package.** Optional handover.

## Reply

Root cause, RED/GREEN, review, G3, package.
