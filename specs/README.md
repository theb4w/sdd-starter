# specs

Esta pasta guarda o estado rastreavel do trabalho.

| Area | Papel |
|---|---|
| `SPEC_INDEX.md` | Painel de status dos modulos e decisoes |
| `modules/` | Especificacoes de modulo ou feature |
| `stories/` | User stories (fatia; exige SPEC de modulo) |
| `plans/` | Planos e tarefas antes de implementar |
| `decisions/` | ADRs, uma decisao relevante por arquivo |

## Ciclo de arquivos

```text
SPEC_<MODULO>.md
  -> PLAN_<MODULO>.md
  -> TASKS_<MODULO>.md
  -> implementacao + validacao
  -> handover
```

Templates com `_TEMPLATE.md` nao sao artefatos finais. Copie, renomeie e
preencha para o projeto real.

