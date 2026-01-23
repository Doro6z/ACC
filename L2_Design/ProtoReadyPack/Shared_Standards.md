# Proto Ready Pack — Shared Standards

**Created**: 2026-01-22  
**Status**: Draft  
**Version**: 0.1

> **CRITICAL** : Ces standards DOIVENT être respectés par tous les modules. Toute modification nécessite validation humaine et mise à jour de ce document.

---

## Table of Contents

1. [Naming Conventions](#naming-conventions)
2. [DataAsset Patterns](#dataasset-patterns)
3. [Blueprint API Standards](#blueprint-api-standards)
4. [Documentation Requirements](#documentation-requirements)
5. [Demo Map Requirements](#demo-map-requirements)
6. [Code Quality Standards](#code-quality-standards)
7. [Performance Targets](#performance-targets)
8. [Testing Requirements](#testing-requirements)

---

## Naming Conventions

### General Rules

- **Prefix** : `PR_` (Proto Ready) pour éviter collisions
- **Case** : PascalCase pour classes, camelCase pour variables
- **Clarity** : Noms descriptifs, pas d'abréviations sauf standard UE (BP, UI, AI)

---

### C++ Classes

**Components** :
```cpp
UPR<Module>Component
```
**Examples** :
- `UPRStrideWheelComponent`
- `UPRAmbienceComponent`
- `UPRSettingsComponent`

**Actors** :
```cpp
APR<Module>Actor
```
**Examples** :
- `APRTitanRoot`
- `APRAmbientZone`

**DataAsset Classes** :
```cpp
UPR<Module>Data
```
**Examples** :
- `UPRStrideWheelData`
- `UPRAmbienceData`
- `UPRSettingsProfile`

**Subsystems** :
```cpp
UPR<Module>Subsystem
```
**Examples** :
- `UPRAmbienceSubsystem`
- `UPRSettingsSubsystem`

---

### Enums

**Format** :
```cpp
EPR<Module><Purpose>
```

**Examples** :
```cpp
UENUM(BlueprintType)
enum class EPRFootstepSurface : uint8
{
    Grass,
    Stone,
    Wood,
    Water,
    Metal
};

UENUM(BlueprintType)
enum class EPRAmbienceState : uint8
{
    Inactive,
    FadingIn,
    Active,
    FadingOut
};
```

---

### Structs

**Format** :
```cpp
FPR<Module><Purpose>
```

**Examples** :
```cpp
USTRUCT(BlueprintType)
struct FPRStrideWheelConfig
{
    GENERATED_BODY()
    
    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    float StrideInterval = 1.0f;
    
    UPROPERTY(EditAnywhere, BlueprintReadWrite)
    float VolumeMultiplier = 1.0f;
};
```

---

### Unreal Assets

**DataAssets** :
```
DA_<ModuleName>_<Purpose>
```
**Examples** :
- `DA_StrideWheel_Default`
- `DA_Ambience_JungleDay`
- `DA_Settings_GameDefaults`

**Blueprints** :
```
BP_<ModuleName>_<Type>
```
**Examples** :
- `BP_StrideWheel_Component`
- `BP_TitanRoot_Actor`
- `BP_Settings_Widget`

**Maps** :
```
DM_<ModuleName>_Showcase
```
**(DM = Demo Map)**
**Examples** :
- `DM_StrideWheel_Showcase`
- `DM_TitanRoot_Showcase`

**Materials** :
```
M_<ModuleName>_<Purpose>
```
**Examples** :
- `M_TitanRoot_Bark`
- `M_UI_Button`

**Textures** :
```
T_<ModuleName>_<Type>_<Variant>
```
**Examples** :
- `T_TitanRoot_BaseColor`
- `T_UI_Icon_Settings`

**Sounds** :
```
SFX_<ModuleName>_<Type>
```
**Examples** :
- `SFX_Footstep_Grass`
- `SFX_Ambience_Wind`

---

## DataAsset Patterns

### Base Class Requirement

**ALL** DataAssets MUST inherit from `UPrimaryDataAsset` :

```cpp
#include "Engine/DataAsset.h"

UCLASS(BlueprintType)
class PROTOREADYPACK_API UPR<Module>Data : public UPrimaryDataAsset
{
    GENERATED_BODY()

public:
    // Override for Asset Manager
    virtual FPrimaryAssetId GetPrimaryAssetId() const override
    {
        return FPrimaryAssetId("<ModuleName>Data", GetFName());
    }
    
    // Module-specific configuration properties...
};
```

### Why UPrimaryDataAsset?

- ✅ Async loading support
- ✅ Asset Manager integration
- ✅ Memory optimization (load on demand)
- ✅ Cook-time validation
- ✅ Referenceable by FPrimaryAssetId (not FSoftObjectPath)

### Example: Stride Wheel Data

```cpp
UCLASS(BlueprintType)
class PROTOREADYPACK_API UPRStrideWheelData : public UPrimaryDataAsset
{
    GENERATED_BODY()

public:
    virtual FPrimaryAssetId GetPrimaryAssetId() const override
    {
        return FPrimaryAssetId("StrideWheelData", GetFName());
    }

    /** Distance between stride triggers (cm) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel")
    float StrideInterval = 100.0f;

    /** Volume multiplier for all footsteps */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel", meta = (ClampMin = "0.0", ClampMax = "2.0"))
    float VolumeMultiplier = 1.0f;

    /** Sound to play on each stride */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel")
    TObjectPtr<USoundBase> StrideSound;
};
```

---

## Blueprint API Standards

### Exposure Rules

**Public Properties** :
- Use `EditAnywhere` + `BlueprintReadWrite` for config
- Add `Category` for organization
- Use `meta` tags for constraints (`ClampMin`, `ClampMax`, `UIMin`, `UIMax`)
- Add tooltips via `meta = (ToolTip = "Description")`

**Public Functions** :
- Use `BlueprintCallable` for actions
- Use `BlueprintPure` for getters (no side effects)
- Add `Category` matching component/module name
- Return values for chaining (`return this;` pattern)

**Events** :
- Use `BlueprintAssignable` for delegate events
- Prefix with `On` (e.g., `OnStrideTrigger`)
- Pass relevant data via delegate signature

### Example Component API

```cpp
UCLASS(ClassGroup = (ProtoReady), meta = (BlueprintSpawnableComponent))
class PROTOREADYPACK_API UPRStrideWheelComponent : public UActorComponent
{
    GENERATED_BODY()

public:
    //~ Configuration
    
    /** Stride Wheel configuration DataAsset */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel")
    TObjectPtr<UPRStrideWheelData> StrideData;

    /** Enable/disable stride tracking */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Stride Wheel")
    bool bEnableStride = true;

    //~ API Functions

    /** Set stride interval distance (cm) */
    UFUNCTION(BlueprintCallable, Category = "Stride Wheel")
    void SetStrideInterval(float NewInterval);

    /** Get current stride interval */
    UFUNCTION(BlueprintPure, Category = "Stride Wheel")
    float GetStrideInterval() const;

    /** Check if stride is currently active */
    UFUNCTION(BlueprintPure, Category = "Stride Wheel")
    bool IsStrideActive() const;

    /** Reset accumulated distance */
    UFUNCTION(BlueprintCallable, Category = "Stride Wheel")
    void ResetStride();

    //~ Events

    /** Delegate signature for stride trigger */
    DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnStrideTrigger, float, DistanceTraveled);

    /** Called when stride interval is reached */
    UPROPERTY(BlueprintAssignable, Category = "Stride Wheel")
    FOnStrideTrigger OnStrideTrigger;
};
```

---

## Documentation Requirements

### README.md Structure

**Every module MUST include** : `Documentation/README.md`

**Required sections** :

```markdown
# [Module Name] — Proto Ready Pack

> One-line description of what the module does

## Quick Start (< 5 min)

**Goal** : Get module working in < 5 min

1. Add component to Actor
2. Assign DataAsset
3. Press Play
4. Done!

## Setup (< 10 min)

### 1. Add Component

[Screenshot: Component in Details panel]

Drag `PR[Module]Component` to your Actor.

### 2. Create DataAsset

[Screenshot: Create DataAsset menu]

Right-click Content Browser → Miscellaneous → Data Asset → `PR[Module]Data`

### 3. Configure DataAsset

[Screenshot: DataAsset properties]

Set properties:
- Property 1: Description
- Property 2: Description

### 4. Assign to Component

[Screenshot: Assign DataAsset]

In component details, assign your DataAsset.

### 5. Test

Press Play. You should see/hear [expected behavior].

## API Reference

### Functions

#### `FunctionName(Params)`
**Description** : What it does  
**Parameters** :
- `Param1` (Type) : Description
**Returns** : Type — Description  
**Example** :
```cpp
Component->FunctionName(Value);
```

### Events

#### `OnEventName`
**When** : Triggered when X happens  
**Signature** : `void(ParamType Param)`  
**Example** :
```cpp
Component->OnEventName.AddDynamic(this, &AMyActor::HandleEvent);
```

## Properties

| Property     | Type | Default | Description      |
| ------------ | ---- | ------- | ---------------- |
| PropertyName | Type | Value   | What it controls |

## Troubleshooting

**Problem** : Nothing happens  
**Solution** : Check DataAsset is assigned

**Problem** : Errors in log  
**Solution** : Verify UE version (5.3+)

## Example Project

Open `DM_[Module]_Showcase.umap` for a working example.

## Performance

- CPU cost: < X ms/frame
- Memory: ~X MB
- Tested on: UE 5.5, mid-range hardware (RTX 3060)

## Version

- **Version** : 1.0.0
- **UE Compatibility** : 5.3+
- **Last Updated** : YYYY-MM-DD

## Support

- **Issues** : [Report on Fab]
- **Documentation** : This file
- **Discord** : [Optional community link]
```

---

## Demo Map Requirements

### File Naming

```
Content/Demo/DM_<ModuleName>_Showcase.umap
```

### Required Elements

1. **Lighting**
   - Directional Light (sun)
   - Sky Atmosphere or Sky Sphere
   - Acceptable: Simple skybox

2. **Camera**
   - Third-person camera OR
   - Free-fly camera (player start)
   - Clear view of demonstration

3. **Demonstration Actor**
   - Actor using module component
   - Clearly visible/audible behavior
   - Auto-start demo (no user input required) OR
   - Clear instructions (Text Render / Widget)

4. **Instructions**
   - Text Render Actor OR UMG Widget
   - "Press [Key] to [Action]" if interactive
   - Position: Visible on spawn

5. **Performance**
   - Target: 60 FPS on mid-range hardware (RTX 3060 / RX 6600)
   - No unnecessary assets (keep map clean)
   - Use LODs if relevant

### Map Template Structure

```
DM_[Module]_Showcase/
├── Lighting
│   └── DirectionalLight
│   └── SkyAtmosphere
├── Camera
│   └── PlayerStart (with camera setup)
├── Demo Actor
│   └── BP_[Module]_Demo
├── Instructions
│   └── TextRenderActor
└── Ground/Environment (minimal)
    └── Plane or simple floor
```

### Example: Stride Wheel Showcase

```
DM_StrideWheel_Showcase.umap:
- Character with StrideWheel component
- Walks in circle automatically (AIController or Timeline)
- Different surface types (PhysicalMaterials zones)
- Text: "Character footsteps change per surface"
```

---

## Code Quality Standards

### C++ Standards

**Must follow** :
- Unreal Engine coding conventions
- U prefix for UObject classes
- F prefix for structs
- E prefix for enums
- A prefix for Actors

**Compilation** :
- ✅ Zero errors
- ✅ Zero warnings (treat warnings as errors)
- ⚠️ Acceptable: Platform-specific warnings (document why)

**Comments** :
```cpp
// Simple comments for clarification

/**
 * Detailed comments for public API
 * @param ParamName Description of parameter
 * @return Description of return value
 */
UFUNCTION(BlueprintCallable)
ReturnType FunctionName(ParamType ParamName);
```

**No TODOs in final version** :
- ❌ `// TODO: Implement this`
- ✅ Issue tracker or documentation for future work

---

### Blueprint Standards

**Node Organization** :
- Use Comment boxes for sections
- Group related nodes
- Use Reroute nodes for clarity (avoid spaghetti)

**Variable Naming** :
- Descriptive names (not `NewVar_0`)
- Prefix `b` for booleans (`bIsActive`)
- Category organization

**Functions** :
- Keep functions small (< 20 nodes ideal)
- Pure functions when possible (no side effects)
- Use local variables for clarity

---

## Performance Targets

### Per-Frame Cost

**Target** : Each component should cost < 0.1ms per Actor

**Measurement** :
```
stat game
stat unit
```

**If exceeded** : Document why and optimization plan

---

### Memory

**Target** : < 5 MB per module plugin (Content included)

**Measurement** :
```
stat memory
memreport
```

---

### Loading Time

**Target** : < 500ms to load module DataAssets

**Use async loading** :
```cpp
FStreamableManager& Streamable = UAssetManager::GetStreamableManager();
Streamable.RequestAsyncLoad(AssetPath, FStreamableDelegate::CreateUObject(this, &UMyClass::OnAssetLoaded));
```

---

## Testing Requirements

### Pre-Submission Checklist

**Functional Tests** :
- [ ] Component works in clean project (no dependencies)
- [ ] DataAsset loads without errors
- [ ] Blueprint API all functions work
- [ ] Events fire correctly
- [ ] Demo map runs at 60 FPS

**Compatibility Tests** :
- [ ] UE 5.3 (if backward compatible)
- [ ] UE 5.4
- [ ] UE 5.5 (primary target)
- [ ] Windows (primary)
- [ ] Optional: Mac, Linux

**Edge Cases** :
- [ ] Null DataAsset (graceful handling)
- [ ] Component removed at runtime
- [ ] Multiple instances in same level

**Documentation Tests** :
- [ ] README Quick Start works (< 5 min)
- [ ] Screenshots up-to-date
- [ ] API examples compile

---

## Version Control

### Semantic Versioning

**Format** : `MAJOR.MINOR.PATCH`

**Rules** :
- `MAJOR` : Breaking changes (API incompatible)
- `MINOR` : New features (backward compatible)
- `PATCH` : Bug fixes

**Examples** :
- `1.0.0` : Initial release
- `1.1.0` : Added new function (compatible)
- `1.0.1` : Fixed crash bug
- `2.0.0` : Changed DataAsset structure (breaking)

---

## Exceptions & Overrides

**When standards can be bent** :
- Performance-critical code (document why)
- Platform-specific workarounds (document limitation)
- UE API constraints (e.g., can't inherit UPrimaryDataAsset due to X)

**How to request exception** :
1. Document reason in code comments
2. Add note in module README.md
3. Get human validation before module submission

---

## Updates to Standards

**Process** :
1. Identify need for standard change
2. Create ADR (Architecture Decision Record)
3. Human validation required
4. Update this document (version bump)
5. **Notify all modules** : May require updates retroactively

**Last Updated** : 2026-01-22  
**Version** : 0.1 (Draft)

---

*Shared Standards — Proto Ready Pack*  
*All modules MUST comply — Non-compliance = rejection*
