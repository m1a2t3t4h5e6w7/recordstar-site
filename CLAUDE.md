# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

The marketing landing page for **recordstar.shop** — a one-page static site for STAR Recorder, a Chrome extension that records screen/window/tab/webcam plus microphone and downloads the video locally.

The site is four files. `index.html` is the entire product; everything else is deployment configuration.

## Commands

There is no build, no test suite, no linter, and no package manifest. Editing `index.html` is the whole development loop.

Preview locally:

```
python3 -m http.server 8000   # then open http://localhost:8000
```

## Deployment

Deployed by GitHub Pages serving the repo root directly — there is no Actions workflow, so **a push to the Pages branch is the deploy**. Two files exist only to make that work:

- `CNAME` — pins the custom domain `recordstar.shop`. Deleting or rewriting it breaks the domain mapping.
- `.nojekyll` — stops Pages from running the content through Jekyll.

`deploy.mjs` is listed in `.gitignore`: a deploy script exists on the author's machine but is not in version control, so the deploy path is not fully reproducible from this repo. Don't recreate or guess at it — ask.

## Conventions

`index.html` is deliberately self-contained: CSS lives in a single `<style>` block, the favicon is an inline `data:` SVG, and there are no external assets, fonts, scripts, or network requests of any kind. Preserve that — do not introduce a build step, a bundler, npm dependencies, or CDN links.

Colors are CSS custom properties on `:root` (`--bg`, `--panel`, `--border`, `--text`, `--muted`, `--accent`, `--rec`). Change the theme through those variables rather than hardcoding hex values in rules.

## Page content is coupled to the product's status

The page asserts facts about STAR Recorder that go stale as the extension ships:

- It states the extension "isn't in the Chrome Web Store yet" and gives manual `chrome://extensions` → Developer mode → **Load unpacked** install steps. All of that is replaced by a store link at launch.
- The footer says the product is "in early development."
- Install step 1 says "Get the extension folder" but the page has no download link, and the hero CTA is only an in-page anchor to `#install`. Wiring up a real download or store URL is the main outstanding gap.
