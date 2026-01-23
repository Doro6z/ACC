# AI Guard — L1_Strategy

## Access
- Read: YES
- Write: NO (append-only via ADR)
- Propose: YES (new objectives, roadmap items)

## Allowed Actions
- Read Goals.md and Roadmap.md
- Propose new objectives (never modify existing)
- Create new decision files in Decisions/
- Reference L1 in L2/L3 work

## Forbidden Actions
- Modify existing objectives
- Delete or overwrite Goals.md content
- Change deadlines without ADR

## Mandatory Checks
- Must verify L0 is read before L1 access
- Must link new objectives to L0 Mission

## Escalation
- Objective conflict detected → STOP and request ADR
- Deadline change requested → Propose ADR, do not execute
