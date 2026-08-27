# AGENTS.md — sdd-starter

Skill pack SDD. Procedure: `sdd-mode/` on the host skill root (`skill-root.md`). This checkout: `.agent/skills/sdd-mode/`. Process for this pack: this `SDD/` folder.

**Smoke:** follow `.agent/skills/sdd-mode/references/dry-run.md` (A–E). This pack has no app runtime.

## Rules

1. **Spec-first.** No production code without the playbook contract (SPEC, story, or none on bug-fix).
2. **Stops follow the catalog row.** Default `agentic`: product CLARIFY + package. `full` = G1+G2. Never-block on HOW is `agentic`. Do not skip the package. sdd-mode does not merge `main`.
3. **Primary source.** Technical choice needs a URL or the ADR is blocked.
4. **No secrets in git or logs.** Sensitive in this pack: none (no app).
5. **Backward-compat.** A commit on `main` preserves the previous state.
6. **Traceability.** Code (if any) → TASK → SPEC → ADR, all under `SDD/`.
7. **One home.** Playbooks in `sdd-mode/playbooks/` (catalog: `references/catalog.md`). Product artifacts in `SDD/`. Do not revive `specs/`, `docs/`, `prompts/`, `QUICKSTART/`.
8. **Under pstack.** pstack executes; sdd-mode is the contract layer (`with-pstack.md`). Never-block on HOW = `agentic`. Overnight land = pstack shipping after G3, only if the human asked. “Best spec is code” stays rejected.

## Modules

Source: `SDD/INDEX.md`. Today: SDD_MODE.

## Out of scope

- Cursor plugin as core
- sdd-mode merging `main`
- Mandatory product stack
