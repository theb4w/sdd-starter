# QUICKSTART — Feature Pequena (≤100 LOC)

> **Cenário:** adicionar funcionalidade pequena num módulo existente.
> Ex.: novo endpoint trivial, novo campo num form, novo flag.
>
> **Tempo:** 30-60 min.
>
> **Pré-requisito:** SDD ativo, módulo afetado já tem SPEC.

---

## Quando isto é uma feature pequena (e não média)?

| Critério | Pequena | NÃO é pequena |
|---|---|---|
| LOC estimado | ≤100 | >100 |
| Arquivos novos | 0-1 | ≥2 |
| Decisão arquitetural | Nenhuma | Há trade-off |
| Serviço externo novo | Não | Sim |
| Mudança de schema | Não | Sim |

**Se respondeu "NÃO é pequena" em qualquer linha, use `medium-feature.md`.**

---

## TL;DR

```
1. Cole prompts/NEW_FEATURE.md (modo "pequena")
2. Etapa 1: análise + escopo confirmado
3. Etapa 2: estende SPEC existente (sem PLAN/ADR)
4. Vai direto pra implementação (1-3 tarefas)
5. Smoke + Commit + Handover (curto)
```

---

## Passo 1 — Use NEW_FEATURE com modo pequena

Cole `prompts/NEW_FEATURE.md`, marcando tamanho `pequena`:

```
Quero adicionar a feature: <descrição em 1-2 frases>
Tamanho estimado: pequena
Módulo afetado: <MODULO>
Prazo desejado: <hoje | semana | sem prazo>
```

---

## Passo 2 — Etapa 1 (Análise rápida)

Agente confirma que é pequena (LOC, arquivos, sem trade-off).

**Se agente discordar** ("isso é média porque..."), **escute**. Re-classifique.

---

## Passo 3 — Etapa 2 (Estender SPEC)

Em vez de criar SPEC nova, **estender** a do módulo:

- Adiciona linha em §3 (Design)
- Adiciona caso em §4 (Regras de negócio) se aplicável
- Adiciona flag em §5 (Env vars) se aplicável
- Atualiza §7 (Testes) com 1-2 tests novos
- Atualiza §8 (DoD)

Mostra diff. **Você revisa.** AGUARDE GO.

---

## Passo 4 — TASKS curta (sem PLAN)

Agente gera lista de 1-3 tarefas atômicas direto, **sem PLAN.md** intermediário:

```
T-1: implementar endpoint /v1/<feature>
T-2: pytest+lint full
T-3: smoke + commit
```

🛑 **GATE 2** (TASKS) — você aprova.

---

## Passo 5 — IMPLEMENT (rápido)

Agente implementa 1 tarefa por vez. Você revisa diff antes da próxima.

---

## Passo 6 — Smoke + Commit

🛑 **GATE 3:** smoke staging do endpoint/comportamento novo.

🛑 **GATE 4:** commit:

```bash
git commit -m "$(cat <<'EOF'
feat(<modulo>): <título imperativo curto>

<1 parágrafo sobre o por quê + comportamento esperado>.
SPEC_<modulo>.md §<seção> atualizada.
EOF
)"
```

---

## Passo 7 — Handover só se sessão termina

Para feature pequena, handover pode ser inline numa atualização do SPEC_INDEX.md:

```markdown
## Histórico
- <DATA>: feature <X> adicionada ao módulo <Y>. Cobertura: <Z>%.
```

Sem precisar `handover_*.md` formal (a menos que pause antes do commit).

---

## Anti-padrões em feature pequena

| Anti-padrão | Por quê é ruim |
|---|---|
| Pular SPEC update ("é só 50 linhas") | Próximo dev não sabe que existe |
| Esquecer testes | Feature sem teste = feature defeituosa |
| Fazer 3 features juntas no mesmo commit | Histórico ruim, rollback impossível |
| "While I'm here, refactor X" | Misturar refator + feat = PR enorme |

---

## Critérios de pronto

- [ ] SPEC do módulo atualizada (diff revisado)
- [ ] 1-2 testes novos cobrindo a feature
- [ ] Pytest -q 0 falhas
- [ ] Smoke staging OK
- [ ] PR ≤100 LOC
- [ ] Conventional Commit `feat(<modulo>):`
- [ ] SPEC_INDEX.md histórico atualizado

---

*Veja: `prompts/NEW_FEATURE.md` para o prompt completo, `QUICKSTART/medium-feature.md` se cresceu.*
