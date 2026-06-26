# World Cup 2026 Data Acquisition Request

**Created:** 2026-06-26  
**Purpose:** list the exact data and API access needed to fill xG, event data, team analytics, player analytics, latest news, and Monte Carlo inputs for all World Cup teams.

---

## 0. Current state

The repository is ready structurally, but the current public data available in-repo is not enough for high-confidence advanced analytics.

The file below tracks all teams and missing advanced fields:

```text
football-intelligence/data/world-cup-2026/team-analytics-status-20260626.yaml
```

Most xG/event fields are intentionally `null` because no complete trusted current World Cup 2026 xG/event feed has been connected yet.

---

## 1. Highest-priority data needed

### Tier 1 — must-have for serious prediction quality

```text
1. Match-level xG and xGA
2. Shot-level xG with shot location, body part, play pattern, pressure, assist type
3. Official lineups and substitutions
4. Injuries, suspensions, yellow-card risk, rotation news
5. Corners for/against and corner timing
6. Cards/fouls and referee profile
7. Odds: opening/current/closing 1X2, AH, totals, BTTS, corners, cards
8. Team rolling form with no future leakage
```

### Tier 2 — needed for better Monte Carlo v4

```text
1. Event stream: passes, carries, pressures, tackles, interceptions, clearances
2. Possession chains and sequence IDs
3. Progressive passes/carries
4. Box entries and final-third entries
5. Crosses and blocked crosses
6. Set-piece events and set-piece xG
7. Transition events and counterattacks
8. Goalkeeper actions and post-shot xG / xGOT if available
```

### Tier 3 — elite model layer

```text
1. Tracking data / 360 freeze frames
2. Pitch control
3. Defensive line height
4. Team compactness
5. Pressing traps and pressure radius
6. Player speed/acceleration/fatigue proxies
7. Off-ball runs
```

---

## 2. Best data-source options

### Option A — StatsBomb / StatsBomb Open Data

**Use for:** event-schema development, xG/shot model training, 360-data method prototypes.

Pros:

```text
- Open Data has JSON competitions, matches, events, lineups, and selected 360 files.
- Great for building event pipeline, xT, VAEP, and shot-model testing.
- No API key needed for open-data repository.
```

Limitations:

```text
- Open data does not automatically include live/current World Cup 2026 full coverage.
- Must check available competitions/seasons before assuming coverage.
- Attribution rules apply.
```

Need from user:

```text
No key needed for open data.
If user has paid StatsBomb API access, provide API credentials or exported JSON files.
```

---

### Option B — Opta / Stats Perform

**Use for:** highest-quality current event data, xG, xA, xGOT, lineups, player stats, team stats, match centre feeds.

Pros:

```text
- Commercial-grade football event/stat data.
- Strong for current tournament coverage if licensed.
- Likely best source for full current World Cup analytics if available.
```

Limitations:

```text
- Paid/commercial.
- Redistribution restrictions likely apply.
- Raw data may not be commit-safe unless license permits.
```

Need from user:

```text
Stats Perform / Opta API access, export files, or dashboard screenshots/tables with permission to use internally.
```

Do not commit raw commercial feeds unless license allows it.

---

### Option C — Wyscout / Hudl

**Use for:** event data, player roles, tactical scouting, video-backed events.

Pros:

```text
- Strong scouting/event platform.
- Good for player movement and tactical mechanisms.
```

Limitations:

```text
- Paid/commercial.
- Export/API rights must be checked.
```

Need from user:

```text
Wyscout/Hudl access, API/export permission, or manually exported CSV/JSON.
```

---

### Option D — SkillCorner / Second Spectrum / tracking providers

**Use for:** off-ball movement, compactness, line height, speed, pressing, pitch control.

Pros:

```text
- Best for the model's missing off-ball layer.
- Improves pressing, defensive block, and transition simulations.
```

Limitations:

```text
- Usually paid.
- Current World Cup access uncertain.
- Raw tracking data can be restricted.
```

Need from user:

```text
Tracking data access or exported tracking metrics.
```

---

### Option E — FBref / Stathead-style tables

**Use for:** xG/xGA, shooting, possession, passing, defense, keeper, standard team/player stats when available.

Pros:

```text
- Useful for team and player stat tables.
- Often includes xG-style metrics for major competitions.
```

Limitations:

```text
- Scraping restrictions/rate limits must be respected.
- Current World Cup 2026 coverage must be verified page-by-page.
- Not always event-level.
```

Need from user:

```text
No API key usually, but we need permission-compliant access or manual CSV exports.
```

---

### Option F — FotMob / SofaScore / ESPN / Flashscore / 365Scores

**Use for:** match stats, lineups, player ratings, shots, SOT, possession, corners, cards; sometimes xG.

Pros:

```text
- Good current-match coverage.
- Often fast and complete for basic match stats.
```

Limitations:

