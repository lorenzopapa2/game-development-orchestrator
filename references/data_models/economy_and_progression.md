# Game Economy & Progression Mathematical Models

This file contains the foundational mathematical models required for expert-level game balancing. When designing a game, you MUST align the numerical output with these proven systems rather than using arbitrary numbers.

For design methodology, templates, and genre-specific balance tables, see [../balance-economy.md](../balance-economy.md).

## 1. Combat & Damage Formulas

### 1.1 Effective Health Pool (EHP) / Armor Mitigation
Used in: RPGs, MOBAs, Hero Shooters, Strategy games.
- **Formula (League of Legends/Warcraft 3 style):** `Damage Taken = Raw Damage * ( C / (C + Armor) )`
  - *C is a constant (often 100).*
  - *Why use this:* Every point of armor adds the same amount of EHP, preventing exponential scaling of defense.
  - *EHP calculation:* `EHP = HP * (1 + Armor / C)`
  - *Design implication:* At Armor = C, damage is halved. At Armor = 2C, damage is 1/3. Linear EHP growth.

### 1.2 Subtraction Model
Used in: Tactical RPGs (Fire Emblem), Board Games.
- **Formula:** `Damage Taken = MAX(1, Raw Damage - Defense)`
  - *Why use this:* Easy for players to calculate mentally. Requires strict bounded scaling, otherwise defense completely nullifies low damage (0 damage problem).
  - *Safe range:* Keep `max_defense < 0.7 * max_attack` to prevent nullification.

### 1.3 Multiplicative Reduction (Percentage-Based)
Used in: Action RPGs (Diablo, Path of Exile), Survival games.
- **Formula:** `Damage Taken = Raw Damage * (1 - Reduction%)`
  - *Stacking rule:* Multiple sources stack multiplicatively, not additively: `Total = 1 - ((1-R1) * (1-R2) * (1-R3))`
  - *Why multiplicative:* Prevents 100% damage immunity through stacking.
  - *Design ceiling:* Cap effective reduction at 75-90% to maintain damage relevance.

### 1.4 Type Effectiveness Matrix
Used in: Pokemon-like, tactical RPGs, elemental combat.
- **Formula:** `Damage = Base * TypeMultiplier[attack_type][defense_type]`
  - Standard multipliers: Super effective = 2.0, Neutral = 1.0, Not effective = 0.5, Immune = 0.0
  - *Constraint:* With N types, you need an N×N matrix. Keep N ≤ 8 for player comprehension.
  - *Balance rule:* Each type should have equal count of strengths and weaknesses.

### 1.5 TTK (Time To Kill) Reference Values
| Context | TTK Target | Formula Verification |
|---------|-----------|---------------------|
| PvP twitch shooter | 0.3-0.8s | `TTK = EHP / DPS` |
| PvP tactical | 1-3s | Player must have time to react |
| PvE fodder enemy | 1-3s | Fast resolution, many encounters |
| PvE standard enemy | 3-10s | Satisfying fight, not tedious |
| PvE elite enemy | 15-45s | Demands resource commitment |
| PvE boss (action) | 60-300s | Multi-phase, learn and adapt |
| Turn-based common | 2-3 turns | Quick tactical resolution |
| Turn-based boss | 8-20 turns | Strategic depth, resource pressure |

## 2. Progression & Pacing Curves

### 2.1 Exponential Growth (The Standard RPG Curve)
Used for: Level XP requirements, late-game gold costs.
- **Formula:** `Cost(Level n) = Base_Cost * (Multiplier ^ (n - 1))`
  - *Multiplier range:* 1.15 to 1.25 (gentle) to 1.5+ (aggressive/idle games)
  - *Creates:* Fast early game, massive grind in late game.
  - *Verification:* Total cumulative XP at level N = `Base * (M^N - 1) / (M - 1)`

