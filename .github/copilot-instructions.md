## Purpose
This repo is a small static invitation site. The goal of these instructions is to make AI coding agents productive quickly when editing the site or adding simple features.

## Big picture
- Single-page, static HTML with two entry points: `index.html` (hand-edited, interactive) and `index2.html` (exported from figma.to.website). Prefer edits to `index.html` unless the user asks to regenerate the figma export.
- Assets served from top-level `img/` and `audio/` directories and referenced with root paths (example: `/img/carte.jpg`, `/audio/Heuss L'Enfoiré Bar-Mitzvah.mp3`).
- Styling is mostly inline in `index.html` and Tailwind is included via CDN (`https://cdn.tailwindcss.com`). No bundler or build step.
- Interactivity implemented with small inline scripts in `index.html` (see `openEnvelope()`, `toggleMusic()`, `submitForm()`).

## Key files to inspect
- `index.html` — primary interactive implementation (CSS variables in `:root`, envelope animation, music control). Look here first for behavioral changes.
- `index2.html` — auto-generated Figma export; large auto-generated CSS/HTML. Only modify when intentionally replacing the design from Figma.
- `img/` and `audio/` — media assets. Keep file names and root paths stable; many references use absolute paths starting with `/`.

## Project-specific patterns & conventions
- Inline CSS: a large, handcrafted `<style>` block drives layout and the envelope animation (variables like `--paper-color`, `--liner-color` are defined in `:root`).
- DOM-driven animation: `openEnvelope()` toggles CSS classes (`.flap.open`, `.card-preview.slide-out`, `.card-preview.highlight`) to animate the UI — modify classes consistently in both CSS and JS.
- Music control: audio element has id `bg-music` and button `music-toggle`. Use these IDs if adding controls or telemetry.
- Minimal JS: the form `onsubmit="submitForm(event)"` is client-side only and fakes a submit. There is no backend in this repo.
- External dependencies are CDN-based (Tailwind, Font Awesome, Google Fonts). Changes to classes assume Tailwind utilities are available at runtime.

## How to run / test locally
- Open `index.html` directly in a browser for quick checks.
- For correct asset paths (root `/img` and `/audio`) run a simple static server from the repo root, e.g.:

  python3 -m http.server 8000

Then open `http://localhost:8000/index.html`.

## Safe edit recommendations
- Edit `index.html` for behavior and animation fixes. If you change CSS class names, update the JS selectors used by `openEnvelope()` and `toggleMusic()`.
- Avoid renaming asset files in `img/` and `audio/` without updating every absolute reference starting with `/`.
- If adding new tooling (build step, bundler), document it in this file and keep the original `index.html` runnable without the build step.

## Examples (search targets)
- Toggle envelope: `openEnvelope()` and `flap.open` (in `index.html`).
- Music element: `id="bg-music"` and button `id="music-toggle"`.
- Card image: `/img/carte.jpg`

## Pull request hints
- Keep changes small and focused (this is a tiny static site).
- Include screenshots or short GIFs for UI animation changes (envelope open, card highlight, music button states).

If anything here is unclear or you'd like different emphasis (tests, CI, or converting to a build pipeline), tell me which areas to expand. 
