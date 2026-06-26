# Model Validation and Calibration Protocol v1

**Created:** 2026-06-26  
**Purpose:** define how Football Intelligence should prove that each model improvement actually improves prediction quality instead of just sounding smarter.

---

## 0. Core principle

A prediction model is only better if it improves out-of-sample probability quality.

Do not judge only by:

- one winning bet,
- one correct score,
- one impressive narrative,
- or one post-match explanation.

Judge by:

- calibration,
- Brier score,
- log loss,
- market-specific accuracy,
- closing-line value,
- and repeatable mechanism detection.

---

## 1. Prediction objects

Every prediction should be stored as structured data.

```yaml
prediction:
  prediction_id:
  match_id:
  created_at:
  kickoff_time:
  model_version:
  data_quality_tier:
  market:
  predicted_probability:
  fair_odds:
  market_odds:
  edge:
  confidence:
  tier: tier1_core | tier2_lean | tier3_live_only | no_bet
  key_assumptions:
  scenario_survival:
    favorite_scores_first:
    underdog_scores_first:
    zero_zero_ht:
    red_card:
  missing_data:
  confidence_cap:
```

---

## 2. Result objects

```yaml
prediction_result:
  prediction_id:
  match_id:
  actual_outcome:
  hit: true|false|push|null
  closing_odds:
  closing_line_value:
  brier_component:
  log_loss_component:
  error_type:
  notes:
```

---

## 3. Required metrics by market

### 3.1 1X2 / protected side

Track:

```text
accuracy
Brier score
multiclass log loss
calibration by probability bucket
protected-side push-adjusted accuracy
closing-line value
```

### 3.2 Goals totals

Track:

```text
Brier score per threshold
Over/Under hit rate
calibration by probability bucket
false over rate
false under rate
```

### 3.3 BTTS

Track:

```text
Brier score
hit rate
false-positive rate
false-negative rate
```

### 3.4 Correct score

Correct score should not be judged only by exact hit rate.

Track:

```text
top_5_score_coverage
actual_score_probability_rank
distribution sharpness
probability assigned to actual score
```

### 3.5 Corners

Track:

```text
team_corner_mean_absolute_error
total_corner_mean_absolute_error
over_under_hit_rate
team_corner_side_accuracy
live_trigger_success_rate
```

### 3.6 Cards

Track:

```text
total_card_mae
over_under_hit_rate
team_card_side_accuracy
red_card_probability_calibration
referee_profile_error
```

### 3.7 Parlays / bet construction

Track separately.

```text
bet_construction_accuracy
leg_dependency_score
unpriced_failure_modes
was_extra_leg_independently_justified
```

A correct side read can still be a bad recommendation if the combination adds a fragile total leg.

---

## 4. Probability buckets

All binary markets must be bucketed.

| Probability bucket | Expected long-run hit rate |
|---|---:|
| 50–55% | 50–55% |
| 56–60% | 56–60% |
| 61–65% | 61–65% |
| 66–70% | 66–70% |
| 71–80% | 71–80% |
| 81%+ | 81%+ and should be rare |

If the 70% bucket hits 55%, the model is overconfident even if the narrative sounds good.

---

## 5. Calibration checks

### 5.1 Brier score

For binary market:

```text
Brier = (predicted_probability - actual_result)^2
```

For 1X2:

```text
Brier = sum((p_i - outcome_i)^2 for i in [home, draw, away])
```

### 5.2 Log loss

```text
LogLoss = -log(probability assigned to actual outcome)
```

Rules:

- Never assign 0% to plausible football outcomes.
- Very confident wrong predictions are punished heavily.
- Correct low-confidence predictions should not be over-rewarded.

### 5.3 Reliability diagram

Every 20–30 predictions per market:

1. group by predicted probability bucket,
2. compute actual hit rate,
3. plot or table predicted vs actual,
4. adjust confidence caps if buckets are inflated.

---

## 6. Backtesting design

### 6.1 No future leakage

Every feature must be timestamped.

Bad:

```text
using season-end xG table before matchday 5
using final standings as team strength
using closing odds if prediction was supposedly made before odds moved
```

Good:

```text
rolling xG before kickoff
pre-match odds timestamped before kickoff
lineups only if prediction created after lineup release
injury report timestamped before kickoff
```

### 6.2 Temporal split

Preferred:

```text
train: older seasons
validate: recent previous season
backtest: latest completed season / tournament phase
```

For tournaments:

```text
train: historical comparable tournaments
calibrate: earlier matches in tournament
test: later matches, with strict pre-match cutoff
```

### 6.3 Walk-forward evaluation

Use walk-forward updates:

```text
before match N:
    train/calibrate only on matches 1..N-1
    predict match N
    after final whistle: grade and update
```

---

## 7. Ablation testing

Every major new module must prove value.

Test model versions:

| Version | Features included |
|---|---|
| Baseline | current 16 dimensions only |
| +Ratings | Elo/FIFA/team strength |
| +Odds | market-implied probabilities |
| +xG | rolling xG/xGA |
| +Events | xT/VAEP/shot map/team style |
| +Context | rest/travel/weather/referee/bracket |
| +Simulation v4 | scenario-weighted Monte Carlo |
| Ensemble | weighted combination |

For each version record:

```yaml
ablation_result:
  version:
  market:
  sample_size:
  accuracy:
  brier:
  log_loss:
  calibration_error:
  roi_if_bet:
  conclusion:
```

---

## 8. Confidence scoring update

Confidence must represent data quality and calibration history, not just analyst conviction.

```text
confidence = base 5.0
+ data completeness
+ source quality
+ scenario robustness
+ historical market calibration
+ tactical clarity
+ market price edge
- missing fields
- fragile first-goal dependency
- poor historical market accuracy
- unverified lineup/referee/player role
```

### 8.1 Maximum confidence caps

| Situation | Max confidence |
|---|---:|
| Missing lineups for player prop | 5/10 |
| Missing referee for card market | 5/10 |
| Missing team-specific corner data | 5/10 |
| Missing xG/shot-quality data for goals | 6.5/10 |
| Missing odds/market price for value bet | 6/10 |
| Simulation not run | 6/10 |
| Simulation and tactical read diverge >8 pts | 6/10 until resolved |
| Correct score market | 4/10 |
| Strong data + robust scenario tree + calibrated market | 8/10 max |

---

## 9. Model-version rules

Every rule update must specify:

```yaml
model_update:
  version:
  date:
  reason:
  affected_markets:
  evidence_matches:
  changed_rules:
  expected_improvement:
  risk_of_overfitting:
  rollback_condition:
```

Do not create a new rule from a one-off event unless it has a repeatable mechanism and would have improved the pre-match read.

---

## 10. Market efficiency and value betting

The model should separate:

```text
true probability estimate
market probability
edge
recommended bet
```

A market can be correctly predicted but have no value.

Example:

```yaml
market_value:
  predicted_probability: 0.62
  implied_probability: 0.60
  edge: 0.02
  recommendation: no_bet
  reason: edge too small after uncertainty and bookmaker margin
```

### 10.1 Edge thresholds

Suggested minimum edge after uncertainty:

| Market | Minimum edge |
|---|---:|
| 1X2 | 4–6 percentage points |
| double chance / DNB | 3–5 percentage points |
| totals | 4–6 percentage points |
| corners | 6–8 percentage points |
| cards | 6–8 percentage points |
| player props | 7–10 percentage points |
| parlays | each leg independently justified |

---

## 11. Post-match review standard

Every post-match review must answer:

1. Was the data correct?
2. Was the tactical read correct?
3. Was the coach behavior read correct?
4. Did game state invalidate the pre-match bet?
5. Did the market already price the edge?
6. Was the miss repeatable or variance?
7. Should a rule change, or should the model simply record noise?

---

## 12. Dashboard fields to track later

```yaml
model_dashboard:
  model_version:
  total_predictions:
  predictions_by_market:
  brier_by_market:
  log_loss_by_market:
  calibration_by_bucket:
  confidence_bucket_accuracy:
  no_bet_accuracy_check:
  strongest_market:
  weakest_market:
  recent_rule_changes:
  rules_helped:
  rules_hurt:
```

---

## 13. Immediate action items

1. Add prediction ledger CSV/YAML.
2. Add calibration bucket table.
3. Add bet-construction metric.
4. Run backtest every 20 completed predictions.
5. Demote any market whose high-confidence bucket underperforms.
6. Keep correct score as distribution summary until top-5 score coverage is proven.

---

## 14. Final rule

Do not confuse a smarter explanation with a better model.

A better model must show better calibrated probabilities over time.
