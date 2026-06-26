# Monte Carlo Simulation v4 — Event-Aware Probabilistic Engine

**Created:** 2026-06-26  
**Target model:** Football Intelligence v3.1+  
**Purpose:** replace the current conceptual match simulation with a stronger, auditable, scenario-weighted, uncertainty-aware Monte Carlo framework.

---

## 0. Core upgrade

The current simulation idea is useful but too static. It mostly simulates final match outcomes from fixed probabilities.

v4 must simulate football as a branching process:

```text
pre-match state → tactical plan → first goal / no goal → game-state transition → substitutions/cards/fatigue → final score and markets
```

The output should not only say who wins. It should explain which match story creates that result.

---

## 1. Simulation levels

### Level 1 — Static outcome simulation

Use when data is weak.

Inputs:

- calibrated 1X2 probabilities,
- over/under probabilities,
- BTTS probability,
- draw floor,
- confidence cap.

Output:

- result probabilities,
- basic score distribution,
- confidence capped at 5.5–6/10.

### Level 2 — Goal-rate simulation

Use when team xG and strength data exist.

Inputs:

- home expected goals,
- away expected goals,
- draw inflation/deflation,
- low-event/open-game branch weights.

Model:

- Poisson or negative binomial goals.
- Dixon-Coles style correction for low scores if implemented.
- Overdispersion for tournament chaos or weak data.

### Level 3 — Scenario-weighted simulation

Use for serious pre-match predictions.

Branches:

1. favorite scores first early,
2. underdog scores first,
3. 0-0 at halftime,
4. favorite leads by one after 70',
5. draw after 75',
6. red card between 55' and 75',
7. late chase / goal-difference push,
8. low-block sterile possession.

### Level 4 — Event-aware simulation

Use when event/tracking data are available.

Simulate:

- possession chains,
- shot creation,
- shot quality,
- set pieces,
- corners,
- fouls/cards,
- substitutions,
- player availability,
- tactical shifts,
- fatigue.

---

## 2. Required pre-simulation input sheet

```yaml
simulation_input:
  match_id:
  model_version:
  generated_at:
  data_quality_tier: 0|1|2|3|4
  teams:
    home:
      name:
      rating:
      attack_strength:
      defense_strength:
      xg_for:
      xg_against:
      xg_uncertainty:
      finishing_modifier:
      set_piece_modifier:
      transition_modifier:
      low_block_breaking_rating:
      tactical_control_rating:
      lineup_absence_penalty:
    away:
      # same fields
  context:
    venue:
    neutral:
    weather:
    rest_days_home:
    rest_days_away:
    travel_km_away:
    bracket_state:
    home_draw_utility:
    away_draw_utility:
    gd_chase_home:
    gd_chase_away:
  referee:
    name:
    cards_per_match:
    reds_per_match:
    penalties_per_match:
    strictness_uncertainty:
  market:
    home_odds:
    draw_odds:
    away_odds:
    total_line:
    handicap_line:
    odds_timestamp:
  confidence_caps:
    missing_fields: []
    max_confidence:
```

---

## 3. Uncertainty propagation

Do not run simulation from one fixed xG estimate. Sample the input assumptions.

Example:

```text
home_xg ~ Normal(mean_home_xg, uncertainty_home_xg)
away_xg ~ Normal(mean_away_xg, uncertainty_away_xg)
ref_cards ~ Normal(ref_avg_cards, ref_uncertainty)
lineup_penalty ~ Distribution based on absence confidence
```

If data is weak, widen distributions.

| Data condition | Uncertainty adjustment |
|---|---:|
| official xG available | normal |
| only shot counts available | xG uncertainty +30% |
| only narrative available | xG uncertainty +60% |
| lineup unconfirmed | attack/defense uncertainty +15–25% |
| referee unknown | cards confidence cap 5/10 |
| weather unknown in outdoor match | totals uncertainty +10% |

---

## 4. Goal model

### 4.1 Base goal rate

```text
home_lambda = base_home_attack × away_defense_weakness × context_modifiers
away_lambda = base_away_attack × home_defense_weakness × context_modifiers
```

### 4.2 Context modifiers

