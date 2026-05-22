<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/RESUME.md — Retomar fase intermediária de SPEC multi-fase
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO:
  - Você está no MEIO de uma SPEC multi-fase
  - Encerrou sessão anterior com handover de fase
  - Quer continuar a próxima fase (T-X1) com contexto preservado

  COMO USAR:
  1. PREENCHA todos os <PLACEHOLDERS> abaixo conforme seu projeto
  2. Cole o resultado no chat do agente
  3. Agente vai LER tudo, mostrar plano com checkboxes, e AGUARDAR seu GO

  IMPORTANTE: este prompt assume que GATE 1 e GATE 2 já foram aprovados em
  sessão anterior. Não revisa decisões já tomadas.
═══════════════════════════════════════════════════════════════════════════════
-->

# RESUME — Retomar fase de <MODULO>

```
Retomar <PROJETO> — iniciar SPEC_<MODULO> Fase <X> (<descrição_curta>).

LEIA NESTA ORDEM antes de qualquer ação:
1. docs/SDD_WORKFLOW.md (metodo)
2. AGENTS.md (instrucoes do projeto, se agentes participam)
3. instrucoes opcionais de tooling adotadas pelo projeto
4. docs/handover_<MODULO>_FASE_<X-1>_<DATA>.md (autoridade do estado previo)
5. specs/SPEC_INDEX.md
6. specs/modules/SPEC_<MODULO>.md §<seção_relevante>
7. specs/plans/PLAN_<MODULO>.md §"Fase <X>"
8. specs/plans/TASKS_<MODULO>.md §"Fase <X>" (T-<X>1..T-<X>N)
9. .agent/skills/<dominio>/SKILL.md (skills relevantes para esta fase, se existirem)

ESTADO ATUAL (verificar antes de codar):
- Workspace : <caminho local>
- Branch    : main em <COMMIT_HASH>
- Repo      : github.com/<user>/<repo>
- Testes    : <N>/<N> passing — manter
- Release/alvo validado : <REV ou referencia equivalente>
- Toolchain : git, <runtime>, <pacote-mgr>, validadores relevantes

GATES JÁ APROVADOS (não revisar):
- GATE 1 (PLAN) aprovado em <DATA>
- GATE 2 (TASKS) aprovado em <DATA>
- ADRs aceitos: ADR-NNN, ADR-MMM
- Fases concluídas: A, B (esta sessão é fase C)

PRÓXIMA TAREFA: T-<X>1 — <descrição> conforme SPEC §<sec>.
AC esperado: <critério verificável>

REGRAS NÃO-NEGOCIÁVEIS (extraídas de AGENTS.md):
- <regra absoluta 1: ex.: AsyncClient para I/O>
- <regra absoluta 2: ex.: Sem log de conteúdo de mensagens>
- <regra absoluta 3: ex.: PR ≤250 LOC>
- Conventional Commits
- Backward-compat por tarefa
- Sem commit/push sem aprovação humana
- Tarefas [bloq.] em TASKS são gates humanos (G3, G4)

PROCEDA:
1. Leitura completa dos arquivos acima
2. Confirme entendimento em 1 parágrafo
3. Mostre plano de execução de T-<X>1 com checkboxes:
   - [ ] Edição do arquivo Y
   - [ ] Teste local Z
   - [ ] Lint/typecheck
   - [ ] Atualizar o status da tarefa no artefato ou tracking adotado
4. AGUARDE meu GO antes de iniciar a primeira edição.

NÃO escreva código nesta resposta. Só leia, planeje, mostre.
```

---

## Como preencher os placeholders

| Placeholder | Onde encontrar |
|---|---|
| `<PROJETO>` | Nome em `AGENTS.md` §"Identidade" |
| `<MODULO>` | Nome do módulo atual (ex.: AUTH, SESSIONS) |
| `<X>`, `<X-1>` | Número da fase (A=1, B=2, C=3...). Letras nas TASKS |
| `<DATA>` | Data do último handover, formato YYYY-MM-DD |
| `<COMMIT_HASH>` | `git log -1 --format=%h` (7 chars) |
| `<REV>` | Revisao, build, release ou referencia ativa equivalente |
| `<runtime>`, `<pacote-mgr>` | Python 3.11 + pip; Node 20 + npm; etc. |
| `<dominio>` | Nome da pasta em `.agent/skills/<dominio>/` |
| `<descrição>`, `<AC esperado>` | Da linha T-X1 em `specs/plans/TASKS_<MODULO>.md` |
| `<regra absoluta N>` | Da §"Regras Absolutas" do AGENTS.md |

---

## Checklist do humano antes de colar este prompt

- [ ] Handover anterior existe e está atualizado?
- [ ] Branch correta (main em commit verde)?
- [ ] Testes passando localmente?
- [ ] Recursos cloud provisionados (não falta DB / secret novo)?
- [ ] Nada pendente no SPEC_INDEX que bloqueia esta fase?
- [ ] Você tem ~1-2h disponíveis (multi-fase exige foco contínuo)?

Se algum item falhar, **NÃO retome** ainda. Resolva primeiro ou pause.
