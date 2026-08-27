# Dry-run (prove this pack)

No product runtime. Proof is that an agent following `SKILL.md` produces a consistent `SDD/` tree and a valid package body.

Run after changing playbooks, catalog, SKILL, or templates. Record the date in `SDD/INDEX.md`.

## A — Headers = catalog

Every `playbooks/*.md` starts with **Family / Intent / Profile** identical to `catalog.md`. If they drift, catalog wins; fix the file. `refactor.md` has two blocks.

## B — Step 0 on a throwaway dir

In a temp directory (not this repo):

1. Point skill root at this `sdd-mode/`.
2. Invoke `sdd-mode` as **New project, I know the brief** with a one-paragraph fake brief.
3. Expect `SDD/README.md`, `BRIEF.md`, `AGENTS.md`, `INDEX.md` plus empty `modules/ plans/ decisions/ stories/ design/ handovers/`.
4. `SDD/AGENTS.md` contains a `Smoke:` line (may still be a placeholder).
5. No `specs/`, `docs/`, `prompts/`, `QUICKSTART/`, or process `scripts/` created.

## C — Bug path (no new SPEC)

Still in the temp dir, invoke **Broken / repro** on a fake defect against the brief. Expect: no new `SPEC_*.md`; `review.md` package table; **Ask** is not `accept` if `Smoke:` is still a placeholder (must-fix: fill `Smoke:`).

## D — Resume

Write a one-line handover. Invoke **Continue**. Expect: no extra human GO if branch matches and profile is not `full` waiting on G1/G2.

## E — pstack glue

Confirm `.cursor/rules/sdd-under-pstack.mdc` (this repo) or the copied `templates/cursor-rule.mdc` exists in the product. Confirm `with-pstack.md` unskippable block is what the rule cites.

## Pass

A–E hold. Fail = fix the pack, do not ship a “docs only” commit that leaves catalog/playbook drift.
