---
name: principle-sequence-verifiable-units
description: "Break multi-step work into units that each end in a check. Verify before the next. Use when stacking TASKS, commits, or phases."
---

# Sequence verifiable units

One TASK, one story slice, or one phase ends in an observable check (test, command, smoke) before the next starts. Order delivery so a reviewer can replay the proof from git history (failing test commit, then fix).

Do not batch five TASKS and “test at the end”.

**Source:** `references/workflow.md` §7; `sdd-mode/templates/tasks.md`.
