# QUICKSTART — Feature Média (100-400 LOC)

> **Cenário:** feature significativa que toca 2-5 arquivos, talvez tenha trade-off técnico.
> Ex.: novo recurso de billing, integração com serviço externo, novo módulo pequeno.
>
> **Tempo:** 2-6h (pode ser dividida em sessões).
>
> **Pré-requisito:** SDD ativo no projeto.

---

## Quando é média (e não pequena/grande)?

| Critério | Pequena | **Média** | Grande |
|---|---|---|---|
| LOC estimado | ≤100 | **100-400** | >400 |
| Arquivos novos | 0-1 | **1-3** | >3 |
| Decisão arquitetural | Não | **Talvez 1 trade-off** | Múltiplas |
| Serviço externo | Não | **0-1 novo** | ≥2 |
| Schema DB | Não | **Mudança simples** | Migração complexa |
| Multi-fase | Não | **Não (single PLAN)** | Sim |

---

## TL;DR

```
1. Cole prompts/NEW_FEATURE.md (modo "média")
2. Etapa 1-2: análise + criar SPEC nova
3. Etapa 3-4: CLARIFY + ADR (se trade-off)
4. Etapa 5: PLAN single-phase → GATE 1
5. Etapa 6: TASKS → GATE 2
6. Etapa 7: IMPLEMENT (1 tarefa por vez)
7. Etapa 8: Smoke + Commit + Handover
```

---

## Passo 1 — Use NEW_FEATURE com modo média

```
Quero adicionar a feature: <DESCRIÇÃO 1-3 frases>
Tamanho estimado: média
Módulo afetado: <MODULO ou "novo módulo">
Prazo desejado: <hoje | semana | sem prazo>
```

---

## Passo 2 — Etapa 1 (Análise + escopo)

Agente apresenta:
- LOC estimado real (pode discordar do seu chute)
- Trade-offs detectados (que viram ADR)
- Perguntas CLARIFY abertas

**Sua ação:** revise o escopo. Se ele propôs grande/multi-fase, **considere** (não é arrogância — overfit acontece muito).

---

## Passo 3 — Etapa 2 (SPEC nova)

Para feature média, criar SPEC nova faz sentido (mesmo se "ramo" de módulo existente):

- `specs/modules/SPEC_<NOME_FEATURE>.md` baseado em `_SPEC_TEMPLATE.md`
- Status inicial: 📝 RASCUNHO
- §3 (Design) com diagrama mermaid se ajuda
- §9 (CLARIFY) com perguntas abertas

**Sua ação:** revise SPEC inteira. Status fica RASCUNHO até CLARIFY resolvido.

---

## Passo 4 — Etapa 3 (CLARIFY)

Agente lista perguntas:

```
Q1: Quando webhook do Stripe falha em retry, qual TTL?
Q2: Devemos persistir tentativas falhas em logs ou em tabela?
Q3: Há limite de quantos retries fazer?
```

**Você responde.** Agente atualiza §10 (Histórico) da SPEC com decisões e suas justificativas.

Promove status para 📋 PLAN.

---

## Passo 5 — Etapa 4 (ADRs se trade-off)

Para CADA trade-off arquitetural identificado em CLARIFY:

- Agente cria `specs/decisions/ADR-NNN-<slug>.md` baseado em template
- Status: 📝 PROPOSTA
- 2+ alternativas com prós/contras
- Recomendação técnica

**Você decide.** Status → ✔️ ACEITO somente após GO.

⚠️ ADRs viram norma — releia em 2 meses, não vai querer reverter à toa.

---

## Passo 6 — Etapa 5 (PLAN single-phase)

Para feature média, PLAN é single-phase:

- 1 fase só (sem dividir A/B/C)
- 5-15 tarefas estimadas
- Mapa de dependências (mermaid simples)
- Riscos com mitigação

🛑 **GATE 1** — você aprova. **Não pule.** É o filtro mais barato.

---

## Passo 7 — Etapa 6 (TASKS)

`specs/plans/TASKS_<MODULO>.md` com:

- T-1.1, T-1.2, ... atômicas
- Última = commit; penúltima = smoke; antepenúltima = pytest+lint full
- AC verificável em cada
- Marca [bloq.] em gates humanos

🛑 **GATE 2** — você aprova.

---

## Passo 8 — Etapa 7 (IMPLEMENT)

Use `.agent/workflows/sdd_implement.md`. Loop:

```
Para cada tarefa T-X:
  1. Agente anuncia: "vou começar T-X"
  2. Implementa código
  3. Verifica AC (roda comando)
  4. Mostra diff
  5. Você dá GO para próxima
```

⚠️ Tarefa [bloq.] = pause. Não automatize.

---

## Passo 9 — Etapa 8 (Smoke + Commit)

🛑 **GATE 3 (Smoke):**
- Rode `pytest tests/smoke/` ou equivalente
- Smoke manual do fluxo end-to-end
- Validar comportamento esperado em staging real (não só local)

🛑 **GATE 4 (Commit):**
- Revisão humana do diff completo (use `git diff main...HEAD`)
- Commit Conventional:

```bash
git commit -m "$(cat <<'EOF'
feat(<modulo>): <título imperativo>

<1-2 parágrafos sobre o por quê + comportamento + ADRs aplicadas>.
- SPEC_<modulo>.md ✔️ APROVADA
- ADR-NNN ✔️ ACEITO
- Tests: <X> unit + <Y> integration + <Z> smoke
- Cobertura módulo: <W>%
EOF
)"
```

---

## Passo 10 — Handover

`prompts/HANDOVER.md` com nome `handover_<MODULO>_<DATA>.md` (sem fase, é single-phase).

Atualize `specs/SPEC_INDEX.md`:
- Status SPEC: ✔️ IMPLEMENTADA
- ADRs: ✔️ ACEITO
- Histórico: linha nova com data + delivery

---

## Anti-padrões em feature média

| Anti-padrão | Por quê é ruim |
|---|---|
| Pular CLARIFY ("vou descobrir codando") | Decisões viram tribal, ADR perdido |
| Pular ADR de trade-off | Próximo dev questiona escolha sem contexto |
| Pular GATE 1 (PLAN) | Implementação diverge do escopo |
| PR único de 400 LOC | Revisor não consegue revisar bem |
| Smoke pulado | Bug arquitetural escapa para produção |

---

## Critérios de pronto

- [ ] SPEC ✔️ APROVADA (CLARIFY resolvido)
- [ ] ADRs ✔️ ACEITO (todas aplicáveis)
- [ ] PLAN ✔️ APROVADO (GATE 1)
- [ ] TASKS ✔️ APROVADAS (GATE 2)
- [ ] Todas as tarefas implementadas
- [ ] Pytest+lint+coverage 0 falhas
- [ ] Smoke staging OK (GATE 3)
- [ ] Commit Conventional (GATE 4)
- [ ] PR ≤250 LOC (se passar, dividir)
- [ ] Handover criado
- [ ] SPEC_INDEX.md atualizado

---

*Veja: `prompts/NEW_FEATURE.md`, `QUICKSTART/large-feature.md` se cresceu para >400 LOC.*
