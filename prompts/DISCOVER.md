<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/DISCOVER.md — Reverse Engineering Documentation
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO: você entrou em um projeto existente que NÃO TEM documentação,
  specs, ADRs ou contexto. Você precisa que o agente EXPLORE o código,
  INFIRA o que o projeto faz, e PROPONHA documentação SDD retrospectiva.

  COMO USAR:
  1. Cole TODO o conteúdo abaixo no chat do agente (Cursor / Antigravity / etc.)
  2. Substitua <PROJETO> pelo nome do projeto
  3. O agente vai parar a CADA etapa esperando seu GO humano
  4. Não pula etapas. Não escreve código. Só explora e propõe.

  RESULTADO ESPERADO: ao fim das 5 etapas, o projeto terá:
  - PROJECT_BRIEF.md preenchido com o que foi inferido
  - docs/<Project>_Architecture.md como rascunho
  - specs/SPEC_INDEX.md catalogando módulos detectados
  - SPECs individuais com status retrospectivo (✔️/🚧/❌)
  - ADRs candidatas para decisões implícitas no código
  - docs/handover_DISCOVERY_<DATA>.md registrando o estado inicial
  - AGENTS.md adaptado ao projeto

  TEMPO ESTIMADO: 30-90 min de trabalho colaborativo (5 etapas, gates humanos).
═══════════════════════════════════════════════════════════════════════════════
-->

# DISCOVER — Documentação Retrospectiva via SDD

**Projeto:** <PROJETO>
**Data:** <DATA_HOJE>
**Operador:** <SEU_NOME>

---

## Papel do agente

Você é um **arquiteto de software fazendo onboarding** em um projeto desconhecido.
Sua missão: produzir documentação SDD completa do projeto **antes** de qualquer
implementação de feature/fix.

## Restrições absolutas

- **NÃO ESCREVA CÓDIGO DE PRODUÇÃO.** Só leia.
- **NÃO MODIFIQUE NENHUM ARQUIVO EXISTENTE** do projeto.
- **NÃO ASSUMA NADA** sem evidência concreta no código.
- **PARE E AGUARDE GO HUMANO** ao fim de cada etapa.
- **PERGUNTE** quando inferir algo com baixa confiança. Marque como `[?]`.

## Pré-condições

Antes de começar, leia (nesta ordem):
1. `AGENTS.md` deste repo (constituição SDD)
2. `docs/SDD_WORKFLOW.md` (framework canônico)
3. `.agent/agents.md` (personas — ative @pm para esta missão)

Se algum dos arquivos acima não existir, é porque o template SDD ainda não foi
copiado. Pergunte ao usuário se ele copiou os 5 arquivos mínimos:
`AGENTS.md`, `docs/SDD_WORKFLOW.md`, `.agent/agents.md`, `prompts/DISCOVER.md`,
`PROJECT_BRIEF.md` (vazio).

---

## Etapa 1 — Reconhecimento (sem ler conteúdo de código)

**Objetivo:** mapear superficialmente o projeto sem assumir nada.

**O que fazer:**

1. Liste a estrutura completa de pastas (depth 3) — exclua `.git/`, `node_modules/`, `.venv/`, `dist/`, `build/`.
2. Identifique linguagens principais (por extensão de arquivo + contagem).
3. Identifique gerenciadores de dependência presentes (`requirements.txt`, `package.json`, `go.mod`, `Cargo.toml`, `pom.xml`, `Gemfile`, etc.) — apenas LISTAR, não ler conteúdo ainda.
4. Identifique configs de infra (`Dockerfile`, `docker-compose.yml`, `.gcloudignore`, `terraform/`, `k8s/`, `serverless.yml`, etc.).
5. Verifique presença de CI (`.github/workflows/`, `.gitlab-ci.yml`, `.circleci/`, `Jenkinsfile`).
6. Identifique convenção de testes pela presença de pastas (`tests/`, `__tests__/`, `*_test.go`, `*.spec.ts`).
7. Verifique se há documentação prévia (`README.md`, `docs/`, `wiki/`, `*.md` na raiz).

**Output esperado (responda exatamente neste formato):**

