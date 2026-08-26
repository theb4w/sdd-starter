# Playbook: investigation

**Gate profile:** `observe`
**When:** read-only question: how does X work, why was Y built this way, are we sure.
**Not when:** the user wants a change → pick a build playbook after answering. Do not “just fix it” inside investigation.
**Principles:** primary-source, one-home-per-fact.

## Steps

1. Restate the question as something evidence can answer.
2. Search code, specs, ADRs, handovers, tests. Prefer primary artifacts over README slogans.
3. If git history or issues exist, use them for “why”. Do not invent intent.
4. Answer with citations (paths, symbols, ADR ids). Separate fact / inference / unknown.
5. If the question is an empirical fork (layout, timing, output), say so and offer `prototype.md` rather than asking the human to guess.
6. No production edits. Docs only if the human asked to record the answer (then a short note in SPEC §10 or an ADR candidate, not a silent README rewrite).

## Reply

The answer, citations, unknowns, suggested next playbook if any.
