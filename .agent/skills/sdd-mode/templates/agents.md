# AGENTS.md — <!-- ADAPT: PROJECT_NAME -->

Product constitution. Procedure lives in `sdd-mode/` (skill root). Process lives in this `SDD/` tree.

**Smoke:** <!-- ADAPT: exact command or URL the agent must run for G3, e.g. `npm run smoke` or `https://staging.example.com` -->

Until `Smoke:` is a real command or URL, packages cannot be accepted.

## Identity

- **Name:** <!-- ADAPT -->
- **What / who:** <!-- ADAPT: 1–2 sentences -->
- **Stage:** <!-- ADAPT: Greenfield | MVP | Beta | Production -->
- **Method:** SDD — `sdd-mode` (catalog + playbook). Default profile `agentic` (ADR-003).

## Absolute rules

1. **Spec-first.** No production code without the playbook contract (SPEC, story, or none on bug-fix).
2. **Stops follow the catalog row.** `agentic`: product CLARIFY + package. `full`: also G1 PLAN and G2 TASKS. Never-block on HOW is `agentic`. Do not skip the package. sdd-mode does not merge `main`.
3. **Primary source.** Technical choice needs a URL or it is blocked (ADR in `SDD/decisions/`).
4. **No secrets in git or logs.** Sensitive here: <!-- ADAPT: PII / PHI / PCI / none -->
5. **Backward-compat.** Each commit on `main` preserves the previous working state.
6. **Traceability.** Code → TASK → SPEC → ADR, all under `SDD/`.

## Stack (pinned)

| Layer | Tech | Version | Source URL |
|---|---|---|---|
| <!-- ADAPT --> | | | |

## Out of scope

- <!-- ADAPT -->

## Git

Conventional Commits. PR budget: feat ≤250 LOC, fix ≤100, refactor ≤200. No force-push to `main`.

---

*Keep in sync with `SDD/INDEX.md`. Do not paste `workflow.md` here.*
