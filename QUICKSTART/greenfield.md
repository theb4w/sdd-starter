# QUICKSTART — Greenfield (projeto do zero)

> **Cenário:** você vai começar um projeto novo, do zero, e quer aplicar SDD desde o commit inicial.
>
> **Tempo total esperado:** 1-2h até ter o primeiro PLAN aprovado e estar pronto para implementar.
>
> **Pré-requisito:** Git instalado, ambiente de trabalho escolhido e conta GitHub/GitLab se houver remoto.
>
> **Playbook:** `.agent/skills/sdd-mode/playbooks/bootstrap.md` · **Perfil:** `full` · invoque `sdd-mode`

---

## Passo 0 — Tenha clareza do que vai fazer

Antes de tocar em código ou template, escreva (numa folha, num bloco de notas):

1. **O que é o projeto** em 1 frase
2. **Para quem** (1 frase)
3. **Que problema concreto resolve** (1 frase)
4. **Contexto técnico já decidido** (se houver linguagem, plataforma ou restrição)
5. **Restrições** (compliance, prazo, orçamento)

Se não consegue responder essas 5 em 5 minutos, **PARE**. O projeto ainda não está claro o suficiente.
Volte aqui depois de uma conversa com stakeholder ou de uma session com pen&paper.

---

## Passo 1 — Crie o repo a partir deste template

### Opção A — Use o GitHub (template repo)

1. Abra https://github.com/<sua-org>/sdd-starter
2. Clique em **Use this template** → **Create a new repository**
3. Nome: `<seu-projeto>` (kebab-case, descritivo)
4. Privacy: **Private** se for projeto da empresa; **Public** se for OSS
5. Clone localmente:
   ```bash
   git clone https://github.com/<sua-org>/<seu-projeto>.git
   cd <seu-projeto>
   ```

### Opção B — Copie manualmente do template local

```bash
# Windows PowerShell
Copy-Item -Recurse C:\dev\sdd-starter C:\dev\<seu-projeto>
cd C:\dev\<seu-projeto>
Remove-Item -Recurse -Force .git
git init -b main
git add .
git commit -m "chore: initial commit from sdd-starter template"
```

```bash
# macOS/Linux
cp -R ~/dev/sdd-starter ~/dev/<seu-projeto>
cd ~/dev/<seu-projeto>
rm -rf .git
git init -b main
git add .
git commit -m "chore: initial commit from sdd-starter template"
```

---

## Passo 2 — Preencha PROJECT_BRIEF.md

Abra `PROJECT_BRIEF.md` e preencha as seções §1-§5:

| Seção | O que escrever | Quanto tempo |
|---|---|---|
| §1 Objetivo | 1 parágrafo: o que faz, para quem, problema |
| §2 Contexto técnico | Decisões, preferências e restrições já conhecidas |
| §3 Restrições | Compliance, prazo, orçamento, time disponível |
| §4 Módulos esperados | Lista de 3-7 módulos com 1 frase cada |
| §5 Out-of-MVP | Lista do que NÃO vai entrar nesta versão |
| §6 Métricas de sucesso | Como vai medir que funcionou (3-5 métricas concretas) |

**Dicas:**
- Se uma decisão técnica ainda está aberta, registre a dúvida; CLARIFY ou ADR resolvem depois
- §4 (módulos) não precisa estar perfeito — vai refinar com agente em BOOTSTRAP
- §5 (out-of-MVP) é o mais importante — é o filtro de scope creep

Não deixe nenhum campo `[?]` — esses são para o agente preencher em DISCOVER, não para greenfield.

---

## Passo 3 — Adapte AGENTS.md (manualmente OU via agente)

### Opção A — Manualmente (10-20 min)

Abra `AGENTS.md` e substitua todos os `<!-- ADAPT: ... -->`:

| Placeholder | Como decidir |
|---|---|
| `<!-- ADAPT: NOME_DO_PROJETO -->` | Nome real do projeto |
| `<!-- ADAPT: IDENTIDADE -->` | Cole §1 do PROJECT_BRIEF |
| `<!-- ADAPT: STACK -->` | Contexto técnico do §2 do PROJECT_BRIEF, com fontes quando houver decisão |
| `<!-- ADAPT: ESTRUTURA -->` | Estrutura de diretórios da sua stack |
| `<!-- ADAPT: REGRAS_PROJETO -->` | Regras absolutas específicas (compliance, perf) |

URLs de fonte primária são **obrigatórias** para decisões técnicas relevantes.
Exemplos do projeto podem apontar para documentação oficial da stack escolhida.

### Opção B — Com assistencia

Abra o agente ou canal de assistencia adotado no projeto e cole:

```
Invoque `sdd-mode` com o playbook `bootstrap.md` (ponteiro: `prompts/BOOTSTRAP.md`).

Estamos em modo greenfield. PROJECT_BRIEF.md já está preenchido.
Adapte AGENTS.md substituindo todos os placeholders <!-- ADAPT --> com base no brief.
Mostre o AGENTS.md final antes de salvar e aguarde meu GO.
```

---

## Passo 4 — Use BOOTSTRAP para criar SDD inicial

Envie ao agente escolhido (substituindo só o nome do projeto):

```
Vou usar prompts/BOOTSTRAP.md para inicializar SDD em <NOME_PROJETO>.

PROJECT_BRIEF.md já está preenchido. AGENTS.md já adaptado (ou adapte se ainda não).

Siga as 8 etapas do BOOTSTRAP exatamente:
1. Leitura inicial → análise + módulo crítico sugerido
2. Adaptar AGENTS.md (se ainda não)
3. Architecture document v1
4. SPEC_INDEX inicial
5. SPEC do módulo crítico
6. ADRs (se trade-offs)
7. PLAN (parar no GATE 1)
8. Handover de bootstrap

Pare em CADA etapa para meu GO. Não pule passos.
```

