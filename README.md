# sdd-starter

> Guia pratico e conjunto de templates para aplicar **Spec-Driven
> Development** em projetos de software de qualquer stack e em qualquer
> ambiente de trabalho.

`sdd-starter` organiza uma demanda antes que ela vire codigo. O fluxo transforma
intencao em artefatos pequenos, revisaveis e rastreaveis: brief, spec,
clarificacoes, decisoes, plano, tarefas, validacao e handover.

Ele ajuda especialmente quando agentes de IA participam do desenvolvimento,
porque velocidade sem contexto perde decisoes, escopo e criterios de aceite
muito rapido. Ainda assim, o metodo nao depende de uma IDE, de um agente, de um
terminal, de um provider, de um modelo ou de uma stack especifica.

---

## O Fluxo

```text
Demanda
  -> Brief
  -> Spec
  -> Clarify
  -> ADRs quando houver trade-off
  -> Plan
  -> Tasks
  -> Implement
  -> Validate
  -> Commit
  -> Handover
```

O workflow completo esta em [`docs/SDD_WORKFLOW.md`](docs/SDD_WORKFLOW.md).
Esse documento e o nucleo canonico do repo.

Se voce abriu o repo e nao sabe para que serve cada arquivo, comece pelo mapa
em [`docs/FILE_GUIDE.md`](docs/FILE_GUIDE.md).

## Por Que SDD

Sem um fluxo explicito, projetos tendem a acumular:

- implementacao antes de requisito claro;
- decisoes tecnicas sem registro;
- regressao silenciosa entre sessoes;
- onboarding lento;
- contexto que existe apenas na memoria de uma pessoa ou conversa.

SDD reduz esse risco com seis principios:

| Principio | Significa |
|---|---|
| **Spec-first** | Mudanca significativa começa por escopo e criterio de aceite claros |
| **Gates humanos** | Planejamento, tarefas, validacao e entrega tem pontos de revisao |
| **Fonte primaria** | Decisao tecnica relevante registra referencia verificavel |
| **Backward-compat** | Cada entrega preserva um estado compreensivel e reversivel |
| **Rastreabilidade** | Codigo volta para tarefa, spec e decisao quando aplicavel |
| **Handover** | Trabalho em andamento deixa estado retomavel |

Nem toda mudanca exige o mesmo peso. Bug simples, feature pequena, refatoracao
arquitetural e greenfield usam niveis de rigor diferentes.

## Comece Pelo Seu Cenario

| Cenario | Comece aqui |
|---|---|
| Projeto novo | [`QUICKSTART/greenfield.md`](QUICKSTART/greenfield.md) |
| Projeto existente com pouca documentacao | [`QUICKSTART/brownfield.md`](QUICKSTART/brownfield.md) |
| Bug fix | [`QUICKSTART/bug-fix.md`](QUICKSTART/bug-fix.md) |
| Feature pequena | [`QUICKSTART/small-feature.md`](QUICKSTART/small-feature.md) |
| Feature media | [`QUICKSTART/medium-feature.md`](QUICKSTART/medium-feature.md) |
| Feature grande | [`QUICKSTART/large-feature.md`](QUICKSTART/large-feature.md) |
| Refatoracao | [`QUICKSTART/refactor.md`](QUICKSTART/refactor.md) |
| Retomar uma sessao | [`prompts/RESUME.md`](prompts/RESUME.md) |

## Como Navegar

| Pergunta | Resposta |
|---|---|
| "Qual arquivo leio primeiro?" | `README.md`, depois `docs/FILE_GUIDE.md` |
| "Onde esta o metodo completo?" | `docs/SDD_WORKFLOW.md` |
| "Qual guia sigo agora?" | `QUICKSTART/README.md` |
| "Qual prompt uso?" | `prompts/README.md` |
| "Onde ficam specs, plans e ADRs?" | `specs/README.md` |
| "O que e opcional por ferramenta?" | `tooling/README.md` |

## Kit Minimo

Para aplicar o metodo, o leitor precisa entender primeiro estes artefatos:

