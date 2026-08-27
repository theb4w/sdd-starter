---
name: sdd-mode
description: "Sticky SDD mode (spec-kit / Antigravity). Contract layer under pstack/poteto-mode or standalone. Resolves skill root (.cursor/.grok/.kiro/.agent/skills). Default agentic: SDD/ contract, implement, agent review, one package. Use for /sdd-mode, spec-kit, feature, bug, refactor, design, story, greenfield, brownfield, /poteto-mode product changes."
---

# SDD mode

Sticky. Opt out when the user says so by name.

Community SDD: GitHub spec-kit as adopted by Antigravity. Specs in `SDD/` are the SSOT. Default **agentic** (ADR-003): human on intent and the package; agent on HOW, code, and review. `full` is high-ceremony.

Under **pstack / poteto-mode**: this skill is the contract layer. Unskippable load: `references/with-pstack.md`. Cursor always-on rule: `templates/cursor-rule.mdc` (this checkout: `.cursor/rules/sdd-under-pstack.mdc`).

Agent-facing files in this skill are **English**. Product `SDD/` prose follows the team's language.

Sources (open on demand, do **not** dump into the todo): `references/catalog.md`, `references/layout.md`, `references/skill-root.md`, `references/with-pstack.md`, `references/install.md`, `references/sdd-basis.md`. `references/workflow.md` is an **appendix** — open a cited section only.

## Skill root

Do not assume `.agent/skills`. Resolve the folder that contains `sdd-mode/SKILL.md` (`.cursor/skills`, `.grok/skills`, `.kiro/skills`, `.agents/skills`, `.agent/skills`, or user-level). Templates and playbooks sit **next to this file**. `SDD/` is always the target **repo root**. `references/skill-root.md`, `references/install.md`.

## Non-negotiables

1. **Step 0 — Ensure `SDD/`.** First action.
2. Todo: **principles index below** (not 13 extra reads unless a row fires), then **`references/catalog.md`** (one row), then copy that playbook verbatim. `skip: motivo` if a step is skipped. No silent skip.
3. Spec-first: contract in `SDD/` before production code (bug: none new).
4. Stop only where the **profile in the catalog row** says. `agentic` does not stop at G1/G2 (that *is* never-block on HOW).
5. After production diff: `review.md`, G3 from `SDD/AGENTS.md` **`Smoke:`**, **package**. No `Smoke:` → do not ask accept. Branch. sdd-mode does not merge `main`. Overnight land is pstack shipping after G3, only if the human asked.
6. Promote to `full` when: new schema/external service, compliance/money/health, WHAT unclear, or the user asked.
7. Do not load `workflow.md` into the session todo. Do not load `_example_skill` or `.agent/agents.md` personas unless the user asked.

## Step 0 — Ensure SDD/

If `SDD/` is missing at the target repo root:

1. Create the directories in `references/layout.md`.
2. Copy `templates/` from **this skill directory** (`sdd-readme`→`SDD/README.md`, `brief`→`BRIEF.md`, `agents`→`AGENTS.md`, `index`→`INDEX.md`).
3. If the host is Cursor and `.cursor/rules/sdd-under-pstack.mdc` is missing, copy `templates/cursor-rule.mdc` there.
4. Do not invent product facts except on `discover` or a brief the human already gave.
5. Tell the human: process lives in `SDD/` from now on. They must fill **`Smoke:`** in `SDD/AGENTS.md` (command or URL). Until then, packages cannot be accepted.

If `specs/` or `docs/` still hold process files, migrate into `SDD/` this session.

Never create `scripts/`, empty `tests/`, `prompts/`, or `QUICKSTART/` as SDD process.

## Intent → playbook

Canonical table: `references/catalog.md`. Copy it here so a skipped read cannot desync the matcher. If this copy and `catalog.md` differ, **`catalog.md` wins** — fix this file. Tie-breaks and pstack-only list live only in `catalog.md`.

