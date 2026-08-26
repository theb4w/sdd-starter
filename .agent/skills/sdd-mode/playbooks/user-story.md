# Playbook: user-story

**Gate profile:** `standard` (G2, G3, G4). `lite` (G3, G4) only when the module SPEC already exists **and** the slice is ≤1 file with no schema/service change.
**When:** a vertical slice (“as a … I want … so that …”) on a module that already has a SPEC.
**Not when:** the module does not exist yet → `feature.md` or `bootstrap.md`. Story is not a substitute for a module SPEC (`RN-SDD_MODE-05`).
**Template:** `specs/stories/_STORY_TEMPLATE.md`
**Principles:** spec-first, proportional-rigor, tdd-red-green, traceability.
**Skills:** `sdd-tdd`

## Steps

1. Identify the module SPEC. If missing, stop and reclassify.
2. Copy the template to `specs/stories/STORY_<SLUG>.md`. Fill persona, want, value, Given/When/Then, out-of-scope, gate profile, links to SPEC/ADRs.
3. Confirm the story does not contradict the SPEC. If it changes rules, update the SPEC (small extend) or stop for CLARIFY.
4. If `standard`: write a short TASKS file (or a TASKS section in the story). **STOP GATE 2.**
   If `lite`: `skip: lite story, no TASKS` and name the single file you will change.
5. IMPLEMENT via `sdd-tdd`: each Given/When/Then becomes a RED test, then GREEN.
6. **STOP GATE 3** — exercise the story on the real surface, not only the tests.
7. **STOP GATE 4.** Update SPEC_INDEX / SPEC history. `handover.md` if the session ends.

## Reply

Story path, module SPEC, profile, Given/When/Then list, waiting gate or TDD evidence.
