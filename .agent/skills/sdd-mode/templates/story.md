<!--
  Template de user story (fatia vertical).
  Copie para SDD/stories/STORY_<SLUG>.md
  Requer um módulo com SPEC existente. Módulo novo → SPEC, não story.
-->

# STORY_<SLUG> — <título curto>

**Status:** 📝 RASCUNHO | ✅ APROVADO | 🚧 IMPLEMENT | ✔️ CONCLUÍDO
**Módulo:** `SDD/modules/SPEC_<MODULO>.md`
**Perfil de gate:** `standard` | `lite`
**Data:** YYYY-MM-DD

---

## História

Como **<persona>**, quero **<ação>**, para **<valor>**.

---

## Critérios de aceite

Use Given / When / Then. Cada linha vira um teste RED em `sdd-tdd`.

1. **Given** <contexto>, **When** <ação>, **Then** <resultado observável>
2. **Given** …, **When** …, **Then** …

---

## Fora desta story

- ❌ <não fazer agora>

---

## Rastreio

- SPEC: `SDD/modules/SPEC_<MODULO>.md` §
- ADRs: 
- TASKS: `SDD/plans/TASKS_<MODULO>.md` (se perfil `standard`)

---

## Notas

> Trade-off ou CLARIFY. Se mudar regra do módulo, atualize a SPEC — não contradiga em silêncio.
