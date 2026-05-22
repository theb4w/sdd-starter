# PLAN_SDD_CORE_NEUTRALITY - Refatoracao do starter SDD-first

**Status:** aprovado para implementacao nesta branch
**Autor:** Codex + Allan
**Data:** 2026-05-22
**Base:** discussao de direcao do `sdd-starter`

---

## Objetivo

Tornar o `sdd-starter` mais claro como guia e kit de artefatos de
Spec-Driven Development, sem fazer o fluxo principal depender de IDE, agente,
terminal, provider, modelo, linguagem, framework ou cloud.

O workflow SDD que nasceu neste repo continua sendo o nucleo canônico. Setups
opinionados, como o Setup IA Dev v7.1, sao aplicacoes do metodo e nao fontes de
dependencia para o core.

## Decisoes de escopo

- O caminho principal explica SDD antes de citar ferramentas.
- Exemplos concretos continuam permitidos quando rotulados como exemplos.
- `AGENTS.md` continua util para projetos que trabalham com agentes, mas nao
  deve virar manual de uma IDE.
- Material especifico de tooling fica opcional e separado do fluxo principal.
- Esta branch neutraliza o core editorial primeiro; automacoes e CI ficam para
  uma validacao posterior.

## Entregas desta branch

1. Reposicionar `README.md` para SDD-first e orientar o leitor por cenario.
2. Neutralizar `AGENTS.md` e `docs/SDD_WORKFLOW.md` onde havia linguagem de
   Cursor, Antigravity ou stack exemplo como regra universal.
3. Ajustar quickstarts para instalar/adotar o core sem copiar tooling
   especifico por default.
4. Separar notas e assets opcionais de tooling fora do caminho principal.
5. Validar que o core continua legivel para greenfield, brownfield e retomada.

## Fora de escopo

- Definir uma stack de referencia para projetos que adotam SDD.
- Importar o Setup IA Dev v7.1 para este repo.
- Prometer suporte completo a cada agente ou IDE existente.
- Criar automacao de bootstrap ou CI de validacao nesta primeira refatoracao.

## Criterios de aceite

- A abertura do README explica SDD sem exigir ferramenta ou stack.
- Os quickstarts principais funcionam sem copiar `.cursor` ou `GEMINI.md`.
- O workflow canônico usa linguagem de fase e artefato SDD, nao modos de IDE.
- Material especifico de tooling fica explicitamente opcional.
- O diff preserva templates, prompts e estrutura SDD ja existentes.
