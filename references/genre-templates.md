# Genre Templates

## Goal

Provide a structural blueprint for every major game genre so that all downstream modules — strategy, balance, level design, art, audio, UI, QA — can calibrate their output to the specific demands of the project's type. Load this file first when the genre is identified; use it to seed every other reference.

## Relationship to Data Models

This file provides **design templates** — core loops, key systems, emphasis areas, and genre-specific risks for each genre. For **hard production benchmarks** (animation budgets, TTK targets, retention metrics, scope warnings with exact numbers), always cross-reference [data_models/genre_benchmarks.md](data_models/genre_benchmarks.md). Use the benchmarks from data_models to validate scope and ground the templates in production reality.

## How To Use

1. Identify the primary genre from the user's description.
2. If the game mixes genres, find both templates and follow the **Hybrid Combination Rules** at the bottom.
3. Feed the genre's core loop, key systems, and emphasis areas into the relevant downstream modules.
4. Cross-reference [data_models/genre_benchmarks.md](data_models/genre_benchmarks.md) for hard metrics and scope warnings.
5. Use the genre-specific risk list to front-load mitigation in planning.

---

## RPG — Turn-Based

### Core Loop
Explore → encounter → choose actions → resolve → gain rewards → grow → explore deeper.

### Key Systems
- Turn order / initiative
- Action menu (attack, skill, item, defend, flee)
- Party composition and role synergy
- Equipment and stat modification
- Quest / objective tracker
- Dialogue and branching choices

### Balance Emphasis
- Stat growth curves per level; diminishing returns on scaling
- Enemy stat tables per zone with clear power gates
- Skill cost vs. damage vs. utility matrix
- Economy: gold income per encounter vs. shop price curve
- Experience curve shape (polynomial preferred)

### Level Design Emphasis
- Dungeon topology: branching corridors, secret rooms, treasure risk/reward
- Town ↔ Field ↔ Dungeon pacing rhythm
- Boss gates as skill checks, not gear checks alone

### Art Emphasis
- Character portraits and sprites for party + many NPCs + many enemy types
- Tile sets per biome; UI-heavy screens (menus, inventory, status)
- Turn-based allows lower animation count but higher pose quality

### Audio Emphasis
- Layered BGM per zone (explore / battle / boss / victory)
- UI confirmation and menu navigation SFX family
- Spell and skill SFX library scaled to element count

### Genre-Specific Risks
- Stat inflation trivializing content; flat power curves causing grind feeling
- Menu UX overwhelming new players
- Content volume (enemies, skills, items) exceeding production capacity

---

## RPG — Action

### Core Loop
Move → engage enemies in real-time → dodge/block → combo → loot → upgrade → push deeper.

### Key Systems
- Real-time combat with hitboxes and i-frames
- Stamina / resource management
- Dodge / parry / block mechanics
- Weapon movesets and combo trees
- Loot and equipment with gameplay-altering stats
- Lock-on or soft targeting

### Balance Emphasis
- Frame data: startup, active, recovery per attack
- TTK by enemy tier; player DPS benchmarks
- Stamina economy per combo string
- Damage reduction formulas (multiplicative preferred for gear scaling)
- Boss HP and phase thresholds

### Level Design Emphasis
- Arena design for combat readability (sightlines, cover, elevation)
- Exploration reward placement (shortcuts, hidden rooms)
- Pacing: encounter density → rest point → boss gate

### Art Emphasis
- Smooth animation priority: locomotion, attacks, hit reacts, dodge
- Root motion or animation-driven movement
- VFX for impact, elemental effects, status indicators
- Readable enemy telegraphs (wind-up, glow, particle cues)

### Audio Emphasis
- Impact-synced SFX with variation (3-5 variants per hit type)
- Adaptive music: exploration → combat → boss → victory layers
- Spatial audio for off-screen enemy awareness

### Genre-Specific Risks
- Combat feel requires iteration — budget time for tuning
- Animation volume explosion with weapon variety
- Camera-combat-level interaction bugs

---

## Roguelike / Roguelite

### Core Loop
Start run → procedural floor → combat/event → acquire items/upgrades → die or clear → meta-progress → new run.

### Key Systems
- Procedural generation (rooms, encounters, rewards)
- Item/relic pool with synergy matrix
- Run currency vs. meta currency
- Difficulty scaling per floor/zone
- Death and meta-progression persistence

