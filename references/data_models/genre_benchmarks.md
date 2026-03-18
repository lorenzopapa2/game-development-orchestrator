# Genre Production Benchmarks & Design Patterns

When designing or scoping a game for a specific genre, you MUST enforce the constraints and benchmarks listed below. Do not generate generic feature sets that ignore genre-specific production reality.

For full genre design templates (core loops, key systems, art/audio/level emphasis), see [../genre-templates.md](../genre-templates.md).

## 1. Action / Hack & Slash (Soulslike, Character Action)

### Core Mechanics & Metrics
- **Animation Budget (Critical):** Usually 40% of the entire development cost.
- **Combat Hit-Stops:** Attacks MUST have hit-stops (a brief freeze frame on impact), usually 3 to 10 frames depending on weapon weight.
  - Light attack: 3-4 frames. Heavy attack: 6-10 frames. Boss attack: 8-12 frames.
- **Input Buffering:** Mandatory. A 5-10 frame input buffer ensures actions feel responsive.
- **iFrames:** Dodges usually grant 0.2s - 0.4s of invulnerability.
  - Souls-like: 0.3-0.5s (generous). Character action: 0.15-0.3s (tighter).
- **Coyote Time (platforming):** 0.1-0.15s grace period after leaving a ledge.
- **Attack Cancel Windows:** Define per-frame where the player can cancel into dodge, block, or next attack.

### Frame Data Template (Per Attack)
| Move | Startup | Active | Recovery | Cancel Window | iFrames |
|------|---------|--------|----------|--------------|---------|
| Light 1 | 6f | 3f | 12f | 8-18f | None |
| Light 2 | 8f | 4f | 14f | 10-22f | None |
| Heavy | 18f | 5f | 24f | 20-38f | None |
| Dodge | 4f | — | 16f | 12-20f | 4-12f |

### Scope Warning
- Do NOT plan for 50+ enemy types for an indie studio. A viable vertical slice only needs: 1 Grunt, 1 Ranged, 1 Elite, 1 Boss.
- Each unique enemy with full animation set costs 40-120 hours of work.
- Player character: 30-80 unique animations minimum for satisfying combat feel.

## 2. Roguelike / Roguelite (Hades, Slay the Spire, Dead Cells)

### Core Mechanics & Metrics
- **Run Duration Target:** 20 to 45 minutes max for mainstream; 10-15 min for action roguelites.
- **Content Scaling:** Instead of linear levels, use Procedural Generation (ProcGen) paired with "Handcrafted Chunks/Rooms".
- **Economy:**
  1. **Soft Currency (Run specific):** Lost on death (Gold, Temporary Buffs).
  2. **Hard Currency (Metaprogression):** Kept on death (Darkness, Cells) to buy permanent upgrades.
- **Meta-Unlock Pacing:** First 10 runs = ~30% unlocked. 30 runs = ~60%. 100+ runs = completionist.

### Combinatorial Explosion
- **Synergy Matrix:** The game relies on A * B interactions. Instead of 100 weapons, design 10 weapons and 10 status effects that interact with each other (e.g., Fire + Poison = Explosion).
- **Item count benchmarks:** Minimum viable = 30-40 items. Good variety = 80-120. Deep game = 200+.
- **Power budget:** Rate each item 1-10. Average run total should hit 25-35 power. "Broken run" = 45+.

### Floor/Biome Scaling
| Floor | Enemy HP Multiplier | Enemy Damage Multiplier | Elite Chance | Reward Multiplier |
|-------|-------------------|----------------------|-------------|------------------|
| 1 | 1.0x | 1.0x | 5% | 1.0x |
| 2 | 1.4x | 1.2x | 10% | 1.3x |
| 3 | 1.8x | 1.4x | 15% | 1.6x |
| Boss | 3.0x | 1.6x | N/A | 2.5x |

## 3. RPG (ARPG, cRPG, JRPG)

