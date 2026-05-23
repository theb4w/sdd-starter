<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/BOOTSTRAP.md — Inicialização SDD para projetos novos
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO:
  - Projeto NOVO (greenfield) e você TEM o brief preenchido
  - OU projeto existente onde você JÁ CONHECE o domínio e preencheu o brief

  COMO USAR:
  1. Garanta que PROJECT_BRIEF.md está preenchido (manualmente ou via DISCOVER)
  2. Cole TODO o conteúdo abaixo no chat do agente
  3. Substitua <PROJETO> pelo nome real
  4. Agente para no GATE 1 (PLAN do primeiro módulo) sem implementar código

  RESULTADO ESPERADO:
  - AGENTS.md adaptado ao projeto
  - docs/<Project>_Architecture.md como rascunho v1
  - specs/SPEC_INDEX.md com módulos do brief
  - 1 SPEC do módulo crítico (escolhido por você)
  - PLAN proposto para o módulo crítico (aguardando GATE 1)
═══════════════════════════════════════════════════════════════════════════════
-->

# BOOTSTRAP — Inicialização SDD do projeto <PROJETO>

**Data:** <DATA_HOJE>
**Operador:** <SEU_NOME>

---

## Papel do agente

Você é um **arquiteto de software** iniciando um projeto seguindo Spec-Driven
Development (SDD). Sua missão: gerar a documentação base SDD a partir do
`PROJECT_BRIEF.md` que o usuário preencheu.

## Restrições absolutas

- **NÃO ESCREVA CÓDIGO DE PRODUÇÃO** nesta sessão.
- Pare no **GATE 1** (PLAN do primeiro módulo) — aguarde aprovação humana.
- Toda decisão técnica registra URL de fonte primária.
- Toda alternativa em ADR tem mínimo 2 opções consideradas.

---

## Etapa 1 — Leitura inicial

Leia, nesta ordem:
1. `AGENTS.md` (template — você vai adaptar)
2. `docs/SDD_WORKFLOW.md` (framework canônico — siga rigorosamente)
3. `.agent/agents.md` (4 personas — ative @pm para esta missão)
4. `PROJECT_BRIEF.md` (input do usuário — fonte de verdade do escopo)
5. Templates em `specs/`, `docs/_*` para ter referência de formato

Após leitura, responda:
- Qual estágio do projeto (greenfield / brownfield)?
- Qual stack identificada no brief?
- Quais módulos foram listados?
- Qual módulo parece mais crítico para começar (o "core" do produto)?
- Há contradições no brief? Liste para confirmação humana.

**🛑 PARE. Aguarde GO humano para Etapa 2.**

---

## Etapa 2 — Adaptar AGENTS.md ao projeto

Modifique `AGENTS.md` substituindo todos os `<!-- ADAPT -->`:

1. Identidade do projeto (nome, objetivo, estágio, ambiente relevante se houver)
2. Tabela de stack técnica (versões fixadas com URL de fonte)
3. Regras absolutas específicas do projeto (compliance, performance, etc.)
4. Estrutura de diretórios ajustada à stack escolhida
5. Tabela de módulos (do brief)
6. Tabela de ADRs (vazia inicialmente)
7. Lista "O que este projeto NÃO faz" (do brief §5)

**Mostre o AGENTS.md final para aprovação. AGUARDE GO humano.**

---

## Etapa 3 — Criar Architecture document v1

Crie `docs/<NOME_PROJETO>_Architecture.md` baseado em `docs/_ARCHITECTURE_TEMPLATE.md`:

1. §1 Visão Geral — do brief §1
2. §2 Princípios Arquiteturais — derive do brief (P-01, P-02, ...)
3. §3 Stack Técnica — do brief §2 (com versões pinned + URLs)
4. §4 Diagrama de Sistemas — esboço alto-nível em mermaid baseado em módulos
5. §5 Módulos — tabela inicial (do brief §4)
6. §6 Dados e Persistência — esboço (depende dos módulos)
7. §7 Auth — se há módulo de auth, esboço; senão "N/A no MVP"
8. §8-15 — preencher com `[?]` o que ainda não dá pra decidir e marcar para resolver via ADRs

**Mostre o Architecture v1. AGUARDE GO humano.**

