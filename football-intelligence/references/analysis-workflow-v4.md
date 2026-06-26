# Football Intelligence — Step-by-Step Analysis Workflow v4

**Created:** 2026-06-26  
**Supersedes:** `analysis-workflow-v3.md` for new analyses  
**Use together with:** `football-intelligence/OPERATING_GUIDE.md` and `templates/match-analysis-template-v4.md`

---

## 0. Purpose

This workflow makes every football prediction:

- repeatable,
- evidence-graded,
- data-quality aware,
- scenario-tested,
- simulation-checked,
- market-specific,
- and post-match learnable.

The workflow is designed to prevent the model's known failure modes:

```text
possession mistaken for threat
favorite side edge mistaken for goals edge
home emotion mistaken for control
corners projected from scoreline instead of mechanism
cards projected without referee/foul route
player props picked from fame instead of role
post-match rules created from variance
```

---

## 1. Mandatory startup sequence

Before every full match analysis:

```text
1. Read football-intelligence/OPERATING_GUIDE.md
2. Read references/calibration-log.md
3. Read latest calibration addenda / postmortems
4. Read references/h2h-patterns.md
5. Read references/league-profiles.md
6. Read references/match-research-protocol.md
7. Read references/monte-carlo-simulation-v4.md
8. Read references/model-validation-and-calibration-v1.md
9. Use templates/match-analysis-template-v4.md as the report structure
```

For World Cup 2026:

```text
10. Read data/world-cup-2026/data-quality-audit-20260623.md
11. Read data/world-cup-2026/data-fill-log-20260626.md
12. Read latest matches YAML files
13. Read profiles/world-cup-2026/team, coach, and player files
```

If startup files cannot be read, confidence cap is **5/10**.

---

## 2. Build the evidence table first

Before analysis, create a data quality table.

| Category | Needed? | Found? | Source grade | Confidence impact |
|---|---|---|---|---|
| Official score/fixture | yes |  |  |  |
| Standings/bracket | yes |  |  |  |
| Lineups/injuries | yes |  |  |  |
| xG/shot quality | yes |  |  |  |
| Referee | market-dependent |  |  |  |
| Corners/crosses | market-dependent |  |  |  |
| Fouls/cards | market-dependent |  |  |  |
| Odds/market price | yes for betting |  |  |  |
| Weather/venue | yes |  |  |  |
| Player role/movement | yes for props |  |  |  |

Evidence grades:

```text
A = official/current/direct
B = trusted current indirect
C = historical but relevant
D = weak assumption/reputation
X = unknown/unverified
```

Unknown data must be visible in the report.

---

## 3. Apply confidence caps immediately

Use this before betting recommendations:

| Missing data | Confidence cap |
|---|---:|
| bracket/standings unknown in tournament | 5/10 |
| lineups unknown for player props | 5/10 |
| referee unknown for cards | 5/10 |
| corners/crosses unknown for corners | 5/10 |
| xG/shot quality unknown for goals | 6.5/10 |
| odds unavailable for value-bet call | 6/10 |
| simulation not run | 6/10 |
| correct score market | 4/10 |

Caps can only go lower, not higher, unless missing data is verified.

---

## 4. Bracket and incentive check

For tournaments, answer:

```text
Current points:
Current GD:
Remaining fixtures:
Can Team A accept draw?
Can Team B accept draw?
Does GD matter?
Does third-place qualification matter?
Who needs risk?
Who benefits from control?
```

Then translate motivation into behavior:

```text
Higher press?
Deeper block?
Earlier substitutions?
Riskier fullbacks?
Time management?
Goal-difference chase?
Rotation?
```

A motivation claim that does not change expected behavior should not move probabilities.

---

## 5. Coach gameplan read

Complete this before probabilities:

```text
Team A objective:
Team A likely plan:
Team A biggest fear:
Team A tradeoff:

Team B objective:
Team B likely plan:
Team B biggest fear:
Team B tradeoff:
```

Example tradeoffs:

- High press creates chances but opens space behind.
- Deep block protects the box but concedes territory/corners.
- Wide crossing creates corners but may be low-xG.
- Possession control lowers chaos but can become sterile.

---

## 6. Tactical four-phase map

Map:

```text
Team A in possession
Team B in possession
Team A out of possession
Team B out of possession
```

For each possession phase:

```text
build-up shape
progression route
creator
finisher
set-piece route
opponent answer
failure mode
```

For each defensive phase:

```text
press height
block shape
weak zone
rest defense
set-piece defense
transition defense
```

Do not write `will dominate possession` as if that is enough. Convert it into threat.

---

## 7. Player role and movement audit

For each team, identify:

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

Use this rule:

```text
No verified role = no high-confidence player prop.
```

---

## 8. 16-dimension scoring

Score 0–100 with evidence grades.

