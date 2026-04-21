<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/REFACTOR.md — Refator com ADR de migração
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO:
  - Quer melhorar código sem mudar comportamento (refactor interno)
  - OU mudar contrato/arquitetura (refactor arquitetural — exige migração)

  REGRA DE OURO: refator SEM teste de regressão é mudança não-intencional
  esperando para acontecer. SEMPRE testes verdes antes E depois.
═══════════════════════════════════════════════════════════════════════════════
-->

# REFACTOR — Refatorar com rastreabilidade

```
Refator proposto: <DESCRIÇÃO_DO_REFATOR>

Tipo: <interno (sem mudança contratual) | arquitetural (muda contrato)>
Módulo(s) afetado(s): <lista>
Motivação: <por quê — debt técnico, performance, manutenibilidade, prep para feature>
Tamanho estimado: <≤200 LOC | 200-500 | >500>

LEIA NESTA ORDEM antes de qualquer ação:
1. AGENTS.md (regras absolutas)
2. specs/SPEC_INDEX.md
3. specs/modules/SPEC_<MODULO>.md (módulo a refatorar)
4. ADRs aplicáveis (especialmente as que motivaram design atual)
5. tests/ relevantes (cobertura é base do refator seguro)
6. .agent/skills/<dominio>/SKILL.md

PROCEDA NESTA ORDEM (parando entre cada para meu GO):

Etapa 1 — Análise de cobertura e justificativa
   1. Audite cobertura atual do módulo:
      - pytest --cov=app.<modulo> ou equivalente
      - É ≥80%? Se NÃO → adicionar testes ANTES de refatorar (segurança)
   2. Justifique o refator concretamente:
      - Métrica que vai melhorar (latência? LOC? complexidade ciclomática?)
      - Bug que vai prevenir (race condition? memory leak?)
      - Feature futura que vai habilitar (e qual)
   3. Identifique tipo de refator:
      (a) Interno: nomes, extração de função, divisão de arquivo
          → SEM mudança de contrato; sem ADR (a menos que justifique padrão)
      (b) Arquitetural: muda interface pública, troca dependência, schema DB
          → COM ADR de migração obrigatória + plano de rollback
   4. Estime LOC + arquivos tocados.

   APRESENTE: análise + tipo escolhido + justificativa.
   AGUARDE meu GO para Etapa 2.

Etapa 2 — Aumentar cobertura (se necessário)
   Se cobertura <80%:
   1. Identifique funções críticas sem teste.
   2. Adicione testes ANTES de tocar no código de produção.
   3. Confirme pytest --cov ≥80% no módulo.

   Se cobertura ≥80%: pular esta etapa.

   APRESENTE: testes adicionados (se houve) ou confirmação de cobertura.
   AGUARDE meu GO para Etapa 3.

Etapa 3 — Decisão de modo SDD
   (a) Refator interno: vai direto para Etapa 5 (sem SPEC/PLAN, com TASKS curta)
   (b) Refator arquitetural: precisa SPEC nova ("v2") + ADR de migração + PLAN multi-fase

   Para refator arquitetural:
   - Crie ADR de migração baseado em specs/decisions/_ADR_TEMPLATE.md
     * Contexto: por quê o design atual não serve mais
     * Alternativas: opção atual + 1+ alternativas de migração
     * Decisão: nova arquitetura + caminho de migração
     * Como reverter: passos para voltar ao design anterior
   - Crie SPEC nova com sufixo "_v2": specs/modules/SPEC_<MODULO>_v2.md
   - PLAN multi-fase com expand-contract:
     Fase A: implementar novo lado-a-lado do antigo
     Fase B: migrar dados/clientes para o novo
     Fase C: remover antigo

   APRESENTE: ADR + SPEC v2 + PLAN.
   🛑 GATE 1 — AGUARDE aprovação do PLAN.

Etapa 4 — Gerar TASKS (se arquitetural)
   specs/plans/TASKS_<MODULO>_v2.md por fase, atômico.
   🛑 GATE 2 — AGUARDE aprovação das TASKS.

Etapa 5 — Refator (1 tarefa por vez)
   REGRA INVIOLÁVEL: testes verdes antes E depois de cada tarefa.
   - Se fizer 1 mudança e teste quebra → não é refator, é mudança de comportamento → reverter ou atualizar teste com justificativa em commit
   
   Use .agent/workflows/sdd_implement.md como guia.

Etapa 6 — Smoke + Commit + Handover
   🛑 GATE 3 — Smoke staging (validar que comportamento NÃO mudou)
   🛑 GATE 4 — Commit (Conventional Commit tipo `refactor:`)
   
   Mensagem (HEREDOC):
   git commit -m "$(cat <<'EOF'
   refactor(<modulo>): <título — o que mudou estruturalmente>

   <Por quê — qual debt técnico, qual feature futura, qual métrica melhora>.
   Cobertura mantida em <X>%. Comportamento observável idêntico (smoke OK).
   EOF
   )"

REGRAS NÃO-NEGOCIÁVEIS:
- ❌ NUNCA refatorar com cobertura <80% (refator vira aposta)
- ❌ NUNCA misturar refactor com feat ou fix (separar em commits/PRs)
- ❌ NUNCA refatorar sem ADR se muda contrato público
- ❌ NUNCA "big bang refactor" — sempre expand-contract por fases
- ✓  SEMPRE testes verdes antes E depois de cada tarefa
- ✓  SEMPRE Conventional Commits com tipo `refactor:`
- ✓  PR ≤200 LOC para refactor

DEFINIÇÃO DE PRONTO (refator interno):
- [ ] Cobertura mantida ou aumentada
- [ ] Pytest -q 0 falhas
- [ ] Lint sem erros
- [ ] Smoke staging: comportamento idêntico
- [ ] Commit message explica POR QUÊ refatorar (não O QUÊ)

DEFINIÇÃO DE PRONTO (refator arquitetural):
- [ ] ADR de migração ✔️ ACEITO
- [ ] SPEC v2 ✔️ APROVADA
- [ ] Todas as fases (A, B, C) concluídas
- [ ] Migração de dados verificada (sample real)
- [ ] Lado antigo removido com gate humano explícito
- [ ] Plano de rollback documentado e testado em staging
```

---

## Quando NÃO refatorar

| Situação | Razão |
|---|---|
| Time sem testes adequados | Refator vira aposta; aumentar cobertura primeiro |
| Pressão por feature urgente | Não competir por janela; planejar para sprint dedicado |
| Sem buy-in do time | Refator vira flame war; alinhamento ANTES de codar |
| "Não gostei do nome da função" | Triviais não justificam ciclo SDD; PR menor sem prompt |

---

## Padrões de refator arquitetural

### Expand-Contract (Strangler Fig)
```
Fase A: novo coexiste com antigo (feature flag, dispatch)
Fase B: novo recebe % do tráfego (canary)
Fase C: novo recebe 100%; antigo deprecated
Fase D: antigo removido (gate humano explícito)
```

### Dual-write (mudança de DB)
```
Fase A: app escreve em ambos (antigo + novo); lê do antigo
Fase B: backfill histórico para o novo
Fase C: app lê do novo, valida contra antigo (assert)
Fase D: app só usa o novo; antigo removido
```

### Reference: https://martinfowler.com/bliki/StranglerFigApplication.html
