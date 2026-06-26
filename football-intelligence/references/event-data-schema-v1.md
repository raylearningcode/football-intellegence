# Event Data Schema v1

**Created:** 2026-06-26  
**Purpose:** provide a unified schema for match events, tracking-derived features, match stats, source provenance, and model-ready feature rows.

---

## 0. Design principle

The repo currently has strong narrative calibration but incomplete official event/stat data. This schema separates:

1. raw facts,
2. source metadata,
3. derived features,
4. analyst interpretation,
5. model output.

Never mix those layers.

---

## 1. Match identity schema

```yaml
match:
  match_id:
  provider_match_id:
  competition:
  season:
  stage:
  group:
  matchday:
  date_utc:
  kickoff_local:
  timezone:
  venue:
  city:
  country:
  neutral_venue: true|false
  home_team:
    name:
    code:
    provider_id:
  away_team:
    name:
    code:
    provider_id:
  final_score:
    home:
    away:
  halftime_score:
    home:
    away:
  status: scheduled | live | complete | postponed | abandoned
```

---

## 2. Source provenance schema

Every data block should carry provenance.

```yaml
source:
  provider:
  provider_tier: A_official | B_match_centre | C_narrative | D_estimate
  url_or_reference:
  retrieved_at:
  license_status: open | api_terms | private | unknown
  confidence: official | high | medium | partial | conflict_pending_review | estimated
  notes:
```

Rules:

- `D_estimate` cannot be used as final official stat data.
- If two Tier B sources conflict, store both and mark `conflict_pending_review`.
- Model confidence must be capped if major fields are not Tier A/B.

---

## 3. Event schema

Each event row should follow this shape.

```yaml
event:
  event_id:
  match_id:
  period: 1 | 2 | extra_time_1 | extra_time_2 | penalty_shootout
  minute:
  second:
  timestamp:
  possession_id:
  sequence_id:
  team:
    name:
    code:
    provider_id:
  player:
    name:
    provider_id:
    position:
  event_type:
  event_subtype:
  outcome:
  start_location:
    x:
    y:
  end_location:
    x:
    y:
  body_part:
  under_pressure: true|false|null
  play_pattern: open_play | counter | corner | free_kick | throw_in | goal_kick | penalty | kick_off | other
  related_event_ids: []
  qualifiers:
    pass_height:
    pass_length:
    pass_angle:
    cross: true|false|null
    cutback: true|false|null
    through_ball: true|false|null
    switch: true|false|null
    set_piece: true|false|null
    aerial_duel: true|false|null
    blocked: true|false|null
    deflected: true|false|null
    error_forced: true|false|null
  source:
```

---

## 4. Shot event extension

```yaml
shot:
  event_id:
  match_id:
  team:
  player:
  minute:
  location:
    x:
    y:
  body_part:
  shot_type: open_play | header | free_kick | penalty | corner_second_ball | rebound | own_goal_forced
  outcome: goal | saved | off_target | blocked | post | saved_to_post
  xg:
    value:
    provider:
    model_version:
  post_shot_xg:
    value:
    provider:
  assisted_by:
  assist_type: pass | cross | cutback | through_ball | rebound | set_piece | none
  defensive_pressure:
    pressure_count_nearby:
    goalkeeper_position_known: true|false
    shot_angle:
    distance_to_goal:
  source:
```

---

## 5. Pass/carry/progression extension

```yaml
progression_event:
  event_id:
  match_id:
  team:
  player:
  event_type: pass | carry | dribble
  start_location:
  end_location:
  progression_value:
    xT_delta:
    VAEP_delta:
    EPV_delta:
  zone:
    start_zone:
    end_zone:
  pressure_context:
    under_pressure:
    defenders_nearby:
  outcome:
  source:
```

---

## 6. Defensive action extension

```yaml
defensive_event:
  event_id:
  match_id:
  team:
  player:
  event_type: pressure | tackle | interception | block | clearance | foul | duel | recovery
  location:
  outcome:
  target_player:
  tactical_context:
    press_height: high | mid | low | unknown
    transition_defense: true|false|null
    rest_defense_exposed: true|false|null
  card:
    yellow: true|false
    red: true|false
    second_yellow: true|false
  source:
```

---

## 7. Set-piece schema

Set pieces drive corners, goals, cards, and chaos. Track them separately.

```yaml
set_piece:
  set_piece_id:
  match_id:
  minute:
  team:
  type: corner | direct_free_kick | indirect_free_kick | throw_in | penalty
  taker:
  delivery_type: inswing | outswing | driven | short | floated | low_cross | direct_shot | unknown
  target_zone: near_post | central | far_post | penalty_spot | six_yard | edge_box | short_option | unknown
  first_contact_team:
  first_contact_player:
  outcome: shot | goal | clearance | second_ball | foul | recycled | turnover
  xg_created:
  corner_sequence_shot: true|false
  source:
```

