# Quickstart: Stream Reader Product Page + Website Professionalization

## Files in this feature

```
/
├── index.html          # EDIT: replace .coming-soon content with named Stream Reader
│                        #       block; remove embedded #contact section; refresh
│                        #       header (add Stream Reader nav) + footer; add head meta
├── streamreader.html   # NEW: dedicated product page (6 sections, FR-004)
├── contact.html        # EDIT: header/footer refresh; reader/educator/org welcome copy
├── privacy.html        # EDIT: header/footer refresh ONLY — content deferred, do not rewrite
├── styles.css          # EDIT: rename/repurpose .coming-soon → .stream-reader-teaser;
│                        #       add Stream Reader page styles + app-blue secondary accent;
│                        #       add prefers-reduced-motion GIF rule
└── assets/
    ├── favicon.svg
    ├── og-image.png            # default/site OG image
    └── streamreader/
        ├── app-icon.png
        ├── streaming-demo.gif
        ├── streaming-demo-static.png   # first-frame export for reduced-motion
        ├── library.png                 # Library screenshot
        ├── customization.png           # Customization screenshot
        ├── app-store-badge.svg         # official Apple artwork (unmodified)
        └── og-streamreader.png         # OG image for the Stream Reader page
```

Any asset not yet supplied ships as a clearly labeled placeholder (asset-gating clarification); real files swap in via a follow-up commit.

## Asset prep notes

- **App Store badge**: download official "Download on the App Store" artwork from Apple's marketing resources; use unmodified. Do NOT recreate it.
- **Reduced-motion fallback**: export the GIF's first frame once to `streaming-demo-static.png`. A CSS `@media (prefers-reduced-motion: reduce)` rule hides the GIF and shows the static frame (no JS).
- **GIF optimization**: keep the GIF small (FR-023) — trim length/frames/colors so it doesn't materially slow load.
- **App-blue accent**: pick the secondary blue from the app icon/screenshots; verify contrast (FR-021) before using for text or interactive elements.

## No build step

```bash
# Open directly in a browser, or use VS Code Live Server.
# Deploy: push to GitHub → Vercel auto-deploys.
# Enable Web Analytics in the Vercel project dashboard so /_vercel/insights/script.js serves.
```

## Verification checklist (maps to spec)

- [ ] Header identical on all 4 pages, includes Stream Reader + Contact nav, no Privacy link [FR-002]
- [ ] Footer identical on all 4 pages, links Stream Reader + Privacy [FR-003]
- [ ] index.html: Stream Reader block replaces Coming Soon in same grid slot; embedded contact section removed [FR-013, clarification]
- [ ] index.html still establishes MPM self-care identity; soft future-content language kept separate [FR-012, FR-014]
- [ ] streamreader.html: 6 sections in order; tagline exact; badge primary + browser link secondary above the fold [FR-004, FR-005, FR-006, FR-007]
- [ ] Library + Customization screenshots present with descriptive alt [FR-009, FR-019]
- [ ] Privacy callout links to privacy.html [FR-010]
- [ ] contact.html welcomes readers, educators, organizations; mailto present [FR-015, FR-016]
- [ ] Exactly one `<h1>` per page; logical headings [FR-020]
- [ ] One cookieless analytics script site-wide; no consent banner [FR-018, SC-010]
- [ ] Favicon + per-page title/description + OG image; link preview renders [FR-025, FR-026, SC-007]
- [ ] prefers-reduced-motion swaps GIF for static frame [FR-022]
- [ ] Keyboard-operable interactive elements w/ visible focus [FR-024]
- [ ] Contrast incl. dusty rose on off-white + app blue verified [FR-021]
- [ ] No horizontal scroll 375px–2560px+; no console errors [FR-030, SC-008, SC-009]
- [ ] Zero broken internal links [SC-003]

## Constraints (from constitution v1.2.0)

- **Pure HTML5 + CSS3** — no frameworks, no build tools.
- **One JS exception**: the cookieless Vercel Web Analytics script. No other JS.
- **Rounded corners permitted** as a deliberate, consistent design choice.
- **Single stylesheet** `styles.css`, organized: variables → reset → layout → components → utilities.
- **Assets** under `/assets/`; kebab-case filenames.
- **Static deploy** at repo root via Vercel; every commit deployable.
