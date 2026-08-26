# Playbook: design

**Gate profile:** `design`. No production code.
**When:** UX/module/flow still open.
**Not when:** shape already in a SPEC → `feature.md`. Cheap experiment → `prototype.md` first.
**Template:** `templates/design.md`

## Steps

1. Ensure `SDD/`.
2. Name user and problem. Constraints from `SDD/BRIEF.md` and INDEX.
3. Write `SDD/design/<slug>.md` from the template. 2–3 options, each with consequences and a URL if it implies technology.
4. Recommend one. List open questions (future CLARIFY/ADR).
5. **STOP** for human approval of that file.
6. After approval: `feature.md` / `bootstrap.md` or ADRs. Do not IMPLEMENT from the design file alone.

## Reply

`SDD/design/` path, options, recommendation, waiting on approval.
