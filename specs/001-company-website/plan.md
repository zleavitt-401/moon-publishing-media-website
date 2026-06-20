# Implementation Plan: Moon Publishing Media Company Website

**Branch**: `001-company-website` | **Date**: 2026-02-19 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/001-company-website/spec.md`

## Summary

Build a two-page static company website (Home + Contact) for moonpublishingmedia.com using pure HTML5 + CSS3. The site establishes Moon Publishing Media as a credible independent publisher for Apple Developer Program enrollment. It features a warm, minimal design with an inline SVG logo, Google Fonts typography (Cormorant Garamond + Inter), and responsive layout from 375px to 2560px+. No JavaScript, no build tools, no frameworks.

## Technical Context

**Language/Version**: HTML5 + CSS3 (no version management needed)
**Primary Dependencies**: None — Google Fonts loaded via `<link>` tags (only external resource)
**Storage**: N/A — pure static site, no data persistence
**Testing**: Manual browser testing (mobile + desktop viewports); HTML validation via W3C validator
**Target Platform**: Modern web browsers (Chrome, Safari, Firefox, Edge) on mobile and desktop
**Project Type**: Single static site — flat file structure at repository root
**Performance Goals**: Instant page load (no JS, no build, minimal CSS); sub-1s render on 3G connection
**Constraints**: Zero JavaScript (unless strictly necessary for minor UX, or for the one approved cookieless analytics script), zero dependencies, zero build step
**Scale/Scope**: 2 HTML pages, 1 CSS file, 0 JS files — minimal scope by design

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Evidence |
|-----------|--------|----------|
| I. Pure Static Simplicity | PASS | Two HTML files + one CSS file. No JS, no frameworks, no build tools. YAGNI enforced. |
| II. Semantic & Accessible HTML | PASS | Plan uses `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`. Single `<h1>` per page. `alt` attributes on SVG. Keyboard-accessible `<a>` elements. |
| III. Mobile-First Responsive CSS | PASS | Single `styles.css` file. CSS custom properties for tokens. Flexbox layout. Mobile-first with `min-width` breakpoints. No preprocessors. |
| IV. Zero-Dependency Architecture | PASS | No `package.json`, no `node_modules`. Google Fonts via `<link>` only. Inline SVG logo. Deployable as static files. |
| V. Deployment Readiness | PASS | Repository root is deploy directory. No env vars or server config. Works on any static file server. |

**Gate result: ALL PASS — proceeding to Phase 0.**

## Project Structure

### Documentation (this feature)

```text
specs/001-company-website/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/           # Phase 1 output (page structure contracts)
└── tasks.md             # Phase 2 output (/speckit.tasks command)
```

### Source Code (repository root)

```text
/
├── index.html           # Homepage — hero, about, coming soon
├── contact.html         # Contact page — heading, copy, mailto link
└── styles.css           # Single shared stylesheet (variables → reset → layout → components → utilities)
```

**Structure Decision**: Flat file structure at repository root. No `src/`, no `tests/`, no subdirectories for code. This is the simplest possible structure for a two-page static site, directly aligned with Constitution Principle I (Pure Static Simplicity) and the File & Asset Conventions in the constitution. The `assets/` directory is available if needed but not required for the initial build (inline SVG logo, no external images).

## Post-Design Constitution Re-Check

*Re-evaluated after Phase 1 design artifacts (data-model.md, contracts/, quickstart.md).*

| Principle | Status | Post-Design Evidence |
|-----------|--------|---------------------|
| I. Pure Static Simplicity | PASS | All artifacts describe pure HTML5 + CSS3. No JS, no frameworks, no build tools. No abstractions or unused structures. |
| II. Semantic & Accessible HTML | PASS | Page contracts specify `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`. Single `<h1>` per page. SVG logo has `role="img"`, `aria-labelledby`, `<title>`, `<desc>`. All interactive elements are native `<a>` tags. |
| III. Mobile-First Responsive CSS | PASS | Stylesheet contract defines section order (variables → reset → layout → components → utilities → media queries). CSS custom properties for all tokens. Mobile-first `min-width` breakpoints. Flexbox layout. No preprocessors. |
| IV. Zero-Dependency Architecture | PASS | No `package.json` in any artifact. Google Fonts via `<link>` only. Inline SVG logo. Flat file structure at repo root. Deployable by serving static files. |
| V. Deployment Readiness | PASS | Repo root is deploy directory. No env vars, no server config. Quickstart confirms zero-config deployment to Vercel. |

**Post-design gate result: ALL PASS — no violations introduced.**

## Complexity Tracking

> No violations. All five constitution principles are fully satisfied by the planned approach.
