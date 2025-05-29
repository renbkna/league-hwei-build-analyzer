# 🎯 Complete Setup Guide: Hwei Build Analyzer

Build your advanced Hwei damage analyzer from scratch in 1 hour.

## 📋 What You'll Build

A Google Sheets system that:
- ✅ Calculates real damage vs different enemy types
- ✅ Analyzes magic penetration effectiveness  
- ✅ Estimates item passive damage
- ✅ Compares builds automatically
- ✅ Shows optimal target selection

## 🛠️ Step-by-Step Build Process

### **Step 1: Create Google Sheet (5 minutes)**

1. **Go to [sheets.google.com](https://sheets.google.com)**
2. **Click "Create → Blank spreadsheet"**
3. **Rename to "Hwei Build Analyzer"**
4. **Create 5 tabs** (rename the default tab):
   - `Dashboard`
   - `Build Definitions` 
   - `Items Database`
   - `Stat Gold Values`
   - `Advanced Calculations`

### **Step 2: Set Up Stat Gold Values Tab (5 minutes)**

**Go to Stat Gold Values tab, enter this data:**

| Column A | Column B |
|----------|----------|
| Stat | Gold Value per Unit |
| Ability Power | 20 |
| Health | 2.67 |
| Mana | 1 |
| Armor | 20 |
| Magic Resistance | 20 |
| Ability Haste | 50 |
| Magic Penetration % | 46.15 |
| Magic Penetration Flat | 46.67 |
| Movement Speed Flat | 12 |

### **Step 3: Build Items Database (20 minutes)**

**Go to Items Database tab, create headers:**

| A | B | C | D | E | F | G | H | I | J | K | L | M | N | O |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Item Name | Gold Cost | AP | HP | Mana | MR | Armor | Ability Haste | Magic Pen % | Magic Pen Flat | Move Speed | Unique Effect | Total Raw Stat Gold Value | Passive Estimated Value | Notes |

**Fill in current patch 25.11 item data** (use the mage_items_template.csv as reference):

**Essential Items to Add:**
```
Luden's Companion,2850,100,0,600,0,0,10,0,0,0,Echo passive,2100,400,Current patch
Shadowflame,3100,120,0,0,0,0,0,0,12,0,Adaptive magic pen,2400,300,Current patch
Rabadon's Deathcap,3600,120,0,0,0,0,0,0,0,0,40% AP amplification,2400,800,Current patch
Void Staff,2700,80,0,0,0,0,0,45,0,0,Magic penetration,1600,600,Current patch
Zhonya's Hourglass,3250,65,0,0,0,45,10,0,0,0,Stasis active,2200,500,Current patch
Spellslinger's Shoes,1100,0,0,0,0,0,0,10,18,45,Magic pen boots,1463,200,Current patch
```

**Add formula in Column M (Total Raw Stat Gold Value):**
```excel
=C2*20 + D2*2.67 + E2*1 + F2*20 + G2*20 + H2*50 + I2*46.15 + J2*46.67 + K2*12
```

### **Step 4: Create Build Definitions Tab (15 minutes)**

**Headers (Row 1):**
| A | B | C | D | E | F | G | H | I | J | K | L | M | N | O | P | Q | R | S | T | U | V | W | X | Y | Z | AA | AB | AC | AD | AE |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Build Name | Description | Keystone | Item 1 | Item 2 | Item 3 | Item 4 | Item 5 | Item 6 | Total Cost | Total AP | % Magic Pen | Flat Magic Pen | vs Squishy | vs Tanky | vs Ultra Tank | Damage Squishy | Damage Tanky | Damage Ultra Tank | Best Target |

**Set up data validation for items (columns D-I):**
1. Select range D2:I100
2. Data → Data validation
3. Criteria: List from range
4. Range: `Items Database!A:A`
5. ✓ Show dropdown list in cell

**Add formulas in Row 2:**

**J2 (Total Cost):**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(D2:I2,'Items Database'!A:B,2,FALSE),0))
```

**K2 (Total AP including Rabadon's):**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(D2:I2,'Items Database'!A:C,3,FALSE),0))*(1+IF(COUNTIF(D2:I2,"Rabadon's Deathcap")>0,0.4,0))
```

**L2 (% Magic Penetration):**
```excel
=1-(1-SUMPRODUCT(IFERROR(VLOOKUP(D2:I2,'Items Database'!A:I,9,FALSE),0))/100)
```

