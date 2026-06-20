# Player Movement Model — Heatmap, Role, and Mechanism Intelligence

Purpose: teach the framework to learn *how players actually move* and how those movements create or suppress chances, corners, defensive exposure, and scoring probability. Team formations and box-score stats are not enough. The model must study player heatmaps, touch maps, pass maps, carry maps, shot maps, and role behavior.

---

## Core Principle

A formation is only the starting shape. The real match is created by player movement.

Before trusting a team-level read, identify:

- Where each key player receives the ball
- Where each key player carries the ball
- Who attacks the box
- Who stays wide
- Who underlaps or overlaps
- Who drops to connect midfield
- Who makes late runs
- Who creates chaos but does not finish
- Who is the actual finisher
- Which defender is being targeted
- Which player breaks the team structure when possession is lost

Do not confuse nominal position with actual role.

---

## Required Data Sources

When available, collect:

- Player heatmaps
- Touch maps
- Pass networks
- Progressive carry maps
- Shot maps
- Key-pass zones
- Cross locations
- Average positions
- Defensive action maps
- Aerial duel zones
- Substitution impact maps

If these are unavailable, use match reports and video observations, but mark confidence lower.

---

## Player Role Audit

For each key player, classify the actual role:

| Role | Description | Forecast Impact |
|---|---|---|
| Touchline winger | Stays wide, isolates fullback | Raises crossing/corner potential |
| Inverted winger | Cuts inside into shooting or passing lanes | Raises shot/assist potential, may reduce corner volume |
| Half-space creator | Receives between lines | Raises chance creation and through-ball threat |
| Box finisher | Main target for final action | Raises scoring probability |
| False nine | Drops to connect play | Can reduce striker-shot volume but raise creator output |
| Late-run midfielder | Arrives into box after marking shifts | Undervalued scoring threat |
| Overlap fullback | Provides width outside winger | Raises crossing and corner potential |
| Inverted fullback | Moves into midfield | Raises control, may reduce wide corner mechanism |
| Deep playmaker | Controls progression from deeper zones | Raises possession stability, not necessarily xG |
| Ball-winner | Disrupts transitions | Reduces opponent counter threat |
| Target forward | Aerial outlet and set-piece threat | Raises direct-play and set-piece tail |

---

## Heatmap Interpretation Rules

### Rule PM1 — Heatmap Beats Listed Position

A player listed as a winger may act as a striker, creator, or touchline crosser depending on movement. Use heatmap and touch zones to identify actual function.

### Rule PM2 — Creator vs Finisher Separation

The most dangerous player is not always the best scoring pick. Separate:

- Chance creator
- Chaos generator
- Final-shot taker
- Box finisher
- Rebound attacker

A player who creates goalkeeper spills, own goals, or deflections may be better for involvement analysis than pure scorer projection.

### Rule PM3 — Corner Mechanism Depends on Movement

Corner projection must come from movement patterns, not just possession.

Corner-positive patterns:

- Touchline winger repeatedly attacking outside
- Overlapping fullback crossing from byline
- Repeated blocked crosses
- Underdog defending deep in wide zones
- Box crowded with aerial targets

Corner-negative patterns:

- Inverted wingers cutting inside early
- Central combinations
- Low shot volume from distance
- Early clinical goals reducing wide pressure
- Possession recycling without box entry

### Rule PM4 — Offside Count Reveals Run Timing

High offside count can reveal vertical runs behind the defensive line. It may indicate:

- Aggressive forward runs
- Poor timing
- High defensive line vulnerability
- Direct through-ball strategy

Do not ignore offsides; they are movement data.

### Rule PM5 — Shot Map Quality Over Shot Count

Shot count alone is weak. Identify:

- Location
- Body part
- Pressure level
- First-time vs controlled shot
- Assisted vs individual shot
- Rebound/second-ball context

### Rule PM6 — Defensive Heatmap Matters

A fullback or midfielder repeatedly dragged out of zone can create structural weaknesses even if not directly involved in goals.

Track:

- Isolated fullback
- Defensive midfielder pulled wide
- Center-back forced into channels
- Winger not tracking runner
- Back post left open

---

## Team Mechanism Audit

Every serious report must include:

```markdown
## Player Movement Audit

Team A key movement patterns:
Team A main chance-creation zones:
Team A actual finisher(s):
Team A chaos creator(s):
Team A corner-generation mechanism:
Team A defensive movement weakness:

Team B key movement patterns:
Team B main chance-creation zones:
Team B actual finisher(s):
Team B chaos creator(s):
Team B corner-generation mechanism:
Team B defensive movement weakness:
```

---

## Post-Match Movement Review

After the match, compare predicted movement with actual movement:

- Did the key creator receive in expected zones?
- Did the finisher get enough box touches?
- Did wide players stay wide or invert?
- Did fullbacks overlap or stay conservative?
- Did the opponent target a specific defender?
- Did offsides reveal a vertical attack pattern?
- Did corners come from the predicted mechanism?
- Did goals come from movement, finishing quality, or errors?

---

## Calibration Lessons From Brazil vs Haiti Type Matches

A 3-0 scoreline does not automatically mean territorial domination.

If a team wins with limited shot volume but high conversion, classify the mechanism as:

- Clinical finishing
- Efficient movement
- Defensive failure on key actions

Do not upgrade the team's general chance-creation model unless heatmaps, shot maps, and repeated entries show sustained creation.

Likewise, if corner count is balanced despite a large scoreline, do not assume dominance created corner pressure. Check whether the favorite scored through central or direct actions rather than repeated wide siege.

---

## Anti-Blind-Spot Rule

Never analyze only the team. Learn the players.

Team identity is the sum of player movement, spacing, roles, and repeated mechanisms. A model that ignores heatmaps will overrate formations and underrate how goals are actually created.
