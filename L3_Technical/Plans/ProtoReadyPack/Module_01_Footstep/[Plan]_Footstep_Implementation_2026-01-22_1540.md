# Plan — Module 01: Footstep System

**File:** `[Plan]_Footstep_Implementation_2026-01-22_1540.md`  
**Created:** 2026-01-22 15:40  
**L1 Goal:** [G2 — Premiers actifs (Mai 2026)](file:///c:/Obsidian%20Vaults/UE%20Projects/L1_Strategy/Goals.md#L37)  
**Status:** Proposed

---

## Context

### Trigger
- Phase 2 complète (architecture + standards validés)
- Brainstorm Module Footstep validé avec amendements
- Master Plan Phase 3: Premier module comme référence

### Scope
**Inclus**:
- Component C++ : `UPRFootstepComponent`
- DataAsset : `UPRFootstepData`
- AnimNotify : `UAnimNotify_PRFootstep`
- 3 trace modes (Socket, Bone, Capsule)
- 2 sync modes (Distance, AnimNotify)
- N-leg support (UniLeg à Multi-leg)
- Audio effects chain (DSP presets)
- Demo map avec 4 surfaces
- Documentation complète

**Exclus**:
- Gait modulation (Walk/Jog/Sprint) - Phase 2 module si demandé
- Multiplayer replication (cosmetic local only)
- Advanced physics interactions

### Success Criteria
- [ ] Component fonctionne dans clean project
- [ ] DataAsset configuration < 5 min
- [ ] Demo map 60 FPS
- [ ] Documentation README < 10 min setup
- [ ] 0 errors, 0 warnings compilation
- [ ] Module 1 = référence pour modules suivants

---

## Research Base

Documents consultés :
- **[Brnst]_Footstep_Module_2026-01-22** — Architecture complète validée
- **[Arch]_Phase2_PackArchitecture** — Standards techniques
- **Pack_Vision** — Philosophie Proto Ready
- **Shared_Standards** — Naming, DataAsset patterns, BP API
- **Apex LMAudioComponent** — Code source existant pour extraction

---

## Task Breakdown

### Phase A — Plugin Setup (1 jour)

- [ ] **Task A.1** — Créer plugin UE5
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Tools → New Plugin → Blank
    - Name: `PR_Footstep`
    - Category: Proto Ready
    - Template from `PR_Module_Template`
  - Output: Plugin compilable vide
  - Dependencies: None

- [ ] **Task A.2** — Configure Build.cs
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Dependencies: Core, CoreUObject, Engine, PhysicsCore
    - PCH usage configured
  - Dependencies: Task A.1

---

### Phase B — Core Component (2-3 jours)

- [ ] **Task B.1** — Créer UPRFootstepComponent.h
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - Properties: FootstepData, bEnableFootsteps, TraceMode, SyncMode, VolumeMultiplier
    - Properties (perf): TickInterval, bUseLOD, LODDistanceThreshold
    - Functions: TriggerFootstep, TriggerLand, SetTraceMode, GetAccumulatedDistance, ResetDistance
    - Events: OnFootstepPlayed, OnLandPlayed delegates
    - Enums: EPRFootstepTraceMode, EPRFootstepSyncMode
  - Output: Header file complet
  - Dependencies: Task A.2

- [ ] **Task B.2** — Implémenter trace logic
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - Socket mode: LineTraceSingleByChannel from socket
    - Bone mode: LineTrace from bone location
    - Capsule mode: LineTrace from capsule bottom
    - **Multi-surface handling**: Optional SphereTrace for border stability
    - Surface averaging if N-leg enabled (reduce glitching)
    - Return EPhysicalSurface
  - Dependencies: Task B.1

- [ ] **Task B.3** — Implémenter distance tracking + LOD
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - Tick: accumulate distance from movement
    - **Performance**: Tick Interval configuré (default: EveryFrame)
    - **LOD système**: Distant NPCs tick moins fréquent (e.g., 0.2s interval)
    - Compare vs StrideInterval
    - Trigger footstep when threshold reached
    - Cycle through FootSockets array (N-leg support)
  - Dependencies: Task B.1

- [ ] **Task B.4** — Implémenter PlayFootstepSound
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - Get sound from DataAsset TMap by surface
    - **Audio spawning**: Use PlaySoundAtLocation (not SpawnSoundAttached)
    - Rationale: Footsteps are short sounds, avoid component accumulation
    - Fallback: SpawnSoundAttached only if EffectsChain present
    - Apply volume/pitch randomization
    - Apply EffectsChain if present (requires AudioComponent)
    - Broadcast OnFootstepPlayed event
  - Dependencies: Task B.2, B.3

- [ ] **Task B.5** — Implémenter TriggerLand (Jump/Fall)
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - Function: TriggerLand(float FallVelocity)
    - Trace from feet to detect landing surface
    - Volume based on velocity (soft vs heavy land)
    - Optional: Heavy land threshold in DataAsset
    - Reuse surface detection logic from B.2
  - Dependencies: Task B.4

---

### Phase C — DataAsset (1 jour)

- [ ] **Task C.1** — Créer UPRFootstepData.h
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - Inherit UPrimaryDataAsset
    - Properties: SurfaceSounds TMap, DefaultSound
    - Trace settings: TraceLength, FootSockets, FootBones
    - Audio settings: VolumeRange, PitchRange, AttenuationSettings, EffectsChain
    - Distance mode: PreferredStrideInterval
  - Output: DataAsset class
  - Dependencies: Task B.1

- [ ] **Task C.2** — Créer example DataAssets
  - Effort: Low
  - Owner: Humain
  - Détails:
    - DA_Footstep_Human (biped)
    - DA_Footstep_Quadruped (4 legs)
    - DA_Footstep_Spider (8 legs optional)
  - Dependencies: Task C.1

---

### Phase D — AnimNotify Support (0.5 jour)

- [ ] **Task D.1** — Créer UAnimNotify_PRFootstep
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Properties: FootSocket, VolumeMultiplier
    - Notify() calls Component->TriggerFootstep()
  - Output: AnimNotify class
  - Dependencies: Task B.4

---

### Phase E — Audio Effects Presets (1 jour)

- [ ] **Task E.1** — Créer DSP preset assets
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - Preset_Footstep_LowPass (muffled)
    - Preset_Footstep_HiPass (crisp)
    - Preset_Footstep_Reverb (echo)
    - Preset_Footstep_None (clean)
  - Output: 4 USoundEffectSourcePresetChain assets
  - Dependencies: Task C.2

---

### Phase F — Demo Content (2 jours)

- [ ] **Task F.1** — Source/Create footstep sounds
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - Grass, Stone, Wood, Water sounds (royalty-free)
    - At least 2 variations per surface (randomization)
  - Output: Sound assets
  - Dependencies: None (parallèle)

- [ ] **Task F.2** — Create Physical Materials
  - Effort: Low
  - Owner: Humain
  - Détails:
    - PhysicalMaterial_Grass (SurfaceType = Grass)
    - PhysicalMaterial_Stone (SurfaceType = Stone)
    - PhysicalMaterial_Wood (SurfaceType = Wood)
    - PhysicalMaterial_Water (SurfaceType = Water)
  - Dependencies: None (parallèle)

- [ ] **Task F.3** — Build demo map
  - Effort: Medium
  - Owner: Humain
  - Détails:
    - DM_Footstep_Showcase.umap
    - 4 zones with different PhysicalMaterials
    - Character with PRFootstepComponent
    - AIController or Timeline movement
    - Instructions Text Render
    - 60 FPS target
  - Dependencies: Task B.4, F.1, F.2

---

### Phase G — Documentation (1 jour)

- [ ] **Task G.1** — Write README.md
  - Effort: Low-Medium
  - Owner: Humain
  - Détails:
    - Quick Start (< 5 min)
    - Setup (< 10 min) with screenshots
    - API Reference (functions, events, properties)
    - Troubleshooting section
    - Example project reference
  - Output: Documentation/README.md
  - Dependencies: Phase F complete

- [ ] **Task G.2** — Capture screenshots
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Component in Details panel
    - DataAsset configuration
    - Demo map running
    - Min 6 screenshots total
  - Dependencies: Task G.1

---

### Phase H — Testing & Polish (1 jour)

- [ ] **Task H.1** — Clean project test
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Create new UE5 project
    - Add plugin only (no other dependencies)
    - Follow README Quick Start
    - Verify < 5 min to working footsteps
  - Dependencies: Phase G complete

- [ ] **Task H.2** — Performance profiling
  - Effort: Low
  - Owner: Humain
  - Détails:
    - stat game / stat unit
    - Verify < 0.1ms per component
    - Demo map 60 FPS verified
  - Dependencies: Task H.1

- [ ] **Task H.3** — Code cleanup
  - Effort: Low
  - Owner: Humain
  - Détails:
    - Remove debug logs
    - Comment complex logic
    - No TODOs remaining
    - Compile 0 errors 0 warnings
  - Dependencies: Task H.2

---

## Dependencies

### Critical Path
```
Task A.1 (Plugin)
  ↓
Task A.2 (Build.cs)
  ↓
Task B.1-B.4 (Component logic)
  ↓
Task C.1-C.2 (DataAsset)
  ↓
Task D.1 (AnimNotify)
  ↓
Phase E+F (Audio + Demo) — Parallélisables
  ↓
Phase G (Documentation)
  ↓
Phase H (Testing & Polish)
```

### Blockers
- Phase B DOIT être complet avant Phase F (demo needs component)
- Phase G DOIT attendre Phase F (screenshots need demo)
- Phase H DOIT être dernier (validation finale)

---

## Validation Checkpoints

- [ ] **Checkpoint A** — Plugin compilable
  - Criteria: Plugin loads in UE5, no errors

- [ ] **Checkpoint B** — Component fonctionnel
  - Criteria: Footsteps play on different surfaces

- [ ] **Checkpoint C** — N-leg support validated
  - Criteria: Biped, Quadruped, Spider configs work

- [ ] **Checkpoint D** — Demo map 60 FPS
  - Criteria: Performance target met

- [ ] **Checkpoint Final** — Module production-ready
  - Criteria: All tasks complete, README works, clean project test passed

---

## Effort Assessment (Heuristic)

⚠️ Estimations génériques, non calibrées à la vélocité personnelle.

**Par Phase** :
- **Phase A** (Plugin Setup): **Low** (~4h)
- **Phase B** (Component): **Medium** (~12-16h)
- **Phase C** (DataAsset): **Low** (~4-6h)
- **Phase D** (AnimNotify): **Low** (~2h)
- **Phase E** (Audio Effects): **Low-Medium** (~4-6h)
- **Phase F** (Demo Content): **Medium** (~8-12h)
- **Phase G** (Documentation): **Low-Medium** (~4-6h)
- **Phase H** (Testing): **Low** (~4h)

**Total**: ~42-56h travail  
**Timeline suggérée**: 2 semaines (full-time) ou 3-4 semaines (part-time)

---

## Risks & Mitigation

| Risk                                          | Impact | Probability | Mitigation                              |
| --------------------------------------------- | ------ | ----------- | --------------------------------------- |
| **N-leg cycling logic complexe**              | Medium | Medium      | Start simple (biped), iterate to N-leg  |
| **Audio effects incompatibilité UE versions** | Medium | Low         | Test UE 5.3+, document min version      |
| **Physical Material setup confusing**         | Medium | High        | Excellent doc + demo map as reference   |
| **Sounds royalty-free difficiles**            | Low    | Medium      | Use placeholder, user replaces easily   |
| **Performance > 0.1ms**                       | High   | Low         | Profile early, optimize trace frequency |

---

## Notes

### Extraction from Apex

**LMAudioComponent existant** peut servir de base :
- Surface detection logic ✅ Réutilisable
- Sound mapping TMap ✅ Réutilisable
- Quadruped paw delay ❌ Remplacé par N-leg cycling

**Différences majeures** :
- Apex : AnimNotify only
- Proto Ready : Dual sync (Distance + AnimNotify)

### Standards Compliance Checklist

- [ ] Naming: `PR_` prefix utilisé
- [ ] DataAsset: Inherit UPrimaryDataAsset ✅
- [ ] Blueprint API: All functions BlueprintCallable ✅
- [ ] Documentation: README template suivi ✅
- [ ] Demo Map: DM_Footstep_Showcase.umap ✅
- [ ] Performance: < 0.1ms target ✅

---

## Prochaines Actions Immédiates

1. **Validation humaine** de ce plan
2. **Task A.1** : Créer plugin dans UE5
3. **Task B.1** : Commencer Component header
4. **Checkpoint A** : Plugin compiles

---

*Plan generated by DEV.Planner*  
*Based on [Brnst]_Footstep_Module_2026-01-22*  
*Human validation required before execution.*
