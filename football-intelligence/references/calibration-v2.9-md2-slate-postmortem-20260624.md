# Football Intelligence — v2.9 MD2 Slate Postmortem

Date reconciled: 2026-06-24  
Slate covered: Portugal vs Uzbekistan, England vs Ghana, Panama vs Croatia, Colombia vs DR Congo  
Primary failure trigger: England 0-0 Ghana destroyed the England 1X + Over 1.5 combo.

---

## 1. Executive Diagnosis

The model did not fail equally across the slate. It failed in **bet construction**, specifically by pairing a relatively sound result-protection leg with a goal-total leg in a match where the opponent's defensive plan could suppress tempo.

### Actual slate results

| Match | Prediction profile | Actual | Grade |
|---|---|---:|---|
| Portugal vs Uzbekistan | Portugal win; Portugal + Under 4.5; avoid extreme handicap | Portugal 5-0 Uzbekistan | Mixed: winner hit, margin cap failed |
| England vs Ghana | England DNB / England 1X + Over 1.5 | England 0-0 Ghana | Major miss on goal attachment |
| Panama vs Croatia | Croatia DNB / Croatia win; Under 3.5 | Panama 0-1 Croatia | Strong hit |
| Colombia vs DR Congo | Colombia DNB + Under 3.5; Colombia win fair >1.75 | Colombia 1-0 DR Congo | Strong hit |

### Critical lesson

The England miss was not random. It exposed a repeatable model weakness:

> A favorite can be tactically correct, territorially dominant, and still be a bad goals-combo leg when the opponent is comfortable defending for a draw and the favorite has already banked points.

This must become a hard pre-bet gate, not a soft narrative caveat.

---

## 2. Match-by-Match Reconciliation

### 15. Portugal 5-0 Uzbekistan — FINAL (Group K, MD2, Houston, June 23, 2026)

**Pre-match model:**
- Portugal win: 66%
- Draw: 22%
- Uzbekistan win: 12%
- Over 2.5: 48%
- Under 3.5: 73%
- Main lean: Portugal win + Under 4.5
- Stated caution: avoid heavy Portugal -2.0/-2.5 unless lineup and early intent supported it.

**Actual:** Portugal 5-0 Uzbekistan.

**Grade:**

| Market | Result | Calibration |
|---|---|---|
| Portugal win | HIT | Core 1x2 read correct |
| Portugal + Under 4.5 | MISS | Blowout tail underweighted after early goal |
| Avoid extreme handicap caution | MISS by opportunity cost | Portugal ceiling was higher than model allowed |
| Correct score 2-0 | MISS | Correct-score module still weak |

**Learning:**
Portugal's first goal arrived early, which changed the entire match state. The pre-match Under 4.5 was reasonable only under a controlled 2-0 / 3-0 script, but the model did not sufficiently account for the interaction of:
1. early favorite goal,
2. rookie/debutant opponent fragility,
3. goal-difference incentive,
4. elite forward confidence rebound.

**Add to Rule #34 / blowout tail:** When an elite favorite faces a World Cup debutant or low-finals-experience team and scores inside the first 15 minutes, increase 4+ goal tail probability sharply. The correct live adjustment is to abandon pre-match Under 4.5 protection unless the favorite visibly drops tempo.

---

### 16. England 0-0 Ghana — FINAL (Group L, MD2, Foxborough/Boston, June 23, 2026)

**Pre-match model:**
- England win: 58%
- Draw: 25%
- Ghana win: 17%
- Over 2.5: 52%
- Under 3.5: 68%
- BTTS Yes: 49%
- Main lean: England DNB
- Combo lean: England 1X + Over 1.5

**Actual:** England 0-0 Ghana.

**Grade:**

| Market | Result | Calibration |
|---|---|---|
| England DNB | PUSH | Result protection did its job |
| England 1X | HIT | Low-risk outcome leg correct |
| England 1X + Over 1.5 | MISS | Bad packaging; goals leg should not have been attached |
| Over 1.5 | MISS | Favorite chance quality overestimated |
| Draw probability 25% | Undervalued | Should have been 30-34% after bracket context and Ghana block |

**Why the miss happened:**

