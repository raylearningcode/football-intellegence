# Football Intelligence — Master Operating Guide

**Created:** 2026-06-26  
**Updated:** 2026-06-26  
**Status:** Authoritative workflow for v3.3+  
**Purpose:** explain exactly how to run a football analysis, update data, run simulation, grade predictions, improve the model, and keep team analytics/news current without hallucinating stats or overfitting to one match.

---

## 0. Golden rules

1. **Never guarantee outcomes.** Football is probabilistic.
2. **Never invent missing data.** Unknown official stats stay `null` or `missing_official_stats`.
3. **Latest team news is mandatory.** Before analysis, check current lineups, injuries, suspensions, rotation, and coach quotes.
4. **Separate probability from value.** A likely outcome is not automatically a good bet.
5. **Separate side edge from goals edge.** A team can be safe without goals being safe.
6. **Separate reputation from role.** Famous players are not automatically the finisher.
7. **Separate possession from threat.** Possession must become shots, box entries, set pieces, or transition risk.
8. **No Tier 1 pick without data.** Tier 1 requires strong evidence, scenario survival, market edge, and no major contradiction.
9. **Post-match learning must classify error type.** Do not create new rules from random variance.
10. **Every dataset field needs source provenance.** Especially xG, corners, cards, and event data.

---

## 1. File reading order

Before any serious match analysis, read files in this order:

```text
1. README.md
2. football-intelligence/OPERATING_GUIDE.md
3. football-intelligence/SKILL.md
4. football-intelligence/references/calibration-log.md
5. football-intelligence/references/analysis-workflow-v4.md
6. football-intelligence/templates/match-analysis-template-v4.md
7. football-intelligence/references/latest-team-news-protocol-v1.md
8. football-intelligence/references/team-analytics-data-requirements-v1.md
9. football-intelligence/data/world-cup-2026/team-analytics-status-20260626.yaml
```

Required model-improvement files:

```text
football-intelligence/references/h2h-patterns.md
football-intelligence/references/league-profiles.md
football-intelligence/references/match-research-protocol.md
football-intelligence/references/event-data-source-integration-plan.md
football-intelligence/references/event-data-schema-v1.md
football-intelligence/references/monte-carlo-simulation-v4.md
football-intelligence/references/model-validation-and-calibration-v1.md
football-intelligence/references/feature-registry-v1.yaml
```

For World Cup 2026 analysis, also read:

```text
football-intelligence/data/world-cup-2026/data-quality-audit-20260623.md
football-intelligence/data/world-cup-2026/data-fill-log-20260626.md
football-intelligence/data/world-cup-2026/matches-md1-md2-through-20260623.yaml
football-intelligence/data/world-cup-2026/matches-md3-through-20260626-partial.yaml
football-intelligence/data/world-cup-2026/latest-team-news/README.md
football-intelligence/references/world-cup-2026-match-ledger.md
football-intelligence/profiles/world-cup-2026/team-index.md
football-intelligence/profiles/world-cup-2026/team-profiles.md
football-intelligence/profiles/world-cup-2026/coach-watchlist.md
football-intelligence/profiles/world-cup-2026/player-watchlist.md
football-intelligence/profiles/world-cup-2026/profile-update-rules.md
```

If required startup files cannot be read, confidence is capped at **5/10**.

---

## 2. Analysis workflow overview

Every serious prediction follows this sequence:

```text
A. Startup calibration
B. Team analytics status check
C. Latest team-news search
D. Data collection and source grading
E. Bracket and motivation verification
F. Coach gameplan diagnosis
G. Tactical four-phase map
H. Player movement audit
I. 16-dimension scoring
J. Market-specific submodels
K. Scenario tree
L. Monte Carlo v4 validation
M. Betting tier classification
N. Bet construction audit
O. Final report
P. Post-match reconciliation after result
```

Do not skip steps to jump straight to a bet.

---

## 3. A — Startup calibration

Before writing any prediction:

```text
1. Identify current model version.
2. Read latest calibration log.
3. Read latest postmortem addenda.
4. Check active rules and known weak markets.
5. Check if the match belongs to a competition with special baselines.
6. Check if requested market has historically weak calibration.
```

Output internally or in the report:

```text
Model version:
Active rules checked:
Known weak market(s):
Confidence caps before analysis:
```

---

## 4. B — Team analytics status check

Before live web research, check the team status file:

```text
football-intelligence/data/world-cup-2026/team-analytics-status-20260626.yaml
```

For each team, inspect:

```text
group record
qualification status
analytics status
latest news priority
missing xG/event/stat fields
confidence caps
```

If advanced stats are missing, do not act as if they are known. Say:

```text
xG/shot-quality not verified; goals confidence capped at 6.5/10.
```

---

## 5. C — Latest team-news search

Before any analysis, run a current news pass using:

```text
football-intelligence/references/latest-team-news-protocol-v1.md
```

Search order:

```text
1. official team/federation or competition match centre
2. Reuters/AP/BBC/Guardian/ESPN current preview or lineup report
3. trusted local beat reporters
4. official social media
5. secondary injury/suspension aggregators
```

Collect:

```text
confirmed lineup
injuries
suspensions
rotation risk
players protected from yellow-card suspension
coach quotes
formation/tactical hints
weather/venue updates
odds movement after team news if betting requested
```

If no current news is checked, overall confidence is capped at **6/10**.

If news affects future analysis, save a cache file under:

```text
football-intelligence/data/world-cup-2026/latest-team-news/
```

---

## 6. D — Data collection and source grading

Every claim should have an evidence grade.

| Grade | Meaning | Model use |
|---|---|---|
| A | Official/current/direct | Strong probability movement |
| B | Current trusted indirect | Moderate probability movement |
| C | Historical but relevant | Small/moderate modifier |
| D | Weak assumption/reputation | Mention only |
| X | Unknown/unverified | State uncertainty and cap confidence |

Required data:

```text
match identity
competition and stage
venue/weather/referee
current standings and bracket state
latest team news
last 5 and last 10 results
xG/xGA and shot quality if verified
lineups, injuries, suspensions, rotation risk
rest days and travel
odds and market lines
team corner/cross data
team fouls/cards/referee data
player role and movement data
```

If unavailable:

```text
Unavailable: [field]
Confidence impact: [cap/reduction]
```

---

## 7. E — Bracket and motivation verification

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

## 8. F — Coach gameplan diagnosis

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

A tactical plan without a tradeoff is incomplete.

---

## 9. G — Tactical four-phase map

Analyze four phases:

