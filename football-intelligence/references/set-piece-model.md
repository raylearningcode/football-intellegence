# Set-Piece Model — Dead-Ball Threat and Defensive Weakness Engine

Purpose: model set pieces as a separate scoring and pressure mechanism from open play. This is especially important for underdogs, low-possession teams, and tournament matches where one corner, free kick, or long throw can change the entire forecast.

---

## Core Principle

Set-piece threat must be priced separately from open-play xG.

A team can have weak open-play creation but still carry meaningful scoring danger through:

- Corners
- Wide free kicks
- Direct free kicks
- Long throws
- Second balls
- Goalkeeper spills
- Aerial mismatches
- Penalty-box chaos

Do not let low possession or low open-play xG erase set-piece risk.

---

## Required Set-Piece Audit

For both teams, document:

### Attacking Set Pieces

- Corner taker quality
- Free-kick taker quality
- Delivery style: inswing, outswing, driven, floated, short routine
- Primary aerial targets
- Secondary runners
- Rebound/second-ball players
- Long throw usage
- Penalty taker
- Recent set-piece goals or big chances

### Defensive Set Pieces

- Aerial duel strength
- Marking scheme: zonal, man, mixed
- Goalkeeper command of area
- Near-post weakness
- Far-post weakness
- Second-ball weakness
- Fouls conceded near box
- Penalty concession risk

---

## Set-Piece Threat Rating

Score each team 0-100.

| Score | Meaning |
|---|---|
| 0-20 | Minimal dead-ball threat |
| 21-40 | Low threat; needs error or lucky bounce |
| 41-60 | Average threat; can matter in tight games |
| 61-80 | Strong threat; must affect goal and BTTS estimates |
| 81-100 | Elite threat; can define the match plan |

---

## Set-Piece Modifiers

### Modifier S1 — Underdog Set-Piece Tail

When an underdog has strong aerial targets or delivery, increase their scoring tail even if open-play projection is low.

This does not mean the underdog is likely to score. It means clean-sheet confidence should be reduced.

### Modifier S2 — Favorite Defensive Complacency

Favorites that dominate possession can still concede if they give away cheap wide free kicks or corners. Territory dominance does not remove dead-ball risk.

### Modifier S3 — Corner Quantity vs Corner Quality

High corner count is not the same as high set-piece threat. Separate:

- How many corners a team is likely to win
- How dangerous those corners are

A team can win many low-quality corners. Another can score from only two high-quality deliveries.

### Modifier S4 — Second-Ball Teams

Some teams are more dangerous on loose balls than first contact. Track box crashers, late midfield runners, and rebound shooters.

### Modifier S5 — Goalkeeper Spill Risk

If a goalkeeper has poor handling under crosses or wet conditions, increase second-ball and rebound probability.

---

## Required Output Section

Every report must include:

```markdown
## Set-Piece Audit

Team A attacking set-piece threat:
Team A defensive set-piece risk:
Team B attacking set-piece threat:
Team B defensive set-piece risk:
Most dangerous dead-ball mismatch:
Clean-sheet confidence adjustment:
```

---

## Live Set-Piece Update

If live match data is available, update using:

- Current corners
- Wide free kicks
- Fouls near box
- Aerial duel outcomes
- Goalkeeper handling
- Marking failures
- Repeated near-post/far-post targets

If a team is repeatedly winning dangerous dead-ball situations, raise scoring tail even before xG fully reflects it.

---

## Anti-Blind-Spot Rule

Open-play dominance and set-piece vulnerability can coexist.

A favorite can control 70% possession and still concede from one corner. A model that ignores set pieces will overstate clean-sheet confidence and understate underdog scoring tails.
