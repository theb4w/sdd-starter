# Playbook: resume

**Family:** Session
**Intent:** Continue
**Profile:** inherit
**Not when:** starting a module → `bootstrap.md` / `feature.md`. No `SDD/` → **Step 0** then `onboarding.md` or `discover.md`.
**Basis:** spec-kit artifacts live in git so a new session does not reconstruct intent from chat.

No extra human GO. Continue unless the checks below fail.

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). Read latest handover, `SDD/INDEX.md`, SPEC, PLAN/TASKS for this phase.
2. Verify workspace/branch vs handover. **Mismatch → stop** and say so.
3. Restate done vs next TASK, gates already passed, inherited profile.
4. **STOP** only if the handover left `full` waiting on G1 or G2, or an irreversible op is next. Do not relitigate accepted ADRs. Do not ask GO merely because the session is new.
5. Continue with the parent playbook's remaining steps.

## Reply

Handover path, next TASK, inherited profile, whether you continued or stopped (mismatch / `full` gate).