---

## Etapa 4 — Criar SPEC_INDEX.md inicial

Baseado em `specs/SPEC_INDEX.md` template, popule:

1. Tabela de módulos (do brief §4) com status `📝 RASCUNHO` (vão ser criados como SPECs em sequência)
2. Tabela de ADRs (vazia, aguardando primeiro trade-off)
3. §"Próximos Passos" listando o módulo crítico identificado em Etapa 1

**Mostre o SPEC_INDEX. AGUARDE GO humano.**

---

## Etapa 5 — Criar SPEC do módulo crítico

Para o módulo identificado como mais crítico:

1. Crie `specs/modules/SPEC_<MODULO>.md` baseado em `specs/modules/_SPEC_TEMPLATE.md`.
2. Preencha §1 (Objetivo), §2 (Contexto+Justificativa), §3 (Design Técnico),
   §4 (Regras de Negócio com fontes), §5 (Variáveis de ambiente), §6 (Arquivos).
3. **§7 (Testes Requeridos)**: liste pelo menos 3 testes-chave.
4. **§8 (DoD)**: checklist verificável.
5. **§9 (CLARIFY)**: liste perguntas que VOCÊ tem (não invente respostas).

**Mostre a SPEC. AGUARDE responder CLARIFY humano.**

---

## Etapa 6 — Detectar trade-offs → propor ADRs

Durante CLARIFY (humano respondeu), identifique trade-offs com 2+ alternativas
viáveis. Para cada um:

1. Proponha rascunho de ADR baseado em `specs/decisions/_ADR_TEMPLATE.md`.
2. Mínimo 2 alternativas com prós/contras/custo/fonte (URL).
3. Sua recomendação com justificativa.

**Mostre cada ADR. AGUARDE aprovação humana ANTES de marcar como ✔️ ACEITO.**

---

## Etapa 7 — Gerar PLAN do módulo crítico

Após CLARIFY resolvido e ADRs aceitas:

1. Atualize SPEC para status `📋 PLAN`.
2. Crie `specs/plans/PLAN_<MODULO>.md` baseado em `specs/plans/_PLAN_TEMPLATE.md`.
3. Decida multi-fase ou single-phase (critérios em SDD_WORKFLOW §13.1).
4. Mapa de dependências em mermaid.
5. Riscos com mitigação concreta.
6. Checklist pré-IMPLEMENT.

**🛑 GATE 1 — Mostre o PLAN. AGUARDE aprovação humana antes de prosseguir.**

---

## Etapa 8 — Encerramento e handover

Após GATE 1 aprovado (ou se sessão chegou ao fim):

1. Crie `docs/handover_BOOTSTRAP_<DATA>.md` baseado em `docs/_HANDOVER_TEMPLATE.md`.
2. §1: o que esta sessão entregou (lista concreta dos artefatos criados).
3. §7 Próximos Passos:
   - Se GATE 1 aprovado → "Próxima sessão: gerar TASKS, depois IMPLEMENT (T-A1)"
   - Se sessão pausou antes do GATE 1 → "Próxima sessão: continuar do checkpoint X"
4. §8 Como Retomar: cole `prompts/RESUME.md` preenchido.

**Mostre o handover. NÃO commite — aguardar humano revisar.**

---

## Sugestão de primeiro commit (após handover aprovado)

```bash
git add AGENTS.md docs/ specs/ PROJECT_BRIEF.md
git commit -m "docs(sdd): bootstrap SDD framework + first SPEC for <MODULO>"
```

---

## Regras de comportamento durante BOOTSTRAP

| Situação | Ação |
|---|---|
| Brief tem ambiguidade | Pergunte (não decida sozinho) |
| Não tenho URL de fonte para uma decisão | Marque como `[? URL pendente]` e pergunte |
| Detectei trade-off mas humano não pediu ADR | Sugira ADR; humano decide se cria |
| Quero criar mais de uma SPEC nesta sessão | NÃO crie — uma por vez, com gates |
| Sessão muito longa | Encerre na etapa atual + handover parcial |

---

*Após BOOTSTRAP, sessões seguintes usam `prompts/RESUME.md` (continuar fase) ou `prompts/NEW_FEATURE.md` (iniciar próximo módulo).*
