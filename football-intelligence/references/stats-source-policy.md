# Football Intelligence — Reliable Stats Source Policy

**Created:** 2026-06-23  
**Purpose:** Standardize where match statistics come from so analysis does not mix live-blog estimates, screenshots, and unverifiable numbers.

---

## Core principle

There is no such thing as a guaranteed error-free public football statistics website. Even official and commercial providers can revise event data after full-time.

Therefore the repo must use a **source hierarchy** and a **verification rule** instead of trusting one website blindly.

---

## Source hierarchy

### Tier A — Primary official source

Use first whenever available:

1. **FIFA official match centre / official match report**
   - Final score
   - Lineups
   - Substitutions
   - Cards
   - Referee
   - Venue
   - Team statistics
   - Match events

Tier A data can be written into the structured dataset as `verified_official`.

---

### Tier B — Stable full-stat match centres

Use when official FIFA stat table is unavailable or incomplete:

1. **FotMob match page**
2. **ESPN match stats page**
3. **SofaScore match page**
4. **365Scores / Flashscore / AiScore match statistics**

Tier B data can be written into the dataset only if the exact stat table is visible and extractable.

Recommended fields to capture:

- possession
- shots
- shots on target
- big chances
- xG, if provided
- corners
- fouls
- cards
- offsides
- passes / pass accuracy
- goalkeeper saves
- tackles / interceptions, if available

When Tier B sources disagree, keep both values in a note and mark the field `conflict_pending_review`.

---

### Tier C — Narrative sources

Use only for match mechanism, not final stat totals:

1. Reuters
2. Associated Press
3. Guardian match report / live blog
4. BBC / Sky / ESPN article text
5. Local reputable outlets

Tier C is useful for:

- why the game shifted
- tactical quotes
- injury/team news
- goal descriptions
- manager quotes
- pressure/corner mechanism
- card-causing fouls

Tier C should not be used as the final source for exact total corners/cards unless the article explicitly lists the stat.

---

## Required verification rule for detailed stats

For any detailed stat used in betting analysis:

```text
If the stat is from Tier A: accept as official.
If the stat is from Tier B: accept only if visible/extractable and cite source.
If the stat is from Tier C: use only as mechanism evidence, not as official total.
If two sources conflict: do not choose silently; mark conflict and explain.
```

---

## Field-level reliability

| Field | Minimum source tier | Notes |
|---|---|---|
| final score | A or reliable B/C | Usually stable after full-time |
| goals/scorers | A or reliable B/C | Can use Reuters/Guardian if clearly reported |
| lineups | A or B | Prefer official |
| substitutions | A or B | Avoid live-blog-only unless exact |
| referee | A or B | Needed for card confidence |
| yellow/red cards | A or B | Live-blog cards can be incomplete |
| corners | A or B only | Do not infer from live-blog mentions |
| corner times | B or live log with explicit event | Mark partial if from live blog |
| xG | B provider only | Record provider name; xG models differ |
| shots/SOT | A or B | Reuters article totals acceptable only if explicitly stated |
| possession | A or B | Provider differences possible |
| fouls | A or B | Needed for cards model |
| offsides | A or B | Optional |
| weather | official weather/match source | Do not estimate |

---

## Practical rule for SofaScore

SofaScore is allowed as a Tier B source **only when the match statistics table is directly visible and extractable**.

If SofaScore is blocked, not indexed, requires dynamic rendering, or cannot be read reliably, do not use guessed SofaScore numbers. Fall back to FIFA/FotMob/ESPN/Flashscore/AiScore or mark `missing_official_stats`.

---

## Portugal-Uzbekistan immediate source decision

For Portugal vs Uzbekistan and future World Cup matches:

1. Try FIFA official match centre first.
2. If unavailable, try FotMob or ESPN match stats.
3. If unavailable, try SofaScore/Flashscore/AiScore.
4. Use Reuters/Guardian only for mechanism and quotes.
5. Do not fill exact corners/cards from live-blog fragments unless clearly marked as partial event evidence.

---

## Repository write rule

When adding data to `data/world-cup-2026/*.yaml`, every detailed stat must include:

```yaml
source:
  provider:
  tier:
  url_or_reference:
  verified_at:
  confidence: official | high | medium | partial | conflict_pending_review
```

If no reliable source is available, write:

```yaml
corners: null
cards: null
xg: null
detailed_stats_status: missing_official_stats
```

Never fill fake completeness.

---

## Why this matters

The model's biggest current weakness is not lack of ideas. It is bad or incomplete market-specific data, especially corners and cards. Exact corners, cards, fouls, and xG must be treated as auditable data, not memory.

Reliable source discipline protects the betting model from false confidence.
