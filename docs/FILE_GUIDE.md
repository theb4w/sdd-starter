# FILE_GUIDE - Como navegar no sdd-starter

Este arquivo responde a pergunta: "para que serve cada coisa aqui?"

Use como mapa antes de adaptar o template a um projeto real.

---

## Leia nesta ordem

| Ordem | Arquivo | Quando ler |
|---|---|---|
| 1 | `README.md` | Para entender a proposta e escolher um caminho |
| 2 | `docs/SDD_WORKFLOW.md` | Para entender o metodo SDD completo |
| 3 | `QUICKSTART/<cenario>.md` | Para aplicar o metodo ao seu caso |
| 4 | `PROJECT_BRIEF.md` | Para registrar o contexto inicial do projeto |
| 5 | `specs/SPEC_INDEX.md` | Para acompanhar modulos, status e ADRs |
| 6 | `.agent/skills/sdd-mode/SKILL.md` | Procedimento do agente (playbooks) |
| 7 | `prompts/<fluxo>.md` | Ponte humana para o playbook |
| 8 | `AGENTS.md` | Constituicao quando agentes participam |

Se voce so quer experimentar, leia `README.md` e depois o quickstart do seu
cenario. Se voce vai manter o repo, leia tambem `docs/SDD_WORKFLOW.md`.

---

## Tipos de arquivo

| Tipo | Como reconhecer | O que fazer |
|---|---|---|
| Guia | `README.md`, `docs/SDD_WORKFLOW.md`, `QUICKSTART/*.md` | Ler; normalmente nao copiar trecho por trecho |
| Template | nomes com `_TEMPLATE.md` ou placeholders `<...>` | Copiar e preencher para criar artefatos reais |
| Artefato de projeto | `PROJECT_BRIEF.md`, `AGENTS.md`, `specs/SPEC_INDEX.md` | Editar no projeto que adota SDD |
| Skill de modo | `.agent/skills/sdd-mode/` | Invocar; o agente copia os passos do playbook |
| Prompt | `prompts/*.md` | Ponteiro curto para o playbook (humano sem slash) |
| Tooling opcional | `tooling/*` | Usar somente se aquela ferramenta for adotada |
| Exemplo/convenção | `.agent/`, `scripts/`, `tests/` | Adaptar conforme o projeto; nao sao obrigatorios para todo mundo |

---

## Raiz do repositório

| Arquivo | Serve para | Voce edita? |
|---|---|---|
| `README.md` | Porta de entrada humana do starter | Sim, se melhorar a explicacao do framework |
| `PROJECT_BRIEF.md` | Brief inicial do projeto que adotara SDD | Sim, no projeto real |
| `AGENTS.md` | Instrucoes para agentes quando eles participam | Sim, no projeto real |
| `LICENSE` | Licenca MIT | Nao, salvo decisao de licenca |

`PROJECT_BRIEF.md` e `AGENTS.md` sao templates vivos. Eles devem ser adaptados
quando o starter e usado em outro repo.

---

## `docs/`

| Arquivo | Serve para |
|---|---|
| `SDD_WORKFLOW.md` | Workflow canonico do metodo SDD |
| `FILE_GUIDE.md` | Mapa de navegacao do starter |
| `_ARCHITECTURE_TEMPLATE.md` | Base para documentar arquitetura do projeto real |
| `_HANDOVER_TEMPLATE.md` | Base para encerrar uma sessao com estado retomavel |
| `design/_DESIGN_TEMPLATE.md` | Exploracao (UX/forma) antes de SPEC/codigo |

Regra simples: `SDD_WORKFLOW.md` explica o metodo; arquivos com `_TEMPLATE`
viram artefatos preenchidos em projetos reais.

---

## `specs/`

| Caminho | Serve para |
|---|---|
| `SPEC_INDEX.md` | Painel de status dos modulos, ADRs e proximos passos |
| `modules/_SPEC_TEMPLATE.md` | Template de especificacao de modulo/feature |
| `stories/_STORY_TEMPLATE.md` | Template de user story (exige SPEC de modulo) |
| `plans/_PLAN_TEMPLATE.md` | Template de plano antes de implementar |
| `plans/_TASKS_TEMPLATE.md` | Template de tarefas atomicas com criterios de aceite |
| `decisions/_ADR_TEMPLATE.md` | Template de decisao arquitetural |

