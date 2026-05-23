<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/NEW_FEATURE.md — Iniciar nova feature seguindo SDD
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO: você quer adicionar uma feature ao projeto e ele JÁ tem SDD ativo.

  TAMANHO DA FEATURE → ESCOPO DO PROMPT:
  - Pequena (≤100 LOC) — agente pula PLAN e ADR (a menos que detecte trade-off)
  - Média (100-400 LOC) — agente cria SPEC + ADRs + PLAN + TASKS
  - Grande (>400 LOC) — agente cria SPEC + ADRs + PLAN multi-fase + TASKS por fase

  Veja docs/SDD_WORKFLOW.md §2 (Modos de uso) para tabela completa.
═══════════════════════════════════════════════════════════════════════════════
-->

# NEW_FEATURE — Iniciar feature nova

```
Quero adicionar a feature: <DESCRIÇÃO_DA_FEATURE_EM_1-3_FRASES>

Tamanho estimado: <pequena | média | grande>
Módulo afetado (se sabe): <MODULO ou "novo módulo">
Prazo desejado: <hoje | semana | sem prazo>

LEIA NESTA ORDEM antes de qualquer ação:
1. AGENTS.md (regras absolutas)
2. specs/SPEC_INDEX.md (estado dos módulos)
3. docs/<Project>_Architecture.md (visão técnica)
4. docs/handover_*.md mais recente (estado atual)
5. Se feature toca módulo existente: specs/modules/SPEC_<MODULO>.md
6. ADRs aplicáveis (se houver)
7. .agent/skills/<dominio>/SKILL.md relevante

PROPOSTA DE ESCOPO (faça AGORA antes de codar):

1. Identifique o tamanho real da feature:
   - LOC estimado (chute conservador)
   - # de arquivos novos
   - # de arquivos modificados
   - Serviços externos novos? Quais?

2. Determine o modo SDD apropriado (consulte docs/SDD_WORKFLOW.md §2):
   - Pequena (≤100 LOC, sem trade-off): NEW_FEATURE simples
     → Estende SPEC existente, sem PLAN/ADR, com TASKS curta
   - Média (100-400 LOC): NEW_FEATURE com SPEC nova
     → SPEC nova + ADRs se trade-off + PLAN + TASKS
   - Grande (>400 LOC): NEW_FEATURE com SPEC multi-fase
     → SPEC nova + ADRs múltiplas + PLAN multi-fase + TASKS por fase

3. Identifique trade-offs ARQUITETURAIS:
   - Há decisão com 2+ alternativas viáveis?
   - Há impacto em compliance / custo / vendor lock-in?
   - Se sim → propor ADR ANTES de gerar PLAN

4. Liste perguntas CLARIFY que você tem:
   - Comportamento esperado em casos edge?
   - Compatibilidade com módulos existentes?
   - Performance / cost target?

PROCEDA NESTA ORDEM (parando entre cada para meu GO):

Etapa 1 — Análise inicial
   Apresente: tamanho estimado, modo SDD escolhido, trade-offs detectados,
   perguntas CLARIFY. AGUARDE meu GO.

Etapa 2 — Criar/atualizar SPEC (conforme tamanho)
   Pequena: estender specs/modules/SPEC_<MODULO>.md (mostrar diff)
   Média/Grande: criar specs/modules/SPEC_<NOVA>.md baseada em template
   Mostre conteúdo. AGUARDE meu GO.

Etapa 3 — CLARIFY (se houver perguntas)
   Eu respondo as perguntas. Você atualiza §10 (Histórico) da SPEC.
   Promove status para 📋 PLAN se §9 ficar vazia.
   AGUARDE meu GO.

Etapa 4 — Propor ADRs (se trade-offs detectados)
   Para cada ADR: contexto + 2+ alternativas + recomendação.
   AGUARDE minha decisão. Marque como ✔️ ACEITO só após GO.

Etapa 5 — Gerar PLAN (se média/grande)
   specs/plans/PLAN_<MODULO>.md baseado em template.
   Decidir multi-fase ou single-phase pelos critérios de SDD_WORKFLOW §13.1.
   🛑 GATE 1 — AGUARDE aprovação do PLAN.

Etapa 6 — Gerar TASKS
   specs/plans/TASKS_<MODULO>.md atômico, com AC verificável.
   Última tarefa de cada fase = commit; penúltima = smoke; antepenúltima = validação completa definida pelo projeto.
   🛑 GATE 2 — AGUARDE aprovação das TASKS.

Etapa 7 — Implementar (após GATEs)
   Use .agent/workflows/sdd_implement.md como guia.
   1 tarefa por vez, AC verificado a cada uma.
   Smoke staging antes do commit (GATE 3).
   Push após revisão humana do diff (GATE 4).

Etapa 8 — Handover de fase
   Use prompts/HANDOVER.md para gerar handover.
   Atualize SPEC_INDEX.md.

REGRAS NÃO-NEGOCIÁVEIS:
- Sem código sem PLAN+TASKS aprovados (média/grande)
- Toda decisão técnica registra URL de fonte primária
- Regras técnicas específicas do projeto quando houver
- Sem hardcode de credenciais
- Type hints / Types em funções públicas
- PR ≤250 LOC
- Conventional Commits
- Backward-compat por commit
- Tarefas [bloq.] em TASKS são gates humanos

NÃO COMECE pela Etapa 2. Sempre Etapa 1 primeiro com análise + meu GO.
```

---

## Como preencher os placeholders

| Placeholder | Como decidir |
|---|---|
| `<DESCRIÇÃO_DA_FEATURE>` | 1-3 frases descrevendo o que a feature faz e para quem |
| `<pequena/média/grande>` | Use sua melhor estimativa; agente confirmará |
| `<MODULO>` | Olhe SPEC_INDEX.md; se não tem módulo apropriado, escreva "novo módulo" |
| `<prazo>` | Realista — agente NÃO cortará caminho por causa de prazo, só ajusta escopo |

---

## Anti-padrões comuns

| Anti-padrão | Por quê é ruim |
|---|---|
| "Implementa logo, é simples" sem SPEC | Captura zero contexto para próxima sessão |
| Skipear ADR de trade-off | Decisão vira tribal knowledge, perdida em meses |
| PLAN com >5 arquivos novos sem multi-fase | PR gigante, taxa de bug 2-3x maior |
| Pular GATE 3 (smoke) | Refator de prompt LLM passa por unit, falha em UX |
| Commit sem GATE 4 | Self-review é o filtro mais barato; não pular |
