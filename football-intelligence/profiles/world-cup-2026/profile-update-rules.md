# World Cup 2026 Profile Update Rules

Purpose: define how team, coach, and player profiles should be updated during the tournament without overfitting to one match.

---

## Core Rule

Update profiles from mechanisms, not scorelines.

A result can be misleading. Before updating a profile, ask:

1. Did the match show a repeatable mechanism?
2. Did stats support the visual/tactical read?
3. Did player movement confirm the role assumption?
4. Was the outcome driven by structure or variance?
5. Would this lesson have helped before the match?

---

## Team Profile Update Triggers

Update a team profile when:

- The same attacking route appears across matches.
- The same defensive weakness appears across matches.
- A team changes shape after lineup changes.
- A team repeatedly produces or allows similar shot profiles.
- A team consistently generates corners through a clear mechanism.
- A team repeatedly struggles after conceding first.
- A team repeatedly improves after substitutions.

Do not update strongly from:

- One deflected goal
- One red card
- One goalkeeper error
- One unusual penalty
- One opponent collapse without supporting data

---

## Coach Profile Update Triggers

Update a coach profile when:

- Substitution timing repeats.
- Risk appetite in similar game states repeats.
- The coach uses the same control method when leading.
- The coach consistently changes shape after halftime.
- The coach repeatedly targets a specific opponent weakness.

Do not assume coach behavior from country reputation.

---

## Player Profile Update Triggers

Update a player profile when:

- Heatmaps/touch maps show a stable role.
- The player repeatedly receives in the same zones.
- The player repeatedly acts as actual finisher or creator.
- The player repeatedly generates corners, fouls, or cards.
- Substitution impact repeats.
- A listed position does not match real role.

Do not update only because the player scored once.

---

## Evidence Weighting

| Evidence | Weight |
|---|---|
| Heatmap/touch map | High |
| Shot map/xG | High |
| Repeated match stats | High |
| Verified lineup/role | High |
| Manager quote | Medium/High |
| Single goal | Low/Medium |
| Scoreline only | Low |
| Reputation | Very low |

---

## Confidence Rules

- One match with full stats: profile confidence max 6.5/10.
- Two matches with matching mechanisms: profile confidence max 7.5/10.
- Three or more matches with stable mechanisms: profile confidence can reach 8/10.
- Without player movement data, cap player-role confidence at 6/10.
- Without verified coach identity, cap coach-behavior confidence at 5/10.

---

## Required Update Note

Every profile update should include:

```markdown
## Update Note

Date:
Match:
Evidence used:
Mechanism observed:
Repeatable or variance:
Confidence change:
Profile fields changed:
```

---

## Anti-Overfitting Rule

The tournament is short. Do not let one match overwrite long-term football logic unless the mechanism is clear and supported by data.
