# skills

| Caminho | Papel |
|---|---|
| `sdd-mode/` | Interface do agente SDD: roteador + playbooks |
| `sdd-tdd/` | RED → IMPLEMENT → GREEN |
| `principle-*/` | Uma regra SDD por skill |
| `_example_skill/` | Template para skill de **domínio** da stack do produto |

O método permanece em `docs/SDD_WORKFLOW.md`. Esta pasta é o procedimento.

Agentes que só leem `.grok/skills/` ou um plugin: copiem ou registrem
`sdd-mode` e as principles. Não duplique o corpo; `tooling/` explica o adapter.
