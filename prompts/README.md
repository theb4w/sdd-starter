# prompts

Ponte humana para a skill de modo. Os passos canônicos estão em
`.agent/skills/sdd-mode/playbooks/`.

Invoque `sdd-mode` (ou cole o bloco curto do prompt). Não trate estes arquivos
como segunda cópia do procedimento.

| Prompt | Playbook | Perfil |
|---|---|---|
| `BOOTSTRAP.md` | `bootstrap.md` | `full` |
| `DISCOVER.md` | `discover.md` | `observe` |
| `ONBOARDING.md` | `onboarding.md` | `observe` |
| `RESUME.md` | `resume.md` | herda |
| `NEW_FEATURE.md` | `feature.md` | `standard` / `full` |
| `BUG_FIX.md` | `bug-fix.md` | `lite` |
| `REFACTOR.md` | `refactor.md` | `lite` / `full` |
| `HANDOVER.md` | `handover.md` | n/a |

Cenários sem prompt dedicado (só playbook): `investigation`, `design`, `prototype`, `user-story`, `tdd-implement`, `multi-phase`.
