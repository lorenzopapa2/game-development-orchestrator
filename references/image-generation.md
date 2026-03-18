# Image Generation

## Goal

Use multiple image generation tools to produce game visuals: concept art, key art, UI mockups, character sheets, prop sheets, environment mood frames, marketing stills, and production-ready interface designs. Route each task to the best tool based on the asset type and production stage.

## Tool Selection Decision Tree

```
What are you generating?
│
├─ Concept art, character design, environment mood, key art, prop sheets
│  └→ Nano Banana (high-fidelity, batch-consistent, game-optimized)
│
├─ UI wireframes, layout prototypes, interactive mockups
│  └→ Pencil MCP (structured, component-based, designable)
│
├─ Photo-realistic references, texture studies, architectural reference
│  └→ Midjourney (realistic rendering, material quality)
│
├─ UI style exploration (visual direction)
│  └→ Nano Banana for mood → Pencil for production
│
├─ In-game AI-generated textures or illustrations within Pencil
│  └→ Pencil G() operation (AI image generation within design files)
│
└─ Not sure?
   └→ Default to Nano Banana for concepts, Pencil for UI, Midjourney for realism
```

### Tool Comparison Matrix

| Capability | Nano Banana | Pencil MCP | Midjourney |
|-----------|-------------|-----------|----------|
| Concept art | Excellent | Not suited | Good |
| Character sheets | Excellent | Not suited | Moderate |
| Environment moods | Excellent | Not suited | Excellent |
| UI wireframes | Not suited | Excellent | Not suited |
| Production UI mockups | Not suited | Excellent | Not suited |
| Photo-realistic reference | Good | Not suited | Excellent |
| Batch consistency | Excellent (continuity blocks) | Excellent (component reuse) | Moderate (--sref helps) |
| Interactive prototypes | Not possible | Excellent | Not possible |
| Icon design | Good | Good (vector-like) | Good |
| Marketing key art | Excellent | Not suited | Excellent |
| Texture/material studies | Good | Not suited | Excellent |

### Cross-Tool Workflow Patterns

**Pattern 1: Character Pipeline**
1. Nano Banana → Silhouette explorations (4-8 variants)
2. Nano Banana → Refined character sheet (locked direction)
3. Midjourney → Material reference studies for costume details
4. Pencil → Character selection UI using approved design

**Pattern 2: UI Pipeline**
1. Nano Banana → UI style mood exploration (3 visual directions)
2. Pencil → Wireframe layout (information architecture)
3. Pencil → Production mockup (applying chosen visual style)
4. Pencil G() → AI-generated background or illustration elements within UI

**Pattern 3: Environment Pipeline**
1. Midjourney → Real-world reference collection (architecture, nature, materials)
2. Nano Banana → Stylized environment mood frames
3. Nano Banana → Gameplay-readable scene compositions
4. Pencil → Environment-specific UI overlays (HUD in context)

**Pattern 4: Marketing Pipeline**
1. Nano Banana → Key art explorations
2. Midjourney → Photo-realistic alternative for certain store pages
3. Pencil → Store page mockup layout with screenshots and text

---

## Nano Banana Image Generation

### Default Rule

- Default to Nano Banana for high-fidelity image generation.
- Do not generate a single isolated image when the user is building a game pipeline.
- Generate image sets with shared constraints so the art can be reused across design, implementation, and iteration.

### Required Inputs

Extract or ask for these before generating prompts:

- game genre
- target platform
- camera perspective
- art style references
- target use: concept, production guide, UI mockup, marketing, sprite base, loading screen
- subject type: character, enemy, prop, environment, icon, interface
- continuity requirement: one-off or style-consistent batch
- output framing: portrait, full body, orthographic, isometric, close-up, wide shot

### Prompt Pack Structure

Build prompts in layers instead of one paragraph:

1. identity
2. gameplay role
3. silhouette and proportion
4. materials and costume language
5. mood and lighting
6. composition and camera
7. style and rendering constraints
8. exclusions

Example structure:

- subject: forest ranger heroine, mid-20s, agile ranged fighter
- gameplay role: readable player character for top-down action roguelike
- silhouette: triangular cape, compact bow, strong side profile
- material language: weathered leather, moss fabric, brass utility clips
- mood: disciplined, alert, slightly mythic
- camera: character sheet, front side back three-quarter
- style: high-quality stylized realism, production-ready concept sheet, clean shape language
- negative constraints: no cluttered background, no extra limbs, no text watermark, no cinematic blur

### Continuity Rules

For a reusable game art pipeline, keep these fixed across a batch:

- palette logic
- material language
- shape language
- camera lens feel
- line/detail density
- costume motifs
- faction symbols
- rendering finish

When prompting multiple related assets, include a continuity block that repeats the same shared rules.

### Batch Types

Use distinct batch definitions:

- character exploration batch: 4-8 silhouette and costume directions
- final character sheet batch: front, back, side, three-quarter, expression, gear callouts
- environment mood batch: 3-6 lighting and composition directions
- prop sheet batch: 6-12 related items under one faction/style language
- UI exploration batch: HUD framing, panel language, icon tone, hierarchy experiments
- keyframe batch: one gameplay moment shown in escalating fidelity

### Production Conversion

Treat Nano Banana output as one of these:

- inspiration only
- concept approval target
- paintover base
- modeling or illustration guide
- UI layout direction

Do not treat raw generations as final in-game assets unless the user explicitly wants that and the technical/art pipeline supports it.

### Game-Ready Handoff

After generating prompts or images, convert them into downstream artifacts:

- asset name
- purpose in game
- required variants
- animation implications
- implementation notes
- file naming convention
- resolution or aspect needs

### Common Failures

- beautiful image with no gameplay readability
- character art inconsistent across prompts
- concept art too detailed for team capacity
- no distinction between marketing art and in-game asset reference
- asking for sprite-ready output without defining camera, pose, and state list

### Recommended Response Shape

When the user asks for Nano Banana image support, answer with:

1. asset goal
2. style anchor
3. batch plan
4. prompt pack
5. continuity rules
6. downstream production notes

### Prompt Templates

Use these templates as starting points. Replace bracketed fields with project-specific values and keep the continuity block stable across related generations.

#### Character Concept Template

Use for first-pass hero, NPC, or enemy exploration.

```text
Create a high-quality game character concept for [game name], a [genre] game on [platform].
Subject: [character name or type], [age or vibe], [combat/class role].
Gameplay role: [player character / elite enemy / merchant NPC / boss].
Readability goal: readable at [camera distance or framing], clear silhouette, strong faction identity.
Silhouette: [shape language], [height/build], [signature gear].
Costume and materials: [fabric/armor/material language], [damage level], [ornament logic].
Mood: [emotion], [narrative signal], [energy level].
Style: [stylized realism / painterly fantasy / cel-shaded sci-fi / etc.], production-ready concept art, clean shape design, cohesive rendering.
Composition: full body character presentation, neutral backdrop, clear pose, high detail on face, costume, and gear.
Continuity rules: [palette logic], [faction motifs], [material language], [detail density], [rendering finish].
Exclude: cluttered background, extra limbs, duplicated accessories, unreadable hands, text, watermark, cinematic blur.
```

#### Character Sheet Template

Use when the team needs a stable reference sheet after direction is chosen.

```text
Create a production-ready character sheet for [character name] from [game name].
Show front view, back view, side view, three-quarter view, and one expressive action pose.
Character role: [role].
Art style: [style].
Silhouette and proportion: [rules].
Costume breakdown: [key layers and props].
Material language: [materials].
Gameplay readability: prioritize recognizable shape and gear at [camera distance].
Continuity rules: [palette logic], [faction iconography], [rendering finish], [line/detail density].
Background: clean neutral backdrop for reference use.
Exclude: scene composition, heavy perspective distortion, decorative background elements, text labels, watermark.
```

#### Environment Mood Template

Use for scene direction, biome testing, level mood, or key location exploration.

