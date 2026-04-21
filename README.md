# sdd-starter

> Template de **Spec-Driven Development** com agentes de IA — IDE-agnóstico,
> stack-agnóstico, pronto para greenfield ou brownfield.

Funciona em Cursor, Google Antigravity, Jules, Gemini CLI, Claude Code, Cline,
Aider — qualquer agente que respeite o padrão `AGENTS.md`.

---

## Por que SDD?

Ciclo de desenvolvimento com **agentes de IA** sem método vira:
- Código gerado sem rastreabilidade (semana 2: ninguém sabe por que aquela função existe).
- Decisões arquiteturais perdidas (sessão 5: o agente reabre debate já fechado).
- Regressão silenciosa (mudança de prompt quebra UX sem quebrar testes).
- Onboarding lento (dev novo perde 2 dias só entendendo o estado atual).

**SDD resolve isso com 6 princípios não-negociáveis:**

| Princípio | Significa |
|---|---|
| **Spec-first** | Nenhum código de produção sem spec aprovada por humano |
| **Gates humanos** | 4 pontos de aprovação obrigatórios (PLAN, TASKS, SMOKE, COMMIT) |
| **Fonte primária** | Toda decisão técnica registra URL verificável |
| **Backward-compat** | Cada commit preserva o estado funcional anterior |
| **Rastreabilidade** | Código → Tarefa → SPEC → ADR (cadeia auditável) |
| **Reversibilidade** | Cada fase é revertível com `git revert` sem cascata |

E **9 fases ordenadas** com critérios objetivos: SPECIFY → CLARIFY → ADRs → PLAN → TASKS → IMPLEMENT → TEST → DEPLOY+SMOKE → COMMIT → HANDOVER.

Detalhes em [`docs/SDD_WORKFLOW.md`](docs/SDD_WORKFLOW.md) (a peça central).

---

## Como começar

Existem **3 modos** de adoção. Escolha pelo seu cenário:

### Modo 1 — Projeto novo (greenfield)

```bash
gh repo create meu_projeto --template thesasx/sdd-starter --private
cd meu_projeto
# Edite PROJECT_BRIEF.md (5-10 min)
```

No seu IDE com agente, cole o conteúdo de [`prompts/BOOTSTRAP.md`](prompts/BOOTSTRAP.md). O agente:
- Lê seu `PROJECT_BRIEF.md`
- Adapta `AGENTS.md` à sua stack
- Cria `SPEC_INDEX.md` com módulos propostos
- Para no GATE 1 (aguarda você aprovar o PLAN do primeiro módulo)

Guia completo: [`QUICKSTART/greenfield.md`](QUICKSTART/greenfield.md).

### Modo 2 — Projeto existente sem documentação (brownfield)

Cenário típico: você entrou em projeto numa empresa, **não há docs, specs, ADRs, nada**. Você não conhece o domínio do código.

```bash
# 1. Copie 5 arquivos do template para seu projeto:
#    AGENTS.md, GEMINI.md (opcional), .agent/agents.md,
#    docs/SDD_WORKFLOW.md, prompts/DISCOVER.md
```

No seu IDE, cole [`prompts/DISCOVER.md`](prompts/DISCOVER.md). O agente faz **reverse engineering documentation** em 5 etapas, **parando para sua aprovação a cada uma**:

1. Reconhecimento (estrutura, stack, infra detectados)
2. Análise de domínio (lê configs/entry points, infere arquitetura)
3. Mapeamento SDD retrospectivo (propõe SPECs e ADRs com base no código)
4. Geração dos artefatos aprovados
5. Pronto pra trabalhar (próxima task usa NEW_FEATURE/BUG_FIX/REFACTOR)

Guia completo: [`QUICKSTART/brownfield.md`](QUICKSTART/brownfield.md).

### Modo 3 — Projeto que já usa SDD (sessão nova de outro dev)

```bash
git clone <repo> && cd <repo>
```

Cole [`prompts/ONBOARDING.md`](prompts/ONBOARDING.md). O agente lê AGENTS.md + último handover + SPEC_INDEX e te resume o estado em 2 minutos.

---

## Estrutura do template

```text
sdd-starter/
├── AGENTS.md                    ← constituição cross-tool (com placeholders)
├── GEMINI.md                    ← overrides Antigravity (opcional)
├── README.md                    ← este arquivo
├── PROJECT_BRIEF.md             ← escopo do projeto (você preenche)
├── LICENSE
│
├── prompts/                     ← prompts copy-paste prontos
│   ├── BOOTSTRAP.md             ← projeto novo (você tem brief)
│   ├── DISCOVER.md              ← projeto sem docs (agente descobre)
│   ├── ONBOARDING.md            ← sessão nova num projeto SDD
│   ├── RESUME.md                ← retomar fase intermediária
│   ├── HANDOVER.md              ← encerrar sessão
│   ├── NEW_FEATURE.md           ← próxima feature seguindo SDD
│   ├── BUG_FIX.md               ← bug fix com rastreabilidade
│   └── REFACTOR.md              ← refator sob ADR de migração
│
├── QUICKSTART/                  ← 1 página por modo de uso
│   ├── greenfield.md
│   ├── brownfield.md
│   ├── bug-fix.md
│   ├── small-feature.md
│   ├── medium-feature.md
│   ├── large-feature.md
│   └── refactor.md
│
├── .agent/                      ← config IDE-agnóstica
│   ├── agents.md                ← 4 personas (@pm, @engineer, @qa, @devops)
│   ├── skills/_example_skill/   ← exemplo de SKILL.md
│   └── workflows/               ← sdd_implement, sdd_bootstrap, sdd_discover
│
├── specs/
│   ├── SPEC_INDEX.md            ← esqueleto vazio
│   ├── modules/_SPEC_TEMPLATE.md
│   ├── plans/_PLAN_TEMPLATE.md
│   ├── plans/_TASKS_TEMPLATE.md
│   └── decisions/_ADR_TEMPLATE.md
│
├── docs/
│   ├── SDD_WORKFLOW.md          ← framework canônico
│   ├── _ARCHITECTURE_TEMPLATE.md
│   └── _HANDOVER_TEMPLATE.md
│
├── tests/{unit,integration,smoke}/.gitkeep
├── scripts/{.gitkeep, README.md}
│
├── .cursor/rules/sdd.mdc        ← regra Cursor (agente segue SDD por default)
├── .cursor/rules/sdd-bootstrap.mdc
│
├── .gitignore
├── .gcloudignore                ← opcional, com header
├── .dockerignore                ← opcional, com header
└── .env.example
```

