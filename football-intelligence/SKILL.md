---
name: football-intelligence
description: >
  Elite football match prediction and analysis skill. Use this skill for football/soccer match
  predictions, betting analysis, team form, tactical breakdowns, player availability, match previews,
  live-match reads, post-match reviews, calibration updates, or any request involving "predict",
  "analyze", "who will win", "match preview", "betting tips", or two football teams in a versus/vs
  context. This skill is probabilistic, evidence-graded, source-aware, scenario-tested, and
  self-improving through post-match reconciliation.
---

# Football Intelligence System — v3.2 Operating Skill

**Version:** v3.2  
**Repository:** https://github.com/raylearningcode/football-intellegence  
**Authoritative workflow:** `football-intelligence/OPERATING_GUIDE.md`  
**Current report template:** `football-intelligence/templates/match-analysis-template-v4.md`

---

## 0. Purpose

Produce probability-based football analysis with disciplined data handling, tactical reasoning, Monte Carlo validation, market-specific logic, and post-match learning.

The model must answer:

```text
What game state benefits each team?
What mechanism creates the market outcome?
What evidence would prove the model wrong?
```

Football is probabilistic. Never guarantee an outcome.

---

## 1. Non-negotiable rules

1. **Never invent missing stats.** If official xG, corners, cards, lineups, fouls, referee, or event data are not verified, mark them as missing.
2. **Never treat possession as goal threat.** Convert possession into shots, box entries, set pieces, field tilt, or transition risk.
3. **Never treat a famous player as the best prop automatically.** Separate creator, finisher, connector, chaos player, fouler, and fouled player.
4. **Never attach an Over leg to a safe side leg without a goals-combo gate.** A protected side and a goals leg are different markets.
5. **Never make Tier 1 cards without referee data.**
6. **Never make Tier 1 corners without team-specific corner/cross/wide-mechanism data.**
7. **Never make Tier 1 player props without lineup/minutes confidence.**
8. **Never create a new calibration rule from pure variance.** Use the error taxonomy.
9. **Always state uncertainty and confidence caps.**
10. **Always keep source provenance for data updates.**

---

## 2. Required file reading order

Before any serious prediction, read or apply these files in order:

```text
1. football-intelligence/OPERATING_GUIDE.md
2. football-intelligence/references/calibration-log.md
3. latest calibration addenda / postmortems
4. football-intelligence/references/h2h-patterns.md
5. football-intelligence/references/league-profiles.md
6. football-intelligence/references/match-research-protocol.md
7. football-intelligence/references/analysis-workflow-v4.md
8. football-intelligence/references/monte-carlo-simulation-v4.md
9. football-intelligence/references/model-validation-and-calibration-v1.md
10. football-intelligence/references/feature-registry-v1.yaml
11. football-intelligence/templates/match-analysis-template-v4.md
```

For World Cup 2026, also read:

```text
football-intelligence/data/world-cup-2026/data-quality-audit-20260623.md
football-intelligence/data/world-cup-2026/data-fill-log-20260626.md
football-intelligence/data/world-cup-2026/matches-md1-md2-through-20260623.yaml
football-intelligence/data/world-cup-2026/matches-md3-through-20260626-partial.yaml
football-intelligence/references/world-cup-2026-match-ledger.md
football-intelligence/profiles/world-cup-2026/team-index.md
football-intelligence/profiles/world-cup-2026/team-profiles.md
football-intelligence/profiles/world-cup-2026/coach-watchlist.md
football-intelligence/profiles/world-cup-2026/player-watchlist.md
```

If these cannot be read, cap confidence at **5/10**.

---

## 3. Standard analysis workflow

Every full match analysis follows this order:

```text
A. Startup calibration
B. Data collection and source grading
C. Bracket and motivation verification
D. Coach gameplan diagnosis
E. Tactical four-phase map
F. Player movement audit
G. 16-dimension score table
H. Market-specific gates
I. Scenario tree
J. Monte Carlo v4 validation
K. Betting tier classification
L. Bet construction audit
M. Final report
N. Post-match reconciliation
```

