# Pesos — ARS → USD / EUR

Mobile-first, single-file peso converter. Punch in an amount on the built-in
keypad and watch the equivalents update live. Convert **from pesos** (default,
→ USD / EUR) or flip the `$ / €` toggle to convert **from euros** (→ ARS / USD)
— handy when you are travelling in Spain.

**Live:** https://franvillanu.github.io/ars-converter/

## Features
- **Bespoke numeric keypad** — no OS keyboard; big one-handed targets, press
  animation, haptic feedback, and quick-add chips that follow the currency you
  are typing (`+1K / +5K / +10K` for pesos, `+10 / +50 / +100` for USD / EUR).
- **Base-currency toggle (`$` / `€`)** next to the theme button — picks which
  currency the big card holds; the choice persists in `localStorage`
  (`pesos_base`, default `ars`). The selected market persists too
  (`pesos_rate`, default `takenos`).
- **Edit any field** — tap ARS, USD, or EUR to make it the input; the other two
  convert automatically (enter dollars → see pesos, etc.).
- Markets in a sliding segmented control: **Takenos · Blue · Oficial · Tarjeta**.
- **Takenos** is a *synthetic estimate* (default), not an official quote:
  `Takenos = Oficial + 0.67 × (Blue − Oficial)`. The coefficient comes from a
  single observed transaction, so it's labelled as an estimate in the UI.
- Buy/sell spread and last-updated time per rate. EUR tracks the selected market
  (scaled off the official euro; estimates flagged with `*`).
- Auto-fitting amounts (scale to fit any screen width), sun/moon **theme toggle**
  (persists, else follows system), pinch/double-tap zoom disabled.
- **Jump-free layout** — every text row in the result cards has a fixed box, so a
  longer rate or a wrapped note never reflows the page while you type or switch
  markets. Heights use `svh`, not `dvh`, so iOS collapsing its address bar
  cannot move the layout either; the UI is compacted on short screens so it
  fits without scrolling at all (down to the iPhone SE). The keypad stretches
  to fill whatever is left over, so there is no dead space in the middle and
  the slack lands in bigger keys instead.
- Live rates from [dolarapi.com](https://dolarapi.com); last value cached in
  `localStorage` so it still works offline. Auto-refreshes on focus and every 90s.
- Adaptive **light / dark** theme, `prefers-reduced-motion` support, safe-area aware.

## Run locally
Single static file, no build step:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/
```

## Rates
| Market  | Source |
|---------|--------|
| Takenos | computed: `oficial.venta + 0.67 × (blue.venta − oficial.venta)` |
| Blue    | `https://dolarapi.com/v1/dolares/blue` |
| Oficial | `https://dolarapi.com/v1/dolares/oficial` |
| Tarjeta | `https://dolarapi.com/v1/dolares/tarjeta` |
| Euro    | `https://dolarapi.com/v1/cotizaciones/eur` |

Conversion uses each source's `venta` (sell) value: `equiv = ARS / rate`. Pesos
are always the internal pivot, so euro-base mode converts `EUR → ARS → USD` with
the same quotes.
