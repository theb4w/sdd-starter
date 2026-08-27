# Community SDD (basis for this pack)

This pack does not invent Spec-Driven Development. It implements the community cycle that Google Antigravity documents and that GitHub **spec-kit** standardizes.

## Canonical cycle (spec-kit)

Source: https://github.github.io/spec-kit/concepts/sdd.html  
Toolkit: https://github.com/github/spec-kit  
Antigravity + spec-kit: https://codelabs.developers.google.com/sdd-adk-antigravity  
Antigravity intro (SSOT, design-implementation loop, modular granularity): https://codelabs.developers.google.com/codelabs/getting-started-with-spec-driven-development-in-antigravity

| spec-kit / Antigravity | This pack | Artifact |
|---|---|---|
| `/speckit.constitution` | `SDD/AGENTS.md` (generated once, amended) | non-negotiable principles |
| `/speckit.specify` | playbooks `bootstrap` / `feature` / `user-story` | `SDD/modules/SPEC_*.md` (WHAT, tech-agnostic) |
| `/speckit.clarify` | SPEC §9 CLARIFY | answers in SPEC §10 |
| `/speckit.plan` | PLAN after clarify | `SDD/plans/PLAN_*.md` (HOW) |
| `/speckit.tasks` | TASKS | `SDD/plans/TASKS_*.md` |
| `/speckit.analyze` | agent self-check + `review.md` | cross-check spec/plan/tasks/diff |
| `/speckit.implement` | IMPLEMENT + `sdd-tdd` | code; TDD is the test spec as judge |
| Greenfield 0-to-1 | `bootstrap` | brief → constitution → first SPEC |
| Brownfield iterative | `discover` then change playbooks | reverse-spec existing code |
| Creative exploration | `design` / `prototype` | parallel options before locking HOW |

## Software-engineering roots (not slogans)

| Idea | Classic source | Where it lands here |
|---|---|---|
| Requirements as the contract (WHAT before HOW) | ISO/IEC/IEEE 29148 requirements engineering | SPEC / story; `principle-spec-first` |
| Spec is SSOT; update spec when intent changes | Antigravity SDD lab §7; spec-kit “executable specs” | never treat chat as the contract |
| Modular units, isolate regeneration | Parnas 1972, *On the Criteria To Be Used in Decomposing Systems into Modules* https://dl.acm.org/doi/10.1145/361598.361623 | one SPEC per module; `principle-sequence-verifiable-units` |
| Record *why* we chose X over Y | Nygard, *Documenting Architecture Decisions* (2011) https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions | ADR; `principle-primary-source` |
| Test before production code | Beck / Fowler, TDD https://martinfowler.com/bliki/TestDrivenDevelopment.html | `sdd-tdd`; test spec as judge (Antigravity lab) |
| V-model: verify against the spec, not “it compiles” | IEEE 1012 V&V; Antigravity “test specification is the judge” | `principle-prove-it-works` (G3) |
| Characterization tests before changing legacy | Feathers, *Working Effectively with Legacy Code* | `discover`, `refactor` |
| User story as a vertical slice | Cohn, *User Stories Applied*; Cockburn use cases | `user-story` playbook |
| Continuing change / compatibility | Lehman’s laws of software evolution | `principle-backward-compat` |
| Secrets out of the repo | OWASP Secrets Management Cheat Sheet https://cheatsheetseries.owasp.org/cheatsheets/Secrets_Management_Cheat_Sheet.html | `principle-no-secrets` |
| Least data in logs | OWASP Logging Cheat Sheet https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html | `principle-privacy-logging` |
| Human gates on generated work | spec-kit short path; Antigravity one plan GO; this pack default `agentic` (ADR-003) | product CLARIFY + package; G1/G2 only on `full` |
| Ceremony proportional to risk | ISO/IEC 12207 tailoring; spec-kit “shorter path for small features” | `principle-proportional-rigor` |

## What this pack refuses (pstack, not spec-kit)

pstack’s “the best spec is code” is rejected (spec remains SSOT). Never-block on **HOW** is profile `agentic`. Never-block does not skip the contract or the package. Overnight land is pstack `shipping` after `review.md`+G3, only if the human asked. sdd-mode does not merge `main`. What we copy is **agent review after implementation** (`review.md`).

## How to write a skill here

Follow the pstack leaf shape so the text is engineering, not atmosphere:

1. **Rule** — one imperative sentence.
2. **Why** — failure mode if ignored (cost, defect class, reviewability).
3. **Pattern** — observable steps.
4. **Boundaries** — when the rule does not apply.
5. **Source** — URL in this file or a primary standard. No URL → do not keep the claim.
