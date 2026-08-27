# Playbook: design

**Gate profile:** `design`. No production code.
**When:** UX/module/flow still open.
**Not when:** shape already in a SPEC → `feature.md`. Cheap experiment → `prototype.md` first.
**Basis:** Antigravity SDD human step 2 (architectural design) and spec-kit creative exploration. Options before locking HOW. IEEE-style design description, not code.
**Template:** `templates/design.md`

## Steps

1. Ensure `SDD/`.
2. Name user and problem. Constraints from `SDD/BRIEF.md` and INDEX.
3. Write `SDD/design/<slug>.md` from the template. 2–3 options, each with consequences and a URL if it implies technology.
4. Recommend one. List open questions (future CLARIFY/ADR).
5. If a prototype already settled the fork, record that in the file and continue — no extra GO.
6. Else **STOP** once for approval of the recommendation.
7. After GO: `feature.md` / `bootstrap.md`. Do not IMPLEMENT from the design file alone.

## Reply

`SDD/design/` path, options, recommendation, waiting on approval.
