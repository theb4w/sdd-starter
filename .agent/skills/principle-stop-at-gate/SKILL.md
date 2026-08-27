---
name: principle-stop-at-gate
description: "Block only where the profile names a human stop. agentic does not block on G1/G2. Inside IMPLEMENT, do not ask per file. ADR-003."
---

# Stop at the gate

**Why:** Asking GO on every TASK after the list exists adds no review quality. Skipping the **package** (review + G3 + diff) is vibe shipping. ADR-003 moves HOW approval to after the agent has reviewed and proven, except on `full`.

**Pattern:**

- `agentic` / `lite`: do not **STOP GATE 1** or **STOP GATE 2**. Stop for product-only CLARIFY, then after `review.md`+G3 for the package.
- `full`: **STOP GATE 1** and **STOP GATE 2** as written.
- Never per-file “may I edit this?” during IMPLEMENT.
- Always pause: force-push to shared branch, prod delete, customer send.

**Boundaries:** Not pstack never-block. The contract is still written first. The human still sees one package. `main` is not silent.

**Source:** ADR-003; spec-kit short path https://github.github.io/spec-kit/
