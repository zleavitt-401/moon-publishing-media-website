# CLAUDE.md
> 📜 **Single Source of Truth**: All architectural principles, constraints,
> and quality standards are in `.specify/constitution.md`
> Always check constitution before design decisions.

## Project Overview
**Moon Publishing Media Website** — A single-page static site for moonpublishingmedia.com. Primary purpose: satisfy Apple Developer Program organization enrollment requirements while establishing real company credibility. Secondary purpose: introduce MPM as an independent publisher of wellness/self-care content with a digital app in development.

## Tech Stack
- **Language**: Pure HTML5 + CSS3 — no frameworks, no build tools, no JavaScript
- **Fonts**: Google Fonts (Cormorant Garamond + Inter) via `<link>` in `<head>`
- **Logo**: Inline SVG (crescent moon + wordmark) — no external image files
- **Deployment**: Vercel (static site) connected to Namecheap domain DNS

## File Structure
```
/
├── index.html        # Single-page site (all content)
├── styles.css        # Single stylesheet (CSS Grid layout)
└── CLAUDE.md
```

## Development Workflow
```bash
# No build step — open directly in browser or use Live Server in VS Code

# Deploy: push to GitHub → Vercel auto-deploys
git add .
git commit -m "your message"
git push
```

## Core Principles
See `.specify/constitution.md` for full standards. Key reminders:
- **Zero JavaScript** unless strictly necessary
- **Zero rounded corners** — angular, intentional design
- CSS organized: variables → reset → layout → components → utilities
- Mobile-first, responsive via CSS Grid + flexbox (375px → 1200px+)
- Semantic HTML: `<header>`, `<main>`, `<footer>`, `<section>`

## Design Tokens (quick reference)
```css
--color-bg: #E8EDF2;
--color-text: #1C1C1C;
--color-accent: #C4A0A0;
--font-heading: 'Cormorant Garamond', serif;
--font-body: 'Inter', sans-serif;
```

## Page Sections
All content lives in a single `index.html` with an editorial two-column CSS Grid layout on desktop (single column on mobile):

| Section | Description |
|---------|-------------|
| Hero | "Words that move you." tagline + company description (left column) |
| About | "Who We Are" — publisher philosophy (right column, top) |
| Coming Soon | App teaser — vague, no details (right column, bottom) |
| Contact | "Say Hello" + mailto link — compact horizontal bar |
| Footer | Copyright |

## Contact Email
`info@moonpublishingmedia.com` — displayed as a `mailto:` link in the contact section. This is the only point of contact on the site.

## App Teaser Policy
The app section on index.html must stay vague — **no app name, no screenshots, no feature list.** Describe goals only: accessibility, focus, reading for real people. Update this section once the app launches publicly.

## Current Focus
- Single-page consolidated layout with editorial CSS Grid
- Placeholder SVG logo (to be replaced when real logo is provided)
- Deploy to Vercel and connect moonpublishingmedia.com domain via Namecheap DNS

## Active Technologies
- HTML5 + CSS3 (no version management needed) + None — Google Fonts loaded via `<link>` tags (only external resource) (001-company-website)
- N/A — pure static site, no data persistence (001-company-website)

## Recent Changes
- 001-company-website: Added HTML5 + CSS3 (no version management needed) + None — Google Fonts loaded via `<link>` tags (only external resource)
