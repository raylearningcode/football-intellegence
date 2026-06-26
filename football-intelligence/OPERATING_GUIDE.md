# Football Intelligence — Master Operating Guide

**Created:** 2026-06-26  
**Status:** Authoritative workflow for v3.2+  
**Purpose:** explain exactly how to run a football analysis, update data, run simulation, grade predictions, and improve the model without hallucinating stats or overfitting to one match.

---

## 0. Golden rules

1. **Never guarantee outcomes.** Football is probabilistic.
2. **Never invent missing data.** Unknown official stats stay `null` or `missing_official_stats`.
3. **Separate probability from value.** A likely outcome is not automatically a good bet.
4. **Separate side edge from goals edge.** A team can be safe without goals being safe.
5. **Separate reputation from role.** Famous players are not automatically the finisher.
6. **Separate possession from threat.** Possession must become shots, box entries, set pieces, or transition risk.
7. **No Tier 1 pick without data.** Tier 1 requires strong evidence, scenario survival, and no major contradiction.
8. **Post-match learning must classify error type.** Do not create new rules from random variance.

---

## 1. File reading order

Before any serious match analysis, read files in this order.

### Required startup files

```text
1. README.md
2. football-intelligence/OPERATING_GUIDE.md
3. football-intelligence/SKILL.md
4. football-intelligence/references/calibration-log.md
5. football-intelligence/references/analysis-workflow-v3.md
6. football-intelligence/templates/match-analysis-template-v4.md
```

### Required model-improvement files

```text
7. football-intelligence/references/h2h-patterns.md
8. football-intelligence/references/league-profiles.md
9. football-intelligence/references/match-research-protocol.md
10. football-intelligence/references/event-data-source-integration-plan.md
11. football-intelligence/references/event-data-schema-v1.md
12. football-intelligence/references/monte-carlo-simulation-v4.md
13. football-intelligence/references/model-validation-and-calibration-v1.md
14. football-intelligence/references/feature-registry-v1.yaml
```

### Competition-specific files

For World Cup 2026 analysis, also read:

```text
football-intelligence/data/world-cup-2026/data-quality-audit-20260623.md
football-intelligence/data/world-cup-2026/matches-md1-md2-through-20260623.yaml
football-intelligence/data/world-cup-2026/matches-md3-through-20260626-partial.yaml
football-intelligence/data/world-cup-2026/data-fill-log-20260626.md
football-intelligence/references/world-cup-2026-match-ledger.md
football-intelligence/profiles/world-cup-2026/README.md
football-intelligence/profiles/world-cup-2026/team-index.md
football-intelligence/profiles/world-cup-2026/team-profiles.md
football-intelligence/profiles/world-cup-2026/coach-watchlist.md
football-intelligence/profiles/world-cup-2026/player-watchlist.md
football-intelligence/profiles/world-cup-2026/profile-update-rules.md
```

---

## 2. Analysis workflow overview

Every serious prediction follows this sequence:

```text
A. Startup calibration
B. Data collection and source grading
C. Bracket and motivation verification
D. Coach gameplan diagnosis
E. Tactical four-phase map
F. Player movement audit
G. 16-dimension scoring
H. Market-specific submodels
I. Scenario tree
J. Monte Carlo v4 validation
K. Betting tier classification
L. Bet construction audit
M. Final report
N. Post-match reconciliation after result
```

Do not skip steps to jump straight to a bet.

---

## 3. A — Startup calibration

Before writing any prediction:

1. Identify the current model version.
2. Read the latest calibration log.
3. Read the latest postmortem addenda.
4. Check active rules and known weak markets.
5. Check if the match belongs to a competition with special baselines.
6. Check if the requested market has historically weak calibration.

Output this internally or in the report:

```text
Model version:
Active rules checked:
Known weak market(s):
Confidence caps before analysis:
```

If calibration files are missing, cap confidence at **5/10**.

---

## 4. B — Data collection and source grading

Every claim should have an evidence grade.

| Grade | Meaning | Can move model? |
|---|---|---|
| A | Official/current/direct | Strongly |
| B | Current but indirect/trusted | Moderately |
| C | Historical but relevant | Slight/moderate |
| D | Weak assumption/reputation | Mention only |
| X | Unknown/unverified | Must lower confidence |

