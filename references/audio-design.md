# Audio Design

## Goal

Design the complete audio landscape of the game: sound effects, background music, adaptive audio systems, voice/dialogue planning, and audio asset management. This module produces audio design documentation, SFX matrices, BGM maps, and integration specifications — not audio files or code.

## When To Use

- After genre and creative direction are established (see [genre-templates.md](genre-templates.md), [creative-direction.md](creative-direction.md))
- After level design defines zones and encounters (see [level-design.md](level-design.md))
- Before production begins: audio needs drive recording/composition requirements
- When the user asks about "sound design", "music", "SFX", or "audio"

---

## Sound Effects Matrix

Map every game event to its SFX requirements:

### SFX Entry Template

| Field | Definition |
|-------|----------|
| Event | What triggers the sound |
| Category | UI / Combat / Movement / Environment / Feedback / Narrative |
| Priority | Critical (must ship) / Important (should ship) / Polish (nice to have) |
| Variants | Number of variations needed (3+ for frequently repeated sounds) |
| Spatial | 2D (UI, global) / 3D positional / Hybrid |
| Duration | Short (<0.5s), Medium (0.5-2s), Long (2s+) |
| Layering | Standalone, or layered with other SFX |
| Notes | Emotional tone, reference, special behavior |

### Core SFX Categories

**Combat SFX**
| Event | Variants | Priority | Notes |
|-------|----------|----------|-------|
| Player melee hit (light) | 3-5 | Critical | Satisfying impact, varies by weapon type |
| Player melee hit (heavy) | 3-5 | Critical | Weightier, more bass, screen shake companion |
| Player ranged fire | 3-4 | Critical | Matches weapon visual style |
| Player ranged impact | 3-4 | Critical | Distinct from melee to confirm hit at range |
| Enemy hit react | 3-5 | Critical | Confirms damage dealt |
| Enemy death | 3-5 | Critical | Satisfying, genre-appropriate (splat/poof/dissolve) |
| Player damage taken | 2-3 | Critical | Alarming, immediately recognizable |
| Block/parry | 2-3 | Important | Metallic, solid, rewarding |
| Critical hit | 1-2 | Important | Special layer on top of normal hit |
| Status effect apply | 1 per type | Important | Distinct per element/type |
| Heal | 1-2 | Critical | Positive, relief-associated |

**Movement SFX**
| Event | Variants | Priority | Notes |
|-------|----------|----------|-------|
| Footsteps | 3-5 per surface | Critical | Surface-specific (stone, wood, grass, metal, water) |
| Jump | 1-2 | Critical | Effort sound + whoosh |
| Land | 2-3 | Critical | Weight-appropriate, surface-specific |
| Dash/dodge | 1-2 | Important | Quick whoosh, directional |
| Swim/wade | 2-3 | If applicable | Water interaction |
| Climb | 2-3 | If applicable | Grip and effort sounds |

**UI SFX**
| Event | Variants | Priority | Notes |
|-------|----------|----------|-------|
| Menu open/close | 1 | Critical | Clean, non-intrusive |
| Button hover | 1 | Important | Subtle, responsive |
| Button confirm | 1 | Critical | Satisfying, clear confirmation |
| Button cancel/back | 1 | Critical | Distinct from confirm |
| Tab switch | 1 | Important | Light transition |
| Item equip | 1-2 | Important | Tactile, gear-type specific |
| Item pickup | 1-2 | Critical | Rewarding, rarity-differentiated |
| Level up / milestone | 1 | Critical | Celebratory, distinct from other sounds |
| Error/invalid action | 1 | Critical | Clearly "no", not annoying |
| Currency gain | 1 | Important | Coins/gems/appropriate metaphor |

