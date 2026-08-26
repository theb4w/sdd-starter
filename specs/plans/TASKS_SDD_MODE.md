# TASKS_SDD_MODE — Decomposição atômica

**Status:** ✔️ CONCLUÍDO (fases A–C neste repo; G3 = consistência documental)
**Data:** 2026-08-25
**PLAN base:** `specs/plans/PLAN_SDD_MODE.md`

---

## Fase A — Fundação

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| T-A1 | SPEC, ADRs, PLAN, TASKS, SPEC_INDEX | `specs/` → NOVO/MOD | índice lista SDD_MODE + ADR-001/002 |
| T-A2 | Principles absolutas + rigor + stop-at-gate + prove-it-works | `.agent/skills/principle-*/` → NOVO | 10 SKILL.md com `name` e regra em 1 tela |
| T-A3 | Roteador `sdd-mode` | `.agent/skills/sdd-mode/SKILL.md` → NOVO | match, skip-com-motivo, stop-at-gate, índice de principles |
| T-A4 | Playbooks dos cenários atuais | `.agent/skills/sdd-mode/playbooks/` → NOVO | 8 arquivos, cada um com Gate profile |
| T-A5 | Perfis no workflow | `docs/SDD_WORKFLOW.md` §2 → MOD | tabela de perfis + coluna Playbook |

## Fase B — Camada extra

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| T-B1 | Principles TDD, sequence, one-home | `.agent/skills/principle-*/` → NOVO | 3 SKILL.md |
| T-B2 | Skill `sdd-tdd` | `.agent/skills/sdd-tdd/SKILL.md` → NOVO | RED → IMPLEMENT → GREEN + skip |
| T-B3 | Playbooks novos | `playbooks/` → NOVO | investigation, design, prototype, user-story, tdd-implement, multi-phase |
| T-B4 | Templates story e design | `specs/stories/`, `docs/design/` → NOVO | `_STORY_TEMPLATE.md`, `_DESIGN_TEMPLATE.md` |
| T-B5 | Ligar TDD nos playbooks de código | `bug-fix.md`, `feature.md`, `refactor.md` → MOD | passo dispara `sdd-tdd` |

## Fase C — Kit humano

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| T-C1 | Prompts viram ponteiros | `prompts/*.md` → MOD | cada um cita o playbook; passos longos removidos ou reduzidos a checklist humano |
| T-C2 | QUICKSTART aponta playbook + perfil | `QUICKSTART/*.md` → MOD | cada guia tem playbook e perfil |
| T-C3 | Workflows agente | `.agent/workflows/` → MOD | ponteiro para playbook |
| T-C4 | FILE_GUIDE, README, AGENTS, specs/README, SDD_WORKFLOW §14 | docs + raiz → MOD | entrada via sdd-mode; gates por perfil |
| T-C5 | tooling Cursor | `tooling/cursor/` → MOD | rule carrega sdd-mode |
| T-C6 | Consistência | repo | T-SDD_MODE-01..04 da SPEC |
