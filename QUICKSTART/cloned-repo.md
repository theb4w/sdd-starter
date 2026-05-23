# QUICKSTART - Clone de um repo que ja usa SDD

> **Cenario:** voce clonou um projeto que ja contem `docs/SDD_WORKFLOW.md`,
> `specs/SPEC_INDEX.md`, specs, plans ou handovers. Seu objetivo e entender o
> estado atual antes de trabalhar.

Este fluxo e de **onboarding**, nao de bootstrap. Nao adapte templates nem
reorganize o repo antes de entender o que ja existe.

---

## Resultado esperado

Ao final, voce deve saber:

- qual e o objetivo do projeto;
- quais regras e gates valem;
- quais modulos existem;
- qual foi o ultimo estado registrado;
- qual e a proxima acao segura;
- se deve usar `RESUME`, `NEW_FEATURE`, `BUG_FIX` ou `REFACTOR`.

---

## Passo 1 - Clonar e checar o estado

```bash
git clone <repo-url>
cd <repo>
git status --short --branch
```

Nao implemente nada ainda.

---

## Passo 2 - Ler os arquivos de orientacao

Leia nesta ordem:

1. `README.md`
2. `docs/FILE_GUIDE.md`, se existir
3. `docs/SDD_WORKFLOW.md`
4. `AGENTS.md`, se agentes participam do projeto
5. instrucoes opcionais em `tooling/`, se o projeto adotou alguma

Objetivo: entender o metodo e as regras antes de olhar a tarefa.

---

## Passo 3 - Ler o estado do projeto

Leia:

1. `PROJECT_BRIEF.md`
2. `specs/SPEC_INDEX.md`
3. `docs/<Project>_Architecture.md`, se existir
4. `docs/handover_*.md` mais recente
5. SPEC/PLAN/TASKS do modulo em andamento, se houver

Se houver varios handovers, comece pelo mais recente.

---

## Passo 4 - Usar ONBOARDING

Use `prompts/ONBOARDING.md` para resumir o estado.

Se estiver trabalhando com assistencia, cole o prompt no canal adotado. Se
estiver trabalhando manualmente, use o prompt como checklist.

O output esperado e:

```text
- identidade do projeto
- regras obrigatorias
- estado atual dos modulos
- ADRs relevantes
- pendencias ou bloqueios
- proximo passo natural
```

---

## Passo 5 - Escolher o proximo fluxo

| Estado encontrado | Proximo fluxo |
|---|---|
| Ha fase em andamento com PLAN/TASKS aprovados | `prompts/RESUME.md` |
| Ha bug reportado | `prompts/BUG_FIX.md` |
| Ha nova demanda | `prompts/NEW_FEATURE.md` |
| Ha refatoracao proposta | `prompts/REFACTOR.md` |
| Nao ha docs SDD suficientes | volte para `QUICKSTART/brownfield.md` |

---

## Passo 6 - So entao editar

Antes da primeira edicao, confirme:

- branch correta;
- ultimo handover entendido;
- tarefa ou fluxo escolhido;
- gates aplicaveis;
- criterio de aceite claro.

Se alguma dessas respostas estiver incerta, pare e faça CLARIFY.

---

## Anti-padroes

- Comecar pelo codigo sem ler `SPEC_INDEX.md`.
- Usar `BOOTSTRAP.md` em repo que ja usa SDD.
- Ignorar handover e reabrir decisoes ja tomadas.
- Tratar `PROJECT_BRIEF.md` como verdade absoluta se specs e handovers mais
  recentes mostram evolucao do projeto.
