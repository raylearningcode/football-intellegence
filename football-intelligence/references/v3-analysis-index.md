# Football Intelligence v3 — Analysis Module Index

Purpose: define how the expanded v3 framework should be used in every serious match forecast. This file connects the original 16-dimension model with the newer deeper-analysis modules.

---

## Required Reference Order

For every full match analysis, read references in this order:

1. `calibration-log.md`
2. `match-research-protocol.md`
3. `simulation-protocol.md`
4. `manager-profiles.md`
5. `team-player-profile-schema.md`
6. `player-movement-model.md`
7. `game-state-engine.md`
8. `set-piece-model.md`
9. `referee-model.md`
10. `uncertainty-engine.md`
11. `calibration-error-taxonomy.md`
12. `match-stat-log-template.md`
13. `h2h-patterns.md`
14. `league-profiles.md`

The original 16-dimension model remains the backbone. The v3 modules add deeper football realism, player-movement awareness, post-match evidence capture, and anti-blind-spot checks.

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
- Team/player profiles
- Player movement data when available
- Group/table context
- Weather and venue
- Referee
- Set-piece profiles
- Recent xG/shot data
- Match-stat logs from recent games
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

### Phase 3 — Player Movement and Phase-of-Play Map

Use `player-movement-model.md`, `team-player-profile-schema.md`, and the original tactical dimension.

Map:

- Team A in possession
- Team B in possession
- Team A out of possession
- Team B out of possession
- Transition moments
- Set-piece mismatches
- Referee flow effects
- Key player receiving zones
- Key player carry zones
- Actual finishers vs creators
- Wide overloads and corner mechanisms
- Defensive movement weaknesses

Do not confuse formation with role. Do not confuse the most famous player with the actual finisher.

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

### Phase 8 — Post-Match Stat Log

Use `match-stat-log-template.md` before writing calibration lessons.

Capture:

- Possession
- Shots
- Shots on target
- Big chances/xG if available
- Corners
- Fouls/cards
- Offsides
- Goal timeline
- Substitutions
- Player movement notes
- Heatmap/touch-map notes
- Set-piece quality
- Referee flow
- Game-state changes

Never calibrate from scoreline alone.

### Phase 9 — Post-Match Calibration

Use `calibration-error-taxonomy.md`.

Classify errors before changing rules. Do not overfit to random events. Update team and player profiles only when the mechanism appears repeatable.

---

## Required v3 Output Sections

Every serious pre-match report must include:

1. Coach Gameplan Read
2. Team and Player Profile Read
3. Player Movement Audit
4. Tactical Phase Map
5. Set-Piece Audit
6. Referee Flow Read
7. Game-State Sensitivity
8. Simulation Summary
9. Uncertainty Audit
10. Final Forecast

Every serious post-match review must include:

1. Match Stat Log
2. Goal Timeline
3. Team Stats vs Scoreline Check
4. Player Movement Review
5. Game-State Review
6. Set-Piece and Referee Review
7. Simulation Review
8. Calibration Error Classification
9. Team/Player Profile Updates Needed
10. Final Lesson

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
13. Scoreline is not dominance.
14. Formation is not role.
15. Team stats are not player movement.
16. Creator and finisher must be separated.
17. Corner volume requires a mechanism, not just possession.
18. Heatmaps and touch maps override assumed positions when available.

---

## Model Version Note

This index marks the framework's practical transition toward v3.1. The model is now intended to work as:

```text
Calibration Memory
+ 16-Dimension Analysis
+ Match Research Protocol
+ Simulation Protocol
+ Coach Behavior Model
+ Team and Player Profiles
+ Player Movement / Heatmap Model
+ Game-State Engine
+ Set-Piece Model
+ Referee Flow Model
+ Uncertainty Engine
+ Match Stat Log
+ Calibration Error Taxonomy
```

The goal is not to predict every match perfectly. The goal is to produce disciplined, evidence-aware, football-realistic forecasts that improve over time without overfitting.
