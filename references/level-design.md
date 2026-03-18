# Level Design

## Goal

Define the methodology for designing game levels, encounters, pacing, and spatial layouts that serve gameplay and narrative goals. This module produces level documentation, encounter frameworks, and pacing curves — not code or engine-specific implementations.

## When To Use

- After genre and core loop are defined (see [genre-templates.md](genre-templates.md))
- After balance parameters are set (see [balance-economy.md](balance-economy.md))
- Before art asset lists are finalized (levels drive environment and prop needs)
- Before audio design (levels drive ambient and encounter audio needs)
- When the user asks about "level structure", "encounter design", "pacing", or "world layout"

---

## Level Purpose Categories

Every level (or section, room, floor, zone) should have a declared primary purpose:

| Purpose | Description | Design Priority | Pacing Role |
|---------|-------------|----------------|-------------|
| Tutorial | Teach a specific mechanic in a safe environment | Clarity, guided failure | Low tension, high feedback |
| Test | Challenge the player to apply learned mechanics | Fair difficulty, multiple solutions | Rising tension |
| Combination | Combine 2+ mechanics in novel ways | Emergent complexity | Peak tension |
| Reward | Provide loot, story payoff, or visual spectacle | Generous rewards, exploration | Release/satisfaction |
| Narrative | Advance story through environment, dialogue, or events | Atmosphere, story delivery | Emotional engagement |
| Rest | Safe zone for player to manage inventory, upgrade, plan | No threats, resource access | Low tension recovery |
| Boss | Climactic test of accumulated skills | High stakes, phased design | Maximum tension |
| Hub | Central space connecting multiple paths/zones | Navigation clarity, options | Neutral tension |

Rule: every level should have one primary purpose. If it tries to do two, make one secondary and subordinate it.

---

## Pacing Design

### Per-Level Tension Curve

Design each level as a mini-arc:

```
Tension
  ▲
  │         ╱╲
  │        ╱  ╲      ╱╲
  │   ╱╲  ╱    ╲    ╱  ╲
  │  ╱  ╲╱      ╲  ╱    ╲
  │ ╱              ╲╱     ╲__
  │╱
  └──────────────────────────▶ Time
  Entry  Build  Peak  Relief  Exit
```

- **Entry**: Orient the player, establish the space
- **Build**: Introduce encounters of rising challenge
- **Peak**: Hardest encounter or most dramatic moment
- **Relief**: Reward, breather, or story beat
- **Exit**: Transition to next area, forward momentum

### Full-Game Pacing Arc

Map the overall experience across the entire game:

| Act | Duration | Tension Trend | Content Focus | Player State |
|-----|----------|--------------|---------------|-------------|
| Act 1 (Tutorial) | 10-15% of game | Low → Medium | Mechanic introduction, world setup | Learning |
| Act 2a (Rising) | 25-30% | Medium → High | New mechanics combine, stakes rise | Engaged |
| Act 2b (Midpoint) | 10-15% | Peak → Drop | Major story beat, paradigm shift | Invested |
| Act 3a (Escalation) | 25-30% | Medium → Very High | Hardest content, full toolkit used | Mastery |
| Act 3b (Climax) | 10-15% | Maximum → Resolution | Final boss, story payoff | Triumph |

### Mechanic Introduction Rhythm

- **Introduce**: Teach one mechanic in isolation with low risk
- **Reinforce**: Repeat in slightly varied context (3-5 repetitions)
- **Test**: Present a challenge that requires understanding the mechanic
- **Combine**: Mix with a previously learned mechanic
- **Master**: Optional hard challenge using the mechanic at expert level

Spacing: introduce a new mechanic every 15-30 minutes of gameplay for most genres. Never introduce two new mechanics simultaneously.

---

## Spatial Design

### Navigation Clarity Principles

- **Breadcrumbs**: Use lighting, color, landmarks, and audio to guide the player toward objectives
- **Weenies**: Tall, visible landmarks that orient the player in open spaces
- **Gating**: Physical, ability, or narrative gates that control progression flow
- **Sightlines**: Player should be able to see the next objective or area of interest from key vantage points
- **Return paths**: Shortcuts and fast travel for backtracking-heavy designs

### Exploration Reward Placement

| Reward Type | Placement | Visibility | Purpose |
|-------------|-----------|-----------|--------|
| Critical path reward | On main route | Obvious | Maintain momentum |
| Side path reward | Slightly off main route | Visible entrance | Encourage exploration |
| Hidden reward | Behind secret or puzzle | Not immediately visible | Reward curiosity |
| Skill reward | Behind challenge | Visible but gated by ability | Reward mastery |
| Backtrack reward | In previously accessible area with new tool | Context-dependent | Reward memory and return |

### Camera-Specific Spatial Rules

| Camera | Spatial Considerations |
|--------|----------------------|
| Top-down | Height conveyed through shadows, overlaps; clear walkable vs. blocked areas |
| Side-scrolling | Vertical and horizontal flow; platform spacing; screen-by-screen readability |
| Isometric | Depth sorting clarity; occlusion management; interaction range clarity |
| Third-person | Sightlines, cover geometry, camera collision, verticality |
| First-person | Field of view coverage, landmark density, audio navigation cues |
| Fixed camera | Pre-composed framing, entrance/exit placement, tank-control considerations |

