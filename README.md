# Adamax Studios — Viral Audit funnel

A single landing page, styled to the Adamax Studios Brand Kit v1.0:

- **`index.html`**: the page. VSL → "See if my practice qualifies" CTA → results carousel → ROAS qualify form → case studies → proof grid → end card.
- **`assets/`**: everything the page loads, self-hosted (no GHL CDN or Google Fonts):
  - logo files resized for the web from the brand kit originals (table below),
  - `fonts/`: Krona One and Manrope (latin subset, woff2, SIL Open Font License), preloaded,
  - `results/`: the 7 results-carousel images,
  - `proof/`: the 50 proof-grid images,
  - `testimonials/`: the 3 client videos (720p) in the case-study cards.

Other pages on the same site live in their own folders, each with a README: `client-results/` (`/client-results`) and `pre-call-info/` (`/pre-call-info`, the page people see after booking a call).

Legal pages linked from the footer: `privacy/` (`/privacy`), `terms/` (`/terms`) and `results-disclaimer/` (`/results-disclaimer`). They share the landing page's fonts and logo via absolute `/assets/…` paths. **They are drafts written from what the site actually does (the ROAS form, the Meta Pixel it loads, Wistia, Vercel hosting, edited screenshots) and need legal review.** They don't yet name a legal entity, address, contact email or governing law.

| File | Brand kit source | Used for |
|---|---|---|
| `adamax-lockup-on-dark.webp` | lockup on dark (default) | nav, footer, end card on narrow screens |
| `adamax-metallic-lockup-on-dark.webp` | metallic lockup on dark | end card only, rendered ≥ 420px |
| `favicon.png`, `apple-touch-icon.png` | mark on dark | browser tab / home screen |
| `og-image.png` | lockup on dark, on a 1200×630 black canvas | social share preview |

### Images

All carousel and proof images are WebP at quality 80, in several widths so phones don't download desktop-sized files:

- `results/<id>-{300,480,720,900,1080}.webp`: shown 240px tall on desktop and 300px on mobile (`sizes="(min-width: 760px) 240px, 300px"`).
- `proof/<id>-{360,540,720,<original>}.webp`: masonry grid, 3 columns from 760px and 2 below; `sizes` mirrors that layout.

Every `<img>` is in the HTML with `width`/`height` (so space is reserved before it loads), descriptive `alt` text, `loading="lazy"` and `decoding="async"`. The exception is the header logo, which is above the fold (`fetchpriority="high"`, not lazy). The carousel is a single set of images looped by script, with no duplicate copies.

### Old "Spreed" branding covered up

- **18 proof screenshots:** every "Spreed" / "Spreed AI" mention, truncated names ("Talha Ashraf Sp…") and the Spreed chat avatar are covered with flat `#737373` bars, the same grey as the screenshots' existing redactions.

- **3 client videos** (`testimonials/`): on-screen captions, the studio sign and app logos (feather icon included) and "@spreed.ai.global" are pixelated while on screen. **The audio is unchanged, so speakers still say "Spreed" out loud.**

All of these were re-checked with OCR (every image, and every video at 10 fps) and no "Spreed" text remains.

## Deploy

CSS and JS are inline; images load from `assets/` (relative paths).

- **Static host (Vercel etc.):** upload the folder as-is.
- **GoHighLevel custom code:** upload everything under `assets/` to GHL media first, then replace each `assets/…` path in the HTML with its GHL media URL.
- **Live:** https://viral.adamaxstudios.com (Vercel project `adamax-viral-audit`). The canonical URL and `og:image` point at this domain, so update them if it changes.

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

The VSL is a Wistia embed (media `340vni851v`). If the Wistia account restricts playback to certain domains, it may not play locally.

## Brand rules applied

- Built on pure black (`#000`). Surfaces `#030D1A`, hairlines `#172F52`. No drop shadows, glows or pills.
- Azure `#006BE5` is the only button colour. Sky `#009BFC` is for eyebrows, rules and accents. Glow `#03CCFF` only as a thin lit edge (video frame).
- Krona One for uppercase headlines; Manrope for everything else. Left-aligned, except the end card.
- Corners 4 / 8 / 16px; spacing 4 / 8 / 16 / 24 / 40 / 64. Angled accents use the mark's 60° cuts.
- Logo PNGs have black built in, so they only sit on `#000`. Each PNG has ~10% black clear space per side, so the drawn logo is 80% of the file width. Sizes are set so the artwork stays above the brand minimums: 140px for the lockup, 320px for the metallic lockup.

## Editing content

- **Carousel images:** the `<img class="carousel-item">` tags inside `#carouselTrack`. Each needs its `results/` WebP widths, `width`/`height` and `alt`.
- **Proof grid images:** the `.proof-item` blocks inside `#proofGrid`, the same pattern with `proof/` widths.
- **VSL:** the Wistia player stays hidden behind a blurred thumbnail until Wistia's `api-ready` event (12s fallback). Wistia's own layout pass would otherwise count as layout shift.
- **Client stories:** the three `.story` cards (text beside a video). Each has a headline, one line and three stat chips. Wrap the number in a chip in `<strong>` to colour it. Videos autoplay muted while in view and show a "Play with sound" button.
- **Form:** the ROASForm embed inside `#qualify` (form ID `924236-f7060d-0db987`), inline at 600px with `fullScreen: true`: once a visitor answers the first question it takes over the screen, and its × returns them to the same spot on the page with their progress kept. Its colours and theme are set in the ROASForm dashboard.
- Every CTA uses `data-scroll-to="qualify"`. One delegated click handler smooth-scrolls to the form without adding a `#hash` to the URL.
