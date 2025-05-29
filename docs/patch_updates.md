# Patch Update Guide

How to maintain your Hwei Build Analyzer when League of Legends patches change item stats, costs, or introduce new items.

## 📏 Regular Update Schedule

### Major Patches (Every 2 weeks)
- **Check**: Item stat changes
- **Update**: CSV files if needed
- **Verify**: Formula calculations still work
- **Test**: Sample builds for accuracy

### Mid-Season Updates
- **Review**: Major item reworks
- **Add**: New items relevant to Hwei
- **Remove**: Deleted items
- **Recalibrate**: Gold values if basic items change

### Pre-Season Updates
- **Rebuild**: Potentially entire item database
- **Update**: All gold efficiency values
- **Revise**: Build templates
- **Test**: All formulas extensively

## 🔍 Where to Find Patch Information

### Primary Sources
1. **Official Patch Notes**: [leagueoflegends.com](https://www.leagueoflegends.com/en-us/news/tags/patch-notes/)
2. **League Wiki**: [wiki.leagueoflegends.com](https://wiki.leagueoflegends.com/en-us/Gold_efficiency)
3. **PBE Updates**: Early preview of changes

### What to Look For
- 💰 **Cost changes** (affects efficiency calculations)
- 📈 **Stat adjustments** (AP, Health, Haste, etc.)
- 🆕 **New items** (especially AP/Mage items)
- ❌ **Removed items** (clean up database)
- 🔄 **Reworked items** (may need complete re-entry)

## 🔧 Step-by-Step Update Process

### Step 1: Identify Changes

#### Check Patch Notes for:
```
- Item cost adjustments
- Stat number changes (AP, Health, etc.)
- New mage/AP items
- Removed items
- Changes to basic items (Amplifying Tome, etc.)
```

#### Example Patch Note Entry:
```
Luden's Companion
- Ability Power: 100 → 95
- Cost: 2850 → 2900
- Echo damage: 75 → 80
```

### Step 2: Update CSV Files

#### A. Update `hwei_items.csv`
1. Open the file in spreadsheet software
2. Find the changed item (e.g., "Luden's Companion")
3. Update relevant columns:
   - Gold Cost: 2850 → 2900
   - AP: 100 → 95
4. Recalculate "Total Raw Stat Gold Value":
   - Old: (100×20) + (600×1) + (10×50) = 3,100
   - New: (95×20) + (600×1) + (10×50) = 3,500
5. Save the file

#### B. Update `stat_gold_values.csv` (if needed)
Only update if **basic items** change:
- Amplifying Tome cost change → Update AP gold value
- Ruby Crystal cost change → Update Health gold value
- New basic items → Add new stat gold values

#### C. Add New Items
For completely new items:
```csv
"New Item Name",2800,Legendary,85,0,250,0,0,0,20,0,0,0,0,"Unique passive description",2450
```

### Step 3: Re-import to Google Sheets

1. **Open your Google Sheet**
2. **Go to updated tab** (e.g., Items Database)
3. **File → Import → Upload**
4. **Select updated CSV file**
5. **Choose "Replace current sheet"**
6. **Import data**
7. **Verify formulas still reference correct columns**

### Step 4: Test Everything

#### Quick Verification Checklist:
- ✅ Build costs calculate correctly
- ✅ Gold efficiency percentages look reasonable
- ✅ Dropdowns include new items
- ✅ No #N/A or #REF! errors
- ✅ Sample builds still work

#### Test Build Example:
1. Select "Standard Burst" build in Dashboard
2. Verify total cost matches expected value
3. Check that efficiency calculation seems correct
4. Input test DPS value
5. Confirm ratios calculate properly

## 🔄 Common Update Scenarios

### Scenario 1: Simple Stat Adjustment
**Example**: Shadowflame AP: 120 → 115

**Update Process**:
1. Edit `hwei_items.csv`: Change AP column
2. Recalculate stat value: (115×20) + (10×46.67) = 2,766.7
3. Re-import CSV
4. Done!

### Scenario 2: Cost Change
**Example**: Void Staff: 2700g → 2800g

**Impact**: Changes efficiency of all builds using Void Staff
**Update Process**:
1. Edit `hwei_items.csv`: Change Gold Cost column
2. Re-import CSV
3. All builds auto-update due to VLOOKUP formulas

### Scenario 3: New Item Addition
**Example**: "Hwei's Focus" - New AP item

**Process**:
1. Research item stats from patch notes/wiki
2. Add new row to `hwei_items.csv`:
   ```csv
   "Hwei's Focus",3200,Legendary,90,0,0,400,0,0,25,15,0,0,0,"Grants vision on spell hit",3477
   ```
3. Re-import CSV
4. New item appears in all dropdowns automatically

### Scenario 4: Item Rework
**Example**: Major changes to Rod of Ages

**Process**:
1. Completely replace the item's row in CSV
2. Update any sample builds that use it
3. Re-test builds extensively
4. Update build descriptions if item role changed

### Scenario 5: Basic Item Changes
**Example**: Amplifying Tome: 20 AP for 400g → 25 AP for 500g

**Major Impact**: Changes AP gold value for ALL items
**Process**:
1. Update `stat_gold_values.csv`: AP value 20 → 20 (500/25)
2. Recalculate ALL item stat values in `hwei_items.csv`
3. Re-import both files
4. Extensively test - all efficiencies will change

## 📁 Version Control Best Practices

### File Naming Convention
```
hwei_items_v14.21.csv
hwei_items_v14.22.csv
stat_gold_values_v14.21.csv
```

### Change Log Template
```markdown
## Patch 14.22 Changes

### Updated Items:
- Luden's Companion: AP 100→95, Cost 2850→2900
- Shadowflame: Magic Pen 10→12

### New Items:
- Hwei's Focus: 90 AP, 25 AH, 15% Magic Pen

### Removed Items:
- None

### Impact:
- Standard Burst build efficiency: 98.5% → 96.2%
- New build options with Hwei's Focus
```

## 🚑 Emergency Hotfix Updates

For urgent mid-patch hotfixes:

### Quick Update Process:
1. **Identify critical changes** (usually cost or major stat nerfs)
2. **Update only affected items** in CSV
3. **Re-import immediately**
4. **Test affected builds**
5. **Document changes** for full update later

### Critical Items to Watch:
- **Core Hwei items**: Luden's, Shadowflame, Rabadon's
- **High-efficiency items**: Items above 100% efficiency
- **Meta items**: Currently popular in pro play

## 📈 Seasonal Considerations

### Pre-Season (November-December)
- **Expect major changes**: Item system overhauls possible
- **Plan for rebuilds**: May need to recreate entire database
- **Monitor PBE closely**: Get early warning of changes

### Mid-Season (May-June)
- **Moderate changes**: Usually item adjustments, not overhauls
- **New items likely**: Expansion of item options
- **Meta shifts**: Popular items may change

### Regular Season
- **Small adjustments**: Minor stat/cost tweaks
- **Predictable timing**: Every 2 weeks
- **Maintain vigilance**: Even small changes matter for efficiency

## 📄 Automation Opportunities

### Future Enhancements:
- **API Integration**: Automatically pull item data
- **Notification System**: Alert when items change
- **Version Comparison**: Track changes over time

### Current Manual Process Benefits:
- **Quality Control**: Human verification of changes
- **Customization**: Add Hwei-specific notes and insights
- **Understanding**: Better grasp of meta implications

Staying current with patches ensures your build analyzer remains accurate and valuable for optimizing Hwei gameplay! 🏆

---

**Pro Tip**: Set a calendar reminder for every patch day to check for updates. It's easier to maintain regularly than to fix after falling behind! 📅