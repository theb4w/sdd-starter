# INDEX — módulos e decisões (sdd-starter)

> **Fonte canônica do estado de cada módulo do projeto.**
> Mantenha sincronizado com `AGENTS.md` (tabela de módulos) e
> `SDD/architecture.md` §5 (Módulos).

Este índice, neste repositório, descreve o **próprio starter**. Quando você
adaptar o template a um produto, substitua as linhas abaixo pelos módulos
desse produto.

---

## Status válidos

| Símbolo | Significado |
|---|---|
| 📝 RASCUNHO | SPEC criada, esqueleto preenchido, CLARIFY pendente |
| 🔍 CLARIFY | Perguntas abertas aguardando resposta humana |
| 📋 PLAN | CLARIFY resolvido, PLAN gerado, aguarda **GATE 1** |
| ✅ APROVADO | PLAN+TASKS aprovados, IMPLEMENT pode começar |
| 🚧 IMPLEMENT | Em desenvolvimento (incluir % concluído ou fase atual) |
| ✔️ CONCLUÍDO | Deployado em produção, smoke OK, handover gerado |
| ⏸️ PAUSADO | Trabalho suspenso (registrar razão no rodapé) |
| ❌ CANCELADO | Decidiu-se não implementar (registrar ADR de justificativa) |

---

## Módulos

| Módulo | Spec | ADRs aplicáveis | Status | Observações |
|---|---|---|---|---|
| SDD_CORE_NEUTRALITY | (editorial; PLAN/TASKS em `SDD/plans/`) | — | ✔️ | Core tool-neutral |
| SDD_MODE | `SDD/modules/SPEC_SDD_MODE.md` | ADR-001, ADR-002 | ✔️ CONCLUÍDO | Skill de modo + playbooks |

---

## ADRs (Architectural Decision Records)

| ID | Decisão | Arquivo | Status |
|---|---|---|---|
| ADR-001 | Skill de modo como interface, não plugin | `SDD/decisions/ADR-001-skill-as-interface.md` | ✔️ ACEITO |
| ADR-002 | Perfis de gate (`observe`…`full`) | `SDD/decisions/ADR-002-gate-profiles.md` | ✔️ ACEITO |

---

## Próximos Passos

- [x] Fundação `sdd-mode` (fase A)
- [x] Camada extra: design, story, TDD (fase B)
- [x] Reorganizar sdd-mode playbooks (see .agent/skills/sdd-mode/playbooks/)quickstarts (fase C)

---

## Histórico de Mudanças no Projeto

| Data | Sessão | Mudança | Handover |
|---|---|---|---|
| 2026-05-22 | Neutralidade do core | README/workflow/tooling SDD-first | — |
| 2026-08-25 | Skill de modo | `sdd-mode` + perfis de gate + playbooks | — |

---

*Última atualização: 2026-08-25 | Sincronizar com `AGENTS.md` e `SDD/architecture.md`.*
