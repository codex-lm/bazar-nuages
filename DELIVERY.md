# Delivery note — The Cloud Bazaar (Le Bazar des nuages)

One-off mission for the Z Code workshop, 31 October 2026. Specification by
Cédric; implementation, art, balancing and verification by Z Code.

## What was built

- Single self-contained `index.html` (no network, no dependencies):
  deterministic engine, DOM/SVG interface, WebAudio sounds, EN/FR/ES.
- Loop: morning market (prices + demand forecast) → three customers
  (orders, per-unit offers, partial sales) → evening mooring fee → day 5
  upgrade choice → day 10 verdict against the 62-coin goal.
- Tracking file `MISSION.json` holds the mission log, simulation results and
  publication identifiers.

## Interpretation choices (spec → game)

- « Produits frais perdent de la valeur » → per-unit freshness: −25 %/night,
  floor 25 %, never spoils to zero; payments show each unit's percentage.
- « Certaines commandes demandent une combinaison » → Navigator and Aeronaut
  profiles order two goods at once.
- « Une seule amélioration en cours de partie » → one choice among three on
  day 5, with exact numbers on the cards.
- « Scénarios reproductibles » → every run is generated from a visible seed
  (`?seed=`), and the balancing study replays 600 seeds per strategy.
- Bankruptcy: the mooring fee can end the run, but starting capital equals
  the total fees for ten days, so coasting (never buying) always ends at
  exactly 0 — ruin only comes from overspending, never from the draw.

## Verification

- 18/18 Node rule tests executed against the shipped `index.html`
  (buy/capacity bounds, partial-sale and FIFO freshness math, sign upgrade,
  fee, day-5 gate, victory threshold 61 vs 62, bankruptcy, day-1 guardrail,
  budget = Σ qty×offer, price coherence over 400 seeds, determinism,
  i18n parity, bounded economy over 300 seeds).
- 600-seed × 5-strategy simulation (see README table) used to tune GOAL=62
  and the +30 %/−15 % demand spread.
- Real browser play (Chromium, 420×860 and 900×720): full winning run on
  seed `mission1` in French (final 102 coins, 14 customers served, shelf
  upgrade), partial-sale arithmetic checked live, replay button, EN/ES runs,
  rules screen, persistence of best run. Screenshots in the workshop's
  `evidence/bazar-nuages/`.
- Visual review of scene and cover by an image-analysis pass (final PASS).

## Known limits

- Balancing validated against scripted strategies, not human playtests;
  the baseline "follow the forecast" wins ~81 %, a human should do better.
- Sounds are synthesized and were checked functionally, not ear-mixed.
- No save-and-resume mid-run (a run is ~10 minutes by design).
