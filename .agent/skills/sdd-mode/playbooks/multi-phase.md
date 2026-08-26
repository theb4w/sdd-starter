# Playbook: multi-phase

**Gate profile:** `full` per phase (G1 is the overall PLAN; G2/G3/G4 repeat per phase).
**When:** large feature, architectural refactor, or a PLAN already split into phases.
**Not when:** one PR fits → `feature.md` / `refactor.md`.

## Steps

1. Ensure `SDD/`. SPEC and multi-phase PLAN must exist under `SDD/`. Else parent playbook first, **STOP GATE 1**.
2. TASKS for the current phase only. **STOP GATE 2.**
3. IMPLEMENT with `sdd-tdd`. Phase commit leaves previous phase working.
4. **STOP GATE 3.** **STOP GATE 4.** `handover.md` naming the next phase.
5. Default next session: `resume.md`.

## Reply

Phase id, TASK range, waiting gate, next phase.
