# CLAUDE.md
> 📜 **Single Source of Truth**: All architectural principles, constraints,
> and quality standards are in `.specify/constitution.md`
> Always check constitution before design decisions.

## Project Overview
**Moon Publishing Media Website** — A simple, professional two-page static site for moonpublishingmedia.com. Primary purpose: satisfy Apple Developer Program organization enrollment requirements while establishing real company credibility. Secondary purpose: introduce MPM as an independent publisher of wellness/self-care content with a digital app in development.

## Tech Stack
- **Language**: Pure HTML5 + CSS3 — no frameworks, no build tools, no JavaScript
- **Fonts**: Google Fonts (Cormorant Garamond + Inter) via `<link>` in `<head>`
- **Logo**: Inline SVG (crescent moon + wordmark) — no external image files
- **Deployment**: Vercel (static site) connected to Namecheap domain DNS

## File Structure
```
/
├── index.html        # Homepage
├── contact.html      # Contact page
├── styles.css        # Single shared stylesheet
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
- Mobile-first, responsive via flexbox (375px → 1200px+)
- Semantic HTML: `<header>`, `<main>`, `<footer>`, `<section>`

## Design Tokens (quick reference)
```css
--color-bg: #FAF9F6;
--color-text: #1C1C1C;
--color-accent: #C4A0A0;
--font-heading: 'Cormorant Garamond', serif;
--font-body: 'Inter', sans-serif;
```

## Pages
| Page | File | Key Sections |
|------|------|-------------|
| Home | index.html | Hero, About, Coming Soon teaser, Footer |
| Contact | contact.html | Heading, copy, mailto link, Footer |

## Contact Email
`info@moonpublishingmedia.com` — displayed as a prominent `mailto:` link on contact.html. This is the only point of contact on the site.

## App Teaser Policy
The app section on index.html must stay vague — **no app name, no screenshots, no feature list.** Describe goals only: accessibility, focus, reading for real people. Update this section once the app launches publicly.

## Current Focus
- Initial build: both pages + stylesheet from scratch
- Placeholder SVG logo (to be replaced when real logo is provided)
- Deploy to Vercel and connect moonpublishingmedia.com domain via Namecheap DNS

## Active Technologies
- HTML5 + CSS3 (no version management needed) + None — Google Fonts loaded via `<link>` tags (only external resource) (001-company-website)
- N/A — pure static site, no data persistence (001-company-website)

## Recent Changes
- 001-company-website: Added HTML5 + CSS3 (no version management needed) + None — Google Fonts loaded via `<link>` tags (only external resource)
