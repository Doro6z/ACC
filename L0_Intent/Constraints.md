---
type: constraints
status: active
locked: true
created: 2026-01-18
---

# Contraintes

> Non-négociables techniques. Réalité infrastructure.
> Ce document définit les paramètres obligatoires à renseigner pour toute instance du workflow.

## 1. Contraintes de principe

Ces règles s’appliquent à toute utilisation du système, indépendamment du contexte.

- Le système est conçu pour adresser des problématiques techniques complexes,
  où la structure, la performance et la maintenabilité sont des critères déterminants.
- Les décisions engageant la stratégie ou l’architecture suivent un processus de validation explicite et restent sous le contrôle de l'utilisateur.
- Toute action agentique doit être traçable et reproductible.

## 2. Environnement technique

### Moteur & Code

- **Unreal Engine** : UE 5.5+ (5.7) (Build Source si nécessaire, target latest stable)
- **Langage** : C++20, Blueprints
- **Netcode** : Replication-first
- **Style** : Coding standards Unreal officiels

### Outils & Infra

- **IDE principal** : Antigravity (VS Code agentique)
- **IDE secondaire** : Rider
- **Version Control** : Git + LFS
-  Production de contenu :
  - DCC traditionnels (Blender, Pro Tools..)
  - Génération IA (images, textures, concepts, sons, vidéos)
  - Références externes (ArtStation, benchmarks, research)

### Configuration hardware

- **CPU** : Intel Core i7-9700K @ 3.60GHz (8 cores / 8 threads)
- **GPU** : NVIDIA GeForce GTX 1660 SUPER (6GB GDDR6)
- **RAM** : 32 Go DDR4 (4x 8Go)
- **Carte Mère** : ASUS ROG STRIX Z390-H GAMING
- **Stockage** :
    - Crucial MX500 1TB SSD (système + projets UE)
    - DREVO X1 120GB SSD
    - WD Blue 1TB HDD (archives)
- **OS** : Windows 10 Professionnel

## 3. Règles Agentiques 

## IA/Agentique

- **Plateforme Agent** : Antigravity (Google Deepmind)
- **Règles d'Engagement** : 
	- Lecture obligatoire de L0 avant toute tâche.
	- Interdiction de modifier les documents verrouillés.
	- Usage strict des templates.
	- Obligation de signaler toute modification transversale.
	- Toute demande impliquant une implémentation rapide, partielle ou non conforme aux standards doit être explicitement signalée.
		- Les solutions dites "Quick & Dirty" sont autorisées uniquement si :
		  - elles sont identifiées comme telles,
		  - leur dette est documentée,
		  - et un plan de résolution est associé.

---

*🔒 Les agents DOIVENT lire avant tout travail L2/L3.*
