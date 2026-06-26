# Latest Team News Protocol v1

**Created:** 2026-06-26  
**Purpose:** make every future analysis faster and more current by forcing a compact latest-news pass before tactical prediction.

---

## 0. Why this exists

Football analysis becomes stale quickly. Lineups, injuries, suspensions, coach quotes, weather, travel, and tactical hints can change the model more than historical form.

Every serious analysis must include a **latest-team-news pass** before probabilities.

---

## 1. Mandatory latest-news search order

For each team, search in this order:

```text
1. Official team/federation account or website
2. Competition official match centre
3. Reuters / AP / BBC / Guardian / ESPN match preview or live blog
4. Trusted local beat reporters
5. Club/team press conference quotes
6. Injury/suspension aggregators only as secondary support
7. Social media only if official or corroborated
```

---

## 2. What to collect

For every team:

```yaml
latest_team_news:
  team:
  checked_at:
  match:
  sources:
    - provider:
      url_or_reference:
      source_grade: A | B | C | D | X
      retrieved_at:
  squad_status:
    confirmed_absences:
      - player:
        reason: injury | suspension | illness | personal | tactical | unknown
        expected_impact: 1-10
        replacement:
    doubts:
      - player:
        issue:
        probability_to_start:
    returns:
      - player:
        status:
  lineup_signals:
    confirmed_xi_available: true|false
    expected_shape:
    rotation_risk:
    players_on_yellow_card_risk:
  coach_quotes:
    objective:
    risk_appetite:
    rotation_hint:
    tactical_hint:
  tactical_news:
    press_height_hint:
    defensive_shape_hint:
    set_piece_hint:
    transition_hint:
  environment_context:
    travel:
    rest_days:
    weather:
    pitch:
  model_impact:
    side_market:
    goals_market:
    corners_market:
    cards_market:
    player_props:
    confidence_cap:
```

---

## 3. Source grading

| Grade | Meaning | Examples | Model effect |
|---|---|---|---|
| A | Direct official/current | Official lineup, federation post, FIFA match centre | Can move probabilities strongly |
| B | Trusted current indirect | Reuters lineup report, AP preview, BBC injury report | Can move probabilities moderately |
| C | Current but incomplete | Live blog note, local reporter, partial press quote | Small modifier or watch item |
| D | Weak/uncorroborated | Fan account, rumor, old article | Do not anchor |
| X | Unknown | No source found | Cap confidence |

---

## 4. Fast analysis checklist

Before producing picks, answer:

```text
[ ] Did either team rotate?
[ ] Is any key creator/finisher/defensive anchor missing?
[ ] Are any players protected from suspension?
[ ] Did coach signal risk appetite?
[ ] Is the team already qualified/eliminated?
[ ] Is the match in heat/rain/wind/altitude?
[ ] Did odds move after team news?
[ ] Does the news affect side, goals, corners, cards, or player props differently?
```

---

## 5. Market-specific news effects

### Side market

Upgrade/downgrade based on:

```text
key absences
rotation
midfield control
defensive anchor missing
goalkeeper change
motivation/bracket clarity
```

### Goals market

Upgrade/downgrade based on:

```text
attacking rotation
defensive absences
weather
coach risk appetite
draw utility
finishing quality
```

### Corners market

Upgrade/downgrade based on:

```text
wide players starting
set-piece takers starting
target forward starting
opponent low block
fullback rotation
first-goal branch
```

### Cards market

Upgrade/downgrade based on:

```text
referee strictness
players on suspension risk
tactical foul routes
emotional rivalry
must-win chase
late-game desperation
```

### Player props

Upgrade/downgrade based on:

```text
confirmed lineup
minutes risk
role
set-piece duty
opponent matchup
coach rotation quote
```

---

## 6. Speed workflow for future match requests

When the user asks for analysis:

```text
1. Identify match and kickoff time.
2. Pull current standings/bracket.
3. Search latest news for Team A.
4. Search latest news for Team B.
5. Search lineups if within lineup-release window.
6. Search referee/weather/venue.
7. Search odds only if betting/value is requested.
8. Apply confidence caps.
9. Run v3.2/v4 analysis workflow.
10. Store notable verified news into team-news cache if it affects future matches.
```

---

## 7. Team-news cache policy

Create/update files under:

```text
football-intelligence/data/world-cup-2026/latest-team-news/
```

Suggested filename:

```text
YYYYMMDD-team-vs-opponent-news.yaml
```

Only save:

- official or trusted current news,
- lineup reports,
- injury/suspension notes,
- coach quotes,
- tactical hints,
- verified weather/venue context.

Do not save rumors unless marked as `D` and not used for strong conclusions.

---

## 8. Required final note in every analysis

Every analysis should include:

```text
Latest-news confidence:
- Strong: official lineup/team news checked.
- Medium: trusted preview/news checked but lineups not confirmed.
- Low: no current team news; analysis relies on older profiles.
```

This keeps the model honest and fast.