### Balance Emphasis
- Item power budget: each relic rated on a 1-10 power scale
- Synergy matrix: which combinations are intended to be broken-strong
- Per-floor difficulty curve (enemy count, elite frequency, trap density)
- Run length target and variance (median 25-40 min for mainstream)
- Meta-unlock pacing: first 10 runs should unlock ~30% of content

### Level Design Emphasis
- Room templates with entrance/exit constraints
- Encounter composition rules per floor tier
- Reward room / shop / event / boss room distribution
- Procedural grammar: guaranteed shop before boss, no consecutive elite rooms

### Art Emphasis
- Modular tile sets for procedural assembly
- Distinct silhouettes for items/relics (icon readability critical)
- Enemy visual escalation per floor tier
- UI for run information density (relics, HP, map, currency)

### Audio Emphasis
- Per-biome BGM with tension escalation layers
- Run-start and run-end musical stingers
- Item pickup and synergy activation SFX (satisfying, distinct)

### Genre-Specific Risks
- Item pool too small → runs feel samey after 5-10 runs
- Broken synergy combos trivializing content without counterplay
- Procedural generation producing degenerate layouts

---

## Tower Defense

### Core Loop
Wave announcement → place/upgrade towers → wave spawns → enemies traverse path → player adjusts → wave clear → spend resources → next wave.

### Key Systems
- Tower placement grid or free-form
- Tower type matrix (DPS, slow, AoE, support, special)
- Enemy type matrix (fast, armored, flying, swarm, boss)
- Wave composition and pacing
- Resource economy (kill income + wave bonus)
- Upgrade paths per tower

### Balance Emphasis
- DPS/cost ratio per tower type at each upgrade tier
- Enemy HP/speed/armor scaling per wave
- Wave budget system: total "threat points" per wave, distributed across enemy types
- Optimal vs. suboptimal tower placement gap (reward smart play without hard-failing new players)
- Late-game scaling: multiplicative tower synergies vs. exponential enemy scaling

### Level Design Emphasis
- Path design: chokepoints, split paths, elevation for range advantage
- Placement slots: count and position determine strategy space
- Map-specific gimmicks (environmental hazards, moving paths)

### Art Emphasis
- Top-down or isometric readability at zoomed-out scale
- Tower visual escalation through upgrade tiers
- Enemy readability: type identifiable at a glance (silhouette + color)
- Path and terrain clarity (walkable vs. placeable vs. blocked)

### Audio Emphasis
- Tower firing SFX families (rapid, heavy, magical, mechanical)
- Wave start/end fanfares
- Enemy death and boss arrival stingers
- Background tension escalation across waves

### Genre-Specific Risks
- Dominant tower strategy making 80% of tower types useless
- Late-game visual noise from many towers firing simultaneously
- Wave pacing too uniform causing monotony

---

## Action / Platformer

### Core Loop
Run → jump → overcome obstacle → reach checkpoint → face new mechanic combination → boss/goal.

### Key Systems
- Precise movement controller (acceleration, deceleration, coyote time, jump buffer)
- Obstacle vocabulary (static, moving, timed, destructible)
- Hazard types (spikes, pits, projectiles, enemies)
- Checkpoint and life system
- Collectibles and optional challenges

### Balance Emphasis
- Movement parameters: gravity, jump height, air control, dash distance
- Frame-perfect windows vs. generous windows (target audience calibration)
- Obstacle rhythm: beats per second, recovery windows
- Difficulty curve: teach → test → combine → master pattern
- Speedrun-friendly design considerations

### Level Design Emphasis
- Mechanic introduction sequence: safe → guided → combined → free
- Rhythm and flow: tension/release, safe landing → next challenge
- Camera framing: player always sees the next challenge
- Secret areas rewarding mastery or exploration

### Art Emphasis
- Foreground gameplay layer vs. background atmosphere layer
- Platform readability: solid ground vs. hazard vs. decoration
- Character animation: run cycle, jump, fall, land, wall-slide, death
- Parallax scrolling layers for depth

### Audio Emphasis
- Movement SFX: footsteps, jump, land, wall-slide with surface variation
- Hazard warning audio cues
- BGM tempo matching level energy
- Death and checkpoint jingles

### Genre-Specific Risks
- Movement feel requires extensive tuning — prototype early
- Camera and level geometry conflicts at edges and transitions
- Difficulty spikes in mechanic combination levels

