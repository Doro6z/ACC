# Language Convention — Agentic Command Center

> Defines language usage across the Command Center.
> This document is human-authored and governance-level.

---

## Purpose

Ensure clarity, robustness, and separation of concerns between:
- agent-facing contracts
- human-facing documentation

Language choice is intentional and functional.

---

## Language Rules

### Agent-Facing Documents → ENGLISH ONLY
Applies to:
- All `AI_Guard.md`
- All `Lω_Agentic/*` (Personas, Rules, Workflows)
- Any document directly consumed as execution rules by agents

Rationale:
- Normative keywords (MUST, MUST NOT, STOP)
- Reduced ambiguity
- Cross-model robustness
- Reusability and portability

---

### Human-Facing Documents → FRENCH (default)
Applies to:
- Mission, Constraints, Goals, Roadmap
- `_Guidance.md`
- Design and documentation intended for reading or decision-making

Technical terms in English are allowed when relevant.

---

### Mixed or Ambiguous Documents → FORBIDDEN
No document may mix:
- agent-facing rules
- human-facing explanations

If dual purpose is needed:
→ split into two documents.

---

## Enforcement

Agents MUST respect this convention.
Any violation → STOP and human escalation.

---

*This convention is stable.
Changes require explicit human action in Lω.*
