# Planning

## Goal

Convert the strategy into a dependency-aware production plan.

## Milestone Order

1. Paper design or simulation
2. Graybox prototype
3. Vertical slice
4. Content-ready production
5. QA, polish, launch or handoff

Do not plan content production before the core interaction and technical feasibility are proven.

## Scope Framework

Split features into:

- must ship for the loop to work
- improves retention or clarity
- polish only
- future backlog

For each feature, specify:

- player-facing purpose
- dependency
- owner discipline
- acceptance test
- cut strategy

## Vertical Slice Rule

A vertical slice is not "many systems partially done". It is one representative player experience done end to end with production intent across code, UI, audio, VFX, animation, and content.

## Effort Estimation Framework

### T-Shirt Sizing

| Size | Effort | Description | Example |
|------|--------|-------------|--------|
| XS | 1-2 days | Single task, one discipline, no dependencies | Add a sound effect, fix a UI label |
| S | 3-5 days | Small feature, 1-2 disciplines | New enemy type using existing systems |
| M | 1-2 weeks | Multi-discipline feature, some dependencies | Inventory screen with art and functionality |
| L | 2-4 weeks | Major feature, multiple disciplines, integration | Combat system with animation and VFX |
| XL | 1-2 months | System-level feature, all disciplines involved | Procedural level generation with full art pass |

### Genre Calibration

Multiply base estimates by genre complexity factor:

| Genre | Complexity Factor | Reason |
|-------|------------------|--------|
| Puzzle | 0.7x | Fewer interacting systems |
| Platformer | 0.8x | Tight loop, less content variety |
| Visual Novel | 0.8x | Art-heavy but system-light |
| RPG (Turn-Based) | 1.2x | Many interacting systems, content volume |
| Action RPG | 1.5x | Real-time feel + RPG depth |
| Roguelike | 1.3x | Procedural generation + balance complexity |
| Strategy/4X | 1.5x | Deep systems, AI, balance |
| Open World | 2.0x | Content volume + technical complexity |
| Multiplayer (any) | 1.5-2.0x | Networking, sync, anti-cheat |

## Team Size Heuristics

### Solo Developer (1 person)
- Focus: one genre, minimal scope, use asset stores and AI tools heavily
- Realistic scope: 6-18 months for a small complete game
- Risk: burnout, no external feedback loop
- Mitigation: monthly public playtest, strict scope cuts at month 3

### Small Team (2-5 people)
- Focus: clear role division, shared vision document
- Realistic scope: 12-24 months for a mid-scope game
- Risk: communication overhead, skill gaps
- Mitigation: weekly sync, cross-trained on one backup skill each

### Medium Team (5-15 people)
- Focus: department leads, formal milestone reviews
- Realistic scope: 12-36 months for a full-featured game
- Risk: coordination overhead, scope creep, integration bugs
- Mitigation: bi-weekly integration builds, dedicated QA, scope review every milestone

### Large Team (15+ people)
- Focus: pipeline tooling, formal production management
- Realistic scope: 18-48+ months for large games
- Risk: communication breakdown, wasted work, department silos
- Mitigation: daily standups, sprint cycles, dedicated producers, automated builds

## Genre-Specific Milestone Templates

### RPG / Action RPG Milestones

| Milestone | Exit Criteria | Duration |
|-----------|-------------|----------|
| Paper Design | Core loop, 5 enemy types, stat system on paper, economy sketch | 2-4 weeks |
| Graybox | Player controller + 1 enemy + basic combat + 1 test room | 4-8 weeks |
| Vertical Slice | 1 complete zone: combat, loot, 1 boss, UI, audio, save/load | 8-16 weeks |
| Alpha | All systems functional, 30-50% content | 12-24 weeks |
| Beta | All content in, polish pass, full QA | 8-16 weeks |
| Launch | All bugs S2+ resolved, performance targets met | 4-8 weeks |

### Roguelike Milestones