Do not jump straight to picks.

---

## 4. Evidence grading

Every major claim should be tagged or mentally classified.

| Grade | Meaning | Model use |
|---|---|---|
| A | Official/current/direct | Can move probability strongly |
| B | Current trusted indirect | Can move probability moderately |
| C | Historical but relevant | Small/moderate modifier |
| D | Weak assumption or reputation | Mention only, do not anchor |
| X | Unknown/unverified | State uncertainty and cap confidence |

Required data for full analysis:

```text
match identity, competition, kickoff, venue, weather
standings/bracket and remaining fixtures
last 5 and last 10 form
xG/xGA, shots, shot quality, big chances if available
lineups, injuries, suspensions, rotation risk
tactical shape in and out of possession
coach objective, fear, and tradeoff
referee profile for cards
odds/market lines for value calls
corner/cross data for corners
fouls/cards data for discipline
player role/movement for props
```

---

## 5. Confidence caps

Apply caps before recommending markets.

| Missing / weak condition | Max confidence |
|---|---:|
| Startup/calibration files unread | 5/10 |
| Tournament bracket state missing | 5/10 |
| Referee missing for card market | 5/10 |
| Team-specific corner/cross data missing | 5/10 |
| Lineups missing for player props | 5/10 |
| xG/shot-quality missing for goals market | 6.5/10 |
| Odds missing for value-bet claim | 6/10 |
| Simulation not run | 6/10 |
| Simulation and tactical read diverge >8 pts | 6/10 until explained |
| Correct score market | 4/10 |
| Strong data + robust scenario tree + calibrated market | 8/10 max |

Confidence represents data quality and calibration, not vibes.

---

## 6. Bracket and motivation logic

For tournaments, never write “must win” until the table proves it.

Document:

```text
Current points/GD/GF/GA for both teams
Remaining fixtures
Whether a draw helps either team
Whether GD matters
Third-place qualification impact
Which team has urgency
How urgency changes behavior
```

Motivation must become behavior:

```text
higher press
riskier fullbacks
earlier substitutions
deep block
time management
goal-difference chase
rotation
```

If behavior does not change, the motivation claim should not move the model.

---

## 7. Coach gameplan read

Before probabilities, complete:

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

A plan without a cost is incomplete.

---

## 8. Tactical four-phase map

Analyze:

1. Team A in possession.
2. Team B in possession.
3. Team A out of possession.
4. Team B out of possession.

For possession:

```text
build-up shape
progression route
key creator
intended finisher
set-piece route
opponent answer
failure mode
```

For defense:

```text
press height
block shape
weak zone
set-piece defense
transition defense
rest defense
```

---

## 9. Player movement audit

For each team identify:

```text
actual finisher
creator
connector
chaos player
wide crosser
set-piece taker
late runner
target forward
fouler
fouled player
substitution impact player
```

Use current role, not reputation.

---

## 10. 16-dimension framework

Use the 16 dimensions as an input layer:

```text
Current form
Head-to-head
Venue/home advantage
Player availability
Team chemistry
Tactical matchup
Manager quality
Motivation/bracket context
Fatigue
Referee
Weather
Advanced metrics
Market analysis
News/sentiment
Live state if applicable
```

The composite score informs probabilities, but market-specific logic and scenario testing decide whether a bet exists.

---

## 11. Market-specific gates

### 11.1 Side / 1X2 / DNB

Ask:

```text
Who controls risk?
Who has midfield control?
Who has defensive structure?
Who can accept a draw?
Who is less emotionally volatile?
Does market price leave an edge?
```

Protected side belongs to the structure/control team, not automatically the home/emotional team.

### 11.2 Goals

Ask:

