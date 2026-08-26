---
name: principle-backward-compat
description: "Each commit on main preserves the previous working state. Multi-phase work must revert without taking down the prior phase. Use when stacking commits or changing contracts."
---

# Backward-compatible commits

A commit on `main` must leave the previous behavior working, or ship an explicit, reversible migration. If phase X reverts, phase X-1 still runs.

A contract break needs an ADR plus a rollback path. Do not land a half-migration that only works if the next commit arrives.

**Source:** `SDD/AGENTS.md` regra 5; `references/workflow.md` §1.1.