Required data:

```text
match identity
competition and stage
venue/weather/referee
current standings and bracket state
last 5 and last 10 results
xG/xGA and shot quality if available
lineups, injuries, suspensions, rotation risk
rest days and travel
odds and market lines
team corner/cross data
team fouls/cards/referee data
player role and movement data
```

If data is unavailable, write:

```text
Unavailable: [field]
Confidence impact: [cap/reduction]
```

Do not silently ignore missing fields.

---

## 5. C — Bracket and motivation verification

For tournaments, bracket logic is mandatory.

Document:

```text
Team A points/GD/GF/GA:
Team B points/GD/GF/GA:
Remaining fixtures:
What result does Team A need?
What result does Team B need?
Is a draw good enough for either side?
Does goal difference matter?
Does third-place qualification matter?
Which team has more urgency?
How urgency changes behavior:
```

Motivation must become behavior:

| Motivation | Behavioral translation |
|---|---|
| Must win | higher press, earlier subs, more fullback risk |
| Draw is useful | lower risk, tempo control, fewer reckless bodies forward |
| GD chase | keep attacking after lead, higher late goal/corner tail |
| Already qualified | rotation, reduced risk, game management |
| Eliminated but proud | emotional start, cards, counters, lower structure |

Never say “must win” unless the table proves it.

---

## 6. D — Coach gameplan diagnosis

Before probabilities, write the coach-room read.

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

A tactical plan without a tradeoff is incomplete.

---

## 7. E — Tactical four-phase map

Analyze four phases:

1. Team A in possession.
2. Team B in possession.
3. Team A out of possession.
4. Team B out of possession.

For possession phases:

```text
build-up shape
progression route
key creator
intended finisher
set-piece route
opponent answer
failure mode
```

For defensive phases:

```text
press height
defensive block
weak zone
set-piece defense
transition defense
```

---

## 8. F — Player movement audit

The model must learn players, not just teams.

For each team:

```text
actual finisher(s):
creator(s):
chaos player(s):
set-piece taker(s):
box runners:
wide/crossing players:
players likely to be fouled:
players likely to foul:
substitution impact players:
```

Key rule:

```text
Most dangerous player ≠ most likely scorer.
```

Use heatmaps/touch maps if available. If unavailable, lower player-prop confidence.

---

## 9. G — 16-dimension scoring

Score the match using the weighted framework, but do not treat the score table as mechanical truth.

Current v3.2 principle:

```text
Composite score informs the model.
Scenario tree and market-specific logic decide the bet.
```

Required dimensions:

```text
Current form
Head-to-head
Home/venue advantage
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
Live match state if applicable
```

Every score needs a reason and evidence grade.

---

## 10. H — Market-specific submodels

### 10.1 Side / 1X2 / DNB

Ask:

```text
Who controls risk?
Who has midfield control?
Who has defensive structure?
Who can accept a draw?
Who is emotionally volatile?
Is home advantage structural or just crowd energy?
```

Do not mark a protected side safe unless it wins the structure-control checklist.

### 10.2 Goals

Ask:

```text
Do both teams have repeatable scoring routes?
Is the favorite likely to chase margin?
Can the underdog produce shots, not just counters in theory?
Does 0-0 HT kill the over?
```

### 10.3 BTTS

BTTS requires both sides to have real scoring mechanisms.

Counter threat alone is not enough unless it can generate shots.

### 10.4 Corners

Use corner-specific logic:

```text
wide attack or central attack?
blocked crosses?
set-piece taker quality?
underdog exit quality?
what happens if underdog scores first?
what happens if favorite scores first?
```

No Tier 1 corner pick without team-specific corner/cross data.

### 10.5 Cards

Cards require:

```text
referee profile
team fouls/cards profile
transition exposure
duel intensity
frustration path
post-red-card discount if live
```

No Tier 1 card pick without referee data.

### 10.6 Player props

Player props require:

```text
confirmed lineup
minutes projection
role verification
shot/key-pass/foul route
opponent matchup
```

No Tier 1 player prop without lineup confirmation.

---

## 11. I — Scenario tree

