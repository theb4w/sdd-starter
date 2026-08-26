# ADR-002 — Perfis de gate no lugar de quatro gates universais

**Status:** ✔️ ACEITO
**Data:** 2026-08-25
**Autores:** Allan + Grok
**Spec relacionada:** `specs/modules/SPEC_SDD_MODE.md`
**Substitui:** a leitura de `AGENTS.md` regra 1 como “sempre G1–G4”, sem mudar os *nomes* dos quatro gates

---

## Contexto

`docs/SDD_WORKFLOW.md` §2 já reduz artefatos por modo (bug = G3+G4; feature pequena = G2+G3+G4). Na prática o agente trata os quatro gates como sempre obrigatórios, ou os ignora todos. O pedido desta refatoração é **poder ter menos gates** (design, user-story, bug) sem esvaziar o ciclo médio/grande.

Os quatro gates continuam existindo. O que muda é *quais disparam*, amarrado ao playbook.

---

## Alternativas Consideradas

### Opção A — Quatro gates sempre, em qualquer demanda

**Descrição:** PLAN, TASKS, SMOKE, COMMIT obrigatórios inclusive em bug de 5 linhas.

- **Prós:** regra simples; máxima rastreabilidade.
- **Contras:** o próprio workflow chama isso de armadilha; ninguém segue; gates viram teatro.
- **Custo:** tempo humano em demanda pequena.
- **Reversibilidade:** fácil (já é o texto de `AGENTS.md` regra 1, lido de forma rígida).
- **Fonte:** `docs/SDD_WORKFLOW.md` §1.3

### Opção B — Perfis declarados pelo playbook (`observe`, `design`, `lite`, `standard`, `full`)

**Descrição:** Cada playbook nomeia o perfil. Downgrade só com reclassificação do cenário. Upgrade sempre permitido. Código de produção ainda exige G3+G4 (`lite` ou acima).

- **Prós:** torna explícito o que §2 já diz; o agente copia o perfil junto com os passos; design/story cabem sem fingir PLAN.
- **Contras:** cinco nomes para aprender; risco de o agente “reclassificar” para pular PLAN.
- **Custo:** documentação + uma linha por playbook.
- **Reversibilidade:** média (reverter perfis exige reescrever playbooks).
- **Fonte:** `docs/SDD_WORKFLOW.md` §2 (tabela de modos)

### Opção C — Autonomia estilo pstack (humano só no irreversível)

**Descrição:** Seguir `never-block-on-the-human`; gates viram review depois do fato.

- **Prós:** throughput; combina com overnight agents.
- **Contras:** contradiz spec-first e GATE 1/2; retrabalho em greenfield e compliance.
- **Custo:** alto em retrabalho de produto.
- **Reversibilidade:** difícil depois que o hábito entra.
- **Fonte:** https://github.com/cursor/plugins/blob/main/pstack/skills/principle-never-block-on-the-human/SKILL.md

---

## Decisão

Escolhemos a **Opção B**. Os quatro gates permanecem o vocabulário. O playbook escolhe o subconjunto. A opção A já foi rejeitada pelo próprio §2. A opção C é incompatível com SDD.

Perfis:

| Perfil | Gates | Código de produção? |
|---|---|---|
| `observe` | nenhum | não |
| `design` | aprovação do artefato de design/protótipo | não |
| `lite` | G3 + G4 | sim |
| `standard` | G2 + G3 + G4 | sim |
| `full` | G1 + G2 + G3 + G4 | sim |

---

## Consequências

### Positivas

- Bug, story mínima e design não carregam PLAN.
- Feature média continua com G1+G2.
- A skill pode recusar `lite` numa feature média sem improvisar.

### Negativas (aceitas)

- `AGENTS.md` deixa de dizer “4 gates sempre”; passa a dizer “gates do perfil do playbook”.
- Dois vocabulários (G1–G4 e perfil) até o leitor decorar a tabela.

### Riscos mitigados

- **Risco:** agente declara “é pequena” para pular PLAN.
  **Mitigação:** critérios de tamanho já em `QUICKSTART/small-feature.md` entram no playbook `feature.md`; discordância do agente prevalece para *upgrade*, não para downgrade.

### Risco residual

- Humano pode mandar “faz logo, sem PLAN” numa média. A skill deve recusar ou exigir reclassificação explícita — aceito como tensão permanente.

---

## Como Reverter

1. Restaurar o texto “4 gates obrigatórios sempre” em `AGENTS.md` e `SDD_WORKFLOW.md` §1.
2. Trocar a linha de perfil dos playbooks para `full`.
3. Marcar este ADR como ⏸️ SUPERSEDED.
