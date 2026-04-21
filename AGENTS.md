<!--
═══════════════════════════════════════════════════════════════════════════════
  AGENTS.md — Constituição cross-tool do projeto
═══════════════════════════════════════════════════════════════════════════════

  Lido por: Cursor, Google Antigravity (v1.20.3+), Jules, Gemini CLI, Claude Code,
            Cline, Aider e qualquer agente que respeite o padrão AGENTS.md.

  Hierarquia de leitura: GEMINI.md (se Antigravity) → AGENTS.md (este) → .agent/

  Como adaptar este template:
    1. Procure por <!-- ADAPT --> e preencha conforme seu projeto.
    2. Apague seções marcadas como [OPCIONAL] que não se aplicam.
    3. Mantenha as 6 regras absolutas universais; some regras específicas da stack.

  Fonte SDD: docs/SDD_WORKFLOW.md (este repo)
═══════════════════════════════════════════════════════════════════════════════
-->

# AGENTS.md — Constituição do <!-- ADAPT: NOME_DO_PROJETO -->

---

## Identidade do Projeto

- **Nome:** <!-- ADAPT: nome do projeto -->
- **Objetivo:** <!-- ADAPT: 1-2 frases descrevendo o que o projeto faz e para quem -->
- **Estágio:** <!-- ADAPT: Greenfield | MVP | Beta | Produção -->
- **IDE primária:** <!-- ADAPT: Cursor | Antigravity | Jules | Gemini CLI | Claude Code -->
- **Metodologia:** Spec-Driven Development (SDD) — ver `docs/SDD_WORKFLOW.md`
- **Arquitetura base:** `docs/<!-- ADAPT: NOME_PROJETO -->_Architecture.md`

---

## Regras Absolutas Universais (válidas em qualquer projeto SDD)

> Estas 6 regras são **invariantes** do framework SDD. Não as remova.
> Conflito entre instrução e regra absoluta = registrar ADR e respeitar a regra.

### 1. Ciclo SDD Obrigatório

Nenhum código de produção é gerado sem spec aprovada por humano.
Sequência obrigatória:

```
SPECIFY → CLARIFY → (ADRs?) → PLAN → [GATE 1] → TASKS → [GATE 2] →
IMPLEMENT → TEST → DEPLOY → SMOKE → [GATE 3] → COMMIT → [GATE 4] → HANDOVER
```

- 4 gates humanos obrigatórios (PLAN, TASKS, SMOKE, COMMIT) — ver `docs/SDD_WORKFLOW.md` §1.
- Qualquer mudança de requisito reinicia o ciclo a partir de SPECIFY.
- Bug fix simples e refator interno têm versão enxuta — ver tabela "Modos de uso" no SDD_WORKFLOW.

### 2. Toda Decisão Técnica Requer URL de Fonte Primária

- Sem URL verificável = decisão bloqueada.
- Registrar trade-off em `specs/decisions/ADR-NNN-<slug>.md`.
- Nunca usar "best practice" como justificativa sem URL específica.
- Nunca reutilizar número de ADR (mesmo se rejeitada).

### 3. Privacidade e Logging

- **Sem conteúdo sensível em logs.** Definição de "sensível" vai abaixo (regra adaptável).
- Logar apenas metadados necessários para debug e operação.
- Conteúdo de usuário em banco de dados é decisão arquitetural — registrar em ADR se aplicável.

<!-- ADAPT: liste o que é "sensível" no SEU projeto. Exemplos:
       - PII de usuário
       - PHI (saúde — HIPAA)
       - Dados financeiros (PCI-DSS)
       - Conteúdo de mensagem (LGPD/GDPR)
     E cite a fonte regulatória. -->

### 4. Sem Hardcode de Credenciais

- API keys, tokens, senhas, connection strings → variáveis de ambiente ou secret manager.
- `.env` no `.gitignore`. Nunca commitar.
- Em produção: usar gerenciador de segredos (Secret Manager / Vault / AWS Secrets Manager / etc).

### 5. Backward-Compatibility por Commit

- Cada commit em `main` preserva o estado funcional anterior.
- Multi-fase: `revert` da fase X não derruba fase X-1.
- Quebra contratual = ADR de migração + plano de rollback.

### 6. Rastreabilidade

- Cada arquivo de código rastreia para uma TASK em `specs/plans/TASKS_*.md`.
- Cada TASK rastreia para uma SPEC em `specs/modules/SPEC_*.md`.
- Cada decisão arquitetural rastreia para uma ADR em `specs/decisions/`.
- Handover de cada sessão em `docs/handover_*_<DATA>.md`.

---

## Regras Absolutas Específicas do Projeto

<!-- ADAPT: regras que dependem da sua stack/domínio. Exemplos comuns:

### Versões fixadas (não atualizar sem processo)

| Dependência | Versão | Fonte |
|---|---|---|
| <runtime> | <versão> | <URL docs oficial> |
| <framework> | <versão> | <URL> |

### Stack-specific

- Async client obrigatório para I/O em rotas async (se usar FastAPI/Express async)
- Estratégia de cache definida em ADR-XXX
- Pattern de error handling: ...

### Compliance

- Região de dados: <região> (motivo regulatório)
- Auditoria de acesso obrigatória em <coleção/tabela>
- Retenção de logs: <período> (motivo)

### Segurança aplicacional

- Inputs externos passam por validação antes de processamento
- Toda chamada externa em try/except com tratamento de erro
- Rate limiting em endpoints públicos
-->

---

## Stack Técnica

<!-- ADAPT: tabela com versões fixadas. Exemplo:

| Camada | Tecnologia | Versão | Fonte |
|---|---|---|---|
| Linguagem | Python | 3.11.x | https://docs.python.org/3.11/ |
| Framework web | FastAPI | >=0.115.0 | https://fastapi.tiangolo.com |
| Banco | PostgreSQL | 16.x | https://www.postgresql.org/docs/16/ |
| Infra | <provider> | - | <url> |
-->

---

## Estrutura de Diretórios

```text
<!-- ADAPT: ajuste à sua stack -->
projeto/
├── AGENTS.md                ← este arquivo (constituição)
├── GEMINI.md                ← overrides Antigravity (apague se não usar)
├── README.md                ← onboarding humano
├── PROJECT_BRIEF.md         ← escopo do projeto (input do BOOTSTRAP/DISCOVER)
├── .agent/                  ← config IDE-agnóstica
│   ├── agents.md            ← personas (@pm, @engineer, @qa, @devops)
│   ├── skills/              ← SKILL.md por domínio técnico
│   └── workflows/           ← workflows SDD reutilizáveis
├── prompts/                 ← prompts copy-paste (BOOTSTRAP, DISCOVER, RESUME, etc.)
├── specs/
│   ├── SPEC_INDEX.md        ← índice + status de cada módulo
│   ├── modules/SPEC_<N>.md
│   ├── plans/PLAN_<N>.md
│   ├── plans/TASKS_<N>.md
│   └── decisions/ADR-NNN-*.md
├── docs/
│   ├── SDD_WORKFLOW.md      ← framework canônico (não editar sem motivo)
│   ├── <Project>_Architecture.md
│   └── handover_*_<DATA>.md
├── app/ | src/              ← código de produção
├── tests/{unit,integration,smoke}/
├── scripts/                 ← deploy, setup, smoke
├── QUICKSTART/              ← guias rápidos por modo de uso
├── .gitignore
├── .env.example
└── <Dockerfile | package.json | requirements.txt | go.mod>
```

---

## Regras por IDE / Ferramenta

### Cursor

- Modes: **Plan** (ambiguidade/design) | **Agent** (execução clara) | **Ask** (só investigar) | **Debug** (bug investigation).
- Rule global do framework: `.cursor/rules/sdd.mdc` (instala junto do template).
- Auto-continue ativo, **mas** GATEs humanos respeitados via `[bloq.]` em TASKS.
- Workspace fora de cloud-sync (Drive/OneDrive/Dropbox) — ver §"Lições" do SDD_WORKFLOW.

### Google Antigravity (v1.20.3+)

- Lê `GEMINI.md` antes de `AGENTS.md` (precedência em conflitos).
- Planning Mode obrigatório para qualquer IMPLEMENT.
- Implementation Plan + Task List como **artifacts** antes de código.
- Settings → Agent → Load nested AGENTS.md = **ativo**.
- Auto-continue ativo (default v1.20.3+), mas GATEs humanos respeitados.
- Fonte: https://discuss.ai.google.dev/t/antigravity-update-1-20-3-2026-3-5/129320

### Jules (jules.google.com)

- Lê `AGENTS.md` automaticamente ao clonar.
- Acionado **apenas** na fase IMPLEMENT, nunca em SPECIFY/PLAN.
- `@jules approve` antes de qualquer commit; `@jules cancel` reinicia ciclo.
- Fonte: https://jules.google/docs/

### Gemini CLI

- Usa `~/.gemini/GEMINI.md` como config global. **Conflito conhecido** com Antigravity:
  workaround é separar regras em `~/.gemini/AGENTS.md` (compartilhado) e
  `~/.gemini/GEMINI.md` (overrides por ferramenta).
- Uso recomendado: scripts, análise de logs, queries pontuais. Nunca implementação sem spec.

### Claude Code / Cline / Aider

