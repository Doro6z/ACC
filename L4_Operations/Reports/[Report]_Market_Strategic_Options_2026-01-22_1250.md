# ACC.Intendant Report — 2026-01-22_1250

## Context
- **Trigger**: User feedback — Previous analysis too self-centered
- **Objective**: Market-oriented research for marketable UE5 assets
- **Scope**: External opportunities, not limited to existing Apex systems

---

## Research Base (External)

**Sources Consultées**:
- Fab/Marketplace trends 2024-2025 (multiple sources)
- Reddit developer discussions (plugin gaps, wanted features)
- Indie developer success stories
- Plugin popularity statistics

**Key Market Data**:
- **850K+** monthly active UE5 users (October 2024)
- **31%** of game sales use Unreal Engine (up from 19% in 2023)
- **88%** revenue share for Fab sellers
- **$6K+** annual profit reported by one indie seller (pre-Fab)

---

## Market Opportunity Analysis

### 🔥 Top-Selling Categories (Market Validated)

| Category                  | Competition | Barrier to Entry | Your Fit        |
| ------------------------- | ----------- | ---------------- | --------------- |
| **Workflow/Editor Tools** | Medium      | Low-Medium       | ⭐⭐⭐⭐ Good       |
| **Gameplay Systems**      | High        | Medium           | ⭐⭐⭐⭐⭐ Excellent |
| **Environment/VFX**       | Very High   | High             | ⭐⭐ Art-heavy    |
| **Procedural Tools**      | Medium      | High             | ⭐⭐⭐ Possible    |
| **Character/Animation**   | Medium      | High             | ⭐⭐⭐ Possible    |

### 🎯 Market Gaps (Developer Requests)

**From Reddit/Forum Research**:

| Gap                                       | Demand Signal | Complexity | Your Fit |
| ----------------------------------------- | ------------- | ---------- | -------- |
| **Modular systems** (not "do-everything") | 🔥🔥🔥 High      | Medium     | ⭐⭐⭐⭐⭐    |
| **Lag compensation for movement**         | 🔥🔥🔥 High      | High       | ⭐⭐⭐⭐     |
| **Better data table management**          | 🔥🔥 Medium     | Low        | ⭐⭐⭐      |
| **In-editor task tracking**               | 🔥🔥 Medium     | Medium     | ⭐⭐       |
| **Blueprint screenshot/documentation**    | 🔥 Low         | Low        | ⭐⭐       |
| **Vehicle systems (heli, planes)**        | 🔥🔥 Medium     | High       | ⭐⭐       |
| **Audio reactivity simplified**           | 🔥 Low         | Medium     | ⭐⭐⭐      |

---

## Strategic Options

### Option A — "Proto Ready Pack" (Your Original Idea)
**What**: Modular, easy-setup systems for rapid prototyping  
**Modules**: Footsteps, Menu, Save, Settings, etc.  
**Pricing**: 5€/module, 60€ pack

**Pros**:
- ✅ Addresses "modular systems" gap
- ✅ Leverages existing Apex code
- ✅ Low entry barrier (familiar tech)
- ✅ Multiple revenue streams (modules + pack)

**Cons**:
- ⚠️ Footsteps/Menu = competitive markets
- ⚠️ May compete with free alternatives
- ⚠️ Low individual module price = volume needed

**Revenue Potential**: Medium (3-5K€/month mature)  
**Effort**: Medium (8-12 weeks for MVP pack)  
**Your Fit**: ⭐⭐⭐⭐ Good

---

### Option B — "Multiplayer Toolbox" (High Demand Gap)
**What**: Lag compensation + client prediction + network debugging tools  
**Focus**: Replication-focused toolkit

**Pros**:
- ✅ High demand, few good solutions
- ✅ Matches your expertise (replication-first)
- ✅ Technical moat (complex, hard to replicate)
- ✅ Higher price justified ($50-100)

**Cons**:
- ⚠️ High complexity
- ⚠️ Longer development time
- ⚠️ Smaller audience (multiplayer devs only)

**Revenue Potential**: High (well-priced niche)  
**Effort**: High (12-16 weeks)  
**Your Fit**: ⭐⭐⭐⭐⭐ Excellent (netcode expertise)

---

### Option C — "Procedural Animation Framework"
**What**: Data-driven animation system (spine cascade, head look-at, IK)  
**From**: Apex animation system (LMSpeciesAnimInstance)

**Pros**:
- ✅ Character rigs with animation = top sellers
- ✅ Already built in Apex
- ✅ Unique (not many procedural quad solutions)

