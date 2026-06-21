# Football Intelligence Analysis Index — v2.7

## System Status

**Current Version:** v2.7 (Tunisia-Japan completed)
**Matches Logged:** 13 (all pre-kickoff predictions)
**Running Accuracy:**
- Match Winner: 84.6% (11/13)
- Over/Under 2.5 Goals: 76.9% (10/13)
- Correct Score: 0% (0/9) — known limitation; Rule #34 addresses
- Corner Markets: 20% (1/5) directional calls; corner 1x2 100% (1/1 limited sample)

**Active Rules:** 36 (+ 10 patterns)
**Most Recent Rules Added:** #32–36 (v2.7)

---

## Rules by Category

### Match Result & Form Rules (1–9)
- **Rule #1:** Study Phase Modifier (quality-gap dependent HT discount)
- **Rule #2:** Correct-Score Tail (+1 goal undershoot correction)
- **Rule #3:** Elite Late Surge (+0.7 xG in 70'–90')
- **Rule #4:** High-Press HT Discount (−10% HT Over 0.5 confidence)
- **Rule #5:** Set-Piece Efficiency (high-PPDA teams)
- **Rule #6:** Halftime Reset Multiplier (SH2 goals more likely)
- **Rule #7:** Mandatory Corner-Mechanism Audit
- **Rule #8:** BTTS Model (xG-based)
- **Rule #9:** Red-Card Live-Adjustment

### Tactical & Execution Rules (10–16, 19–20)
- **Rule #10:** Early-Goal Corner Collapse
- **Rule #11:** Static Corner Audit (player-movement based; NOW possession-conditional)
- **Rule #15:** Possession Paradox (territorial dominance ≠ goal probability)
- **Rule #16:** Central-Play Corner Penalty (−3 corners for midfielder-heavy teams)
- **Rule #19:** Timeline Segmentation (don't anchor explanations on most dramatic event)
- **Rule #20:** Red-Card Live-Adjustment (SH2 remaining-match markets only)

### Manager & Team Chemistry (21–32)
- **Rule #21:** Card Over-Projection in Cautious Games (−5 to −8 on Over 4.5)
- **Rule #22:** Mandatory Bracket/Standings/GD/Remaining-Fixture Check (PHASE-0)
- **Rule #23:** Motivation Bonus (must-win situations unlock aggression, if morale intact)
- **Rule #25–28:** Anytime-Scorer Props (creator vs. finisher, service dependency)
- **Rule #32:** Manager-Hire Prep-Time Discount (non-linear decay, <7 days = hard constraint)

### Morale & Psychological Rules (29–36)
- **Rule #29:** Rookie-Team Tournament Shock Ceiling (early underdog lead, SH2 elite reassertion)
- **Rule #30:** Corner Explosion in Comeback Scenarios (+50–75% on SH2 corners for chasing elite)
- **Rule #31:** Substitute Quality Multiplier (elite benches +0.4–0.6 xG in SH2 when chasing)
- **Rule #33:** Catastrophic-Loss Morale Discount (−0.4 to −0.7 xG, age-dependent)
- **Rule #34:** Blowout Score Tail (quality gap >25 pts; redistribute Poisson for 3+ margins)
- **Rule #35:** Early-Tournament Morale Fragility (age-dependent, ≥5-goal loss recovery)
- **Rule #36:** H2H Psychological Ceiling (never-conceded dominance adds +2–3% to favorite)

### Context & Data Rules (4-year cap, bracket, weather)
- **Rule #18:** 4-Year Data Cap (H2H and form data older than 4 years excluded)
- **Rule #22:** Mandatory Bracket Context (Rule expanded to morale baseline check)
- Weather rules: Neutral (1% weight)

---

## Patterns (10 total)

1. **P1–P8:** Existing (reference v2.5 for details)
2. **P9:** Rookie-Team Shock + Elite Response Cycle (Rule #29 formalization)
   - Early underdog shock (1-0 lead HT vs. elite)
   - Elite adaptation in SH2
   - Underdog mental collapse due to experience gap
   - Result: Elite win, often by narrow margin (2-1, 2-0)
   - Example: Germany 2-1 Ivory Coast (MD2)

3. **P10 (NEW):** Early-Tournament Demoralization Collapse (Rules #33, #35 formalization)
   - Underdog suffers ≥5-goal loss in MD1/MD2
   - Manager sacked OR new manager hired <7 days (Rule #32)
   - Team age older (avg ≥30 years)
   - Psychological breakdown from kickoff of next match
   - No shock (no early lead); never competes
   - Result: Elite blowout (3–4 goal margin)
   - Example: Tunisia 0-4 Japan (MD2)

---

## Next Development Focus (v2.8)

1. **Correct-Score Modeling:** Implement Rule #34 in live analysis; monitor if adjusted distributions improve accuracy from 0%
2. **Manager Effectiveness Decay:** Refine Rule #32 formula; test non-linear decay with morale interaction
3. **Age-Demographic Resilience:** Confirm Rule #35 across next 3–4 matches with age-based team data
4. **Possession-Conditional Corners:** Implement revised Rule #11 with possession % conditioning
5. **Blowout Scenario Database:** Catalog all quality-gap >25pt matches (Tunisia-Japan, Germany-Curaçao 7-1, etc.) to calibrate Rule #34 distribution

---

**Index Updated v2.7. Ready for MD3 and knockout-stage analysis.**