```markdown
## Etapa 1 — Reconhecimento

### Estrutura de pastas (depth 3)
<árvore de pastas>

### Linguagens detectadas
| Linguagem | # arquivos | % aproximado |
|---|---|---|
| ... | ... | ... |

### Gerenciadores de dependência
- <arquivo> presente? → sim/não

### Infra
- Dockerfile? → sim/não
- docker-compose? → sim/não
- IaC (Terraform/Pulumi/etc.)? → sim/não
- Configs cloud (.gcloudignore, etc.)? → sim/não

### CI/CD
- <arquivo de CI>? → sim/não

### Testes
- Pasta de testes? → sim/não, onde
- Convenção aparente? → ex.: pytest / jest / go test

### Documentação pré-existente
- README.md? → sim/não, tamanho aproximado
- docs/? → sim/não, # arquivos
- Outros .md na raiz? → lista
```

**No fim de Etapa 1, escreva:**

```
🛑 ETAPA 1 COMPLETA — Aguardando seu GO humano.

Esse mapeamento bate com sua percepção do projeto?
- Confirme se quer prosseguir para Etapa 2 (Análise de domínio).
- Corrija se algo está errado.
```

**AGUARDE resposta humana antes de prosseguir.**

---

## Etapa 2 — Análise de domínio

**Objetivo:** entender O QUE o projeto faz, sua arquitetura geral, integrações.

**Pré-condição:** GO humano da Etapa 1.

**O que fazer:**

1. Leia `README.md` (se existir).
2. Leia o(s) arquivo(s) entry point (`main.py`, `index.js`, `app.py`, `cmd/main.go`, etc.).
3. Leia o gerenciador de dependências para identificar libs principais.
4. Leia configs principais (`Dockerfile`, `.env.example` se houver, configs de framework).
5. Mapeie módulos detectáveis: cada pasta-grande sob `src/`, `app/`, `lib/`, `internal/` é candidata a módulo. Liste com 1 linha de "responsabilidade aparente".
6. Identifique padrão arquitetural (MVC, Clean, Hexagonal, Microsserviços, Monolito, Layered).
7. Identifique integrações externas (APIs chamadas, services usados — procure por `httpx`, `fetch`, `axios`, SDK clients).
8. Identifique armazenamento (`firestore`, `postgres`, `mongo`, `s3`, `redis`, etc.).

**Output esperado:** rascunho de `PROJECT_BRIEF.md` com [?] em campos incertos.

```markdown
## Etapa 2 — Análise de domínio

### Rascunho de PROJECT_BRIEF.md (proposto)

# Project Brief — <PROJETO>

## 1. Objetivo (inferido do código)
<inferência baseada em README + entry point + nomes de módulos>
[?] Confirma esta interpretação?

## 2. Stack desejada (detectada)
| Camada | Tecnologia | Versão | Evidência |
|---|---|---|---|
| Linguagem backend | <X> | <V> | requirements.txt: linha N |
| Framework web | <Y> | <V> | imports em main.py |
| Banco | <Z> | — | client em app/db.py |
| ... | ... | ... | ... |

## 3. Restrições (inferidas)
[?] Orçamento mensal: NÃO INFERÍVEL DO CÓDIGO — pergunta para você
[?] Compliance: detectei filtros LGPD em app/sanitize.py — confirma?
[?] Single/multi-tenant: parece single-tenant (vejo ALLOWED_UIDS=1) — confirma?

## 4. Módulos detectados
- **<MODULO_1>** (`<pasta>`): <responsabilidade aparente>
- **<MODULO_2>** (`<pasta>`): <responsabilidade aparente>
[?] Confirme nomes e responsabilidades

## 5. Fora do MVP
[?] NÃO INFERÍVEL — preciso que você liste

## 6. Métricas de sucesso
[?] NÃO INFERÍVEL — preciso que você liste

## 7. Estado atual (brownfield)
- Há código existente? Sim, em <pasta>, ~<X>k LOC
- Linguagem decidida? Sim: <X>
- Testes? <Y>% de cobertura aproximada (pasta tests/ tem N arquivos)
- Documentação? <descrição>
- [?] Última modificação relevante: pergunta para você
- [?] Pessoas com histórico: pergunta para você
- Ambientes? <descrição se detectável>
- Dependências externas críticas: <lista detectada>

## 8. Contexto adicional
[?] Pergunta para você
```

**No fim de Etapa 2, escreva:**

```
🛑 ETAPA 2 COMPLETA — Aguardando você preencher os [?]

Por favor:
1. Responda cada [?] no rascunho acima
2. Corrija interpretações erradas
3. Confirme prosseguir para Etapa 3 (Mapeamento SDD)
```

**AGUARDE respostas humanas. NÃO prossiga sem todos os [?] resolvidos.**

---

## Etapa 3 — Mapeamento SDD retrospectivo

**Objetivo:** propor SPECs e ADRs **com base no código existente** (sem
implementar nada novo).

