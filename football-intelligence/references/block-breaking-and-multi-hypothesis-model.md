# Block Breaking and Multi-Hypothesis Model

Purpose: prevent one-sided favorite analysis. The model must test several possible match stories before forecasting: favorite dominance, sterile possession, underdog resilience, goalkeeper variance, set-piece disruption, and transition threat.

---

## Core Principle

Do not ask only: `Who is better?`

Ask:

1. Can the stronger team break the specific defensive block?
2. Can the weaker team survive pressure without panic?
3. Are shots high quality or just volume?
4. Is the goalkeeper likely to become a major variable?
5. Is the match being decided by structure, finishing, or variance?
6. What evidence would prove the favorite read wrong?

A team can dominate shots and still fail to win if the shots are low quality, rushed, blocked, or repeatedly saved.

---

## Low-Block Breaking Rating

Rate the stronger attacking team from 0-100.

Inputs:

- Half-space creators
- Through-ball quality
- Cutback creation
- Box occupation
- Late runners
- One-v-one dribblers
- Crossing quality
- Aerial targets
- Long-shot threat
- Set-piece threat
- Second-ball pressure
- Bench attackers

| Rating | Meaning |
|---|---|
| 0-20 | Very weak block breaking |
| 21-40 | Can dominate ball but struggles to create clear chances |
| 41-60 | Average; needs patience, set pieces, or individual quality |
| 61-80 | Strong; creates repeatable high-quality chances |
| 81-100 | Elite; can break compact blocks through multiple mechanisms |

---

## Sterile Possession Detector

Possession is sterile when a team has territory but lacks repeated high-quality entries.

Warning signs:

- Many passes but few touches in box
- Many shots but low xG per shot
- Shots from poor angles or distance
- Crosses without aerial superiority
- Slow circulation around the block
- Few cutbacks
- Key creator receives too deep
- Striker isolated or surrounded
- Corners without dangerous deliveries

If sterile-possession signs appear, downgrade goal expectation even if possession and shots are high.

---

## Goalkeeper Variance Check

Before calling an attacking forecast wrong, check whether the goalkeeper produced an outlier performance.

Ask:

- How many saves?
- Were saves routine or high difficulty?
- Did the keeper command crosses?
- Did the keeper stop clear chances?
- Did finishing placement help the keeper?
- Did the attacking team produce enough chance quality to normally score?

If the goalkeeper had an extreme performance, classify part of the result as variance, not purely tactical failure.

---

## Multi-Hypothesis Forecasting

Every serious match must test at least four hypotheses.

### H1 — Favorite Control Works

The favorite controls territory, creates repeatable high-quality chances, and wins.

Evidence needed:

- Box touches
- Cutbacks
- Big chances
- Shots on target from dangerous zones
- Weak defensive block behavior

### H2 — Sterile Possession Trap

The favorite controls territory but cannot break the block cleanly.

Evidence needed:

- Low xG per shot
- Slow circulation
- Poor box occupation
- Few central entries
- Crosses without target advantage

### H3 — Underdog Resilience

The underdog defends well enough to survive and frustrate the favorite.

Evidence needed:

- Compact spacing
- Strong goalkeeper
- Good central protection
- Low panic after pressure
- Clearances without chaos

### H4 — Chaos / Transition Punishment

The favorite overcommits and the underdog creates the bigger chances.

Evidence needed:

- High line exposure
- Slow rest defense
- Fast outlets
- Direct runs into space
- Tactical fouls or yellow-card risk

### H5 — Set-Piece Disruption

The match is decided by corners, free kicks, second balls, or penalty-box chaos.

Evidence needed:

- Repeated fouls near box
- Aerial mismatch
- Dangerous deliveries
- Poor goalkeeper command
- Rebounds or loose-ball pressure

---

## Commentary and Highlight Review

When full heatmaps are unavailable, use commentary and highlights carefully.

Extract:

- Where chances came from
- Whether saves were routine or exceptional
- Whether pressure was central or wide
- Whether the favorite created cutbacks or only crosses
- Whether the underdog countered with real threat
- Whether the goalkeeper changed the expected outcome
- Whether the crowd/game state created panic
- Whether substitutions changed mechanisms

Do not treat highlights as complete evidence. Highlights overrepresent drama and underrepresent sterile control.

---

## Post-Match Classification

After a surprising result, classify the main cause:

- Failed block breaking
- Goalkeeper outlier
- Poor finishing
- Low shot quality
- Strong underdog defensive structure
- Bad attacking selection
- Set-piece failure
- Transition fear reducing commitment
- Random variance

Multiple causes can be true. Do not force one explanation.

---

## Ecuador vs Curacao Lesson

Ecuador 0-0 Curacao showed why this module matters.

Known evidence from public reports:

- Ecuador had heavy shot volume.
- Curacao goalkeeper Eloy Room made a record-level save count.
- Curacao earned a historic first World Cup point after losing 7-1 to Germany.

Calibration interpretation:

- The Ecuador win forecast was too confident.
- The under-style environment was correct.
- Curacao were more resilient than the Germany scoreline suggested.
- Ecuador's issue may not be motivation; it may be block breaking, finishing, or goalkeeper variance.
- Future forecasts must test sterile possession and goalkeeper-outlier hypotheses before assuming the stronger team converts control into goals.

---

## Anti-Blind-Spot Rule

Always ask: `What would the underdog's successful match look like?`

If the answer is realistic, the favorite confidence must be reduced.
