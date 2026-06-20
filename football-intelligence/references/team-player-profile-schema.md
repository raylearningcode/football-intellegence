# Team and Player Profile Schema — Durable Football Memory

Purpose: create reusable team and player intelligence profiles so the model learns beyond one match. This schema stores team mechanisms, player movement, role behavior, strengths, weaknesses, and calibration notes.

---

## Core Principle

A team profile should not say only whether a team is good or bad. It should explain *how* the team creates chances, prevents chances, reacts to game states, and which players drive those mechanisms.

A player profile should not say only position and reputation. It should explain actual role, movement, receiving zones, finishing behavior, defensive work, and how the player changes markets and match dynamics.

---

## Team Profile Template

```markdown
# Team Profile: [Team]

Last updated:
Sample period:
Evidence quality:

## Team Identity

Base formation:
In-possession shape:
Out-of-possession shape:
Press height:
Tempo:
Build-up style:
Directness:
Risk appetite:

## Attacking Mechanisms

Primary chance route:
Secondary chance route:
Main creator(s):
Actual finisher(s):
Box runners:
Wide overload mechanism:
Central combination mechanism:
Transition mechanism:
Set-piece mechanism:

## Defensive Mechanisms

Defensive block:
Press trigger:
Rest defense:
Weak zone:
Set-piece weakness:
Transition weakness:
Goalkeeper profile:

## Game-State Behavior

When level:
When leading:
When trailing:
After early goal:
After conceding first:
Late-game behavior:

## Statistical Profile

Average possession:
Shots for:
Shots against:
Shots on target for:
Shots on target against:
Corners for:
Corners against:
Fouls/cards:
xG for:
xG against:

## Reliability Notes

What is repeatable:
What may be variance:
What depends on opponent:
What depends on lineup:

## Calibration Notes

Lessons learned:
Model modifiers:
Confidence notes:
```

---

## Player Profile Template

```markdown
# Player Profile: [Player]

Team:
Position listed:
Actual role:
Sample period:
Evidence quality:

## Movement Profile

Main receiving zones:
Main carry zones:
Average position tendency:
Box entry frequency:
Wide/central tendency:
Depth tendency:
Off-ball runs:
Pressing zones:
Defensive recovery zones:

## Attacking Role

Creator / finisher / connector / runner / target / chaos player:
Shot locations:
Assist zones:
Key-pass zones:
Crossing zones:
Combination partners:
Set-piece role:
Penalty role:

## Forecast Impact

Goal probability modifier:
Assist probability modifier:
Team shot-quality modifier:
Corner modifier:
Transition modifier:
Pressing modifier:
Defensive risk modifier:

## Game-State Behavior

When team leads:
When team trails:
When opponent sits deep:
When opponent presses high:
Against physical defenders:
Against high line:

## Reliability Notes

What is repeatable:
What depends on opponent:
What depends on tactical role:
What is likely variance:

## Calibration Notes

Past forecast hits:
Past forecast misses:
Lessons:
```

---

## Profile Update Rules

Update a profile when:

- A movement pattern repeats across matches
- A player role changes under a new coach
- A team changes formation or pressing behavior
- A substitution pattern becomes predictable
- A statistical trend matches the visual/tactical read
- A calibration error reveals a missing mechanism

Do not update a profile from one isolated event unless it explains a repeatable mechanism.

---

## Anti-Blind-Spot Rule

Profiles must separate reputation from current role. A famous attacker may be acting as a connector. A less famous player may be the actual finisher. The model must learn current function, not only name value.
