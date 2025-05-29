# League of Legends Hwei Build Analyzer

A comprehensive Google Sheets system for analyzing Hwei item builds with gold efficiency calculations, DPS tracking, and strategic build comparisons.

## 🎯 Overview

This system allows you to:
- Define and compare multiple Hwei builds side-by-side
- Calculate accurate gold efficiency based on raw stats
- Track actual DPS/damage performance from testing
- Analyze gold-per-damage ratios for optimal builds
- Make data-driven decisions for build optimization

## 📊 System Architecture

The analyzer consists of **5 interconnected Google Sheets tabs**:

1. **Dashboard/Build Comparator** - Main interface for comparing builds
2. **Build Definitions** - Define each Hwei build with items and runes  
3. **Items Database** - Comprehensive item stats and costs
4. **Stat Gold Values** - Official gold values for each stat type
5. **Runes Database** - Rune names and effects for build documentation

## 🚀 Quick Start

### Step 1: Create Google Sheet
1. Create a new Google Sheet
2. Create 5 tabs with exact names: `Dashboard`, `Build Definitions`, `Items Database`, `Stat Gold Values`, `Runes Database`

### Step 2: Import Data
1. Download CSV files from this repository
2. Import each CSV into its corresponding tab
3. The data includes current patch gold values and common Hwei items

### Step 3: Set Up Formulas
Follow the detailed setup instructions in `SETUP_GUIDE.md` to implement:
- Data validation dropdowns
- Gold efficiency calculations  
- Build comparison formulas
- Conditional formatting

## 📈 Key Features

### Gold Efficiency Analysis
- **Raw Stat Value**: Calculates theoretical gold value of item stats
- **Gold Efficiency %**: Compares stat value vs actual cost
- **Build Efficiency**: Total efficiency across all 6 items

### Performance Tracking
- **Manual DPS Input**: Enter your tested damage values
- **Damage Per Gold**: Efficiency metric for build optimization
- **Side-by-Side Comparison**: Compare up to 3 builds simultaneously

### Smart Data Management
- **Dropdown Validation**: Prevents typos in item/rune selection
- **Automatic Calculations**: Real-time updates when builds change
- **Conditional Formatting**: Visual indicators for efficiency thresholds

## 📁 Repository Structure

```
league-hwei-build-analyzer/
├── README.md                 # This file
├── SETUP_GUIDE.md           # Detailed implementation guide
├── data/                    # CSV files for import
│   ├── stat_gold_values.csv # Official gold values (V14.21)
│   ├── hwei_items.csv       # Common Hwei items with stats
│   ├── runes_database.csv   # Rune names and effects
│   └── sample_builds.csv    # Example Hwei builds
├── templates/               # Google Sheets templates
│   ├── formulas.md         # All formulas with explanations
│   └── formatting.md       # Conditional formatting rules
└── docs/                   # Additional documentation
    ├── gold_efficiency.md  # Gold efficiency methodology
    └── patch_updates.md    # How to update for new patches
```

## 🔧 Current Data (Patch 14.21)

### Gold Values Per Stat Point:
- **Ability Power**: 20 gold (Amplifying Tome)
- **Health**: 2.67 gold (Ruby Crystal)
- **Armor**: 20 gold (Cloth Armor)
- **Magic Resistance**: 20 gold (Null-Magic Mantle)
- **Ability Haste**: 50 gold (Glowing Mote)
- **Magic Penetration %**: 46.15 gold (Blighting Jewel)
- **Mana**: 1 gold (Sapphire Crystal)

### Included Hwei Items:
- **Mythic/Core**: Luden's Companion, Rod of Ages, Liandry's Torment
- **Legendary**: Shadowflame, Rabadon's Deathcap, Void Staff, Zhonya's Hourglass
- **Situational**: Banshee's Veil, Horizon Focus, Malignance, Cosmic Drive
- **Boots**: Sorcerer's Shoes, Mercury's Treads, Ionian Boots

## 🎮 Usage Workflow

1. **Define Builds**: Create your Hwei builds in `Build Definitions` tab
2. **Test In-Game**: Take builds to Practice Tool or live games
3. **Record Performance**: Input actual DPS/damage numbers
4. **Compare & Analyze**: Use `Dashboard` to compare efficiency
5. **Optimize**: Iterate based on gold-per-damage ratios

## 📋 Example Analysis

**Build A**: Luden's → Shadowflame → Rabadon's → Void → Zhonya's → Sorc Shoes
- Total Cost: ~16,100g
- Raw Stat Efficiency: 98.5%
- Your Tested DPS: 2,847
- DPS per 1000g: 177

**Build B**: Rod of Ages → Archangel's → Rabadon's → Void → Zhonya's → Sorc Shoes  
- Total Cost: ~16,800g
- Raw Stat Efficiency: 104.2%
- Your Tested DPS: 2,654
- DPS per 1000g: 158

→ **Build A provides better damage per gold despite lower raw efficiency**

## 🔄 Maintenance

### Patch Updates
When new patches release:
1. Check [League Wiki Gold Efficiency](https://wiki.leagueoflegends.com/en-us/Gold_efficiency) for stat value changes
2. Update `stat_gold_values.csv` if needed
3. Add/modify items in `hwei_items.csv` for reworked items
4. Re-import updated CSV files

### Adding New Items
1. Find item stats on [League Wiki](https://wiki.leagueoflegends.com/en-us/List_of_items)
2. Add row to `hwei_items.csv` with: Name, Cost, AP, Health, Armor, MR, etc.
3. Import updated CSV to refresh your sheet

## 🤝 Contributing

Feel free to contribute:
- Updated item data for new patches
- Additional rune combinations
- Formula improvements
- Documentation enhancements

## 📜 License

Open source project for League of Legends theorycrafting community.

## 🔗 Links

- **Repository**: [github.com/renbkna/league-hwei-build-analyzer](https://github.com/renbkna/league-hwei-build-analyzer)
- **League Wiki**: [wiki.leagueoflegends.com](https://wiki.leagueoflegends.com)
- **Author**: renbkna

---

*Last updated: Patch 14.21 | Created for Hwei build optimization*