O agente vai:
1. Ler `AGENTS.md`, `SDD_WORKFLOW.md`, `PROJECT_BRIEF.md`, templates
2. Sugerir um **módulo crítico** para começar (você confirma ou troca)
3. Gerar `docs/<NOME>_Architecture.md` v1
4. Gerar `specs/SPEC_INDEX.md` inicial
5. Gerar `specs/modules/SPEC_<MODULO_CRITICO>.md`
6. Listar perguntas CLARIFY (você responde)
7. Propor ADRs se houver trade-off (você aprova/rejeita)
8. Gerar `specs/plans/PLAN_<MODULO>.md` → **GATE 1**
9. Gerar handover de bootstrap

---

## Passo 5 — Aprove GATE 1 e gere TASKS

Após GATE 1 aprovado, cole:

```
PLAN aprovado. Gere agora specs/plans/TASKS_<MODULO>.md baseado em
specs/plans/_TASKS_TEMPLATE.md.

Regras:
- Tarefas atômicas (1 commit cada)
- ID estável (T-1.1, T-1.2... ou T-A1, T-A2 se multi-fase)
- AC verificável (comando ou condição)
- Última tarefa = commit; penúltima = smoke; antepenúltima = validação completa definida pelo projeto
- Tarefas [bloq.] = gates humanos (mostrar com 🛑)

🛑 GATE 2 — pare ao final aguardando minha aprovação das TASKS.
```

---

## Passo 6 — Implemente (1 tarefa por vez)

Após GATE 2 aprovado, cole:

```
TASKS aprovadas. Use .agent/workflows/sdd_implement.md.

Comece pela tarefa T-<ID> (primeira não-bloq).

Para CADA tarefa:
1. Anuncie a tarefa que vai começar
2. Implemente apenas o necessário
3. Verifique AC (rode comando indicado)
4. Mostre diff
5. Aguarde meu GO antes da próxima

Ao chegar em tarefa [bloq.] = pare e me avise.
```

Loop até fim da fase (ou do PLAN single-phase).

---

## Passo 7 — Smoke + Commit + Handover

No fim da fase:

```
Tarefas implementadas. Próximos passos do workflow:

1. 🛑 GATE 3 — Smoke aplicável (fluxos críticos no ambiente-alvo)
2. 🛑 GATE 4 — Commit (Conventional Commit)
3. Use prompts/HANDOVER.md para gerar handover_<MODULO>_FASE_<X>_<DATA>.md
4. Atualize specs/SPEC_INDEX.md (status do módulo)
5. Sugira mensagem de commit (HEREDOC)

Eu executo o git commit manualmente.
```

---

## Passo 8 — Push para o remoto

```bash
# Crie o repo remoto (se ainda não tem)
gh repo create <sua-org>/<seu-projeto> --private --source=. --remote=origin

# Push
git push -u origin main
```

---

## Próxima sessão (continuidade)

Use `prompts/RESUME.md` colando-o e preenchendo:

```
Retomar <NOME_PROJETO> — iniciar SPEC_<MODULO> Fase <X> (<descrição_curta>).

LEIA NESTA ORDEM:
1. AGENTS.md
2. instruções opcionais de tooling adotadas pelo projeto
3. docs/handover_<MODULO>_FASE_<X-1>_<DATA>.md
4. specs/SPEC_INDEX.md
5. specs/modules/SPEC_<MODULO>.md §<seção>
6. specs/plans/PLAN_<MODULO>.md §"Fase <X>"
7. specs/plans/TASKS_<MODULO>.md §"Fase <X>"

GATEs aprovados: G1=<sim/não>, G2=<sim/não>, G3=<sim/não>, G4=<sim/não>.
Próxima tarefa: T-<X>1.
```

---

## Checklist final do greenfield

Antes de considerar o BOOTSTRAP completo:

- [ ] PROJECT_BRIEF.md sem nenhum `[?]`
- [ ] AGENTS.md sem nenhum `<!-- ADAPT -->` não-resolvido
- [ ] docs/<NOME>_Architecture.md v1 com diagrama mermaid funcional
- [ ] specs/SPEC_INDEX.md listando todos os módulos do brief §4
- [ ] Pelo menos 1 SPEC criada (módulo crítico)
- [ ] PLAN do módulo crítico ✔️ APROVADO (GATE 1)
- [ ] Handover de bootstrap em docs/
- [ ] Commit inicial pushed

---

## Erros comuns no greenfield

| Erro | Sintoma | Solução |
|---|---|---|
| Pular §5 do brief (out-of-MVP) | Scope creep depois | Liste 5+ coisas que NÃO vão entrar |
| AGENTS.md sem URLs de fonte | Decisões viram opinião | Toda tech tem URL oficial |
| 5 módulos em paralelo | Sem foco; PRs gigantes | 1 SPEC por vez, módulo crítico primeiro |
| Pular GATE 1 ("é simples") | Implementação diverge da SPEC | GATE 1 é não-negociável |
| Sem handover ao fim do dia | Próxima sessão começa do zero | HANDOVER.md a cada pausa de >24h |
| Commit gigante "feat: tudo" | Histórico inútil | 1 tarefa = 1 commit |

---

## Quando NÃO usar greenfield workflow

- Se já existe código → use **brownfield.md** (com DISCOVER se sem docs)
- Se for prova de conceito de 2h → SDD overhead não compensa; rascunhe livre, depois adote SDD se virar projeto

---

*Veja também: `QUICKSTART/brownfield.md` para projeto existente, `prompts/BOOTSTRAP.md` para o prompt detalhado.*