1. **England's opening 4-2 over Croatia was over-weighted.** That scoreline inflated goal expectation for MD2, but it came against an opponent willing to open the midfield, not a low-block Ghana side.
2. **Ghana's tactical objective was mispriced.** Ghana entered with 3 points. A draw was strategically valuable; therefore, Ghana had no need to chase.
3. **England's bracket state reduced urgency.** England also entered with 3 points. A draw was not disastrous, so the urgency to force chaos was lower than a must-win scenario.
4. **Low-event first halves must trigger live de-risking.** If 0-0 at HT with low shots-on-target, abandon Over 1.5 and shift to Under or draw-protection.
5. **The combo was structurally inferior to the straight leg.** England DNB was fine. England 1X + Over 1.5 added an independent failure mode for little analytical gain.

---

### 17. Panama 0-1 Croatia — FINAL (Group L, MD2, Toronto, June 23, 2026)

**Pre-match model:**
- Panama win: 14%
- Draw: 27%
- Croatia win: 59%
- Under 3.5: 76%
- Main lean: Croatia DNB
- Stronger lean: Croatia win

**Actual:** Panama 0-1 Croatia.

**Grade:**

| Market | Result | Calibration |
|---|---|---|
| Croatia DNB | HIT | Correct risk-managed side |
| Croatia win | HIT | Correct directional read |
| Under 3.5 | HIT | Correct low-margin script |
| Correct score 0-1 | HIT if selected from fun picks | Rare correct-score success |

**Learning:**
This was the ideal model case: better technical side, high urgency, but low total-goal ceiling. The combination of Croatia DNB + Under 3.5 was structurally superior to chasing Croatia -1.5.

---

### 18. Colombia 1-0 DR Congo — FINAL (Group K, MD2, Guadalajara/Zapopan, June 23, 2026)

**Pre-match model:**
- Colombia win: 57%
- Draw: 27%
- DR Congo win: 16%
- Under 3.5: 78%
- Main lean: Colombia DNB + Under 3.5
- Straight Colombia only if price better than ~1.75

**Actual:** Colombia 1-0 DR Congo.

**Grade:**

| Market | Result | Calibration |
|---|---|---|
| Colombia DNB | HIT | Correct risk-managed favorite leg |
| Colombia win | HIT | Correct but narrow; price sensitivity justified |
| Under 3.5 | HIT | Strong read |
| Avoid Colombia -1.5 | HIT | DR Congo block made margin fragile |

**Learning:**
This validated the favorite-vs-5-3-2 / low-block caution. Colombia dominated but needed a late 76' breakthrough. The model correctly avoided overextending into handicap markets.

---

## 3. Slate-Level Performance

### Directional market grading

| Category | Calls | Hits | Notes |
|---|---:|---:|---|
| 1x2 / DNB / protection | 5 | 4.5 | England DNB push counted as half-success |
| Under 3.5 style reads | 2 | 2 | Croatia and Colombia strong |
| Over 1.5 / goal-combo reads | 1 | 0 | England combo failure |
| Correct scores | 4 | 2 | Croatia 0-1 and Colombia 1-0 matched listed score set; Portugal/England missed |
| Main card/parlay construction | 1 slate | Failed | England total-goal attachment killed it |

### Net diagnosis

The model's **side selection** was solid. The model's **goals-market packaging** was too aggressive in one match and too capped in another:

- England: goal expectation too high.
- Portugal: favorite margin tail too low.
- Croatia/Colombia: correct low-margin favorites.

This means no broad reset is needed. The improvement should be surgical:
1. tighter gates before attaching Over 1.5 to favorite-protection legs;
2. stronger live and pre-match blowout-tail rules for elite favorites after early goals;
3. mandatory bracket-state aggression scoring before goal-combo construction.

---

## 4. New Rules for v2.9

### Rule #39 — Favorite Protection + Goals Combo Gate

**Definition:** Do not attach Over 1.5 / Over 2.5 to a favorite-protection leg unless the match passes a separate goals-combo gate.

**Gate requirements:**

A favorite 1X/DNB + Over 1.5 combo is allowed only if at least 4 of 6 are true:

1. Favorite needs a win, not merely a draw.
2. Opponent also needs a win or cannot rationally sit on a draw.
3. Opponent's defensive structure is not a compact low block / 5-back / Queiroz-style block.
4. Favorite has produced reliable shots-on-target across multiple recent matches, not only one high-scoring opener.
5. Weather and pitch conditions do not reduce passing tempo or final-third execution.
6. Market total is not already inflated by public perception after a favorite's previous high-scoring match.

**Formula:**

