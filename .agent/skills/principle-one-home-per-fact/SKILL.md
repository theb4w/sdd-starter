---
name: principle-one-home-per-fact
description: "Each rule or procedure lives in one file. Others point to it. Use when editing prompts, playbooks, workflow docs, or adding a lesson from a session."
---

# One home per fact

| Fact | Home |
|---|---|
| Method (what/why/when) | `docs/SDD_WORKFLOW.md` |
| Agent procedure (how, now) | `.agent/skills/sdd-mode/playbooks/` |
| Persisted contract | `specs/`, `docs/` templates |
| A single technical choice | one ADR |
| A domain pitfall | `.agent/skills/<domain>/SKILL.md` |

After a session, put the lesson in that home. Do not add a parallel paragraph in a prompt, a comment, and the workflow.

**Source:** SPEC_SDD_MODE §3.1; skill-design “one home per fact”.
