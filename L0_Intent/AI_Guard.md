# AI Guard — L0_Intent

## Access
- Read: YES
- Write: NO
- Propose: NO

## Rules
- Must read Mission.md and Constraints.md before any task
- Must never modify L0 files


## Mandatory Checks
- Verify `locked: true` in frontmatter before proceeding
- Reference L0 constraints in any architecture decision

## Escalation
- Any attempt to change L0 → STOP and alert human
- Missing L0 files → STOP and alert human
