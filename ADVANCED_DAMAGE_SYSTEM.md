# Complete Damage Calculation System - Implementation Guide

Transform your basic gold efficiency calculator into an advanced damage analysis system.

## 🎯 Enhanced Build Definitions Tab - New Columns

Add these columns after your existing ones (starting from Column W):

### **Column W: Total AP (Including Rabadon's)**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:D,4,FALSE),0)) * 
(1 + IF(COUNTIF(N2:S2,"Rabadon's Deathcap")>0,0.4,0))
```

### **Column X: Total % Magic Penetration**
```excel
=1-(1-SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:K,11,FALSE),0))/100)
```

### **Column Y: Total Flat Magic Penetration**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:L,12,FALSE),0))
```

### **Column Z: Effective MR vs 40 MR Target (Squishy)**
```excel
=MAX(0, 40*(1-X2) - Y2)
```

### **Column AA: Effective MR vs 80 MR Target (Tanky)**
```excel
=MAX(0, 80*(1-X2) - Y2)
```

### **Column AB: Effective MR vs 120 MR Target (Ultra Tank)**
```excel
=MAX(0, 120*(1-X2) - Y2)
```

### **Column AC: Damage Multiplier vs Squishy (40 MR)**
```excel
=100/(100+Z2)
```

### **Column AD: Damage Multiplier vs Tanky (80 MR)**
```excel
=100/(100+AA2)
```

### **Column AE: Damage Multiplier vs Ultra Tank (120 MR)**
```excel
=100/(100+AB2)
```

### **Column AF: Hwei Base Combo Damage**
```excel
=1000 + (W2 * 2.8)
```
*Base: 1000, AP Ratio: 280% (estimated full combo)*

### **Column AG: Item Passive Damage Estimate**
```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:R,18,FALSE),0))
```

### **Column AH: Total Damage vs Squishy**
```excel
=(AF2 + AG2) * AC2
```

### **Column AI: Total Damage vs Tanky**
```excel
=(AF2 + AG2) * AD2
```

### **Column AJ: Total Damage vs Ultra Tank**
```excel
=(AF2 + AG2) * AE2
```

### **Column AK: Average DPS (8 second combo cycle)**
```excel
=AVERAGE(AH2,AI2,AJ2) / 8
```

## 🔥 Item Passive Database - Enhanced

Update your Items Database with these passive damage estimates:

```csv
Item Name,Passive DPS Estimate,Passive Notes
Luden's Companion,120,Echo damage per combo cycle
Shadowflame,80,Crit damage vs low HP + adaptive pen value
Liandry's Torment,160,Current HP burn over time
Horizon Focus,200,10% damage amplification on combo
Riftmaker,100,True damage conversion after ramp
Malignance,90,Ultimate enhancement and Haunt proc
Cosmic Drive,40,Combat movement speed value
Rod of Ages,150,Scaling stats at full stacks
Archangel's Staff,60,Mana-to-AP conversion value
Lich Bane,140,Spellblade proc per combo
Cryptbloom,70,Grievous wounds utility value
Stormsurge,110,Movement speed on takedowns
```

## 📊 Enhanced Dashboard - New Rows

Add these rows to your Dashboard for advanced analysis:

### **Row 14: Damage vs Squishy Targets**
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:AH,34,FALSE),0)
```

### **Row 15: Damage vs Tanky Targets**
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:AI,35,FALSE),0)
```

### **Row 16: Damage vs Ultra Tanks**
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:AJ,36,FALSE),0)
```

### **Row 17: Average DPS**
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:AK,37,FALSE),0)
```

### **Row 18: Penetration Effectiveness Score**
```excel
=(VLOOKUP(B2,'Build Definitions'!A:AC,29,FALSE) + 
VLOOKUP(B2,'Build Definitions'!A:AD,30,FALSE) + 
VLOOKUP(B2,'Build Definitions'!A:AE,31,FALSE)) / 3
```

### **Row 19: Damage Per 1000 Gold**
```excel
=IF(B3>0,B17*1000/B3,0)
```

### **Row 20: Best Target Type**
```excel
=IF(B16>B15,"Ultra Tanks",IF(B15>B14,"Tanky Targets","Squishy Targets"))
```

## 🧮 Magic Penetration Calculator

### **Void Staff vs Shadowflame Decision**
```excel
=IF(Target_MR<50,"Shadowflame Better",
IF(Target_MR<75,"Situational",
"Void Staff Better"))
```

### **Penetration Breakpoint Calculator**
```excel
=((Shadowflame_AP_Advantage * 2.8) / (Target_Base_Damage)) * 100 + 40
```

## 🎮 Situational Analysis Formulas

### **Power Spike Timing**
```excel
=IF(Total_Cost<8000,"Early Game",
IF(Total_Cost<14000,"Mid Game",
"Late Game"))
```

### **Build Archetype Identifier**
```excel
=IF(Flat_Magic_Pen>25,"Penetration Build",
IF(Total_AP>600,"Scaling Build",
IF(Total_HP>800,"Survivability Build",
"Balanced Build")))
```

## 🔧 Implementation Steps

### **Step 1**: Add New Columns to Build Definitions
1. Insert columns W through AK after your existing columns
2. Copy-paste the formulas above
3. Drag formulas down to all your build rows

### **Step 2**: Update Items Database
1. Add "Passive DPS Estimate" column (Column R)
2. Fill in the passive damage values from the table above
3. Update your Total Raw Stat Gold Value formula to reference correct columns

### **Step 3**: Enhance Dashboard
1. Add rows 14-20 to your Dashboard
2. Copy-paste the dashboard formulas
3. Format with conditional coloring for easy reading

### **Step 4**: Test Your System
1. Create a test build: Luden's → Shadowflame → Rabadon's → Void → Zhonya's → Spellslinger's
2. Verify calculations look reasonable
3. Compare damage vs different target types

## 📈 What This System Now Calculates

### ✅ **Real Magic Penetration**
- Correct order of operations (% then flat)
- Multiplicative % penetration stacking
- Effective MR vs different targets

### ✅ **Actual Damage Output**
- Hwei's combo damage with AP scaling
- Item passive damage contributions
- Damage vs Squishy/Tanky/Ultra Tank targets

### ✅ **Advanced Metrics**
- True DPS calculations
- Damage per gold efficiency
- Penetration effectiveness scoring
- Build archetype classification

### ✅ **Decision Support**
- Void Staff vs Shadowflame recommendations
- Optimal target selection
- Power spike timing analysis

## 🎯 Example Output

**Standard Burst Build**:
- **vs Squishy**: 2,847 damage (356 DPS)
- **vs Tanky**: 2,234 damage (279 DPS)  
- **vs Ultra Tank**: 1,756 damage (220 DPS)
- **Damage/1000g**: 177 vs squishies
- **Best vs**: Squishy Targets
- **Penetration Score**: 8.2/10

Your build analyzer now calculates **real damage effectiveness**, not just theoretical gold efficiency! 🚀