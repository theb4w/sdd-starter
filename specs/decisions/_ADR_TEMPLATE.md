<!--
═══════════════════════════════════════════════════════════════════════════════
  Template de ADR (Architectural Decision Record)
═══════════════════════════════════════════════════════════════════════════════

  Como usar:
  1. Copie para specs/decisions/ADR-NNN-<slug-em-kebab>.md
  2. NNN = próximo número disponível (consulte specs/SPEC_INDEX.md)
  3. NUNCA reutilizar número, mesmo se ADR rejeitada/superseded
  4. Mínimo 2 alternativas consideradas (idealmente 3)
  5. Cada alternativa requer URL de fonte primária

  Quando criar ADR:
  - CLARIFY revelou trade-off com 2+ alternativas viáveis
  - Decisão tem impacto financeiro / regulatório / de reversão
  - Decisão contradiz "best practice" comum (precisa justificativa explícita)
═══════════════════════════════════════════════════════════════════════════════
-->

# ADR-NNN — <Decisão em uma frase imperativa>

**Status:** 📝 PROPOSTA | ✔️ ACEITO | ❌ REJEITADO | ⏸️ SUPERSEDED por ADR-MMM
**Data:** YYYY-MM-DD
**Autores:** <nomes>
**Spec relacionada:** `specs/modules/SPEC_<X>.md`
**Substitui:** ADR-MMM (se aplicável)

---

## Contexto

> Qual problema motiva a decisão? Quais restrições?

<!-- Inclua:
- O que está acontecendo no projeto agora que torna esta decisão necessária
- Restrições técnicas (versão de runtime, vendor lock-in, infra existente)
- Restrições de negócio (budget, prazo, compliance)
- Por que NÃO podemos adiar esta decisão
-->

---

## Alternativas Consideradas

### Opção A — <nome curto>

**Descrição:** <1-2 frases>

- **Prós:**
  - <ponto positivo concreto>
  - <ponto positivo concreto>
- **Contras:**
  - <ponto negativo concreto>
  - <ponto negativo concreto>
- **Custo:** <financeiro / esforço / risco>
- **Reversibilidade:** <fácil / médio / difícil — explique>
- **Fonte:** <URL primária>

### Opção B — <nome curto>

**Descrição:** <1-2 frases>

- **Prós:** ...
- **Contras:** ...
- **Custo:** ...
- **Reversibilidade:** ...
- **Fonte:** <URL>

### Opção C — <nome curto>

(Mínimo 2 alternativas, idealmente 3)

---

## Decisão

> Escolhemos a **Opção <X>** porque <justificativa em 2-4 linhas concretas>.

<!-- A justificativa deve referenciar:
- Os critérios da §"Contexto" (qual restrição esta opção resolve melhor)
- O trade-off explícito que aceitamos (toda decisão tem custo)
- Por que as outras opções foram rejeitadas (1 frase cada)
-->

---

## Consequências

### Positivas
- <consequência positiva concreta>
- <consequência positiva concreta>

### Negativas (aceitas)
- <consequência negativa que aceitamos como trade-off>
- <consequência negativa>

### Riscos mitigados
- **Risco:** <descrição>
  **Mitigação:** <ação verificável> (não "monitorar")

### Risco residual
- <risco que sobra mesmo após mitigação> — aceito porque <razão>

---

## Como Reverter

> Passos práticos para sair desta decisão se ela falhar.

<!-- Não escrever "fácil de reverter" sem demonstrar. Lista numerada de passos:

1. Provisionar recurso alternativo (Opção B)
2. Migrar dados existentes via script `scripts/migrate-from-X-to-Y.py`
3. Trocar configuração `<MODULO>_PROVIDER` de `X` para `Y`
4. Deploy em staging, validar smoke
5. Deploy em produção em janela de baixo tráfego
6. Marcar este ADR como ⏸️ SUPERSEDED por ADR-MMM
-->

---

## Métricas de Sucesso

> Como saberemos que esta decisão foi acertada? (Definir antes de implementar.)

- <métrica quantificável>
- <métrica quantificável>
- Revisão programada: <data — ex.: "30 dias após deploy em produção">

---

## Anexos

- Spec: `specs/modules/SPEC_<X>.md`
- PLAN: `specs/plans/PLAN_<X>.md`
- Discussão original: <URL de issue/PR/discussion>
- Documentação técnica: <URLs>

---

*Atualizar `specs/SPEC_INDEX.md` após mudança de status.*
