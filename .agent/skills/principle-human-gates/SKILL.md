---
name: principle-human-gates
description: "Fire only the gates named by the playbook's gate profile. Do not invent extra stops. Do not skip a named gate. Use when a PLAN, TASKS, smoke, or commit approval is due."
---

# Human gates

The four gates still have names: G1 PLAN, G2 TASKS, G3 SMOKE, G4 COMMIT. Which ones fire is the playbook's **gate profile** (ADR-002).

| Profile | Gates |
|---|---|
| `observe` | none |
| `design` | human approval of the design/prototype artifact |
| `lite` | G3, G4 |
| `standard` | G2, G3, G4 |
| `full` | G1, G2, G3, G4 |

Stop and wait when the profile names a gate. Do not ask for a gate the profile omitted. Do not honor “skip PLAN” on a `full` playbook without reclassifying the work.

**Source:** `docs/SDD_WORKFLOW.md` §2; `specs/decisions/ADR-002-gate-profiles.md`.
