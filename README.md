# Hwei Item Damage Calculator

Calculate **real damage and DPS** of individual items vs specific MR/HP targets.

## 🎯 Purpose

**Item-by-item damage analysis**:
- ✅ **1-item damage** vs 60 MR enemy: 1,940 
- ✅ **2-item damage** vs 60 MR enemy: 2,748 (+808)
- ✅ **3-item damage** vs 60 MR enemy: 3,456 (+708)
- ✅ **Item passive effects** (Liandry's burn, Shadowflame crit, etc.)
- ✅ **Magic penetration** (% pen → flat pen → actual damage)

## ⚡ Quick Start

1. **Download**: `core_items.csv`
2. **Follow**: `SETUP_GUIDE_SIMPLIFIED.md` (30 minutes)
3. **Calculate**: Real damage per item vs any target

## 🔥 Core Items (Patch 25.11)

| Item | Cost | AP | Passive | vs 60 MR Enemy |
|------|------|----|---------|----- |
| **Shadowflame** | 3,200g | 110 | Crit vs <40% HP | 1,940 dmg |
| **Rabadon's Deathcap** | 3,500g | 130 | +30% AP | 2,748 dmg |
| **Void Staff** | 3,000g | 95 | 40% Magic Pen | 3,456 dmg |
| **Liandry's Torment** | 3,000g | 60 | Max HP burn + 6% amp | 4,112 dmg |
| **Horizon Focus** | 2,800g | 115 | Long range bonus | 4,567 dmg |
| **Cryptbloom** | 3,000g | 75 | 30% Magic Pen + heal | 4,891 dmg |

## 🧮 Magic Penetration Formula

```
Step 1: Apply % Magic Pen (multiplicative)
Step 2: Apply Flat Magic Pen (subtractive)  
Step 3: Calculate damage = Base × 100/(100 + Effective_MR)
```

**Example**: Void Staff + Cryptbloom vs 100 MR
1. % Pen: 100 × (1-0.4) × (1-0.3) = **42 MR remaining**
2. Flat Pen: 42 - 0 = **42 effective MR**  
3. Damage: 100/(100+42) = **70.4% damage dealt**

## 📁 Files

```
hwei-item-calculator/
├── core_items.csv              # 6 essential items + stats
├── SETUP_GUIDE_SIMPLIFIED.md   # 30-min setup guide
└── README.md                   # This file
```

## 🎮 Usage

**Set target**: 60 MR, 2000 HP enemy  
**Input items**: Shadowflame → Rabadon's → Void Staff → Liandry's  
**See progression**:
- 1 item: 1,940 damage
- 2 items: 2,748 damage (+808)
- 3 items: 3,456 damage (+708)  
- 4 items: 4,112 damage (+656)

**Result**: Know exactly which item gives biggest damage spike!

## 🔗 Links

- **Repository**: [github.com/renbkna/hwei-item-calculator](https://github.com/renbkna/hwei-item-calculator)
- **Author**: renbkna

---

**Transform from guessing to calculating real item damage!** ⚡