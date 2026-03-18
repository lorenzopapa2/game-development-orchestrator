# Implementation

## Important: No Code Generation

This module produces **system design documents, data contracts, configuration schemas, and architecture specifications** — not source code. The Game Development Orchestrator is a game design and planning tool. When implementation details are needed, output them as design specifications that a developer can implement in any engine or language.

## Goal

Translate game design into buildable systems with clear boundaries, data contracts, and configuration-driven design.

## Implementation Order

1. Model gameplay states and transitions.
2. Define the minimum runtime systems needed for the next milestone.
3. Define data contracts between systems.
4. Define content authoring workflow.
5. Define instrumentation, debug commands, and test surfaces.

## System Design Rules

- Prefer specific systems over premature generic frameworks.
- Align subsystem boundaries with actual gameplay responsibilities.
- Make state explicit. Hidden state causes most game bugs.
- Build a fast iteration loop: config reload, cheats, logging, visualizers, test scenes.
- Treat tools and pipeline code as production code if designers or artists depend on them.

## Configuration Schema Design

### Data-Driven Game Systems

Instead of hardcoding game behavior, define configuration schemas that drive gameplay. This approach allows designers to tune without code changes.

#### Schema Definition Template

For each game system, define its config schema:

```
SYSTEM: [System Name]
CONFIG FILE: [filename.json / .yaml / .csv]
OWNER: [Who edits this — designer, artist, programmer]
RELOAD: [Hot-reload supported? Yes/No]

SCHEMA:
  [field_name]:
    type: [int / float / string / enum / array / object]
    range: [min-max or valid values]
    default: [default value]
    description: [what this controls]
    affects: [which gameplay behavior changes]

EXAMPLE:
  [One complete example entry]

VALIDATION RULES:
  - [Rule 1: e.g., damage must be > 0]
  - [Rule 2: e.g., all referenced IDs must exist in master table]
```

#### Common Config Schemas

**Enemy Config**
```
enemy_id: string (unique)
display_name: string
hp: int [1-99999]
damage: int [1-9999]
speed: float [0.1-10.0]
armor: int [0-999]
xp_reward: int [1-9999]
loot_table_id: string (reference)
behavior_id: string (reference)
animation_set_id: string (reference)
audio_set_id: string (reference)
```

**Item Config**
```
item_id: string (unique)
display_name: string
rarity: enum [common, uncommon, rare, epic, legendary]
category: enum [weapon, armor, consumable, material, key]
stats: object { stat_id: modifier_value }
price_buy: int [0-999999]
price_sell: int [0-999999]
icon_id: string (reference)
description: string
max_stack: int [1-999]
```

**Level Config**
```
level_id: string (unique)
display_name: string
biome_id: string (reference)
difficulty: int [1-10]
encounter_list: array of encounter_id
reward_list: array of { item_id, quantity, probability }
bgm_id: string (reference)
ambient_id: string (reference)
next_level_id: string (reference, nullable)
prerequisites: array of level_id
estimated_duration_minutes: int [1-120]
```

### Data Flow Diagrams

Document how data moves between systems:

```
[Player Input]
      ↓
[Input Controller] → reads → [Control Config: keybindings, sensitivity]
      ↓
[Player State Machine] → reads → [Player Config: speed, jump height, abilities]
      ↓
[Combat Resolver] → reads → [Weapon Config, Enemy Config, Damage Formula Config]
      ↓ outputs
[Damage Event] → consumed by → [VFX System, Audio System, UI System, AI System]
      ↓
[Loot Dropper] → reads → [Loot Table Config, Rarity Weights]
      ↓
[Inventory System] → reads → [Item Config, Inventory Capacity Config]
      ↓
[Economy System] → reads → [Shop Config, Currency Config]
      ↓
[Progression System] → reads → [XP Curve Config, Unlock Config]
      ↓
[Save System] → serializes → [Player State, Inventory State, World State, Quest State]
```

Cross-reference: see [balance-economy.md](balance-economy.md) for the numerical values that populate these configs.

## Minimum Technical Spec

For each subsystem, write:

- purpose
- input and output
- owned data
- external dependencies
- update timing or event trigger
- failure modes
- debug method

## Example Subsystems

- player controller
- combat resolver
- enemy AI state machine
- encounter director
- loot/progression config
- camera and feedback stack
- UI state presenter
- save/load or run persistence
- asset loading and pooling

## Subsystem Specification Template

```
SUBSYSTEM: [Name]
PURPOSE: [One sentence]

INPUTS:
  - [Input 1: source → data type]
  - [Input 2: source → data type]

OUTPUTS:
  - [Output 1: data type → consumers]
  - [Output 2: data type → consumers]

OWNED DATA:
  - [State variable 1: type, persistence]
  - [State variable 2: type, persistence]

CONFIG:
  - [Config reference from schema]

DEPENDENCIES:
  - [Subsystem A: what it needs from A]
  - [Subsystem B: what it needs from B]

UPDATE TIMING: [Per frame / Per tick / On event / On demand]

STATE MACHINE (if applicable):
  [State A] →(condition)→ [State B] →(condition)→ [State C]

FAILURE MODES:
  - [What can go wrong and how the system recovers]

DEBUG:
  - [How to inspect this system: logs, visualizers, cheats, test commands]
```

## Architecture Patterns For Games

| Pattern | When To Use | Subsystems |
|---------|------------|----------|
| State Machine | Character controllers, AI, game flow | Player, enemies, game manager |
| Event Bus | Decoupled systems reacting to game events | Combat → UI, audio, VFX |
| Component/Entity | Large numbers of similar-but-different game objects | Entities, abilities, modifiers |
| Data-Driven Config | Designer-tunable systems | Balance, loot, encounters, dialogue |
| Command Pattern | Undo/redo, replay, networking | Turn-based input, replays, netcode |
| Observer | UI responding to state changes | HUD updates, achievement tracking |

## Engineering Red Flags

- abstract entity framework before one concrete gameplay slice works
- configuration spread across code, prefabs, spreadsheets, and prompts with no source of truth
- no plan for determinism, rollback, or save compatibility when those matter
- asset naming and folder structure undefined
- no ownership for integration bugs between design data and runtime code
- designing the engine instead of the game
- optimizing before profiling
- no automated build or test pipeline for a team larger than 2
