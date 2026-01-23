# Brainstorm — Audio/Footstep Module

**Created**: 2026-01-22  
**Type**: Architecture Brainstorm  
**Module**: PR_AudioFootstep

---

## Clarification Structure

**Catégorie** : Audio  
**Modules** :
1. **Footstep** (ce brainstorm)
2. **Ambience** (séparé)

**Footstep ≠ Stride Wheel** :
- Stride Wheel = Une technique de synchronisation parmi d'autres
- Module Footstep = Système complet avec plusieurs options

---

## Objectif Module

**Pitch** : "Configurez des footsteps pour plusieurs personnages en < 10 min avec détection de surface automatique et multiples techniques de synchronisation"

**Scope** :
- ✅ Multi-character support via DataAssets
- ✅ Surface detection automatique (Physical Materials)
- ✅ Plusieurs techniques trace (socket, bone, capsule)
- ✅ Plusieurs techniques sync (distance/Stride Wheel, AnimNotify)
- ✅ Runtime enable/disable
- ✅ Volume/Pitch variation
- ✅ Networking ready

---

## Core Features

### 1. Surface Detection

**Méthode** : Line trace → Physical Material → Sound mapping

**Physical Surfaces (UE5 enum)** :
- Default
- Grass
- Stone
- Wood
- Water
- Metal
- (+ custom via project settings)

**Mapping** : `TMap<EPhysicalSurface, USoundBase*>` in DataAsset

**Fallback** : Si surface pas mappée → DefaultFootstepSound

---

### 2. Trace Techniques

**Option A — Socket-Based (Most Accurate)** :
- Line trace from foot socket (e.g., `foot_l`, `foot_r`)
- Direction: Down (-Z)
- Length: Configurable (default 20cm)
- **Pros** : Precise per-foot, supports quadrupeds
- **Cons** : Requires skeleton with sockets

**Option B — Bone-Based (Fallback)** :
- Line trace from foot bone location
- Same as socket but no socket required
- **Pros** : Works without sockets
- **Cons** : Slightly less flexible positioning

**Option C — Capsule-Based (Simple)** :
- Single trace from capsule bottom center
- Direction: Down
- **Pros** : Simple, no skeleton dependency
- **Cons** : Less precise, no per-foot differentiation

**User Choice** : Enum in Component
```cpp
UENUM(BlueprintType)
enum class EPRFootstepTraceMode : uint8
{
    Socket,      // Precise, per-foot
    Bone,        // Per-foot, no socket needed
    Capsule      // Simple, single trace
};
```

---

### 3. Synchronization Methods

**Method 1 — Distance-Based (Stride Wheel)** :
- Track distance traveled
- Trigger footstep every X cm
- **Pros** : No anim dependency, works with procedural movement
- **Cons** : Not perfectly synced with animation

**Method 2 — AnimNotify** :
- Traditional anim notify in animation
- Per-foot precision
- **Pros** : Perfect anim sync
- **Cons** : Requires anim setup, not procedural-friendly

**User Choice** : Enum in Component
```cpp
UENUM(BlueprintType)
enum class EPRFootstepSyncMode : uint8
{
    Distance,       // Stride Wheel technique
    AnimNotify      // Traditional anim notify
};
```

**Both supported** : User choisit via DataAsset ou Component property

---

### 4. Runtime Control

**Enable/Disable** :
```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite)
bool bEnableFootsteps = true;
```

**Volume Multiplier** :
```cpp
UPROPERTY(EditAnywhere, BlueprintReadWrite, meta = (ClampMin = "0.0", ClampMax = "2.0"))
float VolumeMultiplier = 1.0f;
```

**Per-Foot Control** (advanced) :
```cpp
// Optional: Disable specific feet
TArray<FName> DisabledSockets;
```

---

### 5. Multi-Leg Support (N Pattes)

**Problem** : Support any number of legs (biped, quadruped, spider 8-leg, etc.)

**Solution** : Dynamic foot socket array in DataAsset

**Modes** :
- **UniLeg** : 1 socket only (e.g., cane, pogo stick, monopod creature)
- **Biped** : 2 sockets (human, bird)
- **Quadruped** : 4 sockets (dog, horse)
- **Multi-Leg** : 6+ sockets (spider, insect)

**DataAsset Configuration** :
```cpp
/** Foot socket names (supports 1-N legs) */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Trace")
TArray<FName> FootSockets = { "foot_l", "foot_r" };
```

