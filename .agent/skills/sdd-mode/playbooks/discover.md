# Playbook: discover

**Gate profile:** `observe` until the brief is accepted; then `bootstrap.md`
**When:** existing codebase with missing or stale docs.
**Not when:** `SDD/BRIEF.md` is already trustworthy → `bootstrap.md`.
**Principles:** spec-first, traceability, one-home-per-fact.

## Steps

1. Ensure `SDD/` (skill preamble). No production edits.
2. Inventory languages, entrypoints, tests, CI, deploy, README. Trust code over README.
3. Infer product and user. Mark guesses `[?]`.
4. Fill `SDD/BRIEF.md` from evidence.
5. **STOP** for the human to confirm BRIEF (especially `[?]` and out-of-MVP).
6. Draft `SDD/architecture.md` (inferred vs confirmed).
7. Populate `SDD/INDEX.md` with detected modules.
8. Thin retrospective SPECs in `SDD/modules/`. Do not invent desired behavior.
9. Candidate ADRs in `SDD/decisions/` for decisions already in the code. Do not mark ACEITO without the human.
10. Adapt `SDD/AGENTS.md` to the detected stack.
11. `handover.md`. Next: `bootstrap.md` only for new work.

## Reply

What the system is, `[?]` open, `SDD/` files written. No code changed.