---

## Puzzle

### Core Loop
Observe situation → identify constraint → form hypothesis → execute solution → receive feedback → advance.

### Key Systems
- Core mechanic (spatial, logical, physics, pattern, language)
- Undo/reset system
- Hint system (if any)
- Complexity scaling (new elements, combined rules)
- Level progression or world structure

### Balance Emphasis
- Complexity curve: new mechanic every N levels, combination every M levels
- Solution space: single solution (tight design) vs. multiple valid paths (creative)
- Cognitive load management: max active elements per puzzle
- Teaching sequence: mechanics introduced one at a time with fail-safe levels

### Level Design Emphasis
- Mechanic teaching order (critical — get this wrong and players quit)
- Puzzle dependency graph (which puzzles unlock which)
- Rest levels between difficulty spikes
- Optional hard puzzles for mastery players

### Art Emphasis
- Functional clarity above all: interactive vs. decorative must be obvious
- Color coding for puzzle elements
- Minimal visual noise in puzzle-solving space
- Satisfying solve animation/VFX

### Audio Emphasis
- Manipulation SFX (drag, snap, rotate, connect)
- Success stingers (per-puzzle and per-world)
- Ambient background that doesn't distract
- Audio cues for correct partial progress

### Genre-Specific Risks
- Difficulty spike causing mass player dropout at a single puzzle
- Mechanic tutorial too implicit — players don't understand rules
- Solution too obscure or too obvious (both kill engagement)

---

## Strategy / 4X

### Core Loop
Expand territory → gather resources → research/build → diplomacy/conflict → consolidate → expand further.

### Key Systems
- Resource system (multiple currencies, production chains)
- Tech/research tree
- Unit production and army composition
- Territory control and map fog
- Diplomacy or AI faction behavior
- Turn resolution or real-time with pause

### Balance Emphasis
- Resource generation rates and sink balance
- Tech tree path viability (no dead-end branches)
- Unit counter system (rock-paper-scissors or stat-gradient)
- Faction asymmetry within competitive balance
- Game length pacing (early rush vs. late game viability)

### Level Design Emphasis
- Map generation: resource distribution, starting positions, choke points
- Scenario design for campaign mode
- Victory condition variety

### Art Emphasis
- Map readability at strategic zoom level
- Unit silhouette differentiation by type and faction
- UI density management (many panels, many stats)
- Minimap and overlay clarity

### Audio Emphasis
- Ambient per-biome soundscapes
- Battle SFX scaled to engagement size
- Notification SFX for events (research complete, attack incoming)
- Era-appropriate or faction-appropriate BGM

### Genre-Specific Risks
- Analysis paralysis from too many systems exposed simultaneously
- AI difficulty: too easy or too unfair
- Late-game performance with many units/calculations
- Tutorial complexity for deep systems

---

## Card Game / Deckbuilder

### Core Loop
Draw hand → play cards using resources → resolve effects → end turn → draw new hand → adapt strategy.

### Key Systems
- Card pool and rarity system
- Mana/energy/resource per turn
- Deck construction rules (minimum/maximum, copy limits)
- Card synergy archetypes
- Opponent AI or PvP matchmaking
- Collection and progression

### Balance Emphasis
- Card power budget by mana cost
- Archetype win-rate parity (45-55% target for each viable archetype)
- Curve analysis: mana cost distribution for healthy gameplay
- Rarity vs. power: rare should enable strategy, not guarantee wins
- Card pool expansion cadence and meta impact

### Level Design Emphasis
- Campaign encounter sequence (themed decks per opponent)
- Draft/arena pool construction
- Tutorial sequence: starter deck → first pack → first deckbuilding decision

### Art Emphasis
- Card frame design (rarity differentiation, faction borders)
- Card illustration pipeline (many unique illustrations needed)
- Board/battlefield visual design
- VFX for card play, summon, spell resolution

### Audio Emphasis
- Card draw, play, and shuffle SFX
- Attack and spell resolution audio
- Turn transition audio cues
- Victory/defeat stingers

### Genre-Specific Risks
- Dominant deck meta suppressing variety
- Card text ambiguity causing rule disputes
- Art production volume for large card pools
- Power creep across expansions

---

## Idle / Incremental

### Core Loop
Tap/click → earn currency → buy upgrade → automate earning → prestige/reset → earn faster.

