# Guide — Obsidian Views & Filters

**Created**: 2026-01-22  
**For**: Proto Ready Pack & ACC System

---

## Résumé Rapide

Avec les **metadata frontmatter** et les **préfixes de fichiers**, tu peux créer des vues filtrées dans Obsidian.

### Options de Visualisation

1. **Graph View** (natif) — Filtre par chemin/nom
2. **Search** (natif) — Recherche avancée
3. **Dataview Plugin** (recommandé) — Queries SQL-like
4. **Canvas** (manuel) — Mind maps custom

---

## 1. Graph View — Filtrage Visuel

### Accès
`Ctrl+G` ou cliquer sur icône Graph

### Filtres Utiles

**Voir seulement Plans** :
```
path:L3_Execution/Plans/
```

**Voir seulemen Reports d'analyse** :
```
file:[Report]_
```

**Voir seulement RPA (activité)** :
```
file:[RPA]_
```

**Exclure les templates** :
```
-path:Templates/
```

**Combinaison** (Plans + Reports) :
```
path:L3_Execution/Plans/ OR file:[Report]_
```

### Configuration

1. Ouvrir Graph View
2. Cliquer sur Settings (⚙️)
3. **Filters** → Entrer requête
4. **Groups** → Créer groupes couleur :
   - Group 1: `file:[Plan]_` → Couleur bleue
   - Group 2: `file:[Report]_` → Couleur verte
   - Group 3: `file:[RPA]_` → Couleur orange

---

## 2. Search — Recherche Avancée

### Accès
`Ctrl+Shift+F` ou icône Search

### Requêtes Utiles

**Tous les reports d'analyse** :
```
file:[Report]_
```

**Reports sur Proto Ready Pack** :
```
file:[Report]_ ProtoReady
```

**Plans du projet ProtoReadyPack** :
```
path:ProtoReadyPack/
```

**Documents avec metadata type:analysis** :
```
[type: analysis]
```

**Rapports janvier 2026** :
```
file:[Report]_ file:2026-01
```

---

## 3. Dataview Plugin (Recommandé)

### Installation

1. Settings → Community Plugins
2. Browse → Chercher "Dataview"
3. Install + Enable

### Exemples de Queries

#### Liste Tous les Reports d'Analyse

Créer une note `Dashboard_Reports.md` :

````markdown
# Dashboard — Reports d'Analyse

```dataview
TABLE file.ctime as "Créé", type as "Type", category as "Catégorie"
FROM "L4_Operations/Reports"
WHERE contains(file.name, "[Report]_")
SORT file.ctime DESC
```
````

#### Liste Tous les Plans ProtoReadyPack

````markdown
# Dashboard — Plans Proto Ready Pack

```dataview
LIST
FROM "L3_Execution/Plans/ProtoReadyPack"
WHERE contains(file.name, "[Plan]_")
SORT file.name
```
````

#### Reports par Catégorie

````markdown
# Reports — Par Catégorie

```dataview
TABLE type, file.ctime as "Date"
FROM "L4_Operations/Reports"
WHERE type = "analysis"
SORT category, file.ctime DESC
```
````

#### Timeline Visuelle

````markdown
# Timeline — Proto Ready Pack

```dataview
CALENDAR file.ctime
FROM "L3_Execution/Plans/ProtoReadyPack" OR "L4_Operations/Reports"
WHERE contains(file.name, "ProtoReady")
```
````

---

## 4. Canvas — Mind Maps Manuelles

### Création

1. Nouveau fichier → Canvas
2. Glisser-déposer fichiers
3. Organiser visuellement

### Exemple Structure

```
Canvas: Proto_Ready_Pack_Overview.canvas

┌─────────────────────┐
│  Pack Vision        │
│  (L2_Design)        │
└──────┬──────────────┘
       │
    ┌──┴────┬─────┬─────┐
    │       │     │     │
  Phase1  Phase2  Reports
  Plans   Plans   Analysis
```

---

## 5. Frontmatter Metadata — Best Practices

### Structure Recommandée

#### Pour Reports

```yaml
---
type: analysis | activity
category: market | diagnostic | tracking | audit | vision
agent: ACC.Intendant
project: ProtoReadyPack | ApexPrimal | Other
status: draft | final
---
```

#### Pour Plans

```yaml
---
type: plan
project: ProtoReadyPack
phase: 0 | 1 | 2 | 3
status: proposed | approved | in-progress | completed
---
```

### Avantages

- ✅ Filtrage Dataview par metadata
- ✅ Recherche avancée `[category: market]`
- ✅ Tri automatique
- ✅ Statistiques (nombre reports par catégorie)

