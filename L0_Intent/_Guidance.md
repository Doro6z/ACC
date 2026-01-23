---
type: guidance
scope: L0
product: Agentic Command Center
---

# Guide de Remplissage — L0_Intent

> Instructions pour initialiser votre système. Ce guide s'applique à **toute instance** du système, quel que soit votre projet.

---

## 🎯 Objectif de L0_Intent

L0_Intent définit **ce qui ne change jamais** dans votre système. Si vous changez ces éléments fondamentaux, vous créez un **nouveau système**, pas une évolution.

**Analogie** : L0 est la fondation d'un bâtiment. On ne la modifie pas, on construit dessus (L1, L2...).

---

## 📄 Mission.md — Définir l'ADN du Système

### 1. Raison d'Être (Pourquoi ce système existe)

**Question** : Quel est le **but fondamental** de ce système ?

**Test de validité** :
- Est-ce que cette raison resterait vraie dans 5 ans ?
- Est-ce centré sur le **système** (pas sur vos objectifs personnels) ?

**Exemple** :
> "Fournir un cadre structurel pour livrer des projets technologiques complexes avec un standard AAA, indépendamment des ressources humaines disponibles."

**⚠️ Erreur courante** : Confondre la raison d'être du système avec vos objectifs de carrière. Vos objectifs vont dans L1_Strategy.
NB : L'objectif du système peut être un objectif personnel. 
L0_Intent/Missions et /Constraints ne doit pas être basé sur des objectifs opérationnels de court terme. 
Les objectifs précis sont définis au Layer 1 (Goals & Roadmap)
Cette structure est importante pour l'éxecution des Rules & Workflow de vos futurs Agents. /Lω_Agentic

---

### 2. Valeurs Fondamentales (Comment le système fonctionne)

**Question** : Quels **principes immuables** guident toutes les décisions ?

**Format attendu** : 6-8 valeurs maximum, numérotées, avec une description de 2-3 lignes chacune.

**Structure d'une valeur** :
```markdown
### N. Nom de la Valeur
[2-3 lignes expliquant ce que cela signifie concrètement]
```

**Test de validité** :
- Si deux valeurs entrent en conflit, pouvez-vous dire laquelle gagne ?
- Sont-elles **prescriptives** (elles dictent des actions) ?

**Exemples de valeurs solides** :
- Architecture First
- Agentic Native
- Décision Responsable
- Réalisme Opérationnel

**⚠️ Erreur courante** : Lister des aspirations ("Excellence") sans dire ce que ça implique concrètement.

---

### 3. Lignes Rouges (Ce qui est interdit)

**Question** : Qu'est-ce que vous refusez de faire, **sans exception** ? / Que le système ne doit pas faire / n'est pas prévu.

**Format attendu** : 4-6 interdictions maximum, formulées en "Pas de..."

**Test de la ligne rouge** : Pouvez-vous imaginer une situation où vous la violeriez "pour une bonne raison" ? Si oui, ce n'est pas une vraie ligne rouge.

**Structure d'une ligne rouge** :
```markdown
- **Pas de [Comportement]** : [Explication courte]
```

**Exemples** :
- Pas de "Quick & Dirty" : Interdiction d'implémenter sans phase de Design validée.
- Pas d'Hallucination : Les agents ne décident jamais des choix stratégiques seuls.

**⚠️ Erreur courante** : Pas d'exceptions ("sauf si urgence"). Les lignes rouges sont absolues.

---

## 🔒 Constraints.md — Définir les Limites Techniques

### 1. Contraintes de Principe (Invariants)

**Question** : Quelles **règles architecturales** s'appliquent à tous vos projets, quel que soit le contexte ?

**Format attendu** : bullet points.

**Exemples** :
- Le développement est orienté moteur temps réel et code natif.
- L'architecture est pensée extensible et compatible multijoueur dès l'origine.
- Les décisions stratégiques restent sous contrôle humain.

**Test de validité** : Ces règles sont-elles vraies même si vous changez de projet/technologie ?

---

### 2. Environnement Technique (Configuration utilisateur)

**Question** : Quels sont les **outils et technologies** que vous utilisez obligatoirement ?

**Sections obligatoires** :

#### Moteur & Code
- Version du moteur (ex: Unreal Engine 5.5+)
- Langage principal (ex: C++ 20)
- Standards de codage

#### Outils & Infrastructure
- IDE principal
- IDE secondaire (si applicable)
- Système de version (ex: Git + LFS)
- Outils de création d'assets

#### Configuration Matérielle
- CPU
- GPU
- RAM
- Stockage (préciser quel disque pour les projets)
- OS

**⚠️ Note importante** : Cette config est une "référence", pas une contrainte bloquante. Le système peut fonctionner ailleurs, mais il est optimisé pour cette config.

**Test de validité** : Si vous changez de PC, devez-vous mettre à jour ces infos ? Oui, car les agents doivent connaître vos limites matérielles.

---

### 3. Règles Agentiques (Comment l'IA doit se comporter)

**Question** : Quelles sont les **règles d'engagement** pour les agents IA ?

**Sections obligatoires** :

#### Plateforme
- Nom de la plateforme (ex: Antigravity)

#### Règles d'Engagement (5-7 règles)
- Lecture obligatoire de L0 avant toute tâche
- Interdiction de modifier les documents verrouillés
- Usage strict des templates
- Obligation de signaler toute modification transversale
- Détection du contexte et usage du persona adapté

**Test de validité** : Un nouvel agent pourrait-il comprendre comment se comporter en lisant ces règles ?

---

## ✅ Checklist de Validation Finale

### Avant de verrouiller (`locked: true`)

**Mission.md** :
- [ ] Raison d'être en 1-2 phrases, centrée sur le système (pas vous)
- [ ] 6-8 valeurs avec descriptions concrètes
- [ ] 4-6 lignes rouges absolues (pas d'exceptions)
- [ ] Tout resterait vrai dans 5 ans
- [ ] Compréhensible par quelqu'un d'externe

**Constraints.md** :
- [ ] Contraintes de principe listées (3-5)
- [ ] Version moteur/langage spécifiée
- [ ] Outils et IDE documentés
- [ ] Configuration matérielle complète
- [ ] Règles agentiques claires (5-7)

---

## 🔄 Quand Modifier L0 ?

| Situation                            | Action                     | Raison                    |
| ------------------------------------ | -------------------------- | ------------------------- |
| Correction typo/grammaire            | ✅ Modifier directement     | Pas de changement de sens |
| Clarification d'une valeur existante | ✅ Modifier (avec prudence) | Si le sens reste le même  |
| Ajout d'une nouvelle valeur          | ⚠️ Réfléchir longuement     | Cela change l'ADN         |
| Changement de raison d'être          | ❌ Créer nouveau système    | C'est une refonte totale  |
| Pivot de projet/activité             | ❌ Créer nouveau système    | Archiver l'ancien vault   |

**Règle d'or** : Si vous hésitez, c'est que c'est probablement une modification L1 (Strategy), pas L0.

---

## 📚 Ressources & Sources

- [Aha.io — Product Vision Best Practices](https://aha.io)
- [Indie Game Academy — GDD Templates](https://indiegameacademy.com)
- [TechTarget — Architecture Decision Records](https://techtarget.com)
- [Asana — Mission Statement Guide](https://asana.com)

---

## 🏷️ Nom du Produit

Ce système s'appelle : **Agentic Command Center** (ACC)

Alternative : **Obsidian Project Command System** (OPCS)

---

*🔒 L0 = Fondation. Construisez dessus (L1-L6), ne creusez pas dedans.*
