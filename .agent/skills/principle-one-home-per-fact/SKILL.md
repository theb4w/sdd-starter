---
name: principle-one-home-per-fact
description: "Each rule or procedure lives in one file. Others point to it. Use when editing prompts, playbooks, workflow docs, or adding a lesson from a session."
---

# One home per fact

| Fact | Home |
|---|---|
| Method (what/why/when) | `.agent/skills/sdd-mode/references/workflow.md` |
| Agent procedure (how, now) | `.agent/skills/sdd-mode/playbooks/` |
| Persisted contract | `SDD/` |
| A single technical choice | one file in `SDD/decisions/` |
| A domain pitfall | `.agent/skills/<domain>/SKILL.md` |

After a session, put the lesson in that home. Do not add a parallel paragraph in a prompt, a comment, and the workflow.

**Source:** SPEC_SDD_MODE §3.1; skill-design “one home per fact”.
