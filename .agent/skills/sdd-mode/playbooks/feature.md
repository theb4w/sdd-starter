# Playbook: feature

**Gate profile:** small → `standard` (G2, G3, G4). Medium or large → `full` (G1, G2, G3, G4). Large also uses `multi-phase.md` after PLAN.
**When:** new or changed intended behavior.
**Not when:** a defect in existing behavior → `bug-fix.md`. A vertical slice of an already-specified module → `user-story.md` is allowed. Shape still unknown → `design.md` first.
**Principles:** spec-first, proportional-rigor, human-gates, tdd-red-green, stop-at-gate.
**Skills:** `sdd-tdd`
**Human prompt (pointer):** `prompts/NEW_FEATURE.md`

## Size (do not downgrade silently)

Small only if **all** hold: ≤100 LOC, 0–1 new files, no architectural trade-off, no new external service, no schema change. Otherwise medium (100–400) or large (>400 or multi-module). If unsure, upgrade.

## Steps

1. Read `AGENTS.md`, `SPEC_INDEX.md`, architecture doc, latest handover, affected SPEC, relevant ADRs and domain skills.
2. State size, profile, files likely touched, trade-offs, CLARIFY questions. **STOP** for GO if size is disputed.
3. Contract:
   - small: extend the existing SPEC (diff).
   - medium/large: new or v2 SPEC from `_SPEC_TEMPLATE.md`.
   Unknowns go to §9. **No production code.**
4. Resolve CLARIFY with the human. Update §10. Empty §9 before PLAN. Trade-offs → ADR (2+ options, URL each). **STOP** for ADR acceptance.
5. If `full`: write PLAN from `_PLAN_TEMPLATE.md`. **STOP GATE 1.**
6. Write TASKS from `_TASKS_TEMPLATE.md` (small: short 1-phase list). **STOP GATE 2.**
7. IMPLEMENT one TASK at a time. For each: `sdd-tdd` when a cheap test exists. Do not start the next TASK until this AC is green (`principle-sequence-verifiable-units`).
8. **STOP GATE 3** — smoke the critical flows named in the SPEC.
9. **STOP GATE 4** — conventional commit / PR size per `AGENTS.md`.
10. `handover.md`. Update `SPEC_INDEX.md`.

## Reply

Size, profile, SPEC/PLAN/TASKS paths, which gate is waiting, or evidence if past IMPLEMENT.
