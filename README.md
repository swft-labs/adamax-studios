# Adamax Studios — Viral Audit funnel

A single landing page, styled to the Adamax Studios Brand Kit v1.0:

- **`index.html`**: the page. VSL → "See if you qualify" CTA → results carousel → ROAS qualify form → client stories → proof grid → end card.
- **`assets/`**: logo files resized for the web from the brand kit originals.

| File | Brand kit source | Used for |
|---|---|---|
| `adamax-lockup-on-dark.webp` | lockup on dark (default) | nav, footer, end card on narrow screens |
| `adamax-metallic-lockup-on-dark.webp` | metallic lockup on dark | end card only, rendered ≥ 420px |
| `favicon.png`, `apple-touch-icon.png` | mark on dark | browser tab / home screen |
| `og-image.png` | lockup on dark, on a 1200×630 black canvas | social share preview |

`assets/testimonials/` holds copies of the client proof with the old "Spreed" name covered up:

- **18 proof screenshots** (`.webp`): every "Spreed" / "Spreed AI" mention, truncated names ("Talha Ashraf Sp…") and the Spreed chat avatar are covered with flat `#737373` bars, the same grey as the screenshots' existing redactions. The page loads these via the `REDACTED` list; the other 32 proof images and the carousel had no Spreed mentions and still load from the GHL CDN.
- **3 client story videos** (`.mp4`): on-screen captions, the studio sign and app logos (feather icon included) and "@spreed.ai.global" are pixelated while they're on screen. **The audio is unchanged, so speakers still say "Spreed" out loud.**

All 21 files were re-checked with OCR (every image, and every video at 10 fps) and no "Spreed" text remains.

## Deploy

CSS and JS are inline; images load from `assets/` (relative paths).

- **Static host (Vercel etc.):** upload the folder as-is.
- **GoHighLevel custom code:** upload the `assets/` files (including `assets/testimonials/`) to GHL media first, then replace each `assets/…` path in the HTML with its GHL media URL.
- **Live:** https://viral.adamaxstudios.com (Vercel project `adamax-viral-audit`). The canonical URL and `og:image` point at this domain, so update them if it changes.

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

The vturb player shows "Video not found" outside its whitelisted domains. That's expected locally.

## Brand rules applied

- Built on pure black (`#000`). Surfaces `#030D1A`, hairlines `#172F52`. No drop shadows, glows or pills.
- Azure `#006BE5` is the only button colour. Sky `#009BFC` is for eyebrows, rules and accents. Glow `#03CCFF` only as a thin lit edge (video frame).
- Krona One for uppercase headlines; Manrope for everything else. Left-aligned, except the end card.
- Corners 4 / 8 / 16px; spacing 4 / 8 / 16 / 24 / 40 / 64. Angled accents use the mark's 60° cuts.
- Logo PNGs have black built in, so they only sit on `#000`. Each PNG has ~10% black clear space per side, so the drawn logo is 80% of the file width. Sizes are set so the artwork stays above the brand minimums: 140px for the lockup, 320px for the metallic lockup.

## Editing content

- **Carousel images:** `carouselImages` array (GHL media IDs) in the main `<script>`.
- **Proof grid images:** `proofImages` array in the same script.
- **Client stories:** the three `.story` blocks in the HTML.
- **Form:** the ROASForm embed inside `#qualify` (form ID `924236-f7060d-0db987`). Its colours and theme are set in the ROASForm dashboard.
- Every CTA uses `data-scroll-to="qualify"`. One delegated click handler smooth-scrolls to the form without adding a `#hash` to the URL.
