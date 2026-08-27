# Playbook: discover

**Family:** Arrive
**Intent:** Legacy repo, no docs
**Profile:** `observe`
**Not when:** `SDD/BRIEF.md` is already trustworthy → `bootstrap.md`.
**Basis:** spec-kit brownfield; Feathers characterization. Reverse-spec what the code does.

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). No production edits.
2. Inventory languages, entrypoints, tests, CI, deploy, README. Trust code over README.
3. Infer product and user. Mark guesses `[?]`.
4. Fill `SDD/BRIEF.md` from evidence.
5. **STOP** for the human to confirm BRIEF (especially `[?]` and out-of-MVP).
6. Draft `SDD/architecture.md` (inferred vs confirmed).
7. Populate `SDD/INDEX.md` with detected modules.
8. Thin retrospective SPECs in `SDD/modules/`. Do not invent desired behavior.
9. Candidate ADRs in `SDD/decisions/`. Do not mark ACEITO without the human.
10. Adapt `SDD/AGENTS.md` to the detected stack, including **`Smoke:`** (how this repo is proven — test command, binary, or URL).
11. `handover.md`. Next: `bootstrap.md` only for new work.

## Reply

What the system is, `[?]` open, `SDD/` files written. No code changed.
