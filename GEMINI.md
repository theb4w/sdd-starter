<!--
═══════════════════════════════════════════════════════════════════════════════
  GEMINI.md — Overrides específicos para Google Antigravity
═══════════════════════════════════════════════════════════════════════════════

  Antigravity lê este arquivo ANTES do AGENTS.md. Tem precedência em conflitos.

  [OPCIONAL] Apague este arquivo se você não usa Antigravity.
  Outros IDEs (Cursor, Jules, Gemini CLI, Claude Code) ignoram-no.

  Fonte: https://antigravity.codes/blog/user-rules
  Codelab: https://codelabs.developers.google.com/autonomous-ai-developer-pipelines-antigravity
═══════════════════════════════════════════════════════════════════════════════
-->

# GEMINI.md — Overrides Antigravity para <!-- ADAPT: NOME_DO_PROJETO -->

---

## Modo de operação padrão

- **SEMPRE** usar **Planning Mode** (não Fast Mode) para qualquer IMPLEMENT.
- **SEMPRE** gerar "Implementation Plan" como artifact antes de código.
- **SEMPRE** gerar "Task List" como artifact antes de executar o plano.
- **NUNCA** escrever código sem aprovação humana nos dois artifacts acima.
- Para tarefas triviais (renomear variável, corrigir typo): Fast Mode permitido.

## Persona padrão

- @engineer (ver `.agent/agents.md`).
- Stack: <!-- ADAPT: ex.: Python 3.11 + FastAPI + PostgreSQL -->
- Modelo padrão: <!-- ADAPT: ex.: gemini-2.5-flash-lite -->
- Não sugerir mudança de stack sem ADR aprovado em `specs/decisions/`.
- Sempre ler `.agent/skills/<dominio>/SKILL.md` relevante antes de implementar.

## Referência de arquivos

- Constituição: `AGENTS.md`
- Specs: `specs/modules/SPEC_*.md`
- Decisões: `specs/decisions/ADR-*.md`
- Skills técnicas: `.agent/skills/<nome>/SKILL.md`
- Personas: `.agent/agents.md`
- Workflow SDD: `docs/SDD_WORKFLOW.md`
- Prompts copy-paste: `prompts/`

## Idioma

<!-- ADAPT: linguagem padrão do projeto. Exemplo:

- Responder SEMPRE em português
- Comentários de código: português para decisões, inglês para docstrings técnicas
-->

## Regras de privacidade não-negociáveis

<!-- ADAPT: regras de compliance específicas. Exemplo:

- Nunca logar conteúdo de mensagem do usuário
- Paid tier obrigatório para inferência (não free tier)
- Fonte: https://cloud.google.com/vertex-ai/generative-ai/docs/data-governance
-->
