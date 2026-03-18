# QA And Testing

## Goal

Define testing strategies, playtest methodologies, bug management systems, and quality validation processes that ensure the game ships in a polished, balanced, and functional state. This module produces test plans, bug templates, playtest protocols, and quality checklists — not test code or automation scripts.

## When To Use

- After initial playable build exists (graybox or vertical slice stage)
- Throughout production: testing is continuous, not a final phase
- When the user asks about "testing", "QA", "bugs", "playtest", or "quality"
- When diagnosing why something "doesn't feel right" (systematic testing approach)

---

## Testing Matrix

### Test Categories

| Category | What It Tests | When To Run | Who Runs It |
|----------|-------------|-------------|-------------|
| Functional | Does the feature work as designed? | Every build | QA or developer |
| Balance | Are numbers and difficulty appropriate? | After balance pass | Designer + playtesters |
| Experience / Feel | Is it fun, clear, and satisfying? | Milestone builds | Playtesters (external preferred) |
| Performance | FPS, memory, load times, battery | Weekly + milestone | Technical QA |
| Compatibility | Platform, device, input method, resolution | Pre-launch | QA matrix testing |
| Regression | Did new changes break existing features? | Every build | Automated + QA |
| Localization | Text fits, translations correct, no broken strings | After loc integration | Loc QA |
| Accessibility | Can players with disabilities use the game? | Milestone builds | Accessibility testers |

### Test Coverage Matrix

Track test coverage per feature:

| Feature | Functional | Balance | Feel | Performance | Regression | Status |
|---------|-----------|---------|------|-------------|-----------|--------|
| Player movement | Pass | N/A | Pass | Pass | Pass | Green |
| Combat system | Pass | In Progress | Needs Test | Pass | Pass | Yellow |
| Inventory | Pass | N/A | Needs Test | Not Tested | Pass | Yellow |
| Boss encounter | Not Tested | Not Tested | Not Tested | Not Tested | N/A | Red |

---

## Playtest Methodology

### Four Playtest Types

**1. Smoke Test (Developer Playtest)**
- Who: Development team member
- Duration: 5-15 minutes
- Goal: Verify basic functionality, catch crashes and blockers
- When: Every build, before sharing with others
- Output: Blocker list

**2. Directed Playtest**
- Who: Team member or trusted tester with specific instructions
- Duration: 15-45 minutes
- Goal: Test specific feature, flow, or balance scenario
- When: After feature implementation, after balance changes
- Output: Feature-specific feedback form

**3. Open Playtest**
- Who: External testers (target audience) with no instructions beyond "play the game"
- Duration: 30-90 minutes
- Goal: Discover UX issues, unclear mechanics, emotional responses, natural behavior patterns
- When: Milestone builds (graybox, vertical slice, beta)
- Output: Session recording/notes, post-session survey

**4. Competitive/Stress Playtest**
- Who: Skilled players or QA focused on edge cases
- Duration: 60+ minutes
- Goal: Find exploits, imbalances, degenerate strategies, performance limits
- When: After balance pass, before launch
- Output: Exploit log, balance recommendations

### Playtest Session Design

**Pre-Session**
- Define the test goal (what question are you answering?)
- Prepare the build (stable, no known blockers on critical path)
- Set up recording (screen + audio, or observation notes)
- Prepare the pre-session briefing (minimal — avoid biasing the tester)

**During Session**
- Do NOT help unless the player is completely stuck for 3+ minutes
- Observe: where do they look? What do they try? Where do they hesitate?
- Note moments of confusion, frustration, delight, and surprise
- Track time spent per section/activity

**Post-Session**
- Ask open-ended questions first: "What stood out to you?" "What was frustrating?"
- Then ask specific questions about tested features
- Collect survey data (5-point scale for key metrics)

### Key Observation Metrics

| Metric | What To Watch | Red Flag |
|--------|-------------|----------|
| Time to first success | How long before the player achieves something | >5 minutes with no positive feedback |
| Confusion points | Where does the player stop and look around | Same spot confuses 3+ testers |
| Death/failure frequency | Where and how often players fail | Same spot kills 80%+ of testers |
| Feature discovery rate | % of testers who find optional content | <20% find a feature you intended as common |
| Session length | How long before the player stops voluntarily | <50% of intended session length |
| Emotional peaks | Moments of visible excitement or frustration | No visible positive reaction in first 10 minutes |
| Menu/UI time | Time spent in menus vs. gameplay | >40% in menus (unless menu-heavy genre) |

---

## Bug Management

### Bug Severity System

