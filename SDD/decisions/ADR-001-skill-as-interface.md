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

### Opção C — Prompts copy-paste como interface

**Descrição:** Humano cola roteiros longos a cada sessão.

- **Prós:** zero migração; funciona sem suporte a skills.
- **Contras:** agente resume e pula gates; passos duplicados; não escala.
- **Custo:** inconsistência.
- **Reversibilidade:** n/a (era o status quo).
- **Fonte:** ciclo anterior deste repo (`prompts/`, removido).

---

## Decisão

Escolhemos a **Opção B** porque preserva tool-neutrality e entrega o mecanismo do pstack (modo + playbooks + principles) sem plugin. Artefatos do produto vão em `SDD/`. A opção A vira o método num sotaque de editor. A opção C não resolve o problema.

Não adotamos a filosofia pstack “the best spec is code” nem “never block on the human”. Copiamos só o mecanismo. Fonte do recorte: https://github.com/cursor/plugins/blob/main/pstack/README.md (seção “why are there no planning skills?”) vs `.agent/skills/sdd-mode/references/workflow.md` §1.

---

## Consequências

### Positivas

- Um ponto de entrada (`sdd-mode`) para todos os cenários.
- Procedimento versionado no mesmo repo que os artefatos.
- Cursor/Grok/Claude podem carregar a mesma skill sem forking do método.

### Negativas (aceitas)

- Quem só usa Cursor não ganha `/add-plugin` no dia um.
- Agentes que não leem `.agent/skills/` precisam copiar o pack ou ser apontados ao `SKILL.md`.

### Riscos mitigados

- **Risco:** plugin virar fonte de verdade.
  **Mitigação:** este pack não envia plugin; o corpo da skill não se duplica.

### Risco residual

- Ferramentas com path diferente exigem cópia ou nota de adapter — aceito porque o core permanece um arquivo.

---

## Como Reverter

1. Remover `sdd-mode/` e `principle-*` do skill root em uso.
2. Restaurar o kit antigo a partir do git (commit anterior a `32ca261`).
3. Marcar este ADR como ⏸️ SUPERSEDED.

---

## Addendum 2026-08-27

A decisão (skill, não plugin) não muda. O **parent** da skill não é só `.agent/skills/`. Hosts usam `.cursor/skills`, `.grok/skills`, `.kiro/skills`, `.agents/skills` (Antigravity), `.agent/skills` (este checkout), ou equivalentes do usuário. Resolver via `sdd-mode/references/skill-root.md`. Copiar `sdd-mode/` (e `principle-*`, `sdd-tdd`) para a pasta do host; não forkar o Markdown. `SDD/` continua na raiz do repo alvo.

Sob pstack/poteto-mode, sdd-mode é a **camada de contrato** (`references/with-pstack.md`): pstack executa; sdd grava `SDD/` e o pacote. Never-block no HOW = perfil `agentic`. Overnight land = pstack `shipping` após G3, só se o humano pediu. “Best spec is code” continua recusado. sdd-mode não mergeia `main`. Cursor: rule always-on + `references/install.md`.
