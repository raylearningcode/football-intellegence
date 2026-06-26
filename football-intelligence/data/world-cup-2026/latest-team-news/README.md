# Latest Team News Cache

**Created:** 2026-06-26

This folder stores fast, source-backed team-news snapshots for upcoming World Cup 2026 matches.

Use this only for current, match-relevant information:

- official lineups,
- confirmed injuries,
- suspensions,
- players protected from yellow-card suspension,
- coach quotes,
- rotation hints,
- tactical hints,
- venue/weather notes,
- trusted live-blog or wire-service updates.

Do not store rumors as model-driving facts.

## Filename format

```text
YYYYMMDD-team-vs-opponent-news.yaml
```

Example:

```text
20260626-new-zealand-vs-belgium-news.yaml
```

## Required schema

```yaml
match:
  date:
  team_a:
  team_b:
  competition:
  stage:
  kickoff:
  venue:

team_news:
  team_a:
    checked_at:
    source_grade: A | B | C | D | X
    confirmed_lineup:
    injuries:
    suspensions:
    rotation_risk:
    coach_quotes:
    tactical_hints:
    model_impact:
  team_b:
    checked_at:
    source_grade: A | B | C | D | X
    confirmed_lineup:
    injuries:
    suspensions:
    rotation_risk:
    coach_quotes:
    tactical_hints:
    model_impact:

sources:
  - provider:
    url_or_reference:
    retrieved_at:
    confidence:
```

## Analysis rule

Before every serious prediction, check this folder first. If no current news file exists, perform a fresh latest-news search and create one if the news affects analysis.
