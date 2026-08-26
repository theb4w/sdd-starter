# Playbook: bootstrap

**Gate profile:** `full` (per module; stop at GATE 1 of the first module in this session)
**When:** greenfield, or brownfield whose `PROJECT_BRIEF.md` is already filled.
**Not when:** the repo has no brief and no one knows the domain → `discover.md`.
**Principles:** spec-first, primary-source, stop-at-gate, one-home-per-fact.
**Human prompt (pointer):** `prompts/BOOTSTRAP.md`

## Preconditions

- [ ] Workspace is the *target* project, not a random folder
- [ ] `PROJECT_BRIEF.md` filled (§1–§6 at minimum)
- [ ] Git initialized, `.env` not committed

## Steps

1. Read `AGENTS.md`, `docs/SDD_WORKFLOW.md` §1–2, `PROJECT_BRIEF.md`, templates under `specs/` and `docs/`.
2. Summarize: stage (greenfield/brownfield), stack constraints from the brief, listed modules, which module is the product core. **No production code.**
3. Adapt `AGENTS.md` placeholders (`ADAPT`) from the brief. Do not invent a stack the brief left open; that is CLARIFY or an ADR.
4. Draft `docs/<Project>_Architecture.md` from `docs/_ARCHITECTURE_TEMPLATE.md` (v1, incomplete is fine).
5. Fill `specs/SPEC_INDEX.md` with modules from the brief (status 📝).
6. Write `specs/modules/SPEC_<CORE>.md` from `_SPEC_TEMPLATE.md`. Put unknowns in §9 CLARIFY.
7. Walk CLARIFY with the human. Record answers in §10. Trade-offs → propose ADR (2+ options, URL each).
8. Write `specs/plans/PLAN_<CORE>.md`. **STOP GATE 1.** Do not write TASKS or code until the human approves the PLAN.
9. After GATE 1, if this session continues: TASKS → **STOP GATE 2** (`feature.md` / `multi-phase.md`). Otherwise `handover.md`.

## Reply

Stage, core module, SPEC path, open CLARIFY, ADRs proposed, PLAN path, waiting on GATE 1.
