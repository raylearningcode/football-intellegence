---
name: football-intelligence
description: >
  Elite football match prediction and analysis skill. ALWAYS use this skill when the user asks
  about football/soccer match predictions, betting analysis, team form, tactical breakdowns,
  player availability, match previews, or any request involving "predict", "analyze", "who will win",
  "match preview", "betting tips", or names two football teams in a versus/vs context.
  Also triggers on post-match review requests like "how did we do?", "update the skill",
  "learn from last match", or "was the prediction right?". This skill self-improves after
  every analysis cycle — log lessons learned and update calibration weights each time.
---

# Football Intelligence System — Elite Prediction & Self-Improvement Engine

**Version: v2.3** | Backed up at: https://github.com/raylearningcode/football-intellegence
(push updates there after significant changes — see that repo's README for why this exists)

## PURPOSE

Perform a complete multi-dimensional football intelligence investigation and produce the most accurate probability-based prediction possible. Self-audit after every match. Improve calibration weights and analytical precision iteratively.

**Football is probabilistic, not deterministic. Never guarantee outcomes. Always communicate uncertainty.**

---

## PHASE 0 — SELF-CHECK BEFORE STARTING

Before any analysis, read the calibration log:

```
/mnt/skills/user/football-intelligence/references/calibration-log.md
```

If the file doesn't exist yet, initialize it (see PHASE 7).

Apply any active weight adjustments and lessons from prior predictions.

**IMPORTANT — file location fix (v2.3):** this file lives INSIDE the skill folder, not in /tmp. /tmp is volatile scratch space and should never be used for anything meant to persist across matches or sessions. Always read/write the calibration log at the path above. This has broken the system's memory more than once — see calibration-log.md's "File-Location Incident" section for the full history before assuming any prior "it's updated" claim is accurate. When in doubt, check the GitHub backup (link above) as the source of truth.

---

## PHASE 1 — DATA COLLECTION

Use `web_search` and `fetch_sports_data` to gather all of the following. Do NOT skip any category. If data is unavailable, note it explicitly and adjust confidence rating accordingly.

### 1.1 Team Data
- League position, points, GD
- Home record (W/D/L, GF, GA)
- Away record (W/D/L, GF, GA)
- Last 5 matches (result, score, opponent strength)
- Last 10 matches
- Season xG, xGA

### 1.2 Player Data
- Expected lineup (search press conference / team news)
- Injuries (position, severity, replacement quality)
- Suspensions
- Returning players
- Top scorer / key creator fitness
- Defensive anchor availability

### 1.3 Match Context
- Competition type & stage
- **If group/bracket stage: pull current group standings (points, GD, GF/GA) for BOTH teams, and check both teams' remaining fixtures — this is a default step, not optional, not just for "motivation." See D9 for what to do with this.**
- Title race / relegation battle implications
- Derby / rivalry status
- European spot implications
- Cup progression stakes

### 1.4 Environmental Data
- Stadium name, capacity, pitch size
- Weather forecast (temp, rain, wind)
- Altitude (if relevant)
- Home crowd impact

### 1.5 External Factors
- Rest days since last match
- Travel distance (away team)
- International break lingering effects
- Manager changes (last 30 days)
- Dressing room news / morale signals

---

## PHASE 2 — ANALYSIS FRAMEWORK (16 Dimensions)

Score each dimension 0–100. Justify every score in 2–4 sentences.

### D1. Current Form (Weight: 18%)
- Last 5 + Last 10 results
- xG vs actual goals (over/underperforming?)
- Home vs Away form split
- Winning/losing streaks
- Clean sheets trend

> **Score: Home [X] | Away [X]**

### D2. Head-to-Head (Weight: 4%)
- Last 5 and last 10 meetings
- Same competition meetings
- Same venue meetings
- Psychological edge patterns
- Tactical dominance patterns

> **Score: [X] (favors Home / Away / Neutral)**

### D3. Home/Away Advantage (Weight: 10%)
- Home win rate this season
- Away win rate this season
- xG at home vs away
- Goals conceded at home vs away

> **Score: Venue Edge = [X]**

### D4. Stadium Factor (Weight: included in D3)
- Historical avg goals in this stadium
- Pitch dimensions
- Surface quality
- Crowd intensity / decibel factor

> **Stadium Note: [observation]**

### D5. Player Availability (Weight: 14%)

For every key absentee:
```
Player | Position | Impact (1-10) | Replacement Quality (1-10)
```

- Injury list completeness
- Rotation risk (cup/league fatigue management)
- Returning star players

> **Score: Home [X] | Away [X]**

### D6. Team Chemistry (Weight: 4%)
- Starting XI consistency (# changes last 5 games)
- Recent transfers bedding in
- Manager-player tensions (press signals)
- Contract dispute news

> **Score: Home [X] | Away [X]**

### D7. Tactical Matchup (Weight: 16%)
- Formations (both teams)
- Pressing intensity vs build-up style
- Counterpressing vs deep block
- Set-piece threat (attacking + defensive)
- Transition speed
- Width vs compactness
- Which system tactically counters the opponent?

> **Tactical Edge: [Team] | Magnitude: [Low/Medium/High]**

### D8. Manager Quality (Weight: 3%)
- Career win % at this level
- Record vs this opponent
- Tactical flexibility rating
- Big-match performance history
- In-game adjustment ability

> **Score: Home [X] | Away [X]**

### D9. Motivation & Bracket Context (Weight: 8%)

**For ANY tournament with groups/brackets (World Cup, Euros, Champions League groups, etc.), this is NOT optional and is NOT just a vibe score. Pull the actual standings before writing anything else. Required sub-checks:**
- Current points/GD for both teams entering the match.
- What result does each team actually NEED — to top the group, guarantee qualification outright, or avoid a risky final-matchday decider?
- Is a draw "good enough" for either or both sides given their group situation? (This changes expected aggression directly — state it.)
- Who do they play in their LAST group match, and how strong is that opponent? A team already through, or already eliminated, often visibly changes effort/rotation in match 2.
- Does GD matter as a tiebreaker here — especially under "best third-placed team" rules (e.g., 2026 World Cup's 8-best-thirds-advance rule)? If so, note whether either team has incentive to keep scoring or avoid conceding even after the match result is functionally decided.

Beyond bracket state, also check the standard motivation factors:
- Derby stakes?
- Championship / Top-4 / Relegation battle (domestic leagues)?
- Nothing-to-play-for risk (rotation, reduced intensity)?
- Player-level incentives (contract year, records)?

> **Motivation Score: Home [X] | Away [X]**
> **Bracket State: [explicit 1-2 sentence summary of what each team needs and how it likely affects their approach]**

### D10. Fatigue (Weight: 5%)

Last 14 days:
```
Team | Matches | Avg Minutes | Travel KM | Rest Days
```

- Fixture congestion index
- Rotation depth quality
- International break returnees (jet lag, fitness)

> **Fatigue Risk: Home [Low/Med/High] | Away [Low/Med/High]**

### D11. Referee Analysis (Weight: 2%)
- Avg yellow cards per match
- Avg red cards per match
- Penalty award rate
- Fouls per game
- Home/away bias tendency
- Style: strict / lenient / advantage-play

> **Referee Impact: [observation + which team benefits]**

### D12. Weather (Weight: 1%)
- Temperature (cold favors defensive? heat favors technical?)
- Rain (disrupts passing game?)
- Wind (long ball / set-piece effect)
- Heavy pitch (favors direct play)

> **Weather Advantage: [Team / Neutral]**

### D13. Advanced Metrics (Weight: 12%)
- xG per match (season average)
- xGA per match
- PPDA (pressing metric — lower = higher press)
- Possession % (home vs away)
- Shot conversion rate
- Big chances created vs conceded
- Progressive passes per 90
- Set-piece goals % of total goals

> **xG Edge: [Team] | Metric Confidence: [Low/Med/High]**

### D14. Betting Market (Weight: 2%)
- Opening odds (1 / X / 2)
- Current odds
- Odds movement direction
- Asian handicap line
- Over/Under line and movement
- Sharp money signals (odds shortening vs public)

> **Market Lean: [observation]**

### D15. News & Sentiment (Weight: 1%)
- Press conference key quotes
- Manager body language signals
- Fan sentiment index
- Club official announcements
- Transfer window distraction risk

> **Sentiment Signal: [Positive / Neutral / Negative per team]**

### D16. Live Match (if applicable, replaces static weights)
- Possession %, xG live, shots on target
- Dangerous attacks
- Cards, subs, injuries live
- Momentum shift indicators
- Dynamically updated probability

**Game-state rules (learned from calibration — see calibration-log.md Rules #19, #20, #23, #24):**
- Once any goal goes in (own goal, deflection, or otherwise), immediately re-run the goals-market read using GAME STATE, not pre-match tactical identity. Trailing team must commit forward; leading team usually has no incentive to sit back — UNLESS that manager/team has a specific stated "protect the result" pattern.
- BUT: "team must chase" reliably predicts more SHOTS/CORNERS/CARDS — it does NOT automatically predict more GOALS. Defensive execution quality is a separate variable that can fully absorb game-state pressure. Check the leading team's defensive quality before assuming pressure converts to goals.
- High possession share (e.g., 80%+) after taking a lead does not by itself mean continued goal threat — cross-check actual shot counts and final-third entries. Passive/circulating possession (control-and-protect) looks different from possession backed by a high shot rate (continued genuine threat). Distinguish the two explicitly.
- A team generating zero (or very few) shots deep into a half is a stronger live signal of genuine struggle than pre-match form — update the read the moment live data diverges from pre-match expectation, in either direction.
- Cross-reference bracket state (D9) live too: a team already "safe enough" on points may visibly shift to control-and-protect once ahead, while a team needing GD insurance keeps pushing even with a comfortable lead. Don't assume either default without checking.

> **Live Momentum Score: [X/100]**

---

## PHASE 3 — WEIGHTED COMPOSITE SCORING

Default weights (adjust with justification when context demands). **Current adjusted weights are
v2.1, carried forward from calibration-log.md's Active Weight Table — start from these, not the
raw defaults, then adjust further per-match if the specific fixture calls for it:**

| Dimension | Default Weight | v2.1 Adjusted | Justification |
|---|---|---|---|
| Current Form | 18% | 16% | xG-form projections missed goal volume in several matches |
| Tactical Matchup | 16% | 18% | Decisive in 4/8 matches (bus-parking, press intensity) |
| Player Availability | 14% | 15% | Montes suspension pivotal; key injuries underweighted |
| Advanced Metrics | 12% | 10% | Possession metrics misleading (Rule #15) |
| Home Advantage | 10% | 10% | Unchanged |
| Motivation & Bracket Context | 8% | 8% | Scope expanded (Rule #22), weight unchanged so far |
| Fatigue | 5% | 5% | Unchanged |
| Head-to-Head | 4% | 4% | Unchanged |
| Team Chemistry | 4% | 4% | Unchanged |
| Manager | 3% | 3% | Unchanged |
| Referee | 2% | 3% | England-Croatia card impact underweighted |
| Market Analysis | 2% | 2% | Unchanged |
| Weather | 1% | 1% | Unchanged |
| News & Sentiment | 1% | 1% | Unchanged |
| **TOTAL** | **100%** | **100%** | |

Calculate:
- Home Composite Score
- Away Composite Score
- Draw Indicator (closeness of scores + historical draw rate in this matchup type — see Rule #13
  for World Cup-specific hardcoded draw floors that should never be undercut)

---

## PHASE 4 — PROBABILITY GENERATION

### 4.1 Match Winner
```
Home Win:  XX%
Draw:      XX%
Away Win:  XX%
```

### 4.2 Double Chance
```
1X (Home or Draw): XX%
X2 (Draw or Away): XX%
12 (Home or Away): XX%
```

### 4.3 Goal Markets
```
Over 0.5:  XX%
Over 1.5:  XX%
Over 2.5:  XX%
Over 3.5:  XX%
Over 4.5:  XX%
Under 2.5: XX%
```

Base on: combined xG of both teams, historical avg goals in H2H, season avg goals, team attacking/defensive ratings, weather/fatigue modifiers.

### 4.4 BTTS
```
BTTS Yes: XX%
BTTS No:  XX%
```

### 4.5 First Half
```
First Half Winner: [Home / Draw / Away]
First Half Goals: [Over/Under 0.5 / 1.5]
First Half Probability: XX%
```

### 4.6 Correct Score (Top 5)
```
1. X-X  (XX%)
2. X-X  (XX%)
3. X-X  (XX%)
4. X-X  (XX%)
5. X-X  (XX%)
```

### 4.7 Player Props
```
Most Likely Goalscorer(s): [Player | Est. probability]
Most Likely Assister:      [Player | Est. probability]
Most Likely Yellow Card:   [Player | Reason]
Most Likely Chance Creator:[Player | Reason]
```

---

## PHASE 5 — MONTE CARLO SIMULATION

Conceptually simulate 10,000 match instances using:
- Team strength differentials
- Home advantage factor
- Form momentum coefficient
- Fatigue modifier
- Key player availability multiplier
- Historical variance in this type of fixture

Output:
```
Simulated Home Win:  XX%
Simulated Draw:      XX%
Simulated Away Win:  XX%
Expected Goals Range: X.X – X.X total goals
```

Compare simulation output to Phase 4. If divergence > 8%, investigate and reconcile.

---

## PHASE 6 — FINAL OUTPUT

### SELF-AUDIT CHECKLIST (complete before finalizing)

```
✓ Recent form analyzed?
✓ Home/away splits analyzed?
✓ Injuries + suspensions covered?
✓ Tactical matchup assessed?
✓ Manager influence considered?
✓ Referee profiled?
✓ Weather checked?
✓ Fatigue evaluated?
✓ Motivation established?
✓ Betting market checked?
✓ Advanced metrics used?
✓ Uncertainty explained?
✓ Monte Carlo run?
✓ Calibration log checked?
```

Any NO → continue analysis until resolved.

---

### FINAL REPORT FORMAT

```
═══════════════════════════════════════════════════
  FOOTBALL INTELLIGENCE REPORT
  Match:       [Home] vs [Away]
  Competition: [League/Cup]
  Date:        [Date + KO Time]
  Venue:       [Stadium]
═══════════════════════════════════════════════════

WIN PROBABILITIES
  Home Win:  XX%
  Draw:      XX%
  Away Win:  XX%

CONFIDENCE RATING: X/10
  [Explain why — data completeness, variance, key uncertainties]

MOST LIKELY SCORE: X-X
SCORE PROBABILITY:  XX%

TOP BETTING LEANS
  1. [Market] — [Est. Probability] — [Reason]
  2. [Market] — [Est. Probability] — [Reason]
  3. [Market] — [Est. Probability] — [Reason]

KEY REASONS SUPPORTING PREDICTION
  1.
  2.
  3.
  4.
  5.

BIGGEST RISKS / PREDICTION KILLERS
  1.
  2.
  3.
  4.
  5.

MONTE CARLO VALIDATION
  Simulated: Home XX% | Draw XX% | Away XX%
  Model/Sim Agreement: [Strong / Moderate / Divergent]

FINAL VERDICT
  [3–5 sentence professional analyst conclusion]
  [Always acknowledge uncertainty and probabilistic nature]

═══════════════════════════════════════════════════
  ⚠ This is a probability model, not a guarantee.
  Football produces upsets. Bet responsibly.
═══════════════════════════════════════════════════
```

---

## PHASE 7 — POST-MATCH SELF-IMPROVEMENT (CRITICAL)

After the match result is known, run this improvement loop.

### 7.1 Outcome Logging

Append a new entry to the "Match Log" section of
`/mnt/skills/user/football-intelligence/references/calibration-log.md`, following the format
already established there (see existing entries #1-10 for the actual structure in use):

```markdown
### N. [Home] [Score] [Away] — FINAL (or IN PROGRESS) [Competition/Stage, Date]
- Predicted: Home XX% / Draw XX% / Away XX%. Leans: [market 1], [market 2], [market 3].
- Actual: [score]. Scorer(s)/key moments with minute markers.
- Stats (via MCP or web search): possession, shots, corners, cards — cite the source.
- Grade: [Market] ✓/✗ for each major lean, with a one-line reason for each miss.
- New rule(s) born from this match, if any — write the rule directly into the "Active
  Calibration Rules" section above (using the next available rule number) and reference it here.
```

This richer format (vs. a generic fill-in-the-blanks template) is what's actually been used in
practice — match log entries should read like a genuine post-mortem, not a checklist.

### 7.2 Weight Recalibration Rules

After 5 logged matches, review patterns:

- If form weight predictions consistently overshoot: reduce form weight by 1–2%, redistribute to Tactical Matchup or Player Availability
- If xG-based predictions consistently miss: reduce Advanced Metrics weight, increase Head-to-Head
- If home advantage is underestimated in specific leagues: add a league-specific home boost modifier
- If weather/referee impact was significant: temporarily boost their weights for similar fixture types

Document all changes in calibration log.

### 7.3 Precision Improvement Targets

Track across predictions:
```
Match Winner Accuracy:    X/N correct (XX%)
Correct Score:            X/N correct (XX%)
BTTS Accuracy:            X/N correct (XX%)
O/U 2.5 Accuracy:         X/N correct (XX%)
Top Scorer Named:         X/N correct (XX%)
Confidence Calibration:   [was 7/10 confidence, won X% of those]
```

Goal: Improve each metric by ≥5% every 10 matches.

---

## REFERENCES

- `references/calibration-log.md` — Running log of predictions vs outcomes + weight adjustments
- `references/league-profiles.md` — League-specific home advantage, avg goals, tactical norms
- `references/h2h-patterns.md` — Notable recurring H2H tactical/psychological patterns

---

## SKILL EVOLUTION PHILOSOPHY

> "Each match is a data point. Each error is a lesson. Each correct prediction validates a weight. The system improves by challenging its own assumptions — never by simply repeating the same formula."

This skill is **never finished**. It is a living analytical engine. After every match:
1. Log the outcome
2. Audit the prediction
3. Update the weights
4. Sharpen the heuristics
5. Carry lessons forward
