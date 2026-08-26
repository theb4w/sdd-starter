---
name: principle-spec-first
description: "No production code without the playbook's approved contract. Contract may be a SPEC, a user story, or none (bug-fix). Use when tempted to implement before specify."
---

# Spec-first

Do not write production code until the playbook's contract exists and, if the gate profile requires it, has been approved.

**When:** any path that would change runtime behavior.

**What counts as contract**

| Playbook | Contract |
|---|---|
| feature (média/grande), bootstrap, refactor arquitetural | `SDD/modules/SPEC_*.md` |
| feature pequena, user-story | SPEC existente estendida, ou story ligada a SPEC de módulo |
| bug-fix | nenhum novo; comportamento esperado já documentado ou o repro |
| design, prototype, investigation | não geram código de produção |

**Do not:** treat a chat agreement as a SPEC. Write the file.

**Source:** `SDD/AGENTS.md` regra 1 (after generate); `references/workflow.md` §1.1.