---

## 6. Workflows Rapides

### Vue Globale Projet

**Créer** : `Views/ProtoReadyPack_Dashboard.md`

````markdown
# Proto Ready Pack — Dashboard

## 📋 Plans Actifs

```dataview
TABLE status, phase
FROM "L3_Execution/Plans/ProtoReadyPack"
WHERE status != "completed"
SORT phase
```

## 📊 Reports Récents

```dataview
TABLE type, category
FROM "L4_Operations/Reports"
WHERE contains(file.name, "ProtoReady")
SORT file.ctime DESC
LIMIT 5
```

## ✅ Checkpoints

- [ ] Phase 0 — ACC Setup
- [ ] Phase 1 — Juridique
- [ ] Phase 2 — Architecture
- [ ] Phase 3 — Module 1
````

### Vue Timeline

**Graph View Filter** :
```
path:ProtoReadyPack/ OR (file:[Report]_ ProtoReady)
```

### Vue par Agent

**Dataview Query** :

````markdown
## Reports par Agent

```dataview
TABLE file.ctime as "Date", category
FROM "L4_Operations/Reports"
GROUP BY agent
SORT file.ctime DESC
```
````

---

## 7. Plugins Recommandés (Optionnels)

| Plugin         | Usage              | Priorité       |
| -------------- | ------------------ | -------------- |
| **Dataview**   | Queries dynamiques | ⭐⭐⭐ Essentiel  |
| **Kanban**     | Task boards        | ⭐⭐ Utile       |
| **Excalidraw** | Diagrammes         | ⭐⭐ Utile       |
| **QuickAdd**   | Templates rapides  | ⭐ Nice-to-have |

---

## 8. Exemple Complet — Dashboard Proto Ready Pack

Créer : `Views/Dashboard_ProtoReadyPack.md`

````markdown
---
type: dashboard
project: ProtoReadyPack
---

# 🎯 Proto Ready Pack — Dashboard Central

> Dernière mise à jour : [[2026-01-22]]

---

## 📅 Timeline

```dataview
CALENDAR file.ctime
FROM "L3_Execution/Plans/ProtoReadyPack" OR "L4_Operations/Reports"
WHERE contains(file.name, "ProtoReady") OR contains(file.path, "ProtoReadyPack")
```

---

## 📋 Plans en Cours

```dataview
TABLE phase, status, file.ctime as "Créé"
FROM "L3_Execution/Plans/ProtoReadyPack"
WHERE status = "in-progress" OR status = "proposed"
SORT phase
```

---

## 📊 Reports d'Analyse (Derniers 7 jours)

```dataview
TABLE category, file.ctime as "Date"
FROM "L4_Operations/Reports"
WHERE contains(file.name, "[Report]_") AND contains(file.name, "ProtoReady")
WHERE file.ctime >= date(today) - dur(7 days)
SORT file.ctime DESC
```

---

## 🔄 Activité Récente (RPA)

```dataview
LIST
FROM "L4_Operations/Reports"
WHERE contains(file.name, "[RPA]_")
SORT file.ctime DESC
LIMIT 3
```

---

## 📂 Structure Projet

- [[L2_Design/ProtoReadyPack/Pack_Vision|Pack Vision]]
- [[L2_Design/ProtoReadyPack/Shared_Standards|Shared Standards]]
- [[L3_Execution/Plans/ProtoReadyPack/[Plan]_Master_2026-01-22_1345|Master Plan]]

---

## ✅ Checkpoints G2 (Mai 2026)

- [x] Phase 0 — ACC Setup
- [ ] Phase 1 — Juridique & Business
- [ ] Phase 2 — Architecture Pack
- [ ] Phase 3 — Module 1 (Stride Wheel)
- [ ] Phase 4 — Publication Workflow
- [ ] Phase 5 — Modules 2-4
- [ ] Phase 6 — Bundle & Marketing

---

## 🔗 Liens Rapides

- [[L1_Strategy/Goals#G2|Objectif G2]]
- [[Lω_Agentic/Rules/Naming_Conventions|Naming Conventions]]
- [[L4_Operations/Reports/[Report]_Expanded_Pack_Strategy_2026-01-22_1325|Strategy Report]]

````

---

## Résumé Actions

1. ✅ **Installer Dataview** (Community Plugin)
2. ✅ **Créer Dashboard** (`Views/Dashboard_ProtoReadyPack.md`)
3. ✅ **Configurer Graph View** (filters + groups)
4. ✅ **Ajouter frontmatter** aux fichiers progressivement

---

*Guide créé pour faciliter navigation Obsidian avec nouvelles conventions ACC*
