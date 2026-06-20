# Brazil vs Haiti — Live Simulation Snapshot

Competition: FIFA World Cup 2026 Group C  
Match ID: 66456932  
Snapshot context: Brazil 0-0 Haiti, live  
Data quality: low-data live snapshot  
Model version: v2.4 draft inputs

---

## 1. Available Live Data

Verified from available match feed:

- Score: Brazil 0-0 Haiti
- Match status: live
- Group: C

Not available in this snapshot:

- Exact match minute
- Live xG
- Shots
- Shots on target
- Corners
- Cards
- Substitutions
- Field tilt

Because the live data is incomplete, confidence is capped at 6.5/10 under the simulation protocol.

---

## 2. Important Method Correction

A useful draw does not automatically mean that a team will sit deep or stop pursuing victory.

Correct interpretation:

- A draw can reduce reckless risk.
- It does not erase the desire to win.
- Big teams usually continue to pursue victory because of reputation, qualification security, and tactical superiority.
- Underdogs may defend compactly while still countering aggressively.

For Brazil vs Haiti, Brazil should still be modeled as pursuing the win, not passively accepting 0-0. Haiti can be modeled as compact and counter-oriented, but not automatically passive.

---

## 3. Simulation Inputs

### 3.1 Goal Inputs

Brazil expected goals remaining: 2.07  
Haiti expected goals remaining: 0.50

Input rationale:

- Brazil have superior attacking talent and should control territory.
- Haiti are expected to defend compactly and look for transitions or set pieces.
- The current 0-0 live state slightly reduces total remaining goal expectation compared with a full pre-match model, depending on elapsed time.
- Because exact minute is unavailable, the model uses a low-data live estimate rather than precise time decay.

### 3.2 Corner Inputs

Brazil expected corners: 7.3  
Haiti expected corners: 1.9  
Total expected corners: 9.2

Input rationale:

- Brazil territorial control should create repeated wide attacks and blocked entries.
- Haiti compact defending can increase Brazil corner share.
- If Brazil score early, corner volume may drop because Haiti's defensive block opens.
- If the match stays level, Brazil corner pressure likely remains higher.

---

## 4. Simulation Setup

Runs: 200,000  
Goal model: Poisson-style low-data live model  
Corner model: Poisson-style team split model  
Scenario branches included qualitatively:

1. Brazil score first.
2. Haiti score first.
3. Match stays level into later stages.
4. Brazil lead by one late.
5. Match remains low-event.
6. Match opens after the first goal.

---

## 5. Simulation Output

### 5.1 Result Probabilities

| Outcome | Probability |
|---|---:|
| Brazil win | 71.4% |
| Draw | 19.4% |
| Haiti win | 9.1% |

### 5.2 Goal Distribution

| Output | Probability |
|---|---:|
| 2+ total goals | 69.5% |
| 3+ total goals | 45.7% |
| 4+ total goals | 26.3% |
| Both teams score | 32.2% |
| Not both teams score | 67.8% |

### 5.3 Corner Distribution

Median total corners: 9  
Central range: 6-12

| Total Corner Threshold | Probability Above |
|---|---:|
| 7.5 | 61.2% |
| 8.5 | 51.9% |
| 9.5 | 42.9% |
| 10.5 | 34.8% |

### 5.4 Most Common Scores

1. Brazil 1-0
2. Brazil 2-0
3. Brazil 3-0
4. 0-0
5. 1-1

---

## 6. Tactical Reconciliation

Simulation and tactical read broadly agree:

- Brazil remain the likely winner.
- The most robust goal profile is Brazil win without requiring a large margin.
- High corner outcomes depend heavily on whether the match remains level long enough for sustained pressure.
- If Brazil score early, total corners can underperform despite Brazil dominance.
- If Haiti score first or the match stays 0-0 for a long time, Brazil pressure and corner volume should rise.

---

## 7. Main Uncertainty

The main uncertainty is live data incompleteness.

Missing live minute, shots, corners, cards, and xG means the simulation cannot correctly time-decay the match or detect whether Brazil's possession is genuinely dangerous or merely sterile.

Upgrade needed for future live simulations:

- Minute-by-minute score state
- Current corner count
- Shot count and shots on target
- Live xG if available
- Card state
- Substitutions
- Field tilt / dangerous attacks

---

## 8. Calibration Note

After the match, compare:

- Actual result vs simulated result distribution
- Actual goals vs goal distribution
- Actual corners vs corner distribution
- Whether Brazil produced real chance quality or sterile territory
- Whether Haiti's compact plan created meaningful transition danger

Only add a new calibration rule if the error is repeatable and mechanism-based, not random finishing variance.
