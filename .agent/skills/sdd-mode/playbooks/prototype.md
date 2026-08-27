# Playbook: prototype

**Gate profile:** `design`
**Basis:** spec-kit “parallel implementations” / creative exploration. Observe, then specify; do not merge the sketch as the spec.
**When:** an empirical fork; throwaway sketch is cheaper than asking.
**Not when:** the sketch is meant to ship → `feature.md`. Do not merge to `main`.

## Steps

1. Ensure `SDD/`. State the question in one sentence.
2. Isolate: branch, temp dir, or throwaway path. Say where it will be deleted.
3. Smallest sketch that makes the question observable.
4. Record observation in `SDD/design/<slug>.md`.
5. **STOP** for the human to pick.
6. Winner is rewritten via `design.md` / `feature.md`, not kept as prototype on `main`.

## Reply

Question, sketch location, observation, waiting on the pick.
