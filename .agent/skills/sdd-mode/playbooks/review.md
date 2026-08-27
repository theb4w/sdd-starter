# Playbook: review

**Family:** Understand
**Intent:** Review this diff / PR
**Profile:** `observe`
**Not when:** no contract and no diff — that is `investigation.md`.
**Basis:** spec-kit `/speckit.analyze` + pstack interrogate, anchored on the spec (test spec as judge). https://github.github.io/spec-kit/
**Also:** after IMPLEMENT of a Change playbook, before the human package. Does not merge. Does not replace G3.

## Steps

1. Name the contract: `SDD/modules/SPEC_*`, `SDD/stories/STORY_*`, or the bug repro.
2. Read the actual diff (not a delegate summary).
3. Check, with evidence (path/line or AC id):
   - each AC / Given-When-Then / repro still holds or is newly covered
   - blast radius: other modules/INDEX that read the same types or routes
   - secrets, sensitive logs
   - spec-plan-tasks contradictions
   - diff size vs the project's PR budget (`SDD/AGENTS.md`)
4. **G3.** Read `Smoke:` from `SDD/AGENTS.md` (command or URL). Run it on the real surface. Record command + result. If `Smoke:` is missing or still a placeholder (`<…>`, `TBD`, empty): **must-fix**. Do not set Ask = accept.
5. Classify findings: **must-fix** / **nit** / **ok**.
6. Must-fix: correct, re-run this playbook **once**. If still red, put it in the package — do not hide it. Ask stays fix/reject until G3 evidence exists.
7. Do not push `main`. Review is not smoke; G3 is.

## Reply (the package body)

| Field | Content |
|---|---|
| Contract | paths |
| Diff | summary + key files |
| Findings | must-fix / nit / ok |
| G3 | `Smoke:` command or URL + result (required) |
| Ask | accept / fix / reject — **accept only if G3 is evidence, not a promise** |
