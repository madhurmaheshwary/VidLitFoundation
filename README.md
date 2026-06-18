# VidLitFoundation

Landing page for Vidarbha Literary Foundation — a community initiative running
reading outreach programmes and a free book exchange library across Nagpur
and the Vidarbha region.

## Stack

Plain HTML, CSS, and a few lines of vanilla JS. No build step, no framework,
no dependencies — deploys as a static site anywhere, including Vercel.

## Local preview

Open `index.html` directly in a browser, or serve it locally:

```bash
python3 -m http.server 8080
```

Then visit `http://localhost:8080`.

## Deploying

This is a static site, so on Vercel just import the repo and leave the
framework preset as "Other" — no build command or output directory needed.

## Structure

```
index.html     -- page markup and content
styles.css     -- design system and layout (tokens at the top of the file)
```

## Editing content

All copy lives directly in `index.html`. The colour palette, type scale, and
spacing tokens are defined as CSS variables at the top of `styles.css` under
`:root` — change values there to retheme the whole page.
