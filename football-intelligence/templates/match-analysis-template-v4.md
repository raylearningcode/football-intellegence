# Match Analysis Template v4

**Use this for every new full match report.**  
This template forces data quality, scenario sensitivity, Monte Carlo validation, and market discipline before any betting recommendation.

---

## 1. Match header

```text
Match:
Competition:
Stage / Group:
Date and kickoff:
Venue:
Neutral venue:
Weather:
Referee:
Model version:
Data quality tier:
```

---

## 2. Data quality summary

| Data category | Status | Source | Confidence impact |
|---|---|---|---|
| Current standings / bracket |  |  |  |
| Recent form |  |  |  |
| xG / shot quality |  |  |  |
| Lineups / absences |  |  |  |
| Referee |  |  |  |
| Weather / venue |  |  |  |
| Odds / market lines |  |  |  |
| Corners / crosses data |  |  |  |
| Cards / fouls data |  |  |  |
| Player movement / roles |  |  |  |

**Confidence cap from missing data:**  
`X/10 because...`

---

## 3. Bracket state / motivation

```text
Team A current points/GD:
Team B current points/GD:
Remaining fixtures:
Does draw help Team A?
Does draw help Team B?
Does GD matter?
Third-place qualification effect:
Expected behavior change:
```

Do not say `must win` unless the table proves it.

---

## 4. Coach gameplan read

```text
Team A coach objective:
Team A likely plan:
Team A biggest fear:
Team A tradeoff:

Team B coach objective:
Team B likely plan:
Team B biggest fear:
Team B tradeoff:
```

---

## 5. Tactical four-phase map

### Team A in possession

- Build-up shape:
- Main progression route:
- Key creator:
- Intended finisher:
- Opponent answer:
- Failure mode:

### Team B in possession

- Build-up shape:
- Main progression route:
- Key creator:
- Intended finisher:
- Opponent answer:
- Failure mode:

### Team A out of possession

- Press height:
- Defensive block:
- Weak zone:
- Set-piece defense:
- Transition defense:

### Team B out of possession

- Press height:
- Defensive block:
- Weak zone:
- Set-piece defense:
- Transition defense:

---

## 6. Player movement audit

```text
Team A key movement patterns:
Team A actual finisher(s):
Team A creator(s):
Team A chaos player(s):
Team A set-piece taker(s):
Team A corner-generation mechanism:
Team A defensive movement weakness:

Team B key movement patterns:
Team B actual finisher(s):
Team B creator(s):
Team B chaos player(s):
Team B set-piece taker(s):
Team B corner-generation mechanism:
Team B defensive movement weakness:
```

Separate reputation from current role.

---

## 7. 16-dimension score table

| Dimension | Weight | Team A | Team B | Edge | Evidence grade | Notes |
|---|---:|---:|---:|---|---|---|
| Current form |  |  |  |  |  |  |
| Tactical matchup |  |  |  |  |  |  |
| Player availability |  |  |  |  |  |  |
| Advanced metrics |  |  |  |  |  |  |
| Home/venue advantage |  |  |  |  |  |  |
| Motivation/bracket |  |  |  |  |  |  |
| Fatigue |  |  |  |  |  |  |
| H2H |  |  |  |  |  |  |
| Team chemistry |  |  |  |  |  |  |
| Manager |  |  |  |  |  |  |
| Referee |  |  |  |  |  |  |
| Market analysis |  |  |  |  |  |  |
| Weather |  |  |  |  |  |  |
| News/sentiment |  |  |  |  |  |  |

---

## 8. Scenario tree

| Scenario | Probability | 1X2 effect | Goals effect | BTTS effect | Corners effect | Cards effect | Best live trigger |
|---|---:|---|---|---|---|---|---|
| Favorite scores first early |  |  |  |  |  |  |  |
| Underdog scores first |  |  |  |  |  |  |  |
| 0-0 at HT |  |  |  |  |  |  |  |
| Favorite leads by one after 70' |  |  |  |  |  |  |  |
| Draw after 75' |  |  |  |  |  |  |  |
| Red card 55'–75' |  |  |  |  |  |  |  |

A Tier 1 bet must survive at least two major scenario branches.

---

## 9. Monte Carlo validation

```yaml
simulation:
  version: monte-carlo-v4
  runs:
  data_quality_tier:
  input_uncertainty:
  result_probabilities:
    team_a_win:
    draw:
    team_b_win:
  goal_distribution:
    over_0_5:
    over_1_5:
    over_2_5:
    over_3_5:
    btts_yes:
  top_scores:
    - score:
      probability:
  corner_distribution:
    team_a_mean:
    team_b_mean:
    total_mean:
    over_8_5:
    over_9_5:
  card_distribution:
    total_mean:
    over_3_5:
    over_4_5:
    red_card_probability:
  simulation_tactical_agreement: strong | moderate | divergent
  divergence_reason:
```

If divergence is greater than 8 percentage points, explain before recommending bets.

---

## 10. Market-specific analysis

### 10.1 Result / side

```text
Model probability:
Market implied probability:
Edge:
Best side market:
Risk:
Recommendation:
```

### 10.2 Goals

```text
Combined xG logic:
Scenario sensitivity:
Over/under line:
Recommendation:
```

### 10.3 BTTS

```text
Team A repeatable scoring route:
Team B repeatable scoring route:
Counter-only warning:
Recommendation:
```

### 10.4 Corners

```text
Wide attack mechanism:
Blocked-cross mechanism:
Underdog exit quality:
First-goal branch risk:
Team-corner vs total-corner preference:
Recommendation:
```

### 10.5 Cards

```text
Referee profile:
Tactical foul routes:
Match tension:
Post-red card adjustment if live:
Recommendation:
```

### 10.6 Player props

```text
Lineup confirmed:
Player role:
Creator vs finisher:
Minutes risk:
Recommendation:
```

---

## 11. Betting tier table

| Tier | Market | Probability | Fair odds | Market odds | Edge | Confidence | Scenario survival | Reason |
|---|---|---:|---:|---:|---:|---:|---|---|
| Tier 1 |  |  |  |  |  |  |  |  |
| Tier 2 |  |  |  |  |  |  |  |  |
| Tier 3 live-only |  |  |  |  |  |  |  |  |
| No bet |  |  |  |  |  |  |  |  |

No bet is valid when the edge is not real.

---

## 12. Bet construction audit

Before combining legs:

```text
Does each leg have independent support?
Are legs relying on the same fragile assumption?
Does adding the leg create an unpriced failure mode?
Would straight DNB/1X be better than combo?
Does total-goal leg survive mutual draw utility?
```

---

## 13. Biggest prediction killers

1. 
2. 
3. 
4. 
5. 

---

## 14. Final report

```text
Win probabilities:
Team A:
Draw:
Team B:

Best score cluster:
Best markets:
Confidence:
Final verdict:
```

Always state uncertainty.

---

## 15. Self-audit checklist

```text
[ ] Calibration log read
[ ] Latest addenda read
[ ] Data quality table completed
[ ] Bracket state verified
[ ] Coach gameplan read completed
[ ] Four-phase tactical map completed
[ ] Player movement roles separated
[ ] 16-dimension score table completed
[ ] Scenario tree completed
[ ] Monte Carlo run or confidence cap stated
[ ] Market edge separated from probability
[ ] Bet construction audited
[ ] Biggest risks listed
[ ] No unsupported Tier 1 pick
```
