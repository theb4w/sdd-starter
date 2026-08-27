# Playbook catalog (single source)

Every playbook file **must** repeat Family, Intent, and Profile exactly as in this table. If they drift, this table wins — fix the file.

| Intent (developer phrasing) | Family | File | Profile |
|---|---|---|---|
| New project, I know the brief | Arrive | `bootstrap.md` | `agentic` |
| Legacy repo, no docs | Arrive | `discover.md` | `observe` |
| First chat, `SDD/` already there | Arrive | `onboarding.md` | `observe` |
| How / why / are we sure / blast radius | Understand | `investigation.md` | `observe` |
| Review this diff / PR | Understand | `review.md` | `observe` |
| Shape / UX still open | Shape | `design.md` | `design` |
| Two sketches / experiment | Shape | `prototype.md` | `design` |
| Broken / repro | Change | `bug-fix.md` | `lite` |
| User should be able to X (module SPEC exists) | Change | `user-story.md` | `agentic` |
| New behavior | Change | `feature.md` | `agentic` |
| Reshape, same contract | Change | `refactor.md` | `lite` |
| Reshape, public contract | Change | `refactor.md` | `full` |
| Large / many modules | Change | `multi-phase.md` | `agentic` |
| Tests first on an approved unit | Change | `tdd-implement.md` | inherit |
| Going away / stop | Session | `handover.md` | n/a |
| Continue | Session | `resume.md` | inherit |

Promote `feature.md` / `multi-phase.md` / `bootstrap.md` to `full` when: new schema or external service, compliance/money/health, WHAT unclear, or the user asked.

`standard` = `agentic`.

Header required in each playbook file (do **not** use `Gate profile:` / `When:` as the catalog keys):

```text
**Family:** …
**Intent:** …
**Profile:** …
```

`Intent` and `Profile` must be the catalog strings, character-for-character. `refactor.md` repeats the block once per row.

## Tie-breaks

If two rows could match, pick in this order:

1. **Broken / repro** over New behavior when expected behavior already exists and fails.
2. **User should be able to X** over New behavior when `SDD/modules/SPEC_*` for that module already exists.
3. **Shape / UX still open** when HOW/UX is the open question, even if they said “feature”.
4. **How / why / are we sure / blast radius** when they asked a question and did not ask for a change.
5. **Reshape, public contract** over same-contract when callers or schema change.

## pstack-only (do not force an sdd Change playbook)

perf, hillclimb, runtime/trace forensics, visual parity, babysit, shipping, autonomous-run, orchestrate, autopilot-*, worktree cleanup, authoring a skill, eval.

If that work also changes product behavior, still run sdd Step 0 + catalog match first (`with-pstack.md`).
