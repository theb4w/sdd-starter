# SPEC_SDD_MODE — Skill de modo SDD (roteador + playbooks + principles)

**Status:** ✔️ CONCLUÍDO
**Autor(es):** Allan + Grok
**Data de criação:** 2026-08-25
**Última atualização:** 2026-08-27
**Spec relacionadas:** `SDD/decisions/ADR-001-skill-as-interface.md`, `SDD/decisions/ADR-002-gate-profiles.md`, `SDD/decisions/ADR-003-agentic-default.md`

---

## 1. Objetivo

Dar ao desenvolvedor um ponto de entrada único (`sdd-mode`) que aplica Spec-Driven Development em todos os cenários do starter. Formato operacional no estilo pstack (modo sticky, playbooks verbatim, principles invocáveis). Sob pstack/poteto-mode, **sdd-mode é a camada de contrato** (pstack executa). Sem depender de uma IDE e sem autonomia que pule o pacote humano.

---

## 2. Contexto e Justificativa

- **Architecture:** o starter não tem `SDD/architecture.md` preenchido; a visão canônica do método é `sdd-mode/references/workflow.md` (skill root).
- **Problema resolvido:** o procedimento era prompts + QUICKSTART + workflows em paralelo; o agente resumia e pulava GATE. Agora só `sdd-mode` + `SDD/`.
- **ADRs aplicáveis:** ADR-001, ADR-002, ADR-003.
- **Constraints:** tool-neutrality; skill root host-agnostic; regras em `SDD/AGENTS.md`; templates na skill.
- **Fonte do formato:** https://github.com/cursor/plugins/blob/main/pstack/README.md
- **Fonte do método:** `sdd-mode/references/workflow.md` e https://codelabs.developers.google.com/sdd-adk-antigravity

---

## 3. Design Técnico

### 3.1 Estruturas de dados

Camadas (uma casa por fato):

| Camada | Casa | Papel |
|---|---|---|
| Método | `sdd-mode/references/workflow.md` | o quê / por quê / quando |
| Procedimento | `sdd-mode/` no skill root | como executar agora |
| Catálogo | `sdd-mode/references/catalog.md` | intenção → playbook (ganha se houver drift) |
| Contrato persistido | `SDD/` | o que a skill escreve |
| Templates | `sdd-mode/templates/` (ao lado de `SKILL.md`) | copiados para `SDD/` no Step 0 |

Skill root: primeira pasta que contém `sdd-mode/SKILL.md` (`.cursor/.grok/.kiro/.agents/.agent/skills` ou user-level). Este checkout: `.agent/skills/`. Ver `references/skill-root.md`.

A skill `sdd-mode` casa a demanda a uma linha de `catalog.md`, copia os passos do playbook, dispara principles/skills nomeadas, e **para** só onde o perfil da linha manda. Skip só com `skip: motivo`.

Perfis de gate: `observe` | `design` | `lite` | `agentic` (default, ADR-003) | `full`. `standard` = `agentic`.

### 3.2 Sequence diagram

```mermaid
sequenceDiagram
    participant Dev
    participant Mode as sdd-mode
    participant Book as playbook
    participant Artifacts as SDD
    participant Human as gate humano

    Dev->>Mode: demanda
    Mode->>Mode: ler índice de principles
    Mode->>Book: match + copiar passos
    Book->>Artifacts: escrever/ler contrato do perfil
    Book->>Artifacts: Step 0 Ensure SDD/
    Book->>Human: parar só no stop do perfil
    Human-->>Book: aprovar ou rejeitar
    Book->>Artifacts: IMPLEMENT (agentic: após CLARIFY; full: após G1+G2)
    Book->>Book: review.md
    Book->>Human: um pacote (review + G3 + diff)
    Book->>Dev: evidência + reply
```

### 3.3 Fluxos críticos

1. **Feature média:** catalog `New behavior` → `feature.md` / `agentic` → SPEC/CLARIFY produto → PLAN+TASKS gravados → TDD IMPLEMENT → `review.md` → G3 → **pacote** → handover. `full` só se promover.
2. **Bug simples:** catalog `Broken / repro` → `bug-fix.md` / `lite` → repro → causa raiz → RED-GREEN → `review.md` → G3 no mesmo repro → pacote.
3. **Design sem código:** catalog `Shape / UX still open` → `design.md` / `design` → `SDD/design/<slug>.md` → um GO → sem código de produção.
4. **User story:** catalog row → `user-story.md` / `agentic` → exige SPEC de módulo → Given/When/Then → TDD → `review.md` → G3 → pacote.

---

## 4. Regras de Negócio

