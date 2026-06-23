# World Cup 2026 Match Ledger

**Purpose:** Track every completed World Cup 2026 match that has entered the system context, including which matches still need full post-match reconciliation.

**Status:** Completed through Jordan 1-2 Algeria, Group J MD2.

---

## Completed matches known to the repo/session

| Date EDT | Match | Score | Group | Reconciliation status |
|---|---|---:|---|---|
| 2026-06-11 | Mexico vs South Africa | 2-0 | A | Needs full stat reconciliation |
| 2026-06-11 | South Korea vs Czechia | 2-1 | A | Needs full stat reconciliation |
| 2026-06-12 | Canada vs Bosnia and Herzegovina | 1-1 | B | Needs full stat reconciliation |
| 2026-06-12 | United States vs Paraguay | 4-1 | D | Needs full stat reconciliation |
| 2026-06-13 | Qatar vs Switzerland | 1-1 | B | Needs full stat reconciliation |
| 2026-06-13 | Brazil vs Morocco | 1-1 | C | Needs full stat reconciliation |
| 2026-06-13 | Haiti vs Scotland | 0-1 | C | Needs full stat reconciliation |
| 2026-06-14 | Australia vs Turkey | 2-0 | D | Needs full stat reconciliation |
| 2026-06-14 | Germany vs Curacao | 7-1 | E | Needs full stat reconciliation; blowout-tail case |
| 2026-06-14 | Netherlands vs Japan | 2-2 | F | Needs full stat reconciliation |
| 2026-06-14 | Ivory Coast vs Ecuador | 1-0 | E | Needs full stat reconciliation |
| 2026-06-14 | Sweden vs Tunisia | 5-1 | F | Needs full stat reconciliation |
| 2026-06-15 | Spain vs Cape Verde | 0-0 | H | Needs full stat reconciliation; draw-floor case |
| 2026-06-15 | Belgium vs Egypt | 1-1 | G | Needs full stat reconciliation |
| 2026-06-15 | Saudi Arabia vs Uruguay | 1-1 | H | Needs full stat reconciliation |
| 2026-06-15 | Iran vs New Zealand | 2-2 | G | Needs full stat reconciliation |
| 2026-06-16 | France vs Senegal | 3-1 | I | Needs full stat reconciliation |
| 2026-06-16 | Iraq vs Norway | 1-4 | I | Needs full stat reconciliation |
| 2026-06-16 | Argentina vs Algeria | 3-0 | J | Needs full stat reconciliation; Algeria baseline before Jordan match |
| 2026-06-17 | Austria vs Jordan | 3-1 | J | Needs full stat reconciliation; Jordan baseline before Algeria match |
| 2026-06-17 | Portugal vs DR Congo | 1-1 | K | Needs full stat reconciliation; possession paradox case |
| 2026-06-17 | England vs Croatia | 4-2 | L | Needs full stat reconciliation; cards/referee case |
| 2026-06-17 | Ghana vs Panama | 1-0 | L | Needs full stat reconciliation |
| 2026-06-17 | Uzbekistan vs Colombia | 1-3 | K | Needs full stat reconciliation |
| 2026-06-18 | Czechia vs South Africa | 1-1 | A | Needs full stat reconciliation |
| 2026-06-18 | Switzerland vs Bosnia and Herzegovina | 4-1 | B | Needs full stat reconciliation |
| 2026-06-18 | Canada vs Qatar | 6-0 | B | Needs full stat reconciliation; high-corner siege candidate |
| 2026-06-18 | Mexico vs South Korea | 1-0 | A | Partially logged in patterns; needs full stat ledger |
| 2026-06-19 | United States vs Australia | 2-0 | D | Partially logged in patterns; needs full stat ledger |
| 2026-06-19 | Scotland vs Morocco | 0-1 | C | Partially logged in patterns; needs full stat ledger |
| 2026-06-19 | Brazil vs Haiti | 3-0 | C | Needs full stat reconciliation |
| 2026-06-19 | Turkey vs Paraguay | 0-1 | D | Needs full stat reconciliation |
| 2026-06-20 | Netherlands vs Sweden | 5-1 | F | Partially logged; goals/corners decoupling case |
| 2026-06-20 | Germany vs Ivory Coast | 2-1 | E | Needs full stat reconciliation |
| 2026-06-20 | Ecuador vs Curacao | 0-0 | E | Needs full stat reconciliation; draw-floor case |
| 2026-06-21 | Tunisia vs Japan | 0-4 | F | Needs full stat reconciliation |
| 2026-06-21 | Spain vs Saudi Arabia | 4-0 | H | Needs full stat reconciliation |
| 2026-06-21 | Belgium vs Iran | 0-0 | G | Fully logged in calibration v2.8 |
| 2026-06-21 | Uruguay vs Cape Verde | 2-2 | H | Needs full stat reconciliation |
| 2026-06-21 | New Zealand vs Egypt | 1-3 | G | Needs full stat reconciliation |
| 2026-06-22 | Argentina vs Austria | 2-0 | J | Needs full stat reconciliation |
| 2026-06-22 | France vs Iraq | 3-0 | I | Needs full stat reconciliation |
| 2026-06-22 | Norway vs Senegal | 3-2 | I | Needs full stat reconciliation |
| 2026-06-22 | Jordan vs Algeria | 1-2 | J | Corner calibration addendum added; exact official stat split still needed |

---

## Priority reconciliation queue

### Priority 1 — direct model failures or new-rule cases

1. Jordan 1-2 Algeria — corner/set-piece siege, Rule #39 validation.
2. Belgium 0-0 Iran — red-card draw probability, Rule #37/#38 validation.
3. Portugal 1-1 DR Congo — possession paradox and underdog deep block.
4. Canada 6-0 Qatar — siege blowout and corner-volume extreme.
5. Netherlands 5-1 Sweden — goals/corners decoupling.
6. Germany 7-1 Curacao — blowout-tail underprojection.

### Priority 2 — draw-floor and tournament incentive cases

1. Spain 0-0 Cape Verde.
2. Ecuador 0-0 Curacao.
3. Netherlands 2-2 Japan.
4. Uruguay 2-2 Cape Verde.
5. Iran 2-2 New Zealand.
6. Belgium 1-1 Egypt.

### Priority 3 — player-prop and creator/finisher cases

1. Mexico 1-0 South Korea.
2. United States 2-0 Australia.
3. Scotland 0-1 Morocco.
4. Jordan 1-2 Algeria.

---

## Missing data fields for each completed match

For each match above, fill:

```yaml
match_id:
date:
competition_stage:
venue:
referee:
weather:
final_score:
halftime_score:
goals:
  - minute:
    team:
    scorer:
    assist:
    mechanism: open_play | corner | free_kick | penalty | own_goal | transition | error
xg:
shots:
shots_on_target:
possession:
corners:
  team_a:
  team_b:
  total:
corner_times:
cards:
fouls:
offsides:
lineups:
substitutions:
pre_match_predictions:
actual_market_results:
model_grade:
new_lessons:
unresolved_data_gaps:
```

---

## Running match count

Known completed matches listed here: **44**.

Fully reconciled with rich post-match log: **1** definite full entry in current calibration file: Belgium 0-0 Iran.

Partial/special addendum: **Jordan 1-2 Algeria** corner calibration.

This ledger shows the key repository gap: many completed matches have been used as examples in rules/patterns, but most do not yet have complete official post-match stat reconciliation.
