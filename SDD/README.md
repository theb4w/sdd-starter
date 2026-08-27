# SDD

Pasta de processo deste projeto, gerada por `sdd-mode`.

Não edite o método aqui. O método e os playbooks vivem na skill
(`sdd-mode/` no skill root do host — ver `references/skill-root.md`).
Aqui ficam só os artefatos **deste** produto.

| Arquivo | Papel |
|---|---|
| `BRIEF.md` | Escopo inicial |
| `AGENTS.md` | Regras absolutas do produto |
| `INDEX.md` | Status de módulos e ADRs |
| `architecture.md` | Visão técnica |
| `modules/` | SPECs |
| `stories/` | User stories (exigem SPEC de módulo) |
| `plans/` | PLAN e TASKS |
| `decisions/` | ADRs |
| `design/` | Exploração antes de SPEC |
| `handovers/` | Estado retomável |

Invocar `sdd-mode` e deixar o playbook escrever nesta pasta.

`AGENTS.md` precisa de **`Smoke:`** (neste pack: `sdd-mode/references/dry-run.md`). Sem evidência G3 o pacote não aceita.
