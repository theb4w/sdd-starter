# Playbook: discover

**Gate profile:** `observe` until the brief is accepted; then hand off to `bootstrap.md`
**When:** existing codebase with missing or stale docs.
**Not when:** the brief is already trustworthy → `bootstrap.md`. Code changes requested → classify as bug/feature/refactor after discover, do not mix.
**Principles:** spec-first, traceability, one-home-per-fact.
**Human prompt (pointer):** `prompts/DISCOVER.md`

## Preconditions

- [ ] This is the real repo (code exists)
- [ ] No production edits in this playbook

## Steps

1. Inventory: languages, entrypoints, tests, CI, deploy, README age. Do not trust the README over the code.
2. Infer what the product does and for whom. Mark guesses with `[?]`.
3. Fill `PROJECT_BRIEF.md` from evidence. Leave `[?]` where the code cannot answer.
4. **STOP** for the human to confirm the brief (especially `[?]` and out-of-MVP).
5. Draft `docs/<Project>_Architecture.md` as a reverse-engineering sketch. Label inferred vs confirmed.
6. Populate `specs/SPEC_INDEX.md` with detected modules and status (`✔️` / `🚧` / `📝` / `❌`).
7. For each critical module, a thin retrospective SPEC (objective, current behavior, unknown). Do not invent desired behavior as if it were already specified.
8. Propose candidate ADRs for decisions already baked into the code (still 2+ alternatives + URL). Do not mark ACEITO without the human.
9. Adapt `AGENTS.md` to the detected stack.
10. `handover.md` for discovery. Next session: `bootstrap.md` only if they want new work, or `onboarding.md` if they only needed the map.

## Reply

What the system is, `[?]` still open, modules found, candidate ADRs, files written. Explicit: no code was changed.
