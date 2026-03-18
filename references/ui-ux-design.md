# UI/UX Design

## Goal

Design the information architecture, interaction logic, screen flows, and interface systems of the game. This module covers UX structure and UI specification — not just visual styling, but how information is organized, how the player interacts, and how UI serves gameplay clarity. Integrates with art tools (Pencil for wireframes and production UI, Nano Banana for style exploration, Midjourney for reference gathering).

## When To Use

- After core loop and key systems are defined (see [genre-templates.md](genre-templates.md))
- After creative direction sets visual tone (see [creative-direction.md](creative-direction.md))
- Before art production: UI design drives asset requirements for panels, icons, fonts
- When the user asks about "HUD", "menus", "interface", "information architecture", or "screen flow"

---

## Information Architecture

### HUD Information Audit

List every piece of information the player needs during gameplay:

| Information | Type | Urgency | Frequency | Display Method |
|-------------|------|---------|-----------|---------------|
| Player health | Numeric + bar | Always visible | Constant | HUD bar |
| Mana/energy | Numeric + bar | Always visible | Constant | HUD bar |
| Minimap | Spatial | Frequently needed | Constant or toggle | HUD corner |
| Objective | Text | Periodically needed | Update on change | HUD banner or compass |
| Ammo/resource count | Numeric | During combat | Constant | Near crosshair/weapon |
| Cooldowns | Timer + icon | During combat | Per ability | Ability bar |
| Status effects | Icon | While active | Duration-based | Near health bar |
| Currency | Numeric | In menus | On change + menu | HUD corner or menu only |
| Score/combo | Numeric | During action | On event | Center/top |
| Notifications | Text/icon | On event | Temporary | Toast or banner |

### Information Priority Matrix

Rank information by urgency for screen real estate allocation:

| Priority | Category | Rule |
|----------|----------|------|
| P0 — Survival | Health, imminent threats | Always visible, largest display |
| P1 — Action | Current abilities, ammo, cooldowns | Visible during gameplay, quick-glance |
| P2 — Context | Objective, minimap, compass | Available, can be toggled |
| P3 — Progress | Score, XP, currency | Shown on events or in menus |
| P4 — Meta | Settings, social, achievements | Menu-only access |

### Cognitive Load Management

- **7±2 rule**: No more than 5-9 distinct information elements visible at once during gameplay
- **Progressive disclosure**: Show information when relevant, hide when not
- **Grouping**: Related information clustered spatially (health + status near each other)
- **Consistency**: Same information always in the same position across all screens
- **Reduce, don't remove**: Minimize information display, but never remove critical data

---

## Screen Flow Design

### Full Screen Map

Document every screen in the game and transitions between them:

```
[Splash] → [Main Menu]
                ├→ [New Game] → [Character Select] → [Gameplay HUD]
                ├→ [Continue] → [Save Select] → [Gameplay HUD]
                ├→ [Settings] → [Settings Subpages]
                ├→ [Gallery/Codex]
                └→ [Credits]

[Gameplay HUD]
    ├→ [Pause Menu]
    │       ├→ [Settings]
    │       ├→ [Save/Load]
    │       └→ [Return to Main Menu]
    ├→ [Inventory]
    │       ├→ [Equipment]
    │       ├→ [Items]
    │       └→ [Crafting]
    ├→ [Map]
    ├→ [Quest Log]
    ├→ [Character Status]
    ├→ [Shop] (when at vendor)
    └→ [Dialogue] (when in conversation)
```

### Screen Inventory Table

| Screen ID | Screen Name | Access Method | Contains | Exit Method |
|-----------|------------|---------------|----------|-------------|
| SCR-01 | Main Menu | Game launch | New Game, Continue, Settings, Credits | Quit game |
| SCR-02 | Gameplay HUD | Start/continue game | HP, mana, minimap, abilities, objective | Pause menu |
| SCR-03 | Inventory | Hotkey (I) or menu | Equipment, items, stats, crafting | Close (Esc/B) |
| SCR-04 | Pause Menu | Esc/Start | Resume, settings, save, quit | Resume |
| ... | ... | ... | ... | ... |

