# SDD/ layout

All project process artifacts live in `SDD/` at the **target repo root**. The skill never writes SPEC, ADR, PLAN, TASKS, story, design, brief, index, or handover outside this tree.

```text
SDD/
├── README.md           ← what this folder is
├── BRIEF.md            ← project brief
├── AGENTS.md           ← product constitution (absolute rules)
├── INDEX.md            ← modules, ADRs, next steps
├── architecture.md     ← system view (optional until bootstrap)
├── modules/SPEC_*.md
├── stories/STORY_*.md
├── plans/PLAN_*.md
├── plans/TASKS_*.md
├── decisions/ADR-NNN-*.md
├── design/<slug>.md
└── handovers/handover_*.md
```

Templates live next to `SKILL.md` (resolve skill root — `references/skill-root.md`). Copy from that `templates/` folder:

| Generate | From |
|---|---|
| `SDD/README.md` | `templates/sdd-readme.md` |
| `SDD/BRIEF.md` | `templates/brief.md` |
| `SDD/AGENTS.md` | `templates/agents.md` |
| `SDD/INDEX.md` | `templates/index.md` |
| `SDD/architecture.md` | `templates/architecture.md` |
| `SDD/modules/SPEC_<M>.md` | `templates/spec.md` |
| `SDD/plans/PLAN_<M>.md` | `templates/plan.md` |
| `SDD/plans/TASKS_<M>.md` | `templates/tasks.md` |
| `SDD/decisions/ADR-NNN-*.md` | `templates/adr.md` |
| `SDD/stories/STORY_<S>.md` | `templates/story.md` |
| `SDD/design/<slug>.md` | `templates/design.md` |
| `SDD/handovers/handover_*.md` | `templates/handover.md` |

On Cursor hosts, if `.cursor/rules/sdd-under-pstack.mdc` is missing, copy `templates/cursor-rule.mdc` there (Step 0).

Do not create `specs/`, `docs/`, `prompts/`, `QUICKSTART/`, `scripts/`, or empty `tests/` as SDD process folders.
