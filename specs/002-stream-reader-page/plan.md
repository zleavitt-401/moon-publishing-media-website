# Implementation Plan: Stream Reader Product Page + Website Professionalization

**Branch**: `feature/stream-reader-page` | **Date**: 2026-06-20 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/002-stream-reader-page/spec.md`

## Summary

Turn MPM's enrollment-only placeholder into a credible "learn more" destination that names Stream Reader and drives App Store downloads, while preserving MPM's self-care-publisher identity. Add a dedicated `streamreader.html` product page (hero with App Store badge as primary CTA + streamreader.app as secondary; what-it-does GIF; Library + Customization screenshots; privacy callout; who-it's-for; closing CTA). Update the homepage to replace the vague "Coming Soon" teaser with a named Stream Reader block in its existing grid slot, refresh the shared header (add Stream Reader nav) and footer across all pages, welcome readers/educators/organizations on Contact, add favicon/OG/SEO metadata, and add the single cookieless Vercel Web Analytics script. Pure HTML5 + CSS3, no build step, per constitution v1.2.0.

## Technical Context

**Language/Version**: HTML5 + CSS3 (no version management needed)
**Primary Dependencies**: Google Fonts via `<link>` (Cormorant Garamond + Inter); Vercel Web Analytics (single cookieless `<script>`, the only JS)
**Storage**: N/A — static site, no data persistence
**Testing**: Manual browser testing (375px–2560px+ viewports); W3C HTML validation; accessibility spot-checks (contrast, keyboard, reduced-motion, single-h1, alt text); link-graph check
**Target Platform**: Modern web browsers (Chrome, Safari, Firefox, Edge), mobile + desktop
**Project Type**: Multi-file static site — flat `.html` files at repo root sharing one `styles.css`
**Performance Goals**: Fast static load (no build, minimal CSS, one deferred analytics script, optimized GIF per FR-023)
**Constraints**: No frameworks/build tools/bundlers; one permitted JS script (cookieless analytics); rounded corners allowed; single `styles.css`; assets under `/assets/`; deployable at repo root on Vercel
**Scale/Scope**: 4 HTML pages (1 new, 3 edited), 1 CSS file, ~7 image assets (placeholders acceptable until real assets supplied)

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

Evaluated against constitution v1.2.0:

| Principle | Status | Notes |
|---|---|---|
| I. Pure Static Simplicity | ✅ PASS | Pure HTML5+CSS3. The one JS script (Vercel Web Analytics) is the explicitly permitted cookieless-analytics exception added in v1.2.0. No frameworks, no other JS. |
| II. Semantic & Accessible HTML | ✅ PASS | Semantic sections, one `<h1>`/page, keyboard-accessible, alt text on all images, reduced-motion support, contrast verification — all required by spec (FR-019–FR-024). |
| III. Mobile-First Responsive CSS | ✅ PASS | Reuses existing single `styles.css` (variables→reset→layout→components→utilities), mobile-first `min-width` queries, CSS Grid/flexbox. Rounded corners now permitted (v1.2.0). |
| IV. Zero-Dependency Architecture | ✅ PASS | No `package.json`/build. Analytics added via static `<script src="/_vercel/insights/script.js">`, not the npm package (which would need a bundler). New images live under `/assets/` per convention. |
| V. Deployment Readiness | ✅ PASS | Repo root stays deploy dir; every commit deployable; no env vars/secrets; works from any static server. Web Analytics enabled in Vercel dashboard. |

**Result**: PASS — no violations. Complexity Tracking table not required.

## Project Structure

### Documentation (this feature)

```text
specs/002-stream-reader-page/
├── plan.md              # This file
├── research.md          # Phase 0 output
├── data-model.md        # Phase 1 output
├── quickstart.md        # Phase 1 output
├── contracts/
│   └── page-structure.md  # Phase 1 output (UI/structure contract)
├── checklists/
│   └── requirements.md  # from /speckit.specify
└── tasks.md             # /speckit.tasks output (NOT created here)
```

### Source Code (repository root)

```text
index.html          # EDIT — Stream Reader block replaces Coming Soon; remove inline
                     #        contact section; header/footer refresh; head meta
streamreader.html   # NEW  — dedicated product page (6 sections per FR-004)
contact.html        # EDIT — header/footer refresh; reader/educator/org welcome copy
privacy.html        # EDIT — header/footer refresh ONLY (content deferred, do not rewrite)
styles.css          # EDIT — repurpose .coming-soon; Stream Reader page styles;
                     #        app-blue secondary accent; reduced-motion GIF rule
assets/             # NEW  — favicon, OG image(s), and assets/streamreader/ images
                     #        (placeholders acceptable until real assets supplied)
```

**Structure Decision**: Multi-file static site, matching the repo's existing real layout (`index.html` + `contact.html` + `privacy.html` already share `styles.css`). The spec/CLAUDE.md previously described a "single-page" site, but the working tree is already multi-file; the plan follows the real structure. `streamreader.html` is added as a flat top-level file (no subdirectory), consistent with the other pages. The duplicate embedded contact section in `index.html` is removed since `contact.html` is canonical (per clarification).

## Deviations from Spec Assumptions (resolved during planning)

- **Spec/CLAUDE.md said "single-page"; repo is actually multi-file.** Plan follows the real multi-file structure. CLAUDE.md "Active Technologies" updated to reflect this.
- **`index.html` had a duplicate embedded contact section** alongside the standalone `contact.html`. Per clarification, the embedded section is removed; `contact.html` is canonical.
- **Privacy page content rewrite is deferred** (user direction). This feature only refreshes `privacy.html`'s shared header/footer and wires the footer + Stream Reader privacy callout to link to it. The existing privacy copy (which states the app collects nothing) is NOT rewritten now; the website-analytics disclosure is a follow-up. FR-017's full app-vs-website separation is therefore partially deferred — tracked below.

## Outstanding / Deferred

| Item | Status | Rationale |
|---|---|---|
| FR-017 website-analytics privacy disclosure | Deferred | User deferred privacy.html content rewrite; only linking is wired this build. Revisit before/after launch. |
| Real image assets (icon, GIF, screenshots, badge, OG, favicon) | Placeholder-first | Per asset-gating clarification — ship labeled placeholders, swap real assets via follow-up commit. |
| App-blue secondary accent hex | Decide in implementation | Derived from the actual app icon/screenshots; contrast-checked when chosen. |

## Complexity Tracking

No constitution violations — table intentionally omitted.
