# Collaboration

## Goal

Turn design intent into handoff-ready work for multiple disciplines.

## Task Writing Standard

Each task should include:

- objective
- player-facing result
- files or systems touched
- dependencies
- acceptance criteria
- test method
- fallback cut if blocked

## Handoff Rule

Do not hand off a task like "make combat feel good". Rewrite it into executable work such as:

- implement hit-stop on confirmed melee impact
- add 3-frame anticipation on heavy attack
- expose attack cancel window in config
- create slash VFX variant for fire weapon family

## Review Loop

Run lightweight reviews at three levels:

1. strategy review: is the feature still serving the thesis
2. integration review: do design, code, and assets still fit together
3. production review: is the cost still justified by player impact

### Extended Review Types

**Balance Review**
- Are the numbers producing the intended difficulty/economy behavior?
- Do spreadsheet simulations match in-game feel?
- See [balance-economy.md](balance-economy.md) for validation framework
- Participants: designer + QA tester with balance focus

**Creative Review**
- Does the asset pass the style bible consistency test?
- See [creative-direction.md](creative-direction.md) for creative review checklist
- Participants: art lead + creative director (or equivalent role)

**UX Review**
- Is the information hierarchy correct for this screen?
- Do all interaction states work on all target platforms?
- See [ui-ux-design.md](ui-ux-design.md) for interaction state matrix
- Participants: designer + at least one person unfamiliar with the feature

**Audio Review**
- Do SFX match the game events and emotional targets?
- Are music transitions smooth and state-appropriate?
- See [audio-design.md](audio-design.md) for audio trigger design
- Participants: audio designer + game designer

**QA Review**
- Have all test categories been covered for this feature?
- Are there outstanding bugs at S1 or S2 severity?
- See [qa-testing.md](qa-testing.md) for test coverage matrix
- Participants: QA lead + feature owner

### Cross-Module Review Checklist

Before any milestone delivery, verify across all modules:

- [ ] **Strategy**: Feature still aligns with game thesis and product pillars
- [ ] **Balance**: Numbers validated in spreadsheet and in-game
- [ ] **Creative**: Assets pass style bible consistency (silhouette, color, material, tone)
- [ ] **Level Design**: Pacing curve follows design intent, encounters tested
- [ ] **Audio**: All gameplay events have appropriate SFX, BGM transitions work
- [ ] **UI/UX**: All screens functional, all states defined, platform-appropriate
- [ ] **Implementation**: Data contracts respected, no broken references
- [ ] **QA**: No S1/S2 bugs, test coverage adequate

## Module-Specific Handoff Templates

### Design → Engineering Handoff

```
FEATURE: [Name]
DESIGN DOC: [Link/reference]
CONFIG SCHEMA: [Reference to implementation.md schema]
ACCEPTANCE CRITERIA:
  - [Testable criterion 1]
  - [Testable criterion 2]
DATA TABLES NEEDED: [List of config files to create]
INTEGRATION POINTS: [Which existing systems this touches]
DEBUG NEEDS: [Cheats, visualizers, or tools needed for testing]
```

### Design → Art Handoff

```
FEATURE: [Name]
ASSETS NEEDED: [List with purpose]
STYLE REFERENCE: [Link to style bible section or mood board]
CAMERA DISTANCE: [How far the camera is from this asset]
ANIMATION STATES: [If animated, list all states]
VFX: [List VFX with triggers]
TOOL: [Pencil / Nano Banana / Midjourney / Manual]
DEADLINE: [Date]
REVIEW PROCESS: [Who reviews, what criteria]
```

### Design → Audio Handoff

```
FEATURE: [Name]
AUDIO EVENTS: [List of gameplay events needing sound]
MOOD/TONE: [Reference to creative direction]
PRIORITY: [Critical / Important / Polish]
SPATIAL: [2D / 3D / Hybrid for each event]
ADAPTIVE BEHAVIOR: [State-driven changes if any]
REFERENCE TRACKS: [Existing sounds to match tone]
```

### Art → Engineering Handoff

```
ASSET: [Name]
FILES: [Filename, format, resolution]
PIVOT/ANCHOR: [Position]
ANIMATION DATA: [Frame count, FPS, state labels]
NAMING CONVENTION: [Following project standard]
ATLAS/SHEET: [Which atlas this belongs to]
INTEGRATION NOTES: [Sorting order, render layer, special behavior]
```

## Stakeholder Communication Templates

### Weekly Status Update

```
WEEK: [Date range]
MILESTONE: [Current milestone name]
PROGRESS: [X% complete]

COMPLETED THIS WEEK:
- [Item 1]
- [Item 2]

IN PROGRESS:
- [Item 1] — [% complete, ETA]
- [Item 2] — [% complete, ETA]

BLOCKERS:
- [Blocker 1] — [Impact, proposed resolution]

NEXT WEEK GOALS:
- [Goal 1]
- [Goal 2]

RISKS:
- [Risk update if any]
```

### Milestone Review Presentation

```
MILESTONE: [Name]
DATE: [Review date]

GOALS:
- [Goal 1]: [Met / Partially Met / Not Met]
- [Goal 2]: [Met / Partially Met / Not Met]

DEMO: [What to show]

METRICS:
- Build stability: [crash rate]
- Feature completion: [X/Y features]
- Bug count: [S1: x, S2: x, S3: x, S4: x]
- Playtest feedback summary: [key findings]

SCOPE CHANGES:
- Added: [if any]
- Cut: [if any]
- Deferred: [if any]

NEXT MILESTONE PLAN:
- [Key goals]
- [Timeline]
- [Resource needs]
```

## Coordination Outputs

Useful artifacts include:

- discipline-specific task lists
- shared glossary
- naming convention sheet
- asset import checklist
- bug triage labels
- daily or weekly blocker summary
- cross-module review checklist
- handoff document per feature
- stakeholder status updates
