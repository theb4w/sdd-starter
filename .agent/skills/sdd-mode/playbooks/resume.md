# Playbook: resume

**Gate profile:** inherit the phase already approved (do not re-open GATE 1/2 unless the human rejects prior artifacts)
**When:** continuing after a handover, with PLAN/TASKS already approved for this phase.
**Not when:** starting a module → `bootstrap.md` / `feature.md`. Repo unknown → `onboarding.md` then this.
**Human prompt (pointer):** `prompts/RESUME.md`

## Steps

1. Read, in order: `docs/SDD_WORKFLOW.md` (method), `AGENTS.md`, latest `docs/handover_*`, `SPEC_INDEX.md`, SPEC, PLAN section for this phase, TASKS for this phase, domain skills.
2. Verify workspace, branch, HEAD. If they do not match the handover, stop and say so.
3. Restate: what is done, what TASK is next, which gates already passed, which profile applies.
4. **STOP** for GO to start the next TASK. Do not relitigate accepted ADRs.
5. Continue with the playbook that owns the remaining work (`tdd-implement.md`, `feature.md` IMPLEMENT steps, `multi-phase.md`, `bug-fix.md`, …). Copy those steps from here on.

## Reply

Handover file, next TASK id, inherited profile, first action after GO.