### Core Mechanics & Metrics
- **Content Volume:** Highly narrative-driven. Dialogue and quest implementation take 50% of the time.
- **Economy Curve:** Use an Exponential Growth model for both Player XP and Enemy Stats. See [economy_and_progression.md](economy_and_progression.md) §2.1.
- **Loot Tables:** Use a tiered rarity system (Common, Uncommon, Rare, Epic, Legendary) with weighted probability drop tables (PRD). See [economy_and_progression.md](economy_and_progression.md) §4.3.

### Stat Budget Benchmarks
| Level Range | Stat Total (sum of all attributes) | Gear Contribution | Level-Up Feels Like |
|------------|-----------------------------------|-------------------|-------------------|
| 1-10 | 30-60 | 20-40% | Significant power jump |
| 11-25 | 60-120 | 30-50% | Noticeable upgrade |
| 26-50 | 120-250 | 40-60% | Incremental but satisfying |
| 50+ | 250+ | 50-70% | Gear-driven, stat gains slow |

### Content Volume Benchmarks
| Scope | Main Quest (hours) | Side Content (hours) | Enemy Types | Unique Locations | NPCs |
|-------|-------------------|---------------------|------------|-----------------|------|
| Small RPG | 8-15 | 5-10 | 10-20 | 5-10 | 15-30 |
| Mid RPG | 20-40 | 15-30 | 20-40 | 10-25 | 30-60 |
| Large RPG | 40-80 | 30-60+ | 40-80 | 25-50 | 60-120 |

