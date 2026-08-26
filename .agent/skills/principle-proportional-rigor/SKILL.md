---
name: principle-proportional-rigor
description: "Match ceremony to the scenario. Do not force the full cycle on a five-line bug. Do not empty PLAN out of a medium feature. Use when classifying size or picking a playbook."
---

# Proportional rigor

The playbook picks the weight. Upgrade (more gates, more artifacts) is always allowed. Downgrade requires reclassifying the work in the open (bug, not feature; story, not new module).

Size cues for `feature.md` (from `QUICKSTART/small-feature.md`): small is ≤100 LOC, 0–1 new files, no architectural trade-off, no new external service, no schema change. Any “no” → not small.

**Source:** `docs/SDD_WORKFLOW.md` §2; ADR-002.