```text
Team A in possession
Team B in possession
Team A out of possession
Team B out of possession
```

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
defensive block
weak zone
set-piece defense
transition defense
rest defense
```

---

## 10. H — Player movement audit

For each team:

```text
actual finisher(s)
creator(s)
chaos player(s)
set-piece taker(s)
box runners
wide/crossing players
players likely to be fouled
players likely to foul
substitution impact players
```

Key rule:

```text
Most dangerous player ≠ most likely scorer.
```

---

## 11. I — 16-dimension scoring

Score the match using the weighted framework, but do not treat the table as mechanical truth.

Current principle:

```text
Composite score informs the model.
Scenario tree and market-specific logic decide the bet.
```

Every score needs a reason and evidence grade.

---

## 12. J — Market-specific submodels

### Side / 1X2 / DNB

Ask:

```text
Who controls risk?
Who has midfield control?
Who has defensive structure?
Who can accept a draw?
Who is emotionally volatile?
Is home advantage structural or just crowd energy?
```

### Goals

Ask:

```text
Do both teams have repeatable scoring routes?
Is the favorite likely to chase margin?
Can the underdog produce shots, not just counters in theory?
Does 0-0 HT kill the over?
```

### BTTS

BTTS requires both sides to have real scoring mechanisms.

### Corners

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

### Cards

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

### Player props

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

## 13. K — Scenario tree

Every full report must test at least:

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

## 14. L — Monte Carlo v4 validation

Use:

```text
football-intelligence/references/monte-carlo-simulation-v4.md
```

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

## 15. M — Betting tier classification

| Tier | Meaning | Requirements |
|---|---|---|
| Tier 1 | Core pick | A/B evidence, scenario survival, market edge, no major contradiction |
| Tier 2 | Lean | good logic but incomplete data or price sensitivity |
| Tier 3 | Live only | depends on early tempo, lineups, first goal, or tactical reveal |
| No bet | no stable edge | market efficient, assumptions conflict, or data too weak |

No bet is valid.

---

## 16. N — Bet construction audit

Before combining legs:

```text
Does each leg have independent support?
Are legs dependent on the same fragile assumption?
Does the added leg create an unpriced failure mode?
Is straight DNB/1X better than combo?
Does mutual draw utility hurt over-goals legs?
Is the payout increase worth the added failure path?
```

Do not attach Over 1.5 / Over 2.5 to a favorite-protection leg unless the goals-combo gate passes.

---

## 17. O — Final report structure

Use:

```text
1. Match header
2. Data quality summary
3. Latest team-news summary
4. Bracket state
5. Coach gameplan read
6. Tactical four-phase map
7. Player movement audit
8. 16-dimension score table
9. Scenario tree
10. Monte Carlo validation
11. Market-specific analysis
12. Betting tier table
13. Bet construction audit
14. Biggest prediction killers
15. Final verdict
16. Self-audit checklist
```

---

## 18. P — Post-match reconciliation

After the match:

```text
1. Create/update reconciliation file using templates/post-match-reconciliation-template.yaml.
2. Fill official facts only from trusted sources.
3. Grade every recommended market.
4. Classify error using calibration-error-taxonomy.md.
5. Update team/player/coach profiles only if mechanism is repeatable.
6. Update calibration only if the rule would have helped before the match.
7. Update model accuracy tables and confidence calibration.
```

Do not create a new rule from one freak event.

---

## 19. Data update workflow

When filling missing data:

```text
1. Search official source first.
2. Search trusted match-centre/stat sources second.
3. Use Reuters/AP/BBC/Guardian/ESPN only for narrative/event mechanism unless stats are explicitly listed.
4. Store source provenance.
5. Mark conflict if sources disagree.
6. Leave unknown fields null.
7. Add data-fill log explaining what changed.
8. Update team-analytics-status file if the team's readiness changes.
```

Never overwrite a structured dataset with unsourced values.

---

## 20. Team analytics update workflow

When building team profiles:

```text
1. Check team-analytics-status file.
2. Fill group record and qualification status from standings.
3. Fill advanced fields only from verified provider.
4. Add latest-news cache for upcoming matches.
5. Update player/coach/team profiles only from repeatable mechanisms.
6. Mark analytics readiness tier.
```

Required source-backed fields before high-confidence analytics:

```text
xG/xGA
shots/SOT
corners/crosses
cards/fouls/referee
lineups/substitutions
player roles/minutes
latest injuries/suspensions
odds/market price if betting value is requested
```

---

## 21. Validation workflow

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

## 22. Required final self-check

Before sending or committing analysis:

```text
[ ] Calibration and latest addenda checked
[ ] Team analytics status checked
[ ] Latest team news checked
[ ] Bracket/standings verified
[ ] Missing data stated clearly
[ ] Side, goals, BTTS, corners, cards, props separated
[ ] Scenario tree completed
[ ] Monte Carlo done or cap stated
[ ] Bet construction audited
[ ] No fake xG/stat data used
[ ] Confidence matches evidence quality
[ ] Post-match update path defined
```

---

## 23. One-line operating philosophy

The system should not ask only **who is better**. It should ask:

```text
What game state benefits each team, what mechanism creates the market outcome, what has changed in latest team news, and what evidence would prove the model wrong?
```
