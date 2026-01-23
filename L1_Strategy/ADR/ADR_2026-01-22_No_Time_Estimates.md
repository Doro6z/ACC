# ADR — Prohibition des Estimations Temporelles dans Plans

**Date**: 2026-01-22  
**Status**: Accepted  
**Décision par**: Humain  
**Contexte**: Proto Ready Pack planning

---

## Context

DEV.Planner générait des estimations temporelles (heures, jours, semaines) dans les plans L3, malgré règles existantes préférant "effort levels".

**Problème identifié** :
- Plan Footstep estimé "42-56h (2-4 semaines)"
- Réalité : 1 journée (développeur expérimenté)
- Écart : 400-800% surestimation

**Cause racine** :
- Agent ne connaît pas la vélocité personnelle du développeur
- Estimations heuristiques basées sur "développeur moyen" fictif
- Crée fausses attentes et perte de confiance

---

## Decision

**INTERDICTION ABSOLUE** des estimations temporelles dans tous plans (L3) et reports (L4).

**Allowed** : Effort levels uniquement
- Low
- Medium
- High
- Low-Medium / Medium-High (granularité si nécessaire)

**Forbidden** :
- Heures (h)
- Jours (d)
- Semaines (w)
- Mois (m)
- Toute unité de temps

---

## Consequences

### Positives
- ✅ Honnêteté : Agent reconnaît ne pas connaître vélocité
- ✅ Flexibilité : Développeur calibre selon sa vitesse
- ✅ Confiance : Pas de fausses promesses temporelles
- ✅ Universalité : Effort levels valables pour tous développeurs

### Negatives
- ⚠️ Moins "concret" pour planification calendrier
- ⚠️ Humain doit calibrer manuellement (Low = X jours pour lui)

**Mitigation** :
- Humain peut créer tableau calibration personnel (Low = 1j, Medium = 2-3j, etc.)
- Stored in `L0_Intent/Dev_Velocity_Calibration.md` (optionnel)

---

## Implementation

### Files Modified
1. `Lω_Agentic/Rules/DEV.Planner_Rules.md`
   - Strengthened "Time Estimation Constraint" → "Effort Assessment Rules"
   - Explicitly forbidden temporal units
   - Examples of compliant/non-compliant output

2. `Templates/T_Plan_L3.md`
   - Removed "heuristic" warning
   - Removed "human calibration required" note
   - Simplified to effort levels only

### Enforcement
- DEV.Planner MUST follow rules (hard constraint)
- If Agent produces time estimate → Rule violation
- Human should report for rule improvement

---

## Alternatives Considered

### Alternative 1: Keep time estimates but add disclaimer
**Rejected** : Disclaimer ne résout pas problème, estimates restent faux

### Alternative 2: Ask human for velocity calibration
**Rejected** : Trop complexe, velocity varie par tâche/contexte

### Alternative 3: Use story points (1, 2, 3, 5, 8, 13)
**Rejected** : Trop proche de temps, effort levels plus clairs

---

## Status

✅ **Accepted and Implemented** (2026-01-22)

---

*ADR_2026-01-22_No_Time_Estimates_In_Plans*
