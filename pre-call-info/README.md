# Adamax Studios: pre-call page

The page people land on after booking a viral audit call. A single self-contained page (`index.html`, inline CSS and JS) styled to the Adamax Studios Brand Kit v1.0.

## Files

- `index.html`: the page. Headline and three step cards → Step 1 video (Wistia) with the ROASForm Add to Calendar button → Step 2 numbers to prepare → client proof → client results CTA → end card.
- `assets/`: logo, favicon and touch icon built from the brand kit sources.
  - `proof/`: profile photos for the proof cards (`<handle>.webp`, 150px).
  - `proof/thumbs/`: 360×640 preview frames taken from each account's own videos.

Asset paths are root-absolute (`/pre-call-info/assets/...`), so the page works with or without a trailing slash.

## Live

https://viral.adamaxstudios.com/pre-call-info

The Vercel project `adamax-viral-audit` deploys this repo's `main` branch, with this folder at `/pre-call-info`. Merging to `main` deploys it.

## Add to calendar

Both calendar buttons read the booking from the URL params the ROASForm booking redirect appends: `roasform_start`, `roasform_end`, `roasform_tz`, `roasform_title`, `roasform_location` and `roasform_desc`.

- **Under the video:** the ROASForm widget (`my.roasform.com/roasform-atc.js`), set to `data-width="full"` so it matches the video's width. Without booking params its options are inert.
- **Step 3 card in the header:** the page's own menu (Google, .ics, Outlook.com). It also accepts `?start=<ISO or Unix>&duration=<min>&join=<url>`. Without a start time it tells people to use their email invite.

## Editing the proof cards

Edit the `CASES` array in the script. The named doctors come first, then the doctor example, aesthetics and dentist cases. Cases marked `more: true` are hidden behind a "Show N more client results" button under the grid. DOXA was removed on purpose.

- `stat` / `label`: the headline number (e.g. `100M+` / `views`). `detail`: optional line underneath.
- `links`: platform buttons. The first link is also where the video preview goes.
- `img`: profile photo in `assets/proof/`. Without one the card shows initials.
- `thumb`: 9:16 preview frame in `assets/proof/thumbs/`, taken from the account's own video.

Every link was checked live when added. `instagram.com/billionaremansions` was unavailable, so that case links to TikTok only.

## Preview locally

From the repo root:

```sh
python3 -m http.server 8000   # then open http://localhost:8000/pre-call-info/
```

The Wistia video may not play locally if the account restricts playback to certain domains.
