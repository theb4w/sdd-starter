---
name: principle-spec-first
description: "No production code without the playbook's approved contract (SPEC, story, or none for a bug). Use when tempted to implement from a chat prompt. Maps to spec-kit specify-before-implement."
---

# Spec-first

Do not write production code until the playbook's contract exists in `SDD/` and, if the gate profile requires it, has been approved.

**Why:** Spec-kit inverts the old loop where specs were discarded once coding began. If the agent codes from a sentence, intent is not reviewable and cannot be regenerated. IEEE 29148 treats requirements as the contract between need and solution. Antigravity's SDD lab: humans own steps 1–3 (requirements, architecture, test spec); agents own generation and validation.

**Pattern:**

| Playbook | Contract (WHAT) |
|---|---|
| bootstrap, feature média/grande, reshape-arch | `SDD/modules/SPEC_*.md` (tech-agnostic) |
| feature pequena, user-story | existing SPEC extended, or `SDD/stories/STORY_*` tied to a module SPEC |
| bug-fix | no new spec; expected behavior already in SPEC or the repro |
| design, prototype, investigation | no production code |

Write the file. A chat “OK” is not a spec.

**Boundaries:** Throwaway prototype code stays off `main`. Bug-fix does not invent a SPEC for a missing feature — reclassify.

**Source:** https://github.github.io/spec-kit/concepts/sdd.html (intent-driven, WHAT before HOW); https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity (SSOT, design-implementation loop); ISO/IEC/IEEE 29148. See `references/sdd-basis.md`.
