# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Lectio Pages — a static GitHub Pages site for the **Lectio** app (reading-based English learning, targeting Korean speakers, expanding to multilingual markets).

Two roles:
1. **Marketing landing** — `index.html` showcases the app to prospective users (pre-install).
2. **Legal hosting** — `privacy.html` / `terms.html` (+ `.en.html`) provide the public URLs required for Play Store / App Store listings.

Hosted at: `agentic-education/lectio-pages` on GitHub Pages.
Sibling repos: `agentic-education/lectio` (private app code), `ykmaeng/ikda-columns` / `ykmaeng/ikda-originals` (OTA content).

## Architecture

No build system. All pages are self-contained HTML with inline CSS and vanilla JS.

- **index.html** — Marketing landing (Korean copy, light cream theme, scroll-reveal sections).
- **privacy.html** / **privacy.en.html** — Privacy policy (Korean + English).
- **terms.html** / **terms.en.html** — Terms of service (Korean + English).
- **icon_512.png** — App icon (copied from the main `lectio` repo's `src-tauri/icons/`).

## Conventions

- **Language**: UI copy is Korean. Brand name "Lectio" stays English. English-only legal pages live as `.en.html` siblings.
- **Fonts**: `Lora` + `Noto Serif KR` for serif body (matches app's reading aesthetic). `Inter` for sans/UI labels.
- **Color palette** — matches Lectio app brand:
  - `--cream` #fbf8ef (page bg)
  - `--cream-deep` #f4ecd6 (alt section bg)
  - `--ink` #2a2018, `--ink-soft` #4a3e30, `--muted` #8a7a68
  - Accent rays: `--plum` #6f57a4 / `--wine` #a44d68 / `--gold` #a07a2e / `--terra` #965c39 / `--forest` #327d57
- **No external JS** dependencies. Inline `<script>` blocks only. ES5-safe (avoid optional chaining etc. for old WebView fallback).
- **Commits**: Korean messages.

## Updating Legal Content

The canonical source is `lectio/scripts/export-legal-static.mjs` in the main app repo. To regenerate:

```bash
cd ../lectio
node scripts/export-legal-static.mjs   # outputs to lectio/docs/
cp ../lectio/docs/privacy.html ../lectio/docs/privacy.en.html ../lectio/docs/terms.html ../lectio/docs/terms.en.html .
```

When the app's `LegalContent.tsx` changes (in-app legal viewer), keep this repo in sync.

## Adding New Pages

- Keep them self-contained. Reuse the color palette via inline `:root` CSS variables.
- Link from `index.html` footer and any relevant nav.
- For SEO: include `<meta name="description">` and `og:` tags.

## Development

Open in browser directly or serve with any static server:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deployment

Pushed to `main`, GitHub Pages auto-deploys (Settings → Pages → Source: main branch, root folder).
Public URL: `https://agentic-education.github.io/lectio-pages/`

Store listings should reference:
- Privacy: `https://agentic-education.github.io/lectio-pages/privacy.html`
- Terms: `https://agentic-education.github.io/lectio-pages/terms.html`
