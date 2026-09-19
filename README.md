# Video Director Portfolio

A single-page portfolio site for a video director / filmmaker. Built with plain HTML, CSS and JavaScript — no build step or dependencies required.

## Sections

- **Hero** — full-bleed intro with tagline and calls to action
- **Showreel** — embedded video reel
- **Selected Work** — project grid that opens a video preview modal on click
- **About** — bio and skills
- **Services** — narrative direction, commercial/branded content, music videos, post supervision
- **Contact** — email and social links

## Customizing

Everything lives in `index.html`:

- Replace the `iframe` `src` in the **Showreel** section and each `.work-card`'s `data-video` attribute with your own YouTube/Vimeo embed URLs.
- Swap the Unsplash placeholder images (`background`/`src` URLs) for your own stills or posters.
- Update the name, tagline, bio, email and social links to match yours.

## Running locally

No build tools needed — just open `index.html` in a browser, or serve the folder:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deploying

This is a static site, so it can be hosted directly with GitHub Pages: in the repo settings, enable Pages for this branch (or `main`) with the root as the source.
