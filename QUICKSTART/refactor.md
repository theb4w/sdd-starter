# QUICKSTART — Refator

> **Cenário:** melhorar código sem (necessariamente) mudar comportamento.
> Pode ser refator interno ou arquitetural.
>
> **Tempo:** 1h - vários dias dependendo do tipo.
>
> **Pré-requisito:** SDD ativo, cobertura de testes ≥80% no módulo (CRÍTICO).

---

## Decida em 30 segundos: interno ou arquitetural?

| Critério | Interno | Arquitetural |
|---|---|---|
| Muda contrato público (API, schema)? | NÃO | SIM |
| Substitui dependência? | NÃO | SIM |
| Muda padrão arquitetural? | NÃO | SIM |
| LOC estimado | ≤200 | >200 |
| Precisa migração de dados? | NÃO | SIM |
| Precisa ADR? | Raro | OBRIGATÓRIO |

**Se ≥1 critério é "SIM" → arquitetural.**

---

## TL;DR (interno)

```
1. Verifique cobertura ≥80% (se não, adicione testes ANTES)
2. Cole prompts/REFACTOR.md tipo "interno"
3. Etapas 1-2: análise + cobertura
4. Etapa 5: refactor (1 tarefa por vez, testes verdes)
5. Smoke + Commit
```

## TL;DR (arquitetural)

```
1. Verifique cobertura ≥80%
2. Cole prompts/REFACTOR.md tipo "arquitetural"
3. ADR de migração obrigatória
4. SPEC v2 (lado-a-lado com SPEC v1)
5. PLAN multi-fase (expand-contract / strangler fig)
6. Implementação fase a fase
7. Cutover final com rollback validado
```

---

## REGRA DE OURO

Refator com cobertura <80% NÃO É REFATOR. É **aposta**.

Se módulo tem 30% de cobertura:
1. **PARE.**
2. Adicione testes para aumentar cobertura para ≥80%.
3. **DEPOIS** refatore.

Isso parece overhead, mas:
- Tempo gasto adicionando testes = 30% do tempo do refator
- Bugs evitados = >100% economia de tempo no longo prazo

---

## Refator interno — passo a passo

### Passo 1 — Cobertura

```bash
pytest --cov=app.<modulo> --cov-report=term-missing
```

Se <80%:
- Cole `prompts/NEW_FEATURE.md` modo "pequena" e peça testes
- Continue refator só depois

Se ≥80%:
- Continue para Passo 2

### Passo 2 — Use prompts/REFACTOR.md

```
Refator proposto: <descrição clara>
Tipo: interno
Módulo(s) afetado(s): <lista>
Motivação: <debt técnico | performance | manutenibilidade | preparar para feature X>
Tamanho estimado: ≤200 LOC
```

### Passo 3 — Análise

Agente apresenta:
- Cobertura atual
- Justificativa do refator (métrica que melhora)
- Confirma: tipo interno, sem ADR

**Você aprova.**

### Passo 4 — TASKS curtas

Sem PLAN intermediário (refator interno é menor):

```
T-1: extrair função X de Y
T-2: renomear Z → W
T-3: pytest full + lint
T-4: smoke
T-5: commit
```

🛑 **GATE 2** — você aprova TASKS.

### Passo 5 — Implementação

Para CADA tarefa:
- Implementar
- **Pytest verde antes E depois.**
- Se quebrou teste → não é refator, é mudança de comportamento → reverter

### Passo 6 — Smoke + Commit

🛑 **GATE 3:** smoke staging — comportamento idêntico ao anterior?

🛑 **GATE 4:** commit:

```bash
git commit -m "$(cat <<'EOF'
refactor(<modulo>): <título — o que mudou estruturalmente>

<Por quê — qual debt, qual feature futura habilitada, qual métrica melhorou>.
Cobertura mantida em <X>%. Comportamento observável idêntico (smoke OK).
EOF
)"
```

---

## Refator arquitetural — passo a passo

### Passo 1 — Análise extensa

```
Refator proposto: substituir <X> por <Y>
Tipo: arquitetural
Motivação: <debt crítico | performance crítica | feature impossível com design atual>
Tamanho estimado: >200 LOC, multi-fase
```

### Passo 2 — ADR de migração (OBRIGATÓRIA)

`specs/decisions/ADR-NNN-migrate-<X>-to-<Y>.md`:

- Contexto: por quê o design atual não serve mais (concreto: bug Z aconteceu N vezes; performance Y travou feature W)
- Alternativas:
  1. Status quo (manter X) — prós/contras
  2. Migrar para Y — prós/contras
  3. Migrar para Z — prós/contras