---

## Encounter Design

### Encounter Composition Framework

An encounter is any interactive challenge. Build encounters from:

| Component | Definition | Example |
|-----------|-----------|--------|
| Threat | Something that can hurt the player | Enemy, hazard, timer |
| Enabler | Something that helps the player | Cover, power-up, ally |
| Modifier | Something that changes the rules | Terrain effect, buff zone, weather |
| Objective | What the player must achieve | Kill all, survive, reach exit, protect target |

### Encounter Difficulty Formula

```
Encounter Difficulty = (Total Threat Power) - (Enabler Value) ± (Modifier Impact)
```

Compare against player's expected power level from [balance-economy.md](balance-economy.md).

### Boss Design Checklist

For every boss encounter:

- [ ] Clear visual/audio telegraph for every attack
- [ ] At least 2 phases with distinct behavior changes
- [ ] One mechanic that tests a skill the player has been developing
- [ ] One safe moment per cycle to attack or heal
- [ ] Health bar or clear damage feedback
- [ ] No damage that the player cannot learn to avoid
- [ ] Arena design supports the boss's mechanics
- [ ] Reward matches the investment (time, resources, emotional stakes)

### Encounter Diversity Matrix

Track encounter variety to avoid repetition:

| Encounter ID | Enemies | Objective | Environment | Mechanic Tested | Difficulty |
|-------------|---------|-----------|-------------|-----------------|----------|
| E01 | 3 melee grunts | Kill all | Flat arena | Basic combat | Easy |
| E02 | 2 ranged + 1 melee | Kill all | Pillared room | Cover use | Medium |
| E03 | Swarm + elite | Survive 60s | Open field | Crowd control | Hard |
| E04 | None (puzzle) | Open door | Pressure plate room | Physics puzzle | Medium |
| E05 | Boss + adds | Kill boss | Multi-level arena | Phase recognition | Hard |

---

## Content Structure Templates

### Linear Progression

```
Level 1 → Level 2 → Level 3 → ... → Final Level
```
- Best for: platformers, puzzle games, narrative-driven action
- Each level self-contained, clear progression
- Risk: no player agency in path choice

### Hub and Spoke

```
        Level A
         ↑
Level D ← HUB → Level B
         ↓
        Level C
```
- Best for: metroidvania, adventure, RPG
- Hub provides rest, shop, story; spokes provide challenges
- Players choose order (within gating constraints)

### Open World Regions

```
Region A ↔ Region B ↔ Region C
   ↕            ↕            ↕
Region D ↔ Region E ↔ Region F
```
- Best for: open world RPGs, survival, exploration games
- Each region has a difficulty band and unique content
- Soft-gating through difficulty, hard-gating through story or ability

### Procedural Generation

```
Start Room → [Generated Floor: Room Pool × Rules] → Exit/Boss → Next Floor
```
- Best for: roguelike, roguelite, endless modes
- Define: room templates, connection rules, difficulty scaling, reward distribution
- Must-have: guaranteed shop before boss, no impossible rooms, max floor length

### Wave-Based

```
Wave 1 → Intermission → Wave 2 → ... → Boss Wave → Victory
```
- Best for: tower defense, arena survival, horde mode
- Define: wave budget, enemy composition rules, intermission duration, escalation rate

---

## Level Documentation Format

### Level Design Document Template

```
LEVEL: [Name/ID]
PURPOSE: [Tutorial / Test / Reward / Narrative / Boss / Hub]
DURATION: [Expected play time]
DIFFICULTY: [1-10 relative to game]
PREREQUISITES: [What the player must know/have]

LAYOUT:
- [Description or sketch reference of spatial structure]
- Key areas: [list with gameplay purpose for each]
- Flow: [intended player path through the space]

ENCOUNTERS:
- [List each encounter with composition and objective]

REWARDS:
- [Critical path rewards]
- [Optional/hidden rewards]

PACING:
- [Entry] → [Build event] → [Peak moment] → [Relief] → [Exit]

NARRATIVE BEATS:
- [Story elements delivered in this level, if any]

ART REQUIREMENTS:
- Tileset/biome: [x]
- Unique props: [list]
- Lighting mood: [x]

AUDIO REQUIREMENTS:
- BGM: [track reference or mood]
- Ambient: [soundscape description]
- Key SFX: [encounter-specific sounds]

TESTING NOTES:
- [Specific things to playtest]
- [Known risk areas]
```

### Zone Overview Template

For larger games, document zones at a higher level:

```
ZONE: [Name]
LEVELS CONTAINED: [Count and list]
PROGRESSION ROLE: [Where in the game arc]
DIFFICULTY BAND: [Min-Max]
NEW MECHANICS INTRODUCED: [List]
BIOME: [Visual/audio theme]
NARRATIVE ARC: [Zone-level story summary]
BOSS: [Yes/No, name if yes]
ESTIMATED PLAY TIME: [Hours]
```
