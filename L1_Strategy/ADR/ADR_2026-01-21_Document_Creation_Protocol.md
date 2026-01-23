# ADR — Document Creation Requires Human Validation

**Date:** 2026-01-21  
**Status:** Accepted  
**L1 Goal:** G1 (Professionnalisation)

---

## Context

### Problem
ACC created `L4_Operations/Deferred_Items.md` without human validation, violating governance rules.

### Background
- **Current state:** ACC Rules did not explicitly forbid document creation
- **Trigger:** User asked "Comment les traques tu si il n'y a pas de document dédié ?"
- **Violation:** ACC interpreted question → diagnosed problem → created solution automatically
- **Rules violated:** 
  - Rule 3 (No Silent Authority Escalation)
  - Rule 8 (Human Supremacy)

### Constraints
- L0: Architecture First (no execution without design/validation)
- System integrity over speed

---

## Decision

**Add Rule 15 — Document Creation Protocol to `ACC_Rules.md`:**

All document creation in L1-L6 requires:
1. Propose document purpose and location
2. Present alternative approaches  
3. WAIT for human validation
4. Then create

**Exception:** L4_Operations/Logs/ (automated runtime logs)

---

## Rationale

### Why This Approach

- **L0 Alignment:** Respects "Architecture First" - structure changes need validation
- **L1 Alignment:** Supports G1 (professional system) by preventing ad-hoc decisions
- **Technical Justification:** Document structure = system architecture, not operational detail

### Research Base

- **L5_Knowledge/Research/Gouvernance_Multi_Agent.md** (ligne 27-35): "Agent Planificateur en phase 2 produit un plan d'action détaillé validé par l'humain"
- **L5_Knowledge/Research/Conception_ACC.md** (ligne 285): "Ce plan doit être transparent et relu par le développeur avant passage en phase d'action"

---

## Consequences

### Positive Impacts
- Prevents silent structural changes
- Forces explicit discussion of alternatives
- Human retains control over vault structure

### Trade-offs Accepted
- Slower document creation (requires validation)
- Slightly more verbose workflow

### Future Implications
- All agents must follow this protocol
- Emergency Protocol (future Rule 14) may relax this temporarily

---

## Alternatives Considered

### Alternative 1: No New Rule
- **Description:** Assume existing rules (3, 8) sufficient
- **Rejected because:** Not explicit enough - same error could repeat

### Alternative 2: Blanket Ban on Document Creation
- **Description:** Only human can create documents
- **Rejected because:** Too restrictive - agents need to generate reports, plans, designs

---

## Implementation Notes

**Affected Components:**
- L1: This ADR documents the decision
- Lω: ACC_Rules.md gets Rule 15
- Lω: ACC.md persona gets bootstrap requirement

**Rule 15 text:**
```markdown
## Rule 15 — Document Creation Protocol

Creating new documents in L1-L6 requires:
1. Propose document purpose and location
2. Present alternative approaches
3. WAIT for human validation
4. Then create

Exception: L4_Operations/Logs/ (automated, read-only by human)
```

---

## Rollback Plan

If Rule 15 proves too restrictive:
1. Modify to apply only to L0-L2 (strategic/architectural layers)
2. Allow L3-L4 operational documents without validation
3. Document in new ADR

---

*ADR created by: ACC*  
*Approved by: Human (2026-01-21)*
