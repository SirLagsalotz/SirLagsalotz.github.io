# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

The repo has a Gulp 4 build system for the legacy SCSS → CSS pipeline (used by old template files only):

```bash
npm install    # install dependencies
npm start      # runs `gulp watch` — compiles SCSS, starts BrowserSync on port 3000
```

The **active site** does not use Gulp. Edit `assets/css/frutiger-aero.css` directly — no build step required.

## Architecture

Static GitHub Pages site deployed to `andremoura.ca` (defined in `CNAME`). All active pages are self-contained HTML files using a shared CSS file.

### Active Pages

| File | Purpose |
|---|---|
| `index.html` | Landing / home |
| `about.html` | About Me |
| `resume.html` | Resume with timeline layout |
| `social.html` | Social media links grid |
| `404.html` | Not found |

`social.html` additionally loads `vendor/fontawesome-free/css/all.min.css` for the platform icons.

### Page Structure Pattern

Every page has this exact body structure (order matters for z-index stacking):

```html
<div class="light-rays"></div>        <!-- fixed sunburst overlay -->
<div class="water-line"></div>         <!-- fixed shimmer at ~43% down -->
<div class="clouds">...</div>          <!-- 4 CSS cloud divs drifting across sky -->
<div class="bubbles">...</div>         <!-- 12 soap bubble divs floating upward -->
<div class="fish-container">...</div>  <!-- 7 emoji fish swimming (🐠🐟🐬🐡) -->
<div class="sparkles">...</div>        <!-- 10 twinkling star divs -->
<nav class="navbar navbar-expand-md">...</nav>
<div class="page-content">...</div>    <!-- z-index: 1, all visible content here -->
<footer>...</footer>
```

All background layers are `position: fixed; z-index: 0; pointer-events: none`.

### CSS — `assets/css/frutiger-aero.css`

Single source of truth for all styling. Bootstrap 4 is kept only for grid and navbar collapse.

**Key component classes:**
- `.glass-panel` — frosted-glass card (backdrop-filter blur, semi-transparent white, gloss sheen via `::before`)
- `.btn-aero` — glossy aqua pill button with two-stop gradient split at 49%/50%
- `.hero-card` — centered full-viewport hero variant of `.glass-panel`
- `.error-card` — centered 404 variant
- `.page-header-card` / `.content-card` — inner page layout cards (max-width 860px, centered)
- `.timeline-item` + `.timeline-dot` — resume timeline rows
- `.skill-tag` — glossy pill badge
- `.social-grid` / `.social-link` / `.social-icon` — social page grid layout

**Background animation classes** (all `position: fixed`, driven purely by CSS keyframes):
- `.bubble` — soap-style with `::before` specular highlight and `::after` reflection; `floatUp` keyframe
- `.cloud` / `.cloud-1` through `.cloud-4` — CSS blob clouds; `driftCloud` keyframe
- `.fish` / `.fish-1` through `.fish-7` — emoji fish; `swimRight` / `swimLeft` keyframes (swimRight includes `scaleX(-1)` in keyframes to flip left-facing emoji)
- `.sparkle` / `.sparkle-1` through `.sparkle-10` — 8-point star via `clip-path polygon`; `twinkle` keyframe
- `.water-line` — single div with gradient + blur; `waterShimmer` keyframe

### Legacy Files (unused)

- `oldindex.html` — archived coming-soon page, not linked
- `scss/`, `css/`, `js/resume.js` — original StartBootstrap Resume template, not used
- `assets/img/vapor2.jpg`, `assets/img/egg.png` — old background images, not referenced
- `Refrence Images/` — Frutiger Aero wallpapers used as design reference