```text
Create a high-quality environment concept for [game name].
Scene type: [hub / combat arena / dungeon corridor / boss room / town street / forest path].
Gameplay purpose: [exploration / navigation clarity / combat readability / story reveal].
Camera: [top-down / side view / third-person / isometric / wide cinematic establishing shot].
World tone: [tone].
Lighting: [time of day], [contrast level], [atmosphere].
Landmarks: [3-5 must-read landmarks].
Traversal readability: clear paths, gameplay-critical surfaces readable, strong foreground-midground-background separation.
Style: [style], production-quality concept art, coherent materials and architecture.
Continuity rules: [palette], [faction/biome motifs], [surface language], [fog/effects treatment].
Exclude: random props with no gameplay purpose, over-busy composition, unreadable pathways, text, watermark.
```

#### UI And HUD Template

Use for menu direction, in-game HUD exploration, or panel language studies.

```text
Create a high-quality game UI concept for [game name], a [genre] game.
UI target: [main HUD / inventory / equipment screen / shop / map / pause menu].
Platform: [PC / mobile / console].
Interaction style: [mouse-heavy / controller-first / touch-first].
Visual tone: [clean tactical / ornate fantasy / brutal industrial / etc.].
Hierarchy requirements: emphasize [health/ammo/cooldowns/objective/minimap/dialogue].
Layout goal: readable within [camera/gameplay context], strong contrast, low clutter, clear information grouping.
Style: polished game UI mockup, production-quality, aligned with [art direction].
Continuity rules: [shape language], [border treatment], [icon style], [color system], [panel material cues].
Exclude: lorem ipsum paragraphs, fake tiny unreadable text, browser chrome, watermark.
```

#### Prop Sheet Template

Use for weapon families, pickups, interactables, or faction-based object sets.

```text
Create a prop sheet for [game name].
Prop family: [weapons / healing items / shrine objects / sci-fi tools / crafting resources].
Gameplay purpose: [combat / economy / puzzle / worldbuilding / loot clarity].
Count: [number] related props with one shared visual language.
Style: [style].
Material language: [materials].
Readability: each prop must be distinguishable at [camera distance or icon size].
Continuity rules: [palette], [faction motifs], [surface wear], [detail density].
Composition: clean prop sheet presentation on a simple backdrop, consistent scale logic.
Exclude: unrelated props, decorative filler, scene background, watermark, text labels unless explicitly requested.
```

#### Key Art Or Marketing Frame Template

Use for store capsules, pitch decks, splash images, or announcement visuals.

```text
Create premium key art for [game name].
Focus: [main hero / hero vs boss / team lineup / signature world reveal].
Player fantasy: [fantasy].
Genre signal: [genre].
Composition: striking focal hierarchy, readable silhouettes, premium lighting, strong foreground and background separation.
Mood: [mood].
Style: highly polished promotional game art, cohesive with the game's visual identity.
Must include: [hero prop], [enemy motif], [world landmark], [FX type].
Continuity rules: [palette], [faction symbols], [rendering finish], [costume motifs].
Exclude: logo, text, watermark unless explicitly requested.
```

#### Multi-Image Continuity Block Template

Append this block to every prompt in a batch:

```text
Shared continuity for this batch:
- same game universe: [game name]
- same art direction: [style anchor]
- same palette logic: [palette rules]
- same material language: [material rules]
- same faction motifs: [motifs]
- same line/detail density: [detail rule]
- same rendering finish: [finish]
- preserve identity consistency across all images
```

### Batch Recipes

Use these recipe sequences instead of ad hoc generations.

#### Character Pipeline

1. Generate 4 silhouette directions.
2. Select 1-2 strongest directions.
3. Generate costume/material refinements for the selected direction.
4. Generate a locked character sheet.
5. Generate 2-3 gameplay key poses based on the locked sheet.

#### Environment Pipeline

1. Generate 3 biome or mood directions.
2. Lock one lighting and architecture direction.
3. Generate a gameplay-readable exploration frame.
4. Generate one combat-use frame for the same location language.

#### UI Pipeline

1. Generate 3 hierarchy/layout directions.
2. Lock one information architecture direction.
3. Generate a clean polished mockup.
4. Generate 1-2 state variants such as combat, inventory open, low health warning.

### Output Packaging

