# QUICKSTART — Bug Fix

> **Cenário:** detectou bug, precisa corrigir com rastreabilidade SDD.
>
> **Pré-requisito:** projeto JÁ TEM SDD ativo (passou por greenfield/brownfield).
>
> **Tempo:** 30 min - 2h dependendo da complexidade.

---

> **Playbook:** `.agent/skills/sdd-mode/playbooks/bug-fix.md` · **Perfil:** `lite` (G3, G4)

## TL;DR

```
1. /sdd-mode bug-fix (playbook bug-fix.md)
2. Reproduzir → causa raiz → classificar
3. sdd-tdd: RED + fix mínimo + GREEN
4. G3 no mesmo repro + G4
```

---

## Passo 1 — Reproduza o bug

ANTES de abrir IDE/agente:

- [ ] Você consegue reproduzir local ou em staging?
- [ ] Tem stack trace / log / screenshot?
- [ ] Tem severidade (crítico/alto/médio/baixo)?

Se NÃO consegue reproduzir, **pause**. Pesquise mais antes de envolver agente — vai economizar horas.

---

## Passo 2 — Use o prompt BUG_FIX

Copie `prompts/BUG_FIX.md` e preencha:

```
Bug detectado: <DESCRIÇÃO>
Onde foi visto: <produção | staging | local | log/relato>
Severidade: <crítico | alto | médio | baixo>
Reprodução: <passos>
```

O prompt instrui o agente em 4 etapas. **Não pule etapas.**

---

## Passo 3 — Etapa 1 (Investigação)

Agente vai:
- Localizar arquivo/função suspeita
- Identificar root cause (não sintoma)
- Verificar se foi mudança recente
- Avaliar blast radius

**Sua ação:** confirmar root cause faz sentido. Se agente está chutando, peça mais investigação.

---

## Passo 4 — Etapa 2 (Decisão de escopo)

Agente classifica em:
- **(a) Fix puro** (≤30 LOC, sem mudança de comportamento)
- **(b) Regra de negócio errada** (precisa CLARIFY humano)
- **(c) Arquitetural** (race condition, design flaw)

**Sua ação:**
- Se (a): GO direto pra Etapa 3
- Se (b): responda CLARIFY antes de proceder
- Se (c): considere abrir `prompts/REFACTOR.md` em vez de fix gambiarra

---

## Passo 5 — Etapa 3 (Test + Fix)

⚠️ **REGRA NÃO-NEGOCIÁVEL:** regression test PRIMEIRO.

Agente vai:
1. Escrever teste que reproduz o bug (deve falhar)
2. Implementar fix mínimo
3. Confirmar teste passa
4. Rodar suite full (0 regressão)

**Sua ação:**
- Veja o regression test — ele realmente captura o bug?
- Veja o fix — é mínimo (só o necessário)?
- Se viu refactor "while I'm here", **rejeite** — separar em PR diferente

---

## Passo 6 — Etapa 4 (GATEs + Commit)

🛑 **GATE 3 (Smoke):** rode os smoke tests (`tests/smoke/`) + valide UX/comportamento manualmente em staging. Bug NÃO ocorre mais? Nada relacionado quebrou?

🛑 **GATE 4 (Commit):** revise o diff completo. Comando final:

```bash
git commit -m "$(cat <<'EOF'
fix(<modulo>): <título imperativo>

<Por quê o bug acontecia (root cause)>.
Adiciona regression test em tests/unit/test_<modulo>.py.

Fixes #<issue> (se houver).
EOF
)"
```

---

## Passo 7 — Handover (se sessão termina aqui)

Use `prompts/HANDOVER.md`. Categoria: `handover_BUGFIX_<DATA>.md` (não está numa fase de SPEC).

Atualize `specs/SPEC_INDEX.md` se mudou status do módulo (ex: 🚧 → ✔️).

---

## Anti-padrões clássicos

| Anti-padrão | Sintoma | Correção |
|---|---|---|
| Fix do sintoma | Bug volta diferente | Root cause analysis |
| Refactor opportunista | PR enorme | Separar em 2 commits |
| Sem regression test | Bug volta | TDD: teste antes |
| Pular smoke | UX quebrada em prod | GATE 3 obrigatório |
| Commit "fix bug" | Histórico inútil | Conventional + por quê |

---

## Critérios de pronto

- [ ] Root cause documentado em commit message
- [ ] Regression test que falha sem o fix, passa com
- [ ] Pytest -q 0 falhas
- [ ] Smoke staging OK
- [ ] PR ≤100 LOC (se passar, separar)
- [ ] SPEC atualizada se mudou regra de negócio
- [ ] Handover (se sessão termina)

---

*Veja: `prompts/BUG_FIX.md` para o prompt detalhado, `QUICKSTART/refactor.md` se virou refactor.*
