---
name: principle-traceability
description: "Code traces to a TASK or story, which traces to a SPEC, which traces to an ADR when a decision exists. Use when creating files, commits, or skipping an artifact."
---

# Traceability

Every production file created in an SDD session names the TASK (or story) it fulfills. Every TASK names a SPEC. Every architectural choice names an ADR.

User stories trace to an existing module SPEC (`RN-SDD_MODE-05`). Bug-fixes trace to the SPEC of the broken behavior, or to a regression test if no SPEC exists yet.

**Source:** `AGENTS.md` regra 6.
