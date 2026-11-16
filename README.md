# Spreed — Viral Audit landing page

Single-file landing page (`index.html`): VSL → "See if you qualify" CTA → results carousel → GoHighLevel qualify form → video testimonials → proof grid.

## Deploy

The page is fully self-contained (inline CSS + JS, all media on the GHL CDN).

- **GoHighLevel:** paste the whole of `index.html` into a Custom Code / Custom HTML element on a blank funnel step.
- **Anywhere else:** upload `index.html` as-is to any static host.

## Preview locally

```sh
python3 -m http.server 8000   # then open http://localhost:8000
```

The vturb player shows "Video not found" outside its whitelisted domains — that's expected locally.

## Editing content

- **Carousel images:** `carouselImages` array (GHL media IDs) in the main `<script>`.
- **Proof grid images:** `proofImages` array in the same script.
- **Testimonials:** the three `.testimonial-card` blocks in the HTML.
- **Form:** the GHL iframe inside `#qualify` (form ID `Gsa0YAtp6rVAKB0jeEOv`).
- Every CTA uses `data-scroll-to="qualify"`. One delegated click handler smooth-scrolls to the form without adding a `#hash` to the URL.
