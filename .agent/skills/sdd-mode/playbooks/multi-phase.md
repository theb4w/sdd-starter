# Playbook: multi-phase

**Gate profile:** `full` **per phase** (G1 is the overall PLAN; G2/G3/G4 repeat per phase as in `docs/SDD_WORKFLOW.md` §13)
**When:** feature large, architectural refactor, or any SPEC the PLAN split into phases.
**Not when:** a single phase fits in one PR under the usual size limits → `feature.md` or `refactor.md`.
**Principles:** backward-compat, sequence-verifiable-units, stop-at-gate.

## Steps

1. Confirm the SPEC and the multi-phase PLAN exist. If not, `feature.md` / `refactor.md` first, **STOP GATE 1**.
2. For the current phase only, write or reuse TASKS. **STOP GATE 2** for that phase.
3. IMPLEMENT with `sdd-tdd` / `tdd-implement.md`. A phase commit must leave the previous phase working (`principle-backward-compat`).
4. **STOP GATE 3** for this phase's critical flows.
5. **STOP GATE 4** for this phase. `handover.md` naming the next phase.
6. Do not start phase N+1 in the same un-gated rush. `resume.md` next session is the default.

## Reply

Phase id, TASK range, compatibility note, waiting gate, next phase name.
