# Playbook: user-story

**Family:** Change
**Intent:** User should be able to X (module SPEC exists)
**Profile:** `agentic`
**Not when:** no module SPEC → `feature.md` / `bootstrap.md`.
**Basis:** Cohn slice; spec-kit specify at story grain.
**Skills:** `sdd-tdd`, `review.md`

Promote to `full` if the slice changes a product rule, schema, or service.

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). Identify module SPEC. Missing → reclassify.
2. Write `SDD/stories/STORY_<SLUG>.md`. Given/When/Then → RED tests.
3. Must not contradict the SPEC. Product rule change → **STOP** CLARIFY.
4. Write short TASKS. No G2 stop on `agentic`.
5. IMPLEMENT via `sdd-tdd`.
6. `review.md` + G3 (`Smoke:` in `SDD/AGENTS.md`).
7. **Package.** INDEX.

## Reply

Story path, profile, package or CLARIFY stop.