### Scope Warning
- Open World RPGs are lethal for small teams. Force the scope down to "Hub & Spoke" (like Monster Hunter or Demon's Souls) or linear dungeons unless the user explicitly defines a massive budget.
- Each hour of RPG content costs 100-500 person-hours to produce (writing + design + art + audio + QA).

## 4. Strategy & City Builders (RTS, 4X, Factory Builders)

### Core Mechanics & Metrics
- **Performance:** CPU bound, not GPU bound. Pathfinding (A* / Flow Fields) for thousands of units is the primary technical bottleneck.
- **Economy:** Sinks and Faucets are the entire gameplay loop. Supply lines, storage limits, and processing ratios (e.g., 2 Iron + 1 Coal = 1 Steel).
- **Lanchester's Square Law:** Applies heavily to ranged unit stacking. See [economy_and_progression.md](economy_and_progression.md) §5.

### Unit Balance Benchmarks (RTS)
| Unit Class | HP Relative | DPS Relative | Cost Relative | Speed Relative | Counter |
|-----------|-----------|-------------|-------------|---------------|---------|
| Melee grunt | 1.0x | 0.8x | 1.0x | 1.0x | Ranged |
| Ranged | 0.6x | 1.0x | 1.2x | 0.8x | Melee rush |
| Tank/Heavy | 2.5x | 0.5x | 2.0x | 0.5x | Anti-armor |
| Anti-armor | 0.7x | 2.0x vs heavy | 1.5x | 0.7x | Swarm |
| Fast/Scout | 0.4x | 0.3x | 0.6x | 2.0x | AoE |
| Siege | 0.5x | 3.0x vs buildings | 3.0x | 0.3x | Any direct |

### Tech Tree Benchmarks
- **Depth:** 3-5 tiers typical. Each tier unlocks in 5-15 min of focused play.
- **Breadth:** 3-6 branches per tier. Player should explore 40-60% per game.
- **Dead-end test:** Every branch must lead to at least one viable endgame strategy.

## 5. Mobile Hypercasual / Hybridcasual

### Core Mechanics & Metrics
- **Session Length:** 30 seconds to 3 minutes.
- **Retention Targets:** D1 > 40%, D7 > 15%. If the prototype fails these metrics, kill it immediately.
- **Input:** Single-touch (Swipes, Taps, or Virtual Joysticks). Do not introduce complex multi-button combos.
- **CPI (Cost Per Install):** Visual clarity is key for ad creatives. High-contrast colors, clear feedback.
  - Benchmark: CPI < $0.30 for hypercasual, < $1.00 for hybridcasual.
- **LTV targets:** Hypercasual: $0.10-0.50/user. Hybridcasual: $0.50-3.00/user.

### Monetization Benchmarks
| Model | eCPM Target | Ad Frequency | IAP % Revenue |
|-------|-----------|-------------|--------------|
| Pure ad (hypercasual) | $20-60 | Every 1-2 levels | 0-10% |
| Hybrid (rewarded ads + IAP) | $30-80 | Opt-in + interstitial | 20-40% |
| IAP-first (hybridcasual) | $10-30 | Light interstitial | 60-80% |

## 6. Tower Defense

### Core Mechanics & Metrics
- **Wave count:** 20-40 waves for a standard map. 60+ for endless mode.
- **Tower types:** 4-8 base types is optimal. Fewer feels shallow, more overwhelms.
- **Upgrade tiers:** 2-3 upgrade tiers per tower. Each tier = 50-100% power increase for 200-300% cost.

### DPS/Cost Efficiency Benchmark
| Tower Tier | DPS/Cost Ratio | Purpose |
|-----------|---------------|---------|
| Tier 1 (basic) | 0.08-0.12 | Affordable, spammable |
| Tier 2 (upgraded) | 0.06-0.09 | Cost-efficient for single target |
| Tier 3 (max) | 0.04-0.07 | Expensive but powerful |
| Utility (slow/buff) | N/A (0 DPS) | Value through synergy |

**Key balance rule:** DPS/Cost should DECREASE with tier — you pay premium for convenience and power spikes, but quantity of tier 1 towers should be competitive with fewer tier 3.

### Wave Budget System
- **Formula:** `WaveBudget(n) = BaseBudget * WaveMultiplier^(n-1)`
  - WaveMultiplier = 1.08-1.15 (gentle) to 1.20-1.30 (steep).
- **Budget distribution:** Assign cost per enemy type, then fill wave budget with composition.
  - Grunt = 1 point, Fast = 1.5, Armored = 2, Flying = 2.5, Boss = 10-20.

## 7. Card Game / Deckbuilder

### Core Mechanics & Metrics
- **Deck size:** 20-40 cards (constructed). 15-25 cards (roguelike deckbuilder).
- **Card pool size:** Minimum viable = 80-120 unique cards. Healthy meta = 200+.
- **Mana/resource curve:** Peak density at 2-3 cost. 60% of deck should be 1-3 cost cards.

### Archetype Win Rate Benchmarks
- **Healthy meta:** Top archetype ≤ 55% win rate. Bottom viable archetype ≥ 45%.
- **Tier list distribution:** 2-3 Tier 1, 3-5 Tier 2, 5-8 Tier 3. If >1 archetype at 58%+, emergency nerf.

### Card Power Budget
| Mana Cost | Stat Points | Effect Points | Total Budget |
|-----------|-----------|-------------|-------------|
| 1 | 2-3 | 0-1 | 2-4 |
| 2 | 4-5 | 1-2 | 5-7 |
| 3 | 6-7 | 2-3 | 8-10 |
| 4 | 8-9 | 3-4 | 11-13 |
| 5+ | 10+ | 4+ | 14+ |

Stat point = 1 attack or 1 HP. Effect point = keyword, card draw, removal, etc. valued by rarity.

## 8. Puzzle Game

### Core Mechanics & Metrics
- **Puzzle count:** 50-100 for short game. 150-300 for full release. 500+ for puzzle game as service.
- **Solve time target:** 30s-3 min per puzzle (casual). 3-15 min (enthusiast). 15+ min (expert/optional).
- **New mechanic cadence:** Every 10-15 puzzles (casual) or 5-8 puzzles (enthusiast).

### Complexity Curve
| Phase | Puzzles | Mechanics Active | Difficulty | Purpose |
|-------|---------|-----------------|-----------|---------|
| Intro | 1-5 | 1 | Trivial | Teach base mechanic |
| Learn | 6-15 | 1-2 | Easy | Build confidence |
| Combine | 16-30 | 2-3 | Medium | Test understanding |
| Challenge | 31-50 | 3-4 | Hard | Reward mastery |
| Expert | 51+ | 4+ | Very Hard | Optional, for enthusiasts |

### Dropout Risk
- **Critical threshold:** If >30% of players quit at the same puzzle, it's a difficulty spike — fix it.
- **Hint system:** First hint after 2 min, second after 4 min, full solution after 6 min (optional, player-controlled).

## 9. Fighting Game

### Core Mechanics & Metrics
- **Roster size:** 8-12 at launch (indie). 16-24 (AA). 30+ (AAA).
- **Animation per character:** 40-80 unique animations minimum (normals + specials + supers + movement + reactions).
- **Input latency target:** < 4 frames (66ms). Rollback netcode mandatory for online play.

### Frame Data Benchmarks
| Move Type | Startup (frames) | Active | Recovery | On Block |
|----------|-----------------|--------|----------|----------|
| Jab (fastest) | 4-6 | 2-3 | 8-12 | -2 to +1 |
| Medium | 7-10 | 3-4 | 14-18 | -4 to -1 |
| Heavy | 12-20 | 4-6 | 20-28 | -8 to -4 |
| Special | 8-16 | varies | 18-30 | varies |
| Super | 5-12 | 5-8 | 30-40 | -10 to -5 |
| Throw | 5-7 | 2-3 | 25-35 | N/A |
| Jump | 4 (pre-jump) | — | 4 (landing) | — |

### Balance Benchmark
- **Matchup spread:** Best case 6-4, worst case 4-6. Any 7-3 matchup is a design problem.
- **Combo damage scaling:** 100% → 80% → 60% → 50% → ... per successive hit (prevents infinites).
- **Round length target:** 30-90 seconds per round.

## 10. Survival / Crafting

### Core Mechanics & Metrics
- **Day/night cycle:** 10-20 min real time per in-game day.
- **Need drain rates:** Hunger/thirst should require attention every 5-15 min of play (not every 30s).
- **Crafting tree depth:** 3-5 tiers. Each tier unlocks new biome access or threat mitigation.

### Resource Availability Benchmarks
| Resource Tier | Availability | Usage Rate | Progression Gate |
|-------------|-------------|-----------|-----------------|
| Basic (wood, stone) | Abundant everywhere | Constant | None |
| Intermediate (iron, leather) | Moderate, specific biomes | Regular | Mid-game |
| Advanced (steel, circuits) | Scarce, dangerous areas | Occasional | Late-game |
| Rare (endgame materials) | Very scarce, boss drops | Infrequent | Endgame |

## 11. Visual Novel / Narrative

### Core Metrics
- **Word count:** 50K-100K (short VN). 100K-300K (standard). 300K+ (epic).
- **CG count:** 10-20 (short). 30-60 (standard). 80+ (premium).
- **Character sprites:** 8-15 expressions per character, 2-3 outfits for main characters.
- **Route count:** 3-5 character routes typical. Each route = 15-30% unique content.

### Branching Benchmarks
- **Choice frequency:** Every 500-1500 words of text.
- **Meaningful vs. cosmetic ratio:** At least 30% of choices should affect route/ending.
- **Testing burden:** N choices with 2 options each = 2^N possible paths. Keep total meaningful branch points < 15 to maintain testing feasibility.

---
**EXPERT DIRECTIVE:** When a user requests a game design or plan, you MUST identify the closest matching genre from this document and apply its constraints, scope warnings, and metrics to your output. Cross-reference [../genre-templates.md](../genre-templates.md) for full design methodology and [economy_and_progression.md](economy_and_progression.md) for mathematical models.
