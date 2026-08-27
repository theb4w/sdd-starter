---
name: principle-primary-source
description: "A technical choice with two or more viable options needs an ADR; each option needs a primary-source URL. Use when picking a library, protocol, or 'best practice'."
---

# Primary source

**Why:** Nygard’s ADR pattern exists because architectural knowledge evaporates into tribal memory. “Best practice” without a document is not evidence. Spec-kit’s plan phase is where stack and constraints are decided — those decisions must be replayable.

**Pattern:** If two options are viable, write `SDD/decisions/ADR-NNN-*.md` with ≥2 alternatives, each with a vendor/RFC/standard URL. No URL → stop; do not invent citations.

**Boundaries:** Local naming, formatting, and one-line refactors are not ADRs.

**Source:** https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions ; spec-kit plan (HOW after WHAT) https://github.github.io/spec-kit/concepts/sdd.html
