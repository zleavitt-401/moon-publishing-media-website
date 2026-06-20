# UI Contract: Page Structure & Shared Components

This static site exposes no API. Its "contract" is the structural HTML and link
graph that every page MUST honor. Implementation and tests verify against this.

## Shared Header (identical on all four pages)

```html
<header class="site-header">
  <a href="/" class="logo-link" aria-label="Moon Publishing Media home">
    <svg aria-hidden="true" ...>…crescent…</svg>
    <span class="logo-wordmark">Moon Publishing Media</span>
  </a>
  <nav>
    <a href="streamreader.html">Stream Reader</a>
    <a href="contact.html">Contact</a>
  </nav>
</header>
```

**Contract**:
- Logo links to `/` (Homepage). [FR-002, FR-009-equivalent]
- Nav contains exactly two links: Stream Reader, Contact — in that order. [FR-002]
- No Privacy Statement link in the header. [Clarification]
- Byte-identical across `index.html`, `streamreader.html`, `contact.html`, `privacy.html`. [FR-002]

## Shared Footer (identical on all four pages)

```html
<footer class="site-footer">
  <p>&copy; 2026 Moon Publishing Media. All rights reserved.</p>
  <p class="footer-links">
    <a href="streamreader.html">Stream Reader</a>
    <a href="privacy.html">Privacy Policy</a>
  </p>
</footer>
```

**Contract**:
- Copyright notice present. [FR-003]
- Footer links: Stream Reader + Privacy Policy (Home reachable via logo). [FR-003]
- Byte-identical across all four pages. [FR-003]

## Link Graph (zero broken internal links — SC-003)

| From | Link | To |
|---|---|---|
| any header logo | `/` | `index.html` |
| any header nav | `streamreader.html` | Stream Reader page |
| any header nav | `contact.html` | Contact page |
| any footer | `streamreader.html` | Stream Reader page |
| any footer | `privacy.html` | Privacy page |
| Homepage Stream Reader block | `streamreader.html` | Stream Reader page |
| Stream Reader hero badge | App Store URL | external |
| Stream Reader hero browser link | `https://streamreader.app` | external |
| Stream Reader privacy callout | `privacy.html` | Privacy page |
| Stream Reader closing badge/link | App Store URL / streamreader.app | external |
| Contact email | `mailto:info@moonpublishingmedia.com` | mail client |

## Stream Reader Page — Section Order Contract (FR-004)

```html
<main>
  <section class="sr-hero">        <!-- 1: icon, name, tagline, badge, browser link -->
  <section class="sr-what">        <!-- 2: GIF + copy -->
  <section class="sr-features">    <!-- 3: Library + Customization screenshots -->
  <aside  class="sr-privacy">      <!-- 4: privacy callout → privacy.html -->
  <section class="sr-audience">    <!-- 5: who it's for -->
  <section class="sr-cta">         <!-- 6: closing badge + browser link -->
</main>
```

**Contract**:
- Sections appear in exactly this order. [FR-004]
- Exactly one `<h1>` (the app name in the hero). [FR-020]
- Each screenshot and the GIF has non-empty descriptive `alt`. [FR-019]
- Badge uses official unmodified Apple artwork, primary; browser link secondary. [FR-006, FR-007]
- Tagline text is exactly "One line. Your pace. Nothing in the way." [FR-005]

## Head Metadata Contract (per page)

```html
<title>…unique per page…</title>                 <!-- FR-025 -->
<meta name="description" content="…unique…">     <!-- FR-025 -->
<link rel="icon" href="assets/favicon.svg">      <!-- FR-026 -->
<meta property="og:title" content="…">           <!-- FR-026 -->
<meta property="og:description" content="…">
<meta property="og:image" content="…">
<meta property="og:url" content="…">
<meta name="twitter:card" content="summary_large_image">
```

## Analytics Contract (FR-018, Constitution I)

```html
<!-- exactly one analytics script, on every page, just before </body> -->
<script defer src="/_vercel/insights/script.js"></script>
```

**Contract**:
- Exactly one analytics script site-wide; no other tracking/analytics. [FR-018]
- Cookieless; no consent banner rendered. [FR-018, SC-010]

## Accessibility Contract

- One `<h1>` per page; logical `<h2>`/`<h3>` nesting. [FR-020]
- All interactive elements keyboard-focusable with visible `:focus-visible`. [FR-024]
- Text/background contrast meets WCAG AA, incl. dusty rose on off-white. [FR-021]
- `@media (prefers-reduced-motion: reduce)` swaps the GIF for its static frame. [FR-022]
- No console errors on any page. [SC-009]

## Responsive Contract

- No horizontal scroll, no overflow, 375px → 2560px+. [FR-030, SC-008]
- Images (screenshots, GIF, badge) scale without distortion. [Edge cases]
