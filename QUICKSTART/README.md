# QUICKSTART

Escolha um guia pelo tipo de trabalho, nao pela ferramenta usada.

Cada quickstart indica o **playbook** em `.agent/skills/sdd-mode/playbooks/`,
o **perfil de gate**, e quais artefatos criar. Os passos canônicos estão no
playbook. Invoque `sdd-mode`; não cole um plano paralelo.

| Se voce quer... | Leia | Playbook | Perfil |
|---|---|---|---|
| Comecar projeto novo | `greenfield.md` | `bootstrap.md` | `full` |
| Adotar SDD em projeto existente | `brownfield.md` | `discover.md` | `observe` |
| Corrigir um bug | `bug-fix.md` | `bug-fix.md` | `lite` |
| Feature pequena | `small-feature.md` | `feature.md` | `standard` |
| Feature media | `medium-feature.md` | `feature.md` | `full` |
| Feature grande ou multi-fase | `large-feature.md` | `feature.md` + `multi-phase.md` | `full` |
| Refatorar | `refactor.md` | `refactor.md` | `lite` / `full` |
| Design sem código | (playbook direto) | `design.md` | `design` |
| User story | (playbook direto) | `user-story.md` | `standard` / `lite` |
| TDD RED-GREEN | (playbook direto) | `tdd-implement.md` | herda |

