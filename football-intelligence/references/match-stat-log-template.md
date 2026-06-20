# Match Stat Log Template — Evidence Capture for Post-Match Learning

Purpose: prevent the model from learning from scorelines alone. Every serious post-match review should capture the full statistical and tactical evidence before creating calibration lessons.

---

## Core Principle

The final score is an outcome, not the full story.

A match can be:

- Dominant in score but balanced in shots
- Dominant in possession but sterile in chance quality
- Low-scoring but tactically one-sided
- High-scoring because of finishing variance
- Corner-heavy without real set-piece danger
- Card-heavy because of game state, not referee tendency

Never calibrate from the scoreline alone.

---

## Required Match Log

```markdown
# Match Stat Log

Match:
Competition:
Date:
Final score:
Group/table context:
Pre-match forecast summary:

## Team Stats

| Stat | Team A | Team B |
|---|---:|---:|
| Possession | | |
| Shots | | |
| Shots on target | | |
| Big chances | | |
| xG | | |
| Corners | | |
| Fouls | | |
| Yellow cards | | |
| Red cards | | |
| Offsides | | |
| Saves | | |
| Passes into final third | | |
| Touches in box | | |
| Crosses | | |
| Accurate crosses | | |
| Counterattacks | | |
| Set-piece shots | | |

## Goal Timeline

- Goal 1:
- Goal 2:
- Goal 3:

## Substitutions and Tactical Changes

- Substitution:
- Shape change:
- Impact:

## Player Movement Notes

Team A:
- Main creator:
- Actual finisher:
- Wide overload source:
- Box runners:
- Defensive weak zone:

Team B:
- Main creator:
- Actual finisher:
- Wide overload source:
- Box runners:
- Defensive weak zone:

## Heatmap / Touch Map Notes

- Key player receiving zones:
- Key carry zones:
- Defensive target zones:
- Average-position surprise:
- Movement mismatch:

## Set-Piece Notes

- Corner count:
- Dangerous corners:
- Free-kick danger:
- Aerial mismatch:
- Goalkeeper handling:

## Referee and Discipline Notes

- Foul pattern:
- Yellow-card pattern:
- Penalty/VAR moments:
- Did referee change flow?

## Game-State Review

- Before first goal:
- After first goal:
- Halftime state:
- Late-game state:
- Did game state change volume or conversion?

## Calibration Classification

Primary error type:
Secondary error type:
Repeatable mechanism or variance?
Rule update needed?

## Final Lesson

One-sentence football mechanism:
Evidence supporting it:
Confidence in lesson:
```

---

## Required Post-Match Questions

1. Did the score reflect the chance volume?
2. Did the score reflect chance quality?
3. Was dominance territorial, clinical, transitional, set-piece-based, or opponent-error-based?
4. Did corners come from the predicted mechanism?
5. Did the main creator and actual finisher match pre-match expectations?
6. Did substitutions change the match?
7. Did the referee change tactical behavior?
8. Did the first goal change the match model?
9. Was the forecast wrong, or was the result variance?
10. Should the framework change, or should the result simply be logged?

---

## Anti-Blind-Spot Rule

If team stats, player movement, and scoreline disagree, do not force them into one narrative. Explain the disagreement. The disagreement is often the best lesson.
