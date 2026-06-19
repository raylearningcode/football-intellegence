# League Profiles — Contextual Reference

> Used to apply league-specific modifiers in the analytical framework.
> Update this file as empirical data accumulates.

---

## Premier League (England — Tier 1)

- Avg goals per match: ~2.75
- Home win rate: ~44%
- Draw rate: ~24%
- Away win rate: ~32%
- Home advantage modifier: +5% (standard)
- Tactical norm: High pressing, physical duels, fast transitions
- xG reliability: High (well-tracked)
- BTTS typical rate: ~52%
- Notes: Most unpredictable top league in Europe. Away wins very common vs expectation.

---

## La Liga (Spain — Tier 1)

- Avg goals per match: ~2.55
- Home win rate: ~46%
- Draw rate: ~27%
- Away win rate: ~27%
- Home advantage modifier: +6%
- Tactical norm: Possession-based, technical buildup, low PPDA elite teams
- xG reliability: High
- BTTS typical rate: ~46%
- Notes: Top-heavy competition. High draw rate for mid-table clashes.

---

## Bundesliga (Germany — Tier 1)

- Avg goals per match: ~2.95
- Home win rate: ~44%
- Draw rate: ~24%
- Away win rate: ~32%
- Home advantage modifier: +5%
- Tactical norm: High pressing, vertical play, high defensive lines
- xG reliability: High
- BTTS typical rate: ~55%
- Notes: Most goals per game of top 5 leagues historically. Overs market strong.

---

## Serie A (Italy — Tier 1)

- Avg goals per match: ~2.60
- Home win rate: ~45%
- Draw rate: ~28%
- Away win rate: ~27%
- Home advantage modifier: +6%
- Tactical norm: Defensive structure, late goals, tactical fouls
- xG reliability: Medium (defensive systems skew xGA)
- BTTS typical rate: ~44%
- Notes: Unders market historically stronger. VAR heavily influences results.

---

## Ligue 1 (France — Tier 1)

- Avg goals per match: ~2.55
- Home win rate: ~44%
- Draw rate: ~26%
- Away win rate: ~30%
- Home advantage modifier: +5%
- Tactical norm: Varied — physical and fast
- xG reliability: Medium
- BTTS typical rate: ~47%
- Notes: High variance outside top 3. Historically dominated by PSG skewing data.

---

## Champions League (UEFA)

- Avg goals per match: ~2.60 (Group) / ~2.40 (KO)
- Home win rate: ~44%
- Draw rate: ~26%
- Away win rate: ~30%
- Home advantage modifier: +4% (neutral/high-level away teams reduce it)
- Tactical norm: Ultra-cautious in KO rounds, explosive in group stage
- xG reliability: High
- BTTS typical rate: ~48%
- Notes: KO stage: unders lean in first legs. Away goals mindset matters (even post-rule change).

---

## FIFA World Cup 2026 (Group Stage, 48-team format)

> Added because every match logged in calibration-log.md to date is a World Cup 2026 fixture —
> this profile is derived from actual observed data across those matches, not external averages,
> and should be treated as a live, evolving baseline rather than a fixed historical figure.

- Sample size so far: ~10 matches (small — treat all figures below as provisional)
- Draw rate: notably HIGHER than typical domestic-league baselines — see Rule #13's hardcoded
  draw floors (22-32% depending on composite gap), which exist specifically because group-stage
  draws have been under-projected by default models that don't account for the format.
- Tactical norm: significant bus-parking / deep-block prevalence among underdogs in the early
  group stage (see h2h-patterns.md Pattern P6) — more pronounced than typical league play, likely
  because a single point has outsized qualification value in a 3-game group.
- Possession is LESS predictive of goals here than in domestic league play — see Pattern P1 (the
  Possession Paradox), repeatedly confirmed across multiple matches with different teams.
- Corners are the single hardest market to call in this tournament so far (28% accuracy) — high
  variance driven by game-state (early goals collapsing deep blocks, central vs. wide build-up
  styles) rather than stable team averages. See Patterns P5 and Rules #7/#10/#11/#16.
- Favorite blowout margins have been under-projected multiple times (Germany 7-1, Argentina 3-0,
  Canada 6-0) — see Pattern P3. Consider wider upside variance on score margin for composite
  gaps > 25 once more data confirms this isn't a small-sample fluke.
- Heat/altitude factors are genuinely relevant given host countries (Mexico, USA, Canada) and
  should be checked per-venue, not assumed uniform across the tournament (e.g., Guadalajara's
  altitude/heat profile differs meaningfully from Seattle's).
- Referee pool is drawn from multiple confederations with varying card-rate baselines (e.g.,
  Gustavo Tejera's personal ~5 cards/game average is well above several other assigned referees
  in this tournament) — always check the specific assigned referee's individual rate rather than
  assuming a single tournament-wide card baseline.
- Bracket/standings context matters more here than in a single round-robin league table — see
  Rule #22. A draw can be a genuinely good result for one or both sides depending on group
  position, and this changes expected match aggression in ways a generic "motivation" score misses.

### Calibration Notes (World Cup-specific)
- Re-derive these figures from calibration-log.md's Match Log after every 5 additional matches.
- Do NOT treat this section as a stable baseline the way the major-league profiles above are
  treated — it is explicitly provisional and should be the fastest-updating section in this file.

---

## General Calibration Notes (applies to all leagues above)

- These are baseline figures. Team-specific data always overrides league averages.
- Update after every 10 matches in each league with observed averages.
