# Gold Efficiency Methodology

Detailed explanation of how gold efficiency is calculated and interpreted in League of Legends.

## 📊 What is Gold Efficiency?

Gold efficiency is a **theoretical metric** that compares an item's statistical value to its purchase cost. It answers the question: "How much bang am I getting for my buck?"

### Formula:
```
Gold Efficiency % = (Theoretical Stat Value / Actual Item Cost) × 100%
```

### Example:
**Amplifying Tome**:
- Cost: 400 gold
- Stats: 20 AP
- Stat Value: 20 AP × 20 gold/AP = 400 gold
- Efficiency: 400/400 = 100%

## 📈 Reference Values (Patch 14.21)

These gold values are derived from the cheapest basic items that provide each stat:

| Stat | Gold Value | Reference Item | Notes |
|------|------------|----------------|---------|
| **Ability Power** | 20g per point | Amplifying Tome | Core mage stat |
| **Health** | 2.67g per point | Ruby Crystal | Effective HP scaling |
| **Mana** | 1g per point | Sapphire Crystal | Sustain for casting |
| **Armor** | 20g per point | Cloth Armor | Physical damage reduction |
| **Magic Resist** | 20g per point | Null-Magic Mantle | Magic damage reduction |
| **Ability Haste** | 50g per point | Glowing Mote | Cooldown reduction |
| **Magic Pen %** | 46.15g per point | Blighting Jewel | Percentage penetration |
| **Magic Pen Flat** | 46.67g per point | Sorcerer's Shoes | Flat penetration |
| **Movement Speed** | 12g per point | Boots | Mobility |

## 🎨 Interpreting Efficiency Ratings

### 100%+ Efficient (Gold Efficient)
- **Meaning**: Item provides stats worth more than its cost
- **Example**: Needlessly Large Rod (60 AP for 1250g = 96% base + passive value)
- **Implication**: Good statistical value, even ignoring passive effects

### 90-99% Efficient (Near Efficient)
- **Meaning**: Slightly below statistical cost, but passive likely compensates
- **Example**: Many legendary items fall here due to powerful passives
- **Implication**: Acceptable value if passive effect is strong

### <90% Efficient (Stat Inefficient)
- **Meaning**: Poor statistical value, must have very strong passive/active
- **Example**: Items with unique effects like Zhonya's Hourglass
- **Implication**: Purchased for utility, not raw stats

## 🚯️ Important Limitations

### What Gold Efficiency DOESN'T Account For:

1. **Passive/Active Effects**
   - Luden's Echo damage
   - Zhonya's Stasis active
   - Rabadon's 35% AP amplification

2. **Synergistic Effects**
   - How items work together
   - Build path efficiency
   - Power spike timing

3. **Situational Value**
   - Magic penetration vs high MR targets
   - Defensive stats vs specific team comps
   - Utility effects (slows, shields, etc.)

4. **Champion Scaling**
   - How well stats work with Hwei's kit
   - Ability ratios and base damages
   - Playstyle optimization

## 🎯 Practical Applications for Hwei

### Build Comparison
**Use Case**: Comparing two similar builds
- Build A: 98% efficiency, 2,847 DPS
- Build B: 104% efficiency, 2,654 DPS
- **Analysis**: Build A provides better actual performance despite lower efficiency

### Item Selection
**Use Case**: Choosing between similar items
- Void Staff: High efficiency vs high MR targets
- Shadowflame: Lower base efficiency but adaptive penetration
- **Decision**: Depends on enemy team composition

### Budget Optimization
**Use Case**: Maximizing power with limited gold
- Focus on high base efficiency items early
- Add specialized/passive items later
- Balance cost vs immediate power needs

## 📏 Advanced Calculations

### Build-Wide Efficiency
```
Total Build Efficiency = 
(Sum of all item stat values) / (Sum of all item costs)
```

### Weighted Efficiency
Some stats may be more valuable for Hwei than others:

```
Weighted Efficiency = 
(AP_Value × AP_Weight + Health_Value × Health_Weight + ...) / Total_Cost
```

**Example Hwei Weights**:
- AP: 1.0 (full value)
- Magic Pen: 1.2 (high value vs resistances)
- Health: 0.8 (moderate value for positioning)
- Ability Haste: 0.9 (good value for combo frequency)

### Real Performance Integration
```
Performance Efficiency = 
(Actual DPS or Damage) / (Total Build Cost)
```

This accounts for how the build actually performs, not just theoretical stats.

## 📉 Historical Context

### Why These Values?
Gold values are derived from **basic items** - the simplest items that provide each stat:
- **Amplifying Tome**: 20 AP for 400g → 20g per AP
- **Ruby Crystal**: 150 HP for 400g → 2.67g per HP
- **Long Sword**: 10 AD for 350g → 35g per AD

### Evolution Over Time
- Patch updates can change basic item costs
- New items can introduce new stat combinations
- Meta shifts affect which stats are most valuable

## 🔍 Case Studies: Hwei Items

### Luden's Companion Analysis
- **Cost**: 2,850g
- **Stats**: 100 AP + 600 Mana + 10 AH
- **Stat Value**: (100×20) + (600×1) + (10×50) = 3,100g
- **Base Efficiency**: 3,100/2,850 = 108.8%
- **Plus**: Echo passive (significant damage)
- **Verdict**: Excellent efficiency + strong passive

### Rabadon's Deathcap Analysis
- **Cost**: 3,600g
- **Stats**: 120 AP
- **Stat Value**: 120×20 = 2,400g
- **Base Efficiency**: 2,400/3,600 = 66.7%
- **Plus**: 35% AP amplification (massive scaling)
- **Verdict**: Low base efficiency, but passive transforms entire build

### Zhonya's Hourglass Analysis
- **Cost**: 3,250g
- **Stats**: 80 AP + 45 Armor + 10 AH
- **Stat Value**: (80×20) + (45×20) + (10×50) = 2,900g
- **Base Efficiency**: 2,900/3,250 = 89.2%
- **Plus**: Stasis active (game-changing utility)
- **Verdict**: Near-efficient stats + unique defensive tool

## 🏆 Optimization Strategies

### Early Game (0-15 minutes)
Focus on **high base efficiency** items:
- Lost Chapter components
- Basic AP items
- Mana sustain

### Mid Game (15-25 minutes)
Balance **efficiency with power spikes**:
- Complete first legendary
- Add penetration if needed
- Consider defensive options

### Late Game (25+ minutes)
Prioritize **multiplicative effects**:
- Rabadon's for AP scaling
- Void Staff for penetration
- Situational utility items

## 📄 Summary

Gold efficiency is a **valuable starting point** for item analysis, but shouldn't be the only factor in build decisions. It's most useful when:

1. **Comparing similar items** with different stat distributions
2. **Evaluating budget builds** for maximum early power
3. **Understanding item value** relative to cost

For Hwei specifically, combine gold efficiency analysis with actual DPS testing to make optimal build decisions that perform well in real games.

**Remember**: The best build is the one that wins games, not necessarily the one with the highest efficiency percentage! 🏆