---
type: guidance
scope: L1
---

# Guide L1_Strategy

> L1 = Contrat d'intention stratégique vérifiable.

---

## Qu'est-ce que L1 ?

L1 n'est **pas** un backlog. L1 n'est **pas** un plan d'exécution.

L1 définit **où vous allez** et **dans quel ordre de priorité**.

---

## Goals.md — Règles

**Ce qu'il faut** :
- Repères temporels (deadlines)
- Ordres de grandeur (métriques)
- Conditions de succès vérifiables

**Ce qu'il ne faut pas** :
- KPI ultra-précis
- Moyens techniques détaillés (→ L2)
- Audits ou analyses (→ L5)

**Test agentique** : Un agent doit pouvoir répondre :
> "Cet objectif est-il atteint ? Oui / Non / Indéterminé"

---

## Roadmap.md — Règles

- Dérive **explicitement** des Goals
- Phases alignées sur les jalons G1→G5
- Pas de dates précises non validées
- Pas de détails d'exécution (→ L4)

---

## Decisions/ — Quand créer un ADR ?

- Changement d'objectif
- Changement de deadline majeur
- Pivot stratégique

Format : `DEC-YYYY-NNN.md`

---

## Append-only

L1 ne se modifie pas, il s'enrichit.

| Action            | Méthode                       |
| ----------------- | ----------------------------- |
| Ajouter objectif  | Nouvelle section              |
| Modifier objectif | Marquer obsolète + nouveau    |
| Supprimer         | ❌ Interdit (marquer obsolète) |

---

## Tags et Graph View

**Convention de tags** :
- `#layer/L1` : Tous les documents L1
- `#goal` : Goals.md
- `#roadmap` : Roadmap.md
- `#decision` : Fichiers ADR

**Stratégie de liens** :
- Roadmap → Goals (sections précises avec ancres `^g1`, `^g2`...)
- Goals → Mission (L0)
- Decisions → Goals + contexte

**Masquer _Index dans Graph** :
- Settings → Graph → Files → Exclude: `_Index`

---

*L1 v0 = bootstrap volontairement imparfait, mais suffisant pour analyse future.*
