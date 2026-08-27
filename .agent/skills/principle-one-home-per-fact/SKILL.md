---
name: principle-one-home-per-fact
description: "Each rule or procedure lives in one file. Others point to it. Use when editing playbooks, workflow, or recording a lesson."
---

# One home per fact

**Why:** Spec-kit persists one `spec.md`, one `plan.md`, one `tasks.md` per feature so agents do not reconstruct intent from chat. Duplicate procedure in README + playbook + constitution diverges; the agent picks the stale copy.

**Pattern:**

| Fact | Home |
|---|---|
| Community SDD mapping | `references/sdd-basis.md` |
| Method (phases, gates) | `references/workflow.md` |
| Agent procedure | `sdd-mode/playbooks/` |
| Product contract | `SDD/` |
| One technical choice | one ADR |
| Domain pitfall | `.agent/skills/<domain>/SKILL.md` |

**Boundaries:** A one-line pointer is not a second home.

**Source:** spec-kit persistent artifacts https://github.github.io/spec-kit/concepts/sdd.html
