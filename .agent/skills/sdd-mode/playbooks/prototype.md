# Playbook: prototype

**Gate profile:** `design`
**When:** a fork is empirical (behavior, layout, API feel) and a throwaway sketch is cheaper than asking.
**Not when:** the sketch is intended to ship → that is `feature.md`. Do not merge prototype code to `main`.
**Principles:** prove-it-works, proportional-rigor.

## Steps

1. State the question the prototype must answer in one sentence (yes/no or A vs B).
2. Isolate the work: branch, temp dir, or clearly named throwaway path. Say where it will be deleted.
3. Build the smallest sketch that makes the question observable. No productization (auth, i18n, polish) unless that *is* the question.
4. Run it. Record what you observed (screenshots, output, timings) as evidence in `docs/design/<slug>.md` or the handover.
5. **STOP** for the human to pick. Recommendation allowed; the pick is theirs.
6. Do not clean up by “just keeping the better sketch” on `main`. Next playbook: `design.md` or `feature.md` rewriting the winner as specified work.

## Reply

Question, where the sketch lives, observation, recommendation, waiting on the pick.
