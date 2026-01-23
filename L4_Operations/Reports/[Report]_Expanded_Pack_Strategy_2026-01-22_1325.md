# ACC.Intendant Report — 2026-01-22_1325

## Context
- **Trigger**: User feedback + external recommendations
- **Objective**: Synthesized market analysis with expanded scope
- **Scope**: Proto Ready Pack vision beyond Apex extraction

---

## Research Base

**Internal Sources**:
- [ProtoReadyPack_Brainstorm.md](file:///c:/Obsidian%20Vaults/UE%20Projects/L5_Knowledge/Research/ProtoReadyPack_Brainstorm.md) — Ideas capture
- [Report_2026-01-22_1250](file:///c:/Obsidian%20Vaults/UE%20Projects/L4_Operations/Reports/Report_2026-01-22_1250_Market_Strategic_Options.md) — Previous market options
- Apex Primal audit (SavedInformations.md)

**External Sources**:
- Fab Marketplace trends 2024-2025
- User-provided market recommendations

---

## Synthèse Marché Fab/UE5 (2024-2025)

| Catégorie                     | Demande      | Commentaires                                                  |
| ----------------------------- | ------------ | ------------------------------------------------------------- |
| **Systèmes Audio Dynamiques** | 🔥🔥🔥 Élevé    | Surfaces, spatialisation, ambiences — pain point récurrent    |
| **Kits UI**                   | 🔥🔥🔥 Élevé    | Menus, HUDs, inventaires — multi-résolution, data-driven      |
| **Gameplay Frameworks**       | 🔥🔥 Moyen     | Place pour modules "proto-ready" sans dépendances lourdes     |
| **World Tools**               | 🔥🔥🔥 Élevé    | Génération procédurale, blockout, paysages modulaires         |
| **Multiplayer Frameworks**    | 🔥🔥 Croissant | Lobby, replication, matchmaking — solutions faciles demandées |
| **AI/NPC Behaviour**          | 🔥🔥 En hausse | Comportements modulaires — marché sous-desservi               |

---

## Expanded Module Candidates

### Catégorie 1 — Audio (Forte Demande)

| Module                     | Source     | Effort | Différenciateur                 |
| -------------------------- | ---------- | ------ | ------------------------------- |
| **Stride Wheel Footsteps** | Innovation | Low    | Setup < 2 min, pas d'AnimNotify |
| **Ambience System**        | Apex       | Low    | MetaSound, zones, data-driven   |

---

### Catégorie 2 — UI/UX (Forte Demande)

| Module               | Source  | Effort      | Différenciateur                  |
| -------------------- | ------- | ----------- | -------------------------------- |
| **Menu Data-Driven** | Nouveau | Medium      | Blueprint cascade, thèmes custom |
| **UI Réactive**      | Nouveau | Medium-High | Auto-génération, responsive      |
| **Settings Manager** | Nouveau | Low         | DataAsset-based, persistence     |

---

### Catégorie 3 — World Building (Forte Demande)

| Module                         | Source  | Effort     | Différenciateur           |
| ------------------------------ | ------- | ---------- | ------------------------- |
| **Titan Root Procedural**      | Apex    | Low-Medium | Spline + ISMC, branches   |
| **Procedural Level Generator** | Nouveau | Very High  | Donjons, grilles, navmesh |

---

### Catégorie 4 — Gameplay Frameworks (Demande Moyenne)

| Module                 | Source  | Effort | Différenciateur               |
| ---------------------- | ------- | ------ | ----------------------------- |
| **Survival Stats**     | Apex    | Medium | GAS-free version, replication |
| **Progression System** | Apex    | Medium | Levels, perks, data-driven    |
| **Save System**        | Nouveau | Medium | Async, compression, slots     |

---

### Catégorie 5 — Multiplayer (Demande Croissante)

| Module                       | Source  | Effort | Différenciateur                 |
| ---------------------------- | ------- | ------ | ------------------------------- |
| **Multiplayer Kit**          | Nouveau | High   | Lobby, matchmaking, CTF example |
| **Lag Compensation Toolkit** | Nouveau | High   | Client prediction, debug tools  |

---

### Catégorie 6 — AI/NPC (Demande Croissante)

| Module                   | Source  | Effort | Différenciateur                      |
| ------------------------ | ------- | ------ | ------------------------------------ |
| **Modular AI Framework** | Nouveau | High   | GOAP simple, perception, replication |

---

### Catégorie 7 — Environment/Immersion

| Module                  | Source  | Effort      | Différenciateur                   |
| ----------------------- | ------- | ----------- | --------------------------------- |
| **Weather + Day/Night** | Nouveau | Medium-High | Profils météo, cycle paramétrable |
| **Camera Framework**    | Apex    | Medium      | Profils multiples, transitions    |

---

### Catégorie 8 — Dev Tools

| Module                  | Source | Effort     | Différenciateur             |
| ----------------------- | ------ | ---------- | --------------------------- |
| **Telemetry/Analytics** | Apex   | Low-Medium | In-editor dashboard, export |

---

## Matrice Effort vs Impact

```
                    IMPACT
                Low    Medium    High
           ┌─────────┬─────────┬─────────┐
    Low    │ Telemetry│ Settings│ Stride  │
           │         │ Manager │ Wheel   │
           │         │ Titan   │ Ambience│
           ├─────────┼─────────┼─────────┤
  EFFORT   │         │ Menu    │ Survival│
   Medium  │         │ Camera  │ Progress│
           │         │ Save    │ UI React│
           ├─────────┼─────────┼─────────┤
    High   │         │ Weather │ Multi-  │
           │         │ AI Fwk  │ player  │
           │         │         │ Kit     │
           └─────────┴─────────┴─────────┘
```

**Sweet Spot (Low Effort + High Impact)**:
1. ⭐ Stride Wheel Footsteps
2. ⭐ Ambience System
3. ⭐ Titan Root Procedural

**High Value (Medium Effort + High Impact)**:
4. Menu Data-Driven
5. Survival/Progression
6. UI Réactive

---

## Stratégie Recommandée

### Phase 1 — Quick Wins (G2: Mai 2026)

**Objectif**: 3-4 modules à faible effort, fort impact

| Module                 | Effort     | Semaines | ROI |
| ---------------------- | ---------- | -------- | --- |
| Stride Wheel Footsteps | Low        | 2        | 🔥🔥🔥 |
| Ambience System        | Low        | 2        | 🔥🔥🔥 |
| Settings Manager       | Low        | 1        | 🔥🔥  |
| Titan Root Procedural  | Low-Medium | 2-3      | 🔥🔥🔥 |

**Total**: 7-8 semaines  
**Revenus potentiels**: 4 modules × 5€ = 20€ unitaire, pack intro 15€

---

### Phase 2 — Core Pack (Q3 2026)

**Objectif**: Compléter le pack avec modules gameplay

| Module             | Effort | Semaines |
| ------------------ | ------ | -------- |
| Menu Data-Driven   | Medium | 3        |
| Survival Stats     | Medium | 2-3      |
| Progression System | Medium | 2        |
| Save System        | Medium | 2        |

**Total**: 9-10 semaines  
**Pack complet**: 8 modules → 40€ (vs 40€ unitaire)

---

### Phase 3 — Premium Expansion (Q4 2026+)

**Objectif**: Modules high-effort, high-value

| Module              | Effort      | Semaines |
| ------------------- | ----------- | -------- |
| UI Réactive         | Medium-High | 4        |
| Weather + Day/Night | Medium-High | 3        |
| Camera Framework    | Medium      | 2        |
| Multiplayer Kit     | High        | 6-8      |
| AI Framework        | High        | 6-8      |

---

## Architecture Pack

```
Proto Ready Pack/
├── Core Modules (5€ each)
│   ├── Audio/
│   │   ├── StrideWheel_Footsteps
│   │   └── Ambience_System
│   ├── World/
│   │   └── TitanRoot_Procedural
│   ├── UI/
│   │   ├── Menu_DataDriven
│   │   ├── Settings_Manager
│   │   └── UI_Reactive
│   └── Gameplay/
│       ├── Survival_Stats
│       ├── Progression_System
│       └── Save_System
│
├── Premium Modules (10€ each)
│   ├── Environment/
│   │   ├── Weather_DayNight
│   │   └── Camera_Framework
│   ├── Multiplayer/
│   │   └── Multiplayer_Kit
│   └── AI/
│       └── AI_ModularFramework
│
└── Bundles
    ├── Starter Pack (4 Core) — 15€
    ├── Full Core Pack (9 Core) — 35€
    └── Complete Pack (All) — 60€
```

---

## Principes Standards (Tous Modules)

### Philosophy "Proto Ready"
1. **Setup < 10 min** maximum
2. **Data-Driven** (DataAssets, pas hard-code)
3. **Blueprint-First** API
4. **Standalone** (chaque module fonctionne seul)
5. **Documentation** incluse (README + demo)

### Structure Technique Commune
```
Module_Name/
├── Source/ (C++ si applicable)
├── Content/
│   ├── Demo/
│   │   └── DM_Module_Showcase.umap
│   ├── Data/
│   │   └── DA_Example.uasset
│   └── Blueprints/ (si BP-only)
├── Documentation/
│   └── README.md
└── Module_Name.uplugin
```

### Naming Conventions
- Prefix: `PR_` (Proto Ready)
- Classes: `UPR<Module>Component`, `APR<Module>Actor`
- DataAssets: `DA_<Module>_<Purpose>`

---

## Decision Required

### Validation du Plan

1. **Phase 1 approuvée ?**
   - Stride Wheel
   - Ambience
   - Settings Manager
   - Titan Root

2. **Titan Root** — Confirmer extraction ou déprioritiser ?

3. **Business model validé ?**
   - Core modules: 5€
   - Premium modules: 10€
   - Bundles: 15€ / 35€ / 60€

4. **Nouvelles créations** (Menu, Save, Weather) vs extractions pures ?

---

## Prochaine Étape

Si Phase 1 validée:
1. **DEV.Architect** → Pack_Vision.md + Shared_Standards.md
2. **DEV.Architect** → Module 1: Stride Wheel Architecture
3. **DEV.Planner** → Plan Phase 1 implémentation

---

*Report generated by ACC.Intendant*  
*Integrates user recommendations + market research*  
*Human validation required*
