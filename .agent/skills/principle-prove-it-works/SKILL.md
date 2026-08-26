---
name: principle-prove-it-works
description: "Before declaring done, verify on the real artifact (run the feature, rerun the repro, inspect the diff). Compiling is not proof. Use after IMPLEMENT and at GATE 3."
---

# Prove it works

G3 is evidence on the real surface, not “the unit tests passed” alone. Run the broken path. Read the actual output. For a bug, the original repro must pass on the same surface.

When work is delegated, inspect the diff and the runtime result, not the delegate's summary.

If the project has no runtime yet (this starter is Markdown), proof is consistency checks named in the SPEC (grep, file exists, playbook declares a profile).

**Source:** `docs/SDD_WORKFLOW.md` §1.3 (lição G3); pstack prove-it-works as mechanism, not as a substitute for gates: https://github.com/cursor/plugins/blob/main/pstack/skills/principle-prove-it-works/SKILL.md
