# Launch And Operations

## Goal

Plan the game's release strategy, store presence, analytics infrastructure, live operations framework, community management, and post-launch roadmap. This module covers everything from "the game is feature-complete" to "the game is thriving in market" — producing documentation, checklists, and frameworks rather than code.

## When To Use

- After QA validates the game is shippable (see [qa-testing.md](qa-testing.md))
- During production: plan store pages and analytics early, not last-minute
- When the user asks about "launch", "release", "store page", "analytics", "live ops", or "marketing"
- When transitioning from development to operations mindset

---

## Store Page Design

### Platform Requirements

#### Steam

| Element | Requirement | Best Practice |
|---------|------------|---------------|
| Capsule art | 460x215 (small), 616x353 (large) | Strong focal point, readable at small size |
| Header image | 460x215 | Game logo + key art |
| Screenshots | Min 5, 1920x1080 recommended | Show gameplay variety, include UI |
| Trailer | Recommended, no hard requirement | 60-90s, gameplay first, story hook second |
| Short description | Max 300 chars | Genre + unique hook in first sentence |
| Long description | No hard limit | Features, story, key selling points with formatting |
| Tags | Up to 20 | Most relevant first, match player search behavior |
| System requirements | Minimum + recommended | Be accurate — bad spec = refunds |

#### App Store (iOS)

| Element | Requirement | Best Practice |
|---------|------------|---------------|
| App icon | 1024x1024 | Simple, recognizable, no text |
| Screenshots | Up to 10, device-specific sizes | First 3 are most important — show core loop |
| App preview video | Up to 3, 15-30s each | Silent autoplay — must work without audio |
| Title | Max 30 chars | Game name + core keyword |
| Subtitle | Max 30 chars | Key genre or feature hook |
| Description | Max 4000 chars | First 3 lines visible without expand — front-load value |
| Keywords | 100 chars total | Research competition, no spaces after commas |

#### Google Play

| Element | Requirement | Best Practice |
|---------|------------|---------------|
| App icon | 512x512 | Match iOS for brand consistency |
| Feature graphic | 1024x500 | Hero image for store listing |
| Screenshots | Min 2, up to 8 | Match iOS order and content |
| Video | YouTube link | 30-120s, landscape preferred |
| Title | Max 50 chars | Game name + key search term |
| Short description | Max 80 chars | Core value proposition |
| Full description | Max 4000 chars | Keyword-rich, feature-focused |
| Content rating | IARC questionnaire | Fill accurately to avoid takedowns |

### ASO (App Store Optimization) Basics

- Research competitor keywords with tools or manual search
- Place highest-value keywords in title and subtitle
- Update screenshots and description with every major update
- Respond to reviews (especially negative ones) — affects ranking
- Track conversion rate: store page views → installs
- A/B test icons and screenshots when available (Google Play Experiments)

---

## Analytics and Data

### Core Event Schema

Define these events at minimum for any game:

| Event | Parameters | Purpose |
|-------|-----------|--------|
| `session_start` | platform, build_version, device_id | Track DAU, session frequency |
| `session_end` | duration_seconds, reason (quit/crash/background) | Session length, crash rate |
| `level_start` | level_id, player_level, difficulty | Funnel analysis |
| `level_complete` | level_id, duration, score, deaths, items_used | Completion rates, difficulty tuning |
| `level_fail` | level_id, fail_reason, attempt_number, duration | Difficulty spikes, churn points |
| `purchase_item` | item_id, currency_type, amount, player_balance_after | Economy health |
| `iap_purchase` | product_id, price, currency, store | Revenue tracking |
| `tutorial_step` | step_id, duration, skipped | Onboarding funnel |
| `achievement_unlock` | achievement_id, time_since_install | Content engagement |
| `ad_shown` | ad_type, placement, watched_fully | Ad revenue, player tolerance |
| `error` | error_type, stack_trace_hash, context | Crash and error monitoring |

### Event Naming Convention

- Use `snake_case` for all event names
- Prefix with category: `combat_`, `ui_`, `economy_`, `social_`, `system_`
- Parameters use `snake_case`, consistent types (strings for IDs, integers for counts, floats for durations)
- Never log PII (personal identifiable information)
- Include `event_timestamp`, `session_id`, and `player_id` on every event

### Dashboard Design

Build these dashboards for launch monitoring:

**Executive Dashboard**
- DAU / WAU / MAU with trend
- Revenue (if applicable) daily and cumulative
- Retention: D1, D3, D7, D14, D30
- Session count and average session length
- Crash rate per build

**Gameplay Dashboard**
- Level completion funnel (% reaching each level)
- Average time per level
- Death/fail heatmap by level
- Most-used items/abilities/builds
- Boss clear rates

**Economy Dashboard** (if applicable)
- Currency inflow vs. outflow per day
- Shop purchase frequency by item
- Average player balance over time
- IAP conversion rate and ARPDAU
- Gacha/loot box pull frequency and pity distribution

**Technical Dashboard**
- FPS distribution by device
- Crash rate by platform and build
- Load time distribution
- Memory usage trends
- Network error rates (if online)

---

## Live-Ops Framework

### Content Update Cadence

