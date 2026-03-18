# Strategy

## Goal

Define a game worth building before expanding scope.

## Process

1. State the game in one sentence: `fantasy + action + tension + differentiator`.
2. Identify the target player and why they would choose this instead of adjacent games.
3. Define the core loop in 3-6 steps.
4. Define the emotional rhythm: what the player should feel each minute, each session, and after mastery.
5. Name the hard constraints: team size, timeline, engine, platform, monetization, live-ops or premium.
6. Remove mechanics that do not amplify the core loop or differentiation.

## Genre-Aware Strategy Framework

After step 1, load the matching genre template from [genre-templates.md](genre-templates.md). Use the genre's core loop, key systems, and risk list to calibrate the strategy. If the game is a hybrid, identify primary and secondary genres and follow the merge process.

Genre-specific questions:
- Does the core loop match the genre's expected rhythm? If not, is that intentional differentiation or an oversight?
- Which of the genre's key systems are in scope? Which are deliberately cut?
- What genre-specific risks apply, and how is each mitigated?

## Questions To Answer

- What is the player repeatedly doing?
- What skill or decision is the game testing?
- What makes the game legible in a screenshot, trailer, or first 60 seconds?
- What is the smallest version that still proves the fantasy?
- Which pillar is carrying the game: mastery, expression, progression, social play, narrative, or spectacle?

## Market Positioning

### Competitor Comparison Matrix

| Dimension | This Game | Competitor A | Competitor B | Competitor C |
|-----------|----------|-------------|-------------|-------------|
| Genre | | | | |
| Platform | | | | |
| Art style | | | | |
| Session length | | | | |
| Monetization | | | | |
| Core differentiation | | | | |
| Price point | | | | |
| Target audience overlap | | | | |

### Positioning Statement

Template: "For [target player] who wants [core fantasy], [game name] is a [genre] that [key differentiator], unlike [competitor] which [competitor weakness]."

## Pillar Validation Matrix

For each product pillar, verify it passes all criteria:

| Pillar | Player-Facing Value | Testable In Prototype | Scalable In Production | Team Can Execute | Differentiation |
|--------|-------------------|---------------------|----------------------|-----------------|----------------|
| Pillar 1 | [What player gets] | [How to test] | [Cost to scale] | [Skill match] | [Unique?] |
| Pillar 2 | | | | | |
| Pillar 3 | | | | | |

A pillar that fails any column should be reconsidered.

## Monetization Strategy

### Model Deep Dive

| Model | Description | Best For | Key Metrics | Risks |
|-------|-----------|----------|-------------|-------|
| Premium | One-time purchase | Story-driven, single-player, indie | Units sold, revenue, refund rate | Discovery, demo conversion |
| F2P Cosmetic | Free with cosmetic MTX | Multiplayer, social games | DAU, conversion rate, ARPDAU | Content creation cost, whale dependency |
| Gacha / Loot Box | Random reward MTX | Collection games, RPGs, mobile | Pull rate, pity conversion, ARPPU | Regulation risk, pay-to-win perception |
| Ad-Supported | Free with ad placements | Casual mobile, hypercasual | eCPM, ad frequency tolerance, retention | Player annoyance, revenue ceiling |
| Subscription | Recurring payment for access | Live-service, content-heavy | MRR, churn rate, content velocity | Content treadmill, churn |
| Hybrid | Combination of above | Most F2P games | Varies by component mix | Complexity, balance between revenue streams |

### Monetization Checklist

- [ ] Monetization does not conflict with core gameplay promise
- [ ] Free players have a complete core experience (if F2P)
- [ ] Paying players get value but not unfair advantage (in competitive games)
- [ ] Price points match target audience spending habits
- [ ] Revenue model is sustainable with planned content cadence
- [ ] Regulatory requirements met (loot box disclosure, age ratings)

## Success Metrics Framework

Define what success looks like before building:

| Metric | Target | Measurement Method | Review Frequency |
|--------|--------|-------------------|------------------|
| DAU | [target] | Analytics | Daily |
| D1 / D7 / D30 retention | [targets] | Cohort analysis | Weekly |
| ARPDAU (F2P) | [target] | Revenue / DAU | Weekly |
| Average session length | [target] | Analytics | Weekly |
| Sessions per day | [target] | Analytics | Weekly |
| Completion rate (premium) | [target] | Analytics | Monthly |
| Store rating | [target] | Store dashboard | Weekly |
| Organic install rate | [target] | Attribution | Monthly |

## Product Outputs

Produce concise artifacts such as:

- game thesis
- player promise
- 3 product pillars
- anti-pillars: what the game intentionally will not do
- differentiator list
- competitor comparison matrix
- monetization strategy document
- success metrics dashboard definition
- kill list of tempting but non-essential features

## Red Flags

- multiple unrelated core mechanics
- too many progression systems before the base loop is fun
- "open world", "multiplayer", or "UGC" added without production proof
- style references with no asset budget match
- relying on story or content quantity to hide a weak core loop
- no defined success metric beyond "make a good game"
- monetization strategy conflicts with player promise
- genre choice mismatches team expertise with no mitigation plan
