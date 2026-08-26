---
name: sdd-tdd
description: "Run the RED-IMPLEMENT-GREEN loop for an already-approved acceptance criterion. Use during bug-fix, feature IMPLEMENT, user-story, tdd-implement, or when the user asks for TDD."
---

# sdd-tdd

Use this skill only after the playbook's contract exists (SPEC, story, or bug repro). Do not invent behavior in the test.

## Loop

1. Name the criterion (AC id, Given/When/Then, or repro).
2. **RED** — write the failing test. Run it. Keep the failure output.
3. **IMPLEMENT** — edit production code only as far as that test requires.
4. **GREEN** — run the same test and the relevant suite. No new behavior.
5. Optional cleanup while green. If cleanup needs new behavior, that is a new unit.

## Skip

`skip: <motivo>` when:

- there is no cheap local test runner
- the check is an expensive integration or a manual UI path (then G3 *is* the proof)
- the criterion is still in CLARIFY

Skipping here does not skip **principle-prove-it-works**.

## Reply

RED output (verbatim fail), files touched, GREEN output. If skipped, one line reason.
