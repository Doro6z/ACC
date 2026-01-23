# Plan — Phase 2: Architecture & Standards

**File:** `[Plan]_Phase2_Implementation_2026-01-22_1450.md`  
**Created:** 2026-01-22 14:50  
**L1 Goal:** [G2 — Premiers actifs (Mai 2026)](file:///c:/Obsidian%20Vaults/UE%20Projects/L1_Strategy/Goals.md#L37)  
**Status:** Proposed

---

## Context

### Trigger
- Phase 2 architecture validated ([Arch]_Phase2_PackArchitecture)
- Human approval: décisions naming, C++/BP ratio, pricing
- Master Plan Task 2.1-2.3 ready for detailed breakdown

### Scope
**Inclus**:
- Task 2.1: Pack_Vision.md creation
- Task 2.2: Shared_Standards.md creation
- Task 2.3: UE5 plugin template creation
- All foundational docs before Module 1 development

**Exclus**:
- Module-specific architectures (Phase 3+)
- Legal/business setup (Phase 1)
- UE project setup (done separately)

### Success Criteria
- [ ] Pack_Vision.md created and validated
- [ ] Shared_Standards.md created and validated
- [ ] UE5 plugin template functional
- [ ] Checkpoint 2 passed (standards frozen before dev)

---

## Research Base

Documents consultés :
- **[Arch]_Phase2_PackArchitecture_2026-01-22** — Architecture validated, standards defined
- **[Report]_Expanded_Pack_Strategy_2026-01-22_1325** — Market strategy, modules list
- **[Plan]_Master_2026-01-22_1345** — Phase 2 tasks overview
- **L0/Mission** — Architecture First principle

**Decisions validées** :
- `PR_` namespace ✅
- C++ backend maximal, BP API maximal ✅
- Simple showcase demos ✅
- Semantic versioning ✅
- Pricing ~5€/module (référence) ✅

---

## Task Breakdown

### Task 2.1 — Créer Pack_Vision.md

**Objectif** : Formaliser philosophie "Proto Ready" et roadmap modules

- [ ] **Subtask 2.1.1** — Écrire section Philosophy
  - Effort: Low
  - Owner: Humain (avec template Architect)
  - Détails:
    - Principle 1: Setup < 10 min
    - Principle 2: Data-Driven (DataAssets)
    - Principle 3: Blueprint-First API
    - Principle 4: Standalone modules
    - Principle 5: Proto-ready (functional fast)
  - Dependencies: None

- [ ] **Subtask 2.1.2** — Lister modules Phase 1-3
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Phase 1 (G2): Stride Wheel, Ambience, Settings, Titan Root
    - Phase 2 (Q3): Menu, Survival, Progression, Save
    - Phase 3 (Q4+): UI Reactive, Weather, Multiplayer, AI
  - Dependencies: None (parallèle 2.1.1)

- [ ] **Subtask 2.1.3** — Définir pricing & bundles
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Core modules: ~5€ (référence)
    - Premium modules: ~10€ (référence)
    - Bundles: Starter, Full Core, Complete
    - Note: Prix indicatifs, ajustables
  - Dependencies: None (parallèle)

- [ ] **Subtask 2.1.4** — Identifier USPs vs concurrence
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Speed (10 min setup)
    - Affordability
    - Consistency across pack
    - Innovations (Stride Wheel, etc.)
  - Dependencies: Subtask 2.1.1-2.1.3

- [ ] **Subtask 2.1.5** — Finaliser & valider Pack_Vision.md
  - Effort: Low
  - Owner: Humain
  - Output: `L2_Design/ProtoReadyPack/Pack_Vision.md`
  - Dependencies: Subtask 2.1.4

---

### Task 2.2 — Créer Shared_Standards.md

**Objectif** : Définir standards techniques communs (CRITIQUES avant dev)

- [ ] **Subtask 2.2.1** — Écrire Naming Conventions
  - Effort: Low
  - Owner: Humain (copier depuis Architect)
  - Détails:
    - Classes C++: `UPR<Module>Component`, `APR<Module>Actor`
    - Assets: `DA_<Module>_<Purpose>`, `BP_<Module>_<Type>`
    - Enums: `EPR<Module><Purpose>`
    - Structs: `FPR<Module><Purpose>`
  - Dependencies: None

- [ ] **Subtask 2.2.2** — Définir DataAsset Pattern
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - All inherit `UPrimaryDataAsset`
    - Implement `GetPrimaryAssetId()`
    - Example class structure
  - Dependencies: Subtask 2.2.1

- [ ] **Subtask 2.2.3** — Définir Blueprint API Standards
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Public properties: `EditAnywhere, BlueprintReadWrite`
    - Public functions: `BlueprintCallable`
    - Events: `BlueprintAssignable`
    - Example component API
  - Dependencies: Subtask 2.2.1

- [ ] **Subtask 2.2.4** — Créer Documentation Template
  - Effort: Low
  - Owner: Humain
  - Détails:
    - README.md structure:
      - Quick Start (< 5 min)
      - Setup (< 10 min)
      - API Reference
      - Troubleshooting
      - Example Project
  - Output: Template markdown
  - Dependencies: None (parallèle)

- [ ] **Subtask 2.2.5** — Définir Demo Map Requirements
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Naming: `DM_<Module>_Showcase.umap`
    - Contents: Lighting, camera, demonstration
    - Performance: 60 FPS target
    - Clarity: Instructions visible
  - Dependencies: None (parallèle)

- [ ] **Subtask 2.2.6** — Définir Code Quality Standards
  - Effort: Low
  - Owner: Humain
  - Détails:
    - C++: Unreal conventions, no warnings, comments
    - BP: Organized nodes, comment boxes, named vars
  - Dependencies: None (parallèle)

- [ ] **Subtask 2.2.7** — Finaliser & valider Shared_Standards.md
  - Effort: Low
  - Owner: Humain
  - Output: `L2_Design/ProtoReadyPack/Shared_Standards.md`
  - Dependencies: Subtask 2.2.1-2.2.6

---

### Task 2.3 — Créer UE5 Plugin Template

**Objectif** : Template réutilisable pour accélérer création modules

- [ ] **Subtask 2.3.1** — Créer plugin vide UE5.5
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Location: `Templates/PR_Module_Template/`
    - Create via UE5 Editor: Tools → New Plugin
    - Type: Blank
  - Dependencies: None

- [ ] **Subtask 2.3.2** — Configurer .uplugin file
  - Effort: Low
  - Owner: Humain
  - Détails:
    - FriendlyName: "[Module Name]"
    - Category: "Proto Ready"
    - CanContainContent: true
    - Module type: Runtime
  - Dependencies: Subtask 2.3.1

- [ ] **Subtask 2.3.3** — Créer example Component
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - `Public/Components/PR_ExampleComponent.h`
    - `Private/Components/PR_ExampleComponent.cpp`
    - Includes: Property, Function, Event examples
  - Dependencies: Subtask 2.3.2

- [ ] **Subtask 2.3.4** — Créer example DataAsset
  - Effort: Low
  - Owner: Humain
  - Détails:
    - `Public/Data/PR_ExampleData.h`
    - `Private/Data/PR_ExampleData.cpp`
    - Inherits `UPrimaryDataAsset`
  - Dependencies: Subtask 2.3.2

- [ ] **Subtask 2.3.5** — Créer folder structure
  - Effort: Low
  - Owner: Humain
  - Détails:
    - `Content/Demo/` (for DM map)
    - `Content/Data/` (for DataAssets)
    - `Documentation/` (for README)
  - Dependencies: Subtask 2.3.1

- [ ] **Subtask 2.3.6** — Tester compilation template
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Compile plugin in UE5.5
    - Verify 0 errors, 0 warnings
    - Test in clean project
  - Dependencies: Subtask 2.3.3, 2.3.4

- [ ] **Subtask 2.3.7** — Documenter how-to-use
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Create `Templates/PR_Module_Template/HOW_TO_USE.md`
    - Steps: Copy, rename, customize
  - Output: Usage guide
  - Dependencies: Subtask 2.3.6

---

## Dependencies

### Critical Path
```
Task 2.1 (Pack Vision) ← Parallèle avec 2.2
   ↓
Task 2.2 (Shared Standards) ← CRITIQ UE pour 2.3
   ↓
Task 2.3 (Template) ← Doit respecter standards
   ↓
Checkpoint 2 Validation
```

### Blockers
- **Task 2.2 DOIT** être validé avant Task 2.3 finalization (standards appliqués au template)
- **Checkpoint 2 BLOQUE** Phase 3 (standards frozen)

---

## Validation Checkpoints

- [ ] **Checkpoint 2.1** — Pack Vision validé
  - Criteria: Philosophie claire, modules listés, pricing défini

- [ ] **Checkpoint 2.2** — Shared Standards validés
  - Criteria: Naming complet, BP API défini, docs template prêt

- [ ] **Checkpoint 2.3** — Template fonctionnel
  - Criteria: Compile UE5.5, 0 errors, structure correcte

- [ ] **Checkpoint 2 Final** — Phase 2 complète
  - Criteria: Tous docs créés, standards figés, prêt pour Phase 3

---

## Effort Assessment (Heuristic)

⚠️ Estimations génériques, non calibrées à la vélocité personnelle.

**Par Task** :
- **Task 2.1** (Pack Vision): **Low** (2-3h)
- **Task 2.2** (Shared Standards): **Low-Medium** (4-6h)
- **Task 2.3** (UE5 Template): **Low** (2-3h)

**Total Phase 2**: ~8-12h travail  
**Timeline suggérée**: 2-3 jours (avec validation humaine)

**Human calibration required** pour conversion temps exact.

---

## Risks & Mitigation

| Risk                           | Impact | Probability | Mitigation                            |
| ------------------------------ | ------ | ----------- | ------------------------------------- |
| **Standards incomplets**       | High   | Medium      | Review checklist obligatoire          |
| **Template trop complexe**     | Medium | Low         | Minimal viable, itérer après Module 1 |
| **Naming conflicts futurs**    | Medium | Low         | `PR_` prefix évite collisions UE      |
| **Standards changent Phase 3** | High   | Low         | Freeze après validation Checkpoint 2  |
| **Template non-fonctionnel**   | Medium | Low         | Test obligatoire avant validation     |

---

## Notes

### Assumptions
- Humain a UE5.5 installé
- Temps disponible: 15-20h/semaine Proto Ready Pack
- Validation humaine rapide (< 1 jour par checkpoint)

### Ordre Recommandé
1. **Jour 1 matin** : Task 2.1 (Pack Vision) + Task 2.2.1-2.2.3 (Naming/DataAsset/BP API)
2. **Jour 1 après-midi** : Task 2.2.4-2.2.7 (Docs/Demo standards complets)
3. **Jour 2 matin** : Validation Checkpoint 2.2 (humain)
4. **Jour 2 après-midi** : Task 2.3.1-2.3.6 (Template création + test)
5. **Jour 3 matin** : Task 2.3.7 + Checkpoint 2.3
6. **Jour 3 après-midi** : Checkpoint 2 Final validation

---

## Prochaines Actions Immédiates

1. ✅ **Phase 2 architecture validée** (DEV.Architect done)
2. 📝 **Humain** : Commencer Task 2.1.1 (Philosophy section)
3. 📝 **Humain** : Parallèle Task 2.2.1 (Naming conventions)
4. ⏳ **Attendre** : Validation Checkpoint 2.2 avant Task 2.3

---

## Post Phase 2

**Phase 3 trigger** : Checkpoint 2 Final validé  
**Next step** : DEV.Architect conçoit Module 1 (Stride Wheel) architecture

---

*Plan generated by DEV.Planner*  
*Based on [Arch]_Phase2_PackArchitecture_2026-01-22*  
*Human validation required before execution.*
