# Head-to-Head & Recurring Patterns — Reference

> Referenced by SKILL.md's PHASE 0 and REFERENCES section. This file was originally created in an
> earlier session, lost to the same `/tmp` persistence bug documented in calibration-log.md's
> "File-Location Incident" section, and is being restored here. Its original content has been
> folded into calibration-log.md's "Patterns Under Monitoring" section as well, for redundancy —
> if one copy is ever lost again, the other should still have the core findings.

Two kinds of content live here:
- **(A) Cross-match TACTICAL/PSYCHOLOGICAL patterns** that recur regardless of which specific
  teams are playing — these are the high-value, reusable lessons.
- **(B) Specific fixture head-to-head records** (2022+ only, per Rule #18's 4-year data cap).

---

## (A) Recurring Patterns

### P1 — The Possession Paradox
Territorial dominance does not equal goal probability against a compact or disciplined opponent.
Shots-per-possession is the metric that matters, not raw possession % or raw shot count.

**Evidence:**
- Portugal 75% possession / 7 shots / drew DR Congo 1-1
- DR Congo 25% possession / 8 shots / same match — 3x more efficient per unit of possession
- South Korea 58% possession / 9 shots / lost to Mexico 0-1
- USA 56-44% possession-and-touch dominance over Paraguay, but actually won FEWER corners (5 to 8)

**Action:** When expected possession > 65% vs. a confirmed deep block, apply a −20%
goal-probability discount to the favorite. See Rule #14, #15 in calibration-log.md.

### P2 — The Study Phase
Closely matched sides often feel each other out in the first half of a tournament opener, then
open up significantly after the half-time reset. This collapses when the quality gap between the
teams is large — the stronger side attacks from the opening whistle instead.

**Evidence (Study Phase held):** France-Senegal 0-0 at HT despite France winning 3-1 overall;
Mexico-Korea 0-0 at HT, the eventual winner not scored until the 50th minute.
**Evidence (Study Phase collapsed, large gap):** Norway-Iraq H1 already 2-1.

### P3 — Favorite Margin Variance (systematically under-projected) *(4 confirmed instances — strong candidate for promotion to a numeric rule)*
Heavy favorites blow past the model's central score projection more often than expected.

**Evidence:** Germany 7-1, Argentina 3-0 (Messi hat-trick), Canada 6-0, Netherlands 5-1 (Sweden).
**Candidate fix:** add an explicit upside-variance term for composite gaps > 20-25 points — four
confirmed instances now makes this a load-bearing finding, not a tentative pattern. See
calibration-log.md's Reconciliation TODO for the open task to formalize this into a numbered rule.

### P4 — The Decider Is Often an Error, Not Clean xG
In low-event, tightly-matched games specifically, the winning goal frequently comes from a
goalkeeper or defensive mistake rather than a clearly superior attacking sequence. **But this is
NOT universal** — when one team is genuinely stronger and that strength shows up immediately
(rather than the match being a true coin-flip), the outcome can match the underlying xG cleanly.

**Evidence (error-driven, xG inverted from result):** Luis Romo's winner for Mexico came directly
off a Kim Seung-gyu goalkeeper error, not a clear Mexican attacking move — confirmed by the deep
xG review showing Korea (0.67 xG) actually out-created Mexico (0.48 xG) in that match.

**Evidence (clean quality gap, xG matches result):** Morocco's win over Scotland came from a
genuine defensive lapse exploited by superior individual quality (Saibari finishing a Díaz
through-ball after Grant Hanley was caught out) just 71 seconds in — but unlike the Mexico-Korea
case, the underlying xG (Scotland 0.54, Morocco 0.97) matched the eventual scoreline direction.
Scotland finished the match without a single shot on target — this was a competence gap showing
up early and compounding, not a coin-flip decided by one freak moment.

**Action:** In tight matchups (composite gap small, Rule #27 confidence cap applies), expect the
P4 error-driven pattern. In matchups with a real, even if modest, quality gap, don't assume every
early goal is "just an error" — check whether the underlying chance quality and game state support
the goal being the start of a deserved result, not a freak one-off. The distinguishing question:
did the trailing team generate a meaningful response afterward, or did the gap compound (zero
shots on target for 90 minutes is a compounding-gap signal, not bad luck)?

### P5 — Corner Volume Is Game-State Dependent, Not Just Season-Average Dependent
Corners depend heavily on the specific game state and each team's individual attacking
mechanism — not just on plugging in season-average corners-per-game figures.

**Drivers, observed across matches:**
- An early goal (inside ~20') dissolves the deep block being defended against → corners for the
  leading side drop 30-40% relative to the pre-goal projection (Rule #10).
- Both teams building centrally rather than wide → reduce total corner projection by ~3 (Rule #16).
- A genuinely low-tempo, low-event game can produce near-zero corners regardless of pre-match
  projections (Mexico-Korea: 2 total corners across the full match).
- A lopsided match where one team is pinned back for long stretches can produce extreme volume
  for the dominant side (Canada 18 corners to Qatar's 1).
- An underdog that presses high/mid rather than sitting in a deep block generates 30-35% FEWER
  corners than a passive deep-block team would, because there's less sustained territorial siege.

**Action:** Always model each team's corner-generation mechanism individually (Rule #7), verify
actual recent crossing/corner counts rather than relying on a tactical description alone
(Rule #11), and check the live game state before assuming a pre-match corner projection still
holds once the score changes.

### P6 — The Bus-Parking Meta (tournament-wide observation, first 4 matches)
Across the earliest matches analyzed, full bus-parking (5-3-2 deep block + pure counter-attack)
outperformed aggressive mid-press as an underdog strategy specifically against elite favorites.

**Evidence:**
- Algeria vs. Argentina: nearly parked the bus, lost 0-3 to a Messi hat-trick, but kept it
  competitive for long stretches before Argentina's class told.
- DR Congo vs. Portugal: full bus park, drew 1-1 — bus-parking won a point outright.
- Iraq vs. Norway: aggressive mid-press (NOT bus-parking) → more open game, lost 1-3.
- Senegal vs. France: partial press → lost 1-3, more goals conceded than the full-park sides.

**Caveat:** this is a small, early-tournament sample (4 matches) and should be re-tested as more
data accumulates — it is a real, evidenced pattern but not yet a large-sample statistical certainty.

### P7 — Creator vs. Finisher (anytime-scorer props)
A team's most dangerous, most heavily-involved attacking player is not automatically the same bet
as "most likely to actually score" when their primary threat is creating chaos/pressure rather
than taking the shot themselves.

**Evidence (confirmed independently twice):**
- Mexico-Korea: Quiñones created the goal via a cross that forced a goalkeeper spill; Romo, not
  Quiñones, scored the rebound.
- USA-Australia: Balogun's cross/pressure forced Cameron Burgess into an own goal; Balogun himself
  did not score.

**Action:** see Rule #25. Separately weight players who generate chaos/pressure (better suited to
"involved in a goal" or shots/SCA-based props) from players who are the team's actual intended
finisher (better suited to standalone anytime-scorer props).

**Counter-example (Netherlands-Sweden):** Cody Gakpo both ASSISTED Brobbey's opener AND scored
himself later in the same match — elite players genuinely can do both. Treat P7 as a useful
prior that lowers confidence in a pure creator's standalone scorer odds, not an absolute rule
that a creator never scores. Always check the individual player's own shot/finishing profile
before applying the discount.

### P8 — Goals/Corners Decoupling at the Extremes
A blowout goal margin does NOT automatically mean a high corner count, and vice versa — the two
are driven by HOW a team scores, not just by how many goals are scored.

**Evidence (blowout, LOW corners):** Netherlands 5-1 Sweden produced just 6 total corners. The
goals came almost entirely from open-play combination, quick crosses immediately finished, and
individual quality (Brobbey x2, Gakpo x2, Summerville x1) — not from sustained sieges or repeated
set-piece routes.

**Evidence (blowout, HIGH corners — the opposite extreme):** Canada 6-0 Qatar produced 18 corners
to Qatar's 1 — a siege-style blowout where Canada pinned Qatar back for long stretches.

**Action:** Before projecting a corners total from an expected scoreline, check the EXPECTED GOAL
MECHANISM for the favored team — quick combination/counter-based attacks (lower corners even in a
blowout) vs. sustained crossing/wide-siege attacks (higher corners, scales with dominance). Don't
assume "big win = lots of corners" or "big win = doesn't matter, check the actual team-specific
data" (Rule #11) either way.

---

## (B) Specific Fixture H2H Records (2022+ only)

This section is intentionally sparse — most fixtures analyzed so far in the World Cup 2026 group
stage are first-ever or rare meetings between the two sides (e.g., Scotland and Morocco had never
played each other before their 2026 group match). Populate this section as repeat fixtures occur
or as relevant historical context is gathered for specific upcoming matchups.

| Fixture | Last meeting (2022+) | Result | Notes |
|---|---|---|---|
| *(none logged yet — add as repeat fixtures arise)* | | | |