| Dimension | Team A | Team B | Edge | Evidence grade | Notes |
|---|---:|---:|---|---|---|
| Current form |  |  |  |  |  |
| H2H |  |  |  |  |  |
| Venue/home |  |  |  |  |  |
| Player availability |  |  |  |  |  |
| Chemistry |  |  |  |  |  |
| Tactical matchup |  |  |  |  |  |
| Manager |  |  |  |  |  |
| Motivation/bracket |  |  |  |  |  |
| Fatigue |  |  |  |  |  |
| Referee |  |  |  |  |  |
| Weather |  |  |  |  |  |
| Advanced metrics |  |  |  |  |  |
| Market |  |  |  |  |  |
| News/sentiment |  |  |  |  |  |

The table is an input, not the final answer.

---

## 9. Market-specific gates

### Side / protected side gate

A side pick passes only if it answers:

```text
Who has structure/control?
Who has midfield stability?
Who has less transition exposure?
Who can accept draw?
Who is less emotionally volatile?
Does market price leave edge?
```

### Goals gate

A goals pick passes only if it answers:

```text
What are the repeatable scoring routes?
What happens at 0-0 HT?
Does bracket state support aggression?
Does one team kill tempo?
Is total line inflated?
```

### BTTS gate

BTTS requires both teams to generate real shots, not only theoretical counters.

### Corners gate

A corner pick passes only if it answers:

```text
wide vs central attack
blocked-cross mechanism
set-piece taker quality
underdog exit quality
first-goal branch risk
team-corner vs total-corner preference
```

### Cards gate

A card pick passes only if it has:

```text
referee profile
foul routes
transition exposure
match tension
player-level card risk
```

### Player prop gate

A player prop passes only if it has:

```text
confirmed/likely minutes
role verification
action route
opponent mismatch
market price edge
```

---

## 10. Scenario tree

Required branches:

| Scenario | 1X2 | Goals | BTTS | Corners | Cards | Live trigger |
|---|---|---|---|---|---|---|
| Favorite scores early |  |  |  |  |  |  |
| Underdog scores first |  |  |  |  |  |  |
| 0-0 HT |  |  |  |  |  |  |
| Favorite leads by one after 70' |  |  |  |  |  |  |
| Draw after 75' |  |  |  |  |  |  |
| Red card 55'–75' |  |  |  |  |  |  |

Tier 1 picks must survive multiple branches.

---

## 11. Monte Carlo v4

Run or conceptually run simulation with:

```text
explicit inputs
uncertainty ranges
scenario branches
score distribution
market outputs
simulation/tactical agreement check
```

Output:

```text
Team A win:
Draw:
Team B win:
Over 1.5:
Over 2.5:
BTTS:
Top score cluster:
Corner range:
Card range:
Simulation confidence cap:
```

If simulation is not run, state it and cap confidence at 6/10.

---

## 12. Betting tier table

| Tier | Market | Probability | Fair odds | Market odds | Edge | Confidence | Reason |
|---|---|---:|---:|---:|---:|---:|---|
| Tier 1 |  |  |  |  |  |  |  |
| Tier 2 |  |  |  |  |  |  |  |
| Tier 3 live-only |  |  |  |  |  |  |  |
| No bet |  |  |  |  |  |  |  |

Do not force a pick.

---

## 13. Bet construction audit

Before recommending a combo/parlay:

```text
Is each leg independently supported?
Do legs depend on the same fragile game script?
Does adding a leg increase unpriced failure risk?
Would straight DNB/1X be better?
Does mutual draw utility kill Over legs?
```

If this audit fails, recommend the straight leg or no bet.

---

## 14. Final report order

Use this order:

```text
1. Header
2. Data quality
3. Bracket state
4. Coach gameplan
5. Tactical four-phase map
6. Player movement audit
7. 16-dimension table
8. Scenario tree
9. Monte Carlo validation
10. Market analysis
11. Betting tier table
12. Bet construction audit
13. Prediction killers
14. Final verdict
15. Self-audit checklist
```

---

## 15. Post-match workflow

After result is known:

```text
1. Fill post-match reconciliation template.
2. Use official/trusted stats only.
3. Grade every market.
4. Classify error type.
5. Decide: no change / update rule / create rule / monitor pattern.
6. Update team/player/coach profiles only from repeatable mechanisms.
7. Update accuracy and calibration tables.
```

Do not update rules from pure variance.

---

## 16. Data fill workflow

When adding data to YAML:

```text
1. Official match centre first.
2. Trusted stat source second.
3. Narrative source only for event mechanism/context.
4. Every field needs source provenance.
5. Conflicts must be marked.
6. Unknowns stay null.
7. Add/update data-fill log.
```

---

## 17. End-state checklist

Before finishing any analysis:

```text
[ ] Data gaps stated
[ ] Bracket state verified
[ ] Coach plan explained
[ ] Tactical four phases mapped
[ ] Player roles separated
[ ] Market-specific gates applied
[ ] Scenario tree done
[ ] Monte Carlo done or cap stated
[ ] Bet construction audited
[ ] No fake stats used
[ ] Confidence matches evidence quality
```
