# L2 Design — Proto Ready Pack: Architecture Phase 2

**Created**: 2026-01-22  
**Status**: DRAFT  
**Phase**: Phase 2 — Architecture & Standards  
**L1 Goal**: [G2 — Premiers actifs (Mai 2026)](file:///c:/Obsidian%20Vaults/UE%20Projects/L1_Strategy/Goals.md#L37)

---

## Executive Summary

**Objectif Phase 2** : Établir les fondations architecturales du Proto Ready Pack **avant** tout développement de module.

**Livrables** :
1. **Pack_Vision.md** — Philosophie, objectifs, pricing, modules roadmap
2. **Shared_Standards.md** — Standards techniques communs (naming, DataAssets, BP API, docs)
3. **Templates UE5** — Plugin template réutilisable

**Durée estimée** : 1 semaine  
**Criticité** : ⚠️ **BLOQUANT** pour Phase 3+ — Les standards doivent être figés avant dev modules

---

## Context

### Master Plan Phase 2 Requirements

**Tasks identifiées** :
- Task 2.1 — Finaliser Pack Vision  
- Task 2.2 — Définir Shared Standards  
- Task 2.3 — Créer templates projet UE5

### Principes L0/L1

**From Mission.md** :
- **Architecture First** — Formaliser avant exécuter
- **Cohérence systémique** — Standards cohérents sur tous modules  
- **Traçabilité** — Décisions documentées

**From Goals.md** :
- **G2 (Mai 2026)** : 2+ assets publiés  
- **Timeline** : 4 mois disponibles → minimiser dette technique dès Phase 2

---

## Pack Vision — Design Approach

### 1.1 Objectif

Créer document **Pack_Vision.md** définissant :
- Vision "Proto Ready" (setup < 10 min, data-driven, standalone)
- Liste modules Phase 1-3 (roadmap)
- Business model (pricing: 5€/10€/bundles)
- Positionnement marché vs concurrence

### 1.2 Structure Proposée

```markdown
# Proto Ready Pack — Vision

> "From zero to prototype-ready in 10 minutes per module"

## Philosophy
- **Easy Setup**: < 10 min integration
- **Data-Driven**: DataAssets not hard-code
- **Blueprint-First**: Full BP API, C++ backbone
- **Standalone**: Modules work independently
- **Proto-Ready**: Functional fast, not production-polished

## Modules Roadmap

### Phase 1 (G2: Mai 2026)
1. Stride Wheel Footsteps
2. Ambience System
3. Settings Manager
4. Titan Root Procedural

### Phase 2 (Q3 2026)
5. Menu Data-Driven
6. Survival Stats
7. Progression System
8. Save System

### Phase 3 (Q4 2026+)
... (expansion modules)

## Business Model
- Core modules: 5€ each
- Premium modules: 10€ each
- Bundles: Starter (15€), Full Core (35€), Complete (60€)

## Target Audience
- Indie developers (prototyping)
- Game jam participants
- Studios (rapid scaffolding)

## Unique Selling Points
1. Speed (10 min vs hours)
2. Affordability (5€/module)
3. Consistency (same UX/naming across pack)
4. Innovation (e.g., Stride Wheel)
```

### 1.3 Decisions Required

**Questions Pack Vision** :
1. Modules Phase 1 figés ou flexible ?  
   → **Recommandation** : Figés (Stride Wheel, Ambience, Settings, Titan Root)

2. Pricing définitif ou test marché ?  
   → **Recommandation** : Définitif pour cohérence, ajustable après 3 mois

3. Include roadmap Phase 3 ou TBD ?  
   → **Recommandation** : Liste modules Phase 3 mais "tentative" (évolution possible)

---

## Shared Standards — Design Approach

### 2.1 Objectif

Créer document **Shared_Standards.md** définissant :
- Naming conventions (classes, assets, enums)
- DataAsset patterns communs
- Blueprint API standards
- Documentation structure (README template)
- Demo map requirements

### 2.2 Naming Conventions

#### Classes C++

**Prefix `PR_` (Proto Ready)** :
- Components: `UPRStrideWheelComponent`, `UPRAmbienceComponent`
- Actors: `APRTitanRoot`, `APRAmbientZone`
- DataAssets: `UPR<Module>Data` (e.g., `UPRStrideWheelData`)
- Subsystems: `UPR<Module>Subsystem`

**Enums** : `EPR<Module><Purpose>` (e.g., `EPRFootstepSurface`)

**Structs** : `FPR<Module><Purpose>` (e.g., `FPRStrideWheelConfig`)

#### Assets Unreal

**DataAssets** : `DA_<ModuleName>_<Purpose>`
- Example: `DA_StrideWheel_Default`, `DA_Ambience_JungleDay`

**Blueprints** : `BP_<ModuleName>_<Type>`
- Example: `BP_StrideWheel_Component`, `BP_TitanRoot_Actor`

**Maps** : `DM_<ModuleName>_Showcase`
- Example: `DM_StrideWheel_Showcase`

**Materials** : `M_<ModuleName>_<Purpose>`

**Sounds** : `SFX_<ModuleName>_<Type>`

---

### 2.3 DataAsset Patter

ns Communs

**All DataAssets derive from UPrimaryDataAsset** :
```cpp
UCLASS(BlueprintType)
class PROTOREADYPACK_API UPR<Module>Data : public UPrimaryDataAsset
{
    GENERATED_BODY()
    
public:
    // Asset ID for fast lookups
    virtual FPrimaryAssetId GetPrimaryAssetId() const override;
    
    // ... module-specific config
};
```

**Benefits** :
- Async loading support
- Asset Manager integration
- Memory optimization

---

### 2.4 Blueprint API Standards

**Tous UPR Components exposent** :

1. **Public Properties** (EditAnywhere, BlueprintReadWrite)
   - Configuration properties
   - DataAsset references

2. **Public Functions** (BlueprintCallable)
   - Main API calls
   - Status queries (`IsReady()`, `GetCurrentState()`)

3. **Events** (BlueprintAssignable)
   - State changes (`OnComponentInitialized`)
   - Important events (`OnFootstepPlayed`)

**Example** :
```cpp
UCLASS(ClassGroup = (ProtoReady), meta = (BlueprintSpawnableComponent))
class UPRStrideWheelComponent : public UActorComponent
{
    GENERATED_BODY()

public:
    // Config
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel")
    UPRStrideWheelData* StrideData;

    // API
    UFUNCTION(BlueprintCallable, Category = "Stride Wheel")
    void SetStrideInterval(float NewInterval);

    UFUNCTION(BlueprintPure, Category = "Stride Wheel")
    bool IsStrideActive() const;

    // Events
    UPROPERTY(BlueprintAssignable, Category = "Stride Wheel")
    FOnStrideTrigger OnStrideTrigger;
};
```

---

### 2.5 Documentation Template

**Every module must include** : `Documentation/README.md`

**Structure** :
```markdown
# [Module Name] — Proto Ready Pack

## Quick Start (< 5 min)
1. Add component to Actor
2. Assign DataAsset
3. Done!

## Setup (< 10 min)
### 1. Component Setup
...

### 2. DataAsset Configuration
...

### 3. Blueprint Integration
...

## API Reference
### Functions
- `FunctionName()` — Description

### Events
- `OnEvent` — When triggered

## Troubleshooting
**Problem**: X  
**Solution**: Y

## Example Project
See `DM_[Module]_Showcase.umap`
```

---

### 2.6 Demo Map Requirements

**Every module must include** : `Content/Demo/DM_<Module>_Showcase.umap`

**Requirements** :
- Lighting: Directional Light + Sky
- Camera: Third-person or free-fly
- Character/Actor: Demonstrating module
- Instructions: Text Render or Widget "Press X to..."
- Clean: No clutter, focus on module demo

**Performance target** : 60 FPS on mid-range hardware

---

### 2.7 Code Quality Standards

**C++** :
- Unreal coding conventions (U prefix, F prefix, GENERATED_BODY)
- Comments for complex logic
- No warnings on compilation
- No TODOs in final version

**Blueprint** :
- Organized nodes (use Comment boxes)
- Reroute nodes for clarity
- Named variables (no default names)

---

## UE5 Plugin Template — Design Approach

### 3.1 Objectif

Créer template réutilisable pour accélérer création de nouveaux modules.

**Template location** : `Templates/PR_Module_Template/`

### 3.2 Template Structure

```
PR_Module_Template/
├── PR_Module_Template.uplugin
├── Source/
│   ├── PR_Module_Template/
│   │   ├── Public/
│   │   │   ├── Components/
│   │   │   │   └── PR_ExampleComponent.h
│   │   │   └── Data/
│   │   │       └── PR_ExampleData.h
│   │   ├── Private/
│   │   │   ├── Components/
│   │   │   │   └── PR_ExampleComponent.cpp
│   │   │   └── Data/
│   │   │       └── PR_ExampleData.cpp
│   │   └── PR_Module_Template.Build.cs
│   └── PR_Module_TemplateEditor/ (optional)
├── Content/
│   ├── Demo/
│   │   └── DM_Example_Showcase.umap
│   └── Data/
│       └── DA_Example_Default.uasset
└── Documentation/
    └── README.md
```

### 3.3 .uplugin Template

```json
{
    "FileVersion": 3,
    "Version": 1,
    "VersionName": "1.0",
    "FriendlyName": "[Module Name]",
    "Description": "Proto Ready Pack - [Module Description]",
    "Category": "Proto Ready",
    "CreatedBy": "[Author]",
    "CreatedByURL": "",
    "DocsURL": "",
    "MarketplaceURL": "",
    "SupportURL": "",
    "CanContainContent": true,
    "IsBetaVersion": false,
    "IsExperimentalVersion": false,
    "Installed": false,
    "Modules": [
        {
            "Name": "PR_Module_Template",
            "Type": "Runtime",
            "LoadingPhase": "Default"
        }
    ]
}
```

### 3.4 Build.cs Template

```csharp
using UnrealBuildTool;

public class PR_Module_Template : ModuleRules
{
    public PR_Module_Template(ReadOnlyTargetRules Target) : base(Target)
    {
        PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

        PublicDependencyModuleNames.AddRange(new string[]
        {
            "Core",
            "CoreUObject",
            "Engine"
        });

        PrivateDependencyModuleNames.AddRange(new string[]
        {
            // Add module-specific dependencies
        });
    }
}
```

---

## Dependencies & Constraints

### Technical Dependencies

**Required UE versions** : 5.3+  
**Recommended** : 5.5 (latest LTS)

**Engine Modules (common)** :
- Core, CoreUObject, Engine (basics)
- UMG (if UI module)
- MetaSound (if audio module)

**Third-party** : None (zero external dependencies policy)

### Constraints from L0

**Architecture First** : Tous les standards DOIVENT être définis avant Phase 3

**Cohérence systémique** : Impossible de changer naming mid-project sans refactor total

**Traçabilité** : Standards documentés = source de vérité

---

## Risks & Mitigation

| Risk                           | Impact | Probability | Mitigation                                     |
| ------------------------------ | ------ | ----------- | ---------------------------------------------- |
| **Standards trop restrictifs** | Medium | Medium      | Focus sur essentiels, flexibilité où possible  |
| **Standards trop laxistes**    | High   | Medium      | Review par humain, enforce via checklist       |
| **Naming conflicts UE**        | Low    | Low         | `PR_` prefix évite collisions                  |
| **Template trop complexe**     | Medium | Low         | Minimal viable template, itérer après Module 1 |
| **Standards ignorés Phase 3+** | High   | Medium      | Checklist obligatoire avant publication        |

---

## Validation Criteria

**Pack_Vision.md** :
- [ ] Philosophie "Proto Ready" formalisée
- [ ] Modules Phase 1-3 listés
- [ ] Business model documenté
- [ ] USPs identifiés

**Shared_Standards.md** :
- [ ] Naming conventions complètes (C++, Assets)
- [ ] DataAsset pattern défini
- [ ] Blueprint API standards
- [ ] Documentation template créé
- [ ] Demo map requirements

**Templates** :
- [ ] .uplugin template fonctionnel
- [ ] Folder structure respectée
- [ ] Compile sans erreurs UE 5.5

**Checkpoint 2** :
- [ ] Human validation de Pack_Vision
- [ ] Human validation de Shared_Standards
- [ ] Template testé avec dummy module

---

## Next Steps (Post Phase 2)

1. **Phase 3** : Architect conçoit Module 1 (Stride Wheel) **basé sur ces standards**
2. **Iterate** : Après Module 1, raffiner standards si gaps identifiés
3. **Enforce** : Checklist obligatoire pour Module 2+

---

## Decisions Validées (2026-01-22)

1. **DataAsset namespace** : `PR_<Module>` ✅ **VALIDÉ**

2. **Blueprint vs C++** : C++ backend maximal, BP API surface maximale (helpers pour utilisateurs) ✅ **VALIDÉ**

3. **Demo complexity** : Simple showcase (< 5 min comprendre) ✅ **VALIDÉ**

4. **Versioning** : Semantic versioning (1.0.0) dès v1 ✅ **VALIDÉ**

5. **Pricing** : ~5€/module + bundles (référence, pas définitif) ✅ **NOTÉ**

---

## Status

- **Design State**: ✅ **VALIDATED**  
- **Ready for Planning**: ✅ YES (DEV.Planner peut créer plan détaillé Phase 2)  
- **Requires ADR**: NO (standards internes pack)  
- **Risks Identified**: See table above  
- **Human Approval**: 2026-01-22

---

## Recommended Workflow

### Task 2.1 — Pack Vision (Effort: Low, 2-3h)
1. Copier structure proposée ci-dessus
2. Valider modules Phase 1 avec humain
3. Finaliser pricing (confirmer 5€/10€/bundles)
4. Écrire USPs vs concurrence

### Task 2.2 — Shared Standards (Effort: Low-Medium, 4-6h)
1. Copier naming conventions
2. Créer DataAsset example class
3. Créer Blueprint API example
4. Écrire README.md template
5. Définir demo map checklist

### Task 2.3 — Templates UE5 (Effort: Low, 2-3h)
1. Créer plugin vide UE5.5
2. Ajouter example Component + DataAsset
3. Tester compilation
4. Documenter how-to-use template

**Total Phase 2** : ~8-12h travail

---

*Design by: DEV.Architect*  
*Based on Master Plan Phase 2*  
*Human validation required before Phase 3*
