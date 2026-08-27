# ADR-003 — Perfil `agentic`: humano no intent, agente no HOW e na review

**Status:** ✔️ ACEITO
**Data:** 2026-08-27
**Autores:** Allan + Grok
**Spec relacionada:** `SDD/modules/SPEC_SDD_MODE.md`
**Relaciona:** ADR-002 (perfis); não substitui os nomes G1–G4

---

## Contexto

ADR-002 ligou gates ao playbook. No perfil `full` o humano ainda autoriza PLAN e TASKS **antes** do código. Isso é mais interferência do que o spec-kit (clarify/analyze opcionais) e do que o Antigravity (um GO no plano). O pstack alcança confiança alta com review **depois** no artefato.

Pedido: `sdd-mode` atender vários cenários com **menos gates**, **review do agente**, menos o humano como semáforo — sem never-block e sem merge overnight.

---

## Alternativas

### Opção A — Manter G1+G2 bloqueantes no `full`/`standard` como default

- **Prós:** máximo alinhamento com “approve before execute” do lab Antigravity.
- **Contras:** o humano vira bottleneck; dois GOs para o mesmo HOW; não escala a fluxo agêntico.
- **Fonte:** https://codelabs.developers.google.com/sdd-adk-antigravity

### Opção B — Perfil `agentic` como default: gravar PLAN/TASKS, não esperar GO; agente analisa e revisa; um pacote humano no fim

- **Prós:** spec continua SSOT em `SDD/`; HOW rastreável; um ponto de atenção humana por mudança; G3 permanece; `full` fica para risco real.
- **Contras:** o humano vê o HOW depois de já haver código (retrabalho se o intent estava errado). Mitiga-se: CLARIFY só de produto; promover a `full` se o WHAT for incerto.
- **Fonte:** spec-kit caminho curto https://github.github.io/spec-kit/ ; pstack review-after (mecanismo, não never-block) https://github.com/cursor/plugins/tree/main/pstack

### Opção C — Never-block: executar e só pausar no irreversível, spec opcional

- **Prós:** máximo throughput.
- **Contras:** contradiz spec-kit e ADR-001.
- **Fonte:** pstack never-block-on-the-human (rejeitado).

---

## Decisão

**Opção B.** Default do `sdd-mode` é `agentic`, salvo o playbook ser `observe`/`design`/`lite`/`full` ou o humano pedir `full`.

No `agentic`:

1. Escrever o contrato em `SDD/` (SPEC/story; bug: nenhum novo).
2. Perguntar ao humano só preferência de produto (nenhum experimento responde).
3. Escrever PLAN+TASKS no mesmo fôlego; o agente faz analyze (spec vs plan vs tasks). **Não parar em G1/G2.**
4. IMPLEMENT + TDD sem GO por tarefa.
5. Playbook `review.md` contra o contrato.
6. G3 na superfície real.
7. **Um pacote humano:** contrato + diff + achados da review + evidência G3. Aceitar, corrigir, ou rejeitar.
8. Commit em **branch**. sdd-mode não mergeia `main`. Overnight land é pstack `shipping` depois de `review.md`+G3, só se o humano pediu.

`full` obrigatório quando: schema/serviço externo novo, compliance/dinheiro/saúde, WHAT incerto, ou o humano pediu.

---

## Consequências

### Positivas

- Menos interferência; review vira trabalho do agente.
- PLAN/TASKS ainda existem (rastreio), só não bloqueiam o default.

### Negativas (aceitas)

- Retrabalho se o intent estava errado e o agente implementou. Mitigação: BRIEF/CLARIFY de produto; `full` quando o WHAT não está claro.

### Como reverter

1. Default voltar a `full` no `sdd-mode`.
2. Playbooks de mudança recuperam **STOP GATE 1/2**.
3. Marcar este ADR ⏸️ SUPERSEDED.

---

## Addendum 2026-08-27 (policy split)

Never-block no HOW **é** este perfil. Não é skip de CLARIFY de produto nem do pacote. G3 é a linha `Smoke:` em `SDD/AGENTS.md`; sem evidência o `review.md` não pede accept.
