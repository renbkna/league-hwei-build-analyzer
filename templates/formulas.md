# Google Sheets Formulas Reference

Complete reference for all formulas used in the Hwei Build Analyzer.

## 📈 Build Definitions Tab Formulas

### Total Gold Cost (Column T)
**Purpose**: Calculates the sum of all 6 items' gold costs

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:B,2,FALSE),0))
```

**Explanation**:
- `N2:S2` - Range containing the 6 item names
- `'Items Database'!A:B` - Item names (column A) and costs (column B)
- `VLOOKUP(...,2,FALSE)` - Finds exact match and returns cost
- `IFERROR(...,0)` - Returns 0 if item not found
- `SUMPRODUCT()` - Sums all the costs

### Total Raw Stat Gold Value (Column U)
**Purpose**: Calculates the theoretical gold value of all stats provided by the 6 items

```excel
=SUMPRODUCT(IFERROR(VLOOKUP(N2:S2,'Items Database'!A:T,20,FALSE),0))
```

**Explanation**:
- Similar to cost formula but looks up column T (Total Raw Stat Gold Value)
- Column 20 corresponds to column T in the Items Database
- Each item's theoretical stat value is pre-calculated in the Items Database

### Gold Efficiency Percentage (Column V)
**Purpose**: Calculates efficiency as (Stat Value / Actual Cost) * 100%

```excel
=IF(T2=0,0,U2/T2)
```

**Explanation**:
- `IF(T2=0,0,...)` - Prevents division by zero
- `U2/T2` - Stat value divided by actual cost
- Result is decimal (0.98 = 98% efficiency)

## 📋 Dashboard Tab Formulas

### Build Selection Lookups
**Purpose**: Pulls data from Build Definitions based on selected build name

#### Total Gold Cost (Row 3)
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:T,20,FALSE),0)
```

#### Raw Stat Gold Value (Row 4)
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:U,21,FALSE),0)
```

#### Gold Efficiency % (Row 5)
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:V,22,FALSE),0)
```

### Performance Ratios
**Purpose**: Calculate efficiency metrics based on your testing data

#### DPS per 1000 Gold (Row 8)
```excel
=IF(AND(B6>0,B3>0),B6/B3*1000,0)
```

**Explanation**:
- `AND(B6>0,B3>0)` - Ensures both DPS and cost are positive
- `B6/B3*1000` - DPS divided by cost, multiplied by 1000 for readability
- Shows DPS per 1000 gold spent

#### Total Damage per 1000 Gold (Row 9)
```excel
=IF(AND(B7>0,B3>0),B7/B3*1000,0)
```

### Build Description (Row 10)
```excel
=IFERROR(VLOOKUP(B2,'Build Definitions'!A:B,2,FALSE),"")
```

## 🔍 Advanced Analysis Formulas

### Best DPS Build Identifier
**Purpose**: Automatically identifies which build has highest DPS

```excel
=INDEX(B2:D2,MATCH(MAX(B6:D6),B6:D6,0))
```

**Explanation**:
- `MAX(B6:D6)` - Finds highest DPS value
- `MATCH(...,B6:D6,0)` - Finds position of that maximum
- `INDEX(B2:D2,...)` - Returns build name at that position

### Most Gold Efficient Build
```excel
=INDEX(B2:D2,MATCH(MAX(B5:D5),B5:D5,0))
```

### Best DPS-per-Gold Build
```excel
=INDEX(B2:D2,MATCH(MAX(B8:D8),B8:D8,0))
```

## 🎨 Items Database Calculations

### Total Raw Stat Gold Value Formula (Column T)
**Purpose**: Calculates theoretical gold value for each item based on its stats

```excel
=D2*VLOOKUP("Ability Power",'Stat Gold Values'!A:B,2,FALSE) + 
F2*VLOOKUP("Health",'Stat Gold Values'!A:B,2,FALSE) + 
G2*VLOOKUP("Mana",'Stat Gold Values'!A:B,2,FALSE) + 
H2*VLOOKUP("Magic Resistance",'Stat Gold Values'!A:B,2,FALSE) + 
I2*VLOOKUP("Armor",'Stat Gold Values'!A:B,2,FALSE) + 
J2*VLOOKUP("Ability Haste",'Stat Gold Values'!A:B,2,FALSE) + 
K2*VLOOKUP("Magic Penetration %",'Stat Gold Values'!A:B,2,FALSE) + 
L2*VLOOKUP("Magic Penetration Flat",'Stat Gold Values'!A:B,2,FALSE)
```

**Simplified Version** (if you want to make it more manageable):
```excel
=D2*20 + F2*2.67 + G2*1 + H2*20 + I2*20 + J2*50 + K2*46.15 + L2*46.67
```

**Stat Multipliers**:
- AP: 20 gold per point
- Health: 2.67 gold per point
- Mana: 1 gold per point
- MR/Armor: 20 gold per point
- Ability Haste: 50 gold per point
- Magic Pen %: 46.15 gold per point
- Magic Pen Flat: 46.67 gold per point

## 🔄 Dynamic Reference Formulas

### Flexible Build Comparison
**Purpose**: Compare any number of builds dynamically

#### Average Gold Efficiency Across Selected Builds
```excel
=AVERAGE(B5:D5)
```

#### Standard Deviation of DPS
```excel
=STDEV(B6:D6)
```

#### Best Value Build (Highest DPS per Gold)
```excel
=INDEX(B2:D2,MATCH(MAX(B8:D8),B8:D8,0))
```

## 🛟 Formula Debugging Tips

### Common Issues and Solutions:

1. **#N/A Errors**:
   - Check exact spelling of item/build names
   - Verify tab names match exactly
   - Ensure VLOOKUP ranges include headers

2. **#DIV/0! Errors**:
   - Add IF statements to check for zero denominators
   - Example: `=IF(B3=0,0,B6/B3)`

3. **Wrong Calculations**:
   - Verify column numbers in VLOOKUP (1-indexed)
   - Check that stat gold values are correct
   - Ensure item stats are numbers, not text

### Formula Testing:
```excel
// Test individual VLOOKUP
=VLOOKUP("Luden's Companion",'Items Database'!A:B,2,FALSE)

// Test if cell contains number
=ISNUMBER(B3)

// Debug sum components
=D2&" AP = "&D2*20&" gold"
```

## 📉 Performance Optimization

### For Large Datasets:
1. Use `INDEX/MATCH` instead of `VLOOKUP` for better performance
2. Minimize volatile functions like `INDIRECT`
3. Use absolute references (`$A$1`) for lookup tables

### Example Optimized Formula:
```excel
// Instead of VLOOKUP
=INDEX('Items Database'!B:B,MATCH(N2,'Items Database'!A:A,0))

// Instead of multiple VLOOKUPs
=SUMPRODUCT(--(N2:S2<>""), 
  INDEX('Items Database'!B:B,MATCH(N2:S2,'Items Database'!A:A,0)))
```

These formulas provide the foundation for your comprehensive Hwei build analysis system! 🎯