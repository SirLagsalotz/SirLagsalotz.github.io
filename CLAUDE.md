# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

The repo has a Gulp 4 build system for the legacy SCSS → CSS pipeline (used by the old template files):

```bash
npm install          # install dependencies
npm start            # runs `gulp watch` — compiles SCSS, minifies JS, starts BrowserSync on port 3000
```

The **active site** (`index.html`, `about.html`, `resume.html`, `404.html`) uses a hand-crafted CSS file at `assets/css/frutiger-aero.css` and does **not** go through Gulp. Edit that file directly — no build step required.

## Architecture

This is a static GitHub Pages site deployed to `andremoura.ca` (defined in `CNAME`).

### Active Pages & Their CSS
All active pages share the same structure:
- Load `assets/bootstrap/css/bootstrap.min.css` (Bootstrap 4 grid/utilities)
- Load `assets/css/frutiger-aero.css` (all custom styling — Frutiger Aero theme)
- JS: `assets/js/jquery.min.js` + `assets/bootstrap/js/bootstrap.min.js`

The Frutiger Aero CSS file is the single source of truth for all visual styling. Bootstrap is kept only for the responsive grid and navbar collapse behavior.

### Page Structure Pattern
Every page follows this pattern:
1. `<div class="light-rays">` — fixed background light effect
2. `<div class="bubbles">` with 12 `<div class="bubble">` children — animated floating orbs
3. `<nav class="navbar navbar-expand-md">` — glassy navbar
4. `<div class="page-content">` — wraps all visible content (z-index above bubbles)
5. `<footer>` — simple footer

### Key CSS Classes
- `.glass-panel` — the core frosted-glass card component (use for all content panels)
- `.btn-aero` — glossy aqua button (use instead of Bootstrap `.btn`)
- `.hero-card` / `.error-card` — variants of `.glass-panel` for full-page-centered layouts
- `.page-header-card` / `.content-card` — for inner page layouts
- `.timeline-item` + `.timeline-dot` — resume timeline rows
- `.skill-tag` — glossy pill badge for skills/interests

### Legacy Files
- `oldindex.html` — archived coming-soon page, not linked anywhere
- `scss/`, `css/`, `js/resume.js` — part of the original StartBootstrap Resume template, not used by active pages
- `assets/img/vapor2.jpg`, `assets/img/egg.png` — old background images, no longer referenced
