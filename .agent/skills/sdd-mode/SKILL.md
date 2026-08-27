---
name: sdd-mode
description: "Sticky SDD mode (spec-kit / Antigravity). Default profile agentic: write SPEC/PLAN/TASKS, implement, agent-review, one human package. Creates SDD/. Use for /sdd-mode, feature, bug, refactor, design, story, greenfield, brownfield, review."
---

# SDD mode

Sticky. Apply when a playbook matches or the work needs rigor. Opt out when the user says so.

Community SDD: GitHub spec-kit as adopted by Antigravity. Specs in `SDD/` are the SSOT. Default **agentic** (ADR-003): human on intent and the final package; agent on HOW, code, and review. `full` is explicit high-ceremony. Not pstack never-block; not merge overnight.

Sources: `references/sdd-basis.md`, `references/workflow.md`, `references/layout.md`. ADR-002, ADR-003.

## Non-negotiables

1. **Ensure `SDD/` first** ([below](#create-or-reuse-sdd)).
2. Todo: principles index, then **intent table**, then copy the playbook steps verbatim. Silent skip forbidden (`skip: motivo`).
3. **Spec-first:** contract in `SDD/` before production code (bug: none new).
4. **Stop only where the profile says.** `agentic` does **not** stop at G1/G2. Always stop for product-only CLARIFY, G3 evidence in the package, irreversible ops.
5. After code: run `review.md` then G3, then **one human package**. Commit on a **branch**, not silent `main`.
6. Promote to `full` when: new schema/external service, compliance/money/health, WHAT unclear, or the user asked.

## Create or reuse SDD/

If `SDD/` is missing: create dirs in `layout.md`; copy `templates/` (`sdd-readme`→`README.md`, `brief`→`BRIEF.md`, `agents`→`AGENTS.md`, `index`→`INDEX.md`). Do not invent product facts except on `discover` or a filled brief.

If leftover `specs/` or `docs/` process trees exist, migrate into `SDD/` this session.

Never create `scripts/`, empty `tests/`, `prompts/`, or `QUICKSTART/` as SDD process.

## Intent → playbook (match this first)

| If the request sounds like | Family | Playbook | Default profile |
|---|---|---|---|
| New project, I know the brief | Arrive | `bootstrap.md` | `agentic` |
| Legacy repo, no docs | Arrive | `discover.md` | `observe` (stop on BRIEF) |
| First chat, `SDD/` already there | Arrive | `onboarding.md` | `observe` |
| How / why / are we sure / blast radius | Understand | `investigation.md` | `observe` |
| Review this diff / PR | Understand | `review.md` | `observe` |
| Shape / UX still open | Shape | `design.md` | `design` |
| Two sketches / experiment | Shape | `prototype.md` | `design` |
| Broken / repro | Change | `bug-fix.md` | `lite` |
| User should be able to X (module SPEC exists) | Change | `user-story.md` | `agentic` |
| New behavior | Change | `feature.md` | `agentic` (`full` if schema/service/compliance) |
| Reshape, same contract | Change | `refactor.md` | `lite` |
| Reshape, public contract | Change | `refactor.md` | `full` |
| Large / many modules | Change | `feature.md` + `multi-phase.md` | `agentic` per phase unless `full` |
| Tests first on an approved unit | Change | `tdd-implement.md` | inherit |
| Going away / stop | Session | `handover.md` | n/a |
| Continue | Session | `resume.md` | inherit |

## Gate profiles

| Profile | Human stops | Production code |
|---|---|---|
| `observe` | none (except discover BRIEF confirm) | no |
| `design` | one GO on the design file, unless a prototype already decided | no |
| `lite` | none until package (G3 evidence inside) | yes |
| `agentic` | product CLARIFY only; then **package** (review + G3 + diff) | yes |
| `full` | G1 PLAN, G2 TASKS, then package | yes |
| `standard` | treat as `agentic` (alias) | yes |

**Package** (replaces blocking G4): contract paths, diff, `review.md` findings, G3 evidence. Human: accept / fix / reject. Agent may commit the branch; human merges.

Irreversible always pauses: force-push shared branch, prod data delete, customer message.

## spec-kit mapping

| Phase | This pack |
|---|---|
| constitution | `SDD/AGENTS.md` |
| specify + clarify | SPEC / story; human only if product preference |
| plan + tasks | files always; GO only on `full` |
| analyze | agent self-check + `review.md` |
| implement | TDD; no per-TASK GO |
| 0-to-1 / brownfield / exploration | `bootstrap` / `discover` / `design`+`prototype` |

## Principles

Why / Pattern / Boundaries / Source. Read the leaf when you apply it.

**Absolute:** spec-first, human-gates, primary-source, privacy-logging, no-secrets, backward-compat, traceability.

**Mode:** proportional-rigor, stop-at-gate, prove-it-works, tdd-red-green, sequence-verifiable-units, one-home-per-fact.

## Playbooks

Copy steps from `playbooks/<file>.md`. Write only under `SDD/`. After any production diff: `review.md` then package.

## Subagents

Lead owns contract, review, package. Delegates implement named TASKS. Lead reads the **diff**, not the summary.

## Reply

First lines: playbook, profile, `SDD/` paths. If waiting: name the **one** stop (CLARIFY, design GO, `full` G1/G2, or package).
