---
name: principle-stop-at-gate
description: "Stop at the playbook's named human gate. Inside an already-approved TASK, do not ask permission to write the next file. Opposite of pstack never-block-on-the-human. Use at PLAN/TASKS/SMOKE/COMMIT and during IMPLEMENT."
---

# Stop at the gate

**Block** when the profile names G1, G2, G3, G4, or design approval. Present the artifact and wait.

**Do not block** on reversible work *inside* a unit that already passed those gates. Do not ask “should I implement T-A2?” after GATE 2 approved T-A2.

Still pause for irreversible actions the project forbids without a human: force-push to `main`, production deploy, data deletion.

This is the inverse of pstack's never-block-on-the-human, which is not a default here (ADR-001).

**Source:** `specs/decisions/ADR-001-skill-as-interface.md`; `AGENTS.md` “Respeitar gates humanos ainda que a ferramenta tenha execução automática”.
