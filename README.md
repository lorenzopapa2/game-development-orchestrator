# Game Development Orchestrator

A Claude Code skill that turns rough game ideas into structured, shippable development plans. Covers the full pre-production and production pipeline — from initial concept to launch operations.

## What It Does

Give it a game idea (as vague as "a space roguelike" or as detailed as a full GDD), and it will produce:

- **Strategy** — target audience, differentiation, monetization model, success metrics, competitor analysis
- **Numerical Balance** — combat formulas, economy flows, progression curves, difficulty tuning, gacha/probability systems
- **Level Design** — pacing curves, encounter composition, spatial layouts, boss design checklists
- **Creative Direction** — style bible, world-building, faction identity, tone and mood framework
- **Art Pipeline** — multi-tool routing (Nano Banana for concepts, Pencil MCP for UI, Midjourney for realism), asset specs, animation budgets
- **Audio Design** — SFX matrix, BGM zone mapping, adaptive audio parameters, voice planning
- **UI/UX** — information architecture, screen flows, interaction states, platform adaptation, accessibility
- **Technical Design** — system architecture, data contracts, config schemas (code output available on request)
- **QA & Testing** — test matrices, playtest methodology, bug management, balance validation
- **Launch Operations** — store page optimization, analytics event schemas, live-ops framework, post-launch roadmap

## Key Features

- **Genre-Aware**: Detects game genre and loads specific templates, benchmarks, and risk profiles for 12+ genres (RPG, Roguelike, Tower Defense, Fighting, Card Game, Puzzle, Strategy, Survival, Idle, Visual Novel, Simulation, and hybrids)
- **Data-Driven**: Mathematical models for damage formulas, XP curves, economy balance, PRD probability, Elo matchmaking, and Lanchester's laws
- **Production Risk Assessment**: Built-in scope warnings, team size reality checks, and feature cost heuristics that flag unrealistic proposals before they waste resources
- **Technical Art Specs**: Platform-specific polygon budgets, texture limits, shader complexity caps, and performance targets for mobile/PC/console
- **Multi-Tool Art Pipeline**: Routes art tasks to the best tool (Nano Banana, Pencil MCP, or Midjourney) with graceful fallback to text specs when tools are unavailable
- **Project Context Aware**: Can scan an existing project directory (Unity, Unreal, Godot) and adapt advice to the user's code style and architecture
- **Code When You Need It**: Defaults to design documents and specs, but outputs engine-specific code or pseudocode when explicitly requested

## Installation

### Claude Code (CLI)

```bash
claude install lorenzopapa2/game-development-orchestrator
```

### Manual

Clone this repo into your Claude Code skills directory:

```bash
git clone https://github.com/lorenzopapa2/game-development-orchestrator.git
```

## Usage

```
$game-development-orchestrator
```

### Example Prompts

```
"帮我把这个游戏点子做成完整开发方案。"
"设计我这个 RPG 的战斗数值体系。"
"为 Unity 2D roguelike 做核心循环、任务规划和技术架构。"
"用 Nano Banana 给我的游戏做高质量角色设定图。"
"用 Pencil 做一个 RPG 背包界面。"
"帮我做关卡难度曲线设计。"
"Design the economy and gacha system for my mobile RPG."
"Plan the store page and launch timeline for my indie game."
"做一个太空题材的 Roguelike 的完整策划方案。"
```

## File Structure

```
game-development-orchestrator/
├── SKILL.md                          # Main orchestrator — workflow, routing, policies
├── agents/
│   └── openai.yaml                   # Agent interface config
└── references/
    ├── genre-templates.md            # 12+ genre blueprints with hybrid rules
    ├── creative-direction.md         # Style bible, world-building, narrative design
    ├── balance-economy.md            # Combat math, economy, progression, difficulty
    ├── level-design.md               # Pacing, encounters, spatial layout, boss design
    ├── audio-design.md               # SFX matrix, BGM layers, adaptive audio
    ├── ui-ux-design.md               # Information architecture, screen flows, states
    ├── strategy.md                   # Market positioning, monetization, success metrics
    ├── planning.md                   # Scoping, milestones, effort estimation, sprints
    ├── implementation.md             # System design, data contracts, config schemas
    ├── art-animation.md              # Art pipeline, animation budgets, VFX planning
    ├── image-generation.md           # Nano Banana + Pencil MCP + Midjourney routing
    ├── collaboration.md              # Cross-team handoff, review loops, communication
    ├── qa-testing.md                 # Test matrices, playtest protocols, bug management
    ├── launch-operations.md          # Store pages, analytics, live-ops, post-launch
    └── data_models/
        ├── economy_and_progression.md  # Mathematical formulas (EHP, PRD, Elo, curves)
        ├── genre_benchmarks.md         # Hard production metrics per genre
        ├── risk_matrix.md              # Scope, tech, design, and market risk assessment
        └── technical_art_specs.md      # Platform budgets (polygons, textures, shaders)
```

## Supported Genres

RPG (Turn-Based & Action) | Roguelike / Roguelite | Tower Defense | Action / Platformer | Puzzle | Strategy / 4X | Card Game / Deckbuilder | Idle / Incremental | Survival / Crafting | Fighting Game | Simulation / Management | Visual Novel | Hybrids

## License

MIT