- Decisão: Y, com pattern strangler fig
- Plano de migração: fases A → B → C → D
- Rollback: passos para voltar a X em cada fase
- Métrica de sucesso: latência<100ms, custo<$X/mês, complexity score<Y

🛑 **Você aprova ADR.** Status: 📝 PROPOSTA → ✔️ ACEITO.

### Passo 3 — SPEC v2 lado-a-lado

`specs/modules/SPEC_<MODULO>_v2.md`:
- Documenta o NOVO design (que vai substituir o antigo)
- §3 Design referencia ADR de migração
- Status: 📝 RASCUNHO até ser implementada

SPEC v1 fica como está (status: 🚧 SUNSET).

### Passo 4 — PLAN multi-fase com strangler fig

```markdown
## Fases (Strangler Fig)

| Fase | Objetivo | Risk |
|---|---|---|
| A | Implementar Y lado-a-lado de X (sem cutover) | Baixo |
| B | Migrar dados / clientes para Y (canary 10% → 50% → 100%) | Médio |
| C | App lê do Y, valida contra X (assert) | Médio |
| D | App só usa Y; X marcado deprecated | Baixo |
| E | Cutover: remover X | Crítico (gate humano explícito) |
```

🛑 **GATE 1** — PLAN aprovado.

### Passo 5 — Implementação por fase

Cada fase:
1. TASKS específicas → GATE 2
2. IMPLEMENT (1 tarefa por vez)
3. Smoke staging
4. Commit isolado
5. Handover entre fases

⚠️ Fase E (cutover) tem gate humano EXPLÍCITO:

```markdown
T-E5: [bloq.] CONFIRMAÇÃO HUMANA: 
      - Y rodando 100% por >7 dias
      - 0 incidentes relacionados
      - Métricas de sucesso da ADR atingidas
      - Rollback plan testado em staging
      Antes de remover X, confirme cada item acima.
```

### Passo 6 — Cutover + Cleanup

Após Fase E:
- Remover SPEC v1 ou marcar 🗑️ ARCHIVED
- SPEC v2 promovida a SPEC oficial (rename: SPEC_<MODULO>.md)
- ADR atualizada com retrospectiva: "Migration completed em <DATA>; <métrica>: <valor real>"

---

## Padrões consagrados

### Strangler Fig (Martin Fowler)
> Encapsular sistema antigo gradualmente, substituindo até desaparecer.
> https://martinfowler.com/bliki/StranglerFigApplication.html

### Expand-Contract (DB schema)
1. Expand: adicionar colunas/tabelas novas (sem remover antigas)
2. Migrate: dual-write, backfill
3. Contract: remover colunas/tabelas antigas

### Branch by Abstraction
> Refator com feature flag — toggle entre old/new path em runtime.

### Parallel Run
> Rodar X e Y em paralelo, comparar outputs, gradual cutover.

---

## Anti-padrões em refator

| Anti-padrão | Resultado |
|---|---|
| Refator com cobertura <80% | Aposta; bugs vão aparecer | 
| Big bang refactor (sem fases) | Sistema down 1+ dia |
| Misturar refactor + feat no mesmo PR | PR enorme; revisor odeia |
| Refator sem ADR (em arquitetural) | Decisão tribal; reverter caro |
| Sem smoke ("é só refator") | UX quebrada em prod |
| Cutover sem rollback testado | Refator irreversível em emergência |
| "Vou refatorar tudo de uma vez" | 3 meses sem release; perde momentum |

---

## Critérios de pronto (interno)

- [ ] Cobertura ≥80% (mantida)
- [ ] Pytest+lint 0 falhas
- [ ] Smoke staging idêntico ao anterior
- [ ] PR ≤200 LOC
- [ ] Conventional Commit `refactor(<modulo>):`
- [ ] Commit message explica POR QUÊ refatorar

## Critérios de pronto (arquitetural)

- [ ] ADR ✔️ ACEITO
- [ ] SPEC v2 ✔️ APROVADA
- [ ] Todas as fases concluídas
- [ ] Métricas de sucesso da ADR atingidas (não promessas)
- [ ] Rollback plan documentado E testado
- [ ] Cutover com gate humano explícito (Fase E)
- [ ] SPEC v1 archivada / removida
- [ ] Documentação de migração (se outros consomem o módulo)

---

*Veja: `prompts/REFACTOR.md` para o prompt completo, `QUICKSTART/large-feature.md` se virou feature ao invés de refactor.*
