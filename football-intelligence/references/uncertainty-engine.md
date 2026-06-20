# Uncertainty Engine — Confidence, Error Sources, and No-Edge Detection

Purpose: prevent overconfident forecasts. The model must separate probability from confidence, identify what it does not know, and recognize when the strongest conclusion is that the edge is unclear.

---

## Core Principle

A forecast has two different values:

1. Estimated probability
2. Confidence in that estimate

Example:

- Team A win probability: 68%
- Confidence in estimate: 5.5/10

A high probability can still have low confidence if the inputs are weak, missing, unstable, or contradictory.

---

## Confidence Scale

| Confidence | Meaning |
|---|---|
| 1-3 | Very weak; mostly unknown or chaotic |
| 4-5 | Low; many important inputs missing |
| 6 | Moderate; usable but fragile |
| 7 | Good; multiple independent supports |
| 8 | Strong; high-quality data and tactical agreement |
| 9 | Rare; strong data, clear tactical edge, stable context |
| 10 | Almost never allowed in football |

Football has variance. Do not use 10/10.

---

## Confidence Reducers

Reduce confidence for:

- Unknown lineups
- Unconfirmed injuries
- New coach or new system
- Small sample size
- Missing xG or shot-quality data
- Weak referee information
- Unclear weather/pitch impact
- Conflicting market signals
- High red-card risk
- High goalkeeper-error dependence
- Strong tactical disagreement
- Unclear motivation or bracket incentives
- Low-data live state

---

## Confidence Boosters

Increase confidence only when multiple independent supports align:

- Confirmed lineup matches tactical read
- Recent form and xG agree
- Coach behavior is well known
- Tactical matchup is clear
- Opponent weakness is repeatable
- Market movement supports the read
- Simulation and tactical analysis agree
- Live data confirms pre-match assumption

Never boost confidence from reputation alone.

---

## Probability vs Confidence Template

Every final forecast should include:

```markdown
Estimated probability:
Confidence in probability:
Why confidence is not higher:
What would change the forecast:
Best live data trigger:
```

---

## No-Edge Detection

The model should explicitly allow no-edge conclusions.

Use no-edge when:

- The market or consensus already reflects the model
- Key information is missing
- Multiple outcomes are similarly plausible
- The strongest angle depends on one unstable assumption
- The match is highly game-state dependent
- Simulation and tactical analysis disagree strongly
- Live data is needed before a reliable view exists

No-edge is a successful analytical output. It protects the model from forced predictions.

---

## Uncertainty Buckets

Classify uncertainty by source:

### U1 — Data Uncertainty

Missing or unreliable data: xG, lineups, injuries, referee, weather, live stats.

### U2 — Tactical Uncertainty

Unclear formations, new coach, unexpected player roles, unknown pressing height.

### U3 — Motivation Uncertainty

Unclear whether a team prioritizes margin, control, rotation, or survival.

### U4 — Game-State Uncertainty

Prediction depends heavily on first goal, red card, halftime state, or late substitutions.

### U5 — Variance Uncertainty

Finishing, goalkeeping, deflections, penalties, own goals, and isolated mistakes.

---

## Required Output Section

Every report must include:

```markdown
## Uncertainty Audit

Main uncertainty bucket:
Confidence reducers:
Confidence boosters:
No-edge risk:
What live data would improve confidence:
Final confidence cap:
```

---

## Anti-Blind-Spot Rule

Do not confuse a strong opinion with a strong forecast. A strong forecast requires strong evidence, scenario survival, and calibrated confidence.
