<!--
═══════════════════════════════════════════════════════════════════════════════
  Template de TASKS (decomposição atômica) de módulo
═══════════════════════════════════════════════════════════════════════════════

  Como usar:
  1. Copie este arquivo para specs/plans/TASKS_<MODULO>.md
  2. Pré-requisito: PLAN_<MODULO>.md aprovado (GATE 1)
  3. Cada task = 1 commit lógico, ~10-30 LOC, com AC verificável
  4. Tarefas [bloq.] são gates (não pular sem aprovação humana)
  5. Aguarde GATE 2 antes de qualquer implementação

  Convenções de ID:
  - T-<FASE><N>  (T-A1, T-B2, T-C1.3 quando há sub-fase)
  - IDs nunca mudam. Cancelada: marcar ~~T-A4~~ (riscado), não deletar.
  - Novas tasks no meio: continuar numeração (T-A12, T-A13).
═══════════════════════════════════════════════════════════════════════════════
-->

# TASKS_<MODULO> — Decomposição Atômica

**Status:** 📝 TASKS (aguardando GATE 2)
**Autor:** <nome>
**Data:** YYYY-MM-DD
**PLAN base:** `specs/plans/PLAN_<MODULO>.md`

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
| **T-A9** | Commit + push (Fase A) | git | commit convencional aprovado (**GATE 4**) |

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

- PLAN: `specs/plans/PLAN_<MODULO>.md`
- SPEC: `specs/modules/SPEC_<MODULO>.md`
- ADRs: <lista>

---

*Após GATE 2 aprovado, prosseguir para IMPLEMENT (T-A1). Atualizar handover ao fim de cada fase.*
