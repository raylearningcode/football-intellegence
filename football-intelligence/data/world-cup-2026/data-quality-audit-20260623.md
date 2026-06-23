# World Cup 2026 Data Quality Audit — 2026-06-23

**Scope:** Recheck repository data coverage from MD1 through Jordan 1-2 Algeria.

**Main dataset:** `football-intelligence/data/world-cup-2026/matches-md1-md2-through-20260623.yaml`

---

## Current verified coverage

The repository now has a complete structured match list for all completed World Cup 2026 matches available in the current source set through **Jordan 1-2 Algeria**.

Verified fields for all 44 completed matches:

- game_id
- date in Asia/Taipei
- kickoff time in Asia/Taipei
- group
- teams
- team codes
- final score
- match status
- matchday phase estimate: MD1 / MD2
- reconciliation priority
- stat-completeness status

---

## Honest completeness status

This update completes the **match identity and result ledger**, not the full official stat database.

The following fields are still missing for most matches because they were not available in the verified source set used in this pass:

- referee
- venue
- weather
- halftime score
- goal timestamps and assist mechanisms
- lineups
- substitutions
- xG
- shots
- shots on target
- possession
- corners
- corner times
- cards
- fouls
- offsides
- closing betting lines
- pre-match prediction link
- post-match reconciliation link

These fields must not be guessed. They should be filled only from reliable match-centre or official stat sources.

---

## Data integrity rules

1. **Never invent official stats.** If xG, corners, shots, referee, or cards are unavailable, store `null` or `missing_official_stats`.
2. **Separate verified facts from analytic estimates.** Belgium-Iran includes estimated xG/SOT in the calibration log; official stat reconciliation is still recommended.
3. **Do not treat pattern examples as full match logs.** Many matches are referenced in patterns, but that does not mean their stat packs are complete.
4. **Every match must eventually receive a structured reconciliation record.** Use the YAML schema in the match ledger.
5. **Priority reconciliation first:** fill high-value matches that created or validated calibration rules.

---

## Completion tiers

| Tier | Meaning | Matches currently in this tier |
|---|---|---|
| Tier 0 | Match identity and score only | Most matches |
| Tier 1 | Basic event narrative added | Jordan-Algeria |
| Tier 2 | Basic stats added: shots, SOT, possession, corners, cards | Belgium-Iran partly, but some stats estimated |
| Tier 3 | Full official match-centre stat pack | None confirmed in repo |
| Tier 4 | Full prediction-vs-result calibration with market grading | Belgium-Iran; Jordan-Algeria corner addendum only |

---

## Priority reconciliation list

### Critical

1. Jordan 1-2 Algeria — corner/set-piece siege validation.
2. Belgium 0-0 Iran — red card, post-red card draw, cards, and formation shift validation.
3. Portugal 1-1 DR Congo — possession paradox / underdog bus-park validation.
4. Canada 6-0 Qatar — high-corner siege and blowout mechanism.
5. Netherlands 5-1 Sweden — goals/corners decoupling.
6. Germany 7-1 Curacao — blowout-tail underprojection.
7. Spain 0-0 Cape Verde — favorite draw-floor / possession paradox.
8. Ecuador 0-0 Curacao — draw-floor and low-event calibration.
9. Argentina 3-0 Algeria — Algeria baseline before Jordan comeback.
10. Austria 3-1 Jordan — Jordan baseline before Algeria comeback.
11. Argentina 2-0 Austria — Group J bracket state and Austria baseline.
12. Scotland 0-1 Morocco — low-shot underdog/favorite competence-gap case.
13. Mexico 1-0 South Korea — error-driven decider and low-corner case.

### High

- Brazil 1-1 Morocco
- Netherlands 2-2 Japan
- France 3-1 Senegal
- Iraq 1-4 Norway
- England 4-2 Croatia
- Uruguay 2-2 Cape Verde
- New Zealand 1-3 Egypt
- Norway 3-2 Senegal
- United States 2-0 Australia
- Sweden 5-1 Tunisia
- Belgium 1-1 Egypt
- Iran 2-2 New Zealand

---

## What changed in this pass

Added:

- `data/world-cup-2026/matches-md1-md2-through-20260623.yaml`
- Complete 44-match confirmed score ledger.
- Stat-completeness flags.
- Critical reconciliation priorities.
- Jordan-Algeria verified event notes.

Existing repo files already added in previous pass:

- `references/analysis-workflow-v3.md`
- `references/corner-and-set-piece-rules.md`
- `references/world-cup-2026-match-ledger.md`
- `references/deep-research-improvement-roadmap-20260623.md`
- `references/jordan-algeria-corner-calibration-20260623.md`

---

## Next required step

To truly reach "no missing detail," each match must be reconciled from official or trusted match-centre pages and each record must be upgraded from Tier 0 to Tier 3/Tier 4.

Recommended workflow:

1. Start with Critical list.
2. Fetch official match-centre stats.
3. Fill structured fields in YAML.
4. Create one reconciliation markdown per match.
5. Update calibration-log.md only after official stats are verified.
6. Recalculate market accuracy and confidence calibration after every 5 completed reconciliations.

---

## Important warning

A complete dataset is better than a fake complete dataset. The repo should prefer explicit `missing_official_stats` labels over hallucinated corners, xG, cards, or lineups.
