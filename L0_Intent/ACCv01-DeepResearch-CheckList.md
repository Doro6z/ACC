Ce document est Human-Only. Sers de réference pour la complétition du setup ACC.



Niveau	Rôle
GEMINI.md	Sécurité globale (bootloader)
AI_Guard.md	Contrats par layer
Workflows	Intention explicite (quand déclenché)
Personas	Style et posture



# Deep Research — Agentic Command Center (Antigravity + Obsidian)

Date: 2026-01-19  
Statut: Research (à promouvoir partiellement en Reference après validation)

## 0. Résumé exécutable

Le système tient si (et seulement si) tu appliques ces principes :

1. **Séparation “Plan → Exécution → Validation”** (ne jamais fusionner).
    
2. **Least Privilege / Permissions minimales** par fonction et par layer (Read/Write/Propose) + STOP conditions.
    
3. **Règles contractuelles hors pédagogie** : `AI_Guard.md` normatif en anglais, `_Guidance.md` humain.
    
4. **Observabilité / audit trail** : tout changement “qui compte” doit être traçable (ADR, changelog, logs d’opérations).
    

Conséquence : tes workflows `/phase-*` doivent être un **pipeline à responsabilités distinctes**, pas une commande “magique” qui fait tout.

---

## 1. Taxonomie des fonctions nécessaires (sans noms)

### Bloc A — Gouvernance / Intégrité du système (obligatoire)

Objectif : empêcher la dérive du vault + empêcher l’agent de casser les locks.

- **Function: System Governance (Guard/Audit)**  
    Vérifie structure, locks, présence des guards, cohérence inter-layer, signale les violations, ne modifie rien.
    
- **Function: Policy & Compliance (Rules Steward)**  
    Propose des évolutions de règles (Lω), sans jamais écrire Lω. Produit des diffs/propositions.
    

Pourquoi c’est indispensable : l’absence de “guard” mène aux modifications silencieuses et au drift.

---

### Bloc B — Production (coding pipeline) (obligatoire)

Tu as déjà ce pattern en version artisanale (/phase-plan etc.). Il faut le stabiliser.

- **Function: Brainstorm / Discovery**  
    Génère options, features, alternatives, risques. Aucun code final. Pas de décisions.
    
- **Function: Technical Planning**  
    Transforme un brief en plan actionnable, découpe, définit critères de succès, dépendances, scope. (Plan-only)
    
- **Function: Execution (Implement)**  
    Écrit/édite L3 + code (dans UE), mais uniquement à partir d’un plan validé. Permissions limitées.
    
- **Function: Review / Validation**  
    Vérifie conformité (L0.5 constraints, L2 design, standards), tests, checklists, rejette/valide.
    

Principe “plan then act” et séparation plan/exécution sont considérés comme bonnes pratiques émergentes.

---

### Bloc C — Documentation & Packaging (très recommandé si Fab/Freelance)

- **Function: Documentation & Release Packaging**  
    Produit README, guides d’intégration, exemples, changelog, structure de démo, packaging Fab.
    

---

### Bloc D — Recherche & veille (utile mais cadré)

- **Function: Research**  
    Produit des docs “Research” dans L5, propose une synthèse “Reference/Validated”, TTL, sources.
- **Function: veille actualités**  
    Veille sur les nouveautés Unreal Engine, tech, coding, AI, avancé Agentic, nouveaux IDE, nouveaux outils, nouveaux langages, nouveaux frameworks, nouveaux paradigmes, etc, en pertinence avec le profil utilisateur et produits des rapports de veilles.

---

### Bloc E — Opérations (optionnel au départ)

- **Function: Ops / Task Orchestration**  
    Crée/maintient L4 tasks, états, sprints, daily logs, mais sans jamais pousser de stratégie.
    

---

## 2. Permission model (par fonction → par layer)

Notation : R=Read, W=Write, P=Propose, -=No access

### A) System Governance (Guard/Audit)

- Z_INBOX: R
    
- L0: R
    
- L1: R
    
- L2: R
    
- L3: R
    
- L4: R
    
- L5: R
    
- L6: R
    
- Lω: R (lecture des règles)
    
- Z_ARCHIVE: R  
    **STOP conditions** : guard manquant, lock absent, contradiction critique détectée.
    

### B) Brainstorm / Discovery

- L0: R
    
- L1: R
    
- L2: R (lecture seulement)
    
- L5: W (Exploration/Research)
    
- L6: R/W (capture non-binding)
    
- L3/L4: -
    
- Lω: R  
    **STOP** : si on lui demande de “décider”, “implémenter”, “modifier L1/L2”.
    

### C) Technical Planning

- L0: R
    
- L1: R
    
- L2: R (si design existe) / P (si manque : propose design)
    
- L4: W (création tasks + états)
    
- L3: P (propose specs)
    
- Lω: R  
    **STOP** : plan sans références (pas de L0/L1, ou pas de design quand requis).
    

### D) Execution (Implement)

- L0: R
    
- L1: R
    
- L2: R (obligatoire)
    
- L3: W
    
- L4: W (progress tasks)
    
- L5: W (snippets / notes techniques)
    
- Lω: R  
    **STOP** : pas de plan validé / pas de design / conflit L3↔L2.
    

### E) Review / Validation

- L0: R
    
- L1: R
    
- L2: R
    
- L3: R
    
- L4: W (set validated/rejected)
    
- L5: P (propose consolidation)
    