**Environment SFX**
| Event | Variants | Priority | Notes |
|-------|----------|----------|-------|
| Door open/close | 2-3 | Important | Material-appropriate |
| Chest/container open | 1-2 | Important | Anticipation + reveal |
| Destructible break | 2-3 | Important | Material-appropriate |
| Trap trigger | 1 per type | Important | Warning quality |
| Ambient loops | 1 per zone | Critical | See BGM section for layering |
| Weather | 1 per type | If applicable | Rain, wind, thunder |

---

## BGM Design

### Zone BGM Mapping

Map every game zone/state to its music:

| Zone/State | Track Name | Mood | Tempo (BPM) | Key/Mode | Instruments | Layer Count |
|-----------|-----------|------|-------------|----------|-------------|-------------|
| Main menu | [name] | Inviting, sets tone | 80-100 | Major or neutral | Signature instrument + pad | 2-3 |
| Hub/town | [name] | Safe, warm | 90-110 | Major | Acoustic, melodic | 3-4 |
| Exploration (forest) | [name] | Curious, peaceful | 80-100 | Mixolydian | Strings, woodwinds | 3-4 |
| Combat (normal) | [name] | Energetic, urgent | 120-160 | Minor | Percussion-forward | 4-5 |
| Combat (boss) | [name] | Intense, dramatic | 130-170 | Minor/diminished | Full orchestra or synth layers | 5-6 |
| Victory | [name] | Triumphant, brief | 100-120 | Major | Brass/bright | 2-3 |
| Defeat/game over | [name] | Somber, brief | 60-80 | Minor | Sparse, reflective | 1-2 |

### Music Layer Architecture

Design music as stackable layers that can be mixed dynamically:

```
Layer 1 (Base):     Pad/ambient bed — always playing
Layer 2 (Rhythm):   Percussion — added during action/tension
Layer 3 (Melody):   Main theme — added during exploration/story
Layer 4 (Tension):  Dissonant elements — added during danger/combat
Layer 5 (Climax):   Full arrangement — boss/major moments only
```

### Transition Rules

| From | To | Method | Duration |
|------|-----|--------|----------|
| Exploration → Combat | Cross-fade with percussion lead-in | 1-2 bars |
| Combat → Victory | Hard cut to stinger, then cross-fade to exploration | Immediate + 2s |
| Combat → Defeat | Fade down, stinger | 1-2s fade |
| Zone A → Zone B | Cross-fade on area boundary | 2-4 bars |
| Gameplay → Cutscene | Duck gameplay music, bring in cinematic track | 1-2s duck |
| Menu → Gameplay | Fade out menu theme, fade in gameplay | 1-2s |

---

## Adaptive Audio

### State-Driven Audio Parameters

Design audio that responds to game state:

| Game State Parameter | Audio Response | Example |
|---------------------|---------------|--------|
| Player health low | Add heartbeat layer, filter BGM to low-pass | Below 25% HP |
| Enemy proximity | Increase tension layer volume | Within detection range |
| Combat intensity | Add percussion and raise tempo | Multiple enemies engaged |
| Time pressure | Accelerate BGM tempo or add ticking | Timer below 30s |
| Stealth mode | Reduce BGM to minimal layer, enhance ambient | While sneaking |
| Power-up active | Add energetic layer, brighter mix | Duration of effect |
| Story moment | Duck gameplay audio, spotlight dialogue/narrative | Scripted triggers |

### Middleware Concepts

When specifying adaptive audio behavior, use these concepts (applicable to FMOD, Wwise, or custom):

- **Parameter**: A game value that drives audio behavior (0-1 range typical)
- **Event**: A game action that triggers a sound
- **State**: A named game condition that switches audio behavior
- **Switch**: Selects between audio variants based on a game variable
- **Bus**: Mixing group for volume/effect control (master, music, SFX, voice, ambient)
- **Snapshot**: A preset mix state (e.g., "underwater" reduces high frequencies and adds reverb)

### Audio Trigger Design

Define when and how audio events fire:

| Trigger Type | Description | Example |
|-------------|-------------|--------|
| Direct | Gameplay action fires immediately | Attack → swing SFX |
| Proximity | Distance to source controls volume/activation | Waterfall ambient grows as player approaches |
| State change | Entering/exiting a state triggers audio | Enter combat → combat music |
| Threshold | Crossing a value boundary triggers audio | HP drops below 25% → heartbeat |
| Scheduled | Timer or beat-synced | Wave start horn every 60s |
| Random | Chance-based ambient events | 5% chance per 10s of bird call |

---

## Voice and Dialogue Audio

### Voice Planning (If Applicable)

| Parameter | Options |
|-----------|--------|
| Voice scope | No voice / Effort sounds only / Key lines voiced / Partial VO / Full VO |
| Languages | List target languages for localization |
| Cast size | Number of unique voice actors needed |
| Line count estimate | Per character, per NPC category |
| Recording format | Studio / Remote / AI-assisted (specify tool) |

### Dialogue Audio Rules

- Every voiced character needs a consistent voice profile: pitch, pace, accent, emotional range
- Barks (short combat/reaction lines): 5-10 per character minimum
- Ambient NPC chatter: 10-20 lines per NPC type, randomized
- Story dialogue: exact count from script, allow for re-takes
- Localization: budget for re-recording or subtitle-only for secondary languages

---

## Audio Asset Checklist Template

Use this to track audio production:

```
PROJECT: [Game Name]
AUDIO ENGINE: [FMOD / Wwise / Unity Native / Custom]
TOTAL SFX ESTIMATE: [count]
TOTAL BGM TRACKS: [count]
TOTAL VOICE LINES: [count or N/A]

SFX STATUS:
  Combat:       [x/total] complete
  Movement:     [x/total] complete
  UI:           [x/total] complete
  Environment:  [x/total] complete
  Feedback:     [x/total] complete

BGM STATUS:
  Composed:     [x/total]
  Layered:      [x/total]
  Integrated:   [x/total]
  Transitions:  [x/total] defined

VOICE STATUS:
  Scripts:      [x/total] finalized
  Recorded:     [x/total]
  Edited:       [x/total]
  Integrated:   [x/total]

ADAPTIVE SYSTEMS:
  Parameters defined: [list]
  States defined:     [list]
  Tested:             [yes/no]
```

---

## Genre-Specific Audio Direction

### RPG
- Rich layered BGM per zone (8-15 unique tracks)
- Battle theme with transition from exploration
- Spell/skill SFX library scaled to ability count
- Menu navigation SFX family
- Town/shop ambient with NPC chatter

### Roguelike
- Per-biome BGM with intensity layers (2-4 layers per track)
- Run-start and run-end stingers
- Item pickup SFX differentiated by rarity/power
- Procedural variation in ambient sounds
- Death sound with emotional weight (the run is lost)

### Action/Platformer
- Rhythm-aware BGM that supports movement flow
- Tight, responsive movement SFX (jump, land, dash)
- Hazard warning audio cues before visual confirmation
- Checkpoint and death jingles

### Tower Defense
- Escalating tension across waves (layer-based BGM)
- Tower placement, upgrade, and sell SFX
- Wave countdown and wave-complete fanfares
- Distinct tower firing sounds (rapid, heavy, magical)
- Boss wave introduction stinger

### Horror/Survival
- Sparse, unsettling ambient design
- Silence as a tool — absence of music is as designed as its presence
- Jump scare SFX: restraint over frequency, earned not cheap
- Environmental creaks, groans, and distant sounds
- Player breathing and heartbeat as diegetic audio

### Puzzle
- Calm, non-intrusive BGM that supports concentration
- Highly satisfying manipulation SFX (snap, click, slide)
- Progressive audio feedback for partial and complete solutions
- "Eureka" stinger for solve moments

### Card Game
- Tactile card SFX (draw, play, shuffle, flip)
- Spell/ability resolution audio escalating with power
- Opponent turn ambient tension
- Victory/defeat stingers
