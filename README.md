# Football Intelligence

A self-improving football (soccer) match prediction and betting-analysis system. This repo is the durable backup of the model's rules, workflow, calibration memory, data schemas, and post-match learning process.

## Current status

**Current operating version: v3.2**

The repository now has an authoritative end-to-end workflow:

```text
football-intelligence/OPERATING_GUIDE.md
```

Use that file first. It explains the proper order for reading files, collecting data, grading evidence, running analysis, applying Monte Carlo simulation, classifying bets, updating data, and doing post-match calibration.

## What's in here

```text
football-intelligence/
├── OPERATING_GUIDE.md                 ← master v3.2 operating workflow
├── SKILL.md                           ← skill instruction wrapper, updated to v3.2
├── references/
│   ├── calibration-log.md             ← model memory: rules, weights, match history
│   ├── calibration-error-taxonomy.md   ← how to classify post-match mistakes
│   ├── h2h-patterns.md                ← recurring tactical/psychological patterns
│   ├── league-profiles.md             ← league/tournament baseline stats
│   ├── match-research-protocol.md     ← anti-blind-spot research discipline
│   ├── analysis-workflow-v4.md         ← current step-by-step analysis workflow
│   ├── analysis-workflow-v3.md         ← older workflow, kept for history
│   ├── event-data-source-integration-plan.md
│   ├── event-data-schema-v1.md
│   ├── monte-carlo-simulation-v4.md
│   ├── model-validation-and-calibration-v1.md
│   └── feature-registry-v1.yaml
├── templates/
│   ├── match-analysis-template-v4.md
│   └── post-match-reconciliation-template.yaml
├── data/
│   └── world-cup-2026/
│       ├── matches-md1-md2-through-20260623.yaml
│       ├── matches-md3-through-20260626-partial.yaml
│       ├── data-quality-audit-20260623.md
│       └── data-fill-log-20260626.md
└── profiles/
    └── world-cup-2026/
        ├── team-index.md
        ├── team-profiles.md
        ├── coach-watchlist.md
        ├── player-watchlist.md
        └── profile-update-rules.md
```

## How to run a proper match analysis

Read files in this order:

```text
1. football-intelligence/OPERATING_GUIDE.md
2. football-intelligence/SKILL.md
3. football-intelligence/references/calibration-log.md
4. latest calibration addenda / postmortems
5. football-intelligence/references/h2h-patterns.md
6. football-intelligence/references/league-profiles.md
7. football-intelligence/references/match-research-protocol.md
8. football-intelligence/references/analysis-workflow-v4.md
9. football-intelligence/references/monte-carlo-simulation-v4.md
10. football-intelligence/references/model-validation-and-calibration-v1.md
11. football-intelligence/references/feature-registry-v1.yaml
12. football-intelligence/templates/match-analysis-template-v4.md
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

Then follow this workflow:

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

Do **not** jump straight to picks.

## Core rules

1. Football is probabilistic. Never guarantee an outcome.
2. Missing official stats must stay missing until verified.
3. Probability and betting value are different.
4. Side edge and goals edge are different.
5. Possession is not goal threat unless it becomes shots, box entries, set pieces, or transition risk.
6. Corners require wide/crossing/blocking mechanisms, not just possession or scoreline.
7. Cards require referee and foul-route data.
8. Player props require lineup/minutes/role confidence.
9. Post-match learning must distinguish model error from random variance.
10. No bet is a valid expert conclusion.

## Confidence caps

| Missing / weak condition | Max confidence |
|---|---:|
| Calibration/startup files unread | 5/10 |
| Bracket state missing in tournament | 5/10 |
| Referee missing for card market | 5/10 |
| Team-specific corner/cross data missing | 5/10 |
| Lineups missing for player props | 5/10 |
| xG/shot-quality missing for goals market | 6.5/10 |
| Odds missing for value-bet claim | 6/10 |
| Simulation not run | 6/10 |
| Correct score market | 4/10 |
| Strong data + robust scenario tree + calibrated market | 8/10 max |

## Data policy

The repo intentionally keeps many World Cup 2026 detailed stat fields as `null` or `missing_official_stats`. Do not fill:

```text
xG
shots
shots on target
possession
corners
cards
fouls
offsides
full lineups
substitutions
referee
weather
```

unless they are verified from official or trusted match-centre/stat-table sources.

News reports may be used for:

```text
score
scorers
goal descriptions
manager quotes
lineup notes
injury notes
tactical mechanism notes
```

but they should not be treated as official stat packs unless the article explicitly provides those stats.

## How to update data

When adding data:

1. Official match centre first.
2. Trusted stat-table source second.
3. Reuters/AP/BBC/Guardian/ESPN-style reports for narrative/event context only unless exact stats are stated.
4. Every field needs source provenance.
5. Conflicts must be marked.
6. Unknowns stay `null`.
7. Add or update a data-fill log.

Use:

```text
football-intelligence/templates/post-match-reconciliation-template.yaml
```

for one match at a time.

## How to improve the model

Model improvement should happen through:

```text
verified event data
better feature schemas
Monte Carlo v4 simulation
Brier score / log loss / calibration buckets
market-specific validation
post-match reconciliation
profile updates from repeatable mechanisms
```

Not through:

```text
invented stats
one-match overreaction
reputation-based assumptions
forcing bets when no edge exists
```

## Why this repo exists

The skill's calibration memory previously broke because updates were written to volatile scratch paths instead of durable skill files. This GitHub repo is the durable source of truth. If a session says a calibration was updated, verify it against this repo.

## Using this elsewhere

For a fresh session, load:

```text
football-intelligence/OPERATING_GUIDE.md
football-intelligence/SKILL.md
football-intelligence/references/calibration-log.md
football-intelligence/references/analysis-workflow-v4.md
football-intelligence/templates/match-analysis-template-v4.md
```

For serious predictions, also load the event-data, simulation, validation, and feature-registry files listed above.
