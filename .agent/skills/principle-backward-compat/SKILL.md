---
name: principle-backward-compat
description: "Each commit on main preserves the previous working state. Multi-phase work must revert without taking down the prior phase. Use when stacking commits or changing contracts."
---

# Backward-compatible commits

**Why:** Lehman’s law of continuing change: software is modified, not replaced. A half-migration that only works if the next commit lands is not a release. Spec-kit implement can scope to phases; each phase must leave a working system (Antigravity: isolate failed modules).

**Pattern:** Commit on `main` keeps prior behavior, or ships an explicit reversible migration. Phase X revert must not break phase X-1. Contract breaks need an ADR and rollback.

**Boundaries:** Experimental branches and `prototype` sketches are exempt until merge.

**Source:** Parnas 1972 (isolate change) https://dl.acm.org/doi/10.1145/361598.361623 ; spec-kit iterative enhancement https://github.github.io/spec-kit/concepts/sdd.html
