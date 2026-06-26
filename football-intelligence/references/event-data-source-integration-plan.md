# Event Data Source Integration Plan

**Created:** 2026-06-26  
**Model target:** Football Intelligence v3.1+  
**Purpose:** define exactly which match-event, tracking, odds, ratings, and context data sources should be integrated before the model claims stronger prediction precision.

---

## 0. Core principle

The model must not fill missing official stats from memory, narrative reports, or estimated screenshots.

Use this rule:

```text
No verified source = null, missing_official_stats, or confidence cap.
```

A complete dataset is better than a fake complete dataset. This file exists to move the repo from narrative-only calibration toward auditable event-level modeling.

---

## 1. Immediate source priority

### Tier A — high-value open event data

| Source | Data type | Best use | Integration priority | Notes |
|---|---|---|---:|---|
| StatsBomb Open Data | Event data + some 360 freeze-frame data | xG, shot context, possession chains, pressure, pass maps, set pieces, player roles | 1 | Best free source for event-model development. Use for method training, not necessarily 2026 live coverage. |
| Wyscout public event dataset / soccer logs | Event data | VAEP/xT training, event schema testing, possession sequence modeling | 2 | Strong for broad historical model training. Verify license before redistribution. |
| Metrica Sports sample data | Event + tracking sample | Tracking-derived features, pitch-control prototypes | 3 | Small sample; use for algorithm design only. |
| SkillCorner open tracking data | Tracking sample | Off-ball movement, defensive line, compactness, speed, pressing behavior | 3 | Small sample; use for prototype feature definitions. |

### Tier B — match stats, xG, team strength, odds

| Source | Data type | Best use | Integration priority | Notes |
|---|---|---|---:|---|
| FBref | Team/player match and season stats | rolling xG/xGA, shots, pressures, passes, possession, player usage | 1 | Use through manual export or approved scraping tooling; respect rate limits. |
| Understat | xG and shot data for major leagues | xG/xGA baselines, shot maps, finishing over/underperformance | 1 | Club-league focused, not ideal for every international match. |
| ClubElo | Team strength ratings | pre-match strength, form-adjusted baseline | 1 | Great baseline for clubs; internationals need Elo/FIFA alternative. |
| football-data.co.uk | results + bookmaker odds | implied probability, closing-line benchmark, market efficiency | 1 | Add odds only as features, not as blind predictions. |
| football-data.org | fixtures/results/standings | schedule, standings, lineups where available | 2 | API-key based; good for automation. |
| OpenFootball / football.db | fixtures/results | fallback schedule validation | 3 | Not event-level. |

### Tier C — narrative and manual verification

| Source type | Best use | Warning |
|---|---|---|
| FIFA official match centre | official lineups, events, match stats, referee, venue | Preferred for World Cup official reconciliation when accessible. |
| Reuters/AP/BBC/Guardian/ESPN articles | mechanism, injuries, coach quotes, goal descriptions | Do not use for exact corners/cards unless explicitly listed. |
| Official team pages / federation posts | injuries, suspensions, lineups, training news | Current but may be incomplete. |

---

## 2. What each source should power

### 2.1 Match result model

Required inputs:

```yaml
pre_match_strength:
  home_team_rating:
  away_team_rating:
  rating_source: clubelo | fifa | elo_custom | market_implied
  rating_date:
market:
  home_odds:
  draw_odds:
  away_odds:
  over_under_lines:
  asian_handicap_lines:
  closing_line_available: true|false
team_form:
  last5_points:
  last5_xg_for:
  last5_xg_against:
  last10_goal_diff:
  opponent_adjusted: true|false
context:
  rest_days_home:
  rest_days_away:
  travel_km_away:
  neutral_venue: true|false
  tournament_stage:
  bracket_state_verified: true|false
```

### 2.2 Goals model

Required inputs:

```yaml
goal_model_inputs:
  home_xg_for_rolling:
  home_xg_against_rolling:
  away_xg_for_rolling:
  away_xg_against_rolling:
  shot_quality:
    home_avg_xg_per_shot:
    away_avg_xg_per_shot:
  finishing:
    home_goals_minus_xg:
    away_goals_minus_xg:
  game_state_incentives:
    draw_utility_home:
    draw_utility_away:
    gd_chase_home:
    gd_chase_away:
```

### 2.3 Corner model

Required inputs:

```yaml
corner_model_inputs:
  corners_for_last5:
  corners_against_last5:
  crosses_attempted:
  blocked_crosses:
  wide_attack_share:
  central_attack_share:
  underdog_exit_quality:
  set_piece_taker_quality:
  aerial_targets:
  score_state_sensitivity:
```

### 2.4 Cards/referee model

Required inputs:

