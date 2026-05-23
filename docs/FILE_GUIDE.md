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
| 6 | `prompts/<fluxo>.md` | Para conduzir uma sessao com assistencia |
| 7 | `AGENTS.md` | Para orientar agentes quando eles participarem |

Se voce so quer experimentar, leia `README.md` e depois o quickstart do seu
cenario. Se voce vai manter o repo, leia tambem `docs/SDD_WORKFLOW.md`.

---

## Tipos de arquivo

| Tipo | Como reconhecer | O que fazer |
|---|---|---|
| Guia | `README.md`, `docs/SDD_WORKFLOW.md`, `QUICKSTART/*.md` | Ler; normalmente nao copiar trecho por trecho |
| Template | nomes com `_TEMPLATE.md` ou placeholders `<...>` | Copiar e preencher para criar artefatos reais |
| Artefato de projeto | `PROJECT_BRIEF.md`, `AGENTS.md`, `specs/SPEC_INDEX.md` | Editar no projeto que adota SDD |
| Prompt | `prompts/*.md` | Colar/adaptar em uma sessao de trabalho |
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

### Por que `PROJECT_BRIEF.md` existe?

`PROJECT_BRIEF.md` e a primeira fonte de contexto do projeto. Ele responde:

- o que o projeto quer resolver;
- para quem;
- quais restricoes existem;
- quais modulos parecem necessarios;
- o que fica fora do MVP;
- como sucesso sera medido.

Ele e essencial porque evita que o primeiro agente ou desenvolvedor comece pela
stack, pela pasta de codigo ou por suposicoes. O brief ancora o problema antes
da solucao.

Quem preenche:

| Cenario | Como o brief nasce |
|---|---|
| Greenfield | Humano preenche primeiro; agente pode ajudar a organizar, mas nao inventar objetivo |
| Brownfield sem docs | Agente pode gerar rascunho via `DISCOVER.md`, marcando incertezas com `[?]` |
| Projeto SDD existente | Brief ja existe; specs, ADRs e handovers mais recentes podem complementar ou superar detalhes antigos |

Regra: agente pode **rascunhar** o brief quando houver codigo ou conversa
suficiente, mas humano deve validar objetivo, escopo, restricoes e fora-do-MVP.

---

## `docs/`

| Arquivo | Serve para |
|---|---|
| `SDD_WORKFLOW.md` | Workflow canonico do metodo SDD |
| `FILE_GUIDE.md` | Mapa de navegacao do starter |
| `_ARCHITECTURE_TEMPLATE.md` | Base para documentar arquitetura do projeto real |
| `_HANDOVER_TEMPLATE.md` | Base para encerrar uma sessao com estado retomavel |

Regra simples: `SDD_WORKFLOW.md` explica o metodo; arquivos com `_TEMPLATE`
viram artefatos preenchidos em projetos reais.

---

## `specs/`

| Caminho | Serve para |
|---|---|
| `SPEC_INDEX.md` | Painel de status dos modulos, ADRs e proximos passos |
| `modules/_SPEC_TEMPLATE.md` | Template de especificacao de modulo/feature |
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

| Prompt | Use quando |
|---|---|
| `BOOTSTRAP.md` | Projeto novo ou projeto existente com brief preenchido |
| `DISCOVER.md` | Projeto existente sem documentacao suficiente |
| `ONBOARDING.md` | Nova sessao ou novo dev em projeto que ja usa SDD |
| `RESUME.md` | Retomar uma fase que ja tem PLAN/TASKS aprovados |
| `NEW_FEATURE.md` | Iniciar ou continuar uma feature |
| `BUG_FIX.md` | Corrigir bug com rastreabilidade proporcional |
| `REFACTOR.md` | Refatorar sem perder justificativa e rollback |
| `HANDOVER.md` | Encerrar sessao deixando o estado retomavel |

Prompts sao roteiros. Ajuste placeholders, cole no canal de assistencia adotado
ou use como checklist manual.

---

## `QUICKSTART/`

| Arquivo | Serve para |
|---|---|
| `greenfield.md` | Comecar projeto novo com SDD |
| `brownfield.md` | Adotar SDD em projeto existente |
| `cloned-repo.md` | Entrar em um repo que ja usa SDD |
| `bug-fix.md` | Corrigir bug com fluxo enxuto |
| `small-feature.md` | Feature pequena sem burocracia excessiva |
| `medium-feature.md` | Feature media com spec/plan/tasks |
| `large-feature.md` | Feature grande ou multi-fase |
| `refactor.md` | Refatoracao interna ou arquitetural |

Use apenas um quickstart por vez. O quickstart escolhe quais artefatos sao
necessarios para aquele tipo de trabalho.

`cloned-repo.md` e para onboarding em projeto SDD existente. `brownfield.md` e
para instalar/adotar SDD em projeto que ainda nao tem o metodo.

---

## `.agent/`

| Caminho | Serve para |
|---|---|
| `.agent/agents.md` | Personas reutilizaveis como @pm, @engineer, @qa, @devops |
| `.agent/workflows/` | Roteiros operacionais para bootstrap, discover e implementacao |
| `.agent/skills/` | Exemplo de regras tecnicas por dominio |

Esta pasta ajuda quando o projeto trabalha com assistencia por agentes. Ela nao
substitui o workflow SDD nem e obrigatoria para todo projeto.

### Onde `.agent/workflows/` entra no fluxo?

Pense nos arquivos de `.agent/workflows/` como o "manual interno" de execucao
dos prompts:

| Workflow | Usado junto com | Entra quando |
|---|---|---|
| `sdd_bootstrap.md` | `prompts/BOOTSTRAP.md` | projeto novo ou projeto com brief preenchido vai iniciar SDD |
| `sdd_discover.md` | `prompts/DISCOVER.md` | projeto existente precisa ser entendido antes de documentar |
| `sdd_implement.md` | `prompts/RESUME.md` ou `prompts/NEW_FEATURE.md` | PLAN e TASKS ja foram aprovados e chegou a hora de implementar |

`docs/SDD_WORKFLOW.md` define o metodo. `prompts/*.md` conduzem a sessao.
`.agent/workflows/*.md` detalham como um agente deve executar aquela sessao sem
pular gates.

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

Nao comece editando `tooling/` ou `.agent/` se ainda nao souber qual ambiente
de trabalho sera usado.
