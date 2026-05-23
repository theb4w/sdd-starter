# prompts

Prompts sao roteiros reutilizaveis para conduzir sessoes SDD com assistencia.
Tambem podem ser usados como checklist manual.

| Prompt | Papel |
|---|---|
| `BOOTSTRAP.md` | Inicializar SDD a partir de um brief |
| `DISCOVER.md` | Mapear projeto existente sem documentacao suficiente |
| `ONBOARDING.md` | Entrar em projeto SDD existente |
| `RESUME.md` | Retomar fase em andamento |
| `NEW_FEATURE.md` | Trabalhar em feature |
| `BUG_FIX.md` | Corrigir bug com rastreabilidade proporcional |
| `REFACTOR.md` | Refatorar com decisao e rollback quando necessario |
| `HANDOVER.md` | Encerrar sessao deixando estado retomavel |

Antes de usar, substitua placeholders como `<PROJETO>`, `<MODULO>` e `<DATA>`.

## Relacao com `.agent/workflows/`

Os prompts sao o roteiro que voce usa na conversa. Os workflows em
`.agent/workflows/` explicam a execucao interna esperada para alguns desses
roteiros:

| Prompt | Workflow de apoio |
|---|---|
| `BOOTSTRAP.md` | `.agent/workflows/sdd_bootstrap.md` |
| `DISCOVER.md` | `.agent/workflows/sdd_discover.md` |
| `RESUME.md` / `NEW_FEATURE.md` | `.agent/workflows/sdd_implement.md` quando chega na fase IMPLEMENT |

Se voce nao usa agentes, trate os workflows como checklists detalhados.