- Lê `AGENTS.md` por padrão na maioria dos casos.
- Para gates explícitos: configure no prompt de retomada (ver `prompts/RESUME.md`).

---

## Fluxo SDD — Resumo Operacional

```
SPECIFY  → criar/atualizar specs/modules/SPEC_<MODULO>.md
CLARIFY  → agente faz perguntas; respostas documentadas em §10 da spec
ADR?     → se trade-off arquitetural: criar specs/decisions/ADR-NNN-*.md
PLAN     → specs/plans/PLAN_<MODULO>.md (artefato, sem código ainda)
[GATE 1] → humano aprova PLAN
TASKS    → specs/plans/TASKS_<MODULO>.md (atômicas, com AC)
[GATE 2] → humano aprova TASKS
IMPLEMENT→ código gerado tarefa-por-tarefa, AC verificado a cada uma
TEST     → pytest -q (ou equivalente) verde, sem regressão
DEPLOY   → staging
SMOKE    → 2-3 fluxos críticos manualmente
[GATE 3] → humano aprova SMOKE
COMMIT   → conventional commits, ≤250 LOC por PR
[GATE 4] → humano revisa diff antes de push
HANDOVER → docs/handover_<MODULO>_<DATA>.md + SPEC_INDEX atualizado
```

Detalhes completos: `docs/SDD_WORKFLOW.md`.

---

## Módulos do Projeto

<!-- ADAPT: lista atualizada conforme SPEC_INDEX.md. Exemplo:

| Módulo | Spec | Status |
|---|---|---|
| Auth | `specs/modules/SPEC_AUTH.md` | ✔️ |
| Sessions | `specs/modules/SPEC_SESSIONS.md` | 🚧 |
-->

Fonte canônica: `specs/SPEC_INDEX.md`.

---

## Decisões Arquiteturais (ADRs)

<!-- ADAPT: lista atualizada. Sincronizar com specs/SPEC_INDEX.md. Exemplo:

| ID | Decisão | Arquivo | Status |
|---|---|---|---|
| ADR-001 | Escolha de DB | `specs/decisions/ADR-001-db-choice.md` | ✔️ |
-->

---

## Guardrails de Segurança (universais)

- **Nunca** commitar `.env`, `.env.local`, `*.key`, `service-account*.json`, `credentials*.json`.
- **Nunca** hardcodar credenciais, API keys, tokens, connection strings.
- **Nunca** fazer deploy em produção sem aprovação humana explícita.
- **Nunca** logar conteúdo sensível (definido na §"Regras Absolutas").
- **Nunca** force-push em `main`.
- Todos os inputs externos passam por validação antes de processamento.
- Toda chamada externa em `try/except` com tratamento de erro tipado.

---

## Qualidade de Código

| Regra | Limite | Por quê |
|---|---|---|
| Tamanho de arquivo | ≤300 linhas | Forçar separação de responsabilidades |
| Tamanho de função | ≤30 linhas | Forçar nomes claros + composição |
| `print()` em produção | Zero | Logger estruturado obrigatório |
| Type hints (Python) / Types (TS) | 100% em funções públicas | Catch errors no lint |
| Docstrings em exportadas | Sim | Onboarding + IDE intellisense |
| Comentários redundantes | Zero | Comentários explicam *por quê*, não *o quê* |

---

## Convenções Git

- **Conventional Commits**: `feat:`, `fix:`, `docs:`, `refactor:`, `test:`, `chore:`, `perf:`, `revert:`
- **Título**: ≤72 chars, imperativo ("add", não "added").
- **Tamanho de PR**: ≤250 LOC para `feat`, ≤100 para `fix`, ≤200 para `refactor`.
- **Branch naming**: `feat/<slug>`, `fix/<slug>`, `refactor/<slug>`, `chore/<slug>`.
- **Nunca**: force-push em `main`, merge sem revisão (auto-ou-humana).

---

## O Que Este Projeto NÃO Faz (escopo fora do MVP)

<!-- ADAPT: lista explícita do que está fora. Exemplo:

- ❌ Não suporta multi-tenant (single-user only)
- ❌ Não tem mobile app (web only)
- ❌ Não integra <ferramenta>
-->

---

## Rastreabilidade

- Cada decisão técnica rastreia para uma ADR em `specs/decisions/`.
- Cada feature rastreia para uma SPEC em `specs/modules/`.
- Cada implementação rastreia para uma TASK em `specs/plans/TASKS_*.md`.
- Cada sessão de trabalho deixa um handover em `docs/handover_*.md`.

---

*Versão deste AGENTS.md: 1.0 — Manter sincronizado com `specs/SPEC_INDEX.md` e `docs/SDD_WORKFLOW.md`.*
