# Playbook: multi-phase

**Gate profile:** inherit parent (`agentic` per phase unless `full`).
**Basis:** modular granularity; each phase is a working system.
**When:** large feature, architectural refactor, or a PLAN already split.
**Not when:** one PR fits → `feature.md` / `refactor.md`.
**Skills:** `sdd-tdd`, `review.md`

## Steps

1. Ensure `SDD/`. SPEC + multi-phase PLAN must exist. Else parent playbook first (`full` only: **STOP G1**).
2. TASKS for this phase. `full`: **STOP G2**. `agentic`: continue.
3. IMPLEMENT + `sdd-tdd`. Phase commit leaves previous phase working. Branch.
4. `review.md` + G3.
5. **Package** for this phase. `handover.md` names the next phase.
6. Next session: `resume.md`.

## Reply

Phase id, profile, package, next phase.
