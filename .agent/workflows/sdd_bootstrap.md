# Workflow: SDD Bootstrap

> Workflow operacional para inicializar SDD num projeto novo (greenfield)
> ou existente onde dev JÁ TEM o brief preenchido.
>
> "Pair workflow" do `prompts/BOOTSTRAP.md`.

---

## Quando usar

- Greenfield: projeto novo do zero
- Brownfield com brief: projeto existente onde dev preencheu PROJECT_BRIEF.md
- Após `prompts/DISCOVER.md` ter completado: BOOTSTRAP pode complementar com SPECs adicionais

---

## Princípios

| Princípio | Significa |
|---|---|
| **Brief é fonte de verdade** | Tudo deriva do PROJECT_BRIEF.md |
| **Adapta sem reinventar** | AGENTS.md template com placeholders → preencher, não rescrever |
| **Para no GATE 1** | Não implementa código nesta sessão |
| **Trade-offs viram ADRs** | Toda decisão de stack com 2+ opções → ADR proposta |

---

## Pré-condições

Antes de iniciar:
- [ ] Template SDD instalado (todos os arquivos do sdd-starter copiados)
- [ ] `PROJECT_BRIEF.md` preenchido (manualmente ou via DISCOVER)
- [ ] Workspace é o projeto a inicializar (não o sdd-starter!)
- [ ] Git inicializado e fora de cloud-sync

---

## Sequência

### Etapa 1 — Leitura inicial

**Ferramentas:** `Read`.

**O que ler:**
1. `AGENTS.md` (template — entender placeholders)
2. `docs/SDD_WORKFLOW.md` (framework — siga rigorosamente)
3. `.agent/agents.md` (personas — usar @pm)
4. `PROJECT_BRIEF.md` (input do usuário)
5. Templates em `specs/`, `docs/_*` (formato de referência)

**Output:** análise inicial:
- Estágio do projeto
- Stack identificada
- Módulos do brief
- Módulo crítico (sugestão para começar)
- Contradições no brief (para humano resolver)

**Gate:** humano confirma análise + escolhe módulo crítico.

### Etapa 2 — Adaptar AGENTS.md

**Ferramentas:** `StrReplace` (substituir placeholders um a um).

**O que substituir:**
- `<!-- ADAPT: NOME_DO_PROJETO -->` → nome real
- Identidade do projeto (do brief §1)
- Stack técnica (do brief §2 com URLs de fonte)
- Regras absolutas específicas (compliance, performance)
- Estrutura de diretórios ajustada à stack
- Tabela de módulos (do brief §4)
- "O que NÃO faz" (do brief §5)

**Gate:** mostrar AGENTS.md final, aguardar aprovação.

### Etapa 3 — Architecture document v1

**Ferramentas:** `Write` (baseado em `docs/_ARCHITECTURE_TEMPLATE.md`).

**Conteúdo:**
- §1 Visão geral (do brief §1 + §2)
- §2 Princípios arquiteturais (derivar do brief)
- §3 Stack técnica (do brief §2)
- §4 Diagramas mermaid alto-nível (baseado em módulos)
- §5 Tabela de módulos (status: 📝 RASCUNHO inicialmente)
- §6-15 com `[?]` para resolver via SPECs/ADRs futuras

**Gate:** mostrar v1, aguardar aprovação.

### Etapa 4 — SPEC_INDEX inicial

**Ferramentas:** `Write` (baseado em `specs/SPEC_INDEX.md` template).

**Conteúdo:**
- Tabela de módulos com status 📝 RASCUNHO
- Tabela de ADRs vazia
- §"Próximos Passos" listando módulo crítico

**Gate:** mostrar, aguardar aprovação.

### Etapa 5 — SPEC do módulo crítico

**Ferramentas:** `Write` (baseado em `specs/modules/_SPEC_TEMPLATE.md`).

**Conteúdo:**
- §1-6 preenchido (objetivo, contexto, design, regras, env, arquivos)
- §7 (Testes): mínimo 3 testes-chave
- §8 (DoD): checklist verificável
- §9 (CLARIFY): perguntas abertas (não inventar respostas!)

**Gate:** humano responde CLARIFY.

### Etapa 6 — ADRs (se trade-offs detectados)

**Ferramentas:** `Write` (baseado em `specs/decisions/_ADR_TEMPLATE.md`).

**Para cada trade-off identificado em CLARIFY:**
- Contexto + 2+ alternativas + recomendação
- Status: 📝 PROPOSTA até humano aprovar

**Gate:** humano aprova cada ADR antes de marcar ✔️ ACEITO.

### Etapa 7 — PLAN do módulo crítico

**Ferramentas:** `Write` (baseado em `specs/plans/_PLAN_TEMPLATE.md`).

**Conteúdo:**
- Resumo executivo
- Tabela de fases (decidir multi-fase via critérios SDD_WORKFLOW §13.1)
- Mapa de dependências (mermaid)
- Riscos com mitigação concreta
- Checklist pré-IMPLEMENT

**🛑 GATE 1 — humano aprova PLAN.**

### Etapa 8 — Handover de bootstrap

**Ferramentas:** `Write` (baseado em `docs/_HANDOVER_TEMPLATE.md`).

**Conteúdo:**
- §1: artefatos criados nesta sessão
- §7: próxima sessão = gerar TASKS, depois IMPLEMENT
- §8: prompt RESUME.md preenchido

**Gate:** humano revisa, sugere comando de commit, executa manualmente.

---

## Anti-padrões durante BOOTSTRAP

| Anti-padrão | Por quê é ruim | Solução |
|---|---|---|
| Implementar código nesta sessão | BOOTSTRAP é só docs | Parar no GATE 1 |
| Criar SPEC para todos os módulos de uma vez | Sobrecarga humana | Um por vez, começar pelo crítico |
| Inventar respostas para CLARIFY | Perde rastreabilidade | Perguntar ao humano |
| Aceitar ADR sem aprovação | Mantém decisão tribal | Status PROPOSTA até GO humano |
| Skipar §"Como Reverter" do ADR | Decisão fica irreversível na prática | Sempre escrever |

---

## Diferença prática: BOOTSTRAP vs DISCOVER

| Aspecto | BOOTSTRAP | DISCOVER |
|---|---|---|
| Input | Brief preenchido | Brief vazio + código existente |
| Direção | Documenta o que VAI ser | Documenta o que JÁ é |
| Status SPECs | 📝 RASCUNHO (futuras) | ✔️/🚧/❌ (retrospectivo) |
| Status ADRs | 📝 PROPOSTA (futuras decisões) | ✔️ ACEITO retroativo (decisões já no código) |
| Gate final | GATE 1 (PLAN do 1º módulo) | Etapa 5 (pronto pra próxima task) |

---

## Tempo esperado

| Cenário | Tempo total |
|---|---|
| Greenfield, 3-5 módulos | 1-2h |
| Brownfield com brief, 5-10 módulos | 1.5-2.5h |
| Após DISCOVER (complemento) | 30-60 min |

---

*Ver `prompts/BOOTSTRAP.md` para o prompt copy-paste que orienta o usuário.*
