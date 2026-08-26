---
name: sdd-mode
description: "Sticky SDD mode. Routes work through Spec-Driven Development playbooks (bootstrap, discover, bug-fix, feature, refactor, design, user-story, tdd, investigation, prototype, resume, handover, onboarding, multi-phase). Use when the user runs /sdd-mode, asks to follow SDD, or starts a feature, bug, refactor, design, story, greenfield, or brownfield task."
---

# SDD mode

Sticky. Once entered, apply on any turn that matches a playbook or needs rigor. Stay out of casual chat. Opt out when the user says so.

This is the agent procedure for Spec-Driven Development. The method itself lives in `docs/SDD_WORKFLOW.md`. Do not replace that document. Do not treat this skill as a Cursor-only plugin (ADR-001).

## Non-negotiables

1. Start every multi-step task with a todo list whose **first** items are: read the Principles index below, then **copy the matched playbook's steps verbatim**. Do not rewrite the playbook into a bespoke plan that drops named gates.
2. A skipped step stays in the list as `skip: <motivo>`. Silent skip is forbidden.
3. Match a playbook before reasoning about the solution. If none fit, say so and use `investigation.md` or ask the human to pick. Do not invent a 23rd playbook in-session.
4. **Stop at the playbook's gates** (`principle-stop-at-gate`). Do not apply pstack “never block on the human” or “the best spec is code”.
5. Production code only after the playbook's contract (`principle-spec-first`).
6. Name each principle that changed a decision, with the choice it changed. A citation with no decision is noise.

## Principles

Read the leaf skill in full when you apply it.

**Absolute**

- **spec-first** (`principle-spec-first`) — no production code without the playbook contract.
- **human-gates** (`principle-human-gates`) — fire the profile's gates only.
- **primary-source** (`principle-primary-source`) — technical choice needs a URL; else ADR blocked.
- **privacy-logging** (`principle-privacy-logging`) — no sensitive content in logs.
- **no-secrets** (`principle-no-secrets`) — no hardcoded credentials.
- **backward-compat** (`principle-backward-compat`) — each commit preserves prior working state.
- **traceability** (`principle-traceability`) — code → TASK/story → SPEC → ADR.

**Mode**

- **proportional-rigor** (`principle-proportional-rigor`) — ceremony matches the scenario.
- **stop-at-gate** (`principle-stop-at-gate`) — block on named gates; do not nag inside an approved TASK.
- **prove-it-works** (`principle-prove-it-works`) — G3 is the real surface, not “it compiles”.
- **tdd-red-green** (`principle-tdd-red-green`) — RED then GREEN when a cheap local test exists.
- **sequence-verifiable-units** (`principle-sequence-verifiable-units`) — one checked unit at a time.
- **one-home-per-fact** (`principle-one-home-per-fact`) — procedure lives in the playbook, not a parallel prompt.

## Gate profiles

| Profile | Gates | Production code |
|---|---|---|
| `observe` | none | no |
| `design` | human approval of the design/prototype file | no |
| `lite` | G3 SMOKE, G4 COMMIT | yes |
| `standard` | G2 TASKS, G3, G4 | yes |
| `full` | G1 PLAN, G2, G3, G4 | yes |

The playbook declares the profile. The user may ask for a *heavier* profile. A lighter one requires reclassifying the work in the open.

Definitions: `specs/decisions/ADR-002-gate-profiles.md`.

## Playbooks

Copy steps from `.agent/skills/sdd-mode/playbooks/<file>.md`.

| When | File | Profile |
|---|---|---|
| New project from a filled brief | `bootstrap.md` | `full` per module |
| Existing project, weak or no docs | `discover.md` | `observe` until brief |
| Read-only how/why | `investigation.md` | `observe` |
| Shape UX/architecture before SPEC | `design.md` | `design` |
| Throwaway sketch to settle a fork | `prototype.md` | `design` |
| Vertical slice on an existing module SPEC | `user-story.md` | `standard` or `lite` |
| Defect | `bug-fix.md` | `lite` |
| New or changed behavior | `feature.md` | small `standard`; medium/large `full` |
| Structure change | `refactor.md` | internal `lite`; architectural `full` |
| IMPLEMENT with TDD on an approved unit | `tdd-implement.md` | inherit |
| Multi-phase / stacked SPEC | `multi-phase.md` | `full` per phase |
| Continue after handover | `resume.md` | inherit |
| End the session | `handover.md` | n/a |
| First session on an SDD repo | `onboarding.md` | `observe` |

## Subagents

If the environment can spawn subagents, the lead **owns** design, gates, and review. Delegates implement a named TASK with file paths, AC, and ADRs. The lead reads the diff; do not paste a delegate summary as truth.

If there are no subagents, the lead still executes every playbook step, including stops at gates.

## Reply

Short sentences. Name the playbook and profile in the first lines. Frame impact for the consumer of the product and the next maintainer. Link only files you read or wrote this session.

Every playbook ends with the reply shape it names.
