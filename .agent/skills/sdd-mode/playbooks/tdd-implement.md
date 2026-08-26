# Playbook: tdd-implement

**Gate profile:** inherit from the approved unit. Does not skip inherited G3/G4.
**When:** IMPLEMENT as RED → GREEN on work that already passed specify/plan/tasks of the parent playbook.
**Not when:** no AC yet → parent playbook.
**Skills:** `sdd-tdd`

## Steps

1. Ensure `SDD/`. Name the unit (TASK id or story criterion). Quote the AC from `SDD/`.
2. Run `sdd-tdd` for that unit only.
3. Show RED, diff, GREEN.
4. Next unit only after this AC is green.
5. After the last unit, return to the parent playbook's G3 and G4.

## Reply

Unit id, evidence, next unit or inherited gate.
