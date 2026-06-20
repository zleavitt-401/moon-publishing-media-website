<!-- Sync Impact Report
  Version change: 1.1.0 → 1.2.0
  Amended:
    - I. Pure Static Simplicity: added a named exception permitting a single
      cookieless, privacy-respecting analytics script (Vercel Web Analytics)
      alongside the existing minor-UX-enhancement JS allowance
    - III. Mobile-First Responsive CSS: removed the implicit "zero rounded
      corners" expectation — rounded corners are now a permitted deliberate
      design choice (previously enforced via FR-013, not a constitution
      principle itself, but referenced from CLAUDE.md)
  Added sections: none (Sync Impact Report only; principle bodies amended in place)
  Removed sections:
    - "Zero rounded corners" reminder in CLAUDE.md Core Principles
    - App Teaser Policy section in CLAUDE.md
  Templates requiring updates:
    - .specify/templates/plan-template.md ✅ compatible (no changes needed)
    - .specify/templates/spec-template.md ✅ compatible (no changes needed)
    - .specify/templates/tasks-template.md ✅ compatible (no changes needed)
    - CLAUDE.md ✅ updated (App Teaser Policy removed, rounded-corners
      reminder removed, analytics exception documented)
    - specs/001-company-website/spec.md ✅ updated (FR-006, FR-013, and the
      related acceptance scenario revised to match the new rules)
    - specs/001-company-website/plan.md ✅ updated (constraint line revised)
    - specs/001-company-website/quickstart.md ✅ updated (checklist and
      reminder lines revised)
  Follow-up TODOs: none
-->

# Moon Publishing Media Website Constitution

## Core Principles

### I. Pure Static Simplicity

Every decision MUST favor the simplest viable approach. This is a single-page
company website, not a web application.

- No JavaScript frameworks, build tools, bundlers, or transpilers.
- No CSS frameworks (Bootstrap, Tailwind, etc.).
- Pure HTML5 + CSS3 only.
- JavaScript is permitted ONLY for minor UX enhancements (e.g., mailto link
  construction to prevent spam scraping) and for a single cookieless,
  privacy-respecting analytics script (Vercel Web Analytics). The analytics
  script MUST NOT set cookies or collect personal data, and therefore
  requires no consent banner. No other analytics, tracking, or third-party
  script is permitted. If JS is added, it MUST be inline or in a single
  small script — no external JS dependencies beyond the one approved
  analytics script.
- YAGNI is strictly enforced: do not add features, abstractions, or tooling
  "for later." Build exactly what is needed now.

### II. Semantic & Accessible HTML

All markup MUST use semantic HTML5 elements to communicate document structure
clearly to browsers, screen readers, and search engines.

- Use `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>` — not generic
  `<div>` wrappers — for page structure.
- Heading hierarchy MUST be logical (`<h1>` once per page, then `<h2>`,
  `<h3>` as needed).
- All interactive elements MUST be keyboard-accessible.
- Images and icons MUST include appropriate `alt` attributes.
- HTML MUST validate as clean HTML5 with no console errors.

### III. Mobile-First Responsive CSS

The site MUST be fully usable on mobile devices, tablets, and desktops.

- Use CSS Grid and flexbox for layout.
- CSS MUST be organized in a single `styles.css` file following this order:
  CSS custom properties (variables) → reset/normalize → layout → components
  → utilities.
- Use CSS custom properties for colors, fonts, and spacing to ensure
  consistency and easy theming.
- Media queries MUST use a mobile-first approach (base styles for mobile,
  `min-width` breakpoints for larger screens).
- No CSS preprocessors (Sass, Less, etc.).

### IV. Zero-Dependency Architecture

The project MUST have zero runtime dependencies and zero build dependencies.

- No `package.json`, no `node_modules`, no build step.
- Google Fonts loaded via `<link>` tags in `<head>` — this is the only
  external resource permitted.
- SVG logo MUST be inline in HTML (no external image file needed for the
  logo placeholder).
- Any additional assets (images, icons) MUST live in a single `/assets`
  folder at the project root.
- The site MUST be deployable by serving static files — no server-side
  processing.

### V. Deployment Readiness

The site MUST be ready for Vercel static deployment via GitHub integration
at all times.

- The repository root MUST be the deploy directory (no subdirectory builds).
- Every commit to `main` SHOULD produce a deployable state.
- No environment variables, secrets, or server configuration required.
- The site MUST work correctly when served from any static file server.

## Tech Stack Constraints

| Layer       | Choice                  | Alternatives Prohibited         |
|-------------|-------------------------|---------------------------------|
| Markup      | HTML5                   | JSX, Pug, EJS, Handlebars      |
| Styling     | CSS3 (single file)      | Sass, Less, Tailwind, Bootstrap |
| JavaScript  | None (or minimal inline; one cookieless analytics script permitted) | React, Vue, jQuery, any lib, other analytics/tracking |
| Fonts       | Google Fonts via `<link>`| Self-hosted, Adobe Fonts        |
| Icons/Logo  | Inline SVG              | Icon fonts, external PNGs       |
| Hosting     | Vercel (static)         | SSR, serverless functions       |
| VCS         | Git + GitHub            | —                               |

## File & Asset Conventions

The complete project file structure:

```
moon-publishing-media-website/
├── index.html            # Single-page site (all content)
├── styles.css            # Single stylesheet (CSS Grid layout)
├── assets/               # Images and static assets (if any)
├── .specify/             # Spec Kit working files
└── .claude/              # Claude Code commands
```
- File naming MUST use lowercase with hyphens (kebab-case).

## Governance

This constitution supersedes all other development guidance for this project.
Any proposed change that conflicts with these principles MUST be justified
against the constitution before implementation.

- **Amendments**: Any principle change requires updating this document,
  incrementing the version, and propagating changes to dependent Spec Kit
  artifacts.
- **Versioning**: MAJOR for principle removals or redefinitions, MINOR for
  new principles or material expansions, PATCH for clarifications.
- **Compliance**: Every spec, plan, and task MUST pass a Constitution Check
  validating alignment with these principles before implementation begins.

**Version**: 1.2.0 | **Ratified**: 2026-02-19 | **Last Amended**: 2026-06-19