```
If Gate_Score <= 3/6:
    Ban favorite protection + Over 1.5 combo
    Prefer: favorite DNB, 1X, Under 3.5, or no bet

If Gate_Score == 4/6:
    Allow only at strong price; reduce stake by 30-40%

If Gate_Score >= 5/6:
    Combo allowed at normal stake
```

**England-Ghana application:**
- England needed win? No, draw was acceptable after MD1 win.
- Ghana needed win? No, draw was valuable after MD1 win.
- Ghana low-block risk? Yes.
- England SOT reliability beyond Croatia? Not proven.
- Weather reduced tempo? Yes, persistent drizzle reported.
- Market inflated by Croatia 4-2? Likely yes.

Gate score: 0-1/6. Combo should have been banned.

---

### Rule #40 — Mutual Draw Utility Raises 0-0 / Under Probability

**Definition:** When both teams enter a group-stage MD2 match on 3 points, or both can materially benefit from a draw, raise draw and Under probabilities before evaluating totals.

**Adjustment:**

```
If both teams have 3 pts after MD1:
    Draw probability +5 to +9 percentage points
    Under 2.5 probability +6 to +10 percentage points
    Over 1.5 probability -8 to -12 percentage points
    BTTS Yes probability -5 to -8 percentage points
```

**Rationale:**
Both sides can protect qualification probability. Even if the favorite has superior attacking talent, the match can settle into control-first football. The underdog has no incentive to expose itself; the favorite has no need to create end-to-end variance.

**England-Ghana application:** England and Ghana both entered with 3 points. England had superior talent, but Ghana's point utility was high and England's urgency was lower than modeled. Revised pre-match line should have been:

- England win: 50-53%
- Draw: 30-34%
- Ghana win: 14-17%
- Over 1.5: 48-52%, not 71% combo-leg confidence
- Best bet: England DNB only, or Under 3.5

---

### Rule #41 — Low-Event First-Half Override for Live Betting

**Definition:** If a favorite-backed Over leg is live and the first half ends 0-0 with limited shots on target, the model must override the pre-match goals lean.

**Trigger:**

```
If HT score == 0-0
AND total shots on target <= 1
AND favorite has possession without central penetration:
    Cancel or hedge Over 1.5 exposure
    Increase 0-0 / 1-0 / 0-1 correct-score probability
    Prefer Under 2.5 or no additional bet
```

**England-Ghana application:** The first half reportedly had no shots on target. That is a hard live signal that pre-match attacking assumptions were wrong. The model should have immediately downgraded Over 1.5 and moved toward Under / Draw protection.

---

### Rule #42 — Early Elite-Favorite Goal Blowout Tail

**Definition:** When an elite favorite scores early against a debutant / low-finals-experience opponent, the high-margin tail expands dramatically.

**Trigger:**

```
If favorite Elo/talent gap is large
AND opponent has low World Cup finals experience
AND favorite scores before minute 15:
    Increase Over 3.5 by +10 to +18 pts
    Increase favorite -2.5 by +8 to +14 pts
    Reduce Under 4.5 confidence by 15-25 pts unless favorite visibly slows tempo
```

**Portugal-Uzbekistan application:** Ronaldo scored early and Portugal's confidence snapped back. The pre-match Under 4.5 should have been abandoned live. Portugal -2.5 or Over 3.5 became the better live read after the second goal.

---

## 5. New Pattern for v2.9

### Pattern P12 — Comfortable Underdog Block vs. Low-Urgency Favorite

**Definition:** A disciplined underdog with 3 points can reduce a superior opponent's attacking value by choosing draw-first football. This is most dangerous in MD2 group-stage matches.

**Characteristics:**

1. Underdog already has 3 points.
2. Favorite also has 3 points or does not need a win.
3. Underdog manager is structurally conservative or tournament-pragmatic.
4. First 15 minutes show no pressing panic from the underdog.
5. Favorite possession is lateral, not penetration-heavy.
6. Match remains 0-0 at HT.

**Betting implication:**
Avoid Over 1.5/2.5 combo legs. Prefer:
- favorite DNB only,
- Under 3.5,
- draw ladder small exposure,
- no bet if price is poor.

**Evidence:** England 0-0 Ghana, Group L MD2.

---

## 6. Weight Adjustment Recommendation: v2.8 → v2.9

The active v2.8 weights should not be radically changed. The issue was not broad prediction capability; it was market packaging and match-state conditionality.

