# Playbook: feature

**Family:** Change
**Intent:** New behavior
**Profile:** `agentic`
**Not when:** defect → `bug-fix.md`. Slice of specified module → `user-story.md`. Shape unknown → `design.md`.
**Basis:** spec-kit specify → clarify → plan → tasks → implement. PLAN/TASKS always written. Human GO on HOW only if `full`.
**Skills:** `sdd-tdd`, then `review.md`

Promote to `full` if new schema, new external service, compliance, or WHAT unclear. Large → also `multi-phase.md`.

## Size

Small: ≤100 LOC, 0–1 new files, no architectural trade-off, no new service, no schema change. Else medium/large. Unsure → treat as medium (`agentic` still, unless promote rules fire).

## Steps

1. **Step 0** of `sdd-mode` (ensure `SDD/`). Read BRIEF, INDEX, architecture, handover, SPEC, ADRs.
2. State size and profile (`agentic` or `full`).
3. Contract in `SDD/modules/` (extend or new SPEC). **No production code until the spec file exists.**
4. Product-only CLARIFY → **STOP**. Empirical forks → `prototype.md`, do not ask. ADRs in `SDD/decisions/`; on `agentic` write and proceed (mark PROPOSTA if the human must pick a product option).
5. Write PLAN. If `full`: **STOP GATE 1.** If `agentic`: continue.
6. Write TASKS. If `full`: **STOP GATE 2.** If `agentic`: continue.
7. IMPLEMENT one TASK at a time; `sdd-tdd` when cheap. No per-TASK GO.
8. `review.md`. Fix must-fix once.
9. G3 = `Smoke:` from `SDD/AGENTS.md` on the real surface (evidence in the package). Missing `Smoke:` → must-fix, no accept.
10. **Package** (accept / fix / reject). Branch, not silent `main`. Then `handover.md` + INDEX.

## Reply

Size, profile, `SDD/` paths, package or the one stop.
