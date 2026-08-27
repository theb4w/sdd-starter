# Playbook: user-story

**Gate profile:** `agentic`. `lite` if module SPEC exists and the slice is ≤1 file, no schema/service.
**When:** vertical slice on an existing `SDD/modules/SPEC_*.md`.
**Not when:** no module SPEC → `feature.md` / `bootstrap.md`.
**Basis:** Cohn slice; spec-kit specify at story grain.
**Skills:** `sdd-tdd`, `review.md`

## Steps

1. Ensure `SDD/`. Identify module SPEC. Missing → reclassify.
2. Write `SDD/stories/STORY_<SLUG>.md`. Given/When/Then → RED tests.
3. Must not contradict the SPEC. Product rule change → **STOP** CLARIFY.
4. Write short TASKS unless `lite` (`skip: lite story`). No G2 stop on `agentic`.
5. IMPLEMENT via `sdd-tdd`.
6. `review.md` + G3.
7. **Package.** INDEX.

## Reply

Story path, profile, package or CLARIFY stop.