### Key Systems
- Currency generators (multi-tier)
- Upgrade tree (linear and branching)
- Prestige/ascension mechanic
- Offline progress calculation
- Milestone unlocks and new mechanics reveal

### Balance Emphasis
- Exponential growth curves calibrated to engagement checkpoints
- Prestige multiplier balancing (diminishing returns per reset)
- Active vs. idle earning ratio (reward engagement without punishing absence)
- Time-to-next-milestone targets (decreasing wait → spike at prestige → fast again)
- Ad or IAP value proposition without breaking progression

### Level Design Emphasis
- Content reveal pacing: new mechanic every N minutes of play
- Visual progression milestones
- Prestige layer depth (how many resets before content exhaustion)

### Art Emphasis
- Minimal but satisfying visual feedback for taps/upgrades
- Number display readability (scientific notation handling)
- Upgrade tree visual hierarchy
- Milestone celebration effects

### Audio Emphasis
- Satisfying click/tap SFX with subtle variation
- Upgrade and milestone jingles
- Ambient background that supports long sessions
- Prestige fanfare

### Genre-Specific Risks
- Player hitting a wall where progress feels meaningless
- Offline calculation exploits
- Monetization balance: pay-to-skip vs. pay-to-win perception

---

## Survival / Crafting

### Core Loop
Gather resources → craft tools/shelter → manage needs (hunger, health, temperature) → explore → face threats → improve base → expand range.

### Key Systems
- Resource gathering and inventory management
- Crafting recipe tree
- Needs/status system (hunger, thirst, health, temperature)
- Base building (structure placement, storage)
- Day/night cycle and weather
- Threat system (enemies, environment, other players)

### Balance Emphasis
- Resource spawn rates vs. consumption rates
- Crafting tree depth vs. breadth (progression feeling)
- Need drain rates calibrated to exploration range
- Threat escalation curve (days survived → harder enemies)
- Inventory capacity as pacing tool

### Level Design Emphasis
- Biome variety with distinct resource profiles
- Base location tradeoffs (safety vs. resources vs. access)
- Points of interest distribution
- Environmental storytelling through world placement

### Art Emphasis
- Resource and item icon readability (inventory screen is primary UI)
- Biome visual differentiation
- Day/night and weather visual systems
- Base building piece visual consistency and snapping feedback

### Audio Emphasis
- Environmental ambience per biome and time of day
- Gathering and crafting SFX families
- Threat proximity audio (growls, footsteps approaching)
- Weather and wind audio layers

### Genre-Specific Risks
- Early game too punishing, causing churn before crafting opens up
- Inventory management tedium
- Base building performance with many objects
- Multiplayer: griefing and balance

---

## Fighting Game

### Core Loop
Neutral → approach → pressure/mixup → combo → reset to neutral → adapt.

### Key Systems
- Frame data system (startup, active, recovery, advantage)
- Input buffer and motion commands
- Combo system (chain, link, cancel rules)
- Meter / resource management
- Character roster with distinct movesets
- Netcode (rollback preferred)

### Balance Emphasis
- Frame data tables per character (all normals, specials, supers)
- Damage scaling in combos
- Character matchup chart (5-5 ideal, 4-6 acceptable, 3-7 problematic)
- Meter gain rates and super damage value
- Health values and round timer

### Level Design Emphasis
- Stage design: flat fighting plane, visual clarity, corner dynamics
- Stage hazards (if applicable): fair interaction rules
- Training mode feature set

### Art Emphasis
- High frame-count character animation (24+ unique animations per character minimum)
- Hit effects, block effects, super flash
- Character silhouette distinction across roster
- Stage backgrounds that don't compete with character readability

### Audio Emphasis
- Impact SFX with weight differentiation (light, medium, heavy, launcher)
- Character voice lines (attack shouts, damage reactions, win quotes)
- Round start/end audio cues
- Announcer system

### Genre-Specific Risks
- Balance: one dominant character destroying competitive viability
- Netcode quality determining player retention
- Animation production cost per character
- Execution barrier: too hard for casual, too simple for competitive

---

## Simulation / Management

### Core Loop
Set goals → allocate resources → manage operations → respond to events → evaluate performance → optimize → expand.

### Key Systems
- Resource management (money, staff, materials, time)
- Building/placement system
- NPC/agent simulation
- Event/scenario system
- Progression unlocks
- Performance metrics dashboard

