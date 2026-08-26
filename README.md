# sdd-starter

Skill de **Spec-Driven Development**. Não é um app e não é uma pasta cheia de docs para copiar à mão.

1. Leve `.agent/skills/` para o repo do produto (ou use este repo como template).
2. Invoque **`sdd-mode`**.
3. O modo escolhe o playbook e **gera `SDD/`** com brief, constituição, SPECs, ADRs, plans, stories, design e handovers.

```text
/sdd-mode bootstrap deste projeto
/sdd-mode discover
/sdd-mode feature: …
/sdd-mode bug-fix: …
```

| Peça | Onde |
|---|---|
| Procedimento (playbooks, principles, templates) | `.agent/skills/sdd-mode/` |
| Processo do **produto** (gerado) | `SDD/` |
| Método (o quê / por quê) | `.agent/skills/sdd-mode/references/workflow.md` |

Não recrie `specs/`, `docs/`, `prompts/`, `QUICKSTART/` ou `scripts/` de processo. Se `SDD/` ainda não existe, o primeiro playbook cria.

MIT. Ver `LICENSE`.