### 2.2 Polynomial / Quadratic Growth (Smooth Scaling)
Used for: Stat gains per level, skill point costs, upgrade costs.
- **Formula:** `Cost(Level n) = Base + a*(n^2) + b*n`
  - Typical: `a = 5-20, b = 10-50`, tuned per game feel.
  - *Why use this:* Prevents stats from exploding into billions too quickly, keeping numbers readable while still rewarding progress.
  - *Power law variant:* `Stat(n) = Base * n^exponent` where exponent 0.5-0.8 gives diminishing returns.

### 2.3 Logarithmic Growth (Diminishing Returns)
Used for: Stat soft caps, diminishing investment returns.
- **Formula:** `Bonus = k * ln(1 + investment / c)`
  - *Why use this:* Natural soft cap — each additional point gives less benefit.
  - *Good for:* Preventing any single stat from dominating through over-investment.

### 2.4 S-Curve / Sigmoid (Bounded Growth)
Used for: Skill-based ratings (Elo), adaptive difficulty parameters.
- **Formula:** `Output = L / (1 + e^(-k*(x - x0)))`
  - L = maximum value, k = steepness, x0 = midpoint.
  - *Why use this:* Naturally bounded between 0 and L, fast change near midpoint, slow at extremes.

### 2.5 Idle/Incremental Scaling
Used for: Idle games, prestige systems.
- **Prestige multiplier:** `Bonus = 1 + sqrt(LifetimeEarnings / PrestigeConstant)`
  - *Design rule:* Each prestige should feel like 2-5x faster for the first 50% of previous progress.
