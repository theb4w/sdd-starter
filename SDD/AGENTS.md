<!--
═══════════════════════════════════════════════════════════════════════════════
  AGENTS.md — Constituição cross-tool do projeto
═══════════════════════════════════════════════════════════════════════════════

  Use este arquivo para orientar agentes que participam do projeto.
  O workflow canônico do método fica em .agent/skills/sdd-mode/references/workflow.md.

  Como adaptar este template:
    1. Procure por <!-- ADAPT --> e preencha conforme seu projeto.
    2. Apague seções marcadas como [OPCIONAL] que não se aplicam.
    3. Mantenha as 6 regras absolutas universais; some regras específicas da stack.

  Fonte SDD: .agent/skills/sdd-mode/references/workflow.md (este repo)
═══════════════════════════════════════════════════════════════════════════════
-->

# AGENTS.md — Constituição do sdd-starter

---

## Identidade do Projeto

- **Nome:** sdd-starter
- **Objetivo:** Skill pack SDD: `sdd-mode` gera `SDD/` e executa playbooks.
- **Estágio:** MVP
- **Metodologia:** Spec-Driven Development — `.agent/skills/sdd-mode/references/workflow.md`
- **Arquitetura base:** pasta `SDD/` gerada; skill em `.agent/skills/sdd-mode/`

---

## Regras Absolutas Universais (válidas em qualquer projeto SDD)

> Estas 6 regras são **invariantes** do framework SDD. Não as remova.
> Conflito entre instrução e regra absoluta = registrar ADR e respeitar a regra.

### 1. Ciclo SDD Obrigatório

Nenhum código de produção é gerado sem o contrato do playbook (SPEC, user story
ligada a SPEC de módulo, ou nenhum contrato novo em bug-fix).
Sequência completa (perfil `full`):

```
SPECIFY → CLARIFY → (ADRs?) → PLAN → [GATE 1] → TASKS → [GATE 2] →
IMPLEMENT → TEST → DEPLOY → SMOKE → [GATE 3] → COMMIT → [GATE 4] → HANDOVER
```

- Gates humanos nomeados (PLAN, TASKS, SMOKE, COMMIT). Quais disparam é o **perfil** do playbook (`observe` / `design` / `lite` / `standard` / `full`) — ver `.agent/skills/sdd-mode/references/workflow.md` §1.3 e ADR-002.
- Qualquer mudança de requisito reinicia o ciclo a partir de SPECIFY.
- Bug fix simples e refator interno têm versão enxuta — ver tabela "Modos de uso" no SDD_WORKFLOW.

### 2. Toda Decisão Técnica Requer URL de Fonte Primária

- Sem URL verificável = decisão bloqueada.
- Registrar trade-off em `SDD/decisions/ADR-NNN-<slug>.md`.
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

- Cada arquivo de código rastreia para uma TASK em `SDD/plans/TASKS_*.md`.
- Cada TASK rastreia para uma SPEC em `SDD/modules/SPEC_*.md`.
- Cada decisão arquitetural rastreia para uma ADR em `SDD/decisions/`.
- Handover de cada sessão em `SDD/handovers/handover_*_<DATA>.md`.

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
<!-- ADAPT: ajuste à sua stack de produto -->
projeto/
├── README.md
├── .agent/skills/sdd-mode/   ← procedimento (esta skill)
├── SDD/                      ← processo gerado (brief, specs, ADRs, handovers)
├── app/ | src/
├── .gitignore
└── <manifest da stack>
```

---

## Ambiente de Trabalho e Ferramentas

O fluxo SDD deste projeto deve continuar valido se a equipe trocar de editor,
agente, terminal, provider ou modelo.

- Antes de agir, ler os artefatos SDD relevantes e resumir o estado atual.
- Tarefas de agente: invocar `.agent/skills/sdd-mode/SKILL.md` e copiar o playbook.
- Representar planejamento e tarefas em arquivos revisaveis do repo, mesmo que
  a ferramenta mantenha uma lista interna auxiliar.
- Respeitar gates humanos ainda que a ferramenta tenha execucao automatica,
  auto-continue ou modo autonomo. Perfil mais leve so com reclassificacao explicita.
- Tratar configuracoes de ferramenta como opcionais. Nao substituem `SDD/`.

---

## Fluxo SDD — Resumo Operacional

```
SPECIFY  → criar/atualizar SDD/modules/SPEC_<MODULO>.md
CLARIFY  → agente faz perguntas; respostas documentadas em §10 da spec
ADR?     → se trade-off arquitetural: criar SDD/decisions/ADR-NNN-*.md
PLAN     → SDD/plans/PLAN_<MODULO>.md (artefato, sem código ainda)
[GATE 1] → humano aprova PLAN
TASKS    → SDD/plans/TASKS_<MODULO>.md (atômicas, com AC)
[GATE 2] → humano aprova TASKS
IMPLEMENT→ código gerado tarefa-por-tarefa, AC verificado a cada uma
TEST     → validação apropriada ao projeto, sem regressão conhecida
RELEASE  → deploy, build, preview ou ambiente-alvo aplicável
SMOKE    → fluxos críticos do produto validados
[GATE 3] → humano aprova SMOKE
COMMIT   → conventional commits, ≤250 LOC por PR
[GATE 4] → humano revisa diff antes de push
HANDOVER → SDD/handovers/handover_<MODULO>_<DATA>.md + SDD/INDEX.md atualizado
```

Detalhes completos: `.agent/skills/sdd-mode/references/workflow.md`.

---

## Módulos do Projeto

<!-- ADAPT: lista atualizada conforme SPEC_INDEX.md. Exemplo:

| Módulo | Spec | Status |
|---|---|---|
| Auth | `SDD/modules/SPEC_AUTH.md` | ✔️ |
| Sessions | `SDD/modules/SPEC_SESSIONS.md` | 🚧 |
-->

Fonte canônica: `SDD/INDEX.md`.

---

## Decisões Arquiteturais (ADRs)

<!-- ADAPT: lista atualizada. Sincronizar com SDD/INDEX.md. Exemplo:

| ID | Decisão | Arquivo | Status |
|---|---|---|---|
| ADR-001 | Escolha de DB | `SDD/decisions/ADR-001-db-choice.md` | ✔️ |
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
| Saidas de debug em producao | Zero | Telemetria e logs seguem politica do projeto |
| Contratos/tipos publicos | Conforme stack | Evitar comportamento implicito em interfaces relevantes |
| Documentacao de APIs/exportadas | Conforme projeto | Facilitar onboarding e manutencao |
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

- Cada decisão técnica rastreia para uma ADR em `SDD/decisions/`.
- Cada feature rastreia para uma SPEC em `SDD/modules/`.
- Cada implementação rastreia para uma TASK em `SDD/plans/TASKS_*.md`.
- Cada sessão de trabalho deixa um handover em `SDD/handovers/handover_*.md`.

---

*Versão deste AGENTS.md: 1.0 — Manter sincronizado com `SDD/INDEX.md` e `.agent/skills/sdd-mode/references/workflow.md`.*
