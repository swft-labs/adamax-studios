# Spreed — Viral Audit funnel

Two single-file pages:

- **`index.html`** — landing page: VSL → "See if you qualify" CTA → results carousel → GoHighLevel qualify form → video testimonials → proof grid.
- **`booking.html`** — booking step ("Just Pick a Time"): embedded GHL calendar (`escdhM2THRdejLTLUISY`). Marked `noindex`.

## Deploy

Each page is fully self-contained (inline CSS + JS, all media on the GHL CDN).

- **GoHighLevel:** paste the whole of each file into a Custom Code / Custom HTML element on a blank funnel step.
- **Anywhere else:** upload the files as-is to any static host.

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

## Booking page pre-fill

`booking.html` forwards contact details from its own URL into the calendar widget, so set the qualify form's redirect to e.g.:

```
https://<your-domain>/booking?first_name={{contact.first_name}}&last_name={{contact.last_name}}&email={{contact.email}}&phone={{contact.phone}}
```

- Accepted params: `first_name` / `firstName`, `last_name` / `lastName`, `email`, `phone`. Any `utm_*` params are passed through too.
- The iframe `src` is set by script before its first load, so the widget only loads once (no reload to apply params).
- A spinner shows until the widget loads (15s cap), and an "Open it in a new tab" link (with the same params) is there as a fallback.