When returning prompts to the user, group them as:

- style anchor
- continuity block
- batch prompts
- negative constraints
- implementation notes

---

## Pencil MCP Integration

### When To Use Pencil

Use Pencil MCP for structured, interactive UI and layout work:

- Game HUD design and iteration
- Inventory, shop, and menu screen layouts
- Component libraries (health bars, buttons, card frames, inventory slots)
- Wireframing before visual polish
- Production-ready UI mockups with precise layout control
- Landing pages and promotional layouts

### Pencil Workflow For Game UI

1. **Setup**: `get_editor_state()` → Understand current file state
2. **Guidelines**: `get_guidelines(topic=tailwind)` or `get_guidelines(topic=table)` → Load design rules
3. **Style**: `get_style_guide_tags()` → Find relevant style guides, then `get_style_guide(tags)` for inspiration
4. **Discover**: `batch_get(patterns)` → Search for existing components to reuse
5. **Design**: `batch_design(operations)` → Build UI with Insert, Update, Copy operations
6. **Validate**: `get_screenshot()` → Visually verify the output
7. **Iterate**: Repeat steps 5-6 until the design meets requirements

### Pencil Design Operations For Games

**Building a Health Bar**
```
// Create health bar container
bar=I("parent_frame", { w: 200, h: 24, fill: "#333333", corner: 4 })
// Create health fill
fill=I(bar, { w: 180, h: 20, x: 2, y: 2, fill: "#ff3333", corner: 2 })
// Create health text
text=I(bar, { text: "HP: 80/100", fontSize: 12, fill: "#ffffff", x: 10, y: 4 })
```

**Building an Inventory Grid**
```
// Create inventory container
inv=I("parent", { w: 320, h: 400, fill: "#1a1a2e", corner: 8, padding: 8 })
// Create grid of slots (repeat pattern)
slot1=I(inv, { w: 64, h: 64, fill: "#2a2a4e", corner: 4, stroke: "#4a4a6e" })
// Add item icon using G() for AI generation
G(slot1, "ai", "game inventory icon, potion bottle, pixel art style, transparent background")
```

**Using G() For AI-Generated Images In Pencil**
The `G()` operation generates AI images directly within Pencil designs:
```
G("target_node_id", "ai", "description of the image to generate")
```

Use G() for:
- Icon generation within UI layouts
- Background illustrations for panels
- Placeholder art that matches the style direction
- Texture fills and decorative elements

### Reusable Game UI Components

Build these as Pencil components for reuse across screens:

| Component | Structure | States to Design |
|-----------|----------|------------------|
| Health bar | Container + fill + text overlay | Full, 75%, 50%, 25%, critical, empty |
| Mana/energy bar | Container + fill + icon | Full through empty |
| Inventory slot | Border frame + item icon + quantity badge | Empty, filled, selected, locked |
| Ability button | Circle/square + icon + cooldown overlay | Ready, cooldown, disabled, pressed |
| Card frame | Border + illustration area + text area + cost badge | In hand, played, highlighted |
| Dialog box | Background panel + portrait + text area + continue indicator | Text appearing, choice mode |
| Toast notification | Slide-in panel + icon + text | Appearing, visible, dismissing |
| Tab button | Background + label | Active, inactive, disabled |

---

## Midjourney Integration

### When To Use Midjourney

Use Midjourney when you need:

- Photo-realistic environment reference (real architecture, landscapes, interiors)
- Material and texture studies (metal, wood, fabric, stone close-ups)
- Realistic lighting reference for art direction
- Architectural reference for level design
- Photo-realistic character reference for stylized adaptation
- Nature and biome reference (forests, deserts, oceans, caves)

### Prompt Structure Translation

Convert the Nano Banana layered format to Midjourney syntax:

**Nano Banana layered format:**
```
Subject: dark elf rogue, lithe build, dual daggers
Gameplay role: assassin class, PvP-focused
Silhouette: angular, crouching stance, hooded
Materials: dark leather, obsidian blades, shadow wisps
Mood: dangerous, calculating
Style: stylized realism
```