---

## Os 4 GATEs humanos

| GATE | Quando | Quem aprova |
|---|---|---|
| **G1 — PLAN** | Após PLAN gerado, antes de TASKS | Dono do produto / arquiteto |
| **G2 — TASKS** | Após TASKS, antes de IMPLEMENT | Dono do produto / dev sênior |
| **G3 — SMOKE** | Após DEPLOY staging, antes de COMMIT final | Dono do produto (smoke real) |
| **G4 — COMMIT** | Antes de `git push` para `main` | Dev (revisar diff) |

Auto-continue dos IDEs **respeita** os gates via marcação `[bloq.]` em TASKS.

---

## Modos de uso → artefatos obrigatórios

Nem toda task precisa do ciclo SDD completo. Use a tabela como guia:

| Modo de uso | SPEC | ADR | PLAN | TASKS | Handover | GATEs ativos |
|---|---|---|---|---|---|---|
| Bug fix simples | Não | Só se decisão | Não | Não | Opcional | G3, G4 |
| Feature pequena (≤100 LOC) | Estende existente | Se trade-off | Não | Sim (1 fase) | Sim | G2, G3, G4 |
| Feature média (100-400 LOC) | Sim | Provável | Sim | Sim | Sim | Todos os 4 |
| Feature grande (>400 LOC) | Sim | Múltiplas | Sim, multi-fase | Sim, por fase | Por fase | Todos por fase |
| Refator interno (sem mudança contratual) | Não | Sim (justifica) | Não | Sim (curto) | Sim | G3, G4 |
| Refator arquitetural | Sim ("v2") | Sim (migração) | Sim, multi-fase | Sim | Por fase | Todos por fase |
| Greenfield (projeto novo) | Sim, todas | Várias | Sim por módulo | Sim por módulo | Sim por módulo | Todos |
| Brownfield (entrar em projeto) | Adoção gradual via DISCOVER | — | — | — | — | Adapta-se |

QUICKSTART por modo está em [`QUICKSTART/`](QUICKSTART/).

---

## Adaptação a outras stacks

O framework é **stack-agnóstico**. Os exemplos no template usam Python+FastAPI+GCP por familiaridade, mas funciona com:

- **Python**: FastAPI, Django, Flask, etc.
- **Node**: Express, Fastify, NestJS, Next.js, etc.
- **Go**: net/http, Gin, Fiber, etc.
- **Rust**: Axum, Actix, etc.
- **Java/Kotlin**: Spring Boot, Ktor, etc.
- **Infra**: GCP, AWS, Azure, on-prem, serverless, k8s, ECS, Cloud Run, Lambda.

Adaptar = preencher placeholders `<!-- ADAPT -->` em `AGENTS.md` + criar SKILLs em `.agent/skills/<dominio>/SKILL.md` para regras específicas da sua stack.

Detalhes na §"Adaptação a outras stacks" do [`docs/SDD_WORKFLOW.md`](docs/SDD_WORKFLOW.md).

---

## Regras Cursor (.cursor/rules/)

Se você usa Cursor, o template inclui 2 rules opcionais:

- `.cursor/rules/sdd.mdc` — agente segue SDD por padrão em qualquer task
- `.cursor/rules/sdd-bootstrap.mdc` — detecta projeto sem `AGENTS.md` mas com `PROJECT_BRIEF.md` → sugere `prompts/BOOTSTRAP.md`

Cursor lê automaticamente. Outros IDEs ignoram.

---

## Origem

Este framework foi destilado de um projeto real (`prototype-alfred`) onde o ciclo SDD foi aplicado por ~3 meses, gerando 14 ADRs aceitos, 12 handovers e MVP funcional sem perda de controle. Lições reais estão marcadas como `📚 LIÇÃO` ao longo do `SDD_WORKFLOW.md`.

---

## Contribuir

Issues e PRs são bem-vindos. Antes de propor mudança ao framework:

1. Verifique se sua sugestão é **stack-agnóstica** (não específica a uma linguagem).
2. Se introduz nova regra absoluta, abra ADR no `specs/decisions/` deste próprio repo.
3. PR ≤250 LOC. Convencional commits.

---

## Licença

MIT — ver [`LICENSE`](LICENSE).
