---
name: principle-tdd-red-green
description: "When a cheap local test path exists, write a failing test from the acceptance criterion, then the minimum code, then watch it pass. Use during IMPLEMENT, bug-fix, and user-story."
---

# TDD: RED → IMPLEMENT → GREEN

1. **RED** — write the test that encodes the AC (or Given/When/Then). Run it. Record the failure.
2. **IMPLEMENT** — smallest change that should pass.
3. **GREEN** — run it. Do not widen scope. Cleanup refactor only while green.

Skip only with `skip: motivo` (test would be expensive, integration-only, or the behavior is still unclear). Skipping TDD does not skip G3.

TDD proves an already-written criterion. It does not discover the spec.

**Source:** playbook `tdd-implement.md`; skill `sdd-tdd`. Classic cycle: https://martinfowler.com/bliki/TestDrivenDevelopment.html
