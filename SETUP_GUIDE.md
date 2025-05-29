# Google Sheets Setup Guide

Detailed instructions for implementing the Hwei Build Analyzer in Google Sheets.

## 🔧 Prerequisites

- Google Account with access to Google Sheets
- Basic familiarity with spreadsheet formulas
- Downloaded CSV files from this repository

## 📋 Step-by-Step Setup

### Step 1: Create the Sheet Structure

1. **Create New Google Sheet**
   - Go to [sheets.google.com](https://sheets.google.com)
   - Click "+ Blank" to create new sheet
   - Rename to "Hwei Build Analyzer"

2. **Create Required Tabs** (exact names required):
   - `Dashboard` (rename the default "Sheet1")
   - `Build Definitions`
   - `Items Database`
   - `Stat Gold Values`
   - `Runes Database`

### Step 2: Import Data Files

For each tab, import the corresponding CSV:

#### A. Stat Gold Values Tab
1. Select `Stat Gold Values` tab
2. File → Import → Upload → Select `stat_gold_values.csv`
3. Choose "Replace current sheet" → Import data

#### B. Items Database Tab
1. Select `Items Database` tab
2. File → Import → Upload → Select `hwei_items.csv`
3. Choose "Replace current sheet" → Import data

#### C. Runes Database Tab
1. Select `Runes Database` tab
2. File → Import → Upload → Select `runes_database.csv`
3. Choose "Replace current sheet" → Import data

### Step 3: Set Up Build Definitions Tab

#### Column Headers (Row 1):
```
A1: Build Name
B1: Description
C1: Champion
D1: Keystone
E1: Primary 1
F1: Primary 2
G1: Primary 3
H1: Secondary Tree
I1: Secondary 1
J1: Secondary 2
K1: Shard 1
L1: Shard 2
M1: Shard 3
N1: Item 1
O1: Item 2
P1: Item 3
Q1: Item 4
R1: Item 5
S1: Item 6
T1: Total Gold Cost
U1: Total Raw Stat Gold Value
V1: Gold Efficiency %
```

#### Data Validation Setup:

**For Item Columns (N1:S1):**
1. Select range N2:S100 (covers 99 builds)
2. Data → Data validation
3. Criteria: List from a range
4. Range: `Items Database!A:A`
5. ✓ Show dropdown list in cell
6. Done

**For Rune Columns (D1:M1):**
1. Select range D2:M100
2. Data → Data validation
3. Criteria: List from a range
4. Range: `Runes Database!A:A`
5. Done

#### Formulas for Build Definitions:

**T2 (Total Gold Cost):**
```
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:B,2,FALSE),0))
```

**U2 (Total Raw Stat Gold Value):**
```
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:T,20,FALSE),0))
```

**V2 (Gold Efficiency %):**
```
=IF(T2=0,0,U2/T2)
```

**Copy formulas down to row 100**

### Step 4: Set Up Dashboard Tab

#### Column Headers:
```
A1: Build Selection
B1: Build 1
C1: Build 2
D1: Build 3
A3: Total Gold Cost
A4: Raw Stat Gold Value
A5: Gold Efficiency %
A6: Your Calculated DPS
A7: Your Calculated Total Damage
A8: DPS per Gold
A9: Damage per Gold
A10: Build Description
```

#### Build Selection Dropdowns:
**B2, C2, D2:**
1. Select each cell
2. Data → Data validation
3. Criteria: List from a range
4. Range: `Build Definitions!A:A`
5. Done

#### Dashboard Formulas:

**B3 (Build 1 Total Gold Cost):**
```
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:T,20,FALSE),0)
```

**B4 (Build 1 Raw Stat Gold Value):**
```
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:U,21,FALSE),0)
```

**B5 (Build 1 Gold Efficiency):**
```
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:V,22,FALSE),0)
```

**B8 (DPS per Gold):**
```
=IF(AND(B6>0,B3>0),B6/B3*1000,0)
```

**B9 (Damage per Gold):**
```
=IF(AND(B7>0,B3>0),B7/B3*1000,0)
```

**B10 (Build Description):**
```
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:B,2,FALSE),"")
```

**Copy all formulas to columns C and D for Build 2 and Build 3**

### Step 5: Conditional Formatting

#### Gold Efficiency Formatting:
1. Select Dashboard range B5:D5
2. Format → Conditional formatting
3. Format cells if: Custom formula is
4. Value: `=$B5>=1` (≥100% efficiency)
5. Formatting: Green background
6. Add another rule: `=$B5<1` (Red background)
7. Done

#### Repeat for Build Definitions V2:V100

### Step 6: Add Sample Builds

#### Example Build 1:
- **Build Name**: Standard Burst
- **Description**: High AP burst for team fights
- **Items**: Luden's Companion, Shadowflame, Rabadon's Deathcap, Void Staff, Zhonya's Hourglass, Sorcerer's Shoes

#### Example Build 2:
- **Build Name**: Scaling Late Game
- **Description**: Maximum late game damage
- **Items**: Rod of Ages, Archangel's Staff, Rabadon's Deathcap, Void Staff, Lich Bane, Sorcerer's Shoes

### Step 7: Testing Your Setup

1. **Add a build** in Build Definitions tab
2. **Check calculations** automatically populate
3. **Select build** in Dashboard dropdown
4. **Input test DPS values** (B6, C6, D6)
5. **Verify ratios** calculate correctly

## 🎨 Optional Enhancements

### Charts and Visualizations
1. Insert → Chart
2. Select Dashboard data range (B3:D9)
3. Chart type: Column chart
4. Customize with build names as labels

### Advanced Formulas

**Highest DPS Build (Dashboard A12):**
```
=INDEX(B2:D2,MATCH(MAX(B6:D6),B6:D6,0))
```

**Most Efficient Build (Dashboard A13):**
```
=INDEX(B2:D2,MATCH(MAX(B5:D5),B5:D5,0))
```

## 🔧 Troubleshooting

### Common Issues:

**"#N/A" errors in formulas:**
- Check that tab names match exactly
- Verify CSV import was successful
- Ensure data validation ranges are correct

**Dropdowns not working:**
- Re-check data validation range references
- Make sure ranges include headers

**Calculations showing 0:**
- Verify item names match exactly between tabs
- Check that gold values are numbers, not text

**Wrong gold efficiency:**
- Confirm stat gold values are current (check patch notes)
- Verify item stats are accurate

## 📊 Usage Tips

1. **Test builds in Practice Tool** before inputting DPS values
2. **Use consistent testing conditions** (same target, same combo)
3. **Update item data** when new patches release
4. **Compare similar builds** to identify optimal variations
5. **Track performance over time** by saving different versions

## 🔄 Maintenance

### Monthly Tasks:
- Check for new Hwei-relevant items
- Verify gold values haven't changed
- Update rune options if new runes are added

### Patch Day Tasks:
- Review patch notes for item changes
- Update item stats in Items Database
- Re-test builds if major changes occurred

Your Hwei Build Analyzer is now ready to optimize your builds! 🎯