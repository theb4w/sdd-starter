# INDEX — sdd-starter

**Última atualização:** 2026-08-27

## Módulos

| Módulo | Spec | ADRs | Status | Notas |
|---|---|---|---|---|
| SDD_MODE | `SDD/modules/SPEC_SDD_MODE.md` | ADR-001, ADR-002, ADR-003 | ✔️ | Skill de modo; skill root host-agnostic; default agentic; contrato sob pstack |

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
- [x] Skill root host-agnostic; Step 0 (não “preamble”); catálogo = headers; resíduos agentic; sdd-mode sob pstack
- [x] Colagem Cursor (rule always-on + install); never-block cindido; índice inline de principles; workflow apêndice
- [x] Template AGENTS enxuto + `Smoke:`; resume sem GO extra; review recusa accept sem G3; dry-run A–E

## Histórico

| Data | Mudança |
|---|---|
| 2026-05-22 | Core tool-neutral |
| 2026-08-25 | Skill de modo |
| 2026-08-26 | Geração `SDD/`; remoção do kit paralelo; limpeza |
| 2026-08-27 | ADR-003 agentic; playbook review; match por intenção |
| 2026-08-27 | Skill root; Step 0; catalog.md SSOT; mermaid agentic; with-pstack |
| 2026-08-27 | Cursor glue; policy split; principles index; Smoke/G3; dry-run |
| 2026-08-27 | Dry-run A (headers = catalog): pass. B–E: `references/dry-run.md` |
