# Simulation Protocol — Hybrid Football Intelligence Monte Carlo

Purpose: make simulation a required validation layer for match forecasts. The model must translate football evidence into explicit numerical assumptions, run a scenario-weighted simulation, then compare the simulation with the tactical and coach-read analysis.

---

## 0. Core Rule

Every full match forecast should include a simulation section.

Simulation does not replace football judgment. It stress-tests football judgment.

Required workflow:

1. Gather current evidence.
2. Build tactical and coach assumptions.
3. Convert assumptions into numerical inputs.
4. Run repeated match simulations.
5. Compare outputs with the football read.
6. Explain any disagreement.
7. State confidence and uncertainty.

If simulation is not run, the report must say:

`Simulation not run — confidence capped at 6/10.`

---

## 1. Input Sheet

Before running simulation, define the inputs below.

### 1.1 Goal Inputs

- Team A expected goals baseline
- Team B expected goals baseline
- Attack-strength adjustment
- Defensive-strength adjustment
- Lineup adjustment
- Tactical adjustment
- Venue/weather adjustment
- Coach-risk adjustment
- Live-state adjustment if match is already running

### 1.2 Corner Inputs

- Team A expected corners baseline
- Team B expected corners baseline
- Width and crossing mechanism
- Low-block territory modifier
- Early-goal state modifier
- Chasing-team corner modifier
- Central-play penalty
- Live corner pace if available

### 1.3 Discipline Inputs

- Referee strictness
- Match intensity
- Transition frequency
- Frustration risk
- Live foul/card pace if available

---

## 2. Evidence-to-Number Translation

Do not invent numbers without a reason. Every numerical input must be marked as one of:

- Evidence-backed
- Inferred
- Unknown

Examples:

- Deep block against a stronger team: lower shot-conversion expectation, higher territory share for the stronger team.
- Stronger team under public pressure: higher attacking intent, but possible rushed-shot risk.
- Underdog with aerial or set-piece threat: increase underdog scoring tail even if open-play volume is low.
- Stronger team leading early: reduce crossing/corner expectation if the defending block opens.
- Level score near halftime: increase second-half goal expectation, but check whether either team can rationally accept the current state.

Unknown assumptions reduce final confidence.

---

## 3. Coach and Mentality Modifier

Do not assume that a team becomes passive just because a draw is useful.

Correct interpretation:

- A useful draw reduces reckless risk.
- It does not automatically mean defensive passivity.
- Big teams usually still pursue winning, especially when quality, reputation, or table position demands it.
- Underdogs may defend deep while still countering aggressively.

Coach modifiers should affect:

- Pressing height
- Fullback risk
- Tempo
- Substitution timing
- Late-game aggression
- Whether a team protects a narrow lead or pursues margin

Never write that a team will sit back only because a draw is useful. Require tactical evidence, coach quotes, prior behavior, or live-match behavior.

---

## 4. Base Simulation Method

Minimum simulation size:

- Pre-match: 50,000 runs
- Live match: 100,000 runs preferred

Recommended goal model:

- Poisson or negative-binomial generation
- Adjusted expected goals for each team
- Separate low-event and open-game branches
- Late-goal modifier for elite favorites where supported by evidence

Recommended corner model:

- Poisson or overdispersed Poisson
- Separate team corner means
- Game-state modifiers
- Wider variance when style or live data is incomplete

---

## 5. Scenario-Weighted Simulation

The simulation must include game-state branches, not one static path.

At minimum:

1. Stronger team scores first.
2. Weaker team scores first.
3. Match reaches halftime level.
4. Stronger team leads by one late.
5. Match remains low-event.
6. Match opens into transition exchanges.

Each branch can change:

- Remaining goal expectation
- Corner pace
- Discipline risk
- Final score distribution

---

## 6. Live Simulation Rules

When match is live, update inputs using:

- Current score
- Match minute
- Current cards
- Current corners
- Shots and shots on target if available
- xG if available
- Substitutions, injuries, or red cards
- Reliable field tilt or momentum data

If only score and time are available, state clearly that this is a low-data live simulation.

The live model must reduce remaining time correctly.

---

## 7. Output Format

Simulation output must include:

### Result Probabilities

- Team A win
- Draw
- Team B win

### Goal Distribution

- Probability of 1+ total goals
- Probability of 2+ total goals
- Probability of 3+ total goals
- Probability of 4+ total goals
- Probability both teams score

### Corner Distribution

- Low range
- Central range
- High range
- Team split

### Correct Score Distribution

Top five scores with approximate probabilities.

### Interpretation

- Strongest simulation signal
- Strongest tactical signal
- Consensus read
- Simulation/tactical disagreement
- Main uncertainty

---

## 8. Reconciliation Rule

If simulation and tactical analysis disagree by more than 8 percentage points on a major output, pause and explain why.

Disagreement is useful information. Do not hide it.

---

## 9. Confidence Cap Rules

Cap confidence at:

- 5/10 if no simulation is run.
- 6/10 if simulation has only pre-match assumptions.
- 6.5/10 if live data is limited to score/time only.
- 7/10 if live data includes score, time, corners, cards, and shots.
- 8/10 only if live data includes reliable xG, shot quality, lineups, and game state.

---

## 10. Post-Match Calibration

After the match, log:

- Simulation inputs
- Simulation outputs
- Actual result
- Forecast errors
- Whether the error came from inputs, tactical read, game-state transition, or variance

Update calibration only when the mistake is repeatable, not when it is a one-off event.
