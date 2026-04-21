# scripts/

Scripts operacionais do projeto. Convenções abaixo.

---

## Convenções

### Nomenclatura

- `setup-*.sh` — provisionar recurso (cloud, DB, secret, etc.)
- `deploy-*.sh` — deployar para ambiente (staging/prod)
- `smoke-*.sh` — smoke tests pós-deploy
- `migrate-*.sh|.py` — migrações de dados
- `audit-*.py` — auditoria/relatório (sem efeito colateral)
- `cleanup-*.sh` — limpeza de recursos

### Linguagem

- **Bash** para orquestração simples (≤100 linhas).
- **Python** quando lógica fica complexa (loops, JSON, APIs).
- Evitar PowerShell em projetos cross-platform.

### Header obrigatório

Todo script começa com:

```bash
#!/usr/bin/env bash
# 
# scripts/<nome>.sh — <propósito em 1 linha>
#
# Pré-condições:
# - <ex.: gcloud autenticado>
# - <ex.: variável X exportada>
#
# Uso:
#   bash scripts/<nome>.sh <args>
#
# Side-effects:
# - <ex.: cria recurso Y>
# - <ex.: modifica configuração Z>

set -euo pipefail   # fail-fast
```

### Idempotência

> Rodar 2x o mesmo script não deve quebrar nada.

- `setup-*`: verificar se recurso já existe antes de criar
- `migrate-*`: rastrear migrações aplicadas (timestamps em DB)
- `deploy-*`: tag imutável (commit SHA), nunca `:latest`

### Aprovação humana

Scripts destrutivos (delete, rollback, drop) DEVEM ter prompt de confirmação:

```bash
read -p "Tem certeza? Vai deletar X. (yes/no) " confirm
[[ "$confirm" == "yes" ]] || { echo "Cancelado."; exit 1; }
```

---

## Scripts típicos por categoria

### Setup (uma vez por projeto)
- `setup-gcp.sh` — service account, APIs, project bindings
- `setup-firestore-indexes.sh` — provisionar índices
- `setup-secrets.sh` — popular Secret Manager

### Deploy
- `deploy-staging.sh` — build + deploy staging + smoke automático
- `deploy-production.sh` — promote staging → produção (com gate humano)

### Smoke
- `smoke-staging.sh` — validar 3 fluxos críticos pós-deploy
- `smoke-production.sh` — sanity check pós-promote

### Auditoria
- `list-users.py` — listar usuários (sem PII em log)
- `audit-costs.py` — relatório de custo por módulo
- `audit-security.py` — checklist de segurança

### Migração
- `migrate-from-X-to-Y.py` — rotação de provider/schema
- `cleanup-old-resources.sh` — limpar recursos não-utilizados após migração

---

## Ver também

- `docs/SDD_WORKFLOW.md` §10 (Deploy + Smoke)
- `docs/SDD_WORKFLOW.md` §15 (Lições / Troubleshooting)
- `.agent/workflows/deploy_staging.md` (workflow operacional padrão)