Every full report must test at least these scenarios:

```text
favorite scores first early
underdog scores first
0-0 at halftime
favorite leads by one after 70'
draw after 75'
red card between 55' and 75'
```

For each scenario, state impact on:

```text
1X2
goals
BTTS
corners
cards
player props
```

A Tier 1 bet must survive at least two major scenario branches.

---

## 12. J — Monte Carlo v4 validation

Use `references/monte-carlo-simulation-v4.md`.

Minimum requirements:

```text
run or conceptually simulate with explicit inputs
include uncertainty ranges
include scenario branches
output 1X2, totals, BTTS, score distribution
explain divergence from tactical read
```

If simulation is not run:

```text
Simulation not run — confidence capped at 6/10.
```

If simulation and tactical read differ by more than 8 percentage points:

```text
Pause. Explain the disagreement. Do not average silently.
```

---

## 13. K — Betting tier classification

| Tier | Meaning | Requirements |
|---|---|---|
| Tier 1 | Core pick | A/B evidence, scenario survival, market edge, no major contradiction |
| Tier 2 | Lean | good logic but incomplete data or price sensitivity |
| Tier 3 | Live only | depends on early tempo, lineups, first goal, or tactical reveal |
| No bet | no stable edge | market efficient, assumptions conflict, or data too weak |

No bet is a valid expert conclusion.

---

## 14. L — Bet construction audit

Before combining legs, answer:

```text
Does each leg have independent support?
Are legs dependent on the same fragile assumption?
Does the added leg create an unpriced failure mode?
Is straight DNB/1X better than combo?
Does mutual draw utility hurt over-goals legs?
Is the payout increase worth the added failure path?
```

Hard rule:

```text
Do not attach Over 1.5 / Over 2.5 to a favorite-protection leg unless the goals-combo gate passes.
```

---

## 15. M — Final report structure

Use this order:

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

The best report is not the longest. It is the clearest and most auditable.

---

## 16. N — Post-match reconciliation

After the match:

1. Create or update a reconciliation file using `templates/post-match-reconciliation-template.yaml`.
2. Fill official facts only from trusted sources.
3. Grade every recommended market.
4. Classify the error using `calibration-error-taxonomy.md`.
5. Update team/player/coach profiles only if the mechanism is repeatable.
6. Update calibration only if the new rule would have helped before the match.
7. Update model accuracy tables and confidence calibration.

Do not create a new rule from one freak event.

---

## 17. Data update workflow

When filling missing data:

```text
1. Search official source first.
2. Search trusted match-centre/stat sources second.
3. Use Reuters/AP/BBC/Guardian/ESPN only for narrative/event mechanism unless stats are explicitly listed.
4. Store source provenance.
5. Mark conflict if sources disagree.
6. Leave unknown fields null.
7. Add data-fill log explaining what changed.
```

Never overwrite a structured dataset with unsourced values.

---

## 18. Profile update workflow

Update profiles only when:

```text
team mechanism repeats
player role is verified by lineup/heatmap/events
coach behavior repeats in similar game state
stat profile supports visual/tactical read
```

Do not update strongly from:

```text
one deflection
one red card
one goalkeeper error
one penalty
one opponent collapse
scoreline only
```

---

## 19. Validation workflow

Every 20–30 predictions per market:

```text
calculate Brier score
calculate log loss
bucket predicted probabilities
compare predicted vs actual hit rate
track confidence bucket accuracy
track closing-line value if odds exist
track bet construction quality
```

A model that sounds smarter but has worse calibration is not improved.

---

## 20. Required final self-check

Before sending or committing any analysis, check:

```text
[ ] Read calibration and latest addenda
[ ] Verified bracket/standings
[ ] Marked missing data clearly
[ ] Separated side, goals, BTTS, corners, cards, props
[ ] Built scenario tree
[ ] Ran or capped Monte Carlo
[ ] Audited bet construction
[ ] Avoided fake stats
[ ] Gave confidence based on evidence, not vibes
[ ] Wrote post-match update path
```

---

## 21. One-line operating philosophy

The system should not ask only **who is better**. It should ask:

```text
What game state benefits each team, what mechanism creates the market outcome, and what evidence would prove the model wrong?
```
