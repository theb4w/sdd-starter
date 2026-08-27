---
name: principle-tdd-red-green
description: "When a cheap local test path exists, write a failing test from the acceptance criterion, then the minimum code, then watch it pass. Use during IMPLEMENT. Maps to spec-kit test spec as judge."
---

# TDD: RED → IMPLEMENT → GREEN

**Why:** Beck’s TDD makes the test spec executable before production code exists. Antigravity SDD: generated code is judged by the test specification. A test written after the fact often encodes the bug. The failing test is the trace from SPEC §7 / Given-When-Then to code.

**Pattern:**

1. **RED** — test from the AC. Run it. Keep the failure.
2. **IMPLEMENT** — smallest change.
3. **GREEN** — same test + relevant suite. No extra behavior.

**Boundaries:** Skip with `skip: motivo` if there is no cheap runner, the check is UI-only (then G3 is the proof), or the criterion is still in CLARIFY. TDD does not discover the spec.

**Source:** https://martinfowler.com/bliki/TestDrivenDevelopment.html ; Antigravity lab §7 (test specification is the judge).
