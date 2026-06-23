# Jordan 1-2 Algeria — Corner Calibration Addendum

**Match:** Jordan 1-2 Algeria  
**Competition:** FIFA World Cup 2026, Group J, MD2  
**Date:** 2026-06-23 UTC+8 / 2026-06-22 local  
**Purpose:** Post-match learning entry focused on the corner-market miss and live-adjustment failure.

---

## Pre-match model call

Pre-match corner projection:

| Market | Pre-match probability |
|---|---:|
| Algeria most corners | 61% |
| Algeria over 3.5 team corners | 63% |
| Algeria over 4.5 team corners | 48% |
| Algeria over 5.5 team corners | 34% |
| Total over 8.5 corners | 39% |
| Total over 9.5 corners | 28% |
| Under 9.5 total corners | 72% |

The side/score model performed well: Algeria were projected as a narrow favorite and 2-1 was the top correct-score cluster. The corner model failed by capping the Algeria corner ceiling too low.

---

## Actual match signals

- Algeria won 2-1 after trailing 1-0 at half-time.
- Jordan scored first through Nizar Al-Rashdan in the 36th minute.
- Algeria equalized through Nadhir Benbouali from a Riyad Mahrez corner.
- Algeria scored the winner through Amine Gouiri after another Mahrez corner/set-piece scramble.
- Public reports described Algeria as second-half dominant, including a large second-half shot advantage.

Exact final corner split should be filled when a reliable official match-stat source is available. The tactical lesson is already clear: Algeria's corner/set-piece route was not just high-volume; it was the primary comeback mechanism.

---

## Error diagnosis

### What was correct

1. Algeria were the correct side lean.
2. Algeria most corners was directionally correct.
3. Algeria over 3.5 corners was identified as the best team-corner angle.
4. Live trigger warning existed: if Jordan scored first, Algeria corner volume could rise sharply.

### What was wrong

1. The model treated Jordan's first goal as a generic over-corners trigger, not as a full favorite-siege trigger.
2. It underestimated Mahrez's set-piece delivery as a repeatable chance-creation route.
3. It projected Algeria's attacks as possession/control-based rather than corner-forcing/wide-delivery based.
4. It did not distinguish between "favorite chasing through central possession" and "favorite chasing through wide/set-piece pressure."
5. It left Under 9.5 as a pre-match lean despite a clear scenario branch where it could collapse.

---

## New rule candidate: Rule #39 — Set-Piece Comeback Siege Multiplier

**Definition:** When a technically superior favorite trails a compact underdog from minute 25 onward and has credible wide delivery or set-piece specialists, team-corner and total-corner ceilings must be raised aggressively.

**Trigger conditions:**

Apply when at least 4 of 6 are true:

1. Favorite trails by 1 goal.
2. Underdog is likely to protect lead with compact/deep block.
3. Favorite has strong wide creators or set-piece takers.
4. Favorite needs points urgently in a tournament/bracket context.
5. Favorite has already produced 2+ corners or repeated blocked crosses before 60'.
6. Underdog's counterattacks are isolated rather than sustained.

**Adjustment:**

```text
Favorite_Team_Corners = Base_Team_Corners × 1.35 to 1.60
Total_Corners = Base_Total_Corners + 2.5 to 4.0
Over_8.5_Corners += 15 to 25 probability points
Over_9.5_Corners += 15 to 22 probability points
Unders at 8.5/9.5 should be downgraded to live-only or no-bet once trigger activates.
```

**Jordan-Algeria application:**

- Algeria trailed 1-0 from min 36.
- Jordan's optimal response was to defend lead and counter.
- Mahrez provided elite corner/set-piece delivery.
- Algeria needed the win to keep qualification alive.
- Algeria's second-half pressure converted into two set-piece/corner goals.

Result: Rule #39 would have killed or hedged Under 9.5 and upgraded Algeria team-corners live.

---

## New pattern candidate: Pattern P12 — Corner Mechanism Beats Corner Average

**Definition:** Corner markets should be driven by the attacking mechanism, not by expected match dominance alone.

A favorite can dominate and still produce low corners if goals come through central combinations or quick finishes. But when the favorite's comeback route is wide pressure, blocked crosses, repeated deliveries, and set pieces, corner volume can explode even if the final score is only 2-1.

**Practical test before any corner bet:**

Ask:

1. Does the favorite attack wide or centrally?
2. Does the underdog block crosses or press before crosses happen?
3. Does the favorite have a high-quality set-piece taker?
4. If the underdog scores first, will the favorite chase via wide pressure or central possession?
5. Is the underdog capable of escaping pressure for sustained counters, or will clearances recycle into more corners?

If answers point to wide siege, do not recommend low-corner unders pre-match.

---

## Updated betting discipline

### Pre-match corner rule

Do not make Under 9.5 a core pick when the favorite has a clear live branch that creates a siege. Mark it as price-sensitive or live-only.

### Live-corner rule

If the underdog scores first and the favorite has strong wide/set-piece delivery:

- Upgrade favorite team-corner overs first.
- Upgrade total over 8.5 before over 9.5.
- Avoid doubling down on corner unders unless the favorite is attacking centrally with low crossing volume.

### Market hierarchy after this match

1. Team corners for chasing favorite: strongest corner angle.
2. Total over 8.5: secondary.
3. Total over 9.5: only if early corner pace confirms.
4. Corner unders: avoid when underdog leads and favorite is wide/set-piece strong.

---

## Grade

| Market | Pre-match call | Actual lesson | Grade |
|---|---|---|---|
| Algeria most corners | Directionally supported | Correct side of corner dominance | Partial hit |
| Algeria over 3.5 corners | Best team-corner lean | Correct idea, ceiling too conservative | Hit/partial depending line |
| Under 9.5 total corners | Main safer lean | Bad risk profile once Jordan scored first | Miss |
| Live adjustment after Jordan goal | Mentioned but not weighted enough | Should have flipped to Algeria team-corner overs | Miss |

---

## Lesson banked

Algeria-Jordan proves that corner unders are dangerous when the underdog scores first against a favorite with elite set-piece delivery. The model must separate "favorite possession" from "favorite siege." In future, a trailing favorite with wide/set-piece mechanisms should receive an immediate corner-ceiling multiplier, and team-corner overs should be preferred over total-corner unders.
