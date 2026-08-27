---
name: example-skill
description: "Skill de exemplo — copie este diretório para criar uma SKILL nova"
risk: safe
source: "self"
tags: ["example", "template"]
---

<!--
═══════════════════════════════════════════════════════════════════════════════
  SKILL.md — Template de skill técnica
═══════════════════════════════════════════════════════════════════════════════

  O que é uma SKILL?
  - Conjunto de regras técnicas + exemplos para um domínio específico do projeto
  - Lida pelo agente quando relevante para a tarefa atual
  - Reduz erros recorrentes (ex.: misuse de async, hardcode, padrões errados)

  Como usar este template:
  1. Copie a pasta inteira para o skill root do host: cp -r _example_skill <skill-root>/<nome>
  2. Renomeie a pasta (kebab-case): ex.: firestore-rules, jwt-handling, prisma-orm
  3. Atualize o YAML frontmatter (name, description, tags)
  4. Reescreva conteúdo abaixo conforme o domínio real
  5. Cite-a no AGENTS.md (lista de skills) e nas SPECs relevantes

  Convenções de SKILL:
  - YAML frontmatter obrigatório (name, description, risk, source, tags)
  - Risk: "safe" | "review" | "danger" (orienta gating do agente)
  - Mínimo 3 seções: Quando usar, Regras, Exemplos
  - Exemplos têm ✅ correto e ❌ errado lado-a-lado
  - Toda regra com URL de fonte primária

  Fonte do formato:
  https://github.com/sickn33/antigravity-awesome-skills/blob/main/docs/contributors/skill-anatomy.md
═══════════════════════════════════════════════════════════════════════════════
-->

# <Nome da Skill>

> Skill técnica para <domínio>. Lida automaticamente quando o agente
> trabalha em código relacionado a <descrição>.

---

## Quando usar

Use esta skill quando estiver:
- <cenário 1: ex.: implementando endpoint que escreve em Firestore>
- <cenário 2: ex.: chamando API externa de pagamento>
- <cenário 3: ex.: configurando middleware de autenticação>

NÃO use quando:
- <contra-cenário: ex.: trabalhando com cache em memória local>

---

## Regras

> Cada regra com fonte verificável. Sem URL = remover a regra.

### R1 — <Regra concreta e acionável>

- **Por quê:** <razão técnica>
- **Fonte:** <URL primária>
- **Exemplo:** ver §"Exemplos" abaixo

### R2 — <Regra>

- **Por quê:** <razão>
- **Fonte:** <URL>

### R3 — NUNCA <ação proibida>

- **Motivo:** <explicação do dano>
- **Fonte:** <URL>

---

## Exemplos

### ✅ Correto

```python
# <comentário explicando POR QUE este padrão é correto>
async def buscar_usuario(uid: str) -> User | None:
    async with AsyncClient() as client:
        doc = await client.collection("users").document(uid).get()
        return User(**doc.to_dict()) if doc.exists else None
```

### ❌ Errado

```python
# <comentário explicando o problema>
def buscar_usuario(uid: str) -> User | None:
    # Cliente síncrono dentro de função async = bloqueia event loop
    client = SyncClient()
    doc = client.collection("users").document(uid).get()
    return User(**doc.to_dict()) if doc.exists else None
```

### ⚠️ Aceitável com ressalva

```python
# Aceitável APENAS em scripts CLI (não em Cloud Run / FastAPI async)
def script_offline():
    client = SyncClient()
    ...
```

---

## Checklist mental antes de implementar

- [ ] Estou seguindo R1, R2, R3?
- [ ] Estou usando o cliente correto (async vs sync)?
- [ ] Estou tratando erros tipados (não genéricos)?
- [ ] Estou logando metadados (sem dados sensíveis)?
- [ ] Estou cobrindo o caso "recurso não existe"?

---

## Anti-padrões comuns

| Anti-padrão | Como detectar | Correção |
|---|---|---|
| <ex.: cliente síncrono em async> | `rg "Sync.*Client" app/` | Trocar por `AsyncClient` |
| <anti-padrão> | <comando rg ou lint> | <correção> |

---

## Ver também

- `SDD/architecture.md` §<seção relevante>
- ADR-NNN — <decisão relacionada>
- Skill irmã: `<skill-root>/<outra-skill>/SKILL.md`

---

*Manter atualizado conforme novos pitfalls aparecem em produção.*
