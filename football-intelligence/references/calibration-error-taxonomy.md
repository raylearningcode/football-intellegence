# Calibration Error Taxonomy — Learning Without Overfitting

Purpose: improve post-match learning by classifying why a forecast was wrong. The model should update rules only when the error is repeatable and mechanism-based, not when the result was mostly random variance.

---

## Core Principle

Not every wrong forecast deserves a new rule.

Before updating calibration, identify the error type:

- Bad input
- Bad tactical read
- Bad coach read
- Bad game-state transition
- Bad simulation assumption
- Missing set-piece/referee/weather factor
- Random variance

Only mechanism-based, repeatable errors should change the framework.

---

## Error Categories

### E1 — Input Error

The model used wrong or incomplete information.

Examples:

- Incorrect lineup
- Missed injury
- Wrong formation
- Outdated player role
- Incorrect referee
- Wrong venue/weather context

Fix:

- Improve data collection.
- Do not create tactical rules from bad inputs.

---

### E2 — Tactical Read Error

The model misunderstood how the teams would interact.

Examples:

- Expected high press, but team sat mid-block
- Expected wide buildup, but team played centrally
- Expected compact underdog, but they pressed aggressively
- Expected possession dominance to create chances, but it was sterile

Fix:

- Add tactical mechanism rule if repeated.
- Improve phase-of-play mapping.

---

### E3 — Coach Behavior Error

The model misunderstood coach intent or in-game management.

Examples:

- Assumed useful draw meant passivity
- Assumed favorite would chase margin, but coach protected control
- Assumed trailing team would attack early, but coach waited
- Misread substitution timing

Fix:

- Update manager profile.
- Adjust coach-state modifiers.

---

### E4 — Game-State Transition Error

The pre-match read was reasonable, but the model failed to update after the match state changed.

Examples:

- Early goal collapsed corner volume
- Red card changed tempo
- 0-0 halftime increased favorite urgency
- Underdog goal created siege dynamics
- Favorite lead reduced risk and open-play volume

Fix:

- Update game-state engine.
- Add live trigger rule.

---

### E5 — Set-Piece Error

The model underweighted dead-ball threat or defensive weakness.

Examples:

- Underdog scored from corner despite low open-play xG
- Favorite conceded from repeated wide free kicks
- Goalkeeper spill created rebound goal
- Aerial mismatch was ignored

Fix:

- Update set-piece model.
- Separate open-play xG from set-piece scoring tail.

---

### E6 — Referee/Discipline Error

The model misread how referee style would affect match flow.

Examples:

- Early yellow changed pressing behavior
- Penalty changed goal distribution
- Lenient referee allowed physical disruption
- Strict referee created many free-kick situations

Fix:

- Update referee profile.
- Improve discipline and penalty tail modeling.

---

### E7 — Simulation Assumption Error

The simulation structure was reasonable, but numerical inputs were wrong.

Examples:

- Expected goals too high/low
- Corner mean too high/low
- Wrong variance assumption
- No branch for early goal or red card
- Time decay wrong in live model

Fix:

- Update simulation protocol.
- Recalibrate numerical ranges.

---

### E8 — Market/Consensus Interpretation Error

The model's read was not necessarily wrong, but the value/edge interpretation was wrong.

Examples:

- Correct outcome but poor confidence
- Correct tactical read but price already reflected it
- Chased thin edge in high-variance market
- Forced a pick when no-edge was better

Fix:

- Update uncertainty engine.
- Strengthen no-edge detection.

---

### E9 — Variance / Non-Repeatable Event

The model was reasonable, but football randomness decided the outcome.

Examples:

- Deflected goal
- Goalkeeper mistake
- Own goal
- One-off red card
- Penalty from rare incident
- World-class finish from low xG

Fix:

- Usually no rule update.
- Log as variance.
- Only update if the same mechanism repeats.

---

## Post-Match Review Template

```markdown
## Post-Match Calibration Review

Match:
Predicted result:
Actual result:
Major forecast misses:

### Error Classification
Primary error type:
Secondary error type:
Was this repeatable or random?

### Input Review
Lineup accuracy:
Tactical setup accuracy:
Coach behavior accuracy:
Game-state updates needed:

### Mechanism Lesson
What mechanism did the model miss?
Is this already covered by existing rules?
Should a new rule be created?

### Calibration Action
No change / update existing rule / create new rule / monitor pattern
Reason:
```

---

## Rule Creation Standard

Create a new calibration rule only if:

1. The error has a clear football mechanism.
2. The mechanism is likely to recur.
3. The error is not explained mainly by random variance.
4. Existing rules do not already cover it.
5. The new rule would have improved the forecast before the match, not only in hindsight.

---

## Anti-Overfitting Rule

Do not turn every surprise into a rule. Football contains noise. The goal of calibration is to learn repeatable mechanisms, not chase the last result.
