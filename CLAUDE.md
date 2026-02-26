# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file, zero-dependency static landing page (`index.html`) with a red-tinted Matrix-style terminal aesthetic. No build step, no package manager, no backend — open the file directly in a browser or deploy as-is to any static host (e.g. Vercel, GitHub Pages).

## Architecture

Everything lives in one file (`index.html`) with three logical sections:

1. **CSS** — All styles are inline in `<style>`. Uses CSS custom properties for the color palette. Fonts loaded from Google Fonts (`Share Tech Mono`, `VT323`).

2. **HTML** — Three layered elements:
   - `#matrixCanvas` (z-index 0) — canvas for the rain animation
   - `#scanlines` (z-index 5) — fixed overlay for CRT scanlines effect
   - `#app` (z-index 10) — the actual UI: header → `#terminal` → footer

3. **JavaScript** — One self-contained block at the bottom of `<body>`:
   - **Matrix rain IIFE** — canvas-based animation with white/gray characters, resets on `window resize`

## Color Palette Gotcha

The CSS custom properties are named `--green*` but the actual values are **red** (`#ff2200`, `#cc1a00`, `#3b0000`). The Matrix rain also uses white/gray instead of green. Keep this naming inconsistency in mind when reading or modifying styles — the variable names don't match their colors.

## Terminal Panel

`#terminal` is a purely decorative panel with no chat or input functionality. It contains:
- `.term-bar` — title bar with three dots, RM badge SVG, and a pulsing status dot
- `#content` — static text lines, each with a `> ` prefix via CSS (`::before`)

To update the displayed text, edit the `.line` divs inside `#content` in the HTML.

## Key Design Decisions

- **No framework, no backend** — plain static HTML; zero external dependencies beyond Google Fonts.
- **No chatbot or webhook** — the n8n integration and all chat logic were intentionally removed.
- The `.ascii-logo` title renders at fixed opacity — the `flicker` animation was removed. Do not re-add it.
- The Matrix rain canvas opacity is controlled in CSS (`opacity: 0.18`) — raise/lower to adjust background effect prominence.
- CRT scanline intensity is set by the `rgba(0,0,0,0.07)` value in the `repeating-linear-gradient` on `#scanlines`.

## Custom Agents

The `.claude/agents/landing-page-cro-expert.md` defines a CRO (Conversion Rate Optimization) expert agent for analyzing and optimizing landing pages. It is aware of this project's single-file architecture and design constraints.
