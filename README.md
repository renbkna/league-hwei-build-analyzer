# League of Legends Hwei Build Analyzer

A comprehensive Google Sheets system for analyzing Hwei item builds with **real damage calculations**, magic penetration effectiveness, and strategic build comparisons.

## 🎯 What This Does

**Beyond Simple Gold Efficiency** - This analyzer calculates:
- ✅ **Real damage vs different enemy types** (Squishy/Tanky/Ultra Tank)
- ✅ **Magic penetration effectiveness** (% pen → flat pen → actual damage)  
- ✅ **Item passive damage estimation** (Luden's, Liandry's, Shadowflame, etc.)
- ✅ **Optimal target selection** (which enemies to focus with each build)
- ✅ **Cost efficiency analysis** (damage per gold spent)

## 🚀 Quick Start (1 Hour Setup)

### **Option 1: Follow Complete Build Guide**
📖 **[BUILD_GUIDE.md](BUILD_GUIDE.md)** - Step-by-step instructions to build from scratch

### **Option 2: Use Templates**
1. Download CSV templates from `/data/` folder
2. Import into Google Sheets
3. Follow setup instructions in `/templates/`

## 📊 System Architecture

The analyzer uses **5 interconnected Google Sheets tabs**:

### 1. **Dashboard** - Main comparison interface
- Compare up to 3 builds side-by-side
- See damage vs different target types
- Automatic cost efficiency calculations

### 2. **Build Definitions** - Define Hwei builds
- Select 6 items per build using dropdowns
- Automatic damage calculations
- Magic penetration effectiveness analysis

### 3. **Items Database** - Current patch item stats
- Complete mage item database
- Gold efficiency calculations
- Passive damage estimates

### 4. **Stat Gold Values** - Official League gold values
- Updated for current patch
- Based on basic item costs

### 5. **Advanced Calculations** - Complex damage formulas
- Magic penetration order of operations
- Target-specific damage analysis

## 🧮 How Magic Penetration Works

### **Example: Void Staff + Spellslinger's vs 80 MR Target**

1. **% Magic Pen**: 45% (Void) + 10% (Spellslinger's) = **51.5% total**
2. **Apply % Pen**: 80 × (1-0.515) = **38.8 MR remaining**  
3. **Apply Flat Pen**: 38.8 - 18 (Spellslinger's) = **20.8 effective MR**
4. **Damage Multiplier**: 100/(100+20.8) = **82.8%**

Your 3000 damage combo → **2,484 actual damage**

## 📈 Sample Analysis Output

### **Standard Burst Build**:
- **Items**: Luden's → Shadowflame → Rabadon's → Void → Zhonya's → Spellslinger's
- **Total Cost**: 16,100g
- **vs Squishy (40 MR)**: 2,847 damage **(177 dmg/1000g)**
- **vs Tanky (80 MR)**: 2,234 damage **(139 dmg/1000g)**
- **vs Ultra Tank (120 MR)**: 1,756 damage **(109 dmg/1000g)**
- **Optimal Targets**: Squishy ADCs and mages

### **Tank Shredder Build**:
- **Items**: Luden's → Void → Liandry's → Rabadon's → Zhonya's → Spellslinger's  
- **Total Cost**: 16,450g
- **vs Squishy (40 MR)**: 2,654 damage **(161 dmg/1000g)**
- **vs Tanky (80 MR)**: 2,456 damage **(149 dmg/1000g)**
- **vs Ultra Tank (120 MR)**: 2,189 damage **(133 dmg/1000g)**
- **Optimal Targets**: Tanky bruisers and supports

## 🔧 Current Patch Support

**Patch 25.11** - Updated for latest item changes:
- Void Staff: 45% magic penetration (increased from 40%)
- Shadowflame: 12 flat magic penetration + crit passive
- Zhonya's Hourglass: 65 AP (reduced from 80)
- Spellslinger's Shoes: 18 flat + 10% magic penetration

## 📁 Repository Structure

```
league-hwei-build-analyzer/
├── BUILD_GUIDE.md           # Complete setup instructions
├── QUICK_UPGRADE_GUIDE.md   # Upgrade existing system
├── ADVANCED_DAMAGE_SYSTEM.md # Advanced features explanation
├── data/
│   ├── mage_items_template.csv    # Item database template
│   ├── sample_builds.csv          # Example Hwei builds
│   └── stat_gold_values.csv       # Current patch gold values
├── templates/
│   ├── advanced_formulas.md       # All calculation formulas
│   └── formatting.md              # Conditional formatting guide
└── docs/
    ├── gold_efficiency.md         # Gold efficiency methodology
    └── patch_updates.md           # Maintenance guide
```

## 🎮 How to Use

### **Creating Builds**:
1. Go to **Build Definitions** tab
2. Enter build name and select 6 items
3. System auto-calculates all damage values

### **Comparing Builds**:
1. Go to **Dashboard** tab  
2. Select builds from dropdowns
3. Compare damage vs different target types

### **Reading Results**:
- **vs Squishy**: Damage vs ADCs, mages (40 MR)
- **vs Tanky**: Damage vs bruisers, supports (80 MR)  
- **vs Ultra Tank**: Damage vs full tanks (120 MR)
- **Best Target**: Which enemy type to prioritize
- **Damage/1000g**: Cost efficiency metric

## 🔄 Maintenance

### **Patch Updates**:
1. Check patch notes for item changes
2. Update item stats in database
3. Verify gold efficiency values
4. Test sample builds

### **Adding New Items**:
1. Add item row to Items Database
2. Include all stats and costs
3. Estimate passive damage value
4. Item appears in all dropdowns automatically

## 🤝 Contributing

Submit pull requests with:
- Updated item data for new patches
- New build strategies
- Formula improvements
- Documentation enhancements

## 📜 License

Open source project for the League of Legends community.

## 🔗 Links

- **Repository**: [github.com/renbkna/league-hwei-build-analyzer](https://github.com/renbkna/league-hwei-build-analyzer)
- **League Wiki**: [wiki.leagueoflegends.com](https://wiki.leagueoflegends.com)
- **Author**: renbkna

---

## 🚀 Get Started Now!

**Ready to optimize your Hwei gameplay?**

1. 📖 **Read [BUILD_GUIDE.md](BUILD_GUIDE.md)** for complete setup
2. 🎯 **Build your analyzer** (1 hour)
3. 📊 **Analyze your builds** and climb ranked!

*Transform from guessing item efficiency to calculating real damage output!* ⚡