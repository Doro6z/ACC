# L5 Knowledge — Guide

**Purpose:** Central knowledge repository for strategic research, technical patterns, system analysis, and reusable guides.

**Structure:**

```
L5_Knowledge/
  ├── Research/       Strategic, long-term governance and methodology
  ├── Technical/      UE5 patterns, architectures, technical solutions
  ├── PostMortems/    Analysis of existing systems (successes/failures)
  └── Templates/      Reusable how-to guides and checklists
```

---

## Research/ — Strategic Knowledge

**Content:**
- Governance methodologies
- Agentic system design
- Development philosophy
- Long-term career strategy

**Who uses:**
- ACC.Intendant (mandatory citations for strategic recommendations)
- ACC (governance decision basis)
- DEV.Architect (high-level principles)

**Who contributes:**
- Human (strategic insights)
- ACC.Intendant (synthesis of experience)

**Examples:**
- `Audit_L1_Objectifs.md`
- `Conception_ACC.md`
- `Gouvernance_Multi_Agent.md`

---

## Technical/ — UE5 Patterns & Architecture

**Content:**
- UE5 replication patterns
- System architecture blueprints
- Performance optimization techniques
- C++/Blueprint best practices

**Who uses:**
- DEV.Architect (design references)
- DEV.Planner (technical constraints understanding)
- Future DEV.Coder (implementation patterns)

**Who contributes:**
- Human (discovered patterns)
- DEV.Architect (documented designs that became patterns)

**Examples:**
- `UE5_Replication_Patterns.md`
- `Audio_System_Architecture.md`
- `Procedural_Animation_Techniques.md`

---

## PostMortems/ — System Analysis

**Content:**
- Analysis of existing Apex Primal systems
- What worked, what didn't
- Extractability assessment
- Lessons learned

**Who uses:**
- DEV.Architect (avoid past mistakes)
- ACC.Intendant (evaluate extraction feasibility)
- DEV.Planner (realistic effort estimation)

**Who contributes:**
- Human (hands-on experience)
- ACC.Intendant (structured analysis)

**Examples:**
- `ApexPrimal_AudioSystem.md`
- `ApexPrimal_ClimbingSystem.md`
- `ApexPrimal_SpeciesSystem.md`

---

## Templates/ — Reusable Guides

**Content:**
- Step-by-step extraction guides
- Publishing checklists
- Integration procedures
- Common workflows

**Who uses:**
- All agents (procedural guidance)
- Human (quick reference)

**Who contributes:**
- Human (proven workflows)
- DEV.Architect (design procedures)
- DEV.Planner (planning procedures)

**Examples:**
- `How_To_Extract_UE5_Asset.md`
- `Publishing_Marketplace_Checklist.md`
- `Replication_Setup_Guide.md`

---

## Contribution Guidelines

### Adding Research
- Must be strategic, not tactical
- Must be validated by experience
- Should cite external sources if applicable

### Adding Technical
- Must include working example or reference
- Should follow UE5 official standards
- Must explain "why", not just "how"

### Adding PostMortem
- Must follow template: Context / What Worked / What Failed / Lessons / Extractability
- Should be objective, not emotional
- Must link to L1 goal if extraction is target

### Adding Template
- Must be step-by-step actionable
- Should include validation checkpoints
- Must be tested at least once

---

## Access Pattern

**All agents may READ L5.**  
**Only ACC.Intendant, Human, and (future) specific agents may WRITE L5.**

---

*L5 Knowledge grows organically with project experience.*
