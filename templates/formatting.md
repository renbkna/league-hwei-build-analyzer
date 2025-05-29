# Conditional Formatting Guide

Visual formatting rules to make your Hwei Build Analyzer intuitive and easy to read.

## 🎨 Gold Efficiency Color Coding

### Dashboard Gold Efficiency (Row 5)

**Setup Location**: Dashboard tab, cells B5:D5

#### Rule 1: Excellent Efficiency (Green)
- **Condition**: Custom formula is `=$B5>=1.1`
- **Format**: 
  - Background: Light green (#d9ead3)
  - Text: Dark green (#137333)
  - Bold text
- **Meaning**: ≥110% gold efficient (excellent value)

#### Rule 2: Good Efficiency (Light Green)
- **Condition**: Custom formula is `=AND($B5>=1,$B5<1.1)`
- **Format**:
  - Background: Very light green (#e8f5e8)
  - Text: Green (#0d8043)
- **Meaning**: 100-109% gold efficient (good value)

#### Rule 3: Poor Efficiency (Red)
- **Condition**: Custom formula is `=$B5<1`
- **Format**:
  - Background: Light red (#fce8e6)
  - Text: Dark red (#cc0000)
- **Meaning**: <100% gold efficient (needs passive value)

### Build Definitions Gold Efficiency (Column V)

**Setup Location**: Build Definitions tab, cells V2:V100

**Same rules as Dashboard**, but applied to the entire efficiency column.

## 📈 Performance Indicators

### DPS Rankings

**Setup Location**: Dashboard tab, cells B6:D6 (Your Calculated DPS)

#### Highest DPS (Gold)
- **Condition**: Custom formula is `=$B6=MAX($B$6:$D$6)`
- **Format**:
  - Background: Gold (#fff2cc)
  - Text: Dark orange (#e69138)
  - Bold text

#### Above Average DPS (Light Blue)
- **Condition**: Custom formula is `=$B6>AVERAGE($B$6:$D$6)`
- **Format**:
  - Background: Light blue (#cfe2f3)
  - Text: Blue (#1155cc)

### DPS per Gold Rankings

**Setup Location**: Dashboard tab, cells B8:D8

#### Best Value (Dark Green)
- **Condition**: Custom formula is `=$B8=MAX($B$8:$D$8)`
- **Format**:
  - Background: Dark green (#b6d7a8)
  - Text: White (#ffffff)
  - Bold text

#### Good Value (Light Green)
- **Condition**: Custom formula is `=$B8>AVERAGE($B$8:$D$8)`
- **Format**:
  - Background: Light green (#d9ead3)
  - Text: Dark green (#137333)

## 📀 Cost Analysis

### Total Gold Cost Indicators

**Setup Location**: Dashboard tab, cells B3:D3

#### Expensive Build (Red)
- **Condition**: Custom formula is `=$B3>=17000`
- **Format**:
  - Background: Light red (#fce8e6)
  - Text: Dark red (#cc0000)
- **Meaning**: Very expensive build (>17,000g)

#### Moderate Cost (Yellow)
- **Condition**: Custom formula is `=AND($B3>=15000,$B3<17000)`
- **Format**:
  - Background: Light yellow (#fff2cc)
  - Text: Dark orange (#bf9000)
- **Meaning**: Moderately expensive (15,000-17,000g)

#### Budget Build (Green)
- **Condition**: Custom formula is `=$B3<15000`
- **Format**:
  - Background: Light green (#d9ead3)
  - Text: Dark green (#137333)
- **Meaning**: Budget-friendly build (<15,000g)

## 🏆 Build Comparison Highlights

### Winning Categories

#### Best in Category Highlighting
For each metric row (3-9), highlight the best performing build:

**Gold Efficiency Winner** (Row 5):
- **Condition**: `=$B5=MAX($B$5:$D$5)`
- **Format**: 🏆 Gold star (use custom number format)

**DPS Winner** (Row 6):
- **Condition**: `=$B6=MAX($B$6:$D$6)`
- **Format**: Bold + Gold background

**Best Value Winner** (Row 8):
- **Condition**: `=$B8=MAX($B$8:$D$8)`
- **Format**: Bold + Green background

## 📅 Data Quality Indicators

### Missing Data Highlights

#### Incomplete Builds
**Setup Location**: Build Definitions tab, columns N:S (items)
- **Condition**: Cell is empty
- **Format**:
  - Background: Light gray (#f3f3f3)
  - Text: Gray (#666666)
  - Italic text

#### Missing Performance Data
**Setup Location**: Dashboard tab, cells B6:D7 (DPS/Damage inputs)
- **Condition**: Cell value = 0 or empty
- **Format**:
  - Background: Light orange (#fce8b6)
  - Text: Orange (#bf9000)
  - Italic text
- **Meaning**: Needs testing data input

## 🔢 Number Formatting

### Currency Formatting

#### Gold Costs
**Apply to**: All gold cost cells (B3:D3, T column, etc.)
- **Format**: Custom `"G "#,##0`
- **Example**: "G 15,850" instead of "15850"

#### Gold Efficiency Percentages
**Apply to**: All efficiency cells (B5:D5, V column)
- **Format**: Percentage with 1 decimal place
- **Example**: "98.5%" instead of "0.985"

### Performance Metrics

#### DPS Values
**Apply to**: DPS input cells (B6:D6)
- **Format**: Number with commas
- **Example**: "2,847" instead of "2847"

#### Ratios
**Apply to**: DPS per Gold, Damage per Gold (B8:D9)
- **Format**: Number with 1 decimal place
- **Example**: "177.2" instead of "177.234567"

## 🎨 Advanced Formatting Techniques

### Data Bars

#### Gold Cost Comparison
**Apply to**: Dashboard row 3 (B3:D3)
- Insert → Chart → Data bars
- Color: Blue gradient
- Shows relative cost differences visually

#### DPS Comparison
**Apply to**: Dashboard row 6 (B6:D6)
- Data bars with green gradient
- Makes performance differences obvious

### Icon Sets

#### Efficiency Rating Icons
**Apply to**: Dashboard row 5 (B5:D5)
- **Icon Set**: 3 Traffic Lights
- **Green**: ≥100% efficiency
- **Yellow**: 90-99% efficiency  
- **Red**: <90% efficiency

#### Value Rating Icons
**Apply to**: Dashboard row 8 (B8:D8)
- **Icon Set**: 3 Stars
- **3 Stars**: Highest DPS per gold
- **2 Stars**: Middle value
- **1 Star**: Lowest value

## 🔧 Setup Instructions

### How to Apply Conditional Formatting:

1. **Select target range** (e.g., B5:D5)
2. **Format → Conditional formatting**
3. **Choose condition type**:
   - "Custom formula is" for complex rules
   - "Greater than" for simple comparisons
4. **Enter formula** (e.g., `=$B5>=1`)
5. **Set formatting** (colors, bold, etc.)
6. **Click "Done"**
7. **Repeat for additional rules**

### Pro Tips:

- **Use absolute references** (`$B$5`) for ranges that shouldn't change
- **Use relative references** (`$B5`) when you want rules to apply to each column
- **Layer rules** from most specific to most general
- **Test rules** by changing values to see if formatting updates

### Rule Priority:
Google Sheets applies formatting rules in order. More specific rules should come first:
1. Exact matches (="Specific Value")
2. Range conditions (>1.1, <0.9)
3. General conditions (>1, <1)

This formatting system will make your build analyzer both functional and visually intuitive! 🎆