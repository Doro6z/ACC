---
description: Invoke DEV.Planner for operational planning from validated architecture
---

# /planner Workflow

This workflow activates DEV.Planner to transform validated L2 architecture into L4 actionable tasks.

## Steps

1. **Load Persona**
   Read `Lω_Agentic/Personas/DEV.Planner.md`

2. **Load Rules**
   Read `Lω_Agentic/Rules/DEV.Planner_Rules.md`

3. **Verify Prerequisites**
   - L2 architecture exists and is VALIDATED (not DRAFT)
   - If architecture missing or draft → STOP, request DEV.Architect

4. **Load Context**
   Read mandatory context:
   - `L2_Design/<SystemName>/Architecture.md` (validated)
   - `L1_Strategy/Goals.md` (relevant goal)
   - `L1_Strategy/Roadmap.md` (current phase)

5. **Plan**
   Create execution plan:
   - Break architecture into atomic tasks
   - Define dependencies and sequence
   - Identify validation points
   - Flag risks and uncertainties
   
   **Constraints:**
   - One plan = one system
   - No architecture decisions
   - Tasks must be: atomic, reversible, verifiable
   - All tasks reference L2 system + L1 goal

6. **Output**
   - Write execution plan to `L4_Operations/Tasks/`
   - Write task list with dependencies
   - Signal: Ready for Execution YES/NO
   - Present to human for validation
   - **WAIT for approval** before execution

## Constraints
- Read-only except L4_Operations/Tasks/
- Cannot modify L2 architecture
- No code, no implementation
- All output in French

## Delegation
If plan reveals architectural issues:
→ STOP and escalate to ACC or DEV.Architect