Em um projeto real, voce cria arquivos novos a partir desses templates:

```text
specs/modules/SPEC_AUTH.md
specs/plans/PLAN_AUTH.md
specs/plans/TASKS_AUTH.md
specs/decisions/ADR-001-auth-provider.md
```

---

## `prompts/`

Ponte humana. Passos canônicos: `.agent/skills/sdd-mode/playbooks/`.

| Prompt | Playbook |
|---|---|
| `BOOTSTRAP.md` | `bootstrap.md` |
| `DISCOVER.md` | `discover.md` |
| `ONBOARDING.md` | `onboarding.md` |
| `RESUME.md` | `resume.md` |
| `NEW_FEATURE.md` | `feature.md` |
| `BUG_FIX.md` | `bug-fix.md` |
| `REFACTOR.md` | `refactor.md` |
| `HANDOVER.md` | `handover.md` |

---

## `QUICKSTART/`

| Arquivo | Serve para |
|---|---|
| `greenfield.md` | Comecar projeto novo com SDD |
| `brownfield.md` | Adotar SDD em projeto existente |
| `bug-fix.md` | Corrigir bug com fluxo enxuto |
| `small-feature.md` | Feature pequena sem burocracia excessiva |
| `medium-feature.md` | Feature media com spec/plan/tasks |
| `large-feature.md` | Feature grande ou multi-fase |
| `refactor.md` | Refatoracao interna ou arquitetural |

Use apenas um quickstart por vez. O quickstart escolhe quais artefatos sao
necessarios para aquele tipo de trabalho.

---

## `.agent/`

| Caminho | Serve para |
|---|---|
| `.agent/agents.md` | Personas reutilizaveis como @pm, @engineer, @qa, @devops |
| `.agent/skills/sdd-mode/` | Skill de modo: roteador + playbooks (procedimento) |
| `.agent/skills/principle-*/` | Uma regra SDD por arquivo |
| `.agent/skills/sdd-tdd/` | Loop RED → IMPLEMENT → GREEN |
| `.agent/skills/_example_skill/` | Template de skill de *dominio* (stack do produto) |
| `.agent/workflows/` | Ponteiros para os playbooks equivalentes |

`sdd-mode` nao substitui `docs/SDD_WORKFLOW.md`. O workflow e o metodo; a skill
e como o agente executa agora. Plugin/IDE continua opt-in em `tooling/`.

---

## `tooling/`

| Caminho | Serve para |
|---|---|
| `tooling/README.md` | Explica como usar arquivos opcionais de ferramenta |
| `tooling/antigravity/GEMINI.md` | Exemplo opcional para projetos que usam Antigravity |
| `tooling/cursor/` | Rules opcionais para projetos que usam Cursor |

Tooling e opt-in. Copie somente o que o projeto realmente adotou.

---

## `scripts/` e `tests/`

| Pasta | Serve para |
|---|---|
| `scripts/` | Convenções para scripts de setup, deploy, smoke, auditoria e migracao |
| `tests/` | Estrutura inicial para testes unitarios, integracao e smoke quando aplicavel |

Essas pastas sao pontos de extensao. O starter nao define uma stack de teste ou
linguagem padrao.

---

## O que editar primeiro em um projeto real

1. `PROJECT_BRIEF.md`
2. `AGENTS.md`, se agentes participarem
3. `specs/SPEC_INDEX.md`
4. `docs/<Project>_Architecture.md`, criado a partir do template
5. `specs/modules/SPEC_<MODULO>.md`, criado a partir do template

Nao comece editando `tooling/` se ainda nao souber qual ambiente de trabalho
sera usado. A skill `sdd-mode` ja vem no template; nao a substitua por rules
de IDE.

Quando o trabalho comecar, invoque `sdd-mode` e o playbook do cenario.