**User simply adds/removes sockets** :
- UniLeg: `{"foot_center"}`
- Biped: `{"foot_l", "foot_r"}`
- Quadruped: `{"foot_fl", "foot_fr", "foot_bl", "foot_br"}`
- Spider: `{"leg_1", "leg_2", "leg_3", "leg_4", "leg_5", "leg_6", "leg_7", "leg_8"}`

**Distance Mode Behavior** :
- Cycle through foot sockets sequentially
- Each stride interval triggers next socket in array
- Wraps around (spider: leg_1 → leg_2 → ... → leg_8 → leg_1)

**AnimNotify Behavior** :
- User places AnimNotify per foot in animation
- Each notify triggers specific socket
- Supports any number of notifies

---

### 6. Audio Effects (DSP Chain)

**UE5 Feature** : `USoundEffectSourcePresetChain`

**Purpose** : Apply DSP effects to footsteps (low-pass, hi-pass, reverb, delay, etc.)

**DataAsset Property** :
```cpp
/** Optional audio effects chain to apply */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Audio|Effects")
TObjectPtr<USoundEffectSourcePresetChain> EffectsChain;
```

**Provided Templates** (shipped with module) :
1. **Preset_Footstep_LowPass** : Muffled footsteps (carpet, snow)
2. **Preset_Footstep_HiPass** : Crisp footsteps (metal, glass)
3. **Preset_Footstep_Reverb** : Echo footsteps (cave, hall)
4. **Preset_Footstep_None** : Clean (default)

**User Workflow** :
1. Assign preset in DataAsset
2. OR create custom `USoundEffectSourcePresetChain` asset
3. Automatically applied on PlaySound

**Technical Implementation** :
```cpp
void UPRFootstepComponent::PlayFootstepSound(FName SocketName, EPhysicalSurface Surface)
{
    USoundBase* Sound = GetSoundForSurface(Surface);
    if (!Sound) return;

    UAudioComponent* AudioComp = UGameplayStatics::SpawnSoundAttached(
        Sound,
        GetOwner()->GetRootComponent(),
        SocketName,
        FVector::ZeroVector,
        EAttachLocation::SnapToTarget,
        false, // stop when attached to destroyed
        VolumeMultiplier,
        FMath::RandRange(FootstepData->PitchRange.X, FootstepData->PitchRange.Y),
        0.0f, // start time
        FootstepData->AttenuationSettings,
        nullptr, // concurrency
        false // persist across level transitions
    );

    // Apply effects chain if present
    if (FootstepData->EffectsChain && AudioComp)
    {
        AudioComp->SetSourceEffectChain(FootstepData->EffectsChain);
    }
}
```

---

### 7. Performance Optimizations

**Problem** : 50+ NPCs with Tick footsteps = performance cost

**Solutions** :

**A. Tick Interval** :
```cpp
/** How often to update distance (0 = every frame) */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Performance")
float TickInterval = 0.0f; // 0 = EveryFrame, 0.1 = 10 times per second
```

**B. LOD System** :
```cpp
/** Enable distance-based LOD */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Performance")
bool bUseLOD = true;

/** Distance threshold for reduced tick rate (cm) */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Performance")
float LODDistanceThreshold = 2000.0f; // 20m
```

**Behavior** :
- Player/nearby NPCs: Tick every frame
- Distant NPCs (> LODDistanceThreshold): Tick interval 0.2s
- Out of range: Disable component

**C. Audio Spawning** :
- Use `PlaySoundAtLocation` for short footstep sounds (no component accumulation)
- Use `SpawnSoundAttached` ONLY if EffectsChain present (requires AudioComponent)

---

### 8. Jump/Land Support

**Missing Feature** : Footstep for landing after jump/fall

**Solution** : `TriggerLand` function

```cpp
/** Trigger landing footstep (e.g., after jump/fall) */
UFUNCTION(BlueprintCallable, Category = "Footstep")
void TriggerLand(float FallVelocity);
```

**Logic** :
1. Trace from feet to detect landing surface
2. Volume based on velocity:
   - Low velocity (< 400): Soft land (volume 0.5x)
   - High velocity (> 800): Heavy land (volume 1.5x)
3. Optional: Separate HeavyLandSound in DataAsset
4. Broadcast OnLandPlayed event

**Integration** :
- Character calls `TriggerLand` in `OnLanded()` event
- Distance mode auto-triggers if large Z velocity change detected

---

### 9. Multi-Surface Handling

**Problem** : LineTrace on texture borders = unstable (grass/stone edge glitches)

**Solution** : Optional SphereTrace or surface averaging

