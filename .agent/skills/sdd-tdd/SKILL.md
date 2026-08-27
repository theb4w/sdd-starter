---
name: sdd-tdd
description: "RED-IMPLEMENT-GREEN for an already-approved acceptance criterion. Use during bug-fix, feature IMPLEMENT, user-story, or when the user asks for TDD. Grounded in Beck TDD and Antigravity test-spec-as-judge."
---

# sdd-tdd

The test specification is the judge (Antigravity SDD). This loop makes that spec executable. Use only after the playbook contract exists (SPEC, story, or bug repro). Do not invent behavior in the test.

**Why:** https://martinfowler.com/bliki/TestDrivenDevelopment.html — a test written after the implementation often ratifies the bug. RED is the trace from SPEC §7 / Given-When-Then to code.

## Loop

1. Name the criterion (AC id, Given/When/Then, or repro).
2. **RED** — failing test. Run it. Keep the output.
3. **IMPLEMENT** — production code only as far as that test requires.
4. **GREEN** — same test and the relevant suite. No new behavior.
5. Cleanup only while green. New behavior → new unit (`principle-sequence-verifiable-units`).

## Skip

`skip: <motivo>` when there is no cheap local runner, the check is expensive UI (G3 is then the proof), or the criterion is still in CLARIFY.

Skipping does not skip **principle-prove-it-works**.

## Reply

RED output (verbatim), files touched, GREEN output. If skipped, one line reason.

**Source:** Fowler TDD; https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity §7.
