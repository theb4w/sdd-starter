# TASKS_SDD_CORE_NEUTRALITY - Primeira refatoracao editorial

**Status:** primeira implementacao concluida; aguardando revisao humana
**Data:** 2026-05-22
**PLAN base:** `specs/plans/PLAN_SDD_CORE_NEUTRALITY.md`

| ID | Tarefa | Onde | Criterio de aceite |
|---|---|---|---|
| T-1 | Reposicionar a porta de entrada para SDD-first | `README.md` | leitor entende metodo, caminhos e independencia de stack/tooling antes de extras |
| T-2 | Neutralizar instrucoes centrais para agentes e humanos | `AGENTS.md` | core nao prescreve IDE ou agente especifico |
| T-3 | Neutralizar workflow canônico | `docs/SDD_WORKFLOW.md` | fases usam linguagem SDD, nao modos/comandos de ferramenta |
| T-4 | Ajustar adocao greenfield e brownfield | `QUICKSTART/` | caminho padrao copia/adota o core sem tooling especifico |
| T-5 | Separar tooling opcional | `tooling/` | notas especificas ficam fora do caminho principal |
| T-6 | Validar residuos e diff | repo | busca por claims tool-specific no core e `git diff` revisados |
