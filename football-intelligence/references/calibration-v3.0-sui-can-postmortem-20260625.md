# Football Intelligence — v3.0 Switzerland-Canada Postmortem Calibration

**Date:** 2026-06-25  
**Match:** Switzerland 2-1 Canada  
**Competition:** FIFA World Cup 2026, Group B  
**Primary failed recommendation:** Canada 1X / Canada not to lose  
**Primary correct recommendation:** Over 1.5 goals / BTTS-type match openness  
**Model update type:** Side-protection calibration, home-emotion discount, tournament-control premium

---

## 1. Executive diagnosis

The Switzerland-Canada match did not expose a goals-market failure. It exposed a **protected-side selection failure**.

The pre-match model correctly identified a live scoring environment:

- both teams had attacking form,
- both had top-of-group motivation,
- Canada would push aggressively at home,
- Switzerland were efficient enough to score without needing chaos.

However, the model incorrectly preferred **Canada 1X** because it overweighted:

1. home advantage in Vancouver,
2. recent 6-0 momentum against Qatar,
3. Canada crowd/emotional energy,
4. goal-difference confidence.

It underweighted:

1. Switzerland's tournament-control profile,
2. Switzerland's midfield and defensive structure,
3. Canada's midfield-control risk after injury disruption,
4. the fact that Switzerland's 4-1 win over Bosnia was more structurally meaningful than Canada's 6-0 win over a collapsing Qatar.

Final result: **Switzerland 2-1 Canada**.

Bet grading:

| Market | Pre-match model | Actual | Grade |
|---|---|---|---|
| Canada 1X | Recommended | Switzerland win | MISS |
| Canada ML | Avoid/low confidence | Switzerland win | Correct to avoid |
| Over 1.5 goals | Recommended | 3 goals | HIT |
| BTTS Yes | Playable | 2-1 | HIT |
| Over 2.5 goals | Cautious/playable | 3 goals | HIT, but not primary |
| Switzerland 1X | Not prioritized | Switzerland win | Missed value |

Core lesson: **The goal read was right; the side-protection read was wrong.**

---

## 2. Corrected pre-match probability

Original approximate pre-match side model:

| Outcome | Original |
|---|---:|
| Canada win | 39-40% |
| Draw | 29-30% |
| Switzerland win | 30-31% |

Corrected model after post-match reconciliation:

| Outcome | Corrected |
|---|---:|
| Switzerland win | 36-38% |
| Draw | 29-30% |
| Canada win | 32-34% |

The correct protected side should have been **Switzerland +0.5 / Switzerland 1X**, not Canada 1X.

---

## 3. Why the Canada side read failed

### 3.1 Home advantage was misapplied

Home advantage should not automatically lift a team above an experienced tournament-control opponent when the opponent has superior structure.

Canada had:

- crowd support,
- emotional momentum,
- aggressive attacking rhythm,
- confidence from a 6-0 result.

Switzerland had:

- superior game management,
- more stable defensive structure,
- midfield calm under pressure,
- better ability to punish transition mistakes.

In this matchup, structure beat emotion.

### 3.2 Blowout momentum was overvalued

Canada's 6-0 win over Qatar was real, but the opponent context mattered. Qatar were coming off structural weakness and later showed disciplinary problems. Canada scoring heavily against that profile should have been discounted.

Switzerland's 4-1 win over Bosnia had more predictive value because Bosnia are more physically and tactically resistant than Qatar. The model should have interpreted Switzerland's attacking output as a stronger signal.

### 3.3 Midfield-control risk was underweighted

Canada's midfield issue was identified, but not penalized enough. Against a lower-quality opponent, midfield disruption can be masked. Against Switzerland, it directly affects:

- ability to sustain possession,
- ability to stop Swiss counters,
- ability to manage transitions after losing the ball,
- ability to defend without emotional fouling or structural gaps.

### 3.4 Energy was confused with control

Canada looked like the higher-energy team. Switzerland were the higher-control team.

In betting, the safer side is often the team that controls risk, not the team that creates visible emotional energy.

---

## 4. New calibration rule

### Rule #43 — Tournament-Control Team Protection Rule

When a match has all or most of the following conditions:

1. one emotional/home team,
2. one experienced tournament-control team,
3. quality gap is small or unclear,
4. both teams can accept a draw or have group-stage protection,
5. the home/emotional team has midfield-control injury or availability issues,
6. the opponent has demonstrated structured scoring against stronger resistance,

then **do not automatically select the home team 1X**.

Instead, evaluate protected side in this order:

1. midfield control,
2. defensive structure,
3. transition-risk management,
4. tournament experience/game-state calm,
5. home advantage,
6. recent scoreline momentum.

If the structure/control team grades higher in the first four categories, the preferred protected side becomes:

- structure/control team +0.5,
- structure/control team 1X,
- or no side bet.

Home advantage should only override structure if the home team is also superior in midfield control or chance prevention.

### Practical trigger

If Home Advantage score > Structure score but Midfield Control score < opponent by 8+ points, downgrade home protected-side confidence by **1.0 to 1.5 units**.

If the side edge falls below 55%, separate the goals bet from the side bet.

---

## 5. New calibration pattern

### Pattern P13 — Emotion Team vs Tournament-Control Team

