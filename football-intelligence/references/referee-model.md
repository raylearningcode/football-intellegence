# Referee Model — Match Flow, Discipline, and Penalty Risk

Purpose: model how the referee affects match flow, discipline, penalties, and tactical behavior. Referee analysis should not be a generic card average; it should explain how the referee's style interacts with the specific match.

---

## Core Principle

A referee changes incentives.

The same tactical matchup can produce a different match depending on whether the referee:

- Allows physical contact
- Stops play frequently
- Gives early cards
- Protects attackers
- Punishes tactical fouls
- Awards penalties often
- Lets advantage continue

Referee profile affects tempo, cards, pressing, transition defense, and penalty probability.

---

## Required Referee Inputs

When available, collect:

- Average yellow cards per match
- Average red cards per match
- Penalties awarded per match
- Fouls called per match
- Advantage-play tendency
- Early-card tendency
- Home/away bias indicators if relevant
- Competition-level experience
- Recent match style

If referee is unknown, state it and cap card/penalty confidence.

---

## Referee Style Types

### Type R1 — Strict Controller

Characteristics:

- Early yellow cards
- Frequent whistles
- Low tolerance for tactical fouls
- High impact on pressing teams

Model effects:

- Card expectation rises
- Pressing intensity may drop after early bookings
- Set-piece volume may rise
- Flow can become broken

### Type R2 — Advantage Referee

Characteristics:

- Lets play continue
- Allows physical duels
- Fewer stoppages
- Higher transition continuity

Model effects:

- Fewer cards unless match becomes emotional
- Higher transition flow
- Fewer dead-ball interruptions
- More open-play rhythm

### Type R3 — Penalty-Prone Referee

Characteristics:

- High penalty rate
- Strict box-contact interpretation
- VAR involvement tendency

Model effects:

- Goal distribution gains a penalty tail
- Defensive teams under pressure carry extra risk
- Dribblers in box become more important

### Type R4 — Lenient Until Late

Characteristics:

- Lets early fouls go
- Cards accumulate after repeated fouls
- Match can become heated before discipline arrives

Model effects:

- Late cards rise
- Injury/frustration risk rises
- Early match may be more physical than expected

---

## Tactical Interaction Rules

### Rule R1 — High Press vs Strict Referee

High pressing teams are more vulnerable to early cards under strict referees. If a key midfielder or fullback is booked early, pressing and duel intensity may drop.

### Rule R2 — Counterattacks vs Tactical Fouls

If one team relies on counters and the opponent uses tactical fouls, a strict referee can protect the countering team and raise card risk for the favorite.

### Rule R3 — Box Dribblers vs Penalty Risk

Teams with elite dribblers entering the box gain more penalty tail against penalty-prone referees.

### Rule R4 — Emotional Stakes Need Foul Evidence

High stakes do not automatically mean many cards. Card confidence requires foul style, referee tendency, and game-state aggression.

---

## Required Output Section

Every report must include:

```markdown
## Referee Flow Read

Referee style:
Data confidence:
Team helped by referee style:
Team hurt by referee style:
Card expectation:
Penalty tail:
Main uncertainty:
```

---

## Live Referee Update

If live data is available, update using:

- Fouls called
- Cards shown
- Warning patterns
- Penalty/VAR incidents
- Player reactions
- Whether advantage is being played

If the referee is calling the game differently than historical average, live behavior overrides pre-match profile.

---

## Anti-Blind-Spot Rule

Do not project cards from stakes alone. Stakes, referee style, foul profile, and game state must all align before making a high-discipline forecast.
