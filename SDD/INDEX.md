# INDEX — sdd-starter

**Última atualização:** 2026-08-27

## Módulos

| Módulo | Spec | ADRs | Status | Notas |
|---|---|---|---|---|
| SDD_MODE | `SDD/modules/SPEC_SDD_MODE.md` | ADR-001, ADR-002, ADR-003 | ✔️ | Skill de modo; gera `SDD/`; default agentic |

## ADRs

| ID | Decisão | Arquivo | Status |
|---|---|---|---|
| ADR-001 | Skill de modo como interface, não plugin | `SDD/decisions/ADR-001-skill-as-interface.md` | ✔️ ACEITO |
| ADR-002 | Perfis de gate | `SDD/decisions/ADR-002-gate-profiles.md` | ✔️ ACEITO |
| ADR-003 | Default `agentic` (humano no pacote) | `SDD/decisions/ADR-003-agentic-default.md` | ✔️ ACEITO |

## Próximos passos

- [x] `sdd-mode` + playbooks + principles
- [x] Processo em `SDD/` (sem specs/docs/prompts paralelos)
- [x] Limpeza residual (workflow stack-neutral, prosa quebrada)
- [x] Skills ancoradas em spec-kit / Antigravity + fontes de SE (`references/sdd-basis.md`)
- [x] Perfil `agentic` + review do agente + índice de intenção (ADR-003)

## Histórico

| Data | Mudança |
|---|---|
| 2026-05-22 | Core tool-neutral |
| 2026-08-25 | Skill de modo |
| 2026-08-26 | Geração `SDD/`; remoção do kit paralelo; limpeza |
| 2026-08-27 | ADR-003 agentic; playbook review; match por intenção |
