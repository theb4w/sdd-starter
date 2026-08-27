---
name: principle-prove-it-works
description: "Before declaring done, verify on the real artifact (run the path, reread the value, inspect the diff). Compiling is not proof. Maps to spec-kit implement+test and Antigravity test-spec-as-judge. Use at G3."
---

# Prove it works

**Why:** Antigravity SDD: the system spec is the blueprint; the **test specification is the judge**. IEEE 1012 V&V: verification is against stated requirements, not against “the build succeeded.” Agents report intent; diffs and runtime report fact.

**Pattern:** After IMPLEMENT, ask how this is proven. G3 is the `Smoke:` line in `SDD/AGENTS.md` (command or URL) on the real surface, or the original repro for a bug. Inspect git diff, not the delegate summary. Missing `Smoke:` → not done; `review.md` must-fix, no accept.

**Boundaries:** This pack (Markdown only) proves consistency of `SDD/` files. Product code must run. Skipping `sdd-tdd` does not skip this.

**Source:** https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity (test spec as judge); pstack mechanism https://github.com/cursor/plugins/blob/main/pstack/skills/principle-prove-it-works/SKILL.md