**Cons**:
- ⚠️ Heavy skeleton dependencies
- ⚠️ Complex extraction
- ⚠️ Documentation-intensive
- ⚠️ Niche (quadrupeds)

**Revenue Potential**: Medium-High (niche but valuable)  
**Effort**: Very High (16+ weeks)  
**Your Fit**: ⭐⭐⭐ Possible but risky

---

### Option D — "Blueprint Workflow Tools"
**What**: Editor utilities (Electronic Nodes style, but different focus)  
**Examples**: Better data table UI, Blueprint documentation generator

**Pros**:
- ✅ High demand for workflow tools
- ✅ Lower complexity (editor-only)
- ✅ Quick to develop
- ✅ Recurring passive income

**Cons**:
- ⚠️ Competitive market (many free tools)
- ⚠️ Not leveraging your gameplay expertise
- ⚠️ Outside core competency

**Revenue Potential**: Low-Medium  
**Effort**: Low (4-6 weeks)  
**Your Fit**: ⭐⭐ Mismatch

---

### Option E — "Complete Survival Framework" (From Apex)
**What**: GAS-based survival system (Stamina, Hunger, Health, Progression)  
**From**: LMSurvivalComponent, LMProgressionComponent

**Pros**:
- ✅ Survival games trending
- ✅ Already built
- ✅ GAS-integrated (professional)
- ✅ Replication-ready

**Cons**:
- ⚠️ GAS dependency (complex for some users)
- ⚠️ Competition exists
- ⚠️ Medium-high polish needed

**Revenue Potential**: Medium  
**Effort**: Medium (6-8 weeks)  
**Your Fit**: ⭐⭐⭐⭐ Good

---

### Option F — "Species/Character Config Framework"
**What**: Data-driven character configuration (species switching, camera profiles, abilities)  
**From**: LMSpeciesData (451 LOC)

**Pros**:
- ✅ Unique architecture
- ✅ Data-driven = marketable concept
- ✅ Already production-tested

**Cons**:
- ⚠️ Complex extraction
- ⚠️ Many struct dependencies
- ⚠️ Long documentation

**Revenue Potential**: Medium-High (architects love this)  
**Effort**: High (10-12 weeks)  
**Your Fit**: ⭐⭐⭐⭐ Good

---

## Comparative Analysis

| Option                       | Revenue Potential | Effort    | Time to Market | Competition | Your Fit |
| ---------------------------- | ----------------- | --------- | -------------- | ----------- | -------- |
| **A - Proto Ready Pack**     | Medium            | Medium    | 8-12 weeks     | Medium-High | ⭐⭐⭐⭐     |
| **B - Multiplayer Toolbox**  | High              | High      | 12-16 weeks    | Low         | ⭐⭐⭐⭐⭐    |
| **C - Procedural Animation** | Medium-High       | Very High | 16+ weeks      | Low         | ⭐⭐⭐      |
| **D - Workflow Tools**       | Low-Medium        | Low       | 4-6 weeks      | Very High   | ⭐⭐       |
| **E - Survival Framework**   | Medium            | Medium    | 6-8 weeks      | Medium      | ⭐⭐⭐⭐     |
| **F - Species Config**       | Medium-High       | High      | 10-12 weeks    | Low         | ⭐⭐⭐⭐     |

---

## Recommendation

### For G2 (Mai 2026 — 4 months)

**Primary Path: Option A + E Combined**

**Rationale**:
1. **Proto Ready Pack** (A) gives multiple products fast
2. **Survival Framework** (E) leverages existing code
3. Both are medium effort, achievable in timeline
4. Modules from both can cross-sell

**Alternative Path: Option B (Multiplayer Toolbox)**

**Rationale**:
1. Higher revenue per unit
2. Technical moat (your replication expertise)
3. Less competition
4. But: Higher risk, longer timeline

---

### Beyond G2 (Post Mai 2026)

**Consider Option F (Species Config)** — Unique offering, less time pressure allows proper polish.

---

## Action Required

### Question 1
**Which strategic path appeals more?**
- A + E (Proto Ready + Survival) — Safe, diverse
- B (Multiplayer Toolbox) — Risky, high reward
- Other combination?

### Question 2
**For Proto Ready Pack — which modules matter most to you?**
- From Apex (extraction): Footsteps, Ambience, Survival, Progression
- New creations: Menu, Save, Settings, Loading
- Innovation: Stride Wheel

### Question 3
**Are you willing to create entirely new systems (not from Apex)?**
- This expands market fit but increases effort

---

*Report generated by ACC.Intendant*  
*External market research completed*  
*Human direction required to proceed*
