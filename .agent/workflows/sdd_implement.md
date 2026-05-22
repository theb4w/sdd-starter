# Workflow: SDD Implement

> Workflow operacional para a fase IMPLEMENT do ciclo SDD.
> Use quando GATE 1 (PLAN) e GATE 2 (TASKS) já foram aprovados pelo humano.

---

## Pré-condições

Antes de iniciar este workflow, confirmar:

- [ ] `specs/modules/SPEC_<MODULO>.md` tem status ✅ APROVADO
- [ ] `specs/plans/PLAN_<MODULO>.md` foi aprovado (GATE 1)
- [ ] `specs/plans/TASKS_<MODULO>.md` foi aprovado (GATE 2)
- [ ] ADRs aplicáveis estão ✔️ ACEITO em `specs/decisions/`
- [ ] `.agent/skills/<dominio>/SKILL.md` da stack relevante foi lido
- [ ] Recursos cloud / DB / secrets provisionados (checklist do PLAN)
- [ ] Workspace está fora de cloud-sync e branch correta

---

## Loop principal

Para cada tarefa `T-<X><N>` na fase atual:

### 1. Confirmar pré-condições da tarefa
- Tarefa anterior verde (AC verificado)
- ADRs aplicáveis ainda válidos
- Nenhum bloqueador externo

### 2. Implementar APENAS o escopo da tarefa
- Não antecipar próxima tarefa
- Não refatorar código não-relacionado
- Respeitar regras da SKILL relevante
- Type hints / docstrings em funções públicas
- Sem `print()`, sem hardcode de credenciais

### 3. Verificar AC localmente
- Rodar o check especifico indicado no AC da task
- Verificar comportamento esperado por teste, comando, log ou observacao aplicavel
- Rodar validadores locais relevantes nos arquivos editados

### 4. Marcar tarefa como concluída
- Atualizar o tracking adotado pelo projeto e o artefato aplicavel
- Não acumular múltiplas tarefas sem AC verde

### 5. Próxima tarefa
- Se fim da fase → ir para "Fim de Fase" abaixo
- Se não → voltar ao passo 1

---

## Fim de Fase (multi-fase)

Antes de fechar a fase:

### 6. Tarefa [bloq.] — Testes full sem regressão
```bash
# Python
pytest -q

# Node
npm test

# Go
go test ./...
```

Resultado esperado: 0 falhas. Se houver regressão, voltar para a tarefa que introduziu.

### 7. Tarefa [bloq.] — Smoke staging (GATE 3)

```bash
bash scripts/deploy-staging.sh
bash scripts/smoke-staging.sh   # ou checklist manual
```

**Aguardar aprovação humana antes de prosseguir.** Se smoke falhar, voltar para IMPLEMENT.

### 8. Tarefa final — Commit + push (GATE 4)

```bash
git add <arquivos da fase>
git status                            # auditoria pré-commit
git diff --cached --name-only | grep -E "(\.env$|\.key$|credentials)" && exit 1
git commit -m "feat(<modulo>): <título da fase>"
# Aguardar revisão humana do diff antes do push
git push origin main
```

### 9. Atualizar SPEC_INDEX.md
- Status do módulo (🚧 → ✔️ se foi última fase)
- Adicionar linha no histórico do projeto

### 10. Gerar handover
```bash
# Use prompts/HANDOVER.md
```

Arquivo: `docs/handover_<MODULO>_FASE_<X>_<DATA>.md`

---

## Quando interromper

- **Trade-off arquitetural não previsto:** parar, criar ADR, retomar PLAN.
- **Tarefa toca >5 arquivos não previstos:** parar, atualizar TASKS, recomeçar.
- **Bug investigativo:** interromper execucao linear e investigar a causa antes de editar mais.
- **Sessão >2h sem fim de fase:** parar, gerar handover parcial, retomar amanhã.

---

## Exemplo de execução de 1 tarefa

```
[T-A2: Implementar funcao service.process_payment]

1. Pré-condições:
   ✓ T-A1 verde (dataclass criada)
   ✓ ADR-005 aceito (provider Stripe)
   ✓ Skill .agent/skills/payment/SKILL.md lida

2. Implementar:
   - Edit app/payments/service.py:process_payment
   - 18 LOC, type hints completos, docstring

3. Verificar AC:
   $ pytest tests/unit/test_payments.py::test_process_payment_happy
   ✓ 1 passed in 0.3s

4. Lint:
   $ ruff check app/payments/service.py
   ✓ No issues found

5. Marcar como concluída no tracking adotado.

6. Próxima: T-A3.
```

---

*Ver `docs/SDD_WORKFLOW.md` §8 para detalhes da fase IMPLEMENT.*
