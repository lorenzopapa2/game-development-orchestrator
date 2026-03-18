# Creative Direction

## Goal

Establish a unified creative vision that connects world, narrative, visual identity, audio identity, and emotional intent across all game modules. This file is the connective tissue between art, audio, level design, UI, and balance — ensuring every discipline serves the same creative intent.

## When To Use

- At project start: define the creative pillars before any asset production
- When disciplines diverge: realign art, audio, level design, and UI to a shared vision
- When onboarding new contributors: give them the "why" behind every visual and narrative choice
- When making cut decisions: evaluate what to keep based on creative coherence, not just production cost

---

## World-Building Framework

### Setting Premise
Define in one paragraph:
- When and where the game takes place
- What is normal in this world
- What disruption drives the game's events
- What makes this world distinct from similar settings

### World Rules
Establish 3-5 rules that govern the world and affect gameplay:
- Physical rules (gravity, magic system, technology level)
- Social rules (factions, power structures, taboos)
- Aesthetic rules (what materials exist, what colors dominate, what sounds fill the space)

### History That Matters
Only define history that directly affects gameplay or player understanding:
- 2-3 key events that shaped the current state
- Faction origins tied to gameplay mechanics
- Ruins, artifacts, or scars in the world that tell the story visually

### Faction Identity Template

For each faction or major group:

| Attribute | Definition |
|-----------|----------|
| Name | Faction name and any aliases |
| Core belief | One sentence philosophy |
| Visual signature | Color palette, shape language, material preference |
| Audio signature | Instrument family, tempo range, harmonic character |
| Territory | Biome or region association |
| Gameplay role | Enemy type, ally, merchant, quest giver, rival |
| Symbol/motif | Recurring icon or pattern |

---

## Style Bible Framework

The style bible is the single source of truth for the game's visual and tonal identity. Keep it to one page for quick reference, with deeper documentation linked per section.

### Color System

Define the game's color logic:

- **Primary palette**: 3-5 core colors that define the game's identity
- **Faction palettes**: Each faction gets a dominant + accent color pair
- **Functional colors**: Danger (red), safe (green), interactive (gold/yellow), narrative (blue/purple) — or remap for your world
- **Saturation rules**: Overall saturation level, when to desaturate (danger, flashback), when to oversaturate (power-up, climax)
- **Value structure**: Light vs. dark ratio for readability, mood guidance

### Shape Language

- **Hero shapes**: Round (friendly), angular (aggressive), geometric (technological), organic (natural)
- **Faction shapes**: Each faction uses a dominant shape family
- **Environment shapes**: Architecture and terrain follow the same shape rules
- **Silhouette test**: Every important element must be identifiable by silhouette alone

### Material Language

- **Surface vocabulary**: What materials exist in this world (wood, stone, metal, crystal, bone, fabric, etc.)
- **Wear and damage rules**: Pristine vs. weathered vs. ruined — where does this world sit?
- **Texture density**: Matches camera distance and rendering style
- **Material hierarchy**: Which materials signal power, poverty, magic, technology

### Lighting Direction

- **Key light motivation**: Sun, moon, artificial, magical, bioluminescent
- **Color temperature rules**: Warm for safety, cool for danger (or inverted for your world)
- **Contrast level**: High contrast for action readability, low contrast for atmosphere
- **Time of day logic**: If applicable, how light changes across the day/night cycle

### Typography Direction

- **Display font**: For titles, headings, key UI elements — personality-forward
- **Body font**: For readable text, descriptions, dialogue — clarity-forward
- **Numeric font**: For damage numbers, stats, timers — monospace or tabular preferred
- **Font mood**: How typography reinforces the world (ancient = serif, sci-fi = geometric sans, horror = distressed)

### Icon Rules

- **Style**: Flat, outlined, filled, illustrated, pixel — one style for consistency
- **Grid and sizing**: Base size, padding, stroke width
- **Color usage**: Monochrome base with functional color overlays
- **Readability**: Must be legible at smallest display size (typically 32x32 or 48x48)

---

## Narrative Design

### Narrative Delivery Methods

Choose the methods appropriate to your genre and scope:

| Method | Best For | Production Cost |
|--------|----------|----------------|
| Environmental storytelling | Exploration games, horror, walking sims | Medium (art + placement) |
| Dialogue trees | RPGs, visual novels, adventure games | High (writing + VO) |
| Item descriptions | Souls-like, roguelikes, loot games | Low (text only) |
| Cutscenes | Story-driven action, AAA | Very high |
| In-game events | Roguelikes, simulations, strategy | Medium (scripting) |
| UI/menu narrative | Incremental, management, meta-games | Low |
| Audio logs | Horror, sci-fi, immersive sims | Medium (VO) |
| Companion commentary | Platformers, puzzle, adventure | Medium (writing + VO) |

### Story Structure By Genre

- **Linear**: Beginning → rising action → climax → resolution (platformers, action, puzzle)
- **Branching**: Common route → decision points → multiple endings (RPG, visual novel)
- **Emergent**: Player-generated stories from systemic interaction (sandbox, simulation, roguelike)
- **Episodic**: Self-contained arcs within a larger framework (live-service, seasonal)
- **Environmental**: No explicit narrative — world tells the story (exploration, horror)
- **Layered**: Surface story + deeper lore for invested players (Souls-like approach)

### Character Writing Guidelines

For each significant character, define:

- **Role in gameplay**: What does the player do with/to/for this character?
- **Personality in one line**: Adjective + motivation + flaw
- **Voice**: Formal/casual, verbose/terse, emotional/stoic — defines dialogue tone
- **Arc**: Does this character change? What triggers the change?
- **Gameplay-narrative link**: How does the character's story connect to mechanics?

