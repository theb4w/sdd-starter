# Playbook: bootstrap

**Gate profile:** `agentic` for the first module. `full` if the user asked or WHAT is unclear.
**When:** greenfield, or brownfield whose `SDD/BRIEF.md` is already filled.
**Not when:** no brief and unknown domain → `discover.md`.
**Basis:** spec-kit 0-to-1 + constitution + specify. Human owns intent (BRIEF). HOW is agentic unless `full`.
**Templates:** `brief.md`, `agents.md`, `architecture.md`, `index.md`, `spec.md`, `plan.md`, `adr.md`
**Skills:** `sdd-tdd`, `review.md`

## Preconditions

- [ ] Target project workspace
- [ ] `SDD/` exists
- [ ] BRIEF §1–§6 filled, or fill them with the human **before** SPECs

## Steps

1. Read BRIEF, `SDD/AGENTS.md`, `workflow.md` §1–2.
2. Summarize stage, stack constraints, core module.
3. Fill `SDD/AGENTS.md` from the brief. Do not invent an open stack (CLARIFY or ADR).
4. Draft `SDD/architecture.md`. Fill `SDD/INDEX.md`.
5. Write `SDD/modules/SPEC_<CORE>.md`. Product CLARIFY → **STOP**.
6. ADRs for stack trade-offs (URL each).
7. Write PLAN + TASKS. `full`: **STOP G1** then **STOP G2**. `agentic`: continue.
8. IMPLEMENT first phase + `sdd-tdd`.
9. `review.md` + G3.
10. **Package.** Branch. `handover.md`.

## Reply

Stage, core module, profile, package or BRIEF/CLARIFY stop.
