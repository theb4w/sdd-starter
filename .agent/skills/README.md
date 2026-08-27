# skills

Este checkout usa `.agent/skills/`. Outros hosts: `sdd-mode/references/install.md`. Cursor neste repo: `.cursor/rules/sdd-under-pstack.mdc` (não depende de copiar as skills). Sob pstack: `sdd-mode/references/with-pstack.md`.

Agente: não carregar `_example_skill/` nem `../agents.md` (personas) a menos que o humano peça. Skills agent-facing são inglês.

| Caminho | Papel |
|---|---|
| `sdd-mode/` | Interface: roteador + playbooks + templates → `SDD/` |
| `sdd-mode/references/catalog.md` | Intenção → playbook (ganha se houver drift) |
| `sdd-tdd/` | RED → IMPLEMENT → GREEN |
| `principle-*/` | Uma regra SDD por skill |
| `_example_skill/` | Opcional: copiar para skill de **domínio** da stack |

Personas em `.agent/agents.md` são opcionais (`@pm` etc.). `sdd-mode` não depende delas.

Base da comunidade (spec-kit / Antigravity) e fontes de SE: `sdd-mode/references/sdd-basis.md`.
Método (fases): `sdd-mode/references/workflow.md`. Processo do produto: `SDD/` na raiz do alvo.

Cada principle: regra, por quê (defeito se ignorar), padrão, limites, URL. Sem URL, a afirmação não entra.