**Midjourney translation:**
```
dark elf rogue assassin, lithe crouching stance, dual obsidian daggers,
dark leather armor with hood, shadow wisps, dangerous calculating expression,
stylized realism, game character concept art, clean neutral background
--ar 3:4 --v 6 --style raw
```

### Midjourney-Specific Parameters

| Parameter | Usage | Common Values |
|-----------|-------|---------------|
| `--ar` | Aspect ratio | `1:1` (icons), `3:4` (character), `16:9` (environment), `4:3` (UI) |
| `--v` | Model version | `6` (latest), `5.2` (stable) |
| `--style` | Style intensity | `raw` (less stylized), default (more stylized) |
| `--s` | Stylize value | `0-1000`, lower = more literal, higher = more artistic |
| `--sref` | Style reference | URL of reference image for style matching |
| `--cref` | Character reference | URL of character image for consistency |
| `--no` | Negative prompt | `--no text, watermark, blurry` |
| `--q` | Quality | `1` (default), `2` (higher detail, slower) |

### Midjourney Prompt Templates

**Material Study**
```
close-up macro photograph of [material], showing surface texture and light interaction,
[lighting condition], studio lighting, 8k detail, material reference sheet
--ar 1:1 --v 6 --style raw
```

**Architecture Reference**
```
[architectural style] building exterior/interior, [time period], [condition: pristine/ruined/weathered],
[lighting], cinematic photography, architectural reference
--ar 16:9 --v 6 --style raw
```

**Nature/Biome Reference**
```
[biome type] landscape, [time of day], [weather], [season],
[specific features: ancient trees, crystal formations, volcanic vents],
cinematic landscape photography, environment reference
--ar 16:9 --v 6 --s 250
```

---

## Art Tool Selection Quick Reference

When the user requests art generation, use this matrix:

| User Request | Primary Tool | Secondary Tool | Workflow |
|-------------|-------------|---------------|----------|
| "Design my main character" | Nano Banana | — | Character pipeline recipe |
| "Make an RPG inventory UI" | Pencil | Nano Banana (style) | UI pipeline with Pencil |
| "Show me what the forest level looks like" | Nano Banana | Midjourney (reference) | Environment pipeline |
| "I need realistic material reference" | Midjourney | — | Material study template |
| "Design the HUD for my shooter" | Pencil | Nano Banana (style exploration) | Pencil HUD workflow |
| "Make key art for my store page" | Nano Banana | — | Key art template |
| "Create card frames for my card game" | Pencil | Nano Banana (illustration) | Pencil components + NB art |
| "What should my game's UI style look like?" | Nano Banana | Pencil (wireframe first) | Style exploration → production |
| "Generate game icons" | Nano Banana or Pencil G() | — | Batch icon generation |
| "Architecture reference for my fantasy city" | Midjourney | Nano Banana (stylize) | Reference → concept |

---

## Fallback Strategy (When Tools Are Unavailable)

Not all tools will always be available. When a tool is missing, degrade to text-based output that the user or their team can execute manually with any tool.

### Fallback Rules

1. **Attempt the primary tool first.** If it fails or is not configured, do NOT re-ask — switch to fallback immediately.
2. **Fallback output must be production-usable**, not a vague description. Include all the same structure (layers, continuity rules, negative constraints) as if the tool were present.
3. **Label the fallback clearly**: "Tool [X] is unavailable — outputting as [prompt pack / UI spec / reference brief] instead."

### Fallback Output By Tool

| Unavailable Tool | Fallback Output |
|-----------------|----------------|
| Nano Banana | Full prompt pack in the layered template format (identity, role, silhouette, materials, mood, camera, style, exclusions, continuity block). Usable in any image generator. |
| Pencil MCP | Structured UI specification as text: screen name, layout zones, component list with dimensions, interaction states, color tokens, hierarchy notes. Ready for any design tool. |
| Midjourney | Detailed reference brief: subject, material properties, lighting conditions, camera angle, composition notes, and suggested search terms for stock reference. |
| All tools unavailable | Output complete art direction documents: style bible text, asset spec sheets, prompt packs, and UI wireframe specifications — the production team executes manually. |
