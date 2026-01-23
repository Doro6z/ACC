# ACC.Intendant Report — 2026-01-22_1240

## Context
- **Trigger**: User request — Proto Ready Pack vision & market analysis
- **Scope**: Strategic (L1/L2) — Pack concept, module candidates, business model
- **Objective**: Define comprehensive vision for modular plugin pack

---

## Research Base

**Documents Consultés**:
- [SavedInformations.md](file:///c:/Obsidian%20Vaults/UE%20Projects/SavedInformations.md) — Apex systems audit (15+ systems)
- [Report_2026-01-21_ApexPrimal_Audit](file:///c:/Obsidian%20Vaults/UE%20Projects/L4_Operations/Reports/Report_2026-01-21_1200_ApexPrimal_Audit.md)
- [Developpement_Personnel_Agentique.md](file:///c:/Obsidian%20Vaults/UE%20Projects/L5_Knowledge/Research/Developpement_Personnel_Agentique.md)

**Web Research Completed**:
- UE5 Fab Marketplace trends 2024-2025
- Plugin pricing strategies (indie/bundles)
- Rapid prototyping tools market

---

## Market Analysis

### 🔥 High-Demand Categories (2024-2025)

| Category                 | Market Signal                                   | Competition               |
| ------------------------ | ----------------------------------------------- | ------------------------- |
| **Footstep Audio**       | Always in demand, surface-aware systems popular | Medium (Ovani Sound ~$49) |
| **Menu/UI Systems**      | Common UI, data-driven menus highly sought      | High (many options)       |
| **Gameplay Systems**     | GAS, targeting, progression                     | Medium                    |
| **World Building**       | PCG, modular environments                       | High                      |
| **Character Frameworks** | Species, data-driven configs                    | Low (niche)               |

### 💰 Pricing Intelligence

**Single Plugins**:
- Niche/simple: $5-15
- Mid-tier: $20-50
- Complex: $50-100+

**Bundles**:
- DASH (world building): $7 (Student) → $89 (Enterprise)
- Blockout Tools: $19.99
- Full systems: $60-150

**Key Finding**: Tiered pricing (Personal/Professional) est standard sur Fab.

### 🎯 Gap Identified

**No "Proto Ready" bundle exists** combining:
- Ultra-fast setup (< 10 min/module)
- Data-driven (DataAssets, not hard-coded)
- Indie-friendly pricing ($5/module)
- Common systems every project needs

---

## Proto Ready Pack — Vision

### Core Philosophy

> **"From zero to prototype-ready in 10 minutes per module"**

**Principles**:
1. **Easy Setup** — Plug & Play, minimal configuration
2. **Data-Driven** — DataAssets, not code changes
3. **Blueprint-First** — Full BP API, C++ under the hood
4. **Modular** — Each module works standalone
5. **Proto-Ready** — Not production-polished, but functional fast

### Target Audience

- **Indie developers** starting prototypes
- **Game jam participants** (48-72h constraints)
- **Studios** needing rapid feature scaffolding
- **Learning developers** wanting clean examples

### Unique Selling Points

1. ✅ **Speed** — 10 min setup vs hours of custom code
2. ✅ **Affordability** — 5€/module (indie-friendly)
3. ✅ **Bundle Value** — 60€ for ~12 modules (50% savings)
4. ✅ **Consistency** — Same UX/naming across all modules
5. ✅ **Innovation** — Stride Wheel system (unique)

---

## Module Candidates

### 🟢 Tier 1 — High Priority (Extract from Apex)

| Module                 | Source                       | Effort | Market Appeal | Notes                     |
| ---------------------- | ---------------------------- | ------ | ------------- | ------------------------- |
| **Footstep System**    | LMAudioComponent, AnimNotify | Low    | 🔥🔥🔥           | + Stride Wheel innovation |
| **Ambience System**    | LMAmbienceSubsystem, Zones   | Low    | 🔥🔥🔥           | MetaSound ready           |
| **Survival Stats**     | LMSurvivalComponent          | Medium | 🔥🔥            | Stamina/Hunger/Health     |
| **Progression System** | LMProgressionComponent       | Medium | 🔥🔥            | Levels, perks, growth     |

### 🟡 Tier 2 — Medium Priority (Extract + Polish)

| Module               | Source              | Effort | Market Appeal | Notes                           |
| -------------------- | ------------------- | ------ | ------------- | ------------------------------- |
| **Species Config**   | LMSpeciesData       | High   | 🔥🔥            | Data-driven character framework |
| **Camera Framework** | LMSpeciesCameraData | Medium | 🔥             | Per-state camera profiles       |

### 🔵 Tier 3 — New Creations (Not from Apex)

| Module               | Concept                                | Effort | Market Appeal | Notes                 |
| -------------------- | -------------------------------------- | ------ | ------------- | --------------------- |
| **Menu System**      | Data-driven windows, Blueprint cascade | Medium | 🔥🔥🔥           | Main/Pause/Options    |
| **Save System**      | Slot-based, async, compression         | Medium | 🔥🔥            | Every game needs this |
| **Input Rebinding**  | Enhanced Input remapping UI            | Low    | 🔥🔥            | CommonUI compatible   |
| **Settings Manager** | Video/Audio/Controls persistence       | Low    | 🔥🔥            | DataAsset configs     |
| **Loading Screen**   | Async level + widget                   | Low    | 🔥             | Transitions           |
| **Simple Inventory** | Grid/List, DataAsset items             | Medium | 🔥🔥            | Basic proto system    |

---

## Stride Wheel Innovation

### Concept

Instead of AnimNotify-based footsteps (requires animation setup):

**Stride Wheel** = procedural footstep trigger based on distance traveled.

```
Setup (< 2 min):
1. Add StrideWheelComponent
2. Set StepInterval (e.g., 80 units)
3. Assign Sound Cues (Left/Right)
4. Done — footsteps play on movement
```

### Technical Design

```cpp
UCLASS()
class UStrideWheelComponent : public UActorComponent {
    // Stride settings
    UPROPERTY(EditAnywhere)
    float StepInterval = 80.0f;
    
    UPROPERTY(EditAnywhere)
    TArray<FStrideWheelEntry> StrideWheels; // Support 1-3 wheels
    
    // Each wheel can be: Front, Rear, Custom
    // Useful for quadrupeds (Wheel 1: Front, Wheel 2: Rear with delay)
};
```

### Advantages

- ✅ No AnimNotify setup required
- ✅ Works with any animation
- ✅ Speed-based cadence (auto-adjusts)
- ✅ Quadruped support (multiple wheels)
- ✅ Blueprint API for sync

---

## Business Model

### Pricing Strategy

| Tier                | Price          | Target         |
| ------------------- | -------------- | -------------- |
| **Single Module**   | 5€             | Try before buy |
| **Mini Bundle (4)** | 15€ (25% off)  | Specific needs |
| **Full Pack (12+)** | 60€ (50%+ off) | Best value     |

### Revenue Projection (Conservative)

**Assumptions**:
- 12 modules in pack
- 50 pack sales/month @ 60€ = 3000€
- 100 single module sales/month @ 5€ = 500€
- **Monthly**: ~3500€

**Break-even timeline**: 2-3 months after launch

### Fab Considerations

- Personal license tier (< $100K revenue): Standard price
- Professional license: Could charge 2x for studios
- Epic takes 12% cut

---

## Implementation Roadmap

### Phase 1 — MVP Pack (G2 Target: Mai 2026)

**Modules** (4 minimum):
1. ⭐ Footstep System (Stride Wheel + AnimNotify)
2. ⭐ Ambience System
3. ⭐ Menu System (new creation)
4. ⭐ Settings Manager (new creation)

**Timeline**: 8-10 weeks
- Weeks 1-3: Footstep + Ambience (extract)
- Weeks 4-6: Menu + Settings (create)
- Weeks 7-8: Polish, documentation, demo
- Weeks 9-10: Submission + listing

### Phase 2 — Expansion (Q3 2026)

**Add Modules** (4 more):
5. Survival Stats
6. Progression System
7. Save System
8. Input Rebinding

### Phase 3 — Full Pack (Q4 2026)

**Complete** (12 modules):
9. Loading Screen
10. Simple Inventory
11. Species Config
12. Camera Framework

---

## Folder Structure (L2 → L3)

```
L2_Design/
└── ProtoReady_Pack/
    ├── Pack_Vision.md              # This conceptual doc
    ├── Shared_Standards.md         # Naming, UX, documentation
    └── Modules/
        ├── M01_FootstepSystem/
        │   ├── Architecture.md     # Design
        │   └── StrideWheel_Design.md
        ├── M02_AmbienceSystem/
        ├── M03_MenuSystem/
        ├── M04_SettingsManager/
        └── ...

L3_Execution/
└── Plans/
    └── ProtoReady_Pack/
        ├── Plan_Phase1_MVP.md
        ├── Plan_Module_01_Footsteps.md
        └── ...
```

---

## Decision Required

### Option A — Full Vision First (Recommended)
1. Create `L2_Design/ProtoReady_Pack/Pack_Vision.md` (formalize this report)
2. Architect creates `Shared_Standards.md`
3. Then design modules one by one (Footsteps first)

**Pros**: Consistency, clear direction  
**Cons**: 1-2 days before coding

### Option B — Start Module 1 Immediately
1. Jump to Footstep System design + implementation
2. Define pack standards as we go

**Pros**: Faster to code  
**Cons**: Risk of inconsistency, rework later

### Option C — Parallel Tracks
1. Architect: Footstep System design
2. Intendant: Finalize pack vision document
3. Merge before implementation

**Pros**: Balanced  
**Cons**: Coordination overhead

---

## Recommendation

**Option A** — Spend 1-2 hours finalizing Pack Vision, then Architect designs Module 1 (Footsteps with Stride Wheel).

**Justification**:
- User_Profile.md: "Architecture First" preference
- Developpement_Personnel.md: "Commencer avec cadre clair, éviter éparpillement"
- Pack needs consistent UX across modules (define now, not later)

---

## Action Items

1. **Human Validation** — Approve Proto Ready Pack concept
2. **DEV.Architect** — Create:
   - `L2_Design/ProtoReady_Pack/Pack_Vision.md`
   - `L2_Design/ProtoReady_Pack/Shared_Standards.md`
   - `L2_Design/ProtoReady_Pack/Modules/M01_FootstepSystem/Architecture.md`
3. **DEV.Planner** — Create Phase 1 implementation plan

---

*Report generated by ACC.Intendant*  
*Human validation required before delegation.*