- Lω: R  
    **STOP** : si exigences non testées / pas de preuves / pas de traçabilité.
    

### F) Documentation & Release Packaging

- L0/L1/L2: R
    
- L3: R/W (docs, guides, specs, examples)
    
- L4: W (checklists release)
    
- L5: W (reference)
    
- Lω: R  
    **STOP** : release sans demo / sans guide / sans changelog.
    

Ces découpages suivent des recommandations récurrentes : frontières claires, séparation décision/outils, observabilité.

---

## 3. Bootstrap plan (ordre de création optimal)

### Phase 0 — Sécuriser le système (avant toute prod)

1. **System Governance (Guard/Audit)**
    
2. **Minimum viable AI_Guards** (L0→L4, au moins)
    
3. **Workflow “Read chain + STOP”** (commande Antigravity)
    

Raison : sans guard, tout le reste dérive et tu perds la “source of truth”.

### Phase 1 — Démarrer le pipeline de production (coding)

4. **Technical Planning**
    
5. **Execution (Implement)**
    
6. **Review/Validation**
    

Raison : “plan-and-execute” + validation réduit erreurs, hallucinations et code jetable.

### Phase 2 — Monétisation / qualité pro

7. **Documentation & Release Packaging**
    
8. **Research / Knowledge Curation** (pour stabiliser les playbooks)
    

---

## 4. Minimum viable AI_Guards (L0, L1, L2, L3, L4)

Objectif : sécuriser dès maintenant les couches où une IA peut “casser” ton système.

### L0_Intent/AI_Guard.md (déjà)

- Read YES / Write NO / Propose NO
    
- MUST read before any task
    
- STOP if missing/unlocked
    

### L1_Strategy/AI_Guard.md (fait)

- Read YES / Write NO / Propose YES
    
- append-only / ADR only
    

### L2_Design/AI_Guard.md (minimum viable)

- Read: YES
    
- Write: NO
    
- Propose: YES  
    Rules:
    
- MUST reference L1 decision if changing architecture
    
- MUST write proposals as new files (draft) or in `_Changelog.md` suggestion block (human validates)
    
- STOP if asked to “silently update architecture”
    

### L3_Technical/AI_Guard.md (minimum viable)

- Read: YES
    
- Write: YES (scope limited)
    
- Propose: YES  
    Rules:
    
- MUST reference L2 design (`design_ref`)
    
- MUST NOT contradict L2
    
- MUST log cross-file impacts
    
- STOP on conflict flag
    

### L4_Operations/AI_Guard.md (minimum viable)

- Read: YES
    
- Write: YES
    
- Propose: YES  
    Rules:
    
- MUST link every task to L2 or L3
    
- MUST NOT create tasks from L6 (non-binding) without human promotion
    
- MUST maintain task states (todo/in-progress/done/validated/rejected)
    
- STOP if “orphan task”
    

Ces guards implémentent : frontières, least privilege, auditability.

---

## 5. Anti-patterns (pièges majeurs à éviter)

1. **Super-agent monolithique** (“fait tout”)  
    → mélange plan/exécution/validation = drift + erreurs non détectées.
    
2. **Modifications silencieuses**  
    → l’agent “améliore” Goals/Roadmap/Design sans ADR/validation. C’est une destruction lente de la vérité.
    
3. **Policy statique unique type GEMINI.md**  
    → devient trop gros, incohérent, non contextualisé, et incontrôlable.
    
4. **Absence de kill-switch (STOP)**  
    → boucle infinie, actions dangereuses, corruption du vault.
    
5. **Pas d’audit trail**  
    → impossible de comprendre “pourquoi c’est comme ça”, impossible de vendre/transmettre sérieusement.
    
6. **Confusion guidance/guard**  
    → l’agent prend un tuto comme contrat, ou inversement.
    

---

## 6. Intégration Antigravity : mapping `/phase-*` → fonctions

Tu as déjà le bon pattern : une commande = un workflow = lecture contexte + persona + production fichier.

### Recommandation : chaque `/phase-*` doit mapper **UNE** fonction principale

Exemples (sans noms d’agents) :

- `/phase-guard` → System Governance (audit + STOP conditions)
    
- `/phase-brainstorm` → Brainstorm/Discovery (output L5 Exploration/Research)
    
- `/phase-plan` → Technical Planning (output L4 tasks + plan md)
    
- `/phase-implement` → Execution (output code + L3 updates)
    
- `/phase-review` → Validation (output decision: validated/rejected + checklist)
    

Chaque workflow doit :

1. lire L0
    
2. lire `AI_Guard.md` du layer qu’il va toucher
    
3. produire un output **dans le layer autorisé**
    
4. STOP si violation
    

Ça rejoint les meilleures pratiques “instructions claires + structure + itération test-driven” pour réduire erreurs.

---

## 7. Moderniser “GEMINI.md global rules” → système distribué

### Problème d’un GEMINI.md monolithique

- trop large, trop vague
    
- pas de séparation par layer
    
- pas de permissions enforceables
    
- dur à maintenir
    

### Remplacement proposé (distribué)

- **L0_Intent/Constraints.md** : invariants courts (read chain, language policy, locks)
    
- **Layer AI_Guard.md** : permissions + STOP conditions locales
    
- **Lω_Agentic/Rules/** : règles transversales (conflict protocol, validation protocol, logging policy)
    
- **Workflows Antigravity** : orchestration (quelle fonction, quel output)
    

C’est plus robuste car le contexte “local” (layer) réduit les ambiguïtés.