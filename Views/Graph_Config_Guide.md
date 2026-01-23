# Graph Configuration — Filtres Recommandés

**Objectif:** Réduire bruit visuel dans Graph View, mettre en valeur contenu métier

---

## Configuration Manuelle

### Étape 1: Ajouter `kind: meta` aux fichiers structurels

Ces fichiers doivent avoir en frontmatter :
```yaml
---
kind: meta
---
```

**Fichiers à modifier (exemples):**
- Tous les `_Index.md`
- Tous les `_Guidance.md`
- Tous les `AI_Guard.md`
- `Templates/*.md` (optionnel si déjà exclus par dossier)

### Étape 2: Configurer Graph View Obsidian

**Menu:** `Settings → Graph View`

**Filters à ajouter:**
```
-kind:meta -kind:template -path:Templates
```

**Groupes par layer (couleurs):**
- L0 (Intent): Rouge `#FF0000`
- L1 (Strategy): Orange `#FFA500`
- L2 (Design): Vert `#00FF00`
- L3 (Execution): Cyan `#00FFFF`
- L4 (Operations): Bleu `#0000FF`
- L5 (Knowledge): Magenta `#FF00FF`
- Lω (Agentic): Gris `#808080`

---

## Configuration Automatique (Avancé)

**Si accès à `.obsidian/graph.json`:**

Remplacer/merger avec :
```json
{
  "collapse-filter": false,
  "search": "-kind:meta -kind:template -path:Templates",
  "showTags": false,
  "showAttachments": false,
  "hideUnresolved": true,
  "showOrphans": false,
  "collapse-color-groups": false,
  "colorGroups": [
    {
      "query": "layer:L0",
      "color": {
        "a": 1,
        "rgb": 16711680
      }
    },
    {
      "query": "layer:L1",
      "color": {
        "a": 1,
        "rgb": 16744192
      }
    },
    {
      "query": "layer:L2",
      "color": {
        "a": 1,
        "rgb": 65280
      }
    },
    {
      "query": "layer:L3",
      "color": {
        "a": 1,
        "rgb": 65535
      }
    },
    {
      "query": "layer:L4",
      "color": {
        "a": 1,
        "rgb": 255
      }
    },
    {
      "query": "layer:L5",
      "color": {
        "a": 1,
        "rgb": 16711935
      }
    },
    {
      "query": "layer:Lω",
      "color": {
        "a": 1,
        "rgb": 8421504
      }
    }
  ],
  "collapse-forces": false,
  "centerStrength": 0.5,
  "repelStrength": 10,
  "linkStrength": 1,
  "linkDistance": 250,
  "scale": 1,
  "close": false
}
```

---

## Test Rapide

Après configuration :
1. Ouvrir Graph View (`Ctrl+G` ou menu)
2. Vérifier que `_Index`, `AI_Guard`, templates ne s'affichent plus
3. Vérifier couleurs par layer (si frontmatter appliqué)
4. Ajuster filtres si nécessaire

---

*Configuration guide created: 2026-01-21*