```text
What are the repeatable scoring routes?
Can both teams generate shots?
Does bracket state create aggression or control?
What happens if 0-0 at HT?
Is the line inflated by reputation or previous scoreline?
```

### 11.3 BTTS

BTTS requires both teams to have a repeatable scoring route. Counter threat alone is not enough unless it produces real shots.

### 11.4 Corners

Ask:

```text
wide attack or central attack?
blocked crosses?
set-piece taker quality?
underdog exit quality?
what if underdog scores first?
what if favorite scores first?
team-corners or total-corners?
```

### 11.5 Cards

Ask:

```text
referee strictness
team foul/card rates
transition exposure
duel intensity
frustration path
specific player card risk
```

### 11.6 Player props

Ask:

```text
lineup/minutes confidence
actual role
shot/key-pass/foul route
opponent mismatch
price edge
```

---

## 12. Scenario tree

Every full report must include these branches:

```text
favorite scores first early
underdog scores first
0-0 at halftime
favorite leads by one after 70'
draw after 75'
red card between 55' and 75'
```

For each branch, state impact on:

```text
1X2
goals
BTTS
corners
cards
player props
```

Tier 1 picks must survive at least two major branches.

---

## 13. Monte Carlo v4 validation

Use `references/monte-carlo-simulation-v4.md`.

Minimum output:

```text
Team A win probability
Draw probability
Team B win probability
Over 1.5 / 2.5 / 3.5
BTTS
Top score cluster
Corner range
Card range
Simulation/tactical agreement
Main uncertainty
```

If the model and simulation differ by more than 8 percentage points, explain why before recommending anything.

---

## 14. Betting tiers

| Tier | Meaning |
|---|---|
| Tier 1 | Core pick; strong A/B evidence, scenario survival, market edge |
| Tier 2 | Lean; good logic but incomplete data or price sensitivity |
| Tier 3 | Live-only; depends on early tempo, lineup, first goal, tactical reveal |
| No bet | No stable edge or too many assumptions |

No bet is expert output, not failure.

---

## 15. Bet construction audit

Before any combo/parlay:

```text
Does each leg have independent support?
Do legs rely on the same fragile assumption?
Does the added leg create an unpriced failure mode?
Would straight DNB/1X be better?
Does mutual draw utility damage the over-goals leg?
```

Do not use a safe side leg as an excuse to force a volatile total.

---

## 16. Final report format

Use the v4 template order:

```text
1. Match header
2. Data quality summary
3. Bracket state
4. Coach gameplan read
5. Tactical four-phase map
6. Player movement audit
7. 16-dimension score table
8. Scenario tree
9. Monte Carlo validation
10. Market-specific analysis
11. Betting tier table
12. Bet construction audit
13. Biggest prediction killers
14. Final verdict
15. Self-audit checklist
```

---

## 17. Post-match self-improvement

After the match:

1. Use `templates/post-match-reconciliation-template.yaml`.
2. Fill facts only from official/trusted sources.
3. Grade every recommended market.
4. Classify error using `calibration-error-taxonomy.md`.
5. Update profiles only from repeatable mechanisms.
6. Update calibration only if the rule would have helped pre-match.
7. Update accuracy, Brier/log loss, and confidence buckets when enough samples exist.

---

## 18. Data update workflow

When updating YAML/data files:

```text
official source first
trusted stat-table source second
news/narrative source only for mechanism/context unless exact stats are stated
every field needs source provenance
conflicts must be marked
unknowns stay null
data-fill log must explain what changed
```

---

## 19. Self-audit checklist

Before final answer:

```text
[ ] Calibration checked
[ ] Data gaps stated
[ ] Bracket verified
[ ] Coach plan and tradeoff written
[ ] Tactical four phases mapped
[ ] Player roles separated
[ ] Market gates applied
[ ] Scenario tree completed
[ ] Monte Carlo run or confidence cap stated
[ ] Bet construction audited
[ ] No fake stats used
[ ] Confidence matches evidence quality
```
