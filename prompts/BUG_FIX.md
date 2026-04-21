<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/BUG_FIX.md — Resolver bug com rastreabilidade SDD
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO: detectou bug em produção/staging/local que precisa fix.

  CICLO REDUZIDO: bug fix simples NÃO precisa SPEC nova. Mas:
  - SE o fix muda comportamento → ADR
  - SEMPRE: regression test (sem teste, bug volta)
  - SEMPRE: GATE 3 (smoke) e GATE 4 (commit)
═══════════════════════════════════════════════════════════════════════════════
-->

# BUG_FIX — Investigar e corrigir bug

```
Bug detectado: <DESCRIÇÃO_DO_BUG>

Onde foi visto: <produção | staging | local | logs/relato de usuário>
Severidade: <crítico | alto | médio | baixo>
Reprodução: <passos para reproduzir, OU "ainda não reproduzido">

LEIA NESTA ORDEM antes de qualquer ação:
1. AGENTS.md (regras absolutas)
2. specs/SPEC_INDEX.md (módulos e ADRs)
3. Se sabe módulo afetado: specs/modules/SPEC_<MODULO>.md
4. .agent/skills/<dominio>/SKILL.md (anti-padrões da stack)
5. docs/handover_*.md mais recente (mudanças recentes)

PROCEDA EM 4 ETAPAS (parando entre cada para meu GO):

Etapa 1 — Investigação (NÃO codar ainda)
   1. Localize o módulo/arquivo provável (use rg, glob, semantic search).
   2. Reproduza o bug localmente OU peça mais info para reprodução.
   3. Identifique ROOT CAUSE (não só sintoma):
      - O que esperávamos? (referencie SPEC ou comportamento documentado)
      - O que aconteceu?
      - Por quê?
   4. Verifique se o bug foi introduzido recentemente:
      - git log --oneline -- <arquivo> | head -20
      - Se mudança recente identificada, mencione PR/commit.
   5. Avalie blast radius: quantos usuários impactados? quantas funcionalidades?

   APRESENTE: relatório de investigação (1-2 parágrafos).
   AGUARDE meu GO para Etapa 2.

Etapa 2 — Decisão de escopo
   Determine o modo SDD apropriado:
   (a) Bug fix puro (≤30 LOC, sem mudança de comportamento esperado):
       → Não precisa SPEC nova, não precisa ADR
       → Direto para fix + regression test
   (b) Bug por regra de negócio errada (precisa decidir comportamento correto):
       → Precisa CLARIFY humano + atualizar SPEC + talvez ADR
   (c) Bug arquitetural (afeta design — ex.: race condition, deadlock):
       → Precisa ADR de mitigação + possivelmente refactor (use prompts/REFACTOR.md)

   APRESENTE: modo escolhido + justificativa.
   AGUARDE meu GO para Etapa 3.

Etapa 3 — Fix + Regression test
   1. Crie regression test PRIMEIRO (TDD: teste que reproduz o bug, falha).
   2. Implemente o fix mínimo (apenas o necessário, sem refactor opportunista).
   3. Confirme regression test agora passa.
   4. Rode testes full: 0 regressão.
   5. Se mudança de comportamento esperado:
      - Atualize SPEC §3 (Design) ou §4 (Regras de Negócio)
      - Crie ADR se trade-off envolvido

   APRESENTE: diff + resultados de testes.
   AGUARDE meu GO para Etapa 4.

Etapa 4 — Smoke + Commit + Handover
   🛑 GATE 3 — Deploy staging + smoke do fluxo afetado
              (validar que o bug NÃO ocorre mais E que nada relacionado quebrou)
   🛑 GATE 4 — Commit (após revisão humana do diff)
   
   Mensagem de commit (use HEREDOC):
   git commit -m "$(cat <<'EOF'
   fix(<modulo>): <título imperativo descrevendo o fix>

   <Por quê o bug acontecia (root cause), não o que fizemos>.
   Adiciona regression test em tests/unit/test_<modulo>.py::test_<bug>.

   Fixes #<N> (se houver issue).
   EOF
   )"
   
   Handover (se sessão termina aqui):
   - Use prompts/HANDOVER.md
   - Categoria: handover_BUGFIX_<DATA>.md (não está numa fase de SPEC)

REGRAS NÃO-NEGOCIÁVEIS:
- ❌ NUNCA fix sem regression test (bug volta)
- ❌ NUNCA "while I'm here, also refactor X" (separar refator do fix)
- ❌ NUNCA skip smoke (regressão de UX é o que mais escapa)
- ✓  SEMPRE root cause analysis antes de codar
- ✓  SEMPRE Conventional Commits com tipo `fix:`
- ✓  SEMPRE referência à issue/handover/SPEC quando existir

PR ≤100 LOC para bug fix. Se passar, separar em 2 PRs.
```

---

## Como preencher os placeholders

| Placeholder | Como decidir |
|---|---|
| `<DESCRIÇÃO_DO_BUG>` | Sintoma observável: "endpoint X retorna 500 quando Y" |
| `<onde foi visto>` | Sempre informe — bug de produção tem prioridade alta |
| `<severidade>` | Crítico = data loss / serviço down; alto = funcionalidade quebrada para >1% |
| `<passos para reproduzir>` | Quanto mais preciso, mais rápido o fix |

---

## Anti-padrões clássicos em bug fix

| Anti-padrão | Sintoma | Correção |
|---|---|---|
| Fix do sintoma, não da causa | Bug volta em formato ligeiramente diferente | Root cause analysis |
| Refator opportunista junto do fix | PR enorme, difícil revisar | Separar em 2 commits/PRs |
| Sem regression test | Bug volta em 3 meses | TDD: teste antes do fix |
| Smoke pulado | UX quebrada em produção | GATE 3 obrigatório |
| Mensagem de commit vaga ("fix bug") | Histórico inútil | "fix(modulo): título imperativo + por quê" |

---

## Quando bug fix vira refactor

Se a investigação revelar que:
- O bug é sintoma de design ruim
- Múltiplos bugs similares vão aparecer
- Fix mínimo seria gambiarra

→ NÃO faça gambiarra. Pause, abra `prompts/REFACTOR.md`, e proponha ADR de migração.
