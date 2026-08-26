# Playbook: design

**Gate profile:** `design` (human approves the design file). No production code.
**When:** UX, module shape, or flow is still open, and writing SPEC now would freeze a guess.
**Not when:** the shape is already in a SPEC → `feature.md`. A cheap experiment would settle it → `prototype.md` first, then return here.
**Template:** `docs/design/_DESIGN_TEMPLATE.md`
**Principles:** primary-source, proportional-rigor, stop-at-gate.

## Steps

1. Name the user and the problem in one paragraph. List constraints from the brief, SPEC_INDEX, and compliance.
2. Copy the template to `docs/design/<slug>.md`.
3. Write 2–3 options. Each option: description, consequences, reversibility, a source URL if it implies a technology.
4. Recommend one. State what you are *not* deciding yet.
5. List open questions that become CLARIFY or ADRs later.
6. **STOP** for human approval of the design file (profile `design`).
7. After approval: either `feature.md` / `bootstrap.md` (SPEC from the recommendation) or ADRs for locked trade-offs. Do not start IMPLEMENT from the design file alone.

## Reply

Path of the design file, options table, recommendation, waiting on design approval.
