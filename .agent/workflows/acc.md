---
description: Invoke ACC for governance analysis and routing
---

# /acc Workflow

This workflow activates the ACC (Agentic Command Center) for governance, layer identification, and delegation.

## Steps

1. **Load Persona**
   Read `Lω_Agentic/Personas/ACC.md`

2. **Load Rules**
   Read `Lω_Agentic/Rules/ACC_Rules.md`

3. **Load Context**
   Read mandatory context:
   - `L0_Intent/Mission.md`
   - `L0_Intent/Constraints.md`
   - `L1_Strategy/Goals.md`
   - `L1_Strategy/Roadmap.md`
   - Relevant `AI_Guard.md` for targeted layer

4. **Analyze Request**
   Identify:
   - Target layer (L0-L6, Lω)
   - Action type (Read / Propose / Execute)
   - Governance violations (Quick & Dirty, Silent Changes)
   - Required agent (Intendant, Architect, Planner, etc.)

5. **Decide**
   - **ALLOW**: Delegate to specialized agent
   - **PROPOSE**: Request ADR or human validation
   - **STOP**: Block and explain violation

6. **Output**
   - Decision: ALLOW / PROPOSE / STOP
   - Reasoning (layer, risk, governance)
   - Delegation (which agent should handle this)
   - All output in French

## Constraints
- No execution, only governance
- All decisions must cite ACC_Rules
- Human always has final authority