| Milestone | Exit Criteria | Duration |
|-----------|-------------|----------|
| Paper Design | Core loop, item list (20+), floor structure, meta-progression plan | 2-3 weeks |
| Graybox | 1 run: 3 floors, 5 rooms each, basic combat, 10 items | 4-8 weeks |
| Vertical Slice | Full run: procedural generation, 20+ items, 1 boss, meta-progress | 8-12 weeks |
| Alpha | 3+ biomes, 50+ items, 3+ bosses, full meta-progression | 12-20 weeks |
| Beta | All content, balance pass, achievements, polish | 8-12 weeks |

### Puzzle Game Milestones

| Milestone | Exit Criteria | Duration |
|-----------|-------------|----------|
| Paper Design | Core mechanic defined, 10 puzzle sketches, complexity curve | 1-2 weeks |
| Prototype | 10 playable puzzles, core mechanic feels right | 2-4 weeks |
| Vertical Slice | 20 puzzles, 2 worlds, tutorial, polish on first world | 4-8 weeks |
| Alpha | All puzzles designed and playable | 4-8 weeks |
| Beta | Art pass, audio, accessibility, hint system | 4-8 weeks |

## Dependency Graph Patterns

### Common Dependency Chains

```
Game Design Doc → Prototype
    ├→ Player Controller → Combat System → Enemy AI → Encounters → Boss
    ├→ Core UI Framework → HUD → Inventory → Shop → Character Screen
    ├→ Level Graybox → Art Pass → Lighting → VFX → Polish
    ├→ Audio Design → SFX Implementation → BGM Integration → Adaptive Audio
    └→ Save System → Progression → Meta-game → Achievements
```

### Dependency Rules
- Never start art production before graybox approval
- Never start balance tuning before core systems are functional
- Never start audio integration before gameplay timing is stable
- Never start localization before text is final
- Always have a playable build before adding content

## Risk Register Template

| Risk ID | Risk Description | Probability | Impact | Mitigation | Owner | Status |
|---------|-----------------|------------|--------|-----------|-------|--------|
| R01 | Combat doesn't feel good after prototype | Medium | Critical | Budget 2 extra weeks for feel tuning | Design Lead | Open |
| R02 | Art style too ambitious for team size | High | Major | Define art LOD ladder, test at lowest tier first | Art Lead | Open |
| R03 | Procedural generation produces bad levels | Medium | Major | Hand-curate room templates, constrain generation rules | Design Lead | Open |
| R04 | Scope creep during production | High | Critical | Monthly scope review, scope cut ladder defined | Producer | Open |
| R05 | Key team member unavailable | Low | Critical | Cross-train on critical systems, document everything | Producer | Open |

## Sprint Template

```
SPRINT: [Number] — [Name/Theme]
DURATION: [2 weeks recommended]
GOAL: [One sentence: what is shippable at the end?]

TASKS:
| Task | Owner | Size | Dependency | Status |
|------|-------|------|-----------|--------|
| [Task 1] | [Name] | S | None | To Do |
| [Task 2] | [Name] | M | Task 1 | Blocked |
| [Task 3] | [Name] | S | None | To Do |

SPRINT REVIEW CRITERIA:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

RISKS THIS SPRINT:
- [Risk and mitigation]

CARRYOVER FROM LAST SPRINT:
- [Tasks that didn't complete and why]
```

## Planning Outputs

Prefer these structures:

- milestone table with exit criteria
- dependency graph
- sprint board seeded with implementation-ready tasks
- risk register
- scope cut ladder from safest cuts to highest-impact cuts
- effort estimation matrix with T-shirt sizes
- team allocation map

## Common Planning Mistakes

- scheduling UI, VFX, or animation after engineering lock when they affect feel
- vague tasks like "build combat system"
- no integration buffer
- no debug or telemetry tasks
- assuming tools/pipeline work without proving import, iteration, and export speed
- underestimating art and audio production time
- not planning for playtesting sessions in the schedule
- treating QA as a phase instead of a continuous process
- no contingency time (add 20-30% buffer to all estimates)
- planning the dream scope instead of the minimum shippable scope
