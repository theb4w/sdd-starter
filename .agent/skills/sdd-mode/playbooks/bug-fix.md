# Playbook: bug-fix

**Gate profile:** `lite` (G3, G4). If the fix changes intended behavior or architecture, reclassify (`feature.md` or `refactor.md`) — do not stay lite.
**When:** a defect to reproduce, root-cause, and fix.
**Not when:** missing functionality that was never specified → `feature.md` or `user-story.md`.
**Principles:** prove-it-works, tdd-red-green, sequence-verifiable-units, stop-at-gate.
**Skills:** `sdd-tdd`
**Human prompt (pointer):** `prompts/BUG_FIX.md`

## Preconditions

- [ ] A description of the failure exists (even if unreproduced)

## Steps

1. Read `SPEC_INDEX.md`, the module SPEC if known, latest handover, domain skill if any.
2. Reproduce on the matching surface. Do not hand the repro to the user unless the surface is unreachable, and then say why. If it will not fire, instrument until it does. A bug you cannot reproduce, you cannot prove fixed.
3. Root cause: expected (cite SPEC or current documented behavior) vs actual vs why. Binary-search; git log on the file. Blast radius in one sentence.
4. Classify:
   - (a) pure fix, no intended-behavior change → stay on this playbook
   - (b) the spec was wrong → CLARIFY + update SPEC; maybe ADR
   - (c) architectural (race, contract) → `refactor.md` or ADR first
5. **sdd-tdd:** RED test that fails on the repro, then minimum fix, then GREEN. `skip: motivo` only if no cheap local test; G3 still required.
6. Do not ship “might help” guards that do not follow from the evidence. If evidence refutes the hypothesis, revert what it motivated.
7. **STOP GATE 3** — same surface as step 2; original repro now passes; related flows not obviously broken.
8. **STOP GATE 4** — conventional commit `fix(...): ...`. Prefer history: failing test, then fix.
9. Optional short `handover.md` if the session ends.

## Reply

What broke, root cause, fix, RED then GREEN evidence (verbatim), G3 status.
