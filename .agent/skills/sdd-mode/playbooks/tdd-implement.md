# Playbook: tdd-implement

**Family:** Change
**Intent:** Tests first on an approved unit
**Profile:** inherit
**Not when:** no AC yet → parent playbook.
**Basis:** spec-kit implement; test spec as judge. Does not reopen specify/plan.
**Skills:** `sdd-tdd`

Ends in parent `review.md` + G3 + package, not a lighter exit.

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). Name the unit (TASK id or story criterion). Quote the AC from `SDD/`.
2. Run `sdd-tdd` for that unit only.
3. Show RED, diff, GREEN.
4. Next unit only after this AC is green.
5. After the last unit, parent playbook: `review.md` + G3 + package. Do not invent a lighter exit.

## Reply

Unit id, evidence, next unit or inherited gate.
