# sdd-starter

Skill de **Spec-Driven Development**. Não é um app e não é uma pasta cheia de docs para copiar à mão.

1. Instale no host (`sdd-mode/references/install.md`). Este checkout: `.agent/skills/`. No **Cursor**, a rule `.cursor/rules/sdd-under-pstack.mdc` já aponta para essa pasta.
2. Invoque **`sdd-mode`** — sozinho ou **de dentro do pstack / poteto-mode** (pstack executa; sdd-mode é a camada de contrato). Ver `sdd-mode/references/with-pstack.md`.
3. O modo casa a intenção no catálogo (`references/catalog.md`) e **gera `SDD/`** (Step 0). Preencha **`Smoke:`** em `SDD/AGENTS.md` (comando ou URL). Sem isso o pacote não aceita.

```text
/poteto-mode o usuário precisa exportar o relatório em CSV
/sdd-mode bootstrap deste projeto
/sdd-mode discover
/sdd-mode bug-fix: …
```

| Peça | Onde |
|---|---|
| Procedimento | `<skill-root>/sdd-mode/` |
| Processo do produto | `SDD/` na raiz do alvo |
| Catálogo (ganha se houver drift) | `sdd-mode/references/catalog.md` |
| Método (apêndice; não vai no todo) | `sdd-mode/references/workflow.md` |
| Dry-run deste pack | `sdd-mode/references/dry-run.md` |

Não recrie `specs/`, `docs/`, `prompts/`, `QUICKSTART/` ou `scripts/` de processo.

MIT. Ver `LICENSE`.