| Dimension | v2.8 | v2.9 Proposed | Change | Reason |
|---|---:|---:|---:|---|
| Current Form | 16% | 15% | -1% | England-Croatia 4-2 over-inflated England goal expectation |
| Tactical Matchup | 16% | 17% | +1% | Ghana block suppressed England; DR Congo block kept Colombia narrow |
| Player Availability | 15% | 15% | — | No major issue |
| Advanced Metrics | 10% | 9% | -1% | Possession/chance volume alone misled England/Colombia margin expectations |
| Home Advantage | 10% | 10% | — | Neutral venues; no change |
| Motivation & Bracket Context | 8% | 10% | +2% | Mutual draw utility was underweighted in England-Ghana |
| Fatigue | 5% | 5% | — | No decisive evidence |
| Head-to-Head | 5% | 5% | — | No change |
| Team Chemistry | 5% | 5% | — | No change |
| Manager | 3% | 3% | — | Keep but apply conservative-manager flag inside tactical rules |
| Referee | 3% | 3% | — | No major slate card lesson |
| Market Analysis | 2% | 2% | — | Price still matters; no exact odds audited here |
| Weather | 1% | 1% | — | Weather should trigger gate, not weight shift |
| News & Sentiment | 1% | 1% | — | No change |

Total remains 100%.

---

## 7. Updated Betting Construction Policy

### New hard rule: do not mix safety leg + volatile total without independent confirmation

A side-protection leg such as 1X or DNB is designed to reduce variance. Adding Over 1.5 reintroduces variance unless there is a strong independent reason for goals.

**Bad construction:**
- England 1X + Over 1.5 when both teams are fine with a draw.

**Good construction:**
- England DNB alone.
- England 1X alone.
- England 1X + Under 3.5 if tempo suppression is expected.
- No bet if odds are too short.

### Parlay policy

1. Parlays must not include more than one leg that depends on the same fragile assumption.
2. A favorite result leg and an over-goals leg are correlated only if the favorite is highly motivated to run up score.
3. If the underdog's best outcome is a draw and the favorite can tolerate a draw, Over legs are not safety-compatible.
4. Use DNB/1X as protection, not as a base to force a bigger price.

---

## 8. Revised Accuracy After Slate

Previous log was reconciled through match #14. This addendum logs matches #15-18.

| Market | Previous | Slate Result | New Approx. |
|---|---:|---:|---:|
| Match Winner / protected direction | 11/14 | +3.5/4 | ~14.5/18 |
| Over/Under 2.5 / totals direction | 11/14 | Mixed; England Over miss, Croatia/Colombia Under hits, Portugal cap miss | ~13/18 depending grading |
| Correct Score | 0/10 | +2/4 listed score-set hits | Still weak but improving via low-margin scripts |
| BTTS | 7/12 | England BTTS No implied hit; Colombia BTTS No hit | Improved, but needs exact market tracking |
| Parlay construction | Not tracked cleanly | Failed because England Over attachment | Needs separate metric |

### New metric required

Add a new tracked category:

```
Bet Construction Accuracy:
- Did the recommended combination preserve or destroy edge?
- Did every added leg have independent justification?
- Did combo increase payout without adding an unpriced failure mode?
```

England-Ghana should be logged as:
- Side read: acceptable.
- Total read: miss.
- Bet construction: miss.

---

## 9. Action Items for Next Analysis

Before any future slate betting card, run this checklist:

1. **Separate side edge from total edge.** Never assume favorite edge implies goals edge.
2. **Run Mutual Draw Utility check.** If both teams can accept a draw, reduce over-goal exposure.
3. **Run Low-Block Suppression check.** If underdog has tactical tools to kill tempo, ban goals combos unless price is exceptional.
4. **Run Early Goal Live Override.** If elite favorite scores early vs fragile opponent, reassess blowout tail immediately.
5. **Track bet construction separately.** A correct side read can still become a losing recommendation if packaged badly.

---

## 10. Final v2.9 Verdict

The slate confirms the model should keep its core tactical and protected-side reads. Portugal, Croatia, and Colombia were directionally correct, and Croatia/Colombia low-margin analysis was strong.

The real improvement is market discipline. England-Ghana proves that the model must stop using Over 1.5 as a casual combo booster when bracket incentives and opponent structure point toward a low-event match. From v2.9 onward, every goals-combo recommendation requires an explicit pass through Rule #39.

**System status:** v2.9 addendum created. Main calibration-log.md should be updated next by merging Rules #39-42 and Pattern P12 into the active rules table.
