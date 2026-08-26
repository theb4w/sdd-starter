# ADR-001 — Usar uma skill de modo como interface, não um plugin

**Status:** ✔️ ACEITO
**Data:** 2026-08-25
**Autores:** Allan + Grok
**Spec relacionada:** `SDD/modules/SPEC_SDD_MODE.md`
**Substitui:** —

---

## Contexto

O starter precisa de um ponto de entrada que o agente não consiga ignorar (passos verbatim, principles, playbooks). O pstack prova que esse formato funciona, mas é um plugin Cursor. O `sdd-starter` acabou de se tornar tool-neutral (`SDD/plans/PLAN_SDD_CORE_NEUTRALITY.md`): o fluxo não pode depender de IDE, agente ou terminal.

A pergunta: o desenvolvedor invoca um **plugin**, uma **skill**, ou continua colando **prompts**?

---

## Alternativas Consideradas

### Opção A — Plugin Cursor (formato pstack completo)

**Descrição:** Empacotar o método como plugin (`/add-plugin sdd`) com skills, agents e slash commands.

- **Prós:** descoberta fácil no Cursor; um comando; subagentes nativos.
- **Contras:** amarra o core a um editor; Grok/Claude/humanos ficam de fora; drift entre plugin e `.agent/skills/sdd-mode/references/workflow.md`.
- **Custo:** manutenção dupla.
- **Reversibilidade:** média (desinstalar o plugin não remove o método se os arquivos existirem).
- **Fonte:** https://github.com/cursor/plugins/blob/main/pstack/README.md

### Opção B — Skill de modo no repo (`.agent/skills/sdd-mode`)

**Descrição:** Uma skill sticky que roteia a playbooks e principles. Templates continuam os artefatos. Plugin, se houver, só registra a mesma skill em `tooling/`.

- **Prós:** tool-neutral; vive ao lado de SPEC/PLAN; portável para qualquer agente que leia `SKILL.md`; uma casa para o procedimento.
- **Contras:** descoberta pior que `/add-plugin`; cada ferramenta precisa saber onde ler `.agent/skills/`.
- **Custo:** baixo (Markdown).
- **Reversibilidade:** fácil (remover a pasta; prompts ainda apontam).
- **Fonte:** https://github.com/sickn33/antigravity-awesome-skills/blob/main/docs/contributors/skill-anatomy.md

### Opção C — Manter prompts copy-paste como interface

**Descrição:** Status quo. Humano cola `sdd-mode playbooks (see .agent/skills/sdd-mode/playbooks/)*.md`.

- **Prós:** zero migração; funciona sem suporte a skills.
- **Contras:** agente resume e pula gates; passos duplicados em QUICKSTART/workflows; não escala para design/story/TDD.
- **Custo:** já pago em inconsistência.
- **Reversibilidade:** n/a (é o presente).
- **Fonte:** `.agent/skills/sdd-mode/references/workflow.md` §14.2

---

## Decisão

Escolhemos a **Opção B** porque preserva a regra de tool-neutrality já aprovada, entrega o mecanismo que o pstack acertou (modo + playbooks + principles), e deixa plugin como adaptador em `tooling/`. A opção A vira o método num sotaque de editor. A opção C não resolve o problema que motivou a refatoração.

Não adotamos a filosofia pstack “the best spec is code” nem “never block on the human”. Copiamos só o mecanismo. Fonte do recorte: https://github.com/cursor/plugins/blob/main/pstack/README.md (seção “why are there no planning skills?”) vs `.agent/skills/sdd-mode/references/workflow.md` §1.

---

## Consequências

### Positivas

- Um ponto de entrada (`sdd-mode`) para todos os cenários.
- Procedimento versionado no mesmo repo que os artefatos.
- Cursor/Grok/Claude podem carregar a mesma skill sem forking do método.

### Negativas (aceitas)

- Quem só usa Cursor não ganha `/add-plugin` no dia um.
- Agentes que não leem `.agent/skills/` ainda precisam do ponteiro em `sdd-mode playbooks (see .agent/skills/sdd-mode/playbooks/)`.

### Riscos mitigados

- **Risco:** plugin virar fonte de verdade.
  **Mitigação:** `tooling/` só registra; corpo da skill não se duplica.

### Risco residual

- Ferramentas com path diferente (`.grok/skills/`) exigem cópia ou nota de adapter — aceito porque o core permanece um arquivo.

---

## Como Reverter

1. Manter `sdd-mode playbooks (see .agent/skills/sdd-mode/playbooks/)` utilizáveis como ponteiros (fase 3 não apaga o nome do cenário).
2. Remover `.agent/skills/sdd-mode/` e `principle-*`.
3. Restaurar passos longos em `sdd-mode playbooks (see .agent/skills/sdd-mode/playbooks/)` a partir do git.
4. Marcar este ADR como ⏸️ SUPERSEDED.
