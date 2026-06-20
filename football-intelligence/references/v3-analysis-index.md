# Football Intelligence v3 — Analysis Module Index

Purpose: define how the expanded v3 framework should be used in every serious match forecast. This file connects the original 16-dimension model with the newer deeper-analysis modules.

---

## Required Reference Order

For every full match analysis, read references in this order:

1. `calibration-log.md`
2. `match-research-protocol.md`
3. `simulation-protocol.md`
4. `manager-profiles.md`
5. `game-state-engine.md`
6. `set-piece-model.md`
7. `referee-model.md`
8. `uncertainty-engine.md`
9. `calibration-error-taxonomy.md`
10. `h2h-patterns.md`
11. `league-profiles.md`

The original 16-dimension model remains the backbone. The v3 modules add deeper football realism and anti-blind-spot checks.

---

## v3 Forecast Workflow

### Phase 0 — Calibration Read

Read calibration rules first. Apply active lessons and confidence caps.

### Phase 1 — Evidence Collection

Collect:

- Current form
- Lineups and availability
- Tactical setup
- Manager context
- Group/table context
- Weather and venue
- Referee
- Set-piece profiles
- Recent xG/shot data
- Market/consensus if relevant

Grade evidence quality using the match research protocol.

### Phase 2 — Coach and Tactical Intent

Use `manager-profiles.md` and `match-research-protocol.md`.

Answer:

- What does each coach want?
- What does each coach fear?
- What result is acceptable?
- What game state is ideal?
- What is the tactical cost of each plan?

Do not assume a useful draw means passivity. Do not assume a must-win situation means reckless attack.

### Phase 3 — Phase-of-Play Map

Use the original tactical dimension plus the v3 modules.

Map:

- Team A in possession
- Team B in possession
- Team A out of possession
- Team B out of possession
- Transition moments
- Set-piece mismatches
- Referee flow effects

### Phase 4 — Game-State Scenario Tree

Use `game-state-engine.md`.

Forecast at minimum:

- Favorite scores first
- Underdog scores first
- Level at halftime
- Favorite leads late
- Red card or substitution shock if relevant

### Phase 5 — Simulation

Use `simulation-protocol.md`.

Translate football assumptions into numerical inputs. Run repeated match simulations when possible. If simulation is not run, state it and cap confidence.

Simulation must produce:

- Result probabilities
- Goal distribution
- Corner distribution
- Correct-score distribution
- Main uncertainty
- Tactical/simulation disagreement

### Phase 6 — Uncertainty Audit

Use `uncertainty-engine.md`.

Separate:

- Estimated probability
- Confidence in the estimate

State:

- Confidence reducers
- Confidence boosters
- No-edge risk
- Data that would change the forecast

### Phase 7 — Final Forecast

Final output should include:

```markdown
## Final Forecast

Result probabilities:
Goal outlook:
Corner outlook:
Correct-score range:
Confidence:
Best supported angles:
Angles to avoid:
Main blind spot:
Best live trigger to update:
```

### Phase 8 — Post-Match Calibration

Use `calibration-error-taxonomy.md`.

Classify errors before changing rules. Do not overfit to random events.

---

## Required v3 Output Sections

Every serious report must include:

1. Coach Gameplan Read
2. Tactical Phase Map
3. Set-Piece Audit
4. Referee Flow Read
5. Game-State Sensitivity
6. Simulation Summary
7. Uncertainty Audit
8. Final Forecast
9. Post-Match Calibration Note if reviewing result

---

## v3 Anti-Blind-Spot Commandments

1. Possession is not goal threat.
2. Motivation is not behavior unless translated tactically.
3. A useful draw does not automatically create passivity.
4. A must-win situation does not automatically create attacking quality.
5. Set pieces are separate from open play.
6. Game state changes volume faster than it changes conversion.
7. Referee style changes match flow.
8. Manager behavior is state-dependent.
9. Probability and confidence are different.
10. No-edge is a valid conclusion.
11. Wrong predictions are not always bad analysis.
12. Do not create new rules from random variance.

---

## Model Version Note

This index marks the framework's practical transition toward v3.0. The model is now intended to work as:

```text
Calibration Memory
+ 16-Dimension Analysis
+ Coach Behavior Model
+ Game-State Engine
+ Set-Piece Model
+ Referee Flow Model
+ Simulation Protocol
+ Uncertainty Engine
+ Calibration Error Taxonomy
```

The goal is not to predict every match perfectly. The goal is to produce disciplined, evidence-aware, football-realistic forecasts that improve over time without overfitting.