### Balance Emphasis
- Income vs. expense curves per game phase
- Event difficulty and reward calibration
- Expansion cost scaling
- Failure cascade prevention (player should be able to recover from mistakes)
- Difficulty modes affecting simulation parameters

### Level Design Emphasis
- Scenario design with specific constraints and goals
- Map/lot size and terrain variety
- Tutorial scenario as guided experience
- Sandbox mode parameters

### Art Emphasis
- Isometric or top-down readability at multiple zoom levels
- Building and object visual progression through upgrades
- NPC variety and animation (walk, work, idle, react)
- UI density: many data panels, graphs, status indicators

### Audio Emphasis
- Ambient soundscape matching simulation state (busy vs. quiet)
- Notification SFX for events and milestones
- Construction and upgrade audio feedback
- BGM that supports long play sessions without fatigue

### Genre-Specific Risks
- Information overload for new players
- Optimization: one dominant strategy making decisions trivial
- Performance with many simulated agents
- Feedback clarity: player must understand why things are succeeding or failing

---

## Visual Novel

### Core Loop
Read text → view scene → make choice → branch narrative → reach ending → replay for other branches.

### Key Systems
- Text display and auto-advance
- Choice system with branching logic
- Character relationship/affinity tracking
- Scene and CG gallery
- Save/load with branching state
- Multiple endings logic

### Balance Emphasis
- Branch length balance (no drastically shorter/longer paths)
- Choice impact clarity (meaningful vs. cosmetic choices)
- Relationship point thresholds for route locks
- Pacing: text density per scene, scene count per chapter
- Replay incentive: meaningful alternate content per branch

### Level Design Emphasis
- Story structure: common route → branch point → character routes → endings
- Scene flow diagram
- CG placement (reward pacing)
- Choice placement rhythm

### Art Emphasis
- Character sprite set: expressions (8-15 per character), outfits, poses
- Background illustrations (15-30 for typical VN)
- CG illustrations (key story moments, high quality)
- UI: text box, choice buttons, menu screens, gallery

### Audio Emphasis
- BGM per mood/scene type (8-15 tracks typical)
- Ambient soundscapes per location
- Voice acting (if applicable): full, partial, or key lines only
- SFX for transitions, UI, dramatic moments

### Genre-Specific Risks
- Writing quality is make-or-break — no gameplay to compensate
- Art production volume for many characters and expressions
- Branch testing combinatorial explosion
- Player missing content due to opaque branching

---

## Hybrid Combination Rules

When a game combines two or more genres, follow these rules:

### Identify Primary and Secondary
- Primary genre: defines the core loop and moment-to-moment gameplay
- Secondary genre: provides meta-structure, progression, or context

### Merge Process
1. Take the core loop from the primary genre.
2. Take the meta-progression or structural systems from the secondary genre.
3. For overlapping systems (e.g., both have combat), merge under the primary's design philosophy.
4. Balance emphasis: use primary genre's formulas, add secondary genre's constraints as modifiers.
5. Art and audio: primary genre dictates real-time needs; secondary genre adds asset types.

### Common Hybrids

| Hybrid | Primary | Secondary | Merge Notes |
|--------|---------|-----------|-------------|
| Roguelike Deckbuilder | Card/Deckbuilder | Roguelike | Card combat loop + procedural runs + item relics |
| Action RPG | Action | RPG | Real-time combat + stat growth + loot + quests |
| Survival Crafting + Base Defense | Survival | Tower Defense | Gather/craft loop + wave-based base attacks |
| Puzzle Platformer | Platformer | Puzzle | Movement core + environmental puzzle mechanics |
| Strategy RPG (SRPG) | Strategy | RPG (Turn-Based) | Grid tactics + character growth + story |
| Roguelite Action | Action/Platformer | Roguelike | Real-time combat + procedural levels + meta-progress |
| Management + Story | Sim/Management | Visual Novel | Business sim + narrative choices + character arcs |
| Idle RPG | Idle/Incremental | RPG | Auto-combat + stat growth + prestige resets |

### Hybrid Risk Amplification
- Each added genre multiplies content requirements
- Test the primary loop in isolation before integrating secondary systems
- UI complexity grows with each genre layer — budget for information architecture
- Balance complexity is multiplicative, not additive
