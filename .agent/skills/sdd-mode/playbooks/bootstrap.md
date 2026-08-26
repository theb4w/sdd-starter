# Playbook: bootstrap

**Gate profile:** `full` (per module; stop at GATE 1 of the first module)
**When:** greenfield, or brownfield whose `SDD/BRIEF.md` is already filled.
**Not when:** no brief and unknown domain → `discover.md`.
**Principles:** spec-first, primary-source, stop-at-gate, one-home-per-fact.
**Templates:** `templates/brief.md`, `agents.md`, `architecture.md`, `index.md`, `spec.md`, `plan.md`, `adr.md`

## Preconditions

- [ ] Workspace is the *target* project
- [ ] `SDD/` exists (skill preamble creates it)
- [ ] `SDD/BRIEF.md` has §1–§6, or this session will fill them with the human **before** SPECs

## Steps

1. Read `SDD/BRIEF.md`, `SDD/AGENTS.md`, `references/workflow.md` §1–2, templates listed above.
2. Summarize: stage, stack constraints from the brief, modules, product core. **No production code.**
3. Fill `SDD/AGENTS.md` placeholders from the brief. Do not invent a stack the brief left open (CLARIFY or ADR).
4. Draft `SDD/architecture.md` from `templates/architecture.md` (v1, incomplete is fine).
5. Fill `SDD/INDEX.md` with modules from the brief (status 📝).
6. Write `SDD/modules/SPEC_<CORE>.md` from `templates/spec.md`. Unknowns in §9 CLARIFY.
7. Walk CLARIFY. Record in §10. Trade-offs → `SDD/decisions/ADR-NNN-*.md` (2+ options, URL each).
8. Write `SDD/plans/PLAN_<CORE>.md`. **STOP GATE 1.** No TASKS or code until PLAN is approved.
9. After GATE 1: TASKS → **STOP GATE 2**, or `handover.md`.

## Reply

Stage, core module, `SDD/` paths, open CLARIFY, waiting on GATE 1.
