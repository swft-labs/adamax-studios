# Adamax Studios: client results page

A single self-contained page (`index.html`, with inline CSS and JS) that follows the Adamax Studios brand kit v1.0.

## Files

- `index.html`: the page.
- `assets/`: logo files built from the brand kit sources.
  - `adamax-lockup-on-dark{-420,-640,}.webp`: flat lockup for the nav and small screens (420, 640 and 720 px wide).
  - `adamax-metallic-lockup-on-dark{-640,}.webp`: metallic lockup for the end card only (shown only where it renders 400px wide or more).
  - `fonts/`: self-hosted Krona One and Manrope (variable, 400–700), latin subset, preloaded.
  - `favicon.png`, `apple-touch-icon.png`, `og-image.png`.
  - `proof/`: the 18 chat screenshots with "Spreed" (and its logo) covered in grey: `<id>-360.webp` / `<id>-720.webp` for the grid and `<id>.webp` (1080 px) for the lightbox. These are listed in `COVERED` in the script and never fall back to the GHL originals.
  - `video/`: the three case-study videos re-encoded with every on-screen "Spreed" covered (captions, the wall sign behind Rohit, app screen recordings and the "@spreed.ai.global" tag). The audio is unchanged.
  - `poster/`: a 960×540 poster frame per video (taken from the covered videos).

## Performance notes

- Videos use `preload="none"` with a poster, so nothing downloads until they play. Muted preview autoplay only runs on screens 900 px and wider. On phones the videos wait for a tap.
- The carousel images and video posters load as they approach the viewport. Proof grid images use `loading="lazy"`. Every image has `width`/`height` (CLS is 0).
- Fonts are self-hosted and preloaded, so there is no render-blocking CSS.

The remaining client media (carousel cards and the screenshots that never showed Spreed) loads from the GHL CDN, resized to WebP on the fly by `images.leadconnectorhq.com`.

## Live

https://viral.adamaxstudios.com/client-results

The Vercel project `adamax-viral-audit` deploys this repo's `main` branch to production, with the Viral Audit funnel at `/` and this folder at `/client-results`. Merging to `main` deploys it.

Asset paths are root-absolute (`/client-results/assets/...`) so the page works with or without a trailing slash.

## Deploy elsewhere

- **GoHighLevel Custom Code:** upload the files in `assets/` to GHL Media, replace the `/client-results/assets/...` paths in `index.html` with their URLs, then paste the file. All styles are scoped under `.adx`, so they don't clash with the funnel's own styles.

## Editing

Edit the `CONFIG` block at the top of the script:

- `CTA_URL`: set this to show the "Book a call" buttons in the nav and end card. They stay hidden while it is empty.
- `CAROUSEL` / `PROOF`: GHL media IDs for the carousel and the proof grid.
- `PROOF_INITIAL`: how many proof images show before "Show all".

## Preview

From the repo root:

```sh
python3 -m http.server 8000   # then open http://localhost:8000/client-results
```
