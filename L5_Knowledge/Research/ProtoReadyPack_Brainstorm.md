# Proto Ready Pack — Brainstorm

> Document de capture d'idées. Pas de filtre, pas de validation.
> Ajouter librement, trier plus tard.

---

## Idées Assets — À Explorer

A. Assets procéduraux simples/easy to setup/help au dévelpppement procédural pour LD.
### 1.🌿 Titan Root Procedural System
**Source**: Apex Primal (existant) , prioriser.
**Concept**: BP/Actor avec spline + instanciation le long du mesh  
**Améliorations possibles**:
- Séparation en 1-2 branches (vrai système arborescent)
- Placement via socket, surface projection, ou direct
- Noise/variation controls
- Auto-taper + per-point width scaling
- ISMC pour optimisation

**Effort estimé**: Low-Medium (extraction + polish)  
**Marché**: World building tools (haute demande)

2. Arbre procédural/arbre géant procédural type banyan tree pour compléter les titan root procédural system et en faire un asset plus cher.
3.  Autres idées simple comme titan root.. (nuages ? pierres, etcs.. ?)

---

B. UI
### 🎮 1. Système de Menu Data-Driven 
**Source**: Nouvelle création  
**Concept**: Windows/panels générés via DataAssets  
**Features potentielles**:
- Blueprint cascade (parent → enfants)
- Blueprint API ultra simple & intuitif
- Transitions fluides
- Thèmes custom (DataAsset)
- Multi-résolution


**Effort estimé**: Medium  
**Marché**: UI kits (haute demande)

2. MENU avec matériaux spéciaux, easy to change/modify. HUD & barres de vies etcs avec matériaux etc. Easy api blueprint implementation, CPP back bone. etc..


---

### 🤖 Framework IA Modulaire (pas prioritaire)
**Source**: Nouvelle création  
**Concept**: Comportements plug-and-play (patrouille, poursuite, attaque, fuite)  
**Features potentielles**:
- Config via DataAssets
- Perception (vue, ouïe)
- GOAP simple
- Support multijoueur (replication)

**Effort estimé**: High  
**Marché**: AI/NPC (demande croissante)

---

### 🌐 Kit Multijoueur Rapide
**Source**: Nouvelle création + expertise netcode  
**Concept**: Abstraction de la replication complexe  
**Modules**:
- Lobby/sessions
- Matchmaking local/P2P
- Syncro d'état simplifiée
- Chat + scoreboard
- Exemple CTF

**Effort estimé**: High  
**Marché**: Multiplayer frameworks (croissant)

---

### 🏗️ Générateur de Niveaux Procédural (pas prioritaire, ce sont des domaines que je n'ai pas assez explorer.)
**Source**: Nouvelle création  
**Concept**: Création rapide donjons/bâtiments/terrains  
**Features**:
- Layout grilles, pièces, couloirs
- Placement assets auto (portes, mobilier)
- Compatible navmesh
- Config via DataAssets

**Effort estimé**: Very High  
**Marché**: World tools (best-sellers)

---

### 🌦️ Système Météo + Cycle Jour/Nuit (oui, potentiel de couplage avec Ambiance System)
**Source**: Nouvelle création ou extension Ambience  
**Concept**: Météo dynamique clés en main  
**Features**:
- Pluie, neige, brouillard
- Cycle jour/nuit paramétrable
- Profils météo (DataAssets)
- Intégration sky-sphere + post-process

**Effort estimé**: Medium-High  
**Marché**: Haute demande (peu de solutions complètes)

---

### 📷 Gestion Avancée des Caméras (fais partie nativement d'un systeme  species)
**Source**: Apex (LMSpeciesCameraData) ou nouvelle  
**Concept**: Comportements caméra pré-configurés  
**Features**:
- Profils TPS, FPS, iso, free-look
- Transitions fluides
- Anti-collision murs
- Zoom progressif, shake

**Effort estimé**: Medium  
**Marché**: Utilitaire prototype (demandé)

---

### 📊 Outils Analytics/Télémétrie
**Source**: Apex (TelemetryComponent) ou nouvelle  
**Concept**: Stats de jeu + logs in-editor et runtime  
**Features**:
- Suivi événements
- Dashboard visualisation
- Export CSV/JSON

**Effort estimé**: Low-Medium  
**Marché**: Data-driven devs (niche mais valorisé)

---

### 🖥️ UI/UX Réactives Data-Driven
**Source**: Nouvelle création  
**Concept**: Menus, HUD, inventaires auto-générés  
**Features**:
- Drag-and-drop
- Responsive multi-résolution
- Thèmes custom
- Liaison DataTables/Assets

**Effort estimé**: Medium-High  
**Marché**: UI kits (haute demande, différenciation possible)

---

### 🥽 Framework VR/AR Basique (non pas mon domaine pour le moment)
**Source**: Nouvelle création  
**Concept**: Base pour prototypes VR/AR  
**Features**:
- Gestion casque/contrôleurs
- Interactions raycast/grab
- Widgets 3D

**Effort estimé**: High  
**Marché**: Niche croissante

---

### 👣 Stride Wheel Footstep System
**Source**: Innovation + Apex base  
**Concept**: Footsteps sans AnimNotify  
**Features**:
- Distance-based triggers
- 1-3 wheels (quadrupède)
- Blueprint API sync
- Setup < 2 min

**Effort estimé**: Low  
**Marché**: Audio (haute demande)

---

## Catégories Priorisées (Marché 2024-2025)

| Catégorie               | Demande        | Mes Idées Correspondantes      |
| ----------------------- | -------------- | ------------------------------ |
| **Audio dynamique**     | 🔥🔥🔥            | Stride Wheel, Ambience         |
| **UI Kits**             | 🔥🔥🔥            | Menu Data-Driven, UI Réactives |
| **Gameplay Frameworks** | 🔥🔥             | Survival (Apex), Progression   |
| **World Tools**         | 🔥🔥🔥            | Titan Root, Générateur Niveaux |
| **Multiplayer**         | 🔥🔥 (croissant) | Kit Multijoueur                |
| **AI/NPC**              | 🔥🔥 (croissant) | Framework IA Modulaire         |

---

## Notes Libres

- **Principe "Proto Ready"**: Setup < 10 min, data-driven, modular
- **Business model**: 5€/module, 60€ pack complet (12+ modules)
- **Mix**: Extractions Apex + Créations nouvelles
- **Priorité G2**: 2-4 modules pour Mai 2026

---

*Document de brainstorm — Ajouter librement*
