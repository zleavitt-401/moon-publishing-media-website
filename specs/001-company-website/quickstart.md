# Quickstart: Moon Publishing Media Company Website

**Feature Branch**: `001-company-website` | **Date**: 2026-02-19

## Prerequisites

- A modern web browser (Chrome, Safari, Firefox, or Edge)
- A text editor (VS Code recommended — Live Server extension for hot reload)
- Git installed

## Get Started

```bash
# Clone and switch to feature branch
git clone <repo-url>
cd moon-publishing-media-website
git checkout 001-company-website
```

## Development

There is no build step. Open files directly in a browser or use a local server:

```bash
# Option 1: Open directly
open index.html

# Option 2: VS Code Live Server
# Install "Live Server" extension → right-click index.html → "Open with Live Server"

# Option 3: Python simple server
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## File Overview

| File | Purpose |
|------|---------|
| `index.html` | Homepage — hero, about, coming soon sections |
| `contact.html` | Contact page — heading, copy, mailto link |
| `styles.css` | Single shared stylesheet for both pages |

## Making Changes

1. Edit HTML or CSS files in your text editor
2. Refresh the browser (or Live Server auto-refreshes)
3. Test on both pages — header and footer must match
4. Test at mobile (375px) and desktop (1200px+) widths using browser DevTools

## Testing Checklist

- [ ] Homepage loads with logo, hero, about, and coming soon sections
- [ ] Contact page loads with heading, copy, and prominent email link
- [ ] Email link opens mail client when clicked
- [ ] Navigation works: Contact link → contact.html, Logo → index.html
- [ ] Header and footer are visually identical on both pages
- [ ] Responsive: no horizontal scroll at 375px; centered content at 1200px+
- [ ] Typography: serif headings (Cormorant Garamond), sans-serif body (Inter)
- [ ] No rounded corners on any element
- [ ] No JavaScript errors in browser console
- [ ] Fallback fonts render if Google Fonts fail (disconnect network to test)

## Deployment

Push to GitHub → Vercel auto-deploys from the `main` branch:

```bash
git add index.html contact.html styles.css
git commit -m "your message"
git push
```

No environment variables, build configuration, or server setup required.

## Key Design Tokens

These CSS custom properties control the visual identity:

```css
--color-bg: #FAF9F6;       /* Warm off-white background */
--color-text: #1C1C1C;     /* Soft near-black text */
--color-accent: #C4A0A0;   /* Muted dusty rose */
--font-heading: 'Cormorant Garamond', serif;
--font-body: 'Inter', sans-serif;
```

## Constraints

- **Zero JavaScript** — no JS files, no inline scripts (unless strictly necessary)
- **Zero rounded corners** — angular design only
- **Zero dependencies** — no package.json, no node_modules, no build tools
- **Single stylesheet** — all CSS in `styles.css`
- **Inline SVG** — logo embedded directly in HTML, no external image files
