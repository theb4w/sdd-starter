---
name: principle-human-gates
description: "Fire human stops for the profile. agentic: product CLARIFY + final package (review+G3+diff). full: also G1 and G2. Use at handoffs. ADR-002, ADR-003."
---

# Human gates

Named gates still exist (G1 PLAN, G2 TASKS, G3 SMOKE, G4/package). Which **block the human** is the profile.

| Profile | Human stops | spec-kit analogue |
|---|---|---|
| `observe` | none (BRIEF confirm on discover) | research |
| `design` | one GO on the design file | creative exploration |
| `lite` | package (includes G3 evidence) | short path |
| `agentic` | product CLARIFY; then package | specify then implement; analyze by agent |
| `full` | G1, G2, then package | approve plan/tasks before code |
| `standard` | alias of `agentic` | — |

**Why:** Spec-kit allows a shorter path; Antigravity uses one plan approval, not four. Blocking G1 and G2 on every change makes the human a semaphore. Trust comes from a written contract, agent analyze/review, and G3 — then one human look at the package. Compliance still uses `full`.

**Pattern:** Default `agentic` (ADR-003). Write PLAN/TASKS always when the playbook requires those files; do not wait on G1/G2 unless `full`. Always run `review.md` + G3 before the package. Irreversible ops always pause.

**Boundaries:** Do not drop G3. Do not skip the package. sdd-mode does not merge `main`. pstack `shipping` / overnight land is allowed only after `review.md`+G3 and only if the human asked. Never-block on HOW is profile `agentic`, not a skip of WHAT.

**Source:** ADR-003; https://github.github.io/spec-kit/ ; https://codelabs.developers.google.com/sdd-adk-antigravity