### Character Archetype Template

| Field | Content |
|-------|--------|
| Name | Character name |
| Role | Gameplay function (player, ally, vendor, boss, narrator) |
| Personality | One-line personality summary |
| Visual hook | What makes them instantly recognizable |
| Audio hook | Voice quality, associated instrument or motif |
| Arc summary | Start state → catalyst → end state |
| Key lines | 2-3 representative dialogue lines |

### Quest / Mission Design Framework

For narrative-driven games:

1. **Hook**: Why does the player care? (Emotional, mechanical reward, curiosity)
2. **Objective**: What does the player do? (Clear, measurable, achievable)
3. **Complication**: What makes it non-trivial? (Twist, moral choice, skill challenge)
4. **Resolution**: What changes when complete? (World state, relationship, unlock)
5. **Reward alignment**: Reward matches effort and narrative weight

Quest quality test: Can the player explain to a friend what they did and why it mattered?

---

## Tone and Mood Framework

### Emotional Targets By Game Phase

Define what the player should feel at each stage:

| Phase | Target Emotion | Design Levers |
|-------|---------------|---------------|
| First 5 minutes | Curiosity + competence | Tutorial clarity, world mystery |
| Core loop (per session) | Flow + discovery | Challenge calibration, reward pacing |
| Mid-game | Investment + mastery | Depth reveal, meaningful choices |
| Climax / boss | Tension + triumph | Difficulty spike, audiovisual escalation |
| Endgame / completion | Satisfaction + nostalgia | Payoff on setup, reflection moment |

### Tone Consistency Rules

- Every asset (visual, audio, text) should pass the "does this belong in this world?" test
- Humor level: define the ceiling (no humor, dry wit, slapstick, absurdist) — inconsistent humor breaks immersion faster than anything
- Violence level: define the ceiling and stick to it (implied, cartoon, stylized, realistic, graphic)
- Emotional range: define what emotions the game will NOT attempt (prevents tonal whiplash)
- Reference filter: maintain a "yes references" and "no references" list for the entire team

### Mood Board Structure

Organize mood references into:

1. **World mood**: 5-8 reference images showing the world's feeling
2. **Character mood**: 5-8 references for character design sensibility
3. **Color mood**: 3-5 palette references
4. **UI mood**: 3-5 references for interface tone
5. **Audio mood**: 3-5 music/sound references (linked, not images)

---

## Cross-Module Integration

### How Creative Direction Feeds Each Module

| Module | Creative Direction Input |
|--------|------------------------|
| Art & Animation | Style bible, faction visuals, shape/color language, material rules |
| Audio Design | Faction audio signatures, mood targets, tone ceiling, world soundscape |
| Level Design | World rules, biome identities, environmental storytelling placement |
| UI/UX Design | Typography, icon rules, color system, tone of text/labels |
| Balance & Economy | World-consistent reward naming, faction power fantasy alignment |
| Image Generation | Style anchor, continuity block, mood board, character archetypes |
| Narrative Design | Character templates, quest framework, story structure selection |

### Creative Review Checklist

Before major milestones, verify:

- [ ] All new assets pass the silhouette test
- [ ] Color usage follows the defined palette system
- [ ] New characters fit established shape language
- [ ] Audio additions match faction/biome signatures
- [ ] UI elements use the correct typography and icon style
- [ ] Narrative content matches the defined tone ceiling
- [ ] No tonal contradictions between art, audio, and text
- [ ] World rules are not violated by new mechanics or content

---

## Templates

### One-Page Style Bible Template

```
GAME: [Name]
GENRE: [Genre]
TONE: [1-3 adjective summary]

COLOR: Primary [hex/name], Secondary [hex/name], Accent [hex/name]
       Danger [hex], Safe [hex], Interactive [hex]
SHAPES: Hero=[round/angular/organic], Enemies=[shape], Environment=[shape]
MATERIALS: Primary=[wood/metal/stone/etc.], Wear level=[pristine/worn/ruined]
LIGHT: Key=[natural/artificial/magical], Temperature=[warm/cool/neutral]
FONT: Display=[font], Body=[font], Numbers=[font]
ICONS: Style=[flat/outlined/filled], Size=[px], Color=[mono+functional]

WORLD: [One sentence setting]
MOOD: [Target emotional range]
HUMOR: [None / Dry / Light / Absurd]
VIOLENCE: [Implied / Cartoon / Stylized / Realistic]

FACTIONS:
  [Name]: Color=[x], Shape=[x], Material=[x], Sound=[x]
  [Name]: Color=[x], Shape=[x], Material=[x], Sound=[x]
```

### Faction Identity Card Template

```
FACTION: [Name]
BELIEF: [One sentence]
COLORS: Primary [hex], Accent [hex]
SHAPES: [Dominant shape family]
MATERIALS: [2-3 key materials]
SOUND: [Instrument family], [Tempo], [Mood]
TERRITORY: [Biome/region]
SYMBOL: [Description of recurring motif]
GAMEPLAY ROLE: [Enemy/ally/neutral + mechanical function]
```

### Biome / Zone Identity Template

```
ZONE: [Name]
WORLD POSITION: [Where in the world map / progression]
MOOD: [2-3 adjectives]
COLORS: Dominant [x], Accent [x], Ambient light [x]
MATERIALS: Ground [x], Structures [x], Vegetation [x]
SOUND: Ambient [description], Music mood [x], Signature SFX [x]
WEATHER: [Default state], [Variation if applicable]
NARRATIVE ROLE: [What story does this place tell?]
GAMEPLAY ROLE: [What type of gameplay dominates here?]
UNIQUE ELEMENT: [What makes this zone memorable?]
```
