# Game-State Engine — Match Phase and State Transition Model

Purpose: football matches are not static. A prediction must update when the score, minute, cards, substitutions, or tactical incentives change. This engine defines how to think through state transitions rather than treating pre-match probabilities as fixed.

---

## Core Principle

Every match forecast must describe at least four state branches:

1. Level early
2. Favorite scores first
3. Underdog scores first
4. Favorite leads late

Live analysis must update from the actual state, not from the pre-match story.

---

## Match State Variables

Track:

- Score
- Minute
- Cards
- Corners
- Shots and shots on target
- xG if available
- Substitutions
- Injuries
- Field tilt
- Tactical shape changes
- Bracket/table incentives

If key live variables are unavailable, say so and cap confidence.

---

## State 1 — Level Early

Questions:

- Is the favorite creating real chance quality or sterile territory?
- Is the underdog countering with threat or only surviving?
- Is the press sustainable?
- Are wide attacks generating corners or just turnovers?
- Does either coach look satisfied with the tempo?

Model effects:

- No automatic downgrade to favorite unless chance quality is poor.
- Corner expectation rises if favorite territory is sustained.
- Goal expectation depends on shot quality, not possession.

---

## State 2 — Favorite Scores First

Questions:

- Does the favorite keep attacking or shift to control?
- Does the underdog open up or stay damage-limitation?
- Does the defending block dissolve?
- Does the match become transitional?

Possible effects:

- Favorite win probability rises.
- Total goal expectation may rise if the underdog opens up.
- Favorite corner count may fall if the deep block disappears.
- Underdog card risk can rise if chasing.

Do not assume more favorite goals automatically. Check whether the favorite continues producing shots.

---

## State 3 — Underdog Scores First

Questions:

- Can the favorite break a deeper block?
- Does the underdog have defensive quality to absorb pressure?
- Does the favorite become impatient?
- Are counters now more dangerous?

Possible effects:

- Favorite shot and corner volume rises.
- Favorite goal conversion may still be limited by compact defending.
- Cards and tactical fouls can rise.
- Correct-score distribution widens.

---

## State 4 — Level at Halftime

Questions:

- Which coach is more dissatisfied?
- Which bench has better attacking options?
- Is the draw useful to either side?
- Is the first half low-event by design or because of poor execution?

Possible effects:

- Second-half goal probability often rises if the favorite needs the win.
- Under-style reads may weaken if the favorite has strong bench attackers.
- Corner pressure may rise if favorite urgency increases.

---

## State 5 — Favorite Leads by One Late

Questions:

- Is margin important?
- Does the coach prefer possession control or deep protection?
- Can the underdog generate real pressure?
- Are late substitutions defensive or attacking?

Possible effects:

- Result probability stabilizes toward favorite.
- Total goals depend on whether the leader keeps attacking.
- Underdog corners and cards can rise.
- Favorite corners can fall if they stop forcing wide attacks.

---

## State 6 — Red Card

Questions:

- Which team received the red?
- At what minute?
- Was production already happening before the card?
- Does the red affect remaining time only?

Rules:

- Do not retroactively credit the red card for events that occurred before it.
- Apply red-card effects only to the remaining match.
- A red card changes space, fatigue, and substitution logic.

---

## State 7 — Substitution Shock

Questions:

- Is the substitution tactical or injury forced?
- Does it change formation?
- Does it add width, directness, pressing, or defensive control?
- Does it target a known weak zone?

Model effects:

- Attacking subs can raise late xG and shot volume.
- Defensive subs can reduce open play but increase set-piece pressure conceded.
- Fresh wide players can increase corners.

---

## Required Output Section

Every report must include:

```markdown
## Game-State Sensitivity

If favorite scores first:
If underdog scores first:
If level at halftime:
If favorite leads late:
Best live trigger to update:
Main pre-match assumption that could break:
```

---

## Anti-Blind-Spot Rule

Game state changes volume faster than it changes conversion.

A team chasing usually creates more attacks, shots, crosses, fouls, and corners. It does not automatically score more. Defensive execution and shot quality remain separate variables.
