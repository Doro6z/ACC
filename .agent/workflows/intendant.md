---
description: Invoke ACC.Intendant for system analysis and reporting
---

# /intendant Workflow

This workflow activates the ACC.Intendant agent for internal analysis.

## Steps

1. **Load Persona**
   Read `Lω_Agentic/Personas/ACC.Intendant.md`

2. **Load Rules**
   Read `Lω_Agentic/Rules/ACC.Intendant_Rules.md`

3. **Load Context**
   Read mandatory context:
   - `L0_Intent/Mission.md`
   - `L0_Intent/Constraints.md`
   - `L1_Strategy/Goals.md`
   - `L1_Strategy/Roadmap.md`
   - `L4_Operations/Objective_Tracking.md`
   
   **AND** all relevant research documents:
   - `L5_Knowledge/Research/*.md` (scan directory, load pertinent files based on task)

4. **Analyze**
   Based on user request, perform internal analysis only.
   
   **Constraints:**
   - No external research. No code. No execution.
   - **Do NOT infer strategy without citing L5 research files**
   - All strategic recommendations MUST reference at least one L5 document
   - If no research exists for the topic → STOP and report gap

5. **Output**
   Generate report following `Templates/T_Intendant_Report.md`
   Write to `L4_Operations/Reports/Report_YYYY-MM-DD.md`

## Constraints
- Read-only except Reports folder
- No decisions, only recommendations
- All output in French to human
