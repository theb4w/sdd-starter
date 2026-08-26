# Playbook: onboarding

**Gate profile:** `observe`
**When:** first session on a repo that already uses SDD, or a new person/agent joining.
**Not when:** the repo has no SDD artifacts → `discover.md`.
**Human prompt (pointer):** `prompts/ONBOARDING.md`

## Steps

1. Read and summarize, in order:
   - `AGENTS.md` (absolute rules)
   - optional `tooling/` files the project actually adopted
   - `.agent/skills/sdd-mode/SKILL.md` and domain skills
   - `specs/SPEC_INDEX.md`
   - `docs/<Project>_Architecture.md` if present
   - latest `docs/handover_*.md`
2. Answer, in this order, **before any code**:
   - a. Which absolute rules bind you?
   - b. Which versions are pinned, and why (ADR/URL)?
   - c. Which modules exist and their status?
   - d. Which accepted ADRs affect today's work?
   - e. Which playbook should today's request use?
3. Wait. Do not implement in the onboarding turn.

## Reply

The five answers above, then the recommended next playbook.
