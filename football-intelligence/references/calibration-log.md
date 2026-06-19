# Football Intelligence — Calibration Log

> This file is the memory of the system. Every prediction is logged here after the match.
> Weights are recalibrated based on empirical outcomes, not assumptions.

Model version: v2.3 (post Mexico-Korea + USA-Australia + Scotland-Morocco review)

---

## Active Weight Table (Current Session)

| Dimension | Default | Current | Last Adjusted |
|---|---|---|---|
| Current Form | 18% | 18% | — |
| Tactical Matchup | 16% | 16% | — |
| Player Availability | 14% | 14% | — |
| Advanced Metrics | 12% | 12% | — |
| Home Advantage | 10% | 10% | — |
| Motivation & Bracket Context | 8% | 8% | Expanded scope (not yet weight-adjusted) — see Rule 12 |
| Fatigue | 5% | 5% | — |
| Head-to-Head | 4% | 4% | — |
| Team Chemistry | 4% | 4% | — |
| Manager | 3% | 3% | — |
| Referee | 2% | 2% | — |
| Market Analysis | 2% | 2% | — |
| Weather | 1% | 1% | — |
| News & Sentiment | 1% | 1% | — |

---

## Running Accuracy Stats

| Market | Correct | Total | Accuracy |
|---|---|---|---|
| Match Winner | 2 | 2 | 100% (note: Mexico-Korea was right outcome, wrong process — see lessons) |
| Correct Score | 0 | 2 | 0% |
| BTTS | 1 | 1 | 100% (USA-Australia; Mexico-Korea BTTS No also correct) — 2/2 if counted |
| Over/Under 2.5 | 2 | 2 | 100% (both Under 2.5 calls correct) |
| Top Scorer Named | 0 | 2 | 0% (both top picks were "involved," not scorer — see Rule 11) |
| Corners (directional calls only) | 0 | 1 | 0% (Mexico-Korea Over call; USA-Australia correctly declined to call) |

*Sample size is still very small (2 completed matches + 1 in progress). Don't over-read these percentages yet — revisit after 5+ matches per Phase 7.2.*

---

## Active Lessons (Carry Forward)

**Process / Discipline**
1. When professional consensus or other cited sources actively contradict my own lean (e.g., predictors calling 2-0/2-1 while I lean Under 2.5), that is a flag to REDUCE confidence and size, not a footnote to mention and override. Conflicting expert signal = lower conviction, by default.
2. Never assign "highest confidence" / Tier-1 status to a market built on a single causal mechanism (e.g., "Pulisic out = fewer goals") without independently checking the counter-mechanism (e.g., Balogun/Pepi's standalone scoring output without Pulisic). One-legged reasoning gets demoted to Tier 2 at most.
3. A team's tactical "identity" (e.g., Australia's rigid low-block across 4 matches) is a PRE-MATCH-STATE pattern. It must be explicitly re-tested against in-game-state scenarios (chasing a deficit, defending a lead) before being used to justify a full-match goals/result prediction. Identity holds at 0-0/even; it is NOT assumed to hold once a team is forced into a losing position.
4. Corners and similarly "logical-sounding" derived markets (crossing volume, set-piece counts) require a specific same-team historical corners-per-match number before taking a directional position. A plausible tactical story ("they cross a lot," "they dominate the ball") is NOT sufficient evidence — demonstrated twice: Mexico-Korea (predicted Over on crossing logic, actual was ~1-3 total corners) and the USA-Paraguay review (USA dominated territory 56-44 and touches 23-11, but actually won FEWER corners than Paraguay, 5-8 — territorial dominance does not reliably predict corner count in either direction).
5. Anytime-goalscorer picks should be down-weighted for players who are primarily creators/carriers (high key-passes/SCA, low actual shot-conversion history) in favor of out-and-out finishers, OR explicitly flagged as "high-involvement, moderate-scoring-probability" rather than a clean top pick.
6. In any match graded as near-parity on composite/xG, cap stated confidence at ≤6/10 regardless of which side is picked — these games are disproportionately decided by single-event randomness (keeper errors, deflections, own goals) that the 16-dimension framework does not and cannot model.
7. Re-verify "confirmed lineup" claims against an actual official source or a manager's own on-record statement before treating it as settled fact. Third-party "confirmed lineup" article titles are not themselves confirmation — multiple SEO-driven sites have used "confirmed" while still listing predicted/projected XIs.