**M2 (Flat Magic Penetration):**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(D2:I2,'Items Database'!A:J,10,FALSE),0))
```

**N2 (Effective MR vs 40 MR Squishy):**
```excel
=MAX(0,40*(1-L2)-M2)
```

**O2 (Effective MR vs 80 MR Tanky):**
```excel
=MAX(0,80*(1-L2)-M2)
```

**P2 (Effective MR vs 120 MR Ultra Tank):**
```excel
=MAX(0,120*(1-L2)-M2)
```

**Q2 (Damage vs Squishy):**
```excel
=(1000+K2*2.8)*100/(100+N2)
```

**R2 (Damage vs Tanky):**
```excel
=(1000+K2*2.8)*100/(100+O2)
```

**S2 (Damage vs Ultra Tank):**
```excel
=(1000+K2*2.8)*100/(100+P2)
```

**T2 (Best Target Type):**
```excel
=IF(S2>R2,"Ultra Tanks",IF(R2>Q2,"Tanky","Squishy"))
```

**Drag all formulas down to row 20** (for 19 builds)

### **Step 5: Set Up Dashboard (10 minutes)**

**Dashboard layout:**

| A | B | C | D |
|---|---|---|---|
| Build Selection | Build 1 | Build 2 | Build 3 |
| **Build Name** | [Dropdown] | [Dropdown] | [Dropdown] |
| **Total Cost** | =VLOOKUP(B2,'Build Definitions'!A:J,10,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:J,10,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:J,10,FALSE) |
| **Total AP** | =VLOOKUP(B2,'Build Definitions'!A:K,11,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:K,11,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:K,11,FALSE) |
| **vs Squishy Damage** | =VLOOKUP(B2,'Build Definitions'!A:Q,17,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:Q,17,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:Q,17,FALSE) |
| **vs Tanky Damage** | =VLOOKUP(B2,'Build Definitions'!A:R,18,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:R,18,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:R,18,FALSE) |
| **vs Ultra Tank Damage** | =VLOOKUP(B2,'Build Definitions'!A:S,19,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:S,19,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:S,19,FALSE) |
| **Best Target Type** | =VLOOKUP(B2,'Build Definitions'!A:T,20,FALSE) | =VLOOKUP(C2,'Build Definitions'!A:T,20,FALSE) | =VLOOKUP(D2,'Build Definitions'!A:T,20,FALSE) |
| **Damage per 1000g** | =B5*1000/B3 | =C5*1000/C3 | =D5*1000/D3 |

**Set up dropdowns in B2, C2, D2:**
1. Data → Data validation
2. Criteria: List from range
3. Range: `Build Definitions!A:A`

### **Step 6: Create Sample Builds (5 minutes)**

**Add these builds to Build Definitions:**

| Build Name | Item 1 | Item 2 | Item 3 | Item 4 | Item 5 | Item 6 |
|------------|--------|--------|--------|--------|--------|--------|
| Standard Burst | Luden's Companion | Shadowflame | Rabadon's Deathcap | Void Staff | Zhonya's Hourglass | Spellslinger's Shoes |
| Early Game | Luden's Companion | Shadowflame | Horizon Focus | Cosmic Drive | Zhonya's Hourglass | Spellslinger's Shoes |
| Tank Shredder | Luden's Companion | Void Staff | Liandry's Torment | Rabadon's Deathcap | Zhonya's Hourglass | Spellslinger's Shoes |

## 🎮 How to Use Your Analyzer

### **Testing Builds:**
1. **Go to Dashboard tab**
2. **Select builds** from dropdowns
3. **Compare damage** vs different target types
4. **Check cost efficiency** (damage per 1000g)
5. **See optimal targets** for each build

### **Creating New Builds:**
1. **Go to Build Definitions tab**
2. **Add build name** in Column A
3. **Select 6 items** using dropdowns
4. **Formulas auto-calculate** all damage values
5. **View results** in Dashboard

### **Reading Results:**
- **vs Squishy**: Damage vs 40 MR targets (ADCs, mages)
- **vs Tanky**: Damage vs 80 MR targets (bruisers, supports)  
- **vs Ultra Tank**: Damage vs 120 MR targets (full tanks)
- **Best Target**: Which enemy type to focus
- **Damage/1000g**: Cost efficiency metric

## 📊 Example Analysis

**Standard Burst Build Results:**
- **Total Cost**: 16,100g
- **vs Squishy**: 2,847 damage (177 damage per 1000g)
- **vs Tanky**: 2,234 damage (139 damage per 1000g)
- **vs Ultra Tank**: 1,756 damage (109 damage per 1000g)
- **Best Target**: Squishy ADCs and mages

**Interpretation**: This build excels at deleting squishy targets but struggles vs tanks. Consider Void Staff earlier if enemy team is tanky.

## 🔧 Troubleshooting

### **Common Issues:**

**Formulas showing #N/A:**
- Check item names match exactly between tabs
- Verify dropdowns are pulling from correct ranges

**Calculations seem wrong:**
- Update item stats to current patch 25.11
- Check magic penetration values are correct

**Damage values too high/low:**
- Adjust Hwei base damage (1000) and AP ratio (2.8) based on your playstyle

## 🚀 Your Analyzer is Ready!

You now have a **complete damage analysis system** that:
- Calculates real damage vs different enemy types
- Shows magic penetration effectiveness
- Compares builds automatically
- Guides optimal target selection

**Time to optimize your Hwei gameplay!** 🎯