| Update Type | Frequency | Content | Effort |
|-------------|-----------|---------|--------|
| Hotfix | As needed | Bug fixes, critical balance | Low |
| Minor update | Bi-weekly to monthly | Quality of life, small content additions | Medium |
| Major update | Monthly to quarterly | New features, large content drops | High |
| Seasonal event | Quarterly or by real-world calendar | Themed content, limited-time rewards | Medium-High |
| Expansion / DLC | Semi-annually or annually | Major new content, new systems | Very High |

### Event Design Template

```
EVENT: [Name]
THEME: [Real-world holiday, in-game lore event, seasonal theme]
DURATION: [Start date → End date]
TYPE: [Challenge / Collection / Competitive / Cooperative / Story]

MECHANIC:
- [Core activity: what does the player do?]
- [Progress system: how does the player advance?]
- [Completion target: what is the goal?]

REWARDS:
- Free tier: [Participation rewards, available to all players]
- Premium tier: [Battle pass or paid rewards, if applicable]
- Exclusive: [Limited-time items that won't return]

ENTRY REQUIREMENTS:
- [Minimum player level or progression]
- [Any prerequisite quests or unlocks]

ANALYTICS:
- [Key events to track for this event]
- [Success metrics: participation rate, completion rate, retention lift]
```

### Battle Pass Structure

If applicable to the game:

| Parameter | Recommendation |
|-----------|---------------|
| Duration | 4-8 weeks (aligns with content cycles) |
| Tier count | 30-50 tiers |
| Free tier rewards | ~30-40% of total rewards, including gameplay-relevant items |
| Premium tier rewards | Cosmetics, premium currency, exclusive items |
| XP per tier | Achievable with ~1 hour/day of play |
| Catch-up mechanism | Bonus XP weekends, purchasable tiers (limited) |
| FOMO balance | Core rewards achievable with casual play; only cosmetic exclusives |

---

## Community and Marketing

### Channel Strategy

| Channel | Purpose | Content Type | Frequency |
|---------|---------|-------------|----------|
| Steam/Store page | Convert visitors to buyers/wishlisters | Screenshots, trailers, descriptions | Update with major patches |
| Social media (Twitter/X) | Build awareness, engage community | Dev updates, GIFs, polls, memes | 3-5x/week |
| Discord / Forum | Deepen community, gather feedback | Patch notes, discussions, bug reports | Daily moderation |
| YouTube | Showcase depth, attract search traffic | Trailers, devlogs, tutorials | 1-2x/month |
| Press/Influencer | Reach new audiences | Review keys, press kits, early access | Key moments only |
| Email newsletter | Reach committed fans directly | Major announcements, sales | 1-2x/month |

### Launch Timeline

| Timing | Action |
|--------|--------|
| T-6 months | Store page live, start wishlisting campaign |
| T-3 months | Press outreach begins, demo available (if applicable) |
| T-2 months | Trailer finalized, store page polished |
| T-1 month | Review key distribution, influencer outreach |
| T-2 weeks | Launch trailer, social media ramp-up |
| T-1 week | Final build submitted, store page finalized |
| Launch day | Community engagement, monitor analytics, hotfix ready |
| T+1 day | Respond to initial feedback, address critical bugs |
| T+1 week | First patch based on launch data |
| T+1 month | First content update or major patch |

### Press Kit Contents

- Game name, developer name, release date
- High-res key art and logo
- 5-10 curated screenshots
- Trailer (embedded or download link)
- Game description (short and long)
- Key features bullet list
- Developer background
- Contact information
- Download links for assets (no login required)

---

## Post-Launch Roadmap

### Patch Priority Framework

| Priority | Criteria | Timing |
|----------|---------|--------|
| P0 — Emergency | Crash affecting >10% of players, data loss, security issue | Same day |
| P1 — Critical | Major feature broken, significant balance issue, review-impacting bug | Within 48 hours |
| P2 — Important | Quality of life issues, minor balance adjustments | Next scheduled patch |
| P3 — Enhancement | Feature requests, polish, optimization | Roadmap consideration |

### Update Cadence Template

```
MONTH 1:
  Week 1: Launch + hotfixes
  Week 2: Stability patch (P0/P1 issues from launch)
  Week 3-4: First content patch planning + QoL improvements

MONTH 2:
  Week 1-2: Content Update 1 development
  Week 3: Content Update 1 release
  Week 4: Analytics review, community feedback synthesis

MONTH 3:
  Week 1-2: Content Update 2 development + first seasonal event planning
  Week 3: Content Update 2 release
  Week 4: Roadmap review based on 3 months of data

ONGOING:
  Monthly content updates
  Quarterly seasonal events
  Semi-annual major features or expansions
  Continuous community engagement and analytics monitoring
```

### Post-Launch Success Metrics

| Metric | Healthy | Warning | Critical |
|--------|---------|---------|----------|
| D1 retention | >40% | 25-40% | <25% |
| D7 retention | >20% | 10-20% | <10% |
| D30 retention | >10% | 5-10% | <5% |
| Session length | >15 min | 5-15 min | <5 min |
| Crash rate | <1% | 1-5% | >5% |
| Store rating | >4.0 | 3.5-4.0 | <3.5 |
| DAU trend | Stable or growing | Declining <10%/week | Declining >10%/week |
| ARPDAU (F2P) | >$0.05 | $0.02-0.05 | <$0.02 |
| Refund rate (premium) | <5% | 5-10% | >10% |