---

## 8. Tracking-derived frame schema

Only use when tracking data is legally available.

```yaml
tracking_frame:
  match_id:
  frame_id:
  period:
  timestamp:
  ball:
    x:
    y:
    z:
    speed:
  players:
    - player_id:
      team:
      x:
      y:
      speed:
      acceleration:
      distance_to_ball:
      role_at_frame:
  derived:
    defensive_line_height:
    team_length:
    team_width:
    compactness:
    nearest_defender_distance_to_ball:
    pressure_on_ball:
    pitch_control_home:
    pitch_control_away:
  source:
```

---

## 9. Match-level stat schema

```yaml
match_stats:
  match_id:
  team_stats:
    home:
      xg:
      post_shot_xg:
      shots:
      shots_on_target:
      shots_in_box:
      big_chances:
      possession:
      field_tilt:
      passes:
      pass_accuracy:
      progressive_passes:
      carries:
      progressive_carries:
      box_entries:
      crosses:
      blocked_crosses:
      corners:
      corner_xg:
      fouls:
      yellow_cards:
      red_cards:
      offsides:
      ppda:
      high_turnovers:
      goalkeeper_saves:
    away:
      # same fields
  source:
```

---

## 10. Model-ready feature row

This is the input row for pre-match prediction. It must only include data known before kickoff.

```yaml
pre_match_feature_row:
  match_id:
  generated_at:
  cutoff_time:
  home_team:
  away_team:
  competition:
  stage:
  venue_context:
    neutral_venue:
    travel_km_away:
    rest_days_home:
    rest_days_away:
    weather_forecast:
  ratings:
    home_rating:
    away_rating:
    rating_diff:
    source:
  market:
    home_implied_prob:
    draw_implied_prob:
    away_implied_prob:
    over25_implied_prob:
    btts_implied_prob:
    closing_line: true|false
  rolling_form:
    home_last5_xg_for:
    home_last5_xg_against:
    away_last5_xg_for:
    away_last5_xg_against:
    home_last5_points:
    away_last5_points:
    opponent_adjusted: true|false
  tactical_features:
    home_low_block_breaking_rating:
    away_low_block_breaking_rating:
    home_transition_threat:
    away_transition_threat:
    home_set_piece_threat:
    away_set_piece_threat:
    home_control_advantage:
    away_control_advantage:
  availability:
    home_key_absence_score:
    away_key_absence_score:
    lineup_confirmed: true|false
  bracket:
    home_draw_utility:
    away_draw_utility:
    home_gd_chase:
    away_gd_chase:
    third_place_rules_relevant: true|false
  data_quality:
    missing_critical_fields: []
    confidence_cap:
```

---

## 11. Post-match reconciliation schema

This is different from pre-match data.

```yaml
post_match_reconciliation:
  match_id:
  final_score:
  official_stats_available: true|false
  model_version:
  pre_match_probabilities:
    home_win:
    draw:
    away_win:
    over25:
    btts_yes:
  recommendations:
    - market:
      probability:
      confidence:
      tier:
  actual_market_results:
    home_win:
    draw:
    away_win:
    over25:
    btts_yes:
  grading:
    result:
    goals:
    btts:
    corners:
    cards:
    player_props:
    bet_construction:
  error_taxonomy:
    primary_error: E1_input | E2_tactical | E3_coach | E4_game_state | E5_set_piece | E6_referee | E7_simulation | E8_market | E9_variance
    secondary_errors: []
    repeatable: true|false
  new_lessons:
  action:
    no_change: true|false
    update_existing_rule:
    create_new_rule:
    monitor_pattern:
  source:
```

---

## 12. Data completeness tiers

| Tier | Meaning | Allowed confidence behavior |
|---|---|---|
| Tier 0 | identity + score only | post-match narrative only; no stat calibration |
| Tier 1 | goal events + narrative | mechanism notes allowed; no official stat conclusions |
| Tier 2 | basic official stats | result/goals/corners/cards calibration allowed |
| Tier 3 | event data | tactical/event model calibration allowed |
| Tier 4 | event + tracking + lineups + odds | full model calibration and feature backtest allowed |

---

## 13. Required validation checks

Before a row enters model training:

```text
1. No future leakage.
2. Source tier is A/B or explicitly marked lower.
3. Match IDs are stable.
4. Team names normalized.
5. Neutral venue and home/away labels verified.
6. Odds timestamp is before kickoff.
7. Rolling form window excludes current match.
8. Injury/lineup fields are timestamped.
9. Derived features can be reproduced.
10. Missing fields remain null, not zero.
```

---

## 14. Why this matters

The model's current strength is reasoning and calibration. Its weakness is auditable data depth.

This schema turns the repo into a system that can eventually support:

- event-level Monte Carlo,
- xG/xT/VAEP features,
- source-aware confidence caps,
- no-leakage training,
- better post-match learning,
- and honest model validation.
