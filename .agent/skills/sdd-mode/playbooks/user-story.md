# Playbook: user-story

**Gate profile:** `standard`. `lite` only if module SPEC exists and the slice is ≤1 file with no schema/service change.
**When:** vertical slice on a module that already has `SDD/modules/SPEC_*.md`.
**Not when:** module does not exist → `feature.md` / `bootstrap.md`.
**Template:** `templates/story.md`
**Skills:** `sdd-tdd`

## Steps

1. Ensure `SDD/`. Identify the module SPEC. If missing, stop and reclassify.
2. Write `SDD/stories/STORY_<SLUG>.md`. Given/When/Then become RED tests.
3. Must not contradict the SPEC. Rule changes → update SPEC or CLARIFY.
4. If `standard`: short TASKS in `SDD/plans/`. **STOP GATE 2.** If `lite`: `skip: lite story`.
5. IMPLEMENT via `sdd-tdd`.
6. **STOP GATE 3.** **STOP GATE 4.** Update INDEX.

## Reply

Story path, module SPEC, profile, waiting gate or TDD evidence.