**Definition:** A home or emotionally charged team receives market/model support because of atmosphere, recent blowout, or crowd pressure, but faces an opponent with superior tournament management and defensive structure.

**Common mistaken bets:**

- home team 1X,
- home team DNB,
- home team corners over high line,
- home team win + goals combo.

**Preferred markets:**

- match goals floor if both teams can score,
- BTTS if both attacking mechanisms are clear,
- structure/control team +0.5 if priced as underdog,
- under high corner lines if the control team can slow tempo.

**Applied case:** Switzerland 2-1 Canada.

Canada had the emotion and venue. Switzerland had the structure. Goals were correctly forecast; protected side was wrong.

---

## 6. Weight adjustment recommendation v3.0

This update should not create a total model overhaul. It should surgically rebalance side-selection logic.

| Dimension | v2.9 | v3.0 recommended | Change | Reason |
|---|---:|---:|---:|---|
| Current Form | 15% | 14% | -1% | Blowout form vs weak/collapsing opponent must be discounted |
| Tactical Matchup | 17% | 18% | +1% | Structure/control beat home emotion in SUI-CAN |
| Player Availability | 15% | 15% | — | Canada midfield issue was identified; application needs stricter penalty |
| Advanced Metrics | 9% | 9% | — | No change |
| Home Advantage | 10% | 9% | -1% | Home crowd overvalued vs tournament-control teams |
| Motivation & Bracket Context | 10% | 10% | — | Draw utility remains important |
| Fatigue | 5% | 5% | — | No change |
| Head-to-Head | 5% | 5% | — | No change |
| Team Chemistry | 5% | 5% | — | No change |
| Manager | 3% | 3% | — | No change |
| Referee | 3% | 3% | — | No change |
| Market Analysis | 2% | 2% | — | No change |
| Weather | 1% | 1% | — | No change |
| News & Sentiment | 1% | 1% | — | No change |

Net: Tactical Matchup +1, Home Advantage -1, Current Form -1. The extra point should be assigned to Tactical Matchup because match control was the decisive factor.

Total remains 100%.

---

## 7. Betting construction update

### New protected-side checklist

Before recommending any 1X / DNB / +0.5 side, answer:

1. Is this team better in midfield control?
2. Is this team better in defensive structure?
3. Is this team less emotionally volatile?
4. Is this team less dependent on crowd/tempo?
5. Has this team proven output against a non-collapsing opponent?
6. Does a draw help this team enough to reduce risk?

If fewer than four answers are yes, do not call the protected side safe.

### Canada application

Canada 1X checklist:

| Question | Canada answer |
|---|---|
| Better midfield control? | No / uncertain |
| Better defensive structure? | No |
| Less emotionally volatile? | No |
| Less dependent on crowd/tempo? | No |
| Proven output vs non-collapsing opponent? | Partial |
| Draw useful? | Yes |

Score: 1.5-2/6. Canada 1X should have been downgraded.

Switzerland 1X checklist:

| Question | Switzerland answer |
|---|---|
| Better midfield control? | Yes |
| Better defensive structure? | Yes |
| Less emotionally volatile? | Yes |
| Less dependent on crowd/tempo? | Yes |
| Proven output vs non-collapsing opponent? | Yes |
| Draw useful? | Yes |

Score: 6/6. Switzerland 1X should have been preferred.

---

## 8. Market-specific updates

### Winner / protected side

Downgrade home-team protected sides when:

- opponent has stronger tournament-control profile,
- home team has midfield injury/control weakness,
- home edge comes mostly from emotion,
- recent big win came against a collapsing opponent.

### Goals

Keep goals independent from side when side edge is thin. Switzerland-Canada shows that Over 1.5 can be correct even when the preferred side is wrong.

### Corners

Avoid high corner totals in matches involving tournament-control teams unless chase state is highly likely. Structure teams can reduce chaos and suppress corner volume even while winning.

### Cards

Do not assume home emotion creates more cards. Card projection must be linked to referee profile, trailing-team frustration, and foul mechanism.

---

## 9. Updated post-match record entry

Add match #19:

| Match # | Match | Recommended side | Result | Side Grade | Goals Grade | Key Lesson |
|---:|---|---|---|---|---|---|
| 19 | Switzerland vs Canada | Canada 1X | Switzerland 2-1 Canada | MISS | HIT | Home emotion and blowout form overvalued; tournament-control side should have been protected |

Estimated record movement:

- Protected-side accuracy decreases by one unit.
- Goals-market accuracy improves for Over 1.5 / BTTS profile.
- Corner discipline improves because high corner line was avoided.

---

## 10. Immediate application to future matches

### Mexico-type cases

Do not automatically back the home/already-qualified team if they may rotate and the opponent has urgency. Prefer protection or goals/corners only when mechanism is clear.

### South Korea-type cases

Do not treat the better-name team as safe if camp noise or emotional volatility is high. Check midfield control and defensive structure before recommending 1X.

### Morocco-type cases

This rule supports Morocco-style teams. When the favorite is also the structure/control team, protected side and win bets remain stronger.

---

## 11. Final v3.0 model instruction

For all future tournament group-stage betting analysis:

> Separate **energy advantage** from **control advantage**.  
> Energy can create shots, corners, and momentum.  
> Control wins protected-side bets.

Do not mark a home/emotional side as safe unless it also wins the structure-control checklist.
