<!--
═══════════════════════════════════════════════════════════════════════════════
  PROJECT_BRIEF.md — Escopo do projeto (input do BOOTSTRAP / output do DISCOVER)
═══════════════════════════════════════════════════════════════════════════════

  Este arquivo tem DOIS usos:

  1. GREENFIELD (projeto novo, você sabe o que quer):
     - VOCÊ preenche este arquivo manualmente (5-10 min)
     - Depois cola prompts/BOOTSTRAP.md no agente
     - Agente lê este brief e cria o resto do SDD adaptado

  2. BROWNFIELD sem docs (projeto existente, você não sabe o que tem):
     - Você cola prompts/DISCOVER.md no agente
     - Agente EXPLORA o código existente
     - Agente PREENCHE este brief com [?] nas dúvidas
     - VOCÊ valida e completa os [?]
     - Agente cria SPEC_INDEX retroativo + ADRs detectadas

  Em ambos os casos, este brief vira FONTE DE VERDADE inicial do projeto.
  Atualize-o conforme o projeto evolui (ou deixe envelhecer e use SPEC_INDEX
  como fonte canônica).

  REMOVA este header antes do primeiro commit do seu projeto real.
═══════════════════════════════════════════════════════════════════════════════
-->

# Project Brief — <!-- ADAPT: NOME_DO_PROJETO -->

**Data:** YYYY-MM-DD
**Autor:** <nome>
**Versão:** 1.0

---

## 1. Objetivo (1-2 frases)

> O que este projeto faz e para quem.

<!-- Exemplo:
"Sistema de assistente pessoal conversacional para uso individual, com memória
persistente cross-sessão e custo operacional <$5/mês. Usuário-alvo: o próprio
desenvolvedor (single-user)."
-->

<seu objetivo aqui>

---

## 2. Stack desejada

| Camada | Tecnologia preferida | Versão |
|---|---|---|
| Linguagem backend | <!-- ex.: Python | Node.js | Go --> | <!-- ex.: 3.11 | 20 LTS | 1.22 --> |
| Framework web | <!-- ex.: FastAPI | Express | Gin --> | — |
| Banco de dados | <!-- ex.: PostgreSQL | Firestore | MongoDB --> | — |
| Cache | <!-- ex.: Redis | em-memória | nenhum --> | — |
| Frontend | <!-- ex.: Next.js | vanilla JS | nenhum --> | — |
| Infra/Deploy | <!-- ex.: GCP Cloud Run | AWS Lambda | Vercel | self-hosted --> | — |
| CI/CD | <!-- ex.: GitHub Actions | nenhum --> | — |
| LLM (se aplicável) | <!-- ex.: Gemini 2.5 Flash-Lite | GPT-4 | nenhum --> | — |

> **Nota:** Se preencher como `[?]` qualquer linha, o agente usará o cenário
> mais comum / sensato e propor ADR. Você aprova.

---

## 3. Restrições

| Restrição | Valor |
|---|---|
| Orçamento mensal | <!-- ex.: <$5/mês | <$50/mês | sem limite --> |
| Compliance regulatório | <!-- ex.: LGPD | GDPR | HIPAA | PCI-DSS | nenhum específico --> |
| SLA / latência alvo | <!-- ex.: p95 <500ms | best-effort --> |
| Multi-user ou single-tenant | <!-- ex.: single-tenant | multi-user com 100+ | indeterminado --> |
| Região de dados | <!-- ex.: Brasil (LGPD) | EU (GDPR) | qualquer --> |
| Tempo até MVP | <!-- ex.: 4 semanas | 3 meses | sem prazo --> |
| Time disponível | <!-- ex.: 1 dev solo | 3 devs | 1 dev + 1 designer --> |

---

## 4. Módulos esperados (lista preliminar)

> Apenas o esqueleto. O agente vai refinar e propor SPECs detalhadas.
> Use o nome em UPPER_SNAKE_CASE (será o nome da SPEC).

- **<MODULO_1>**: <responsabilidade em 1 linha>
- **<MODULO_2>**: <responsabilidade em 1 linha>
- **<MODULO_3>**: <responsabilidade em 1 linha>

<!-- Exemplo:
- AUTH: Login via Google OAuth, sessão persistida 30 dias
- SESSIONS: Gestão de conversas (criar, listar, deletar)
- ORCHESTRATOR: Roteador de turnos para o LLM com cost tracking
- API: Endpoints REST para frontend
- WEBUI: Frontend HTML/CSS/JS sem framework pesado
-->

---

## 5. Fora do MVP (importante!)

> O que EXPLICITAMENTE não vamos fazer agora. Evita scope creep.

- ❌ <funcionalidade fora>
- ❌ <funcionalidade fora>
- ❌ <funcionalidade fora>

<!-- Exemplo:
- ❌ Mobile app (web responsivo basta)
- ❌ Integração com WhatsApp/Telegram (v2)
- ❌ Multi-tenant (single-user only no v1)
- ❌ Voz / Live API (v2)
- ❌ Dashboard administrativo (CLI basta)
-->

---

## 6. Métricas de sucesso

> Como saberemos que funcionou? Números, não adjetivos.

- <!-- ex.: ≥10 sessões úteis por dia em uso real -->
- <!-- ex.: Custo operacional < $5/mês -->
- <!-- ex.: Latência p95 < 2s no fluxo principal -->
- <!-- ex.: 0 incidentes de segurança nos primeiros 30 dias -->
- <!-- ex.: Onboarding de novo dev em <1h via SDD docs -->

---

## 7. Estado atual (preencher se BROWNFIELD)

> Se o projeto JÁ EXISTE com código mas sem docs, ajude o agente respondendo:

| Pergunta | Resposta |
|---|---|
| Há código existente? Onde? | <ex.: sim, em `src/`, ~5k LOC> ou `[?]` |
| Linguagem/framework já decididos? | <ex.: Python+FastAPI já em uso> ou `[?]` |
| Há testes? Que cobertura aproximada? | <ex.: ~30% cobertura, tests/unit/> ou `[?]` |
| Há documentação (README, wiki, comentários)? | <ex.: README desatualizado de 6m> ou `[?]` |
| Última modificação relevante (sessão atual ou antiga)? | <ex.: deploy ontem, fix de bug X> ou `[?]` |
| Pessoa(s) que conhecem o histórico? | <ex.: dev anterior já saiu da empresa> ou `[?]` |
| Existe ambiente de staging/produção? | <ex.: sim, `staging.exemplo.com`> ou `[?]` |
| Há dependências externas críticas? | <ex.: API X, banco gerenciado Y> ou `[?]` |

> Se este projeto é GREENFIELD (do zero), ignore esta seção ou apague.

---

## 8. Contexto adicional (opcional)

> Qualquer coisa que ajude o agente a entender o domínio:
> - Inspirações ("é tipo X mas com Y")
> - Restrições culturais/organizacionais ("não podemos usar Y porque empresa")
> - Ferramentas obrigatórias do time ("usamos JIRA, Slack")
> - Histórico ("tentamos abordagem X e falhou por causa Y")

<seu contexto aqui>

---

*Após preencher (ou ter este preenchido pelo DISCOVER), use o prompt apropriado:*
- *Greenfield → `prompts/BOOTSTRAP.md`*
- *Brownfield com brief preenchido → `prompts/BOOTSTRAP.md`*
- *Brownfield sem nada → `prompts/DISCOVER.md`*
