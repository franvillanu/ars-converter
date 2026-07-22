# Conversor de Pesos — ARS → USD / EUR

Mobile-first, single-file converter. Type an amount in Argentine pesos (ARS) and
instantly see the USD and EUR equivalents at the latest exchange rate.

## Features
- Big ARS input with live thousand-separator formatting (es-AR).
- Two columns below: **USD** and **EUR** equivalents.
- Live rates from [dolarapi.com](https://dolarapi.com) (Blue / Oficial for USD, Euro for EUR).
- Blue / Oficial toggle for the dollar rate.
- Last good rate cached in `localStorage` — still usable offline.
- Auto-refresh when the app regains focus.

## Design
Argentina "world-cup shirt" theme: celeste-and-white vertical stripes, **3 gold
stars** (the three World Cups) and a stylized **Malvinas** islands silhouette.

## Live
Once GitHub Pages is enabled (Settings → Pages → Deploy from branch → `main` / root):
**https://franvillanu.github.io/ars-converter/**

## Run locally
It's a single static file — no build step. Open `index.html`, or serve the folder:

```bash
python3 -m http.server 8080
# then open http://localhost:8080/
```

## Rates
- USD Blue:    `https://dolarapi.com/v1/dolares/blue`
- USD Oficial: `https://dolarapi.com/v1/dolares/oficial`
- EUR:         `https://dolarapi.com/v1/cotizaciones/eur`

Conversion uses each source's `venta` (sell) value: `equiv = ARS / rate`.
