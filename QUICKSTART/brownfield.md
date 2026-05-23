# QUICKSTART — Brownfield (projeto existente)

> **Cenário:** você entrou num projeto que JÁ TEM código rodando. Pode ter:
> - **(A)** Documentação parcial (README, alguns docs)
> - **(B)** SDD parcial (alguns specs, sem index, sem ADRs)
> - **(C)** ZERO documentação ← este guia foca aqui (mais comum e mais doloroso)
>
> **Tempo total esperado:** 1-4h dependendo do tamanho do projeto.
>
> **Pré-requisito:** acesso ao código, ambiente de trabalho escolhido e
> autonomia para criar arquivos de docs (sem precisar de PR para cada doc).

---

## Decida em 30 segundos: qual sub-cenário?

| Sintomas | Sub-cenário | Pulo para |
|---|---|---|
| README está desatualizado, sem ADRs, sem specs | **(C) Zero docs** | [Passo 1 (DISCOVER)](#passo-1--rode-discover-coração-deste-guia) |
| Tem README OK + alguns docs/, mas sem SDD | **(A) Docs parciais** | [Passo 1 modificado](#variante-a-projeto-com-docs-parciais) |
| Já tem `specs/`, mas sem `SPEC_INDEX.md` ou desatualizado | **(B) SDD parcial** | [Variante B](#variante-b-sdd-parcial) |

---

## Passo 0 — Avalie escopo de adoção

Antes de instalar template:

1. **É um projeto crítico**? (produção; >1 dev mantém; >3 meses ativo)
   - Sim → adoção SDD vale o investimento
   - Não → considere só BOOTSTRAP rápido sem DISCOVER profundo

2. **Quem mais usa o repo?**
   - Só você → adoção é decisão sua
   - Time → alinhe com colegas; SDD funciona melhor com buy-in

3. **Você tem permissão para criar docs/, specs/, .agent/?**
   - Sim → siga este guia
   - Não → fork pessoal primeiro; provar valor; depois propor

---

## Passo 1 — Instale o template SDD no projeto

⚠️ **NÃO sobrescreva README.md** existente nem qualquer arquivo de produção.

### Opção A — Cópia seletiva (recomendada)

Copie APENAS o que não existe no projeto:

```powershell
# Windows PowerShell
$src = "C:\dev\sdd-starter"
$dst = "C:\dev\<seu-projeto-existente>"

# Estrutura SDD (não conflita com código)
Copy-Item -Recurse "$src\.agent" "$dst\.agent" -ErrorAction SilentlyContinue
Copy-Item -Recurse "$src\specs" "$dst\specs" -ErrorAction SilentlyContinue
Copy-Item -Recurse "$src\prompts" "$dst\prompts" -ErrorAction SilentlyContinue
Copy-Item -Recurse "$src\QUICKSTART" "$dst\QUICKSTART" -ErrorAction SilentlyContinue

# docs/ — APENAS templates, não sobrescreva docs existentes
Copy-Item "$src\docs\SDD_WORKFLOW.md" "$dst\docs\SDD_WORKFLOW.md" -ErrorAction SilentlyContinue
Copy-Item "$src\docs\_HANDOVER_TEMPLATE.md" "$dst\docs\_HANDOVER_TEMPLATE.md" -ErrorAction SilentlyContinue
Copy-Item "$src\docs\_ARCHITECTURE_TEMPLATE.md" "$dst\docs\_ARCHITECTURE_TEMPLATE.md" -ErrorAction SilentlyContinue

# Constituição e brief — só se não existirem
if (-not (Test-Path "$dst\AGENTS.md")) { Copy-Item "$src\AGENTS.md" "$dst\AGENTS.md" }
if (-not (Test-Path "$dst\PROJECT_BRIEF.md")) { Copy-Item "$src\PROJECT_BRIEF.md" "$dst\PROJECT_BRIEF.md" }
```

```bash
# macOS/Linux
SRC=~/dev/sdd-starter
DST=~/dev/<seu-projeto-existente>

cp -Rn $SRC/.agent $DST/.agent
cp -Rn $SRC/specs $DST/specs
cp -Rn $SRC/prompts $DST/prompts
cp -Rn $SRC/QUICKSTART $DST/QUICKSTART

mkdir -p $DST/docs
cp -n $SRC/docs/SDD_WORKFLOW.md $DST/docs/
cp -n $SRC/docs/_HANDOVER_TEMPLATE.md $DST/docs/
cp -n $SRC/docs/_ARCHITECTURE_TEMPLATE.md $DST/docs/

[ ! -f $DST/AGENTS.md ] && cp $SRC/AGENTS.md $DST/AGENTS.md
[ ! -f $DST/PROJECT_BRIEF.md ] && cp $SRC/PROJECT_BRIEF.md $DST/PROJECT_BRIEF.md
```

### Verifique o resultado

```bash
ls .agent specs prompts QUICKSTART docs
# Deve mostrar pastas/arquivos copiados sem ter sobrescrito o que já existia
```

Tooling opcional nao entra nesta copia padrao. Se o projeto escolher arquivos
especificos para uma ferramenta, aplique depois apenas o material necessario de
`tooling/`.

---

## Passo 2 — Rode DISCOVER (coração deste guia)

Esta é a etapa mais importante e mais subestimada. **NÃO PULE.**

### Por quê DISCOVER ANTES de qualquer task

Se você marcar o agente em uma task sem DISCOVER:
- Ele lê arquivos aleatórios (perde contexto)
- Inventa nomes de módulos
- Não conhece convenções do time
- Toma decisões inconsistentes
- Cria SPECs que não batem com código real

Com DISCOVER:
- Mapa coerente do projeto inteiro (1-2h investidos)
- Próximas N tasks ficam 5-10x mais rápidas
- Onboarding de novos devs cai de semanas para horas

### Como rodar DISCOVER

Abra a IDE no projeto e cole:

```
Vamos rodar prompts/DISCOVER.md neste projeto.

CONTEXTO:
- Projeto: <NOME_DO_PROJETO>
- Estágio: <estágio do brief — escolha em PROJECT_BRIEF.md §1>
- Stack: <que você já sabe — Python? Node? Go?>
- O que sei: <1-2 frases sobre o que o projeto faz>
- O que NÃO sei: tudo o resto

Siga RIGOROSAMENTE as 5 etapas:
1. Reconhecimento (estrutura, sem ler conteúdo)
2. Análise de domínio (entry points + configs + brief rascunho)
3. Mapeamento SDD retrospectivo (módulos + ADRs implícitas)
4. Geração de artefatos (UM POR VEZ, com meu GO)
5. Pronto pra trabalhar (handover + próximas tasks)

PARE em cada etapa para meu GO. NÃO escreva código de produção.
NÃO modifique nada existente. Apenas leia, infira, proponha.
Marque [?] em qualquer inferência incerta para eu validar.
```

### O que esperar de cada etapa

#### Etapa 1 — Reconhecimento (10-20 min)

**Output esperado:** uma tabela tipo:

```
Estrutura raiz:
- src/  (50 arquivos, principal código de aplicação)
- tests/ (12 arquivos, parecem unit tests com pytest)
- migrations/ (8 arquivos SQL)
- docs/ (3 arquivos: README, CHANGELOG, deploy.md)
- ...

Stack inferida:
- Python (requirements.txt, pyproject.toml)
- FastAPI (em requirements: fastapi==0.104, uvicorn)
- PostgreSQL (psycopg2 + migrations/)
- Docker (Dockerfile)

Pastas de domínio detectadas em src/:
- src/auth/ → módulo de autenticação?
- src/billing/ → faturamento?
- src/users/ → gerenciamento de usuários?
[?] src/utils/ → não clara responsabilidade
```

**Sua ação:** confirmar/corrigir interpretação de cada pasta.

#### Etapa 2 — Análise de domínio (15-30 min)

**Output esperado:** rascunho de PROJECT_BRIEF.md preenchido:

```markdown
## §1 Objetivo
[?] Sistema de cobrança recorrente para SaaS B2B,
    inferido de routes em src/billing/ e dependência de stripe SDK.

## §2 Stack
- Python 3.11 (pyproject.toml)
- FastAPI 0.104 (requirements.txt) — https://fastapi.tiangolo.com/
- PostgreSQL (psycopg2 + 8 migrations) — versão [?]
- Stripe SDK [?] versão exata
- Deploy: Dockerfile presente, mas [?] qual cloud
```

**Sua ação:** preencher os `[?]`, corrigir inferências erradas.

#### Etapa 3 — Mapeamento SDD retrospectivo (20-40 min)

**Output esperado:** lista de módulos com responsabilidade + status:

```markdown
| Módulo | Resp. (1 frase) | Status | Cobertura | Observações |
|---|---|---|---|---|
| auth | Login/JWT | ✔️ | [?] sem tests visíveis | depende de redis |
| billing | Cobrança Stripe | 🚧 | 30% (4 tests) | webhook não testado |
| ...
```

E ADRs candidatas:
```markdown
ADR-001: PostgreSQL (vs SQLite/MongoDB) — implícita
ADR-002: FastAPI (vs Flask/Django) — implícita
ADR-003: Stripe (vs in-house) — implícita
```

**Sua ação:** aprovar quais SPECs e ADRs gerar.

#### Etapa 4 — Geração de artefatos (40-90 min)

**O agente gera UM ARQUIVO POR VEZ:**
1. PROJECT_BRIEF.md final (com seus inputs)
2. docs/<NOME>_Architecture.md v1
3. specs/SPEC_INDEX.md
4. specs/modules/SPEC_auth.md
5. specs/modules/SPEC_billing.md
6. ... (todos os módulos aprovados)
7. specs/decisions/ADR-001.md
8. ... (todos os ADRs aprovados)
9. AGENTS.md adaptado
10. docs/handover_DISCOVERY_<DATA>.md

**Sua ação:** revisar cada arquivo. Aceitar/rejeitar. **Nunca pula esta revisão** — é a chance de pegar inferências erradas antes de virar oficial.

#### Etapa 5 — Pronto pra trabalhar (5-10 min)

**Output esperado:** resumo + lista de próximos prompts disponíveis.

**Sua ação:** commit manual do que DISCOVER produziu:

```bash
git add AGENTS.md PROJECT_BRIEF.md docs/ specs/ .agent/ prompts/ QUICKSTART/
git commit -m "$(cat <<'EOF'
docs: adopt SDD framework via DISCOVER

Reverse engineering documentation generated by sdd-starter DISCOVER prompt.
- PROJECT_BRIEF.md captures inferred scope
- docs/<NOME>_Architecture.md v1 documents current state
- specs/ captures N modules with retrospective status
- specs/decisions/ documents N implicit ADRs
- AGENTS.md adapted to project specifics

Inferred from existing code; reviewed and approved by <seu-nome>.
EOF
)"
```

---

## Passo 3 — Faça primeira task SDD-style

Agora que tem documentação, escolha uma task. Não importa se é bug fix, feature ou refactor. Use o prompt apropriado:

| Task | Prompt | Tempo extra (vs sem SDD) |
|---|---|---|
| Bug fix simples | `prompts/BUG_FIX.md` | +10-20 min (regression test obrigatório) |
| Feature pequena | `prompts/NEW_FEATURE.md` (modo "pequena") | +5-10 min |
| Feature média | `prompts/NEW_FEATURE.md` (modo "média") | +30-60 min (SPEC + ADR + PLAN) |
| Feature grande | `prompts/NEW_FEATURE.md` (modo "grande") | +1-2h (SPEC multi-fase) |
| Refator interno | `prompts/REFACTOR.md` (tipo "interno") | +20-40 min (cobertura + testes) |
| Refator arquitetural | `prompts/REFACTOR.md` (tipo "arquitetural") | +1-3h (ADR de migração obrigatória) |

**O overhead se paga em 2-3 tasks** porque:
- Próximo dev (incluindo você daqui 2 meses) entende contexto em 5 min via handover
- Bug não volta (regression tests obrigatórios)
- ADRs evitam reinventar decisões
- Smoke gates evitam regressões em produção

---

## Variante (A) — Projeto com docs parciais

Se já tem README.md decente + alguns docs/:

1. **NÃO sobrescreva docs existentes.** DISCOVER complementa, não substitui.
2. Em **Passo 2 (DISCOVER)**, mencione no contexto: "README.md está atualizado, use-o como fonte primária. Complemente com SPECs e ADRs que não existem ainda."
3. Etapa 4 do DISCOVER vai criar ADRs e SPECs faltantes; Architecture document referencia README ao invés de duplicar.

---

## Variante (B) — SDD parcial

Se já tem `specs/` mas falta organização:

1. NÃO rode DISCOVER inteiro — desperdício.
2. Use **prompts/ONBOARDING.md** primeiro:
   ```
   Use prompts/ONBOARDING.md para entender o estado atual do SDD neste projeto.
   ```
3. Agente vai listar gaps:
   - SPEC_INDEX desatualizado?
   - ADRs faltando?
   - Handovers ausentes?
4. Para cada gap, faça uma micro-task:
   - "Atualize SPEC_INDEX.md baseado nas SPECs em specs/modules/"
   - "Crie ADR-NNN para a decisão de usar X (que já está implementada mas não documentada)"

---

## Checklist final do brownfield

Após Passos 1-3, confirme:

- [ ] Estrutura SDD instalada (`.agent/`, `specs/`, `prompts/`)
- [ ] `PROJECT_BRIEF.md` preenchido (manualmente ou via DISCOVER)
- [ ] `AGENTS.md` adaptado (sem `<!-- ADAPT -->` órfãos)
- [ ] `docs/<NOME>_Architecture.md` v1 existe
- [ ] `specs/SPEC_INDEX.md` lista módulos do projeto
- [ ] Pelo menos 2 SPECs criadas (módulos principais)
- [ ] Pelo menos 1 ADR retrospectiva (ex.: choice de DB)
- [ ] `docs/handover_DISCOVERY_<DATA>.md` arquivado
- [ ] Commit inicial pushed (ou em branch para PR de adoção SDD)

---

## Erros comuns no brownfield

| Erro | Sintoma | Solução |
|---|---|---|
| Pular DISCOVER ("vou só fazer a task") | Agente faz inferência ruim, código inconsistente | Sempre DISCOVER primeiro em projeto desconhecido |
| Sobrescrever docs existentes | Conflito git, perda de info | Cópia seletiva no Passo 1 |
| Aceitar todas as inferências do agente sem revisar | Documentação fica errada | Revisar cada arquivo na Etapa 4 |
| DISCOVER sem `[?]` (agente "tem certeza" de tudo) | Inferências erradas viram fato | Forçar agente a marcar incertezas |
| Tentar documentar 100% antes de qualquer task | Adoção SDD vira projeto eterno | Documente módulos críticos primeiro; resto sob demanda |
| Não fazer commit do DISCOVER | Próxima sessão re-descobre tudo | Commit + push antes da próxima task |

---

## Adoção gradual (recomendada para times)

Se o time não comprou SDD ainda, faça assim:

### Sprint 1 (você sozinho)
- Instala template, roda DISCOVER, gera SPECs dos módulos que VOCÊ vai tocar
- Faz 1 task usando `prompts/NEW_FEATURE.md` ou `BUG_FIX.md`
- PR: mostra a SPEC, o handover, e como o contexto ficou claro

### Sprint 2 (1-2 colegas curiosos)
- Apresenta resultado do Sprint 1
- Ensina prompts/ basic
- Eles fazem 1 task SDD-style cada

### Sprint 3+ (time inteiro)
- Adoção é decisão coletiva, não imposição
- ADRs viram norma; PRs sem ADR de trade-off são rejeitados em review

**Anti-padrão:** "vamos adotar SDD em tudo desde amanhã." Não funciona. Adoção orgânica > mandato top-down.

---

## Quando NÃO usar este guia

- Projeto de protótipo / hackathon (overhead não compensa)
- Projeto que vai ser deprecated em <1 mês (não vale o investimento)
- Code golf / scripts pessoais isolados

---

*Veja também: `QUICKSTART/greenfield.md` para projetos novos, `prompts/DISCOVER.md` para o prompt detalhado de reverse engineering, `prompts/ONBOARDING.md` se SDD já existe.*