```text
- Public scraping/API rules vary.
- xG may be provider-specific or not exportable.
- Some data may be display-only.
```

Need from user:

```text
Manual exported tables/screenshots or approved API access if available.
```

---

### Option G — football-data.co.uk / odds APIs

**Use for:** historical odds, opening/closing lines, market-implied probabilities.

Pros:

```text
- Excellent for market backtesting where competitions are covered.
- Critical for value-bet evaluation.
```

Limitations:

```text
- May not cover all World Cup 2026 props/corners/cards.
- Event data not included.
```

Need from user:

```text
Odds source/API if current World Cup markets are needed: OddsAPI, Bet365 export, Pinnacle feed, Betfair/Exchange, or any odds CSV.
```

---

### Option H — API-Football / SportMonks / similar football APIs

**Use for:** fixtures, standings, lineups, injuries, basic stats, odds depending plan.

Pros:

```text
- Easier API integration than commercial event providers.
- Good for automation and current team news/status.
```

Limitations:

```text
- xG/event depth may be limited or plan-dependent.
- Provider data quality must be tested.
```

Need from user:

```text
API key and plan details.
```

---

## 3. What user should provide

If possible, provide one of these:

### Best option

```text
A paid/current football event-data provider export or API:
- StatsBomb paid API
- Opta / Stats Perform
- Wyscout / Hudl
- SkillCorner / tracking provider
```

### Practical option

```text
A current football API key:
- API-Football
- SportMonks
- football-data.org
- Odds API
- any provider that includes World Cup fixtures, lineups, injuries, stats, and odds
```

### Manual fallback

```text
CSV/Excel exports or screenshots/tables for each match containing:
- xG
- shots / SOT
- possession
- corners
- cards
- fouls
- lineups/subs
- player stats
- odds
```

---

## 4. Environment variables to use later

Do not hardcode secrets into GitHub.

Use `.env` locally:

```bash
STATSBOMB_API_USER=
STATSBOMB_API_PASSWORD=
OPTA_API_KEY=
WYSCOUT_API_KEY=
SKILLCORNER_API_KEY=
API_FOOTBALL_KEY=
SPORTMONKS_API_KEY=
FOOTBALL_DATA_ORG_KEY=
ODDS_API_KEY=
```

Commit only `.env.example`, never `.env`.

---

## 5. Data storage policy

### Safe to commit

```text
schemas
source metadata
field availability maps
small manually curated source-backed summaries
derived model inputs if license permits
```

### Do not commit unless license permits

```text
commercial raw event feeds
commercial tracking data
paid provider bulk exports
premium odds feeds
```

For restricted data, store locally and commit only derived/aggregated values if allowed.

---

## 6. Target files to fill after access is available

```text
football-intelligence/data/world-cup-2026/team-analytics-status-20260626.yaml
football-intelligence/data/world-cup-2026/team-advanced-stats-20260626.yaml
football-intelligence/data/world-cup-2026/match-stat-packs/
football-intelligence/data/world-cup-2026/latest-team-news/
football-intelligence/data/world-cup-2026/odds-snapshots/
football-intelligence/data/world-cup-2026/player-role-stats/
```

---

## 7. Minimal viable fill target

For each team:

```yaml
team:
code:
group:
played:
points:
goals_for:
goals_against:
xg_for:
xg_against:
shots_for:
shots_against:
shots_on_target_for:
shots_on_target_against:
corners_for:
corners_against:
yellow_cards:
red_cards:
fouls_committed:
fouls_won:
primary_finisher:
primary_creator:
set_piece_taker:
latest_news_checked:
sources:
```

---

## 8. Match-level fill target

For every match:

```yaml
match_id:
date:
teams:
score:
venue:
referee:
lineups:
substitutions:
goals:
cards:
shots:
shots_on_target:
xg:
possession:
corners:
fouls:
offsides:
passes:
progressive_passes:
crosses:
blocked_crosses:
set_piece_xg:
transition_xg:
odds_open:
odds_close:
sources:
```

---

## 9. Ingestion plan once credentials/data arrive

```text
1. Confirm provider and license.
2. Create .env.example with required variable names.
3. Write a provider-specific ingestion script.
4. Convert raw data to event-data-schema-v1.
5. Aggregate match-level stats.
6. Aggregate team-level rolling stats.
7. Update team-analytics-status readiness.
8. Add latest-news cache for upcoming matches.
9. Run validation/backtest.
10. Commit only allowed derived outputs.
```

---

## 10. Immediate ask to user

Please provide one of the following:

```text
1. API-Football key / SportMonks key / football-data.org key / Odds API key
2. StatsBomb / Opta / Wyscout / SkillCorner access or exports
3. CSV/Excel exports with match stats and xG
4. Screenshots/tables from trusted stat pages for each match
```

Also tell whether the data can be committed to GitHub, or only used locally to produce derived summaries.
