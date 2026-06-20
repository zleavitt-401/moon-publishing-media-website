# Research: Stream Reader Product Page + Website Professionalization

## Decision: Multi-file static HTML, following existing pattern

**Rationale**: The repo already contains separate `index.html`, `contact.html`, and `privacy.html` files sharing one `styles.css` — not a true single-page site despite CLAUDE.md's description. `streamreader.html` will follow this same established pattern: a new top-level `.html` file, same shared header/footer markup, same `styles.css`.

**Alternatives considered**: Consolidating everything into one `index.html` with anchor sections — rejected because it contradicts the existing multi-file structure already in production and would require a much larger, riskier rewrite of files outside this feature's scope.

## Decision: Remove index.html's embedded `#contact` section

**Rationale**: `contact.html` already exists as the canonical contact page. `index.html`'s inline `.contact` section duplicates the same content with a different visual treatment (horizontal bar vs. prose page), which is redundant and creates two sources of truth. Per user direction, the inline section is removed from `index.html`'s grid, and the homepage's "Say Hello" entry point becomes the "Contact" nav link only.

**Alternatives considered**: Keeping both — rejected by user as redundant.

## Decision: Stream Reader block replaces `.coming-soon` in place

**Rationale**: Per clarification, the homepage's existing 2-column CSS Grid (hero left; about + coming-soon stacked right) is preserved. The `.coming-soon` section's content is replaced with named Stream Reader copy + link; the section's CSS class can be renamed (e.g., `.stream-reader-teaser`) but occupies the same grid area.

**Alternatives considered**: Promoting Stream Reader to a full-width section — rejected by clarification (layout restructuring out of scope).

## Decision: New page `streamreader.html`, not nested under a subdirectory

**Rationale**: Matches flat, kebab-case file convention already established (`contact.html`, `privacy.html` at repo root). No build step or routing exists, so a flat structure is simplest.

**Alternatives considered**: `/stream-reader/index.html` — rejected, adds directory nesting with no benefit on a static host with no routing layer.

## Decision: `assets/` folder for new images, GIF, and OG image

**Rationale**: Constitution's File & Asset Conventions section already names `/assets/` as the convention for images/icons; the folder doesn't exist yet because no non-SVG, non-inline asset has been needed until now. Subfolders: `assets/streamreader/` for the four product images (icon, GIF, two screenshots) plus `assets/og-image.png` and `assets/favicon.ico`/`favicon.svg` at the assets root, since those are site-wide rather than Stream-Reader-specific.

**Alternatives considered**: Flat `assets/` with no subfolder — acceptable too, but a `streamreader/` subfolder keeps product-specific assets grouped as more are likely added later (e.g., when ebooks ship).

## Decision: Official Apple App Store badge — static SVG/PNG, sourced unmodified

**Rationale**: Apple provides official "Download on the App Store" badge artwork (SVG/PNG, multiple locales) for linking to App Store listings. Constitution and spec both require official, unmodified artwork — this is a static `<img>` wrapped in an `<a>` to the App Store URL, no JS needed. The actual badge asset file must be downloaded from Apple's marketing resources and placed in `assets/` (cannot be fetched from this environment); implementation will use a placeholder-labeled badge image until the real file is supplied, per the asset-gating clarification.

**Alternatives considered**: Recreating the badge as inline SVG/CSS — rejected; Apple's brand guidelines require using their unmodified official artwork, not a recreation.

## Decision: Vercel Web Analytics via static script tag (no npm package)

**Rationale**: Since this project has no build step, no `package.json`, and no bundler, Vercel Web Analytics is added via Vercel's framework-agnostic snippet: a single `<script defer src="/_vercel/insights/script.js"></script>` tag (Vercel injects/serves this automatically once Web Analytics is enabled on the linked Vercel project — no client-side install needed for plain static sites). This satisfies the constitution's "single cookieless analytics script" exception (Principle I) without adding any dependency, build step, or framework.

**Alternatives considered**: The `@vercel/analytics` npm package's `inject()` call — rejected, requires a bundler/build step which violates the zero-build-step constraint (Constitution IV).

## Decision: Open Graph image and favicon are new static assets, declared via `<meta>`/`<link>` tags only

**Rationale**: Standard static-site SEO/sharing pattern — `<link rel="icon">` for favicon, `og:title`/`og:description`/`og:image`/`og:url` and matching `twitter:card` meta tags in `<head>`. No JS required. Same pattern applies to all four pages (each with page-specific title/description/og:image where relevant) per FR-025/FR-026.

**Alternatives considered**: Single shared OG image across all pages — rejected for the Stream Reader page specifically, since FR-025 requires a unique title/description, and a distinct OG image (app icon or screenshot) makes cold-email link previews recognizable as the app, not the generic site.

## Decision: prefers-reduced-motion handled via CSS-driven `<picture>`/`<img>` swap or animated-GIF-as-`<img>` plus a small inline CSS media query

**Rationale**: GIFs autoplay natively in `<img>` tags and cannot be paused via CSS alone. The simplest zero-JS-by-default approach: serve the GIF via `<img>` for users without the reduced-motion preference, and use a CSS `@media (prefers-reduced-motion: reduce)` rule to swap visibility to a static `<img>` of the same source's first frame (extracted at asset-prep time as a separate static file, e.g. `streaming-demo-static.png`, generated once from the GIF rather than hand-shot). This keeps the page fully CSS-driven with no JS for motion handling.

**Clarification note**: The clarification answer said the fallback is "auto-derived from the GIF's first frame" — in a zero-JS static site, this still requires producing one static image file from the GIF during asset preparation (a one-time export step, not a runtime/JS behavior). This is documented in quickstart.md asset prep notes.

**Alternatives considered**: A JS-based pause/play control — rejected; adds a second JS script beyond the one approved analytics exception, violating Constitution Principle I.

## Decision: Color contrast — verify dusty rose (#C4A0A0) usages against backgrounds

**Rationale**: Constitution and spec (FR-021) require accessible contrast. Existing `--color-accent: #C4A0A0` is already used as link/CTA color against `--color-bg: #E8EDF2`/`--color-text: #1C1C1C`. The existing site already uses accent-on-bg button styling (`.email-link`) successfully passing review previously; the new app-blue secondary accent must be checked the same way once a specific hex value is chosen during implementation (no fixed brand blue exists yet — Stream Reader's app icon/screenshots will supply the reference blue).

**Alternatives considered**: N/A — this is a verification task carried into implementation/testing, not a design decision requiring research.
