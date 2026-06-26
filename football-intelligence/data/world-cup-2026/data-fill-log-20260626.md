# Data Fill Log — 2026-06-26

**Purpose:** record what was filled after the request to add missing data, and what remains intentionally unfilled.

---

## What was added

Created:

```text
football-intelligence/data/world-cup-2026/matches-md3-through-20260626-partial.yaml
```

This file adds newly sourced MD3 data after the existing MD1-MD2 dataset:

- Czechia 0-3 Mexico
- South Africa 1-0 South Korea
- Switzerland 2-1 Canada
- Bosnia and Herzegovina 3-1 Qatar
- Scotland 0-3 Brazil
- Morocco 4-2 Haiti
- Ecuador 2-1 Germany
- Curacao 0-2 Ivory Coast
- Japan 1-1 Sweden
- Tunisia 1-3 Netherlands
- Turkey vs United States lineup/context only
- Paraguay vs Australia lineup/context only

---

## What was filled by category

### Filled where source-supported

- Final score when directly reported by accessible source.
- Venue when source or schedule source identified it clearly.
- Goal scorers and goal minutes when the source explicitly listed them.
- Lineups for matches where Reuters published lineup reports.
- Group-stage context when clearly stated by source.
- Tactical/event notes when clearly described by source.

### Left unfilled

The following fields remain `null` / `missing_official_stats` unless a trusted stat source is later found:

- official xG
- shots
- shots on target
- possession
- corners
- cards
- fouls
- offsides
- full substitutions
- referee
- weather
- complete lineups for all matches
- minute-by-minute event feed

---

## Why not fill everything from memory or assumptions?

The repository's own data policy now says missing stats must not be invented. Some accessible reports provide score/scorer narratives, but not full stat tables. Narrative sources can explain mechanisms; they are not enough for official xG, corners, cards, or fouls.

Therefore, this update improves coverage while preserving data integrity.

---

## Source confidence notes

### High confidence source types used

- Reuters match reports
- Reuters lineup reports
- Guardian live reports when they clearly state final score and events

### Medium confidence source types used

- Major secondary reports such as NY Post or Times of India when Reuters/official stat pages were not found in this pass.

Medium-confidence records should be upgraded later if FIFA, Reuters, ESPN/FotMob, or official match-centre data becomes available.

---

## Immediate next fill tasks

### Priority 1 — final scores still missing in this pass

```text
Turkey vs United States
Paraguay vs Australia
```

Lineups/context were added, but final score was not verified in this pass.

### Priority 2 — upgrade medium-confidence records

```text
Scotland vs Brazil
Ecuador vs Germany
```

Scores and events were found from secondary reports. Upgrade if official/FIFA/Reuters match-centre data is found.

### Priority 3 — official stat pack reconciliation

For every MD3 match, collect:

```yaml
xg:
shots:
shots_on_target:
possession:
corners:
cards:
fouls:
offsides:
lineups:
substitutions:
referee:
weather:
source:
```

Use `templates/post-match-reconciliation-template.yaml` for one match at a time.

---

## Model impact

This data should immediately improve:

- MD3 bracket context
- team form/profile updates
- scorer/player watchlist updates
- event-mechanism calibration
- future Round of 32 match previews

This data should **not yet** be used for:

- official corner calibration
- official card calibration
- xG-based backtesting
- full event-level Monte Carlo

Those require official or trusted stat-table completion.
