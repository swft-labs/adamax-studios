# Adamax Studios: follow-up booking page

Where people book their follow-up (strategy implementation) call. A single self-contained page (`index.html`, inline CSS) styled to the Adamax Studios Brand Kit v1.0.

Hexagon tick badge → "Book a follow-up call" headline → "Select your preferred time" → GoHighLevel calendar embed → footer with the legal links.

Fonts, logo and favicon load from the site-wide `/assets/` folder (root-absolute paths, so the page works with or without a trailing slash).

## Live

https://viral.adamaxstudios.com/follow-up-booking-call-page (`noindex`). Merging to `main` deploys it.

## Calendar

The GoHighLevel booking widget (calendar `qybQcay1gUkbe4eP8jBX`) in an iframe, plus `link.msgsndr.com/js/form_embed.js`, which resizes the iframe to fit the widget. The iframe keeps a 640px minimum height so the page doesn't jump while it loads.

Everything inside the white card (colours, logo, event name, description, "Ads Inbound" group label, durations, availability) is set in GoHighLevel, not here. If the calendar name or length changes, update the line under "Select your preferred time" to match.
