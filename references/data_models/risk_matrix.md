# Production Risk Matrix

When a user proposes a game feature, system, or scope expansion, you MUST evaluate it against this risk matrix before endorsing the idea. The orchestrator's job is not just to design — it is to protect the project from scope death.

For design methodology and balance frameworks, see [../balance-economy.md](../balance-economy.md).
For genre-specific production benchmarks, see [genre_benchmarks.md](genre_benchmarks.md).

## 1. Scope Risk Assessment

### Feature Cost Heuristics

| Feature Category | Typical Cost (person-weeks) | Risk Level | Warning Trigger |
|-----------------|---------------------------|-----------|----------------|
| New enemy type (full animation set) | 2-6 weeks | Medium | >8 enemy types for indie team |
| New playable character (full moveset) | 4-12 weeks | High | >2 characters for solo dev |
| New biome/zone (art + audio + encounters) | 3-8 weeks | High | >4 biomes for small team |
| Multiplayer netcode | 8-20+ weeks | Very High | Any team without prior netcode experience |
| Open world traversal | 12-30+ weeks | Very High | Any team <10 people |
| Procedural generation system | 4-12 weeks | High | Underestimating handcrafted content needed alongside ProcGen |
| Full voice acting | 2-8 weeks + recording budget | High | >50 voiced lines without dedicated audio budget |
| Branching narrative (>5 branches) | 4-16 weeks writing + implementation | High | Testing burden grows exponentially |
| Custom physics system | 6-16 weeks | Very High | When engine built-in physics would suffice |
| Save system (complex state) | 2-6 weeks | Medium | Underestimated for games with persistent worlds |

### Team Size Reality Check

| Team Size | Realistic Scope Ceiling | Common Failure |
|-----------|----------------------|----------------|
| Solo (1) | 1 core loop, 2-5 hours content, 1 biome, <10 enemy types | Trying to build a 20-hour RPG |
| Micro (2-5) | Focused game, 5-15 hours, 2-4 biomes, 15-25 enemy types | Adding multiplayer or open world |
| Small (5-15) | Full indie game, 15-40 hours, multiple biomes | Feature creep across too many systems |
| Medium (15-30) | AA scope, specialized roles, 40+ hours | Coordination overhead, pipeline bottlenecks |
| Large (30+) | AAA scope with proper management | Management overhead, vision alignment |

### Scope Escalation Warnings

When any of these triggers fire, the orchestrator MUST issue a warning:

| Trigger | Warning Message |
|---------|----------------|
| Feature count exceeds genre benchmark by >50% | "Scope exceeds typical [genre] indie benchmarks. Consider cutting [lowest-priority features] or extending timeline by [estimate]." |
| Animation count exceeds team capacity estimate | "Animation budget is [X] states × [Y] characters = [Z] total. At [team size], this requires [estimate] weeks of dedicated animation work." |
| User requests multiplayer for a team without netcode experience | "Multiplayer adds 3-6 months minimum and fundamentally changes architecture. Recommend: ship single-player first, add multiplayer in a post-launch update." |
| Content volume (hours) exceeds team-months available | "Producing [X] hours of content requires approximately [Y] person-months. Your team of [Z] would need [W] months. Consider reducing to [recommended hours]." |
| User requests open world with team <10 | "Open world games from studios of [team size] typically fail to ship. Consider: Hub-and-Spoke (Monster Hunter), Linear with Exploration (Metroidvania), or Semi-Open (zones with loading)." |

## 2. Technical Risk Assessment

### Engine/Platform Risk Factors

| Decision | Risk | Mitigation |
|----------|------|-----------|
| Custom engine | Very High — 6-18 months before gameplay work begins | Use established engine unless custom tech is the core innovation |
| Unproven middleware | High — integration bugs, abandoned support | Verify active maintenance, community size, escape plan |
| Cross-platform launch | High — platform-specific bugs multiply QA | Launch on 1 platform, port after stable |
| Mobile + PC simultaneous | High — UI, input, and performance need separate passes | Design for mobile first, scale up to PC |
| Targeting bleeding-edge hardware | Medium — small install base, SDK instability | Target current-gen stable, add next-gen enhancements |

