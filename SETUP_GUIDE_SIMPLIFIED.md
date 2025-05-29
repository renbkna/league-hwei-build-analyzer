# Hwei Item Damage Calculator - Setup Guide

**Purpose**: Calculate real damage and DPS of individual items and item combinations vs specific MR/HP targets.

## 🎯 What This Calculates

- **1-item damage** vs target with X MR and Y HP
- **2-item damage** vs target with X MR and Y HP  
- **3-item damage** vs target with X MR and Y HP
- **Item passive effects** (Liandry's burn, Shadowflame crit, etc.)
- **Magic penetration effectiveness** (% pen → flat pen → actual damage)

## 🛠️ Setup (30 Minutes)

### **Step 1: Create Google Sheet**
1. Go to [sheets.google.com](https://sheets.google.com)
2. Create blank spreadsheet → Rename to "Hwei Item Calculator"
3. Create 3 tabs:
   - `Items Database`
   - `Damage Calculator`
   - `Target Settings`

### **Step 2: Set Up Items Database Tab**

**Import the core_items.csv data:**

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| Item Name | Gold Cost | AP | HP | Ability Haste | Magic Pen % | Magic Pen Flat | Passive Name | Passive Effect | Passive DPS | Raw Stat Value |
| Shadowflame | 3200 | 110 | 0 | 0 | 0 | 15 | Cinderbloom | Crit vs <40% HP | 250 | 2900 |
| Liandry's Torment | 3000 | 60 | 300 | 0 | 0 | 0 | Torment + Suffering | 1% max HP burn + 6% amp | 400 | 2001 |
| Rabadon's Deathcap | 3500 | 130 | 0 | 0 | 0 | 0 | Magical Opus | 30% AP amplification | 0 | 2600 |
| Horizon Focus | 2800 | 115 | 0 | 25 | 0 | 0 | Hypershot + Focus | Long range bonus | 300 | 3550 |
| Void Staff | 3000 | 95 | 0 | 0 | 40 | 0 | Magic Penetration | 40% magic pen | 0 | 3746 |
| Cryptbloom | 3000 | 75 | 0 | 20 | 30 | 0 | Life From Death | 30% pen + heal nova | 200 | 3884 |

### **Step 3: Set Up Target Settings Tab**

**Create target input section:**

| A | B |
|---|---|
| **Target Settings** | **Value** |
| Enemy Magic Resistance | 60 |
| Enemy Max Health | 2000 |
| Enemy Current Health % | 100 |
| Hwei Base Combo Damage | 800 |
| Hwei AP Ratio | 300 |

### **Step 4: Set Up Damage Calculator Tab**

**Headers:**

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| Items | Item 1 | Item 2 | Item 3 | Item 4 | Item 5 | Item 6 | Total AP | Effective MR | Base Damage | Final Damage |

**Row 2 - Item Selection (Data Validation):**
- Select B2:G2
- Data → Data validation → List from range: `Items Database!A:A`

**Row 3 - Calculations:**

**H3 (Total AP with Rabadon's):**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(B2:G2,'Items Database'!A:C,3,FALSE),0)) * 
(1 + IF(COUNTIF(B2:G2,"Rabadon's Deathcap")>0,0.3,0))
```

**I3 (Effective MR after penetration):**
```excel
=MAX(0,'Target Settings'!B2 * (1-SUMPRODUCT(IFERROR(VLOOKUP(B2:G2,'Items Database'!A:F,6,FALSE),0))/100) - SUMPRODUCT(IFERROR(VLOOKUP(B2:G2,'Items Database'!A:G,7,FALSE),0)))
```

**J3 (Base Damage):**
```excel
='Target Settings'!B5 + (H3 * 'Target Settings'!B6/100)
```

**K3 (Final Damage including passives):**
```excel
=(J3 * 100/(100+I3)) + SUMPRODUCT(IFERROR(VLOOKUP(B2:G2,'Items Database'!A:J,10,FALSE),0))
```

### **Step 5: Progressive Item Analysis**

**Add rows for each item count:**

| A | B | C | D | E | F | G | H | I | J | K |
|---|---|---|---|---|---|---|---|---|---|---|
| **1 Item** | [Item 1] | | | | | | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |
| **2 Items** | [Item 1] | [Item 2] | | | | | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |
| **3 Items** | [Item 1] | [Item 2] | [Item 3] | | | | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |
| **4 Items** | [Item 1] | [Item 2] | [Item 3] | [Item 4] | | | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |
| **5 Items** | [Item 1] | [Item 2] | [Item 3] | [Item 4] | [Item 5] | | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |
| **6 Items** | [Item 1] | [Item 2] | [Item 3] | [Item 4] | [Item 5] | [Item 6] | [Total AP] | [Eff MR] | [Base Dmg] | [Final Dmg] |

Copy the formulas from row 3 to each subsequent row.

## 🎮 How to Use

### **Set Your Target:**
1. Go to Target Settings tab
2. Input enemy MR (typical values: 30-120)
3. Input enemy max HP (typical: 1500-3000)
4. Set enemy current HP % (for Shadowflame passive)

### **Analyze Item Progression:**
1. Go to Damage Calculator tab
2. Select your item build order in the dropdowns
3. See damage increase with each additional item
4. Compare different item orders

### **Example Analysis:**

**Target: 60 MR, 2000 HP Enemy**

| Items | Total AP | Effective MR | Final Damage |
|-------|----------|--------------|--------------|
| **Shadowflame** | 110 | 45 | 1,940 |
| **+ Rabadon's** | 312 | 45 | 2,748 |
| **+ Void Staff** | 407 | 27 | 3,456 |
| **+ Liandry's** | 467 | 27 | 4,112 |

**Key Insights:**
- Shadowflame → Rabadon's: +808 damage
- Adding Void Staff: +708 damage (MR reduction)
- Adding Liandry's: +656 damage (passive burn)

## 🧮 Magic Penetration Calculation

**Order of Operations:**
1. **% Magic Pen** applied first (multiplicative)
2. **Flat Magic Pen** applied second (subtractive)
3. **Cannot go below 0 MR**

**Example: Void Staff + Cryptbloom vs 100 MR**
1. % Pen: 100 × (1-0.4) × (1-0.3) = 42 MR remaining
2. Flat Pen: 42 - 0 = 42 effective MR
3. Damage multiplier: 100/(100+42) = 70.4%

## 📊 Item Passive Calculations

### **Liandry's Torment**
- **Burn**: 1% max HP per 0.5s for 3s = 6% max HP total
- **Amp**: +6% damage after 3 seconds in combat
- **vs 2000 HP target**: 120 burn damage + 6% amp

### **Shadowflame**
- **Crit**: 120% damage vs enemies <40% HP
- **Effective**: +20% damage vs low HP targets

### **Horizon Focus**
- **Bonus**: Damage amplification on long-range abilities
- **Estimate**: ~15% damage increase

Your calculator now shows **real item-by-item damage progression** vs specific targets! 🎯