**A. SphereTrace Mode** :
```cpp
/** Use sphere trace instead of line (more stable on borders) */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Trace")
bool bUseSphereTrace = false;

/** Sphere radius for trace (cm) */
UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Trace", meta = (EditCondition = "bUseSphereTrace"))
float SphereRadius = 5.0f;
```

**B. Surface Averaging (Multi-Leg)** :
- If N-leg enabled (4+ feet), take most common surface from last N traces
- Reduces glitching when walking on border
- Example: 3/4 feet on grass → play grass sound

---

### 10. Multi-Character Support

**DataAsset contains** :
- Surface → Sound mappings
- Trace settings (length, offset)
- Volume/Pitch ranges
- Sync mode preference
- Foot socket names (if socket mode)

---

## Architecture Proposal

### Component Structure

```cpp
UCLASS(ClassGroup = (ProtoReady), meta = (BlueprintSpawnableComponent))
class UPRFootstepComponent : public UActorComponent
{
    GENERATED_BODY()

public:
    //~ Configuration
    
    /** Footstep configuration DataAsset */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep")
    TObjectPtr<UPRFootstepData> FootstepData;

    /** Enable/disable footstep sounds */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep")
    bool bEnableFootsteps = true;

    /** Trace technique to use */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Trace")
    EPRFootstepTraceMode TraceMode = EPRFootstepTraceMode::Socket;

    /** Synchronization method */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Sync")
    EPRFootstepSyncMode SyncMode = EPRFootstepSyncMode::Distance;

    /** Volume multiplier (runtime adjustable) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Audio", meta = (ClampMin = "0.0", ClampMax = "2.0"))
    float VolumeMultiplier = 1.0f;

    //~ Distance Mode Settings
    
    /** Distance interval for stride triggers (cm) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep|Distance Mode", meta = (EditCondition = "SyncMode == EPRFootstepSyncMode::Distance"))
    float StrideInterval = 100.0f;

    //~ API Functions

    /** Manually trigger footstep (for AnimNotify mode) */
    UFUNCTION(BlueprintCallable, Category = "Footstep")
    void TriggerFootstep(FName SocketName = NAME_None);

    /** Set trace mode at runtime */
    UFUNCTION(BlueprintCallable, Category = "Footstep")
    void SetTraceMode(EPRFootstepTraceMode NewMode);

    /** Get current accumulated distance (Distance mode) */
    UFUNCTION(BlueprintPure, Category = "Footstep")
    float GetAccumulatedDistance() const;

    /** Reset distance counter */
    UFUNCTION(BlueprintCallable, Category = "Footstep")
    void ResetDistance();

    //~ Events

    DECLARE_DYNAMIC_MULTICAST_DELEGATE_TwoParams(FOnFootstepPlayed, FName, SocketName, EPhysicalSurface, Surface);

    /** Called when a footstep sound is played */
    UPROPERTY(BlueprintAssignable, Category = "Footstep")
    FOnFootstepPlayed OnFootstepPlayed;

private:
    // Internal tracking
    float AccumulatedDistance = 0.0f;
    FVector LastPosition;

    // Trace execution
    EPhysicalSurface PerformTrace(FName SocketName, FVector& OutHitLocation);
    void PlayFootstepSound(FName SocketName, EPhysicalSurface Surface);
};
```

---

### DataAsset Structure

```cpp
UCLASS(BlueprintType)
class UPRFootstepData : public UPrimaryDataAsset
{
    GENERATED_BODY()

public:
    virtual FPrimaryAssetId GetPrimaryAssetId() const override
    {
        return FPrimaryAssetId("FootstepData", GetFName());
    }

    //~ Surface Mappings

    /** Map Physical Surface → Footstep Sound */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Surfaces")
    TMap<TEnumAsByte<EPhysicalSurface>, USoundBase*> SurfaceSounds;

    /** Fallback sound if surface not in map */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Surfaces")
    TObjectPtr<USoundBase> DefaultSound;

    //~ Trace Settings

    /** Trace length (cm) below foot */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Trace")
    float TraceLength = 20.0f;

    /** Socket names for feet (Socket mode) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Trace")
    TArray<FName> FootSockets = { "foot_l", "foot_r" };

    /** Bone names for feet (Bone mode fallback) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Trace")
    TArray<FName> FootBones = { "foot_l", "foot_r" };

    //~ Audio Settings

    /** Volume range (random) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Audio")
    FVector2D VolumeRange = FVector2D(0.8f, 1.0f);

    /** Pitch range (random) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Audio")
    FVector2D PitchRange = FVector2D(0.95f, 1.05f);

    /** Sound attenuation settings */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Audio")
    TObjectPtr<USoundAttenuation> AttenuationSettings;

    /** Optional audio effects chain (low-pass, hi-pass, reverb, etc.) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Audio|Effects")
    TObjectPtr<USoundEffectSourcePresetChain> EffectsChain;

    //~ Distance Mode Settings

    /** Preferred stride interval (if using distance mode) */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Distance Mode")
    float PreferredStrideInterval = 100.0f;
};
```

