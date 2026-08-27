<!--
═══════════════════════════════════════════════════════════════════════════════
  Template de TASKS (decomposição atômica) de módulo
═══════════════════════════════════════════════════════════════════════════════

  Como usar:
  1. Copie para SDD/plans/TASKS_<MODULO>.md
  2. Pré-requisito: PLAN_<MODULO>.md escrito (`full`: GATE 1)
  3. Cada task = 1 commit lógico, ~10-30 LOC, com AC verificável
  4. Tarefas [bloq.] são gates (não pular sem o stop do perfil)
  5. `full`: aguarde GATE 2. `agentic`: grave TASKS e IMPLEMENT.

  Convenções de ID:
  - T-<FASE><N>  (T-A1, T-B2, T-C1.3 quando há sub-fase)
  - IDs nunca mudam. Cancelada: marcar ~~T-A4~~ (riscado), não deletar.
  - Novas tasks no meio: continuar numeração (T-A12, T-A13).
═══════════════════════════════════════════════════════════════════════════════
-->

# TASKS_<MODULO> — Decomposição Atômica

**Status:** 📝 TASKS (`full`: aguardando GATE 2; `agentic`: gravado)
**Autor:** <nome>
**Data:** YYYY-MM-DD
**PLAN base:** `SDD/plans/PLAN_<MODULO>.md`

---

## Convenções

- **`T-XX`** é o ID estável da tarefa. NUNCA renumerar.
- **`[arquivo:função]`** indica destino. **→ NOVO** cria; **→ MOD** modifica.
- **`AC`** = criterio de aceite verificavel (teste, comando, observacao ou log).
- **`[bloq.]`** = tarefa que impede início da próxima fase (gate humano).
- Cada fase termina em: validacao completa → smoke aplicavel → commit (3 ultimas tarefas).

---

## Fase A — <nome> (~XXX LOC, 1 PR)

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| **T-A1** | Criar contrato/estrutura base | `<src>/<modulo>/<arquivo>` → NOVO | contrato importavel, instanciavel ou verificavel |
| **T-A2** | Implementar regra principal | `<src>/<modulo>/<arquivo>` → MOD | check especifico do happy path verde |
| **T-A3** | Cobrir erro ou limite | `<src>/<modulo>/<arquivo>` → MOD | check especifico do caso invalido verde |
| **T-A4** | Integrar modulo ao ponto de entrada | `<arquivo-existente>` → MOD | fluxo fica acessivel pelo caminho esperado |
| **T-A5** | Adicionar validacao do fluxo | `tests/<escopo>/<arquivo>` → NOVO | checks do fluxo passam |
| **T-A6** | Atualizar config/docs necessarias | `<manifest-ou-doc>` → MOD | configuracao ou documentacao confere com a entrega |
| **T-A7** [bloq.] | Validacao completa sem regressao | ambiente de trabalho | suite/checklist definido pelo projeto passa |
| **T-A8** [bloq.] | Smoke aplicavel | alvo realista / checklist | fluxos criticos OK (**GATE 3**) |
| **T-A9** | Commit na branch (Fase A) | git | commit convencional após **pacote** humano |

---

## Fase B — <nome> (~XXX LOC, 1 PR)

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| **T-B1** | <descrição> | <onde> | <AC> |
| **T-B2** | <descrição> | <onde> | <AC> |
| ... | ... | ... | ... |
| **T-B<N-2>** [bloq.] | Validacao completa sem regressao | ambiente de trabalho | suite/checklist do projeto passa |
| **T-B<N-1>** [bloq.] | Smoke aplicavel | alvo realista / manual | fluxos criticos OK (**GATE 3**) |
| **T-B<N>** | Commit + push (Fase B) | git | `feat(<modulo>): <fase B>` |

---

## Fase C — <nome>

(Mesma estrutura)

---

## Tarefas Canceladas

> Marcar com ~~strikethrough~~. Não deletar (preserva auditoria).

- ~~T-A12~~ — Cancelada porque <razão>. Decisão em ADR-MMM.

---

## Estimativa Total

| Fase | LOC est. | LOC real (preencher pós-implementação) | Δ |
|---|---|---|---|
| A | ~XXX | — | — |
| B | ~XXX | — | — |
| C | ~XXX | — | — |
| **TOTAL** | **~XXX** | — | — |

---

## Anexos

- PLAN: `SDD/plans/PLAN_<MODULO>.md`
- SPEC: `SDD/modules/SPEC_<MODULO>.md`
- ADRs: <lista>

---

*`full`: após GATE 2, IMPLEMENT (T-A1). `agentic`: IMPLEMENT após gravar TASKS. Pacote (review + G3) ao fim de cada fase. Atualizar handover.*
