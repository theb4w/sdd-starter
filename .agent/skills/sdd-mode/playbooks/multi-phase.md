# Playbook: multi-phase

**Family:** Change
**Intent:** Large / many modules
**Profile:** `agentic`
**Not when:** one PR fits → `feature.md` / `refactor.md`.
**Basis:** modular granularity; each phase is a working system.
**Skills:** `sdd-tdd`, `review.md`

Promote to `full` when the parent change is `full` (schema, service, compliance, WHAT unclear).

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). SPEC + multi-phase PLAN must exist. Else parent playbook first (`full` only: **STOP G1**).
2. TASKS for this phase. `full`: **STOP G2**. `agentic`: continue.
3. IMPLEMENT + `sdd-tdd`. Phase commit leaves previous phase working. Branch.
4. `review.md` + G3 (`Smoke:` in `SDD/AGENTS.md`).
5. **Package** for this phase. `handover.md` names the next phase.
6. Next session: `resume.md`.

## Reply

Phase id, profile, package, next phase.
