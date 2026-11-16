# Adamax Studios — Viral Audit funnel

Two pages, styled to the Adamax Studios Brand Kit v1.0:

- **`index.html`**: landing page. VSL → "See if you qualify" CTA → results carousel → ROAS qualify form → client stories → proof grid → end card.
- **`booking.html`**: booking step ("Pick a time") with the embedded GHL calendar (`escdhM2THRdejLTLUISY`). Marked `noindex`.
- **`assets/`**: logo files resized for the web from the brand kit originals.

| File | Brand kit source | Used for |
|---|---|---|
| `adamax-lockup-on-dark.webp` | lockup on dark (default) | nav, footer, end card on narrow screens |
| `adamax-metallic-lockup-on-dark.webp` | metallic lockup on dark | end card only, rendered ≥ 420px |
| `favicon.png`, `apple-touch-icon.png` | mark on dark | browser tab / home screen |
| `og-image.png` | lockup on dark, on a 1200×630 black canvas | social share preview |

## Deploy

CSS and JS are inline; images load from `assets/` (relative paths).

- **Static host (Vercel etc.):** upload the folder as-is.
- **GoHighLevel custom code:** upload the `assets/` files to GHL media first, then replace each `assets/…` path in the HTML with its GHL media URL.
- `og:image` must be an absolute URL for social previews. Change `assets/og-image.png` to the full URL once the domain is known.

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

The vturb player shows "Video not found" outside its whitelisted domains. That's expected locally.

## Brand rules applied

- Built on pure black (`#000`). Surfaces `#030D1A`, hairlines `#172F52`. No drop shadows, glows or pills.
- Azure `#006BE5` is the only button colour. Sky `#009BFC` is for eyebrows, rules and accents. Glow `#03CCFF` only as a thin lit edge (video frame, calendar loader).
- Krona One for uppercase headlines; Manrope for everything else. Left-aligned, except the end card.
- Corners 4 / 8 / 16px; spacing 4 / 8 / 16 / 24 / 40 / 64. Angled accents use the mark's 60° cuts.
- Logo PNGs have black built in, so they only sit on `#000`. Each PNG has ~10% black clear space per side, so the drawn logo is 80% of the file width. Sizes are set so the artwork stays above the brand minimums: 140px for the lockup, 320px for the metallic lockup.

## Editing content

- **Carousel images:** `carouselImages` array (GHL media IDs) in the main `<script>`.
- **Proof grid images:** `proofImages` array in the same script.
- **Client stories:** the three `.story` blocks in the HTML.
- **Form:** the ROASForm embed inside `#qualify` (form ID `924236-f7060d-0db987`). Its colours and theme are set in the ROASForm dashboard.
- Every CTA uses `data-scroll-to="qualify"`. One delegated click handler smooth-scrolls to the form without adding a `#hash` to the URL.

## Booking page pre-fill

`booking.html` forwards contact details from its own URL into the calendar widget, so set the qualify form's redirect to e.g.:

```
https://<your-domain>/booking?first_name={{first_name}}&last_name={{last_name}}&email={{email}}&phone={{phone}}
```

(Use whatever merge-field syntax ROASForm supports for its redirect URL.)

- Accepted params: `first_name` / `firstName`, `last_name` / `lastName`, `email`, `phone`. Any `utm_*` params are passed through too.
- The iframe `src` is set by script before its first load, so the widget only loads once.
- A light-sweep loader shows until the widget loads (15s cap), with an "Open it in a new tab" fallback link carrying the same params.
