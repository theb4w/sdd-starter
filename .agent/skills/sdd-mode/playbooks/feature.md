# Playbook: feature

**Gate profile:** small → `standard`. Medium/large → `full`. Large also uses `multi-phase.md`.
**When:** new or changed intended behavior.
**Not when:** defect → `bug-fix.md`. Slice of specified module → `user-story.md`. Shape unknown → `design.md`.
**Skills:** `sdd-tdd`

## Size

Small only if all hold: ≤100 LOC, 0–1 new files, no architectural trade-off, no new external service, no schema change. Unsure → upgrade.

## Steps

1. Ensure `SDD/`. Read BRIEF, INDEX, architecture, latest handover, affected SPEC, ADRs.
2. State size, profile, files, trade-offs, CLARIFY. **STOP** if size is disputed.
3. Contract in `SDD/modules/`: small extends existing SPEC; medium/large new or v2 from `templates/spec.md`. **No production code.**
4. Resolve CLARIFY in SPEC §10. ADRs in `SDD/decisions/`. **STOP** for ADR acceptance.
5. If `full`: `SDD/plans/PLAN_*.md`. **STOP GATE 1.**
6. `SDD/plans/TASKS_*.md`. **STOP GATE 2.**
7. IMPLEMENT one TASK; `sdd-tdd` when cheap.
8. **STOP GATE 3.** **STOP GATE 4.**
9. `handover.md`. Update `SDD/INDEX.md`.

## Reply

Size, profile, `SDD/` paths, waiting gate.