```yaml
discipline_model_inputs:
  referee:
    name:
    cards_per_match:
    reds_per_match:
    penalties_per_match:
    fouls_called_per_match:
    advantage_play_tendency:
  teams:
    fouls_for_last5:
    fouls_against_last5:
    yellows_last5:
    red_cards_last20:
  tactical_foul_routes:
    transition_defense_exposure:
    winger_isolation_risk:
    midfield_duel_intensity:
```

### 2.5 Player props

Required inputs:

```yaml
player_prop_inputs:
  confirmed_lineup: true|false
  player:
    name:
    team:
    role: finisher | creator | connector | wide_crosser | target_forward | late_runner | set_piece_taker | fouler | fouled_player
    minutes_projection:
    shots_per90:
    xg_per90:
    xa_per90:
    key_passes_per90:
    touches_in_box_per90:
    fouls_committed_per90:
    fouls_won_per90:
```

---

## 3. Repository data rules

### 3.1 Raw data must not be committed when license is unclear

Do not commit commercial provider data or scraped data if redistribution rights are unclear.

Allowed in repo:

- source metadata
- schemas
- ingestion scripts
- small manually written examples
- derived fields only if license permits
- links and instructions

Not allowed without explicit permission:

- full Opta/Wyscout/StatsPerform feeds
- paywalled data dumps
- copied premium lineups or reports

### 3.2 Every data field needs provenance

All structured match records should include:

```yaml
source:
  provider:
  tier: A | B | C
  url_or_reference:
  retrieved_at:
  license_status: open | api_terms | private | unknown
  confidence: official | high | medium | partial | conflict_pending_review
```

---

## 4. Integration sequence

### Phase 1 — schema before data

1. Add event schema.
2. Add source policy.
3. Add feature registry.
4. Add confidence caps when features are missing.

### Phase 2 — open-data prototype

1. Build StatsBomb Open Data ingestion proof-of-concept.
2. Convert events to unified event schema.
3. Compute match-level aggregates:
   - xG
   - xG per shot
   - shot map zones
   - pressure count
   - possession chains
   - set-piece xG
   - wide attack share
4. Test the features on historical World Cup data.

### Phase 3 — prediction feature store

1. Create one feature row per team per match.
2. Add rolling windows with no future leakage.
3. Add pre-match-only feature cutoffs.
4. Add post-match reconciliation fields separately.

### Phase 4 — model validation

1. Train baseline model without new data.
2. Train event-enhanced model.
3. Train odds/rating-enhanced model.
4. Train ensemble model.
5. Compare:
   - log loss
   - Brier score
   - calibration curve
   - ROI vs closing odds if odds are available
   - market-specific accuracy

---

## 5. Missing data priorities for current World Cup files

The current `matches-md1-md2-through-20260623.yaml` is match-identity complete, but not stat-complete.

Reconciliation order:

1. Matches that created rules or exposed model failures.
2. Matches used as evidence in patterns.
3. Matches needed for bracket incentives.
4. Remaining normal matches.

Critical first batch:

```text
Jordan 1-2 Algeria
Belgium 0-0 Iran
Portugal 1-1 DR Congo
Canada 6-0 Qatar
Netherlands 5-1 Sweden
Germany 7-1 Curacao
Spain 0-0 Cape Verde
Ecuador 0-0 Curacao
England 0-0 Ghana
Switzerland 2-1 Canada
```

For each match, fill only verified values:

```yaml
referee:
venue:
weather:
halftime_score:
goals:
lineups:
substitutions:
xg:
shots:
shots_on_target:
possession:
corners:
cards:
fouls:
offsides:
source:
```

---

## 6. Confidence caps from data completeness

| Missing field | Cap affected market |
|---|---:|
| Missing lineups | player props max 5/10; side max 6.5/10 |
| Missing referee | cards max 5/10 |
| Missing team-specific corner/cross data | corners max 5/10 |
| Missing xG / shot-quality data | goals max 6.5/10 |
| Missing bracket table | tournament side/totals max 5/10 |
| Missing odds/market line | value-bet confidence max 6/10 |
| Missing weather/venue for outdoor tournament match | totals max 7/10 |

---

## 7. Immediate git action list

Add the following files:

```text
football-intelligence/references/event-data-source-integration-plan.md
football-intelligence/references/event-data-schema-v1.md
football-intelligence/references/monte-carlo-simulation-v4.md
football-intelligence/references/model-validation-and-calibration-v1.md
football-intelligence/templates/post-match-reconciliation-template.yaml
football-intelligence/templates/match-analysis-template-v4.md
football-intelligence/references/feature-registry-v1.yaml
```

These files should be additive. Do not overwrite the existing calibration log until verified stats are filled.
