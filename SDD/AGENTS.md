# AGENTS.md — sdd-starter

Skill pack SDD. O procedimento está em `.agent/skills/sdd-mode/`. O processo deste pack está nesta pasta `SDD/`.

## Regras

1. **Spec-first.** Sem contrato do playbook (SPEC, story, ou nenhum em bug-fix), sem código de produção.
2. **Gates pelo perfil.** `observe` / `design` / `lite` / `standard` / `full` — ADR-002. Não aliviar o perfil sem reclassificar.
3. **Fonte primária.** Decisão técnica com URL; senão ADR bloqueada.
4. **Sem secrets em git ou logs.** Sensível neste pack: nenhum (não há app).
5. **Backward-compat.** Commit em `main` preserva o estado anterior.
6. **Rastreabilidade.** Código (se houver) → TASK → SPEC → ADR, tudo sob `SDD/`.
7. **Uma casa.** Playbooks em `.agent/skills/sdd-mode/playbooks/`. Artefatos do produto em `SDD/`. Não reviver `specs/`, `docs/`, `prompts/`, `QUICKSTART/`.

## Módulos

Fonte: `SDD/INDEX.md`. Hoje: SDD_MODE.

## Fora de escopo

- Plugin Cursor como core
- Never-block / merge overnight
- Stack obrigatória
