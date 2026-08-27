# Using sdd-mode from pstack

pstack (`/poteto-mode`) is the high-trust **execution** layer (playbooks, subagents, unslop, prove-it-works, shipping). This pack is the **contract** layer (spec-kit artifacts in `SDD/`, profiles, package).

They compose. They do not replace each other.

## Unskippable — before any pstack Change playbook

When poteto-mode matches **feature / bug-fix / refactoring / prototype / multi-phase / session pickup**, or the user asked for a product change:

0. **Load `sdd-mode`.** Resolve skill root (`skill-root.md`). Read `SKILL.md` + `catalog.md`. This step cannot be `skip:` unless the user opted out of sdd-mode by name.
1. **Step 0 — Ensure `SDD/`.**
2. **Match `catalog.md`.** Map the pstack playbook to the same-named sdd file (`feature`→`feature.md`, `bug-fix`→`bug-fix.md`, `refactoring`→`refactor.md`, `investigation`→`investigation.md`, `session pickup`→`resume.md`, `prototype`→`prototype.md`). Copy the **sdd** steps into the todo. pstack steps (architect, prove, unslop) run **inside** IMPLEMENT, not instead of the contract.
3. After code: sdd `review.md` then G3. pstack `interrogate` is extra; it does not replace `review.md`.
4. Present the sdd **package**. Then pstack may open the PR (`opening-a-pr`).

Silent skip of 0–4 is a defect. `skip: motivo` is allowed only for a named sdd step that does not apply (and still not for Step 0 on a product change).

## Who owns what

| Concern | Owner |
|---|---|
| Parallelism, model routing, unslop, prove on the real surface | pstack / poteto-mode |
| `SDD/` tree, SPEC/story/PLAN/TASKS/ADR, profiles, package body | sdd-mode |
| Merge to `main` / Graphite land | **pstack shipping**, and only if the human asked (bed / land / autonomous-run). sdd-mode never merges `main`. |

## Never-block vs overnight (split)

| pstack piece | In sdd-mode |
|---|---|
| `never-block-on-the-human` on **HOW** (reversible code, PLAN/TASKS) | **Yes** — that is profile `agentic`. Do not ask G1/G2. |
| `never-block` on **WHAT** (product CLARIFY) or skipping the **package** | **No.** Contract first; one package (or pstack shipping after G3 if the human pre-authorized land). |
| Overnight / `shipping` / `autopilot-full` / `autonomous-run` | **pstack owns it.** sdd-mode does not implement these playbooks and does not veto them. They still require `review.md` + G3 **before** arming merge. |
| “the best spec is code” | **Rejected.** Spec in `SDD/` stays SSOT. |

## pstack-only (do not force an sdd Change playbook)

perf, hillclimb, runtime/trace forensics, visual parity, babysit, shipping, autonomous-run, orchestrate, autopilot-*, worktree cleanup, authoring a skill, eval.

If that work **also** changes product behavior, run the unskippable block first, then the pstack-only playbook.

## What not to do

- Do not keep the spec only in pstack todos.
- Do not skip Step 0.
- Do not treat pstack never-block as license to skip the package.
- Do not treat sdd-mode as license to block G1/G2 on `agentic`.
