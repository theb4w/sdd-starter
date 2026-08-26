# Playbook: tdd-implement

**Gate profile:** inherit from the approved unit (TASK, story, or bug). This playbook does not open scope and does not skip inherited G3/G4.
**When:** the human wants IMPLEMENT run as RED → IMPLEMENT → GREEN on work that already passed the specify/plan/tasks gates required by its parent playbook.
**Not when:** there is no AC yet → go back to `feature.md` / `user-story.md` / `bug-fix.md`.
**Skills:** `sdd-tdd`
**Principles:** tdd-red-green, sequence-verifiable-units, stop-at-gate.

## Preconditions

- [ ] SPEC or story or bug repro exists
- [ ] GATE 1/2 already passed if the parent profile includes them
- [ ] Current TASK or AC is named

## Steps

1. Name the unit (T-id or story criterion). Quote the AC.
2. Run `sdd-tdd` for that unit only.
3. Show RED output, the diff, GREEN output.
4. Next unit only after this AC is green. Do not batch.
5. After the last unit of the parent playbook: return to that playbook's G3 and G4. Do not invent a lighter exit.

## Reply

Unit id, RED evidence, GREEN evidence, next unit or inherited gate.
