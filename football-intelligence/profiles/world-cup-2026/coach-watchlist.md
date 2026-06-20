# World Cup 2026 Coach Watchlist

Purpose: track current national-team managers and their observed tournament behavior. This is not complete until every coach is verified from reliable current sources.

Status labels:

- `Verified` — current coach confirmed from recent reliable source.
- `Observed` — coach behavior observed in this tournament.
- `Verify` — do not use as confirmed until checked.

---

## Verified / Observed Coaches

### Brazil — Carlo Ancelotti

Status: Verified / Observed

Observed tournament behavior:

- After 1-1 Morocco draw, Brazil still pursued a strong win vs Haiti.
- Matheus Cunha starting changed finishing profile.
- Brazil 3-0 Haiti was clinical finishing, not full territorial domination.

Model note:

- Do not assume Brazil accept draw passively because table state is useful.
- Ancelotti can still seek control, but player-quality finishing can solve games early.
- Against stronger teams, upgrade finishing quality more than chance-creation dominance.

### Haiti — Sebastien Migne

Status: Verified / Observed

Observed tournament behavior:

- Haiti remained competitive in effort despite talent gap.
- Compact/counter/set-piece identity likely, but defensive quality was not enough vs Brazil.

Model note:

- Haiti underdog scoring tail should come from set pieces/counters, not sustained open play.

### Germany — Julian Nagelsmann

Status: Verified / Observed

Observed tournament behavior:

- Germany destroyed Curacao 7-1, then needed comeback vs Ivory Coast.
- Subs mattered: Deniz Undav changed Germany's finishing profile vs Ivory Coast.

Model note:

- Germany can dominate chance volume but remain vulnerable to athletic transitions.
- Do not overfit from the Curacao blowout.
- Bench striker/finisher impact is important.

### Ivory Coast — Coach verify before use

Status: Observed team behavior / Coach name verify

Observed tournament behavior:

- Beat Ecuador 1-0.
- Led Germany through Franck Kessie before losing 2-1.
- Athletic transition threat is real.

Model note:

- Strong underdog profile against favorites.
- Not a passive low block by default.

### Netherlands — Ronald Koeman

Status: Verified / Observed

Observed tournament behavior:

- After 2-2 Japan draw, changed attack by starting Brian Brobbey.
- Netherlands beat Sweden 5-1 with improved box presence.
- Crysencio Summerville made strong bench impact.

Model note:

- Netherlands attack improves when a true box presence is used.
- Bench impact and wide attackers matter.

### Sweden — Graham Potter

Status: Verified / Observed

Observed tournament behavior:

- Sweden beat Tunisia 5-1 then lost 5-1 to Netherlands.
- High volatility profile.

Model note:

- Do not treat Sweden's Tunisia win as stable dominance.
- Defensive transition and early-game stability need checking.

---

## Coaches To Verify Before Use

The following teams need current coach verification before any profile is treated as high confidence:

- Mexico
- South Africa
- South Korea
- Czechia
- Canada
- Bosnia and Herzegovina
- Qatar
- Switzerland
- Morocco
- Scotland
- United States
- Paraguay
- Australia
- Turkey
- Curacao
- Ecuador
- Japan
- Tunisia
- Belgium
- Egypt
- Iran
- New Zealand
- Spain
- Cape Verde
- Saudi Arabia
- Uruguay
- France
- Senegal
- Iraq
- Norway
- Argentina
- Algeria
- Austria
- Jordan
- Portugal
- DR Congo
- Uzbekistan
- Colombia
- England
- Croatia
- Ghana
- Panama

---

## Coach Profile Rule

Never infer coach behavior from country reputation alone. Coach behavior must come from:

- Verified manager identity
- Recent matches
- Lineups
- Substitution timing
- Press conference or credible reporting
- Repeated tactical patterns

If coach identity is unverified, cap coach-behavior confidence at 5/10.
