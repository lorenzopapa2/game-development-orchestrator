# Art And Animation

## Goal

Make visual production serve gameplay clarity and schedule reality.

## Required Mapping

For every gameplay feature, define:

- visible game objects
- states each object can enter
- animation or VFX events per state
- UI signals required for player clarity
- audio cues if relevant

If this mapping does not exist, asset planning is incomplete.

## Multi-Tool Art Pipeline

### Tool Selection Decision Tree

Choose the right tool for each art task:

```
What are you making?
│
├─ Structured UI (wireframes, layouts, components)
│  └→ Pencil MCP
│
├─ High-fidelity concept art (characters, environments, key art)
│  └→ Nano Banana (via image-generation.md)
│
├─ Photo-realistic reference or material studies
│  └→ Midjourney
│
├─ UI style exploration (visual mood, aesthetic direction)
│  └→ Nano Banana first, then Pencil for production
│
├─ Icon or pixel art
│  └→ Nano Banana for concepts → Manual refinement
│
├─ Character sheet or prop sheet
│  └→ Nano Banana (via image-generation.md templates)
│
└─ In-engine asset
   └→ Use concepts from above as reference → Manual production
```

### Tool Strengths

| Tool | Best For | Limitations |
|------|---------|-------------|
| Pencil MCP | Interactive UI layouts, component systems, wireframes, production mockups | Not for illustration or concept art |
| Nano Banana | Character concepts, environment moods, key art, style exploration, batch consistency | Not for precise layout or interaction design |
| Midjourney | Photo-realistic references, texture studies, material exploration, architecture reference | Less control over composition, no interactive output |

### Cross-Tool Workflow

1. **Creative Direction** ([creative-direction.md](creative-direction.md)): Define style bible
2. **Style Exploration**: Nano Banana generates mood and character concepts
3. **UI Wireframing**: Pencil creates layout structure
4. **Material/Texture Reference**: Midjourney generates realistic material studies
5. **Production UI**: Pencil refines wireframes into polished mockups using style from step 2
6. **Asset Handoff**: All outputs compiled into art spec for production

## Style Bible Cross-Reference

Before starting any art production, ensure the style bible from [creative-direction.md](creative-direction.md) is established:

- Color system defined → feeds into all visual assets
- Shape language defined → feeds into character, environment, and UI design
- Material language defined → feeds into texture and rendering decisions
- Faction identities defined → feeds into all faction-specific assets

## Asset Planning

Build an asset matrix with columns such as:

- asset name
- gameplay owner
- screen size or camera distance
- style complexity
- reuse potential
- creation method: hand-made, kitbash, procedural, AI-assisted (specify tool)
- blocking dependency
- implementation destination

## Animation Planning

Specify animation state lists early:

- locomotion
- idle variants
- attack windup, release, recovery
- hit react
- death
- interact
- UI transitions
- VFX timing markers

Note whether the game needs frame-perfect gameplay timing, root motion, blend trees, sprite sheets, skeletal rigs, or cutscene tools.

### Animation Budget By Genre

| Genre | Player Animations | Enemy Animations (per type) | NPC Animations | UI Animations |
|-------|------------------|----------------------------|----------------|---------------|
| Platformer | 15-25 | 5-10 | 3-5 | 5-10 |
| Action RPG | 30-60 | 10-20 | 5-10 | 10-15 |
| Turn-Based RPG | 10-15 | 5-8 | 3-5 | 10-15 |
| Fighting Game | 40-80 per character | N/A (all are characters) | N/A | 5-10 |
| Puzzle | 5-10 | N/A | N/A | 10-20 |
| Strategy | 5-10 per unit type | 5-10 per unit type | 3-5 | 5-10 |
| Visual Novel | 1-3 (sprite changes) | N/A | 5-15 expressions | 5-10 |
| Idle/Incremental | 3-5 | 3-5 | 1-3 | 15-25 |

### Animation State List Template

