# Football Intelligence — Step-by-Step Analysis Workflow v3

**Purpose:** Make every match analysis repeatable, auditable, and less vulnerable to blind spots. This workflow converts the repository's 16-dimension framework into a strict operating procedure for pre-match, live, and post-match analysis.

---

## 0. Mandatory startup sequence

Before writing any prediction:

1. Read `references/calibration-log.md`.
2. Read the latest single-match calibration addenda, especially recent failures.
3. Read `references/h2h-patterns.md` for active patterns.
4. Read `references/league-profiles.md` for competition baselines.
5. Read `references/match-research-protocol.md` for evidence discipline.
6. State the current model version and active rule set.

If any of these files cannot be read, confidence is capped at 5/10.

---

## 1. Data collection checklist

For every match, collect and label each item with an evidence grade:

| Grade | Meaning | Example |
|---|---|---|
| A | Direct/current/official | Official lineup, official injury report, official match stats |
| B | Current but indirect | Trusted journalist, market movement, recent tactical trend |
| C | Historical but relevant | 2022+ H2H, coach tendency, recurring tournament pattern |
| D | Weak assumption | Reputation, old data, generic motivation narrative |
| X | Unknown | Not found or not verified |

Required data:

- Match, competition, kickoff, venue, surface, weather.
- Group/bracket table and remaining fixtures.
- Last 5 and last 10 results.
- Expected lineups and confirmed absences.
- Tactical shape in possession and out of possession.
- Coach objective, coach fear, and coach tradeoff for both teams.
- Referee name, average cards, penalty tendency, red-card tendency.
- Market odds: 1X2, double chance, AH, O/U goals, BTTS, corners, cards.
- Advanced metrics: xG, xGA, shots, big chances, PPDA, set-piece xG, crosses, corners.
- Player-prop mechanisms: finisher, creator, fouling target, card-risk player.

If lineups, referee, or market data are missing, do not recommend Tier 1 cards/player-prop bets.

---

## 2. Bracket and motivation logic

For tournaments, never write "must win" until the table proves it.

Document:

1. Current points, GD, GF/GA for both teams.
2. Remaining fixtures.
3. Whether a draw helps either team.
4. Whether GD matters.
5. Whether third-place qualification changes risk appetite.
6. Which team has more urgency.
7. How urgency becomes behavior: higher press, riskier fullbacks, earlier subs, time management, or deep block.

Output:

```text
Bracket State:
Team A needs ... Therefore expected behavior is ...
Team B needs ... Therefore expected behavior is ...
```

---

## 3. Coach-room diagnosis

Before probabilities, write:

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

A tactical claim is incomplete if it only describes upside and not the cost.

---

## 4. Tactical four-phase map

Map four phases:

1. Team A in possession.
2. Team B in possession.
3. Team A out of possession.
4. Team B out of possession.

For each possession phase:

- Build-up shape.
- Main progression route: central, wide, long ball, set-piece, transition.
- Key creator.
- Intended finisher.
- Opponent answer.
- Failure mode.

For each defensive phase:

- Press height.
- Defensive block.
- Weak zone.
- Set-piece defense.
- Transition defense.

Never equate possession with goal threat. Convert possession into shot quality, box entries, set-piece pressure, and transition exposure.

---

## 5. Market-specific submodels

### 5.1 Match result

Use the weighted 16 dimensions, then enforce tournament draw floors where applicable.

Output:

```text
Home win:
Draw:
Away win:
Confidence:
```

### 5.2 Goals

Check:

- Combined xG.
- Finishing quality.
- Defensive quality.
- Game-state incentives.
- First-goal sensitivity.
- Whether both teams need a win.

Do not recommend Over 2.5 if it only wins in one scenario branch.

### 5.3 BTTS

BTTS requires both teams to have a repeatable scoring route. Counter threat alone is not enough unless the underdog can actually generate shots.

### 5.4 Corners

Use the corner-mechanism checklist in `corner-and-set-piece-rules.md`.

Do not build a corner pick from possession alone. Identify:

- Wide attack vs central attack.
- Crossing volume.
- Blocked-cross probability.
- Set-piece taker quality.
- Underdog exit ability.
- Whether a first goal could trigger siege mode.

### 5.5 Cards

Cards require referee profile, match tension, tactical fouling routes, and favorite/underdog strength bias. Without referee data, cap card confidence at 5/10.

### 5.6 Player props

Separate:

- Creator vs finisher.
- Shot taker vs chance creator.
- Fouler vs fouled player.
- Set-piece taker vs open-play creator.

Do not recommend anytime scorer solely because a player is the most famous or most dangerous.

---

## 6. Scenario tree

Every report must include at least these branches:

1. Favorite scores first early.
2. 0-0 at halftime.
3. Underdog scores first.
4. Favorite leads by one after 70 minutes.
5. Draw after 75 minutes.
6. Red card between 55 and 75 minutes.

For each branch, state impact on:

- 1X2.
- O/U goals.
- BTTS.
- Corners.
- Cards.
- Player props.

A bet can be Tier 1 only if it survives at least two major scenario branches and has two Grade A/B supports.

---

## 7. Confidence scoring

Use this structure:

```text
Base confidence = 5.0
+0.5 if official lineups confirmed
+0.5 if referee confirmed and profiled
+0.5 if market movement supports model
+0.5 if tactical mechanism is clear
+0.5 if two independent A/B evidence sources agree
-0.5 if key data missing
-0.5 if market depends on first-goal state
-0.5 if historical calibration is weak for that market
-1.0 if corner/cards/player-prop market lacks mechanism data
```

Market confidence caps:

| Market | Default cap if data incomplete |
|---|---:|
| 1X2 | 7/10 |
| O/U goals | 7/10 |
| BTTS | 6/10 |
| Correct score | 4/10 |
| Corners | 5/10 |
| Cards | 5/10 |
| Player props | 5/10 |

---

## 8. Monte Carlo validation

Run or conceptually simulate 10,000 match states.

Inputs:

- Team strength differential.
- Expected goals.
- Draw floor.
- First-goal probabilities.
- Game-state modifiers.
- Fatigue and availability.
- Corner siege triggers.
- Red-card triggers.

Compare simulation to model. If divergence is greater than 8 percentage points, investigate before finalizing.

---

## 9. Final output structure

Use this order:

1. Match header.
2. Data quality summary.
3. Bracket state.
4. Coach gameplan read.
5. Tactical four-phase map.
6. 16-dimension score table.
7. Scenario tree.
8. Probabilities.
9. Market-specific leans.
10. Betting tier table.
11. Biggest prediction killers.
12. Monte Carlo validation.
13. Final verdict.
14. Self-audit checklist.

---

## 10. Post-match calibration

After every match:

1. Record final score.
2. Record pre-match probabilities.
3. Record actual match stats: xG, shots, SOT, possession, corners, cards, fouls, offsides.
4. Record key events with timestamps.
5. Grade each market.
6. Diagnose whether the miss was data, model, live adjustment, or variance.
7. Add or update rules only if the mechanism is repeatable.
8. Update running accuracy.
9. Add unresolved data gaps.

Post-match entries should not be generic. They must explain exactly what the model learned.
