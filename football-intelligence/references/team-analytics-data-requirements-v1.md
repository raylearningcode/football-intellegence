# Team Analytics Data Requirements v1

**Created:** 2026-06-26  
**Purpose:** define the full team-level data needed before Football Intelligence can produce high-quality predictions across all World Cup teams.

---

## 0. Core rule

Do not fake xG or advanced stats.

If a trusted xG/event provider is not available for a match or team, store:

```yaml
xg_for: null
xg_against: null
advanced_stats_status: missing_verified_provider
```

The model may still analyze with lower confidence, but it must say the data is incomplete.

---

## 1. Minimum team analytics profile

Each team should eventually have this profile:

```yaml
team_analytics_profile:
  team:
  code:
  group:
  updated_at:
  source_status:
    official_stats:
    xg_provider:
    event_data:
    tracking_data:
    latest_news:
  group_stage_record:
    played:
    wins:
    draws:
    losses:
    goals_for:
    goals_against:
    goal_difference:
    points:
  attacking:
    xg_for:
    goals_for:
    shots:
    shots_on_target:
    shots_in_box:
    big_chances:
    avg_xg_per_shot:
    conversion_rate:
    box_entries:
    progressive_passes:
    progressive_carries:
    crosses:
    blocked_crosses:
    set_piece_xg:
    corner_xg:
  defensive:
    xg_against:
    goals_against:
    shots_against:
    shots_on_target_against:
    big_chances_against:
    box_entries_against:
    ppda:
    high_turnovers_allowed:
    defensive_line_height:
    transition_exposure:
  possession_control:
    possession:
    field_tilt:
    pass_completion:
    directness:
    tempo:
    sterile_possession_risk:
  corners:
    corners_for:
    corners_against:
    corner_creation_mechanism:
    corner_concession_mechanism:
    wide_attack_share:
  discipline:
    fouls_committed:
    fouls_won:
    yellow_cards:
    red_cards:
    tactical_foul_risk:
  player_roles:
    primary_finisher:
    primary_creator:
    set_piece_taker:
    wide_crosser:
    chaos_player:
    defensive_anchor:
    goalkeeper:
    bench_impact_players:
  tactical_identity:
    base_shape:
    in_possession_shape:
    out_of_possession_shape:
    press_height:
    main_attack_route:
    main_defensive_weakness:
    preferred_game_state:
    bad_game_state:
  latest_news:
    checked_at:
    lineup_status:
    injuries:
    suspensions:
    rotation_risk:
    coach_quotes:
    model_impact:
  confidence:
    data_tier: 0|1|2|3|4
    side_market_cap:
    goals_market_cap:
    corners_market_cap:
    cards_market_cap:
    player_props_cap:
  sources:
    - provider:
      field:
      url_or_reference:
      retrieved_at:
      confidence:
```

---

## 2. Data tiers

| Tier | Meaning | Use |
|---|---|---|
| 0 | score/standings only | bracket/form only, low confidence |
| 1 | score + scorers + lineups | basic tactical notes |
| 2 | official match stats | goals/corners/cards calibration |
| 3 | event data/xG | strong tactical and xG modeling |
| 4 | event + tracking + live feeds | full Monte Carlo v4 and player movement modeling |

---

## 3. Source priority for team analytics

### xG / event data

Priority order:

```text
1. StatsBomb / Opta / Stats Perform / Wyscout / SkillCorner / FIFA official analytics if licensed or accessible
2. FBref / provider match reports if xG table is visible and allowed
3. Understat for club-team historical player/team xG context only
4. Public open-data datasets for model training, not necessarily current World Cup coverage
```

### Match stats

Priority order:

```text
1. FIFA official match centre
2. FotMob / ESPN / SofaScore / 365Scores / Flashscore if stat table is visible
3. Reuters/AP/BBC/Guardian only when exact stats are explicitly listed
```

### Latest news

Priority order:

```text
1. official team/federation/competition reports
2. Reuters/AP/BBC/Guardian/ESPN lineup or preview reports
3. trusted local reporters
4. official social media
5. unverified social media only as weak note, not model driver
```

---

## 4. Required pre-match fields by market

### Side market

```text
ratings
recent form
xG/xGA if available
lineups/absences
midfield control
defensive structure
bracket incentive
market price
```

### Goals market

```text
xG/xGA
shot quality
finishing over/underperformance
repeatable scoring routes
defensive absences
weather
bracket aggression/draw utility
```

### Corners market

```text
corners for/against
crosses
blocked crosses
wide attack share
set-piece takers
target forward/aerial strength
underdog exit quality
first-goal branch
```

### Cards market

```text
referee
team fouls/cards
player card risk
tactical foul routes
match tension
suspension risk
```

### Player props

```text
confirmed lineup
minutes projection
role
shots/key passes/fouls per90
set-piece duty
opponent matchup
```

---

## 5. Confidence cap rules

If missing:

```yaml
missing_xg:
  goals_market_cap: 6.5
missing_corners_crosses:
  corners_market_cap: 5.0
missing_referee:
  cards_market_cap: 5.0
missing_lineups:
  player_props_cap: 5.0
missing_latest_news:
  overall_analysis_cap: 6.0
missing_market_odds:
  value_bet_cap: 6.0
```

---

## 6. Update workflow

When adding team data:

```text
1. Verify source and license.
2. Fill only source-backed fields.
3. Keep unknown fields null.
4. Add source provenance per field.
5. Update team status map.
6. Update latest-news cache when news affects future analysis.
7. Do not overwrite older records without a source note.
```

---

## 7. Expected model improvement

Proper team analytics data improves:

- xG-based goal projections,
- side probability calibration,
- corner model accuracy,
- card/player prop confidence,
- Monte Carlo v4 input quality,
- post-match reconciliation,
- profile updates,
- and faster future match analysis.
