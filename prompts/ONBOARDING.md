<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/ONBOARDING.md — Sessão nova num projeto que JÁ usa SDD
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO:
  - Você é um dev novo no projeto (e o projeto JÁ tem SDD ativo)
  - OU sessão nova num projeto seu após dias/semanas afastado
  - OU agente novo (Cursor/Claude/Antigravity) num projeto SDD existente

  RESULTADO ESPERADO: agente lê constituição, último handover e SPEC_INDEX,
  e te resume o estado do projeto em 2-3 minutos. Pronto pra próxima task.
═══════════════════════════════════════════════════════════════════════════════
-->

# ONBOARDING — Sessão nova em projeto SDD existente

**Projeto:** <PROJETO>
**Data:** <DATA_HOJE>
**Operador:** <SEU_NOME>

---

## Antes de qualquer ação, leia e resuma (nesta ordem)

1. `AGENTS.md` — constituição cross-tool do projeto
2. `GEMINI.md` (se existir) — overrides Antigravity
3. `docs/SDD_WORKFLOW.md` — framework canônico
4. `.agent/agents.md` — personas
5. `.agent/skills/*/SKILL.md` — regras técnicas por domínio
6. `specs/SPEC_INDEX.md` — status atual de cada módulo
7. `docs/<Project>_Architecture.md` — visão técnica completa
8. `docs/handover_*.md` (mais recente — `ls docs/handover_*.md | sort | tail -1`)
9. PROJECT_BRIEF.md (se existir)

---

## Responda nesta ordem (sem código, só análise)

### a. Qual a identidade do projeto?
- Nome, objetivo, estágio
- IDE primária esperada
- Stack técnica (versões fixadas)

### b. Quais regras absolutas você está obrigado a seguir?
- Liste as 6 regras universais do AGENTS.md
- Liste as regras absolutas específicas do projeto

### c. Qual o estado atual?
- Módulos no SPEC_INDEX e seus status
- Última fase concluída (do handover mais recente)
- Quem é o próximo módulo / próxima fase

### d. Há ADRs aceitos que afetam trabalho atual?
- Liste ADRs relevantes para próxima task

### e. Há pendências bloqueadoras?
- Do último handover §6 (Pendências)
- Há recursos cloud não-provisionados?

### f. Qual o próximo passo natural?
- Conforme §7 do último handover (Próximos Passos)
- Quem aprova o próximo gate (humano específico)

---

## Aguardar instruções do humano

Após responder a-f, escreva:

```
🛑 ONBOARDING COMPLETO — Aguardando sua próxima instrução.

Sugestões baseadas no estado atual:
- Se quer continuar fase em andamento → use prompts/RESUME.md
- Se quer iniciar nova feature → use prompts/NEW_FEATURE.md
- Se há bug a resolver → use prompts/BUG_FIX.md
- Se quer refatorar algo → use prompts/REFACTOR.md
- Se quer encerrar a sessão → use prompts/HANDOVER.md
```

---

## Restrições

- **NÃO ESCREVA CÓDIGO** nesta sessão de onboarding.
- **NÃO INICIE** nenhuma task sem instrução explícita do humano.
- **NÃO EDITE** nenhum arquivo (mesmo que pareça ter typo / inconsistência) — anote para mencionar e deixar humano decidir.
- Se algum arquivo crítico estiver faltando (AGENTS.md, SPEC_INDEX), avise antes de prosseguir.

---

## Tempo esperado

- Onboarding completo: 2-5 minutos.
- Se passar de 10 min só lendo, algo está errado (handover muito longo, AGENTS.md desatualizado) — sinalize para humano.