**Live / In-Game**
8. Once any goal goes in (own goal, deflection, or otherwise), immediately re-run the goals-market read using GAME STATE, not pre-match tactical identity. A 1-0 or 2-0 lead changes incentives for both sides (trailing team must commit forward and abandon a defensive identity; leading team has no incentive to sit back unless explicitly noted as a stated in-game management style for that specific manager). Do this re-check before reaffirming or doubling down on a pre-match Under/Over lean.
9. Distinguish goal QUALITY (clean buildup vs. scrappy/deflected/OG) from goal QUANTITY's effect on the SCOREBOARD. Scrappy low-quality goals still fully count toward game-state shifts (rule 8) even if they don't validate the pre-match "clean attacking dominance" thesis.
9b. CORRECTION (from USA-Australia): game-state ("team must chase") reliably predicts increased SHOTS/CORNERS/CARDS, but does NOT automatically predict additional GOALS — defensive execution quality is a separate variable that can fully absorb game-state pressure. Don't auto-flip a goals-market lean purely on game-state; isolate which sub-markets it actually affects vs. which require also reassessing the trailing team's finishing quality and the leading team's defensive quality specifically.
14. When one team dominates early possession (e.g., 80% by minute 10) after going ahead, separately track TWO different signals before concluding "they'll keep scoring": (a) are they still generating shots/created chances at a high rate (genuine continued threat), or (b) is the possession passive/circulating, consistent with a "control and protect the lead" approach? High possession share alone does not necessarily mean continued goal threat — cross-check shot counts and final-third entries, not just the possession percentage.
15. A team that "can't find the gap" / generates zero shots deep into the first half (observable directly from live shot data) is a stronger signal for the chasing team's struggle than pre-match form alone — update the goals-market live read using actual in-game shot/chance data the moment it diverges from pre-match expectation, in either direction.

**Anytime-Scorer Pattern**
11. A team's most dangerous/creative attacker (high pressure, key passes, chance creation) is NOT the same bet as "most likely to be on the scoresheet" when their primary threat is generating chaos/pressure rather than taking the shot themselves. Confirmed across 2 consecutive matches (Quiñones/Romo at Mexico-Korea; Balogun/Burgess-OG at USA-Australia). For anytime-scorer props, separately weight: (a) players who create chaos/pressure leading to OGs/deflections/spills, vs (b) players who are the actual intended finisher of the team's main attacking pattern. Pick (b) for anytime-scorer markets; (a) is better suited to "involved in a goal" or shots/SCA-based props if offered.

