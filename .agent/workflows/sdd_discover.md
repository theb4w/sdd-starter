# Workflow: SDD Discover

> Workflow operacional para reverse engineering documentation em projeto
> existente que NÃO TEM docs/specs/ADRs.
>
> Este é o "pair workflow" do `prompts/DISCOVER.md` — ele documenta o
> processo do lado do agente, enquanto DISCOVER.md é o que o usuário cola.

---

## Quando usar

- Dev entrou em projeto sem documentação
- Dev quer adotar SDD em projeto existente
- Agente precisa entender projeto antes de qualquer task

---

## Princípios

| Princípio | Significa |
|---|---|
| **Observar, não modificar** | DISCOVER NUNCA escreve código de produção |
| **Inferir com humildade** | Marcar `[?]` quando não tem certeza |
| **Validar a cada etapa** | 5 etapas, gate humano em cada |
| **Documentar retrospectivamente** | SPECs e ADRs com status retroativo |
| **Não prometer mais do que pode** | Brief só preenche o que código revela |

---

## Pré-condições

Antes de iniciar:
- [ ] Template SDD copiado (mínimo: AGENTS.md, SDD_WORKFLOW.md, agents.md, DISCOVER.md, PROJECT_BRIEF.md vazio)
- [ ] Workspace é o projeto a documentar (não o sdd-starter!)
- [ ] Usuário leu o que DISCOVER vai fazer e aprovou começar

---

## Sequência

### Etapa 1 — Reconhecimento

**Ferramentas:** `Glob`, `ls`, `Grep` (apenas para listagem de arquivos por extensão), file count.

**O que NÃO fazer:** ler conteúdo de arquivos de código (só estrutura).

**Output:** tabela de "o que existe" para humano confirmar.

**Gate:** humano confirma que mapeamento bate com percepção.

### Etapa 2 — Análise de domínio

**Ferramentas:** `Read` (entry points + configs + dependency manifest + README), `Grep` (procurar imports, integrações).

**O que ler:**
- `README.md`
- `main.py` / `index.js` / `app.py` / `cmd/main.go`
- `requirements.txt` / `package.json` / `go.mod`
- `Dockerfile` / `.env.example` / configs de framework

**Output:** rascunho de PROJECT_BRIEF.md com `[?]` em campos incertos.

**Gate:** humano preenche `[?]` e confirma interpretação.

### Etapa 3 — Mapeamento SDD retrospectivo

**Ferramentas:** `SemanticSearch`, `Read` (módulos individuais), `Grep` (encontrar padrões).

**Para cada módulo:**
- Identificar responsabilidade aparente (1 frase)
- Listar arquivos principais (top 5 por tamanho)
- Endpoints/funções públicas
- Variáveis de ambiente lidas
- Status retrospectivo: ✔️/🚧/❌
- `[?]` para gaps (cobertura, última modificação)

**Para identificar ADRs implícitas:**
- Choice de DB → ADR
- Auth strategy → ADR
- Pattern arquitetural → ADR
- Vendor lock-in → ADR

**Output:** SPEC_INDEX rascunho + N SPECs propostas + M ADRs candidatas.

**Gate:** humano aprova/rejeita SPECs e ADRs uma a uma.

### Etapa 4 — Geração dos artefatos

**Ferramentas:** `Write` (criar arquivos baseados em templates).

**Ordem (UM ARQUIVO POR VEZ, AGUARDANDO APROVAÇÃO):**
1. `PROJECT_BRIEF.md` final
2. `docs/<NOME_PROJETO>_Architecture.md` v1
3. `specs/SPEC_INDEX.md` final
4. `specs/modules/SPEC_<MODULO>.md` (uma por módulo aprovado)
5. `specs/decisions/ADR-NNN-<slug>.md` (uma por decisão aprovada)
6. `AGENTS.md` adaptado (substituir placeholders)
7. `docs/handover_DISCOVERY_<DATA>.md`

**Gate:** humano aprova cada arquivo antes do próximo.

### Etapa 5 — Pronto pra trabalhar

**O que fazer:**
- Resumo final
- Lista de prompts para próximas tasks
- Backlog detectado durante DISCOVER (sem implementar)
- Sugestão de primeiro commit

**Gate:** humano aprova handover; commit é manual (sem auto-commit).

---

## Anti-padrões durante DISCOVER

| Anti-padrão | Por quê é ruim | Solução |
|---|---|---|
| Modificar código existente | Sai do escopo de DISCOVER | Anotar para fase posterior |
| Inferir sem evidência | Documentação fica errada | Marcar `[?]` e perguntar |
| Pular Etapa 2 e ir direto pra SPECs | Sem brief = SPECs descontextualizadas | Sequência rigorosa |
| Criar 10 SPECs de uma vez | Humano não consegue revisar | Uma por vez com gate |
| Sugerir refactor durante DISCOVER | Confunde escopo | Anotar para backlog |
| Não criar ADRs retrospectivas | Decisões viram tribal | Identificar e propor |

---

## Caso especial: projeto que JÁ TEM um pouco de docs

Se durante Etapa 1 detectar README.md atualizado, `docs/architecture.md`, ou
qualquer documentação parcial:

1. NÃO ignore — leia primeiro.
2. Use como base, não substitua.
3. Em Etapa 4, crie artefatos SDD que **complementam** o que existe.
4. Em handover, mencione: "Documentação prévia preservada em <local>; SDD adiciona estrutura sem substituir."

---

## Tempo esperado

| Tamanho do projeto | Tempo total estimado |
|---|---|
| Pequeno (<5k LOC, ≤5 módulos) | 30-45 min |
| Médio (5-20k LOC, 5-15 módulos) | 1-2h |
| Grande (>20k LOC, >15 módulos) | 2-4h, considerar quebrar em sessões |

> Se DISCOVER passa de 4h numa sessão, gerar handover parcial e continuar
> próxima sessão (Etapa N onde parou).

---

*Ver `prompts/DISCOVER.md` para o prompt copy-paste que orienta o usuário.*
