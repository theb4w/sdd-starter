# Playbook: handover

**Gate profile:** n/a (does not ship code)
**When:** phase closed, pause > ~30 min, after G3, or context exhausted.
**Human prompt (pointer):** `prompts/HANDOVER.md`
**Template:** `docs/_HANDOVER_TEMPLATE.md`

## Steps

1. Copy the template to `docs/handover_<MODULO>[_FASE_X]_<YYYY-MM-DD>.md`.
2. Fill every section. Use `N/A` with a reason rather than omitting.
3. Facts only: TASK ids and ACs actually verified, paths, commit hashes, open questions.
4. Update `specs/SPEC_INDEX.md` status and history row.
5. Do not commit unless the human asks. Handover is reviewed before GATE 4 of the surrounding work.

## Reply

Path of the handover file, SPEC_INDEX delta, next recommended playbook.
