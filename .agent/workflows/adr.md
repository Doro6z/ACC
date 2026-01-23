---
description: Propose Architecture Decision Record for strategic or architectural changes
---

# /adr Workflow

This workflow creates an ADR (Architecture Decision Record) when significant decisions affect L1 or L2.

## Steps

1. **Load Context**
   Read mandatory context:
   - `L0_Intent/Mission.md`
   - `L0_Intent/Constraints.md`
   - `L1_Strategy/Goals.md`
   - `L1_Strategy/Roadmap.md`
   - Relevant `L2_Design/` documents (if applicable)

2. **Verify Necessity**
   ADR required if decision affects:
   - Strategic objectives (L1)
   - Core architecture (L2)
   - Technology choices
   - Breaking changes
   - Roadmap phase transitions
   
   If NOT strategic → suggest simpler documentation

3. **Draft ADR**
   Create ADR following structure:
   - **Status**: Proposed
   - **Context**: What problem are we solving?
   - **Decision**: What approach are we taking?
   - **Rationale**: Why this choice? (cite L5 research if applicable)
   - **Consequences**: What are the impacts?
   - **Alternatives Considered**: What was rejected and why?

4. **Output**
   - Write to `L1_Strategy/ADR/ADR_YYYY-MM-DD_<Title>.md`
   - Status: Proposed (NEVER Accepted automatically)
   - Present to human for review
   - **WAIT for human decision**: Accept / Reject / Revise

## Constraints
- ADRs are append-only once accepted
- No execution based on ADR without human approval
- Status changes only by human
- All output in French

## Post-Approval
If accepted by human:
- Update status to Accepted
- Link to relevant L1/L2 documents
- Archive decision for future reference
