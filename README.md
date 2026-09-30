# ICC 2026 — Create. Capture. Connect.

A single-page, mobile-first landing page for the guest photographer activation at **Indonesia Comic Convention (ICC) 2026**, JIEXPO Kemayoran, Jakarta. Visitors reach it by QR code or link to meet the photographer, find their photos after the event, join the giveaway, and get in touch about collaborations.

- **Event:** ICC 2026, 3–4 Oct 2026
- **Our activation:** 3 Oct 2026, Session 1 (11:00~15:00), guest photographer on Day 1 only
- **Stack:** plain HTML, CSS and JavaScript in one file. No build step, no dependencies.
- **Languages:** English and Indonesian, with an ID | EN switch in the header.

## Sections

| Section | Purpose |
| --- | --- |
| Hero | "Cosplay Photography Zone" badge, event date, session time, main buttons |
| Creators | Guest photographer profile with Instagram and WhatsApp buttons |
| Why | What we're here for: get photographed, join the giveaway, collaborate |
| Photos | "Find my photo" button (Instagram for now, GDrive link after the event) |
| Giveaway | Three steps: Follow, Share, Register, then the giveaway form button |
| Connect | Social cards (Instagram, WhatsApp, plus optional TikTok, YouTube, Threads) |
| Collab | Invitation for cosplayers, models, creators, photographers and brands |
| Event | Dates, venue, embedded Google Map, "Event Link" button, "Proudly at" organizer block |
| Footer | Instagram links and credits |

On mobile there is also a sticky bottom bar with "Get your photo" and "Giveaway" buttons. It is hidden on wide screens (1000px and up).

## Project structure

```
.
├── index.html          # the whole site (HTML + CSS + JS)
├── icc-favicon.ico     # browser tab icon
├── README.md
└── assets/
    ├── photographer1.jpg   # profile photo (portrait 4:5, e.g. 800x1000 px)
    ├── og-cover.jpg        # share-preview image (recommended 1200x630 px)
    └── hero.jpg            # optional hero background (not used unless set in CONFIG)
```

If an image is missing, the page still works: the profile photo falls back to a "PHOTO PLACEHOLDER" graphic, and the hero falls back to a gradient.

## Run locally

No install needed. Open `index.html` in a browser.

For a more realistic preview (for example, to test on your phone over Wi-Fi), serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

An internet connection is needed for the Google Fonts (Big Shoulders Display, Figtree) and the embedded Google Map.

## Editing the page

Open `index.html` and search (Ctrl+F) for **`CHANGE ME`**. Every spot you're likely to edit is marked, and a quick guide sits at the top of the file.

| To change | Where |
| --- | --- |
| Profile photo | `CONFIG.images.photographer1` in the script at the bottom |
| Hero background image | `CONFIG.images.hero` (leave `""` for the gradient) |
| Links, handles, venue text | `CONFIG` in the script at the bottom |
| Any visible text | `TEXT.en` and `TEXT.id`. Edit **both** languages |
| Map | The `<iframe>` in the Event section. Paste a new embed `src` from Google Maps > Share > Embed a map |
| Colors | The `:root` variables at the top of the CSS |
| Share-preview image | `og:image` and `twitter:image` meta tags at the top |
| Favicon | `<link rel="icon">` at the top |

### Changing the profile photo

1. Put the new photo in the `assets/` folder.
2. Either name it `photographer1.jpg` to replace the old one, or set its path in `CONFIG.images.photographer1`.
3. Refresh the page (hard refresh with Ctrl+Shift+R if the old image still shows).

The photo is cropped to fill a 4:5 frame, so keep the face near the center.

### The CONFIG object

| Key | What it does |
| --- | --- |
| `eventUrl` | Link for the "Event Link" button |
| `photographer1` | Name, Instagram handle and link, WhatsApp number (country code plus number, digits only, no `+` or leading 0) |
| `organizer` | Organizer name, handle, link, and hashtag buttons in the "Proudly at" block |
| `partners` | Partner accounts. Each gets a "Follow" button in the "Proudly at" block and a footer link. Add or remove lines freely |
| `giveawayUrl` | Google Form link for the giveaway buttons |
| `photoGalleryUrl` | "Find my photo" button link |
| `collaborationUrl` | Google Form link for collaboration requests |
| `venue` | Venue text in the Event section |
| `extras` | Optional TikTok, YouTube and Threads cards. A card shows only when a full link is filled in |
| `images` | `hero` and `photographer1` image paths |

A link that is still a `[PLACEHOLDER]` (or empty) doesn't break anything. Tapping it shows the message "This link hasn't been set yet."

### Language

The page picks Indonesian if the browser language starts with `id`, otherwise English. The visitor's choice from the ID | EN switch is remembered in the browser (`localStorage`). Every text key in `TEXT.en` has a matching key in `TEXT.id`.

## Before launch checklist

- [ ] Set `giveawayUrl` to the Google Form link
- [ ] Set `collaborationUrl` to the Google Form link
- [ ] Add the real photo at `assets/photographer1.jpg` (or update the path)
- [ ] Add `assets/og-cover.jpg` and use a full `https://` URL for `og:image` and `twitter:image` once the site is hosted
- [ ] Confirm `icc-favicon.ico` is next to `index.html`
- [ ] Optional: add a hero background image and set `CONFIG.images.hero`
- [ ] Test on a phone (both languages) and scan the QR code once it points to the live URL

After the event:

- [ ] Upload photos to Google Drive and point `photoGalleryUrl` to the shared folder link
- [ ] Update the note under the button (`photoNote` in both languages) if it still mentions Instagram

## Deploying

Because the site is one static file plus an `assets/` folder, any static host works, for example GitHub Pages, Netlify, Cloudflare Pages or a normal web host. Upload `index.html`, `icc-favicon.ico` and the `assets/` folder together, keeping the same relative layout.

## Accessibility and performance notes

- Skip-to-content link, visible keyboard focus, and proper labels on the menu and language buttons
- Respects `prefers-reduced-motion` (animations and transitions are switched off)
- Responsive from small phones up to large desktop screens, with safe-area support for notched phones
- The map and the profile photo load lazily
