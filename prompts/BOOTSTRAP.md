<!--
  Ponte humana. Passos canônicos: .agent/skills/sdd-mode/playbooks/bootstrap.md
-->

# BOOTSTRAP — Inicialização SDD do projeto <PROJETO>

**Playbook:** `.agent/skills/sdd-mode/playbooks/bootstrap.md`  
**Perfil:** `full` (parar no GATE 1 do primeiro módulo)  
**Data:** <DATA_HOJE>  
**Operador:** <SEU_NOME>

Invoque **sdd-mode** (ou cole este bloco). Não escreva código de produção nesta sessão.

```
/sdd-mode bootstrap do projeto <PROJETO>.
PROJECT_BRIEF.md está preenchido.
Playbook: bootstrap.md. Pare no GATE 1.
```

Checklist humano:

- [ ] `PROJECT_BRIEF.md` §1–§6 preenchidos
- [ ] Workspace é o projeto-alvo
- [ ] Git fora de cloud-sync

O agente copia os passos do playbook. Não aceite um plano improvisado que pule SPEC ou GATE 1.
