# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Egg is a single-file static web app (`egg-chirp.html`) that generates CHIRP-compatible CSV files for programming FRS, GMRS, and MURS radios. It is deployed via GitHub Pages.

There is no build system, no package manager, no dependencies, and no tests. The entire application — HTML structure, CSS, and JavaScript — lives in `egg-chirp.html`.

## Architecture

The file is organized in this order:

1. **CSS** (inline `<style>`) — dark-theme UI using CSS custom properties (`--bg`, `--amber`, etc.)
2. **HTML** — five step cards (`#s1`–`#s5`), only one visible at a time via the `.hidden` class
3. **JavaScript** (inline `<script>`) structured as:
   - **Channel data** — `CH[]` (FRS/GMRS), `MURS_CH[]`, `DCS[]`, `CTCSS[]` constant arrays
   - **State** — single `S` object holds all wizard state (selected services, channels, privacy settings, per-channel overrides)
   - **Step handlers** — one section per step wired to DOM events; `show(n)` switches active step
   - **CSV builder** — `buildRows()` assembles the channel list; `buildCSV()` formats it as CHIRP CSV; `buildPreview()` renders it in `#csvPrev`
   - **Download** — `#dlBtn` triggers a Blob download of the generated CSV

## Key Design Constraints

- **No external JS** — all logic is vanilla JS, no frameworks or libraries
- **Single file** — everything must stay in `egg-chirp.html`; do not split into separate files
- **No server** — deployed as a static GitHub Pages site; there is no backend

## Deployment

Push to `main` — GitHub Pages serves `egg-chirp.html` directly at the URL in `README.md`.