```yaml
context_modifiers:
  home_advantage:
  neutral_venue_discount:
  fatigue_modifier:
  weather_modifier:
  bracket_aggression_modifier:
  player_availability_modifier:
  tactical_matchup_modifier:
```

### 4.3 Distribution choice

Use:

- Poisson when match is normal and data is stable.
- Negative binomial when variance is high.
- Mixture model when match has strong branch uncertainty.

```text
if data_quality_tier <= 1:
    use wider negative-binomial distribution
elif tactical_scenarios_are_polarized:
    use mixture distribution
else:
    use Poisson or Dixon-Coles adjusted Poisson
```

---

## 5. Scenario tree engine

Every serious report must create a scenario table before final bets.

```yaml
scenario_tree:
  - scenario: favorite_scores_first_early
    probability:
    home_xg_remaining_modifier:
    away_xg_remaining_modifier:
    corner_modifier:
    card_modifier:
    btts_modifier:
    notes:
  - scenario: underdog_scores_first
    probability:
    favorite_siege_trigger:
    underdog_exit_quality:
    over_goals_modifier:
    corner_modifier:
  - scenario: score_0_0_halftime
    probability:
    urgency_shift:
    draw_modifier:
    under_modifier:
  - scenario: red_card_55_75
    probability:
    affected_team:
    draw_modifier:
    card_decay_modifier:
```

Scenario probabilities must sum to realistic bounds, but branches can overlap in more advanced simulation.

---

## 6. Game-state transition rules

### 6.1 First goal effect

```text
If favorite scores first before 30':
    If GD chase or elite blowout conditions active:
        increase high-margin tail.
    Else:
        reduce favorite corner ceiling and reduce open-game chaos.

If underdog scores first:
    If favorite has wide/set-piece route:
        activate corner siege multiplier.
    If favorite lacks block-breaking tools:
        increase draw/underdog result tail.
```

### 6.2 0-0 halftime effect

```text
If 0-0 at HT and total SOT <= 1:
    reduce over-goals probability.
    increase 0-0, 1-0, 0-1 distribution.
    kill favorite-protection + over combo unless live shot quality improves.
```

### 6.3 Red card effect

```text
If red card at 0-0 between 55' and 75':
    increase draw probability if defending team bunkers.
    reduce post-red card-over probability.
    increase corners for attacking 11v10 team if width remains.
    do not automatically increase goals unless block-breaking quality is high.
```

### 6.4 Late favorite lead

```text
If favorite leads by 1 after 70':
    If draw is enough / bracket safe:
        reduce second goal chase.
    If GD needed:
        keep attacking tail active.
    If opponent has strong transition threat:
        increase BTTS/late equalizer tail.
```

---

## 7. Substitution model

Substitutions should affect xG and control.

```yaml
substitution_profile:
  team:
  expected_sub_window:
    - minute_range: 55-65
      role: attacking_boost | defensive_lock | fresh_runner | set_piece_specialist | midfield_control
      xg_delta:
      corner_delta:
      card_delta:
      confidence:
```

Known patterns:

- elite bench attacker chasing game: +0.20 to +0.60 remaining xG,
- defensive CB after red card: lowers opponent chance quality but increases territorial pressure,
- set-piece specialist chasing game: raises corner quality and set-piece xG,
- injured/limited star: lower starting xG and raise substitution uncertainty.

---

## 8. Cards simulation

Cards should be modeled from fouls, referee, transition exposure, and game state.

```text
expected_cards = referee_baseline × match_tension × transition_frequency × tactical_foul_routes × game_state_modifier
```

Game-state rules:

- trailing frustrated team: card risk up,
- mutual draw utility: card risk can fall if tempo suppressed,
- post-red-card: additional cards often decline because players become cautious,
- late knockout chase: cards and fouls can spike.

Output:

```yaml
cards_output:
  total_cards_mean:
  total_cards_distribution:
  home_cards_mean:
  away_cards_mean:
  red_card_probability:
  highest_card_risk_players: []
```

---

## 9. Corner simulation

Corners need separate engine from goals.

```text
corner_mean = width × crossing × blocked_crosses × opponent_clearance × score_state × underdog_exit_failure
```

Rules:

- possession alone is not enough,
- quick central goals can produce high goals but low corners,
- trailing wide favorite can produce high corners even in a 2-1 match,
- underdog high press can reduce favorite corners by preventing siege.