| Severity | Definition | Response Time | Examples |
|----------|-----------|---------------|--------|
| S1 — Critical | Game is unplayable, data loss, crash | Fix immediately, block release | Crash on launch, save corruption, soft lock |
| S2 — Major | Feature broken, significant negative impact | Fix before next milestone | Combat doesn't deal damage, quest can't complete |
| S3 — Minor | Feature partially broken, workaround exists | Fix before launch | UI element misaligned, audio plays wrong clip |
| S4 — Cosmetic | Visual/audio polish issue, no gameplay impact | Fix if time allows | Minor texture seam, subtitle timing off |

### Bug Report Template

```
BUG ID: [auto-assigned]
TITLE: [Short descriptive title — verb + object + problem]
SEVERITY: [S1 / S2 / S3 / S4]
CATEGORY: [Gameplay / UI / Audio / Visual / Performance / Localization]
PLATFORM: [PC / Mobile / Console / All]
BUILD: [Build number or date]

STEPS TO REPRODUCE:
1. [Step 1]
2. [Step 2]
3. [Step 3]

EXPECTED RESULT: [What should happen]
ACTUAL RESULT: [What actually happens]
FREQUENCY: [Always / Often (>50%) / Sometimes (10-50%) / Rare (<10%)]

ATTACHMENTS: [Screenshot / Video / Save file / Crash log]

NOTES: [Additional context, workaround if known]
```

### Bug Triage Process

Weekly (or per-build) triage meeting:

1. Review all new bugs
2. Assign severity (confirm or adjust reporter's assessment)
3. Assign owner (who will fix it?)
4. Set target milestone (when should it be fixed?)
5. Identify duplicates and related bugs
6. Re-assess deferred bugs: still valid? Priority changed?

### Triage Decision Framework

```
Is it S1?
  → Yes: Fix now, delay other work
  → No: Continue

Is it on the critical path?
  → Yes: Fix before next playtest
  → No: Continue

Does it affect >30% of players?
  → Yes: Fix before launch
  → No: Continue

Is it quick to fix (<1 hour)?
  → Yes: Fix in current sprint
  → No: Schedule for future sprint or post-launch
```

---

## Balance Testing

### Spreadsheet Simulation

Before implementing in-game, validate balance in spreadsheets:

1. Model player power curve across levels (see [balance-economy.md](balance-economy.md))
2. Simulate 100 encounters at each difficulty tier
3. Track: win rate, average TTK, resource consumption, health remaining
4. Target: 85-95% win rate for common encounters, 50-70% first-attempt boss clear

### In-Game Balance Validation

After spreadsheet validation, test in the actual game:

| Test | Method | Target |
|------|--------|--------|
| Common enemy TTK | Time 10 encounters per enemy type | Within 20% of design target |
| Boss clear rate | 10+ playtest attempts per boss | 50-70% first-attempt clear for Normal |
| Economy validation | Play 1 hour, track income vs. spending | Player can afford 1 upgrade per ~15 min |
| Build diversity | 5+ testers build independently | 3+ distinct viable approaches |
| Difficulty spike detection | Track death heatmap | No single point with >3x average death rate |

### Stress Test Scenarios

| Scenario | What To Test | Red Flag |
|----------|-------------|----------|
| Maximum entities | Spawn max enemies + projectiles + effects | FPS drops below 30 |
| Maximum inventory | Fill all inventory slots | UI breaks or performance degrades |
| Extended session | Play for 4+ hours continuously | Memory leak, save corruption |
| Rapid state changes | Open/close menus rapidly, spam inputs | Soft lock, state corruption |
| Edge case values | 0 HP, max currency, negative stats | Crash or undefined behavior |
| Save/load cycle | Save, load, verify all state preserved | Lost progress, broken references |

---

## Automated Testing Strategy

### What To Automate

| Test Type | Automation Value | Method |
|-----------|-----------------|--------|
| Smoke test (does it launch?) | Very High | CI/CD build verification |
| Save/load integrity | High | Automated save-load-compare cycle |
| Performance benchmarks | High | Automated scene profiling |
| UI navigation flow | Medium | Input sequence scripting |
| Balance regression | Medium | Automated simulation with fixed seed |
| Gameplay feel | Not automatable | Human playtest only |
| Fun | Not automatable | Human playtest only |

### Test Checklist Before Milestone

- [ ] All S1 and S2 bugs resolved
- [ ] Core loop playable start to finish without crashes
- [ ] Save/load verified on all target platforms
- [ ] Performance within target on minimum spec
- [ ] All new features have been playtested at least once
- [ ] Balance spreadsheet matches in-game behavior within 20% margin
- [ ] Accessibility baseline features functional
- [ ] Audio plays correctly (no missing clips, no stuck loops)
- [ ] UI functional on all target resolutions
- [ ] No placeholder content visible to players
