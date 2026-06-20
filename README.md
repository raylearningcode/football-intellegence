# Football Intelligence

A self-improving football (soccer) match prediction and betting-analysis system, built as a
Claude Skill. This repo is the durable backup of that skill — see "Why this repo exists" below.

## What's in here

```
football-intelligence/
├── SKILL.md                          ← the actual skill: phases, framework, output format
└── references/
    ├── calibration-log.md            ← the system's memory: rules, weights, match history
    ├── h2h-patterns.md               ← recurring tactical/psychological patterns across matches
    └── league-profiles.md            ← league/tournament baseline stats (goals, draw rate, etc.)
```

**Start with `calibration-log.md`** if you want the fastest overview of what this system has
actually learned — it has the full rule list, the running accuracy stats, and the match-by-match
history that everything else is derived from.

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

As of the last sync: **v2.5**, 11 matches fully logged across FIFA World Cup 2026 (all FINAL, none
pending), 28 active calibration rules. Match-winner accuracy 82% (9/11), Over/Under 2.5 at 73%
(8/11), BTTS at 67% (6/9). Corners remain the weakest GRADED market (28%), but Rule #11's actual
audit process is now 3/3 when properly applied (Mexico-Korea, Scotland-Morocco, Netherlands-
Sweden) — the lesson is "pull real team-specific corner data first," not "corners are
unpredictable." New Pattern P8 (goals/corners decoupling at the extremes — even a 5-1 blowout
produced only 6 corners). Favorite-margin-variance now has 4 confirmed instances (Germany 7-1,
Argentina 3-0, Canada 6-0, Netherlands 5-1) and is flagged as the top-priority item to formalize
into a real numeric rule next. See `calibration-log.md`'s Reconciliation TODO for the full list
of open items.

## Using this elsewhere

If you're running this skill in a fresh Claude session (web, desktop, or API) and it doesn't
already have these files loaded: paste the contents of `SKILL.md` as a system/project instruction,
and feed in `calibration-log.md` + `h2h-patterns.md` + `league-profiles.md` as reference context
before asking for a match analysis. The skill is designed to read its own calibration log first
(Phase 0) before doing anything else.