```
CHARACTER: [Name/Type]
RIG TYPE: [Skeletal / Sprite sheet / Spine / Frame-by-frame]

LOCOMOTION:
  - idle (1-3 variants)
  - walk
  - run
  - jump_up
  - jump_peak
  - fall
  - land (light / heavy)
  - turn (if applicable)

COMBAT:
  - attack_light (windup → active → recovery)
  - attack_heavy (windup → active → recovery)
  - attack_special_[n]
  - hit_react (front / back if applicable)
  - block / parry (if applicable)
  - death (1-2 variants)
  - stagger

INTERACTION:
  - pickup
  - use_item
  - open_door / open_chest
  - talk (if animated)

SPECIAL:
  - [Game-specific: climb, swim, mount, transform, etc.]

VFX MARKERS:
  - [Frame numbers for particle spawn, sound trigger, hitbox activation]
```

## VFX Planning

### VFX Categories

| Category | Examples | Priority |
|----------|---------|----------|
| Combat feedback | Hit sparks, blood/particles, damage numbers | Critical |
| Ability effects | Spell casting, buff auras, projectile trails | Critical |
| Environmental | Weather, ambient particles, fog, water | Important |
| UI feedback | Button press, level up, achievement popup | Important |
| Transition | Screen wipes, teleport, death dissolve | Polish |

### VFX Specification Template

```
VFX: [Name]
TRIGGER: [What causes it]
DURATION: [Seconds]
SPAWN POINT: [Relative to character/world]
MOVEMENT: [Static / Follow source / World-space]
LAYERS: [Particles, sprites, distortion, light]
COLOR: [From style bible palette]
SCALE: [Relative to screen/camera distance]
PERFORMANCE: [Particle count budget]
```

## Sprite Sheet / Atlas Planning

For 2D games:

| Asset | Frame Count | Resolution Per Frame | Atlas Size | Animation FPS |
|-------|------------|---------------------|-----------|---------------|
| Player (all states) | [count] | [wxh] | [atlas size] | [fps] |
| Enemy Type A | [count] | [wxh] | [atlas size] | [fps] |
| Props (static) | [count] | [wxh] | [atlas size] | N/A |
| UI elements | [count] | [wxh] | [atlas size] | [fps if animated] |
| VFX sprites | [count] | [wxh] | [atlas size] | [fps] |

## 3D Art Planning (If Applicable)

| Asset | Polycount Budget | Texture Size | LOD Levels | Rig Complexity |
|-------|-----------------|-------------|-----------|---------------|
| Player character | [tris] | [resolution] | [count] | [bone count] |
| Enemy (common) | [tris] | [resolution] | [count] | [bone count] |
| Environment (modular) | [tris per piece] | [resolution] | [count] | N/A |
| Props | [tris] | [resolution] | [count] | N/A |

## Art Pipeline Stages

### Production Pipeline With Tool Mapping

| Stage | Description | Tool | Output | Gate |
|-------|-----------|------|--------|------|
| 1. Concept | Mood exploration, silhouette studies | Nano Banana | Concept images | Creative director approval |
| 2. Reference | Material studies, real-world reference | Midjourney | Reference boards | Style consistency check |
| 3. Design | Detailed character/environment design | Nano Banana → Manual refinement | Design sheets | Team review |
| 4. UI Layout | Interface wireframing and structure | Pencil MCP | Wireframe files | UX review |
| 5. UI Production | High-fidelity interface mockups | Pencil MCP | Production mockups | Visual QA |
| 6. Production | In-engine asset creation | Engine tools / DCC tools | Game-ready assets | Technical validation |
| 7. Integration | Assets in-game with animation, VFX, audio | Engine | Playable build | Playtest |
| 8. Polish | Final tuning, effects, transitions | All tools | Polished build | Final review |

## Art Direction Rules

- Pick a style the team can sustain, not just admire.
- Match detail level to camera distance and content volume.
- Favor readability over rendering ambition for action-heavy games.
- Lock naming conventions, pivot rules, export format, and texture limits before asset production scales.

## Common Failures

- one concept image treated as a production pipeline
- animation count underestimated by ignoring state variations
- effects and UI feedback left until the end even though they define game feel
- AI image generation used without conversion rules for in-engine consistency
- no art review process — individual artists diverge from style bible
- VFX performance budget not defined until optimization phase
- 3D models built at AAA quality for an indie-scale project
