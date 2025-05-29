# Enhanced Formulas Reference - Patch 25.11

Advanced formulas for the Hwei Build Analyzer with damage calculations, penetration effectiveness, and passive value estimation.

## 🎯 Enhanced Build Definitions Formulas

### Advanced Total Gold Cost (Column T)
**Purpose**: Calculate build cost with component efficiency consideration

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:B,2,FALSE),0))
```

### Total Raw Stat Gold Value (Column U) - Enhanced
**Purpose**: More accurate stat value calculation with current gold values

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:Q,17,FALSE),0))
```

### Passive Value Estimation (Column V) 
**NEW**: Estimates the gold value of item passives

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:R,18,FALSE),0))
```

### True Gold Efficiency (Column W)
**NEW**: Includes passive values in efficiency calculation

```excel
=IF(T2=0,0,(U2+V2)/T2)
```

## 🔥 Damage Calculation Formulas

### Effective Magic Resistance vs Target (Columns X-Z)
**Purpose**: Calculate how much MR your build actually faces

#### Against 30 MR Target (Column X):
```excel
=MAX(0, 30 * (1 - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:K,11,FALSE),0))/100) - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:L,12,FALSE),0)))
```

#### Against 60 MR Target (Column Y):
```excel
=MAX(0, 60 * (1 - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:K,11,FALSE),0))/100) - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:L,12,FALSE),0)))
```

#### Against 100 MR Target (Column Z):
```excel
=MAX(0, 100 * (1 - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:K,11,FALSE),0))/100) - SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:L,12,FALSE),0)))
```

### Damage Multiplier Formulas (Columns AA-AC)
**Purpose**: How much damage you deal vs each target type

#### vs 30 MR (AA):
```excel
=100/(100+X2)
```

#### vs 60 MR (AB):
```excel
=100/(100+Y2)
```

#### vs 100 MR (AC):
```excel
=100/(100+Z2)
```

### Build Total AP Calculation (Column AD)
**Purpose**: Calculate total AP including Rabadon's passive

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:D,4,FALSE),0)) * (1 + IF(COUNTIF(N2:S2,"Rabadon's Deathcap")>0,0.4,0))
```

### Estimated DPS vs Targets (Columns AE-AG)
**Purpose**: Theoretical DPS based on build stats

#### Base DPS Calculation:
```excel
=AD2 * 0.8 + 200  // Hwei base damage estimate
```

#### DPS vs 30 MR (AE):
```excel
=(AD2 * 0.8 + 200) * AA2
```

#### DPS vs 60 MR (AF):
```excel
=(AD2 * 0.8 + 200) * AB2
```

#### DPS vs 100 MR (AG):
```excel
=(AD2 * 0.8 + 200) * AC2
```

## 📊 Enhanced Dashboard Formulas

### Advanced Build Comparison

#### Weighted Damage Score (Row 11)
**Purpose**: Weighted average damage across target types

```excel
=(VLOOKUP(B2,'Build Definitions'!A:AE,31,FALSE) * 0.4) + 
(VLOOKUP(B2,'Build Definitions'!A:AF,32,FALSE) * 0.4) + 
(VLOOKUP(B2,'Build Definitions'!A:AG,33,FALSE) * 0.2)
```

#### Build Power Spike Analysis (Row 12)
**Purpose**: When does this build peak in power?

```excel
=IF(COUNTIF(VLOOKUP(B2,'Build Definitions'!N:S,{1,2,3,4,5,6},FALSE),"Rabadon's Deathcap")>0,"Late Game",
IF(SUMPRODUCT(IFERROR(VLOOKUP(VLOOKUP(B2,'Build Definitions'!N:S,{1,2,3,4,5,6},FALSE),'Items Database'!A:B,2,FALSE),0))>12000,"Mid-Late Game","Mid Game"))
```

#### Penetration Effectiveness Rating (Row 13)
**Purpose**: How well does this build deal with MR?

```excel
=AVERAGE(
VLOOKUP(B2,'Build Definitions'!A:AA,27,FALSE),
VLOOKUP(B2,'Build Definitions'!A:AB,28,FALSE),
VLOOKUP(B2,'Build Definitions'!A:AC,29,FALSE)
)
```

## 🎮 Situational Analysis Formulas

### Best Item vs Target MR Calculator
**Purpose**: Which penetration item is optimal vs target MR?

```excel
=IF(Target_MR<45,"Shadowflame",
IF(Target_MR<65,"Either",
"Void Staff"))
```

### Build Path Efficiency Score
**Purpose**: How good is the build path for early power?

```excel
=(Component_Efficiency_Sum / Number_of_Items) * Build_Path_Smoothness_Factor
```

## 🔬 Advanced Passive Calculations

### Luden's Companion Damage Estimate
**Purpose**: Estimate Luden's proc damage per combo

```excel
=75 + (Total_AP * 0.05) + ((6-1) * (15 + Total_AP * 0.01))
```

### Liandry's Torment DPS Estimate
**Purpose**: Estimate burn damage over time

```excel
=(Target_HP * 0.012) * 3 * (1 + Additional_Damage_Multipliers)
```

### Rabadon's Effective AP Boost
**Purpose**: How much AP does Rabadon's actually add?

```excel
=Base_AP_Without_Rabadon * 0.4
```

### Void Staff Damage Increase Calculator
**Purpose**: Damage increase vs different MR values

```excel
=((100/(100+Original_MR)) / (100/(100+(Original_MR*0.6)))) - 1
```

## 📈 Performance Optimization Formulas

### Gold Per Damage Point (Enhanced)
**Purpose**: True efficiency including passive value

```excel
=Total_Build_Cost / (Theoretical_DPS + Passive_DPS_Estimate)
```

### Target Priority Score
**Purpose**: Which enemy should you focus based on your build?

```excel
=IF(Penetration_Rating>0.8,"Tanks",
IF(AP_Ratio>2.5,"Squishies",
"Balanced"))
```

### Build Completion Priority
**Purpose**: Which item to complete first?

```excel
=INDEX(Item_Names,MATCH(MAX(Efficiency_Per_Gold_Remaining),Efficiency_Per_Gold_Array,0))
```

## 🛠️ Helper Functions

### MR Breakpoint Calculator
**Purpose**: At what MR does Void Staff become better than Shadowflame?

```excel
=((Shadowflame_AP_Advantage * AP_Ratio) / (Void_Flat_Pen_Advantage)) + Base_MR_Threshold
```

### Optimal Item Order Suggestion
**Purpose**: Best item purchase order for your playstyle

```excel
=IF(Game_Time<15,"Early_Power_Items",
IF(Enemy_MR_Average>50,"Penetration_Items",
"AP_Scaling_Items"))
```

## 🔄 Dynamic Calculations

### Adaptive Penetration Calculator (Shadowflame)
**Purpose**: Calculate Shadowflame's actual penetration based on target HP

```excel
=MIN(20,MAX(10,20-(Target_Current_HP-1000)*0.01))
```

### Multiplicative Penetration Stack Calculator
**Purpose**: Calculate combined % penetration effects

```excel
=1-((1-Void_Staff_Pen)*(1-Boots_Pen)*(1-Other_Percent_Pen))
```

These formulas create a comprehensive damage calculation system that goes far beyond simple gold efficiency, providing real-world effectiveness analysis for your Hwei builds! 🎯