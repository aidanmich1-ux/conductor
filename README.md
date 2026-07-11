# PLS& — Penelope Studios website concept (static build)

A working static build of the site concept, following the PLS& Brand Guidelines for colour, type, and logo usage.

## How to view it
Open `index.html` directly in a browser, or serve the folder locally:

```
python3 -m http.server 8000
```

then visit `http://localhost:8000`.

To put it on the web as-is, drag the whole folder into Netlify Drop, or push it to a GitHub repo and enable GitHub Pages.

## Pages
- `index.html` — Home (hero video, statement section, Subscription/Campaign split)
- `work.html` — Our Work hub (same split, as its own landing page)
- `work-subscription.html` / `work-campaign.html` — filterable galleries (All / Fashion / Product / Business), click a card to open the project overlay
- `about.html` — Our Team (Penelope Gibson, Millie Vincent)
- `contact.html` — Contact
- `404.html` — the "Are you still here???" easter egg page
- `design-notes.html` — not part of the public nav. Documents the colour palette, typography, the three footer colourway options side by side, and every open decision still to confirm

## Annotations
Every pink annotation from the original concept PDF is preserved on the live pages, toggle them off with the button in the bottom-right corner (persists per browser session). Treat them as the brief for what to build or swap out next, not decoration.

## Logo
The header, homepage hero, and every footer use the real PLS& logo SVG, not styled text. Three colourways are included (`assets/logo/PLS_Hero_Black.svg`, `PLS_Hero_Cream.svg`, `PLS_Hero_Red.svg`). The site swaps automatically: black on the cream page background, cream over the dark hero video and the red footer, so it's never invisible against its own background. The footer colourway picker on `design-notes.html` demonstrates all three.

## Typography
Per the Brand Guidelines type hierarchy (p.21):
- **Blissful Radiance** (supplied webfont) → hero tagline, "let's be friends!", and every other handwritten brand-voice moment
- **EB Garamond** (free on Google Fonts, matches the guidelines exactly) → all body copy
- **Bookmania SemiBold + Neue Haas Grotesk Display 65 Medium** (both supplied, Neue Haas has a paid licence on file covering web + desktop up to 15K monthly uniques) → the title-card treatment on project overlays, e.g. "Brotherwolf"
- **TT Interphases Pro Mono, the primary heading/caption typeface, has not been supplied.** Space Mono stands in for every heading sitewide until the licensed file arrives. Swapping it in later is a one-line change in `css/style.css`'s `@font-face` block and the `--font-heading` variable. Flagged again on `design-notes.html`.

## Colour
Exact brand values from the guidelines (p.19): red `#821619`, black `#000000`, cream `#EDEADF`. The magenta used for the pink annotation callouts is my own addition for tracking concept notes, it isn't part of the brand palette.

## Photography
Real photos are used everywhere they were available:
- **Hero video**: `assets/hero.mp4` / `.webm`, autoplays muted and loops with no controls or player UI
- **Team photos**: Penelope Gibson and Millie Vincent's real portraits, plus a group shot as a banner at the top of the About page. All stripped of EXIF metadata (the originals had embedded GPS location data)
- **Statement section, Subscription/Campaign split panels**: the real napkin, Campari-drink, and black-and-white portrait photos from the original concept PDF
- **Gallery cards**: 16 real editorial photos pulled from the Brand Guidelines' imagery section (p.28-31), cycled across both galleries. Two images from that section were deliberately left out, they had another shoot's branding baked into the frame ("Gina Mari / Jennifer Meyers", a "paloma—wool" tag), and using those as if they were PLS&'s own portfolio work would be misleading
- **Brotherwolf project overlay**: the real barbershop photo from the guidelines (p.24), with the actual Bookmania/Neue Haas title-card typography over it

Still placeholder: the statement section is a still photo rather than the "napkin video" concept, and the Subscription/Campaign panels use a hover-zoom on stills rather than hover-video, since no video footage exists yet for either.

## Fixed this pass
The stray video control/cast-button overlay was Chrome injecting its own cast icon onto the background video. Suppressed via CSS (`::-internal-media-controls-overlay-cast-button` and related pseudo-elements) plus `pointer-events: none` on the video itself, since it's purely decorative and never needs to be clicked.

## Adding more media
Drop new files into `assets/` and point the relevant `src` at them.
- Google Drive share links don't work as direct `<img>`/`<video>` sources, they need the `drive.google.com/uc?export=download&id=FILE_ID` conversion, and even then Drive can rate-limit or serve a virus-scan interstitial for larger files. Safer long-term: host video on Vimeo (unlisted) and images on a real CDN.
- Any photo from a phone or modern camera likely has GPS EXIF data baked in. Strip it before it goes anywhere public (`convert file.jpg -strip output.jpg` with ImageMagick, or equivalent).

## Known open items
- **TT Interphases Pro Mono** not yet supplied, see Typography above.
- **Contact email inconsistency**: the source material uses two different addresses, `hello@penelopestudio.com.au` (footer, used sitewide here) and `hello@penelopestudios.com.au` (the contact page mockup, with an "s"). Flagged on `design-notes.html`, worth confirming the correct one before this goes live anywhere real.
- **Napkin video and Subscription/Campaign hover video** not yet supplied, both currently use still photography instead.

## Stack
Plain HTML/CSS/JS, no build step, no framework. Blissful Radiance, Bookmania SemiBold, and Neue Haas Grotesk Display are self-hosted in `assets/fonts/`. EB Garamond and Space Mono (placeholder) load from Google Fonts.
