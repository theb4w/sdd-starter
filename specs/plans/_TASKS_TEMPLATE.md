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
- **`AC`** = critério de aceite verificável (teste, comando, http response, log).
- **`[bloq.]`** = tarefa que impede início da próxima fase (gate humano).
- Cada fase termina em: testes full → smoke staging → commit (3 últimas tarefas).

---

## Fase A — <nome> (~XXX LOC, 1 PR)

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| **T-A1** | Criar dataclass `<Nome>` | `app/<modulo>/models.py` → NOVO | `from app.<modulo>.models import <Nome>` funciona |
| **T-A2** | Implementar `<funcao>` happy path | `app/<modulo>/service.py:funcao` → NOVO | `pytest tests/unit/test_<modulo>.py::test_funcao_happy` verde |
| **T-A3** | Adicionar validação de input | `app/<modulo>/service.py:funcao` → MOD | `pytest tests/unit/test_<modulo>.py::test_funcao_invalid_input` levanta `ValueError` |
| **T-A4** | Endpoint HTTP `POST /<modulo>` | `app/api/<modulo>.py` → NOVO | `curl -X POST localhost:8000/<modulo>` retorna 200 |
| **T-A5** | Registrar router em `main.py` | `app/main.py` → MOD | `curl localhost:8000/openapi.json` lista endpoint |
| **T-A6** | Testes unit (3 cenários) | `tests/unit/test_<modulo>.py` → NOVO | `pytest tests/unit/test_<modulo>.py -q` 3/3 verde |
| **T-A7** | Logs estruturados | `app/<modulo>/service.py` → MOD | grep `"<modulo>"` nos logs mostra entrada e saída de cada chamada |
| **T-A8** | Atualizar `requirements.txt` | `requirements.txt` → MOD | `pip install -r requirements.txt` sem erro |
| **T-A9** [bloq.] | Testes full sem regressão | terminal | `pytest -q` 0 falhas em todo o repo |
| **T-A10** [bloq.] | Smoke staging | manual / `scripts/smoke.sh` | 3 fluxos críticos OK + logs limpos (**GATE 3**) |
| **T-A11** | Commit + push (Fase A) | git | `feat(<modulo>): implementa <funcionalidade> (Fase A)` |

---

## Fase B — <nome> (~XXX LOC, 1 PR)

| ID | Tarefa | Onde | AC |
|---|---|---|---|
| **T-B1** | <descrição> | <onde> | <AC> |
| **T-B2** | <descrição> | <onde> | <AC> |
| ... | ... | ... | ... |
| **T-B<N-2>** [bloq.] | Testes full sem regressão | terminal | `pytest -q` 0 falhas |
| **T-B<N-1>** [bloq.] | Smoke staging | manual | 3 fluxos OK (**GATE 3**) |
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