### Architecture Red Flags

| Red Flag | What It Means | Recommended Action |
|----------|-------------|-------------------|
| No data-driven systems | Game logic hardcoded, can't tune without recompile | Design config schemas before coding (see implementation.md) |
| No save/load plan at start | Save system becomes a retrofit nightmare | Define serializable state early |
| Singletons everywhere | Testing impossible, state bugs, hidden dependencies | Use dependency injection or service locator pattern |
| No build pipeline | Manual builds, no CI/CD, no automated testing | Set up automated builds in week 1 |
| Physics-dependent gameplay without physics prototype | Core feel unknown until late | Prototype physics interactions in week 1 |

## 3. Design Risk Assessment

### Balance Risks

| Risk | Detection Method | Mitigation |
|------|-----------------|-----------|
| Dominant strategy (one build wins everything) | Playtest with 5+ testers building independently | Ensure counter-play exists for every strong strategy |
| Economy inflation (player wealth spirals) | Track wealth curve over 10-session simulation | Add sinks that scale with income |
| Difficulty wall (sudden unbeatable spike) | Death heatmap from playtests | Smooth curve, add optional assist mechanics |
| Progression dead zone (nothing new for 30+ min) | Track unlock cadence in spreadsheet | Ensure new content/ability every 15-30 min |
| RNG frustration (outcomes feel random, not earned) | Monitor variance in player outcomes | Use PRD instead of true random (see economy_and_progression.md §4.1) |

### Content Risks

| Risk | Trigger | Mitigation |
|------|---------|-----------|
| Art style inconsistency | Multiple artists without style bible | Lock style bible before production art begins |
| Narrative-gameplay disconnect | Story says one thing, gameplay rewards another | Align narrative incentives with core loop rewards |
| Tutorial failure | >30% playtest dropout before completing tutorial | Simplify, add progressive hints, remove text walls |
| Endgame emptiness | Players reach "end" in <50% of expected time | Design endgame systems (prestige, ranked, sandbox) early |
| Platform rejection | Content violates store guidelines | Review platform content policies before finalizing design |

## 4. Market and Business Risks

| Risk | Indicator | Mitigation |
|------|----------|-----------|
| No comparable successful title | Can't find 3+ games in the same niche that sold well | Validate demand before investing heavily — prototype and gauge interest |
| Competing with well-funded studios | Direct competitor has 10x budget | Differentiate on a specific axis they can't match (niche audience, unique mechanic, art style) |
| Monetization-gameplay conflict | Core loop requires spending to progress | Redesign so spending accelerates but never gates progress |
| Launch window collision | Releasing same month as major AAA title in same genre | Track release calendars, shift by 2-4 weeks if needed |
| Platform dependency | Single store, single platform, no diversification | Plan for at least 2 platforms within 6 months of launch |

## 5. Risk Response Protocol

When a risk is identified, the orchestrator must:

1. **Name the risk explicitly** — don't hedge or bury it
2. **Quantify the impact** — person-weeks, percentage of budget, delay estimate
3. **Offer exactly 2-3 concrete alternatives** — not vague "consider reducing scope"
4. **Recommend one option** with reasoning
5. **Ask the user to decide** before proceeding with the plan

Example:
> "Risk: Your 12-character roster requires ~480 unique animations (40 per character). For a 3-person team, this is approximately 32 weeks of dedicated animation work.
>
> Options:
> 1. Reduce roster to 4 characters at launch, add more post-launch (recommended — ships in 11 weeks of animation)
> 2. Use shared animation skeletons — 6 characters with 50% shared moves (18 weeks)
> 3. Keep 12 characters but use simpler animation style (sprite-based instead of skeletal, ~20 weeks)
>
> Which approach fits your timeline?"