| Intent (developer phrasing) | Family | File | Profile |
|---|---|---|---|
| New project, I know the brief | Arrive | `bootstrap.md` | `agentic` |
| Legacy repo, no docs | Arrive | `discover.md` | `observe` |
| First chat, `SDD/` already there | Arrive | `onboarding.md` | `observe` |
| How / why / are we sure / blast radius | Understand | `investigation.md` | `observe` |
| Review this diff / PR | Understand | `review.md` | `observe` |
| Shape / UX still open | Shape | `design.md` | `design` |
| Two sketches / experiment | Shape | `prototype.md` | `design` |
| Broken / repro | Change | `bug-fix.md` | `lite` |
| User should be able to X (module SPEC exists) | Change | `user-story.md` | `agentic` |
| New behavior | Change | `feature.md` | `agentic` |
| Reshape, same contract | Change | `refactor.md` | `lite` |
| Reshape, public contract | Change | `refactor.md` | `full` |
| Large / many modules | Change | `multi-phase.md` | `agentic` |
| Tests first on an approved unit | Change | `tdd-implement.md` | inherit |
| Going away / stop | Session | `handover.md` | n/a |
| Continue | Session | `resume.md` | inherit |

Each `playbooks/<file>.md` starts with the same **Family / Intent / Profile** lines. After any production diff, run `review.md` then the package (except `observe` / `design` with no code).

## Gate profiles

| Profile | Human stops | Production code |
|---|---|---|
| `observe` | none (except discover BRIEF confirm) | no |
| `design` | one GO on the design file, unless a prototype already decided | no |
| `lite` | none until package (G3 evidence inside) | yes |
| `agentic` | product CLARIFY only; then **package** (review + G3 + diff) | yes |
| `full` | G1 PLAN, G2 TASKS, then package | yes |
| `standard` | `agentic` | yes |

**Package:** contract paths, diff, `review.md` findings, G3 evidence (`Smoke:` + result). Accept / fix / reject. Commit on a branch. Human merges, unless they already invoked pstack shipping/autonomous-run after G3.

Irreversible always pauses: force-push shared branch, prod data delete, customer message.

## Principles (inline index)

Read this table at task start. **Open the leaf** `principle-*/SKILL.md` only when a row fires. A citation with no decision means you skipped the leaf.

| Principle | Fire when | Changes |
|---|---|---|
| `spec-first` | tempted to code from chat | write the `SDD/` contract first |
| `human-gates` | at a handoff | stop only where the profile says |
| `stop-at-gate` | tempted to ask GO per file / G1 on `agentic` | do not; package still required |
| `proportional-rigor` | sizing or picking a playbook | `full` on schema/service/compliance/unclear WHAT |
| `primary-source` | a technical choice | URL or ADR; no “best practice” |
| `privacy-logging` | logging / telemetry | metadata only; no sensitive payload |
| `no-secrets` | env, keys, connection strings | env / secret manager; never git |
| `backward-compat` | commit / phase | `main` stays safe; revert phase X keeps X-1 |
| `traceability` | new file or TASK | code → TASK → SPEC → ADR |
| `prove-it-works` | about to say done | G3 = `Smoke:` on the real surface, not compile |
| `tdd-red-green` | IMPLEMENT and a cheap runner exists | RED then minimum code then GREEN |
| `sequence-verifiable-units` | multi-step / multi-PR | each unit ends checkable |
| `one-home-per-fact` | editing procedure or recording a lesson | one file owns it; others point |

Absolute: spec-first, human-gates, primary-source, privacy-logging, no-secrets, backward-compat, traceability. Mode: the rest.

## Subagents

Lead owns contract, review, package. Delegates implement named TASKS. Lead reads the **diff**, not the summary. Under pstack, use `poteto-agent` for implementation if that host requires it; still run sdd `review.md` before the package.

## Reply

First lines: catalog row (file + profile), `SDD/` paths, skill root used. If waiting: the **one** stop (CLARIFY, design GO, `full` G1/G2, or package).