Output:

```yaml
corner_output:
  home_corners_mean:
  away_corners_mean:
  total_corners_mean:
  over_8_5_probability:
  over_9_5_probability:
  best_team_corner_angle:
  live_trigger:
```

---

## 10. Event-aware possession simulation

Only for Level 4.

Pseudo-process:

```text
for each simulation:
    initialize score, minute, formations, fatigue
    while minute < 90:
        choose possession team based on control/press context
        sample possession type:
            build-up
            transition
            set-piece
            long ball
            recycle
        sample progression success
        if chance created:
            sample shot quality
            sample shot outcome
        if cross blocked:
            sample corner
        if transition/foul trigger:
            sample foul/card
        update fatigue, substitutions, game state
```

This allows corners/cards/goals to emerge from mechanisms instead of independent fixed probabilities.

---

## 11. Calibration outputs

Every simulation run should export:

```yaml
simulation_output:
  match_id:
  model_version:
  runs:
  result_probabilities:
    home:
    draw:
    away:
  goal_distribution:
    over_0_5:
    over_1_5:
    over_2_5:
    over_3_5:
    btts_yes:
  score_distribution:
    top_scores:
      - score:
        probability:
  corner_distribution:
    home_mean:
    away_mean:
    total_mean:
    over_8_5:
    over_9_5:
  cards_distribution:
    total_mean:
    over_3_5:
    over_4_5:
    red_card:
  scenario_contribution:
    favorite_scores_first:
    underdog_scores_first:
    zero_zero_ht:
    red_card:
  uncertainty:
    credible_interval_home_win:
    credible_interval_draw:
    credible_interval_away_win:
  confidence_cap:
  model_notes:
```

---

## 12. Reconciliation rule

If simulation and tactical read disagree by more than 8 percentage points, stop and explain.

```text
Do not average silently.
```

Classify disagreement:

- data weakness,
- tactical uncertainty,
- market disagreement,
- scenario polarization,
- model bug,
- real no-bet situation.

---

## 13. Backtesting requirements

Backtest by market.

| Market | Required metric |
|---|---|
| 1X2 | log loss, Brier score, calibration curve |
| Over/Under | Brier score, threshold accuracy, price sensitivity |
| BTTS | Brier score, false-positive rate |
| Correct score | distribution coverage, not raw accuracy only |
| Corners | mean absolute error, over/under hit rate |
| Cards | mean absolute error, red-card calibration |
| Parlays | bet-construction accuracy, dependency audit |

---

## 14. Implementation pseudocode

```python
def simulate_match(input_sheet, n_runs=50000, seed=42):
    rng = Random(seed)
    outputs = []

    for run in range(n_runs):
        sampled = sample_uncertain_inputs(input_sheet, rng)
        state = initialize_match_state(sampled)

        scenario = sample_pre_match_scenario(sampled, rng)
        apply_scenario_modifiers(state, scenario)

        while state.minute < 90:
            phase = sample_phase(state, rng)
            event = simulate_phase_event(state, phase, rng)
            update_match_state(state, event)

            if should_make_substitution(state, rng):
                sub_event = simulate_substitution(state, rng)
                update_match_state(state, sub_event)

            state.minute += sample_time_increment(event, rng)

        outputs.append(extract_markets(state))

    return aggregate_outputs(outputs)
```

---

## 15. Minimum viable v4 implementation

Start small.

### MVP

1. Use expected goals for both teams.
2. Add draw-floor correction.
3. Add scenario branches:
   - early favorite goal,
   - underdog first goal,
   - 0-0 HT,
   - red card.
4. Output 1X2, totals, BTTS, top scores.
5. Add confidence caps.

### v4.1

1. Separate corners engine.
2. Separate cards engine.
3. Add referee and set-piece fields.

### v4.2

1. Add player availability and substitution model.
2. Add event-data based xT/VAEP features.

### v4.3

1. Add possession-chain simulation.
2. Add tracking-derived compactness/pressing features.

---

## 16. Final operating rule

Simulation is not a decoration at the end of the report.

It must be used as a falsification tool:

```text
If the simulation cannot reproduce the analyst story, either the simulation inputs are wrong, the story is overconfident, or the match has no stable betting edge.
```
