---
name: sdd-mode
description: "Sticky SDD mode. Creates SDD/ and routes work through playbooks (bootstrap, discover, bug-fix, feature, refactor, design, user-story, tdd, investigation, prototype, resume, handover, onboarding, multi-phase). Use when the user runs /sdd-mode, asks to follow SDD, or starts a feature, bug, refactor, design, story, greenfield, or brownfield task."
---

# SDD mode

Sticky. Once entered, apply on any turn that matches a playbook or needs rigor. Stay out of casual chat. Opt out when the user says so.

This skill **is** the method's procedure. Project artifacts are generated under `SDD/` at the target repo root. Do not scatter process files in `specs/`, `docs/`, `prompts/`, or `QUICKSTART/`. Do not treat this as a Cursor-only plugin.

Method reference (what/why): `references/workflow.md`. Folder contract: `references/layout.md`.

## Non-negotiables

1. **Ensure `SDD/` first.** Before matching a playbook, run [Create or reuse SDD/](#create-or-reuse-sdd).
2. Start every multi-step task with a todo list whose next items are: read the Principles index below, then **copy the matched playbook's steps verbatim**. Do not rewrite the playbook into a bespoke plan that drops named gates.
3. A skipped step stays in the list as `skip: <motivo>`. Silent skip is forbidden.
4. Match a playbook before reasoning about the solution. If none fit, say so and use `investigation.md` or ask the human to pick.
5. **Stop at the playbook's gates** (`principle-stop-at-gate`). Do not apply “never block on the human” or “the best spec is code”.
6. Production code only after the playbook's contract (`principle-spec-first`). Write that contract inside `SDD/`.
7. Name each principle that changed a decision, with the choice it changed.

## Create or reuse SDD/

If `SDD/` does not exist in the **target** repo:

1. Create the directories in `references/layout.md`.
2. Copy templates from `.agent/skills/sdd-mode/templates/` to the paths in that table (`sdd-readme.md` → `SDD/README.md`, `brief.md` → `SDD/BRIEF.md`, `agents.md` → `SDD/AGENTS.md`, `index.md` → `SDD/INDEX.md`). Do not fill BRIEF/AGENTS with invented product facts; leave placeholders unless this playbook is `discover` or the human already provided a brief.
3. Tell the human: process lives in `SDD/` from now on.

If `SDD/` exists, use it. If you find leftover `specs/` or `docs/` process files from an older starter, migrate them into `SDD/` in this session (do not maintain two trees).

Never create `scripts/`, empty `tests/` trees, `prompts/`, or `QUICKSTART/` as part of SDD.

## Principles

Read the leaf skill in full when you apply it.

**Absolute:** `principle-spec-first`, `principle-human-gates`, `principle-primary-source`, `principle-privacy-logging`, `principle-no-secrets`, `principle-backward-compat`, `principle-traceability`.

**Mode:** `principle-proportional-rigor`, `principle-stop-at-gate`, `principle-prove-it-works`, `principle-tdd-red-green`, `principle-sequence-verifiable-units`, `principle-one-home-per-fact`.

## Gate profiles

| Profile | Gates | Production code |
|---|---|---|
| `observe` | none | no |
| `design` | human approval of the design/prototype file | no |
| `lite` | G3 SMOKE, G4 COMMIT | yes |
| `standard` | G2 TASKS, G3, G4 | yes |
| `full` | G1 PLAN, G2, G3, G4 | yes |

The playbook declares the profile. Heavier is always allowed. Lighter requires reclassifying the work in the open.

## Playbooks

Copy steps from `playbooks/<file>.md`. All write under `SDD/`.

| When | File | Profile |
|---|---|---|
| New project; BRIEF filled or about to be | `bootstrap.md` | `full` per module |
| Existing project, weak or no docs | `discover.md` | `observe` until brief |
| Read-only how/why | `investigation.md` | `observe` |
| Shape before SPEC | `design.md` | `design` |
| Throwaway sketch | `prototype.md` | `design` |
| Vertical slice on an existing module SPEC | `user-story.md` | `standard` or `lite` |
| Defect | `bug-fix.md` | `lite` |
| New or changed behavior | `feature.md` | small `standard`; medium/large `full` |
| Structure change | `refactor.md` | internal `lite`; architectural `full` |
| IMPLEMENT with TDD on an approved unit | `tdd-implement.md` | inherit |
| Multi-phase SPEC | `multi-phase.md` | `full` per phase |
| Continue after handover | `resume.md` | inherit |
| End the session | `handover.md` | n/a |
| First session on a repo that already has `SDD/` | `onboarding.md` | `observe` |

## Subagents

If the environment can spawn subagents, the lead owns design, gates, and review. Delegates implement a named TASK. The lead reads the diff.

## Reply

Name the playbook, profile, and `SDD/` paths in the first lines. Link only files you read or wrote this session.