| ID | Regra | Fonte |
|---|---|---|
| RN-SDD_MODE-01 | Código de produção só após o contrato do playbook (SPEC, story, ou “nenhum” em bug) | `SDD/AGENTS.md` regra 1; principle-spec-first |
| RN-SDD_MODE-02 | O playbook declara o perfil de gate; o agente não escolhe `lite` para pular PLAN em feature média | ADR-002 |
| RN-SDD_MODE-03 | Skip de passo só com `skip: motivo` no todo | pstack poteto-mode (mecanismo) |
| RN-SDD_MODE-04 | Parar no gate do perfil; não perguntar permissão dentro de TASK já aprovada | principle-stop-at-gate |
| RN-SDD_MODE-05 | Módulo novo não nasce só de user story | esta SPEC §3.3 |
| RN-SDD_MODE-06 | TDD RED-GREEN é default quando o teste local for barato; skip com motivo; G3 permanece nos perfis que geram código | principle-tdd-red-green |
| RN-SDD_MODE-07 | Skill canônica em `sdd-mode/` no skill root do host; não é plugin | ADR-001; `skill-root.md` |
| RN-SDD_MODE-08 | Não copiar “best spec is code”. Never-block no HOW = `agentic`. sdd-mode não mergeia `main` | ADR-001; `with-pstack.md` |
| RN-SDD_MODE-10 | Pacote sem `Smoke:` evidenciado não pede accept | `review.md`; principle-prove-it-works |
| RN-SDD_MODE-11 | Sob pstack, carregar sdd-mode antes de feature/bug/refactor (não `skip:`) | `with-pstack.md`; `.cursor/rules/sdd-under-pstack.mdc` |
| RN-SDD_MODE-09 | Artefatos só em `SDD/`; passos só nos playbooks | principle-one-home-per-fact |

---

## 5. Variáveis de Ambiente

Nenhuma. A skill não lê secrets nem escolhe stack.

---

## 6. Arquivos a Criar/Modificar

### Arquivos novos

| Caminho | Função |
|---|---|
| `<skill-root>/sdd-mode/SKILL.md` | Roteador sticky |
| `<skill-root>/sdd-mode/playbooks/*.md` | Passos por cenário (header = catalog) |
| `<skill-root>/sdd-mode/references/catalog.md` | Intenção → playbook (SSOT do match) |
| `<skill-root>/principle-*/SKILL.md` | Uma regra cada |
| `<skill-root>/sdd-tdd/SKILL.md` | Loop RED-GREEN |
| `<skill-root>/sdd-mode/templates/` | Fontes copiadas para `SDD/` no Step 0 |
| `<skill-root>/sdd-mode/templates/cursor-rule.mdc` | Always-on Cursor: load sdd under pstack |
| `SDD/` | Processo gerado do produto |

### Arquivos modificados

| Caminho | Mudança |
|---|---|
| `<skill-root>/sdd-mode/SKILL.md` | **Step 0 — Ensure `SDD/`** (não “preamble”) |
| `README.md` | Skill pack; sem docs paralelos |
| `SDD/INDEX.md` | Este módulo + ADRs |

---

## 7. Testes Requeridos

Não há runtime. Verificação por consistência documental.

| ID | Tipo | Cobertura | AC |
|---|---|---|---|
| T-SDD_MODE-01 | review | cada playbook declara Family/Intent/Profile iguais ao catálogo | `catalog.md` vs headers em `playbooks/` |
| T-SDD_MODE-02 | review | playbooks escrevem só em `SDD/` | nenhum path `specs/` ou `prompts/` nos playbooks |
| T-SDD_MODE-03 | review | uma casa por fato | processo em `SDD/`; procedimento na skill |
| T-SDD_MODE-04 | review | composição pstack | `with-pstack.md` cinde HOW vs package vs shipping; skill não mergeia `main` |
| T-SDD_MODE-05 | review | dry-run A | headers = `catalog.md` |
| T-SDD_MODE-06 | review | G3 | `review.md` recusa accept sem `Smoke:` |

---

## 8. Critérios de Aceite (DoD)

- [x] `sdd-mode` casa os cenários (bootstrap … onboarding + camada extra)
- [x] Playbooks: investigation, design, prototype, user-story, tdd-implement, multi-phase
- [x] Principles + TDD + stop-at-gate
- [x] Perfis de gate no workflow e nos playbooks
- [x] Templates na skill; artefatos em `SDD/`
- [x] Sem plugin como core
- [x] `SDD/INDEX.md` e ADRs atualizados
- [x] Cursor rule + install; índice inline de principles; `Smoke:`; resume sem GO extra; dry-run

---

## 9. CLARIFY — perguntas abertas

Nenhuma. Decisões em ADR-001 e ADR-002.

---

## 10. Histórico

- 2026-08-25: SPEC criada a partir do plano aprovado (skill de modo, formato pstack, método SDD).
- 2026-08-27: ADR-003 agentic; skill root host-agnostic; Step 0 no lugar de “preamble”; catálogo único; composição com pstack.
- 2026-08-27: Cursor glue; never-block cindido; workflow apêndice; G3=`Smoke:`; dry-run.
