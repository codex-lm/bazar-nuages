# The Cloud Bazaar · Le Bazar des nuages · El Bazar de las nubes

A small shop-management game for the browser: you keep a stall hanging from
balloons on a floating market. **Ten days** to buy wisely, serve three
customers a day, and fund the voyage to a new island.

Play: `index.html` (fully self-contained, works offline) — also on
GitHub Pages: <https://codex-lm.github.io/bazar-nuages/>

## Rules (summary)

- You start with **30 coins** and a **6-slot warehouse**; every unit of goods
  takes one slot.
- Four goods, in two families:
  - **Fresh** (loses 25 % of its value each night, floor 25 %): Mistberries,
    Lanternfruit;
  - **Ordinary** (keeps its value): Cloudwool, Stormtea.
- Each morning shows a **demand forecast**: two goods are in demand —
  customers ask for them far more often and pay **+30 %**; all other goods
  fetch **−15 %**. Buy prices drift daily (−20 % … +20 %).
- Then **three customers** visit, one after another (6 profiles, from the
  Kite Kid to the Aeronaut). Each shows an order (sometimes a **combination**
  of goods), a per-unit offer and a budget. Choose how many units to hand
  over — oldest stock leaves first, and every line shows its arithmetic —
  or turn them away.
- Every evening, pay the **3-coin mooring fee**. If you cannot, the run ends.
- On **day 5**, pick exactly **one** shop improvement: pine shelf (+2 slots),
  sign balloon (+15 % on all offers) or ice box (fresh loses only 10 %/night).
- Reach **62 coins** by the end of day 10 to fund the voyage.

Every number the game shows you (offers, per-unit payments, freshness
percentages, fees, ledger) is the exact number used in computation.

## Controls

Point & tap / click. Steppers (+/−) to buy or serve, big buttons to confirm.
Works on touch screens; responsive portrait and landscape.

## Reproducibility & QA

- Days are generated from a seed (`?seed=...` in the URL; shown on the end
  screen and on retry). Same seed → same prices, demand and customers.
- `?lang=en|fr|es` forces the language (English by default).
- `window.__bazar` exposes a read-only state hook for automated checks.
- Development kit (build, tests, strategy simulator, cover generator) lives
  outside this repository; test suite: **18/18** rule tests run against the
  shipped `index.html` (legal/illegal buys, partial sales, FIFO freshness,
  fees, upgrades, victory/defeat thresholds, price coherence across 400
  seeds, i18n parity, determinism, bounded economy).

## Balancing study (600 seeds × 5 strategies)

| Strategy | Win rate | Median capital |
|---|---|---|
| Follow the forecast (baseline) | 81 % | 97 |
| Buy ordinary goods only | 67 % | 86 |
| Buy fresh only | 14 % | 28 |
| Chaotic (random buys, big orders only) | 0 % | 34 |
| Never buy | 0 % | 0 |

- **No infinite profit**: max final capital observed over all strategies and
  seeds is bounded (249 coins with GOAL 62).
- **No impossible start**: day 1 demand always includes an ordinary
  (non-perishable) good, and 30 coins cover exactly the ten mooring fees, so
  a player who stops buying can never be ruined by the draw — bankruptcy only
  follows from spending everything down and then failing the fee.

## Credits & license

- Concept: Cédric Bernadac (specification for the Z Code workshop).
- Implementation, art, audio: Z Code (automated production with Z Code).
- MIT license — see `LICENSE`. No third-party assets; all graphics are
  inline SVG, all sounds are synthesized WebAudio.
