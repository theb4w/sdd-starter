---
name: principle-sequence-verifiable-units
description: "Break multi-step work into units that each end in a check. Verify before the next. Use when stacking TASKS, commits, or phases. Maps to spec-kit tasks + modular granularity."
---

# Sequence verifiable units

**Why:** Parnas: modules limit the blast radius of change. Antigravity SDD: apply SDD to fine-grained modules; if one fails validation, only that module is re-specified. Spec-kit tasks are ordered, checkable, and phase-scoped. Batching five TASKS then “testing at the end” hides which change broke the spec.

**Pattern:** One TASK, story slice, or phase ends in an observable check before the next starts. Git history should replay: failing test, then fix.

**Boundaries:** A single-line typo is already one unit.

**Source:** https://dl.acm.org/doi/10.1145/361598.361623 ; https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity (modular granularity); spec-kit `/speckit.tasks`.
