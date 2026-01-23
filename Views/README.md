# Views — Visual Navigation & Dashboards

**Purpose:** Visual navigation layer for the vault - dashboards, maps, and boards to understand system state at a glance.

**Philosophy:** Views/ ne contient pas de "contenu métier", seulement des **vues** sur le contenu existant dans L0-L6.

---

## Structure (Progressive)

```
Views/
  ├── README.md                      (ce fichier)
  ├── Home_Dashboard.md              (Phase 2 - overview général)
  ├── Strategy_Dashboard.md          (Phase 2 - L1 goals + roadmap)
  ├── Operations_Board.md            (Phase 2 - L4 tasks kanban)
  ├── Projects_Map.canvas            (Phase 3 - Apex + futurs)
  ├── Assets_Map.canvas              (Phase 3 - portfolio G4)
  └── ApexPrimal_SystemMap.canvas    (Phase 3 - systems extraction)
```

**Phase 1 (actuelle):** Structure vide, conventions définies  
**Phase 2:** Dashboards Dataview  
**Phase 3:** Canvas maps  
**Phase 4 (optionnel):** Agent ACC.Visualizer

---

## Frontmatter Conventions (Mandatory)

Toute note "réelle" (pas template/guard/_Index/_Guidance) DOIT inclure :

```yaml
---
layer: L0 | L1 | L2 | L3 | L4 | L5 | L6 | Lω
domain: asset | game | ops | admin
project: apex_primal | <asset_name> | system
goal: G1 | G2 | G3 | G4 | G5
status: active | proposed | completed | archived
---
```

### Fields Explained

**layer:** Couche architecturale (L0-L6, Lω)
- L0: Intent (Mission, Constraints)
- L1: Strategy (Goals, Roadmap, ADR)
- L2: Design (Architecture, ADR techniques)
- L3: Execution (Plans, Code - dans projet UE)
- L4: Operations (Tasks, Reports, Logs)
- L5: Knowledge (Research, PostMortems, Technical)
- L6: Validation (Tests, QA - dans projet UE)
- Lω: Agentic (Personas, Rules, Governance)

**domain:** Domaine métier
- `asset`: Assets UE5 commerciaux (Fab, Marketplace)
- `game`: Apex Primal ou autres jeux
- `ops`: Opérationnel (rapports, suivi, admin)
- `admin`: Méta-système (templates, guards, guides)

**project:** Projet parent
- `apex_primal`: Projet Apex Primal
- `<asset_name>`: Nom asset spécifique (ex: `audio_system`)
- `system`: Système transversal (ACC, workflows)

**goal:** Objectif L1 lié
- G1: Professionnalisation
- G2: Premiers revenus (Mai 2026)
- G3: Revenus stables (Fin 2026)
- G4: Portfolio technique
- G5: Projet fondateur Apex

**status:** État actuel
- `active`: En cours
- `proposed`: Proposé, pas validé
- `completed`: Terminé
- `archived`: Archivé, référence historique

---

## Graph View Configuration

**Objectif:** Masquer bruit structurel, montrer contenu métier

### Filters Recommandés

**Dans `.obsidian/graph.json` :**
```json
{
  "hideUnresolved": true,
  "search": "-kind:meta -kind:template",
  "groups": [
    {
      "query": "layer:L0",
      "color": {"a":1,"rgb":16711680}
    },
    {
      "query": "layer:L1",
      "color": {"a":1,"rgb":16744192}
    },
    {
      "query": "layer:L2",
      "color": {"a":1,"rgb":65280}
    },
    {
      "query": "layer:L4",
      "color": {"a":1,"rgb":255}
    },
    {
      "query": "layer:L5",
      "color": {"a":1,"rgb":16711935}
    },
    {
      "query": "layer:Lω",
      "color": {"a":1,"rgb":8421504}
    }
  ]
}
```

**Masquer structurels :** Ajouter `kind: meta` aux:
- `_Index.md`
- `_Guidance.md`
- `AI_Guard.md`
- Templates (déjà dans `/Templates/`)

---

## Usage Patterns

### 1. Navigation Macro
**Outil:** Graph view + Home Dashboard  
**Quand:** Comprendre où je suis, quel layer actif  
**Filtres:** Par layer, par goal, par project

### 2. Suivi Exécution
**Outil:** Operations Board (Dataview kanban)  
**Quand:** Voir tâches actives, blocages  
**Vue:** Tasks par goal, par status

### 3. Design Visuel
**Outil:** Canvas maps  
**Quand:** Conception système, extraction asset  
**Vue:** Modules, dépendances, API

### 4. Flows/State Machines
**Outil:** Mermaid diagrams (in-document)  
**Quand:** Specs techniques, workflows  
**Vue:** Flowcharts, sequences, states

---

## Plugins Requis

**Essentiels (Phase 2):**
- Dataview — Dashboards dynamiques
- Canvas — Natif Obsidian

**Optionnels (Phase 3):**
- Excalidraw — Diagrammes sur-mesure
- Kanban — Boards visuels alternatifs

**Vérifier installation** avant Phase 2.

---

## Contribution Rules

**Views/ est géré par:**
- Human (création manuelle dashboards/maps)
- Future ACC.Visualizer (Phase 4, génération automatique)

**Agents actuels DOIVENT:**
- Ne PAS modifier Views/ (lecture seule)
- Respecter frontmatter conventions dans leurs outputs
- Suggérer création dashboard si pertinent, mais humain décide

**Exception:** ACC.Intendant peut suggérer vues dans rapports, mais n'exécute pas.

---

## Next Steps (Progressive)

- [x] **Phase 1:** Structure + conventions (ce fichier)
- [ ] **Phase 2:** Créer 3 dashboards Dataview (Home, Strategy, Operations)
- [ ] **Phase 3:** Créer Canvas maps (Projects, Assets, Systems)
- [ ] **Phase 4:** Optionnel - Créer ACC.Visualizer agent

**Timeline:**
- Phase 2: Fin Phase 0 / Début Phase 1
- Phase 3: Pendant Phase 1 (production assets)
- Phase 4: Phase 1.5+ (quand patterns stabilisés)

---

*Views structure created: 2026-01-21*  
*Last updated: 2026-01-21*