---

## AnimNotify Support

**Class** : `UAnimNotify_PRFootstep`

```cpp
UCLASS()
class UAnimNotify_PRFootstep : public UAnimNotify
{
    GENERATED_BODY()

public:
    /** Which foot socket to trace from */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep")
    FName FootSocket = "foot_l";

    /** Optional volume override */
    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Footstep")
    float VolumeMultiplier = 1.0f;

    virtual void Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation) override
    {
        if (AActor* Owner = MeshComp->GetOwner())
        {
            if (UPRFootstepComponent* FootstepComp = Owner->FindComponentByClass<UPRFootstepComponent>())
            {
                FootstepComp->TriggerFootstep(FootSocket);
            }
        }
    }
};
```

---

## Demo Map Design

**DM_Footstep_Showcase.umap** :

**Layout** :
1. **Zone 1** : Grass surface (PhysicalMaterial_Grass)
2. **Zone 2** : Stone surface (PhysicalMaterial_Stone)
3. **Zone 3** : Wood surface (PhysicalMaterial_Wood)
4. **Zone 4** : Water shallow (PhysicalMaterial_Water)

**Character** :
- Third-person character
- Walks in path crossing all zones
- AIController or Timeline-driven movement
- Shows sound changes per surface

**UI Instructions** :
- Text Render: "Character footsteps change per surface type"
- Show current trace mode + sync mode (UMG Widget)

**Interactivity (optional)** :
- Press 1/2/3 to switch trace mode (Socket/Bone/Capsule)
- Press Q/E to switch sync mode (Distance/AnimNotify)

---

## Technical Challenges & Solutions

### Challenge 1: Distance Mode + AnimNotify Coexistence

**Problem** : User peut vouloir les deux simultaneously ?  
**Solution** : Mutually exclusive via enum. Clear in doc.

**Alternative** : Hybrid mode (distance as fallback si pas AnimNotify) ?  
**Decision** : Keep simple, one mode at a time. User can switch runtime.

---

### Challenge 2: Quadruped Support

**Problem** : 4 feet vs 2 feet  
**Solution** : `FootSockets` array supports N sockets. User defines all foot sockets in DataAsset.

**Distance Mode** : How to handle 4 feet timing ?  
**Approach** : Cycle through foot sockets sequentially on each interval.

```cpp
// Pseudo-code
int CurrentFootIndex = 0;
OnDistanceIntervalReached()
{
    FName Socket = FootstepData->FootSockets[CurrentFootIndex];
    TriggerFootstep(Socket);
    CurrentFootIndex = (CurrentFootIndex + 1) % FootstepData->FootSockets.Num();
}
```

---

### Challenge 3: Network Replication

**Sounds local or replicated ?**  
**Answer** : Local playback (cosmetic), no replication needed.  
**Rationale** : Footsteps are client-side audio cosmetics. Replicating = bandwidth waste.

**Exception** : If gameplay-relevant (stealth game, sound alerts enemies), user adds custom replication logic.

---

## Comparison with Apex Implementation

**Apex "LMAudioComponent"** had :
- ✅ Surface detection
- ✅ Gait volume modulation (Walk/Jog/Sprint)
- ✅ Quadruped paw delay
- ❌ Only AnimNotify sync
- ❌ No distance mode
- ❌ No trace mode options

**Proto Ready Footstep** adds :
- ✅ Multiple trace techniques
- ✅ Multiple sync methods
- ✅ Simpler API (no GAS dependency)
- ✅ DataAsset-first (Apex had tight coupling)

**Extraction strategy** : Refactor LMAudioComponent logic, remove coupling, add new features.

---

## Next Steps

1. **Validate** : Human approval of this architecture
2. **Update Docs** :
   - Pack_Vision.md : Rename "Stride Wheel" → "Footstep" module
   - Shared_Standards.md : Add Footstep examples
3. **Create L2 Architecture** : Full technical design document
4. **Template Plugin** : Apply standards to template
5. **Implement** : Phase 3 execution

---

*Brainstorm — DEV.Architect*  
*Human validation required before proceeding*