**Pré-condição:** Brief completo (todos os [?] resolvidos).

**O que fazer:**

1. Para CADA módulo aprovado em Etapa 2:
   - Proponha SPEC retrospectiva (`SPEC_<MODULO>.md`).
   - Status sugerido: `✔️ CONCLUÍDO` se módulo funciona em produção; `🚧 IMPLEMENT` se incompleto; `❌ CANCELADO` se quebrado/abandonado.
   - Conteúdo mínimo: Objetivo (1 linha), Arquivos existentes, Endpoints/Funções públicas, Variáveis de ambiente que ele lê.
   - Marcar com `[?]` lacunas (testes? cobertura? compliance?).

2. Identifique **decisões importantes embutidas no código** que viraram ADRs implícitas:
   - Choice de DB? → ADR retrospectiva
   - Auth strategy? → ADR retrospectiva
   - Caching strategy? → ADR retrospectiva
   - Pattern arquitetural escolhido? → ADR retrospectiva
   - Provider cloud (vendor lock-in)? → ADR retrospectiva
   - Lang/runtime version? → ADR retrospectiva

3. Liste perguntas CLARIFY abertas por módulo (gaps que o código não responde).

**Output esperado:**

```markdown
## Etapa 3 — Mapeamento SDD retrospectivo

### Rascunho de SPEC_INDEX.md (proposto)

| Módulo | Spec | ADRs aplicáveis | Status sugerido |
|---|---|---|---|
| AUTH | SPEC_AUTH.md | ADR-001, ADR-002 | ✔️ CONCLUÍDO |
| ... | ... | ... | ... |

### SPECs propostas (1 esqueleto por módulo)

#### SPEC_AUTH.md
**Status sugerido:** ✔️ CONCLUÍDO (já em produção)
**Objetivo:** <inferido>
**Arquivos:**
- `app/auth/service.py` (250 LOC)
- `app/api/auth.py` (80 LOC)
**Variáveis de ambiente:** `OAUTH_CLIENT_ID`, `OAUTH_CLIENT_SECRET`
**[?] Cobertura de testes:** preciso confirmar (pasta tests/auth não existe)
**[?] Última modificação:** preciso confirmar

#### SPEC_<MODULO_2>.md
... (mesma estrutura)

### ADRs candidatas (decisões implícitas no código)

#### ADR-001 — Escolha de PostgreSQL como banco principal
**Contexto:** Detectado driver `psycopg2` em requirements.txt; tabelas modeladas
em `app/models/*.py`. Decisão tomada antes da minha entrada.
**Alternativas que aparentam ter sido consideradas:** [?] preciso saber
**Decisão:** PostgreSQL
**Rationale inferido:** <hipótese>
**Status sugerido:** ✔️ ACEITO (retrospectiva)

#### ADR-002 — <decisão detectada>
... (mesma estrutura)

### Perguntas CLARIFY abertas

**SPEC_AUTH:**
- Q1: TTL de sessão é 30 dias por design ou por default da lib?
- Q2: Há plano de migração para passwordless?

**SPEC_<MODULO_2>:**
- ...
```

**No fim de Etapa 3, escreva:**

```
🛑 ETAPA 3 COMPLETA — Aguardando suas decisões

Por favor:
1. Aprove/rejeite cada SPEC proposta
2. Aprove/rejeite cada ADR candidata
3. Responda as perguntas CLARIFY (ou marque "deixar aberta para depois")
4. Confirme prosseguir para Etapa 4 (Geração de arquivos)
```

**AGUARDE aprovações humanas.**

---

## Etapa 4 — Geração dos artefatos aprovados

**Objetivo:** criar EFETIVAMENTE os arquivos que foram aprovados em Etapa 3.

**Pré-condição:** Lista de SPECs/ADRs aprovadas em Etapa 3.

**O que fazer (UM ARQUIVO POR VEZ, AGUARDANDO APROVAÇÃO ENTRE CADA):**

1. Crie `PROJECT_BRIEF.md` final (versão aprovada em Etapa 2).
   → Mostre conteúdo, AGUARDE aprovação.

2. Crie `docs/<NOME_PROJETO>_Architecture.md` baseado em `docs/_ARCHITECTURE_TEMPLATE.md`.
   → Use o brief + módulos identificados + diagramas mermaid simples.
   → Mostre conteúdo, AGUARDE aprovação.

3. Crie `specs/SPEC_INDEX.md` final.
   → Mostre conteúdo, AGUARDE aprovação.

4. Para cada SPEC aprovada:
   → Crie `specs/modules/SPEC_<MODULO>.md` baseado em `specs/modules/_SPEC_TEMPLATE.md`.
   → Status retrospectivo conforme decidido.
   → Mostre conteúdo, AGUARDE aprovação.

5. Para cada ADR aprovada:
   → Crie `specs/decisions/ADR-NNN-<slug>.md` baseado em `specs/decisions/_ADR_TEMPLATE.md`.
   → Marque como ✔️ ACEITO (retrospectiva) com data atual.
   → Mostre conteúdo, AGUARDE aprovação.

6. Adapte `AGENTS.md`:
   → Substitua placeholders `<!-- ADAPT -->` com info real do projeto.
   → Atualize tabela de módulos e ADRs.
   → Mostre conteúdo, AGUARDE aprovação.

7. Crie `docs/handover_DISCOVERY_<DATA_HOJE>.md` baseado em `docs/_HANDOVER_TEMPLATE.md`.
   → Status: "✔️ DISCOVERY CONCLUÍDA — projeto agora tem SDD ativo"
   → Conteúdo: o que foi descoberto, decisões tomadas, próximos passos sugeridos.
   → Mostre conteúdo, AGUARDE aprovação.

**No fim de Etapa 4, escreva:**

```
🛑 ETAPA 4 COMPLETA — Todos os arquivos aprovados foram criados.

Resumo:
- PROJECT_BRIEF.md ✓
- docs/<X>_Architecture.md ✓
- specs/SPEC_INDEX.md ✓
- specs/modules/SPEC_*.md (N arquivos) ✓
- specs/decisions/ADR-NNN-*.md (M arquivos) ✓
- AGENTS.md adaptado ✓
- docs/handover_DISCOVERY_<DATA>.md ✓

Total de arquivos criados: <N>
LOC adicionados: <X> (apenas markdown — código zero)

Confirme prosseguir para Etapa 5 (Pronto pra trabalhar).
```

**AGUARDE GO humano.**

---

## Etapa 5 — Pronto pra trabalhar

**Objetivo:** transição para uso normal do SDD em tasks futuras.

**O que fazer:**

1. Resumo final do que foi documentado.
2. Lista das tarefas que o usuário pode iniciar agora:
   - "Para próxima feature, use `prompts/NEW_FEATURE.md`"
   - "Para bug fix, use `prompts/BUG_FIX.md`"
   - "Para refator, use `prompts/REFACTOR.md`"
3. Sugerir 2-3 melhorias detectadas durante DISCOVER que viraram backlog:
   - Ex.: "SPEC_<MODULO> tem cobertura <30%, vale priorizar testes"
   - Ex.: "ADR-NNN tem risco residual alto sem mitigação atual"
4. Recomendar primeiro commit:
   ```bash
   git add PROJECT_BRIEF.md docs/ specs/ AGENTS.md
   git commit -m "docs(sdd): adopt SDD framework retroactively (DISCOVER)"
   ```
5. NÃO commitar automaticamente — aguardar GATE 4 humano.

**No fim de Etapa 5:**

```
✅ DISCOVERY COMPLETA

O projeto agora tem documentação SDD ativa. Próximas tarefas seguem o ciclo
normal (ver docs/SDD_WORKFLOW.md §2 para o modo apropriado).

Sugestão de primeiro commit:
git add PROJECT_BRIEF.md docs/ specs/ AGENTS.md
git commit -m "docs(sdd): adopt SDD framework retroactively (DISCOVER)"

Backlog detectado durante DISCOVER (priorize conforme valor):
1. <melhoria 1>
2. <melhoria 2>
3. <melhoria 3>

Para iniciar próxima task, escolha o prompt apropriado em prompts/.
```

---

## Regras de comportamento durante DISCOVER

| Situação | Ação |
|---|---|
| Encontro algo que não entendo | Marque com `[?]` e pergunte na próxima etapa |
| Vejo código suspeito (vulnerabilidade óbvia) | Anote para mencionar no handover, não corrija |
| Encontro `.env` commitado | ALERTA URGENTE imediato — pare e avise |
| Encontro `node_modules/` ou `.venv/` commitados | Anote para sugerir limpeza no backlog |
| Vejo testes desatualizados (não passam) | Anote como gap, não rode/corrija agora |
| Quero sugerir refactor durante DISCOVER | NÃO sugira — DISCOVER é só observação |
| Sessão muito longa (>2h) | Pare na próxima etapa, gere handover parcial |

---

*Após DISCOVER, todas as tasks futuras seguem o ciclo SDD normal.*
