---
name: principle-traceability
description: "Code traces to a TASK or story, which traces to a SPEC, which traces to an ADR when a decision exists. Use when creating files, commits, or skipping an artifact."
---

# Traceability

**Why:** IEEE 29148 requires bidirectional traceability between needs, requirements, and verification. Spec-kit persists `spec.md` / `plan.md` / `tasks.md` in git so a later agent (or human) reconstructs intent. Chat history is not that record.

**Pattern:** Production file → TASK or story in `SDD/plans` or `SDD/stories` → `SDD/modules/SPEC_*` → `SDD/decisions/ADR-*` when a trade-off existed. User stories require a module SPEC. Bug-fixes trace to the SPEC of the broken behavior or to the regression test.

**Boundaries:** Generated `SDD/` scaffold files (empty INDEX) need no TASK id.

**Source:** ISO/IEC/IEEE 29148; spec-kit persistent Markdown artifacts https://github.github.io/spec-kit/concepts/sdd.html
