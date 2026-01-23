# Naming Conventions — ACC System

**Status**: Active  
**Created**: 2026-01-22  
**Authority**: Lω (Governance)

---

## Document Types & Prefixes

| Type                 | Prefix     | Location               | Example                                       |
| -------------------- | ---------- | ---------------------- | --------------------------------------------- |
| **Plans**            | `[Plan]`   | L3_Execution/Plans/    | `[Plan]_Master_2026-01-22_1345.md`            |
| **Analysis Reports** | `[Report]` | L4_Operations/Reports/ | `[Report]_Market_Analysis_2026-01-22_1240.md` |
| **Activity Reports** | `[RPA]`    | L4_Operations/Reports/ | `[RPA]_System_State_2026-01-21_1000.md`       |
| **Research**         | `[Rsch]`   | L5_Knowledge/Research/ | `[Rsch]_Fab_Marketplace_2026-01-22.md`        |
| **Brainstorm**       | `[Brnst]`  | L5_Knowledge/Research/ | `[Brnst]_ProtoReady_Ideas_2026-01-22.md`      |
| **ADR**              | `ADR`      | L1_Strategy/ADR/       | `ADR_2026-01-21_Document_Creation.md`         |
| **Architecture**     | `[Arch]`   | L2_Design/             | `[Arch]_AudioSystem_2026-01-22.md`            |

---

## Format Structure

**General Pattern**: `[Type]_<DescriptiveName>_YYYY-MM-DD_HHMM.md`

**Rules**:
- **Type prefix**: In brackets, ALL CAPS inside (e.g., `[Plan]`, `[Report]`)
- **Descriptive name**: CamelCase or underscores, no spaces
- **Date**: YYYY-MM-DD (ISO 8601)
- **Time**: HHMM (24h format, optional for some types)
- **Extension**: Always `.md`

**Examples**:
- ✅ `[Plan]_ProtoReadyPack_Master_2026-01-22_1345.md`
- ✅ `[Report]_Market_Strategic_Options_2026-01-22_1250.md`
- ✅ `[Brnst]_ProtoReadyPack_2026-01-22.md`
- ❌ `Plan_2026-01-22_ProtoReady.md` (old format)

---

## Project Hierarchies

### L3 Plans

```
L3_Technical/Plans/
└── <ProjectName>/
    ├── [Plan]_Master_<Date>.md              # Master plan du projet
    ├── <ModuleName>/
    │   ├── [Plan]_Implementation_<Date>.md
    │   ├── [Plan]_Testing_<Date>.md
    │   └── ...
    └── <AnotherModule>/
        └── ...
```

**Example**:
```
L3_Technical/Plans/
└── ProtoReadyPack/
    ├── [Plan]_Master_2026-01-22_1345.md
    ├── Module_01_StrideWheel/
    │   ├── [Plan]_Implementation_2026-01-25.md
    │   └── [Plan]_Testing_2026-02-05.md
    ├── Module_02_Ambience/
    └── Module_03_Settings/
```

---

### L2 Designs

```
L2_Design/
└── <ProjectName>/
    ├── [Arch]_Overview_<Date>.md           # Architecture globale
    ├── <ComponentName>/
    │   └── [Arch]_<Component>_<Date>.md
    └── ...
```

**Example**:
```
L2_Design/
└── ProtoReadyPack/
    ├── Pack_Vision.md                      # Documents structurels (pas de date)
    ├── Shared_Standards.md
    ├── Brainstorm.md
    └── Modules/
        ├── M01_StrideWheel/
        │   └── [Arch]_StrideWheel_2026-01-24.md
        └── M02_Ambience/
            └── [Arch]_AmbienceSystem_2026-01-25.md
```

---

### L5 Research

```
L5_Knowledge/Research/
├── [Rsch]_<Topic>_<Date>.md
├── [Brnst]_<Topic>_<Date>.md
└── <Category>/
    └── ...
```

---

### L4 Reports

**Two types** :
- `[Report]_` — Rapports d'analyse (Intendant)
- `[RPA]_` — Rapports d'activité (tracking, status)

```
L4_Operations/Reports/
├── [Report]_<Subject>_<Date>.md
├── [RPA]_<Subject>_<Date>.md
└── ...
```

---

## Special Cases

### Documents Structurels (Sans Date)

Certains documents sont des références permanentes et n'ont pas de timestamp :
- `Pack_Vision.md`
- `Shared_Standards.md`
- `README.md`
- `L0_Intent/Mission.md`
- `L1_Strategy/Goals.md`

**Règle** : Si le document est une référence vivante mise à jour régulièrement (pas un snapshot), pas de date dans le nom.

---

### ADR (Architecture Decision Records)

Format spécial : `ADR_YYYY-MM-DD_<ShortTitle>.md`

**Example**: `ADR_2026-01-21_Document_Creation_Protocol.md`

---

## Migration Legacy Files

**Anciens fichiers** (pré-2026-01-22) peuvent utiliser ancien format.  
**Nouveaux fichiers** DOIVENT utiliser nouveau format.

**Renommage progressif** : OK si besoin, mais maintenir cohérence dans nouveau travail.

---

## Enforcement

- **DEV.Planner** : DOIT utiliser nouveau format pour tous plans
- **ACC.Intendant** : DOIT utiliser nouveau format pour tous reports
- **DEV.Architect** : DOIT utiliser nouveau format pour architectures avec date
- **Humain** : Recommandé de suivre conventions pour cohérence

---

*Conventions centralisées — Référence unique*  
*Toute modification de ce document = ADR requis*