**Tournament/Bracket Context**
12. Every match preview in a tournament with groups/brackets must explicitly read the GROUP TABLE / STANDINGS / REMAINING FIXTURES as a PHASE-0 default step, not just "motivation" as a vague single score, and not only when the user asks. Specifically check and state:
    a. Current points/GD for both teams entering the match, and what result each needs to realistically top the group / guarantee qualification / avoid a winnable-but-risky final matchday decider.
    b. Whether a draw is a "good enough" result for either or both sides given their group situation (this materially changes expected aggression).
    c. Who they play in their LAST group match and that opponent's relative strength — a team already through, or already eliminated, often visibly changes effort/rotation in the second match of the group stage.
    d. GD as a tiebreaker matters specifically once two teams are likely to finish on the same points, or where third-place/best-third-place-team rules are in play (e.g., 2026 WC's 8-best-third-place-teams rule) — note if either team has incentive to keep scoring/avoid conceding even once the match result is functionally decided.
13. Distinguish "trying to score more" from "trying to see out the game" explicitly once a team takes an early lead in a group match — this depends on bracket state (rule 12), not just general "identity." State which scenario applies before assuming either default.

**Sizing**
10. Tier-1 / "core slip" status requires: (a) at least two independent, non-correlated supporting mechanisms, (b) no actively-contradicting expert/market signal, (c) a specific (not generic) evidentiary basis if the market is corners/cards/props. Anything with only one of these three should be Tier 2 at most, sized down accordingly.

---

## Match Log

### 1. Mexico 1-0 South Korea (Group A, MD2) — FINAL
- Predicted: MEX 40-42% / Draw 30-31% / KOR 28-29% | Result: MEX win — correct outcome, wrong process (xG was 0.48-0.69, Korea's favor; decided by a goalkeeper error, pure variance)
- Under 2.5: correct outcome (1-0), wrong stated mechanism (called "cagey/organized," actual cause was a fluke error)
- Corners: predicted Over 9.5 (moderate-confidence) — actual: first corner didn't arrive until 90+2'. SEVERE MISS.
- Anytime scorer (Jiménez, my top pick): missed. Quiñones was most involved (created the goal, 8.6 rating) but didn't score it himself.

### 2. USA 2-0 Australia (Group D, MD2) — FINAL
- Pre-match: Under 2.5 Tier 1 top pick. HT score 2-0 (OG + deflected header), I flipped live to favor Over on game-state logic (Australia must chase, USA has no reason to sit back).
- FINAL: 2-0. Under 2.5 held. Box score (via MCP, fixture 1489391): Shots 10-5 USA, Possession 62-38 USA, Corners 7-4 (11 total), Cards 3Y-4Y (7 total, 0 red).
- Confirmed narrative: Australia DID chase as predicted (pushed numbers forward, box scrambles, 4 cards from desperate fouling) — game-state read was directionally correct. But USA's defense (Ream/Richards) absorbed it; pressure did not convert to goals. See Rule 9b.
- Corners: declined to give a confident directional pick pre-match (insufficient team-specific data). Final total (11) landed in the "fair, no-edge" range estimated. Discipline validated — correctly avoiding a call beats a confident wrong call.
- Anytime scorer: Balogun (top pick) did not score himself — his cross/pressure caused Burgess's own goal. Credited as "involved," not "scored." See Rule 11.

### PATTERN — confirmed across 2 consecutive matches (Mexico-Korea, USA-Australia)
- Mexico-Korea: Quiñones created the goal (cross → keeper spill), Romo scored it. Quiñones rated 8.6, no goal.
- USA-Australia: Balogun's cross/pressure forced Burgess's own goal. Balogun didn't score.
- See Rule 11.

### 3. Scotland vs Morocco (Group C, MD2) — IN PROGRESS, logged live
- Pre-match: Morocco favored (~56-61% market implied), Under 2.5 lean (specific mechanism: fatigue + Morocco's press suppressing space, sourced from named handicapper, not generic).
- Deep gameplay review found specific hard numbers: Scotland-Haiti produced 44 combined fouls (highest in WC group stage since 2010) + 5 yellows; Brazil-Morocco produced 14 Morocco fouls but ZERO Morocco yellows (extreme discipline). Corners: Scotland 3 (vs Haiti), Morocco 3 (vs Brazil) — both undershot their own seasonal averages (Scotland 4.1, Morocco 5.5).
- LIVE: Morocco scored 1' (own early goal), reached 80% possession by min 8-12, Scotland recorded ZERO shots through min 12.
- User-prompted addition: bracket/standings context was missing from the framework entirely until raised mid-match. Added as Rule 12. Applied retroactively: Morocco sat on 1pt pre-match (draw vs Brazil) and needs this win + GD insurance since their final group match is also vs Brazil; Scotland had 3pts banked (beat Haiti) giving them more cushion/less urgency. This independently explained why Scotland looked passive and Morocco kept pushing past 1-0 rather than just "Morocco is better."
- LESSON: bracket context should be PHASE-0 standard, not an add-on prompted by the user mid-match. Gather standings/remaining-fixture context for every team in every World Cup (or any tournament with groups/brackets) preview, by default, before kickoff.
- FILE-LOCATION LESSON (this match): discovered the live calibration log had been written to `/tmp/football-intelligence/references/calibration-log.md` instead of the actual skill's own `/mnt/skills/user/football-intelligence/references/calibration-log.md`. The `/tmp` path is NOT the skill's persistent reference location — SKILL.md's own REFERENCES section points to the `/mnt/skills/...` path. Going forward, ALWAYS read and write the calibration log at the path inside the actual skill folder, not `/tmp`. Phase 0 instruction in SKILL.md itself should be corrected to point here.

---

## Pending result (update once match finishes)
- Scotland vs Morocco: awaiting final score, full box score (corners/cards/shots), and bracket-outcome implications for Group C before closing out the log entry above.
