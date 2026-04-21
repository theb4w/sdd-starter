<!--
═══════════════════════════════════════════════════════════════════════════════
  Template de HANDOVER (passagem de bastão entre sessões)
═══════════════════════════════════════════════════════════════════════════════

  Como usar:
  1. Copie para docs/handover_<MODULO>_<DATA>.md
     - Multi-fase: docs/handover_<MODULO>_FASE_<X>_<DATA>.md
     - Operacional: docs/handover_<OPERACAO>_<DATA>.md
     - Bootstrap inicial: docs/handover_DISCOVERY_<DATA>.md
  2. <DATA> em formato YYYY-MM-DD
  3. Preencha TODAS as seções (mesmo que "N/A")
  4. NÃO commite ainda — gerar e mostrar para revisão humana primeiro

  Quando criar handover (SDD_WORKFLOW §12.3):
  - Sempre ao fechar uma fase (mesmo dentro do mesmo dia)
  - Sempre ao encerrar sessão > 30 min
  - Sempre após deploy + smoke
═══════════════════════════════════════════════════════════════════════════════
-->

# Handover — <MODULO> Fase <X> (se aplicável)

**Data:** YYYY-MM-DD
**Módulo:** `<nome>` (`SPEC_<MODULO>.md`)
**Sessão anterior:** `docs/handover_<...>.md` (se houver)
**Status:** ✔️ FASE CONCLUÍDA | 🚧 EM ANDAMENTO | ❌ BLOQUEADA

---

## 1. O Que Esta Sessão Entregou

> 1-2 parágrafos descrevendo escopo concreto. Sem adjetivos vazios.

<!-- Exemplo:
Implementadas T-A1..T-A11 da Fase A do PLAN_AUTH. Backend de OAuth via Google
está funcional em staging: endpoints `/auth/login`, `/auth/callback` e
`/auth/logout` retornam 200/302 conforme esperado. Sessão persistida em
PostgreSQL com TTL de 30 dias. 8 testes unit + 2 smoke verdes. Cobertura: 87%.
-->

---

## 2. Tarefas Concluídas

| ID | Tarefa | Resultado |
|---|---|---|
| T-X1 | <descrição> | <resultado verificável> |
| T-X2 | <descrição> | <resultado> |
| ... | ... | ... |

---

## 3. Métricas Entregues vs. Estimadas

| Métrica | Estimado | Real | Δ | Comentário |
|---|---|---|---|---|
| LOC | ~XXX | ~YYY | +<X>% | <razão se >20% off> |
| Testes novos | <N> | <M> | <Δ> | — |
| Cobertura | ≥80% | <X>% | — | OK |
| Regressões | 0 | 0 | — | OK |
| Tempo de implementação | <est> | <real> | <Δ> | — |

---

## 4. Estado da Infra

### Ambiente staging / equivalente
```
Serviço     : <nome>
Revision    : <id>
Imagem      : <registry>/<image>:<tag>
URL         : <url>
Custo (24h) : $<X>
```

### Repositório
```
Branch      : main em <COMMIT_HASH>
Commits     : <hash1> (T-X1..T-X4), <hash2> (T-X5..T-X11)
PRs abertos : <#NN, #MM> | nenhum
PRs merged  : <#KK>
```

### Recursos provisionados nesta sessão
- <recurso novo>: <ID/URL/config>
- <recurso modificado>: <antes → depois>

---

## 5. Decisões Reafirmadas

> ADRs validadas na prática + mudanças importantes de comportamento detectadas.

- **ADR-NNN** validada na prática: <evidência concreta>
- **ADR-MMM** parcialmente questionada: <descrever cenário> — ainda válida porque <razão>
- **Mudança de comportamento detectada:** <descrever> — não regressão (esperado)

---

## 6. Pendências (não bloqueiam próxima fase)

### Cleanup
1. <item>: <ação esperada>
2. <item>

### Operacional
1. <item>: <ação esperada — quem é responsável>
2. <item>

### Documentação
1. <item>

---

## 7. Próximos Passos

| Item | Detalhe |
|---|---|
| Próxima fase | <nome> |
| Primeira tarefa | T-Y1 — <descrição> |
| Pré-condições | <lista — ex.: "ADR-NNN aceita", "DB migration N+1 aplicada"> |
| Aguarda | <quem ou quê> |
| Estimativa | <horas / dias> |

---

## 8. Como Retomar

> Cole no próximo chat (Cursor / Antigravity / Claude / etc.) o **prompt de retomada** abaixo.

```text
Retomar <PROJETO> — iniciar SPEC_<MODULO> Fase <X+1> (<descrição_curta>).

LEIA NESTA ORDEM antes de qualquer ação:
1. AGENTS.md (constituição)
2. GEMINI.md (se aplicável)
3. docs/handover_<MODULO>_FASE_<X>_<DATA>.md (este arquivo — autoridade do estado prévio)
4. specs/SPEC_INDEX.md
5. specs/modules/SPEC_<MODULO>.md §<seção_relevante>
6. specs/plans/PLAN_<MODULO>.md §"Fase <X+1>"
7. specs/plans/TASKS_<MODULO>.md §"Fase <X+1>" (T-<X+1>1..T-<X+1>N)

ESTADO ATUAL (verificar antes de codar):
- Workspace : <caminho local>
- Branch    : main em <COMMIT_HASH>
- Repo      : github.com/<user>/<repo>
- Testes    : <N>/<N> passing — manter
- Cloud Run / equivalente : revision <REV> ativa
- Toolchain : git, gh, <runtime>, <pacote-mgr>, .venv local

GATES JÁ APROVADOS (não revisar):
- GATE 1 (PLAN), GATE 2 (TASKS) aprovados em <DATA>
- ADRs aceitos: <lista>
- Fases concluídas: <lista>

PRÓXIMA TAREFA: T-<X+1>1 — <descrição> conforme SPEC §<sec>.

REGRAS NÃO-NEGOCIÁVEIS:
- <regra absoluta 1 do AGENTS.md>
- <regra absoluta 2>
- PR ≤250 LOC
- Conventional Commits
- Backward-compat por tarefa
- Sem commit/push sem aprovação humana
- Tarefas [bloq.] em TASKS são gates humanos

Proceda: leitura → confirme entendimento → mostre plano com checkboxes →
AGUARDE meu GO antes de iniciar a primeira tarefa.
```

---

## 9. Observações Operacionais (opcional)

> Coisas que aprendemos nesta sessão e seriam úteis na próxima.

- <observação 1>
- <observação 2>

---

*Próximo handover esperado: `docs/handover_<MODULO>_FASE_<X+1>_<DATA>.md`*
