<!--
═══════════════════════════════════════════════════════════════════════════════
  prompts/HANDOVER.md — Encerrar sessão gerando handover formal
═══════════════════════════════════════════════════════════════════════════════

  USE QUANDO:
  - Acabou de fechar uma fase (sucesso)
  - Vai pausar a sessão por > 30 min (mesmo que não fechou fase)
  - Após deploy + smoke
  - Sessão chegou no limite (>2h ou contexto saturado)

  RESULTADO ESPERADO: arquivo docs/handover_<MODULO>_<DATA>.md criado
  seguindo o template, sem commit (humano revisa primeiro).
═══════════════════════════════════════════════════════════════════════════════
-->

# HANDOVER — Encerrar sessão e gerar handover formal

```
Antes de encerrar a sessão atual, gere docs/handover_<MODULO>[_FASE_<X>]_<DATA>.md
seguindo RIGOROSAMENTE o template em docs/_HANDOVER_TEMPLATE.md.

CONTEÚDO OBRIGATÓRIO (preencher TODAS as seções, mesmo se "N/A"):

1. O Que Esta Sessão Entregou
   - 1-2 parágrafos descrevendo escopo concreto
   - Sem adjetivos vazios ("ótimo", "robusto") — fatos verificáveis

2. Tarefas Concluídas
   - Tabela com IDs (T-X1, T-X2, ...) e ACs verificados

3. Métricas Entregues vs. Estimadas
   - LOC, # de testes novos, cobertura, regressões, tempo
   - Δ explicado se >20% off da estimativa

4. Estado da Infra
   - Ambiente staging: serviço, revision, imagem, URL, custo 24h
   - Repositório: branch, commit hash atual, PRs abertos/merged
   - Recursos novos provisionados nesta sessão

5. Decisões Reafirmadas
   - ADRs validadas na prática (com evidência)
   - Mudanças de comportamento detectadas (não regressão)

6. Pendências (não bloqueiam próxima fase)
   - Cleanup
   - Operacional
   - Documentação

7. Próximos Passos
   - Próxima fase / tarefa / módulo
   - Pré-condições necessárias
   - Quem ou o que aguarda

8. Como Retomar
   - Cole o template prompts/RESUME.md preenchido com:
     * COMMIT_HASH atual
     * Próxima tarefa (T-X1) com AC
     * Lista de ADRs aceitos
     * Datas dos GATEs já aprovados

9. Observações Operacionais (opcional)
   - Aprendizados desta sessão úteis para a próxima

APÓS GERAR O HANDOVER:
1. Atualize specs/SPEC_INDEX.md:
   - Status do módulo (🚧 → ✔️ se foi última fase)
   - Adicione 1 linha no §"Histórico de Mudanças no Projeto"

2. NÃO COMMITE. Apenas gere os arquivos para revisão humana.

3. Mostre resumo final:
   - "Handover gerado: docs/handover_<X>_<DATA>.md"
   - "SPEC_INDEX.md atualizado: módulo Y status Z"
   - "Aguardando sua revisão antes de commit"

4. Sugira o comando de commit (sem executar):
   git add docs/handover_*.md specs/SPEC_INDEX.md
   git commit -m "docs(handover): <MODULO> Fase <X> concluída (<resumo>)"
```

---

## Quando NÃO usar este prompt

- Tarefas pequenas dentro da mesma fase (não acumular handover por tarefa)
- Sessão muito curta (<15 min) sem mudança real
- Apenas leitura/exploração sem deliverable

---

## Checklist do humano antes de aprovar o handover

- [ ] Todos os deliverables da sessão estão listados em §1?
- [ ] Tabela de tarefas em §2 corresponde ao TASKS_<MODULO>.md?
- [ ] Estado da infra em §4 está correto (commit hash, revision, URL)?
- [ ] §6 (Pendências) lista tudo que ficou faltando (sem omissão)?
- [ ] §7 (Próximos passos) é acionável pela próxima sessão?
- [ ] §8 (Como Retomar) tem prompt RESUME.md preenchido corretamente?

Se sim a tudo: aprovar e commitar conforme sugestão.