| Arquivo ou pasta | Papel |
|---|---|
| `docs/SDD_WORKFLOW.md` | Fluxo, fases, gates e criterios de uso |
| `PROJECT_BRIEF.md` | Contexto inicial do projeto |
| `specs/` | Specs, planos, tasks e ADRs |
| `prompts/` | Prompts reutilizaveis para bootstrap, discover, feature, fix e handover |
| `docs/_*_TEMPLATE.md` | Templates de arquitetura e handover |
| `AGENTS.md` | Instrucoes do projeto quando agentes participam do fluxo |

`AGENTS.md` e util em projetos assistidos por agentes, mas o workflow SDD nao
exige uma ferramenta especifica para existir.

## Modos De Uso

| Modo | Artefatos tipicos | Gates ativos |
|---|---|---|
| Bug fix simples | teste/regressao, validacao e diff | validacao e commit |
| Feature pequena | spec existente atualizada, tasks curtas | tasks, validacao e commit |
| Feature media | spec, plan, tasks e handover | todos |
| Feature grande | spec e plano por fases | todos por fase |
| Refatoracao interna | decisao e tasks curtas quando houver risco | validacao e commit |
| Refatoracao arquitetural | spec, ADR, plan e tasks | todos |
| Greenfield | brief, architecture, specs e planos iniciais | todos |
| Brownfield | discover, brief retroativo, indice e decisoes detectadas | adaptado ao estado real |

## Estrutura Do Starter

```text
sdd-starter/
├── README.md
├── AGENTS.md
├── PROJECT_BRIEF.md
├── docs/
│   ├── SDD_WORKFLOW.md
│   ├── FILE_GUIDE.md
│   ├── _ARCHITECTURE_TEMPLATE.md
│   └── _HANDOVER_TEMPLATE.md
├── specs/
│   ├── README.md
│   ├── SPEC_INDEX.md
│   ├── modules/_SPEC_TEMPLATE.md
│   ├── plans/_PLAN_TEMPLATE.md
│   ├── plans/_TASKS_TEMPLATE.md
│   └── decisions/_ADR_TEMPLATE.md
├── prompts/
│   └── README.md
├── QUICKSTART/
│   └── README.md
├── .agent/
├── scripts/
├── tests/
└── tooling/                 opcional, por ambiente/ferramenta
```

`prompts/` e `.agent/` ajudam a operar o metodo com assistencia, mas os
artefatos SDD continuam legiveis para qualquer desenvolvedor.

## Ferramentas E Stacks

O starter nao escolhe stack por voce. Cada projeto registra linguagem,
framework, infraestrutura, regras de qualidade e comandos de validacao nos
artefatos do proprio projeto.

O starter tambem nao escolhe ambiente de execucao. Ele pode ser usado com:

- edicao e revisao humanas;
- agentes em IDE;
- agentes em terminal;
- agentes remotos ou assincronos;
- combinacoes desses modos.

Quando uma ferramenta precisar de arquivos ou instrucoes proprias, use o
material opcional em [`tooling/`](tooling/). Ele adapta a execucao, nao redefine
o workflow.

## Como Adotar

### Projeto novo

1. Crie um repo a partir deste template.
2. Preencha `PROJECT_BRIEF.md`.
3. Use [`prompts/BOOTSTRAP.md`](prompts/BOOTSTRAP.md) ou siga o quickstart
   greenfield manualmente.
4. Pare no primeiro PLAN aprovado antes de implementar.

### Projeto existente

1. Copie apenas o kit SDD que nao conflita com o repo existente.
2. Use [`prompts/DISCOVER.md`](prompts/DISCOVER.md) para mapear o estado real.
3. Adote specs e ADRs de forma gradual, sem reescrever o historico.

## Contribuir

Antes de propor mudanca ao framework:

1. Verifique se ela melhora o fluxo SDD em mais de uma stack e mais de um
   ambiente de trabalho.
2. Separe regra do metodo de exemplo ou nota de tooling.
3. Registre trade-off relevante em ADR quando a mudanca alterar o workflow.
4. Mantenha o core simples de ler.

## Licenca

MIT. Veja [`LICENSE`](LICENSE).
