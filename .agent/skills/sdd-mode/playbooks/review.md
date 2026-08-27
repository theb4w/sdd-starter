# Playbook: review

**Gate profile:** inherit (`observe` if invoked alone). Does not merge.
**When:** after IMPLEMENT and before the human package; or “review this diff/PR”.
**Not when:** no contract and no diff — that is `investigation.md`.
**Basis:** spec-kit `/speckit.analyze` + pstack interrogate, anchored on the spec (test spec as judge). https://github.github.io/spec-kit/

## Steps

1. Name the contract: `SDD/modules/SPEC_*`, `SDD/stories/STORY_*`, or the bug repro.
2. Read the actual diff (not a delegate summary).
3. Check, with evidence (path/line or AC id):
   - each AC / Given-When-Then / repro still holds or is newly covered
   - blast radius: other modules/INDEX that read the same types or routes
   - secrets, sensitive logs
   - spec-plan-tasks contradictions
   - diff size vs the project's PR budget (`SDD/AGENTS.md`)
4. Classify findings: **must-fix** / **nit** / **ok**.
5. Must-fix: correct, re-run this playbook **once**. If still red, put it in the package — do not hide it.
6. Do not push `main`. Do not skip G3; review is not smoke.

## Reply (the package body)

| Field | Content |
|---|---|
| Contract | paths |
| Diff | summary + key files |
| Findings | must-fix / nit / ok |
| G3 | command or surface + result |
| Ask | accept / fix / reject |
