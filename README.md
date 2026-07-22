# Pesos — ARS → USD / EUR

Mobile-first, single-file peso converter. Punch in an amount in Argentine pesos
on the built-in keypad and watch the USD and EUR equivalents update live.

**Live:** https://franvillanu.github.io/ars-converter/

## Features
- **Bespoke numeric keypad** — no OS keyboard; big one-handed targets, press
  animation, haptic feedback, and `+1K / +10K / +100K` quick-add chips.
- **Edit any field** — tap ARS, USD, or EUR to make it the input; the other two
  convert automatically (enter dollars → see pesos, etc.).
- Sun/moon **theme toggle** (persists your choice, else follows the system).
- Two result columns: **USD** and **EUR**.
- Four markets in a sliding segmented control: **Blue · Oficial · MEP · Tarjeta**.
- Buy/sell spread and last-updated time per rate. EUR tracks the selected market
  (scaled off the official euro; estimates flagged with `*`).
- Live rates from [dolarapi.com](https://dolarapi.com); last value cached in
  `localStorage` so it still works offline. Auto-refreshes on focus and every 90s.
- Adaptive **light / dark** theme, `prefers-reduced-motion` support, safe-area aware.

## Design
Argentina identity, restrained: **3 championship stars**, a faint **Sol de Mayo**
halo, and a solid **Malvinas** islands silhouette — over an airy celeste canvas
with a floating glass input card.

## Run locally
Single static file, no build step:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/
```

## Rates
| Market  | Endpoint |
|---------|----------|
| Blue    | `https://dolarapi.com/v1/dolares/blue` |
| Oficial | `https://dolarapi.com/v1/dolares/oficial` |
| MEP     | `https://dolarapi.com/v1/dolares/bolsa` |
| Tarjeta | `https://dolarapi.com/v1/dolares/tarjeta` |
| Euro    | `https://dolarapi.com/v1/cotizaciones/eur` |

Conversion uses each source's `venta` (sell) value: `equiv = ARS / rate`.
