# Deferred Items — Améliorations Différées

**Purpose:** Track governance improvements and features deferred to later phases  
**Status:** Living document, updated as items are deferred or completed  
**Owner:** Human + ACC

---

## Phase 1.5 (Q2 2026)

### Rule 12 — Auto-Load Research Context
**Status:** ⏳ Deferred  
**Reason:** Phase d'observation en cours, déclenchement manuel préféré  
**Deferred on:** 2026-01-21  
**Target:** Phase 1.5 (when Intendant reports stable)

**What it does:**
- ACC automatically loads Intendant for strategic requests
- Detects keywords: Phase, Agent, Priority, Goal, Roadmap
- Scans L5_Knowledge/Research/ automatically

**Activation criteria:**
- [ ] ACC.Intendant produced 5+ coherent reports
- [ ] Rules stabilized (no changes for 2+ weeks)
- [ ] User trust in pattern established

**Implementation location:** `Lω_Agentic/Rules/ACC_Rules.md` (new Rule 12)

---

### Versioning (L2/L3 Documents)
**Status:** ⏳ Deferred  
**Reason:** Not critical immediately, focus on production first  
**Deferred on:** 2026-01-21  
**Target:** When first design/plan revisions needed

**What it does:**
- Headers vX.Y in L2/L3 documents
- Temporal traceability
- Rollback capability
- Naming: `Architecture_v1.0.md`, `Plan_v1.2_System.md`

**Activation criteria:**
- [ ] First L2 design requires major revision
- [ ] First L3 plan needs structural changes
- [ ] Confusion about "which version" occurs

**Implementation locations:**
- `Lω_Agentic/Rules/DEV.Architect_Rules.md` (Versioning Contract section)
- `Lω_Agentic/Rules/DEV.Planner_Rules.md` (Versioning Contract section)
- `Templates/T_Design_L2.md` (version header)
- `Templates/T_Plan_L3.md` (version header)

---

## Phase 2 (Q3-Q4 2026)

### ACC.Capacity Agent
**Status:** ⏳ Deferred  
**Reason:** Requires real data (time measured vs estimated)  
**Deferred on:** 2026-01-21  
**Target:** Phase 2 (after 3-5 systems completed)

**What it does:**
- Tracks real time via L4_Operations/Logs/
- Compares effort estimated vs actual
- Calculates personal velocity
- Alerts if L1 objectives incompatible with measured capacity

**Activation criteria:**
- [ ] 3+ systems completed with time tracking
- [ ] Patterns of velocity emerge
- [ ] G2/G3 deadlines approaching (need realistic assessment)

**Implementation:**
- Create `Lω_Agentic/Personas/ACC.Capacity.md`
- Create `Lω_Agentic/Rules/ACC.Capacity_Rules.md`
- Create `.agent/workflows/capacity.md`
- Create `L4_Operations/Capacity_Reports/` directory

**Permissions:**
- Read: L1, L3, L4, L5
- Write: L4_Operations/Capacity_Reports/ (private, human-only access)

---

## Unscheduled (Needs Trigger)

### Rule 14 — Emergency Protocol
**Status:** ⏳ Deferred  
**Reason:** Not urgent, current system functional  
**Deferred on:** 2026-01-21  
**Target:** When legitimate emergency occurs

**What it does:**
- Relaxed governance mode (temporary)
- Quick & Dirty accepted if debt documented
- Post-emergency audit mandatory
- ADR created for emergency decisions

**Activation criteria:**
- [ ] Production blocked by critical bug
- [ ] External deadline imposes time pressure
- [ ] L0 constraint becomes obsolete (e.g., hardware change)

**Implementation location:** `Lω_Agentic/Rules/ACC_Rules.md` (new Rule 14)

**Constraints:**
- Emergency ≠ default mode
- Max 1 emergency per month (if more → systemic issue)
- All exceptions audited by ACC.Intendant post-emergency

---

## Completed Items

*(None yet)*

---

## Review Schedule

- **Weekly:** Check if activation criteria met for Phase 1.5 items
- **Monthly:** Assess if Phase 2 items should be pulled forward
- **On-demand:** Review when new deferral needed

---

*Maintained by ACC*  
*Last updated: 2026-01-21*
