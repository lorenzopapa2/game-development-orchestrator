# Balance And Economy

## Goal

Design the numerical foundation of the game: combat math, economic loops, progression curves, probability systems, and difficulty tuning. This module produces the formulas, tables, and parameter frameworks that make gameplay feel fair, rewarding, and deep — without generating code.

## Relationship to Data Models

This file provides **design methodology** — how to think about balance, which frameworks to use, and what templates to fill out. For the **exact mathematical formulas** (EHP calculation, PRD constants, Lanchester's laws, exponential curve parameters), always cross-reference [data_models/economy_and_progression.md](data_models/economy_and_progression.md). Use the formulas from data_models to populate the tables and frameworks in this file.

## When To Use

- After strategy and genre are locked: balance needs a core loop to attach to
- Before level design: difficulty curves inform encounter composition
- Before production art: power tiers affect visual escalation
- During playtesting: use these frameworks to diagnose and fix feel problems
- When the user says "design the numbers" or "make a stat system"

---

## Combat Numerics Framework

### Damage Formula Archetypes

Choose one as a starting point based on genre needs:

**Subtractive (Armor reduces flat damage)**
```
final_damage = base_damage - armor
```
- Simple, intuitive, good for low-number games
- Risk: high armor trivializes low-damage attacks
- Best for: turn-based RPG, strategy, low-complexity action

**Multiplicative (Armor as damage reduction percentage)**
```
final_damage = base_damage × (1 - armor_reduction%)
```
- Smooth scaling, never fully negates damage
- Risk: stacking reduction reaches near-immunity
- Best for: action RPG, shooters, survival

**Scaling (Armor vs. damage in a ratio formula)**
```
final_damage = base_damage × base_damage / (base_damage + armor)
```
- Self-balancing: damage and armor grow together
- Risk: harder for players to intuit
- Best for: deep RPGs, MMO-adjacent, long-progression games

**Threshold (Damage types vs. armor types)**
```
if damage_type counters armor_type: final_damage = base_damage × 1.5
elif armor_type counters damage_type: final_damage = base_damage × 0.5
else: final_damage = base_damage
```
- Strategic layer through type matchups
- Risk: complexity explosion with many types
- Best for: Pokemon-like, tactical RPG, card games

### TTK (Time To Kill) Design

| Context | Target TTK | Why |
|---------|-----------|-----|
| PvP competitive | 0.5-2s | Rewards aim and positioning |
| PvP tactical | 1-5s | Allows reaction and counterplay |
| PvE action | 3-15s per common enemy | Satisfying combat loop without tedium |
| PvE boss | 60-300s | Sustained engagement with phase variety |
| Turn-based RPG (common) | 2-4 turns | Quick resolution, many encounters |
| Turn-based RPG (boss) | 8-20 turns | Strategic depth with resource pressure |

### Variance and Critical Systems

- **Crit rate**: 5-15% base for most genres; higher for builds that specialize
- **Crit multiplier**: 1.5x-2.5x; higher values need lower crit rates
- **Damage variance**: ±5-10% adds feel without unpredictability; ±20%+ adds excitement but frustration
- **Miss chance**: Generally avoid in action games; acceptable in turn-based if feedback is clear
- **Proc rates**: Rare effects at 5-10%, build-enabling effects at 15-30%

---

## Economic System Design

### Source-Sink Analysis

Map every currency in the game:

| Currency | Sources (Income) | Sinks (Spending) | Target Flow |
|----------|-----------------|-------------------|-------------|
| Gold | Combat drops, quest rewards, selling items | Shop purchases, upgrades, repair | Slight surplus early, balanced mid, deficit late |
| Premium | IAP, rare rewards, battle pass | Cosmetics, convenience, gacha | Carefully gated, never required |
| Crafting mats | Gathering, disassembly, drops | Equipment crafting, upgrades | Always slightly scarce to maintain motivation |

### Soft vs. Hard Currency

- **Soft currency**: Earned freely through gameplay; main economic flow
- **Hard currency**: Premium or extremely scarce; purchases with real perceived value
- Rule: never let soft currency buy what hard currency buys, or hard currency loses value
- F2P rule: soft currency should never feel adequate alone; hard currency should never be mandatory

### Wealth Projection Table

Model expected player wealth over time:

| Timeframe | Session Income | Cumulative Wealth | Key Purchases Available | Engagement Check |
|-----------|---------------|-------------------|------------------------|-----------------|
| D1 | X gold | X total | Starter equipment, first upgrade | Can player afford the first meaningful purchase? |
| D3 | Y gold/session | Z total | Second tier equipment, first cosmetic | Is there a clear next goal? |
| D7 | Scaled | Total | Mid-tier unlocks | Are players still finding new things to buy? |
| D14 | Scaled | Total | Advanced content | Is wealth outpacing content? |
| D30 | Scaled | Total | Endgame purchases | Is there still economic motivation? |

### Shop Price Curve

- Price should grow faster than income but slower than power gain
- Pricing formula: `price = base_price × tier_multiplier^tier × inflation_factor`
- Player should always have 1-2 affordable goals and 1-2 aspirational goals visible

---

## Gacha / Probability Systems

### Pity System Design

| Parameter | Recommendation | Reasoning |
|-----------|---------------|-----------|
| Soft pity start | 60-75% of hard pity | Gradually increasing rates feel rewarding |
| Hard pity (guaranteed) | 70-90 pulls for top rarity | Sets maximum spend/grind ceiling |
| Base top-rarity rate | 0.5-1.5% | Low enough to feel exciting, high enough to not feel impossible |
| Rate-up percentage | 50-75% of top rarity | Targeted farming should be viable |
| Duplicate handling | Convert to universal currency or power-up material | Never feel wasted |

### Expected Pull Calculations

Define for each banner type:
- Expected pulls for one copy of target: `1 / rate` with pity adjustment
- Expected pulls for max copies: `copies × expected_per_copy × 0.85` (pity discount)
- F2P monthly pull income vs. expected cost — player should be able to get at least one target per patch cycle

### Rarity Power Budget

| Rarity | Power Budget (1-10) | Availability | Design Role |
|--------|---------------------|-------------|-------------|
| Common | 2-3 | Free, abundant | Baseline functionality |
| Uncommon | 3-5 | Easy to obtain | Core of most builds |
| Rare | 5-7 | Moderate effort | Enables specific strategies |
| Epic | 7-8 | Significant effort/luck | Build-defining |
| Legendary | 8-10 | Very rare or guaranteed via pity | Aspirational, meta-shaping |

Rule: rarity should primarily affect strategic breadth, not raw power. A common at max level should be viable; a legendary should enable more options.

---

## Progression Curves

### Experience Curve Shapes

**Linear**: `XP_required = base + level × increment`
- Simple, predictable; good for short games
- Risk: late levels feel the same effort as early levels

**Polynomial**: `XP_required = base × level^exponent`
- Natural feeling; exponent 1.5-2.5 typical
- Best for: RPGs, most progression games

**Exponential**: `XP_required = base × multiplier^level`
- Aggressive slowing; good for prestige/idle systems
- Risk: late levels feel impossible without boosts

**Stepped**: Different curves per tier
- Control pacing precisely at tier transitions
- Best for: games with gear tiers or story acts

### Level-Up Cadence Targets

| Game Phase | Target Level-Up Frequency | Design Goal |
|-----------|--------------------------|-------------|
| Tutorial (1-5) | Every 5-10 minutes | Rapid reward, teach upgrade system |
| Early game (5-15) | Every 15-30 minutes | Establish growth feeling |
| Mid game (15-30) | Every 30-60 minutes | Meaningful decisions per level |
| Late game (30-50) | Every 1-3 hours | Mastery, build completion |
| Endgame (50+) | Every 3-8 hours | Long-term goals, prestige |

### Ability/Unlock Pacing

- New mechanic every 3-5 levels in early game; every 5-10 in mid/late
- Each unlock should change how the player plays, not just add numbers
- Talent/skill tree point budget: total points = 60-70% of total tree — force meaningful choices
- Respec cost: free or low early (encourage experimentation), moderate later (commitment matters)

### Power Curve Guidelines

- Player power should grow 10-20x from start to endgame for most RPGs
- Enemy power should grow alongside but with intentional gaps (challenge zones)
- New equipment should feel like a 10-20% upgrade per tier, not 2x
- Avoid: linear stat growth with exponential enemy scaling (creates walls)

---

## Difficulty Design

### Difficulty Curve Archetypes

**Linear Ramp**
- Steady, predictable increase
- Best for: puzzle games, casual experiences
- Risk: lacks excitement peaks

**Sawtooth**
- Rising difficulty → relief zone → rising again
- Best for: action games, platformers
- Creates natural session break points

**Staircase with Spikes**
- Plateaus of consistent difficulty → sudden boss/test → new plateau
- Best for: RPGs, metroidvanias, roguelikes
- Spikes serve as skill gates

**Adaptive (DDA)**
- System adjusts difficulty based on player performance
- Parameters: recent death count, completion speed, damage taken ratio
- Best for: broad-audience games, accessibility-focused design
- Risk: rubber-banding feels unfair if too aggressive

### Difficulty Mode Parameters

When offering difficulty settings, adjust these (not just enemy HP):

| Parameter | Easy | Normal | Hard |
|-----------|------|--------|------|
| Enemy damage | 0.5x-0.7x | 1.0x | 1.3x-1.5x |
| Enemy HP | 0.7x-0.8x | 1.0x | 1.2x-1.5x |
| Enemy aggression | Lower | Normal | Higher |
| Resource availability | 1.3x-1.5x | 1.0x | 0.7x-0.8x |
| Checkpoint frequency | More | Normal | Fewer |
| Parry/dodge window | +3-5 frames | Normal | -2-3 frames |
| Hint availability | Generous | Normal | Minimal |

### Difficulty Validation Questions

- Can a new player complete the tutorial without dying?
- Does the player ever feel stuck for more than 3 attempts without progress?
- Is there always a way to get stronger if the challenge feels too hard?
- Do skilled players have a way to engage with higher challenges?
- Are difficulty spikes intentional design or accidental number inflation?

---

## Numerical Validation Framework

### Spreadsheet Simulation Structure

Create tables that model player progression:

| Level | HP | ATK | DEF | DPS | Enemy HP | Enemy ATK | Turns to Kill | Turns to Die | Margin |
|-------|----|-----|-----|-----|----------|-----------|---------------|-------------|--------|
| 1 | 100 | 10 | 5 | 8 | 30 | 8 | 4 | 15 | Safe |
| 5 | 150 | 18 | 10 | 14 | 80 | 15 | 6 | 12 | Comfortable |
| 10 | 220 | 30 | 18 | 24 | 180 | 28 | 8 | 10 | Tight |

### Key Metrics To Track

- **Player vs. Enemy TTK ratio**: Should favor player except at boss encounters
- **Resource surplus/deficit per session**: Slight surplus = satisfying, deficit = frustrating
- **Time to next meaningful upgrade**: Should always be visible and achievable
- **Build diversity at endgame**: Multiple viable paths or one dominant strategy?
- **Comeback potential**: Can a losing player recover through skill or smart play?

### Red Flag Signals

- Player TTK on common enemies exceeds 10 seconds and is not a boss
- Single stat or build dominates all content with no drawback
- Economy has no meaningful sinks — player wealth spirals
- Level-up provides no perceptible power increase
- Difficulty doubles between consecutive stages without new tools given to the player
- Proc/crit variance determines outcome more than player skill
- Pity system average exceeds 2 months of F2P income

---

## Genre-Specific Balance Templates

### RPG Attribute Table Template

| Attribute | Effect | Growth per Level | Cap | Scaling Formula |
|-----------|--------|-----------------|-----|-----------------|
| STR | Melee damage, carry weight | +2-3 | 99 | `damage_bonus = STR × 0.5 + weapon_base` |
| DEX | Attack speed, dodge rate | +1-2 | 99 | `dodge% = DEX × 0.3, cap 60%` |
| INT | Magic damage, mana pool | +2-3 | 99 | `magic_damage = INT × 0.7 + spell_base` |
| VIT | HP, defense | +3-5 | 99 | `HP = 100 + VIT × 8` |
| LCK | Crit rate, drop rate | +1 | 50 | `crit% = 5 + LCK × 0.2` |

### Roguelike Item Power Budget Template

| Relic Tier | Power Score | Max Copies | Example Effect |
|-----------|-------------|------------|----------------|
| Common | 1-2 | 3 | +10% damage, +1 speed |
| Uncommon | 3-4 | 2 | Projectile pierces +1, heal on kill |
| Rare | 5-6 | 1 | Double shot, lifesteal |
| Boss | 7-8 | 1 | Transform mechanic, new ability |
| Secret | 9-10 | 1 | Build-defining, game-warping |

Run power budget: average run should accumulate 20-30 power points; a "broken run" reaches 40-50.

### Tower Defense DPS/Cost Table Template

| Tower | Base DPS | Cost | DPS/Cost | Range | Special | Upgrade Path |
|-------|---------|------|----------|-------|---------|-------------|
| Arrow | 10 | 100 | 0.10 | Medium | None | Speed → Multi-shot |
| Cannon | 25 | 250 | 0.10 | Short | AoE splash | Damage → Range |
| Ice | 5 | 150 | 0.03 | Medium | Slow 30% | Slow% → Freeze |
| Sniper | 40 | 400 | 0.10 | Long | Single target | Crit → Armor pierce |
| Support | 0 | 200 | N/A | Medium | +20% nearby DPS | Range → Buff% |

Note: DPS/Cost ratio should be similar for pure damage towers; utility towers earn value through synergy.

### Card Game Mana Curve Template

| Mana Cost | Typical Stats | Card Budget Points | Expected Cards in Deck |
|-----------|-------------|-------------------|----------------------|
| 1 | 1/1 or minor effect | 2-3 | 6-8 |
| 2 | 2/2 or moderate effect | 4-5 | 6-8 |
| 3 | 3/3 or strong effect | 6-7 | 4-6 |
| 4 | 4/4 or powerful effect | 8-9 | 3-5 |
| 5+ | 5/5+ or game-changing | 10+ | 2-4 |

Deck total: 30-60 cards typical; mana curve should peak at 2-3 cost.
