---
name: principle-proportional-rigor
description: "Match ceremony to risk. Do not force plan+tasks on a five-line bug. Do not skip PLAN on a medium feature. Use when classifying size or picking a playbook."
---

# Proportional rigor

**Why:** ISO/IEC 12207 allows tailoring the life cycle to project risk. Spec-kit documents a shorter path for small features (only specify is strictly required before plan). Forcing the full pipeline on a typo produces theater; skipping PLAN on a new module produces vibe coding.

**Pattern:** Default `agentic` (ADR-003). Upgrade to `full` when schema, new service, compliance, or WHAT is unclear. Downgrade only by reclassifying in the open. Small feature: ≤100 LOC, 0–1 new files, no architectural trade-off, no new external service, no schema change.

**Boundaries:** Compliance, safety, or money-moving changes stay `full` even if the diff is small.

**Source:** https://github.github.io/spec-kit/ (shorter path for small features); ADR-002.