- **Offline earnings:** `OfflineGain = OnlineRate * OfflineDuration * OfflineMultiplier`
  - *OfflineMultiplier:* 0.25-0.75 (reward engagement, don't punish absence excessively).

## 3. Economy Balancing (Sinks and Sources)

### 3.1 Faucet-Sink Flow Analysis
Every economy must have:
1. **Sources (Faucets):** Where value enters the system (Mob drops, daily quests, time-based regen).
2. **Sinks (Drains):** Where value leaves permanently (Consumables, repair costs, gacha pulls, cosmetic sinks).
3. **Converters:** Turning Resource A into Resource B (Crafting).

**Expert Rule:** When generating an economy design, you MUST provide a table balancing `Hourly Source Expected Value (EV)` against `Hourly Sink EV` for the average player.

### 3.2 Wealth Equilibrium Formula
- **Target:** `Source_Rate * PlayTime = Sink_Rate * PlayTime + Desired_Surplus`
- **Healthy economy:** Player accumulates wealth slowly (surplus = 5-15% of income)
- **Inflation check:** If total server/player wealth grows >20% per week without new sinks, the economy will collapse.
- **Price curve:** `Price(tier) = BaseCost * TierMultiplier^tier` where TierMultiplier = 1.5-3.0.

### 3.3 Shop Pricing Formula
- **Sell-back ratio:** Items sell for 25-50% of buy price (standard sink).
- **Opportunity cost rule:** Most expensive item available should cost 3-8 hours of focused play.
- **Aspirational item:** One visible item should cost 20-40 hours (long-term goal).

## 4. Gacha & Probability (RNG)

### 4.1 True Random vs. Pseudo-Random Distribution (PRD)
- Never use True Random for critical hits or gacha pity drops unless the intended experience is gambling.
- **PRD Rule:** Start the probability lower than stated, but increase it by a factor `C` on every failure. Resets on success. (e.g., Dota 2 crits).
- **PRD Formula:** `P(n) = min(1, C * n)` where C is calibrated so average proc rate matches stated %.
  - For 25% stated rate: C ≈ 0.0847
  - For 15% stated rate: C ≈ 0.0322
  - For 5% stated rate: C ≈ 0.003802

### 4.2 Pity System Mathematics
- **Soft pity:** At pull N, rate increases linearly: `Rate(n) = BaseRate + (n - SoftPityStart) * RateIncrease`
  - Typical: soft pity at 60-75% of hard pity, rate increase = 5-10% per pull.
- **Hard pity (guarantee):** At pull N, rate = 100%.
  - Typical: 70-90 pulls for highest rarity.
- **Expected pulls for one copy:** `E[pulls] = Σ(n * P(n on this pull)) ≈ 0.6-0.8 * HardPity` for well-designed systems.
- **Duplicate value:** Convert to universal currency at 15-25% of pull cost to prevent feel-bad moments.

### 4.3 Loot Table Weighting
- **Formula:** `DropChance(item) = item_weight / Σ(all_weights)`
- **Rarity weight ratios (typical):** Common 100 : Uncommon 30 : Rare 10 : Epic 3 : Legendary 1
- **Guaranteed minimum:** After N drops with no rare+, force-upgrade next drop. Prevents frustration streaks.

## 5. Lanchester's Laws (RTS/Strategy Balancing)

### 5.1 Linear Law (Ancient Combat / Melee Chokepoints)
- Fighting strength is proportional to: `Quality * Quantity`
- *Applies when:* Units fight 1v1 in sequence (narrow corridors, chokepoints).
### 5.2 Square Law (Modern Combat / Ranged Focus Fire)
- Fighting strength is proportional to: `Quality * (Quantity ^ 2)`
- *Expert takeaway for Strategy Games:* Ranged units scale quadratically. You must artificially nerf their HP or movement speed compared to melee units to prevent ranged deathballs.
- **Counter-design:** Give melee units gap-closers, AoE, or positional advantages (high ground).

### 5.3 Resource Exchange Ratio
- **Formula:** `ExchangeRatio = (CostA * UnitsA_Lost) / (CostB * UnitsB_Lost)`
- *Design target:* Counter units should achieve 2:1-3:1 exchange ratio vs. their target.
- *Hard counter ceiling:* Never exceed 5:1 — makes the countered unit feel useless.

## 6. Dynamic Difficulty Adjustment (DDA)

### 6.1 Performance-Based DDA
- **Input metrics:** Recent death count, completion time ratio, damage taken ratio, resource usage efficiency.
- **Adjustment formula:** `DifficultyMod = clamp(BaseDifficulty + (PerformanceScore - TargetScore) * Sensitivity, MinDiff, MaxDiff)`
- **Sensitivity:** 0.1-0.3 (subtle), 0.3-0.6 (moderate), 0.6+ (aggressive, risks rubber-banding feel).
- **Hysteresis:** Apply difficulty changes with a 2-3 encounter delay to avoid whiplash.
- **Transparency rule:** If DDA is invisible, it must be subtle. If visible ("the game adjusts to you"), it can be more aggressive.

### 6.2 Director System (Left 4 Dead Style)
- **Intensity curve:** Track emotional intensity on a 0-1 scale.
- **Build phase:** Spawn light enemies, resources. Target intensity 0.2-0.4.
- **Peak phase:** Spawn horde + special enemies. Target intensity 0.7-0.9.
- **Relax phase:** Low spawns, health kits. Target intensity 0.1-0.2.
- **Cycle length:** 60-120 seconds typical. Peak-to-relax ratio = 1:2.

## 7. Matchmaking & Rating (Competitive Games)

### 7.1 Elo Rating System
- **Formula:** `NewRating = OldRating + K * (Actual - Expected)`
  - `Expected = 1 / (1 + 10^((OpponentRating - PlayerRating) / 400))`
  - K factor: 32 (new players) → 16 (established) → 10 (top tier).
- **Placement matches:** Use K = 64 for first 10 matches for fast convergence.

### 7.2 Win Rate Equilibrium
- **Target:** All players converge to 45-55% win rate at their skill level.
- **Matchmaking quality metric:** `AvgRatingDiff < 100 points` in matched games.
- **Queue time tradeoff:** Widen rating range by 25 per 30 seconds of queue time.

---
**EXPERT DIRECTIVE:** When generating any numerical design (stats, prices, drop rates, damage formulas, progression curves), you MUST reference the appropriate formula from this document and show your work with concrete numbers, not just describe the concept.