---

## Interaction State Matrix

Every interactive UI element must define its states:

| State | Visual Change | Audio | Behavior |
|-------|-------------|-------|----------|
| Default | Base appearance | None | Idle |
| Hover / Focus | Highlight, scale up 2-5% or outline | Subtle hover SFX | Show tooltip if applicable |
| Pressed | Depress visual, darken slightly | Click SFX | Trigger action |
| Disabled | Greyed out, reduced opacity | Error SFX on attempt | Block interaction, show reason |
| Loading | Spinner or progress indicator | None | Block interaction |
| Error | Red highlight or shake | Error SFX | Show error message |
| Success | Green flash or check mark | Confirm SFX | Brief feedback, then return to default |
| Selected (toggle) | Highlighted border or filled state | Select SFX | Persistent until deselected |

### State Documentation Per Element

For complex UI elements, document all states:

```
ELEMENT: [Buy Button]
SCREEN: [Shop Screen]
DEFAULT: Gold button with item price, enabled when player has enough currency
HOVER: Slight glow, price text enlarges
PRESSED: Button depresses, coin deduction animation
DISABLED: Greyed out when insufficient funds, tooltip shows "Not enough gold"
LOADING: N/A (instant transaction)
SUCCESS: Green flash, "+1 [item]" floating text
ERROR: Red shake if inventory full, "Inventory full" toast
```

---

## Platform Adaptation

### Input Method Differences

| Feature | Mouse + Keyboard | Gamepad / Controller | Touchscreen |
|---------|-----------------|---------------------|-------------|
| Navigation | Direct pointer, hover states | D-pad/stick focus navigation | Tap targets |
| Selection | Click | A/X button | Tap |
| Cancel/Back | Esc or right-click | B/Circle button | Back gesture or button |
| Tooltips | Hover-triggered | Hold button or focus-triggered | Long press |
| Drag and drop | Native mouse drag | Hold + stick movement | Touch drag |
| Scrolling | Scroll wheel + scrollbar | Stick/bumper scroll | Swipe |
| Min hit target | 24x24px | 48x48px equivalent | 44x44pt (Apple), 48x48dp (Android) |
| Text input | Keyboard direct | Virtual keyboard or preset options | Virtual keyboard |

### Platform-Specific Rules

**PC**
- Support both mouse and keyboard; show rebindable keys
- Hover states for all interactive elements
- High information density acceptable (larger screens)
- Scrollbars and right-click context menus expected

**Console**
- Focus-based navigation (no hover, use selection highlight)
- All actions mappable to controller buttons
- Larger text (minimum 24px at 1080p, visible from couch distance)
- Bumper/trigger for tab switching
- Consistent button prompts (platform-specific icons)

**Mobile**
- Touch targets minimum 44pt
- Avoid hover-dependent interactions
- Bottom-of-screen placement for thumb reach
- Swipe gestures for common actions
- Consider one-hand play mode for portrait games
- Battery and data usage considerations

---

## HUD Design Framework

### HUD Patterns By Genre

| Genre | Primary HUD Elements | HUD Style |
|-------|---------------------|----------|
| Action RPG | Health bar, mana, abilities, minimap, equipment | Persistent frame |
| FPS | Crosshair, ammo, health, grenade count | Minimal centered |
| Platformer | Lives, collectibles, score | Top bar, minimal |
| Strategy | Resources, minimap, selected unit, tech progress | Panels at edges |
| Card game | Hand display, mana, opponent info, deck/discard | Table layout |
| Puzzle | Move count, timer (optional), hint button | Minimal top bar |
| Survival | Health, hunger, thirst, temperature, inventory quick-access | Status bar cluster |
| Racing | Speed, position, lap, minimap | Dashboard-style |

### HUD Layout Zones

```
┌────────────────────────────────────────┐
│ [Top-Left]          [Top-Center]   [Top-Right]     │
│ Player status       Objective      Minimap/Score    │
│                                                     │
│                                                     │
│ [Mid-Left]         [CENTER]        [Mid-Right]     │
│ Alerts          Crosshair/Focus    Context prompts  │
│                                                     │
│                                                     │
│ [Bot-Left]         [Bot-Center]    [Bot-Right]     │
│ Abilities/Items   Dialogue/Status  Resource counts  │
└────────────────────────────────────────┘
```

