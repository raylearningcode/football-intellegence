# Deep Research Improvement Roadmap — 2026-06-23

**Scope:** Repository-wide improvement plan after the Jordan-Algeria corner failure and the broader World Cup 2026 audit.

---

## Executive summary

The repository has a strong analytical foundation: a 16-dimension model, calibration log, pattern file, league profile file, and anti-blind-spot research protocol. The main weakness is not conceptual ambition; it is operational consistency.

The system needs:

1. A stricter step-by-step operating procedure.
2. Better market-specific submodels.
3. Complete post-match reconciliation for every completed World Cup match.
4. Structured data fields instead of narrative-only lessons.
5. Stronger live betting triggers.
6. Confidence caps tied to data completeness and historical market accuracy.
7. A separate corner/set-piece module.
8. A backtest framework for accuracy, calibration, and market-specific reliability.

---

## Critical repo gaps

### 1. Too much knowledge is embedded in prose

Rules and patterns are useful, but many are not machine-checkable. Future improvement should add structured YAML/CSV/JSON logs for each match.

### 2. Incomplete match reconciliation

Many World Cup matches are referenced as evidence, but most do not have full post-match stat entries. This weakens calibration because examples are not consistently quantified.

### 3. Corners lack a standalone model

Corners need their own mechanism model, not a lightweight note inside advanced metrics.

### 4. Cards lack referee integration

Cards cannot be confidently predicted without referee identity, team discipline, match stakes, and favorite/underdog strength bias.

### 5. Player props need role separation

The repo has creator-vs-finisher logic, but every match report should explicitly classify players into:

- Finisher.
- Creator.
- Set-piece taker.
- Shot-volume player.
- Fouler.
- Fouled player.
- Card-risk player.

### 6. Live triggers are underdeveloped

The model often identifies a possible live trigger but does not state how much probabilities should move. This caused the Jordan-Algeria corner failure.

---

## New documents added in this update

1. `references/analysis-workflow-v3.md`
   - Step-by-step analysis guide.
   - Mandatory startup sequence.
   - Data checklist.
   - Scenario tree.
   - Confidence scoring.
   - Post-match calibration procedure.

2. `references/corner-and-set-piece-rules.md`
   - Rule #39 Set-Piece Comeback Siege Multiplier.
   - Pattern P12 Corner Mechanism Beats Corner Average.
   - Corner data fields.
   - Live corner triggers.

3. `references/world-cup-2026-match-ledger.md`
   - Completed match index through Jordan 1-2 Algeria.
   - Priority reconciliation queue.
   - Missing data schema for each match.

4. `references/jordan-algeria-corner-calibration-20260623.md`
   - Specific post-match corner failure case study.
   - Rule #39 origin note.

---

## Recommended next files to add

### `templates/match-analysis-template.md`

A reusable report template that forces:

- Data quality table.
- Bracket state.
- Coach-room diagnosis.
- Tactical four-phase map.
- 16-dimension scoring.
- Scenario tree.
- Market probabilities.
- Betting tier qualification.
- Blind-spot check.
- Post-match reconciliation block.

### `templates/post-match-reconciliation-template.yaml`

Structured match log schema:

```yaml
match:
  id:
  date:
  teams:
  group:
  venue:
  referee:
pre_match:
  model_version:
  probabilities:
  leans:
  confidence:
actual:
  score:
  halftime_score:
  goals:
  xg:
  shots:
  shots_on_target:
  possession:
  corners:
  cards:
  fouls:
  offsides:
grading:
  match_winner:
  goals_ou:
  btts:
  corners:
  cards:
  props:
error_diagnosis:
  data_error:
  model_error:
  live_adjustment_error:
  variance:
new_rules:
open_questions:
```

### `data/world-cup-2026/matches.yaml`

A structured counterpart to the match ledger.

### `data/world-cup-2026/prediction-ledger.csv`

Columns:

```csv
match_id,market,predicted_probability,closing_line,result,hit,confidence,model_version,error_type,lesson
```

---

## Backtest and validation plan

### Metrics

Track by market:

- Accuracy.
- Brier score.
- Log loss.
- ROI if odds are available.
- Expected value vs closing line.
- Calibration by probability bucket.
- Confidence bucket accuracy.

### Probability buckets

For every market:

| Bucket | Required check |
|---|---|
| 50-55% | Should hit roughly 50-55% |
| 56-60% | Should hit roughly 56-60% |
| 61-65% | Should hit roughly 61-65% |
| 66-70% | Should hit roughly 66-70% |
| 71-80% | Should hit roughly 71-80% |
| 81%+ | Should be rare and high quality |

If a 70% model bucket hits only 55%, confidence is inflated.

---

## Market-specific improvement priorities

### 1. Corners

Highest priority because historical calibration is weak.

Add:

- Rule #39.
- Pattern P12.
- Corner mechanism checklist.
- Team-corner preference over total-corner when one team owns pressure.
- Live adjustment thresholds.

### 2. Correct score

Do not treat correct score as a serious betting market until calibration improves. Use only as a distribution summary.

### 3. BTTS

Require both teams to have repeatable scoring routes. Counterattack possibility is not enough.

### 4. Cards

Add referee fields and strength-bias adjustment. Avoid cards without referee data.

### 5. Player props

Add player role tags and avoid fame-based picks.

### 6. Live betting

Every pre-match report should include explicit live triggers:

- What event flips the read?
- Which market improves?
- Which pre-match bet should be killed?
- What threshold confirms the live angle?

---

## Confidence discipline

Confidence should not represent how strongly the model feels. It should represent:

1. Data completeness.
2. Market calibration history.
3. Tactical clarity.
4. Scenario robustness.
5. Market price sensitivity.

Suggested caps:

| Situation | Max confidence |
|---|---:|
| Missing lineups | 6.5/10 |
| Missing referee and betting cards | 5/10 |
| Corner pick without team-specific corner data | 5/10 |
| Correct-score pick | 4/10 |
| Player prop without lineup confirmation | 5/10 |
| Strong data + robust scenario tree | 8/10 |

---

## Implementation roadmap

### Immediate

- Use `analysis-workflow-v3.md` for every new match.
- Use `corner-and-set-piece-rules.md` for every corner market.
- Use `world-cup-2026-match-ledger.md` to prioritize reconciliation.

### Next 1-2 sessions

- Add post-match YAML template.
- Add match-analysis markdown template.
- Reconcile Priority 1 matches with official stats.
- Update calibration-log.md to v2.9 after reconciliation.

### Medium term

- Build structured match database.
- Add market-specific prediction ledger.
- Compute Brier score and calibration curves.
- Separate pre-match and live accuracy.

### Long term

- Add automated match ingestion from official stats sources.
- Add Monte Carlo script.
- Add confidence calibration report.
- Add visual dashboard for market accuracy.

---

## Final principle

The model should not only ask: "Who is better?"

It must ask:

1. What does each coach want?
2. What game state benefits each team?
3. What tactical mechanism creates the market outcome?
4. What event would invalidate the pre-match bet?
5. Has this market been historically reliable for this model?
6. Is this a real edge or a forced bet?

If these questions are unanswered, confidence must be reduced.
