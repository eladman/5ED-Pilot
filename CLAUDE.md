# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

Landing page for **5ED × חמש אצבעות** — an AI-powered personal training pilot program for Israeli teens (ages 12-17). Hebrew RTL site with dark-mode athletic aesthetic.

## Commands

```bash
npm run dev      # Start Vite dev server (localhost:5173)
npm run build    # Production build → dist/
npm run preview  # Preview production build locally
```

## Architecture

Single-page static site using **vanilla HTML/CSS/JS** with **Vite** as the only dependency. No framework, no TypeScript.

- `index.html` — The entire landing page: markup, embedded `<style>` CSS (~540 lines), and `<script>` JS (~75 lines)
- `design.md` — Design system and branding guide (source of truth for colors, typography, components, RTL rules)
- `vite.config.js` — Minimal Vite config (root: `.`, output: `dist/`)

## Design System (from design.md)

- **Colors:** `--orange: #FF8714` (primary), `--dark: #0A0A0F` (background), `--green: #22C55E` (accents)
- **Fonts:** Oswald (display/headings), Heebo (body text) — loaded from Google Fonts
- **Layout:** Dark mode only, RTL (`direction: rtl`), mobile-first with single breakpoint at 480px
- **Effects:** SVG grain texture overlay, entrance-only animations (no looping except pulse indicators), no box shadows
- **Philosophy:** "Athletic fintech" — sports brand × app feel. Clean, premium, minimal.

## Key Conventions

- All user-facing text is in **Hebrew**
- CSS uses custom properties defined in `:root` — always use these instead of raw values
- Scroll reveal animations use IntersectionObserver with `.reveal`/`.visible` classes
- The registration form currently simulates submission (no backend connected yet — see TODO comments in JS)
- Responsive sizing uses `clamp()` for fluid typography