- **Top-Left**: Player status (health, mana, portrait) — eyes naturally scan here
- **Top-Right**: Map, score, or objective — secondary glance zone
- **Bottom-Center**: Ability bar, hotbar, or dialogue — near natural hand position for controllers
- **Center**: Reserved for gameplay — never place persistent UI here; only transient elements (crosshair, damage numbers, interaction prompts)

---

## Menu System Design

### Settings Page Checklist

| Category | Settings |
|----------|----------|
| Video | Resolution, fullscreen/windowed, VSync, brightness, FPS limit, quality preset |
| Audio | Master volume, music volume, SFX volume, voice volume, audio output device |
| Controls | Key/button rebinding, sensitivity, invert axes, vibration toggle |
| Gameplay | Difficulty, language, subtitles, colorblind mode, HUD scale |
| Accessibility | Text size, screen reader support, reduced motion, auto-aim assist, one-hand mode |

### Accessibility Requirements

Minimum accessibility features for any modern game:

- [ ] Remappable controls (all inputs)
- [ ] Subtitle support with size and background options
- [ ] Colorblind mode (protanopia, deuteranopia, tritanopia)
- [ ] UI scale slider (75%-200%)
- [ ] Screen shake intensity slider (0-100%)
- [ ] Audio cue alternatives for visual-only information
- [ ] Hold vs. toggle options for sustained inputs
- [ ] Font legibility (avoid thin or decorative fonts for body text)

---

## Art Tool Integration Workflow

### UI Design Pipeline

```
Phase 1: Information Architecture → Paper/text wireframes (no tools needed)
Phase 2: Wireframing → Pencil MCP (low-fidelity, fast layout iteration)
Phase 3: Style Exploration → Nano Banana (mood and aesthetic direction)
Phase 4: Production UI → Pencil MCP (high-fidelity, component-based)
Phase 5: Style Reference → Midjourney (for specific visual reference if needed)
```

### When To Use Each Tool

| Task | Tool | Why |
|------|------|-----|
| Layout and spacing | Pencil | Structural, grid-based, interactive |
| Component library (buttons, panels, bars) | Pencil | Reusable design components |
| Visual mood exploration | Nano Banana | High-fidelity concept art |
| Icon design exploration | Nano Banana or Midjourney | Visual reference generation |
| Full screen mockup | Pencil | Production-quality, layer control |
| Style bible visual | Nano Banana | Establishing aesthetic direction |
| Photo-realistic UI reference | Midjourney | When needing real-world material reference |

### Pencil UI Workflow

1. `get_editor_state` → Check current file
2. `get_guidelines(topic=table)` or `get_guidelines(topic=tailwind)` → Load UI design rules
3. `batch_get` → Examine existing components for reuse
4. `batch_design` → Build UI structure:
   - Layout frames with auto-layout
   - Text elements with proper hierarchy
   - Interactive components with state variants
   - Color tokens from the style system
5. `get_screenshot` → Validate visual output
6. Iterate with `batch_design` updates

### Common UI Components for Games

Build these as reusable Pencil components:

| Component | Usage | States |
|-----------|-------|--------|
| Health bar | Player/enemy HP display | Full, partial, low, critical, dead |
| Resource counter | Currency, ammo, items | Has amount, zero, gaining, spending |
| Ability button | Skill/spell activation | Ready, cooldown, disabled, pressed |
| Inventory slot | Item grid cell | Empty, filled, selected, locked |
| Card frame | Card game card display | In-hand, played, highlighted, exhausted |
| Tooltip | Contextual information | Appearing, visible, dismissing |
| Dialog box | NPC/story dialogue | Text advancing, choice presented, complete |
| Notification toast | Alerts and feedback | Appearing, visible, dismissing |
| Progress bar | XP, loading, crafting | Empty, filling, complete |
| Tab bar | Screen section navigation | Active tab, inactive tabs, disabled |
