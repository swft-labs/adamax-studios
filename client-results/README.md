# Adamax Studios: client results page

A single self-contained page (`index.html`, with inline CSS and JS) that follows the Adamax Studios brand kit v1.0.

## Files

- `index.html`: the page.
- `assets/`: logo files built from the brand kit sources.
  - `adamax-lockup-on-dark.webp`: flat lockup for the nav and small screens.
  - `adamax-metallic-lockup-on-dark.webp`: metallic lockup for the end card only (shown only where it renders 400px wide or more).
  - `favicon.png`, `apple-touch-icon.png`, `og-image.png`.
  - `proof/`: the 18 chat screenshots with "Spreed" (and its logo) covered in grey: `<id>-480.webp` for the grid and `<id>.webp` for the lightbox. These are listed in `COVERED` in the script and never fall back to the GHL originals.
  - `video/`: the three case-study videos re-encoded with every on-screen "Spreed" covered (captions, the wall sign behind Rohit, app screen recordings and the "@spreed.ai.global" tag). The audio is unchanged.

Client media (videos and screenshots) loads from the GHL CDN. Screenshots are resized to WebP on the fly by `images.leadconnectorhq.com`.

## Live

https://viral.adamaxstudios.com/client-results is served by the Vercel project `adamax-viral-audit` (team Swift Labs), which also serves the Viral Audit funnel at `/`.

To update it, download the project's current production files, put this folder at `client-results/` inside them, rewrite `assets/` paths to `/client-results/assets/` (so the page works without a trailing slash), and run `vercel deploy --prod`. A funnel deploy that doesn't include `client-results/` will remove this page.

## Deploy elsewhere

- **Static host:** upload `index.html` together with the `assets/` folder.
- **GoHighLevel Custom Code:** upload the files in `assets/` to GHL Media, replace the `assets/...` paths in `index.html` with their URLs, then paste the file. All styles are scoped under `.adx`, so they don't clash with the funnel's own styles.
- `og:image` needs an absolute URL once the page has a domain.

## Editing

Edit the `CONFIG` block at the top of the script:

- `CTA_URL`: set this to show the "Book a call" buttons in the nav and end card. They stay hidden while it is empty.
- `CAROUSEL` / `PROOF`: GHL media IDs for the carousel and the proof grid.
- `PROOF_INITIAL`: how many proof images show before "Show all".

## Preview

```sh
open client-results/index.html
```
