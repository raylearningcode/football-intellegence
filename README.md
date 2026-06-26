# Football Intelligence

A self-improving football (soccer) match prediction and betting-analysis system, built as a
Claude Skill. This repo is the durable backup of that skill — see "Why this repo exists" below.

## What's in here

```
football-intelligence/
├── SKILL.md                          ← the actual skill: phases, framework, output format
├── references/
│   ├── calibration-log.md            ← the system's memory: rules, weights, match history
│   ├── h2h-patterns.md               ← recurring tactical/psychological patterns across matches
│   ├── league-profiles.md            ← league/tournament baseline stats (goals, draw rate, etc.)
│   ├── event-data-source-integration-plan.md
│   ├── event-data-schema-v1.md
│   ├── monte-carlo-simulation-v4.md
│   ├── model-validation-and-calibration-v1.md
│   └── feature-registry-v1.yaml
└── templates/
    ├── match-analysis-template-v4.md
    └── post-match-reconciliation-template.yaml
```

**Start with `calibration-log.md`** if you want the fastest overview of what this system has
actually learned — it has the full rule list, the running accuracy stats, and the match-by-match
history that everything else is derived from.

For model-development work, also read the v3.1 architecture files:

1. `references/event-data-source-integration-plan.md` — which data sources to collect and how to avoid fake completeness.
2. `references/event-data-schema-v1.md` — unified schema for events, shots, set pieces, tracking, and model-ready features.
3. `references/monte-carlo-simulation-v4.md` — scenario-weighted, uncertainty-aware simulation design.
4. `references/model-validation-and-calibration-v1.md` — Brier/log-loss/calibration/backtesting rules.
5. `references/feature-registry-v1.yaml` — feature list, sources, leakage rules, and confidence caps.
6. `templates/match-analysis-template-v4.md` — required structure for future match reports.
7. `templates/post-match-reconciliation-template.yaml` — required structure for verified post-match logging.

## How it works

1. **Pre-match:** the skill runs a 16-dimension weighted analysis (form, tactics, player
   availability, advanced metrics, motivation/bracket context, fatigue, H2H, referee, weather,
   market signals, etc.) and produces probabilities for match winner, correct score, goal totals,
   BTTS, and player props, plus a Monte Carlo cross-check.
2. **Live (if applicable):** in-game state (goals, cards, possession swings) triggers a re-read of
   the goals/cards/corners markets using rules learned from prior matches — see the "Live /
   In-Game Rules" section of `calibration-log.md`.
3. **Post-match:** predicted vs. actual is logged, errors are root-caused, and new calibration
   rules or weight adjustments are derived and added to the log — this is what makes the system
   "self-improving" rather than a static formula.
4. **v3.1+ data discipline:** missing official stats stay missing until verified. The model should
   improve by adding source-backed event data, schemas, validation, and simulation—not by guessing.

## Why this repo exists

The skill's calibration memory broke more than once because it was writing to `/tmp/...`, which
is wiped between sessions, while the durable skill folder lived somewhere else entirely. Weeks of
learned rules and match history quietly evaporated each session while the reference files stayed
frozen at their original template state. This is documented in detail in the "File-Location
Incident" section near the top of `calibration-log.md` — read it before assuming any given
session's "it's updated now" claim is actually true.

This GitHub repo is the fix: a location that persists independently of whichever sandbox or
session last touched the skill. **If you're starting a new session and want Claude to pick up
where this left off, point it at this repo first**, or paste in the contents of
`calibration-log.md` directly.

## Current state (update this line whenever you sync)

As of the last sync: **v3.1 architecture update**, additive model-improvement docs have been added
for event-data sources, event schema, Monte Carlo v4, validation/calibration, feature registry, and
new analysis/reconciliation templates. The repo still should not claim all World Cup 2026 detailed
stats are complete: most missing official xG, corners, cards, lineups, referee, and event fields
must remain `null` or `missing_official_stats` until verified from official or trusted match-centre
sources. The next real data task is to reconcile priority matches using the new template, beginning
with rule-creating or model-failure cases such as Jordan-Algeria, Belgium-Iran, Portugal-DR Congo,
Canada-Qatar, Netherlands-Sweden, Germany-Curacao, England-Ghana, and Switzerland-Canada.

## Using this elsewhere

If you're running this skill in a fresh Claude session (web, desktop, or API) and it doesn't
already have these files loaded: paste the contents of `SKILL.md` as a system/project instruction,
and feed in `calibration-log.md` + `h2h-patterns.md` + `league-profiles.md` as reference context
before asking for a match analysis. The skill is designed to read its own calibration log first
(Phase 0) before doing anything else.

For serious predictions after the v3.1 update, also load:

- `event-data-source-integration-plan.md`
- `event-data-schema-v1.md`
- `monte-carlo-simulation-v4.md`
- `model-validation-and-calibration-v1.md`
- `feature-registry-v1.yaml`
- `match-analysis-template-v4.md`
