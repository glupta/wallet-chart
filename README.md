# wallet-chart

A single-page interactive scatterplot positioning ~27 wallet-infrastructure products on two axes: **UX** (horizontal) and **Security** (vertical). Hammock is highlighted; everything else is a competitive reference point.

Live page: [`index.html`](./index.html) — no build step, no dependencies beyond a CDN-hosted Google Font.

## Use

Open `index.html` directly in any modern browser. Hover a dot for product detail (category, UX/Security scores, one-line note).

To host:

```bash
python3 -m http.server 8000
# or any static host: GitHub Pages, Vercel, Netlify, S3, etc.
```

## Editing the data

Products live in the `DATA` array near the top of the `<script>` block in `index.html`. Each entry:

```js
{ name: "Product Name", cat: "category_key", ux: 0–10, sec: 0–10, note: "Short description shown in tooltip." }
```

Categories are defined in the `CATEGORIES` object above `DATA` — each has a `label`, `color`, and optionally a `shape` (currently only `"star"` is used, for Hammock). To add a new category, add an entry to `CATEGORIES`, then reference its key in any `DATA` row's `cat` field.

## Scoring methodology

Scores reflect **structural properties** (architecture, trust model, chain support, key-handling design) rather than feature count or maturity. They are deliberate, opinionated, and meant to be argued with — adjust freely as the landscape moves.

- **UX**: How frictionless is the end-user flow? Seed phrases, hardware devices, and per-signer gas drag UX down. Passkeys, social login, and gas sponsorship push it up.
- **Security**: How strong is the trust model? Lower scores indicate vendor-in-path or operator-trust designs. Higher scores indicate trustless or self-custodial constructions (multisig, threshold crypto, secure elements).

## Browser support

Uses `CanvasRenderingContext2D.roundRect` (Safari 16.4+, Chrome 99+, Firefox 113+) and `letterSpacing` on canvas (Chrome 99+, Firefox 112+, Safari 17.4+). Falls back gracefully on older browsers — labels still render, just without letter spacing.

## License

No license file; treat as all rights reserved unless one is added.
