# Research: Moon Publishing Media Company Website

**Feature Branch**: `001-company-website` | **Date**: 2026-02-19

This document consolidates research findings for all technical decisions in the implementation plan. No items required external clarification — the spec and constitution provided sufficient constraints.

---

## 1. Inline SVG Logo (Crescent Moon + Wordmark)

### 1.1 Crescent Moon Shape Construction

**Decision**: Use cubic Bézier curves (`<path>` with `C`/`S` commands) to draw the crescent moon shape.

**Rationale**: Bézier curves provide precise control over curvature, scale infinitely without quality loss, and produce clean, minimal SVG markup. A crescent can be constructed with 2–4 cubic curves forming the complete arc.

**Alternatives Considered**:
- Overlapping `<circle>` elements with clip-path: More complex markup, less control over shape
- Icon library import: Adds external dependency (violates Constitution IV)
- Raster image: Loses scalability, increases file size

### 1.2 SVG Accessibility

**Decision**: Use `<svg role="img" aria-labelledby="logo-title">` with nested `<title>` and `<desc>` elements.

**Rationale**: This is the most reliably tested pattern across screen readers (NVDA, JAWS, VoiceOver). `<title>` provides the short label; `<desc>` provides context. `aria-labelledby` explicitly links the SVG to its title. When the SVG is inside an `<a>` tag (clickable logo), `aria-label` on the link provides navigation context.

**Alternatives Considered**:
- `aria-label` alone on SVG: Less reliable across browsers; violates first rule of ARIA (use native HTML when available)
- No accessibility attributes: Non-compliant with WCAG
- External `<img src="logo.svg" alt="...">`: Loses inline customization; violates Constitution IV (inline SVG required)

### 1.3 Icon + Wordmark Layout

**Decision**: Side-by-side layout using `<g>` groups — icon on left, wordmark text on right.

**Rationale**: Most recognizable logo format. Clear visual hierarchy. Scales well across responsive breakpoints. Use `<text>` element referencing Google Fonts loaded in CSS (`font-family="Cormorant Garamond, serif"`).

**Alternatives Considered**:
- Stacked/vertical (icon above text): Less common for header logos
- Text converted to `<path>` outlines: Better portability but loses font consistency with page text
- Icon-only on mobile: Possible enhancement but adds complexity; defer to implementation

### 1.4 Responsive Logo Sizing

**Decision**: Use CSS-based sizing with `max-width` on the SVG, controlled via media queries. No `width`/`height` attributes on the SVG element — let `viewBox` + CSS handle scaling.

**Rationale**: `viewBox` establishes the internal coordinate system. CSS `max-width` + `height: auto` preserves aspect ratio while allowing responsive scaling. Logo should remain clear at minimum 80px width.

**Sizing targets**:
- Mobile (375px–640px): `max-width: ~120px`
- Tablet (641px–1024px): `max-width: ~140px`
- Desktop (1025px+): `max-width: ~160–180px`

---

## 2. CSS Architecture

### 2.1 Design Tokens (Custom Properties)

**Decision**: Use a two-layer token system in a single `:root` block — primitive values and semantic aliases.

**Rationale**: For a two-page site, two layers (primitive + semantic) provide enough structure without over-engineering. Semantic tokens make design intent clear. Single `:root` block keeps everything discoverable.

**Token inventory**:
```
Colors:    --color-bg, --color-text, --color-accent, --color-text-muted
Fonts:     --font-heading, --font-body
Sizes:     --font-size-base, --font-size-sm, --font-size-lg, --font-size-xl, --font-size-2xl
Spacing:   --spacing-unit, --spacing-section, --spacing-page-margin
Layout:    --max-width (content container)
```

**Alternatives Considered**:
- Three-layer hierarchy (primitive, semantic, component): Over-engineered for 2 pages
- No tokens (hardcoded values): Inconsistent; harder to maintain
- Framework tokens (Tailwind, etc.): Violates Constitution IV

### 2.2 CSS Reset

**Decision**: Custom lightweight reset (~10–15 lines) at the top of `styles.css`.

**Rationale**: Modern browsers (2026) have good defaults. A minimal reset covering box-sizing, margin/padding removal, font smoothing, and media element constraints addresses 90% of cross-browser issues without bloat.

**Reset covers**:
- `* { box-sizing: border-box; margin: 0; padding: 0; }`
- `body { line-height: 1.5; -webkit-font-smoothing: antialiased; }`
- `img, svg { display: block; max-width: 100%; }`

**Alternatives Considered**:
- normalize.css: 400+ lines, unnecessary for two pages
- Josh Comeau's extended reset: Good but includes features for complex apps
- No reset: Inconsistent spacing across browsers

### 2.3 Layout Strategy

**Decision**: Flexbox for all layouts. No CSS Grid needed.

**Rationale**: The site has simple layouts — header (logo left, nav right), stacked content sections, centered footer. Flexbox handles all of these cleanly. Grid adds complexity without benefit for this scope. Constitution III prefers simplicity over cleverness.

**Key patterns**:
- Header: `display: flex; justify-content: space-between; align-items: center;`
- Content sections: `flex-direction: column` (mobile) → adjustments at breakpoints
- Footer: `display: flex; flex-direction: column; align-items: center;`

**Alternatives Considered**:
- Grid for page structure + Flexbox for components: More semantic but adds complexity
- Grid for everything: Overkill for single-column content flow

### 2.4 Breakpoint Strategy

**Decision**: Three breakpoints using mobile-first `min-width` media queries:
1. **Base** (375px+): No media query — default mobile styles
2. **Tablet** (768px+): `@media (min-width: 768px)`
3. **Desktop** (1200px+): `@media (min-width: 1200px)`

Content constrained with `max-width` to prevent stretching on ultra-wide (2560px+) screens.

**Rationale**: 375px covers ~99% of mobile devices. 768px is standard tablet. 1200px is traditional desktop. A `max-width` on the content container (e.g., 1140px) handles ultra-wide without a 4th breakpoint.

**Alternatives Considered**:
- Device-specific breakpoints (6+): Unmaintainable
- `max-width` (desktop-first) queries: Leads to CSS overrides; not mobile-first
- Dedicated 2560px breakpoint: Only needed if ultra-wide requires distinct layout, which it doesn't

---

## 3. Typography

### 3.1 Google Fonts Loading

**Decision**: Use `preconnect` hints + a single combined `<link>` tag with `display=swap`.

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@400;600;700&family=Inter:wght@400;500&display=swap" rel="stylesheet">
```

**Rationale**: `preconnect` reduces latency ~100ms by establishing early connections. Single `<link>` combining both fonts = one HTTP request. `display=swap` shows fallback fonts immediately, preventing invisible text (FOIT). Load only weights actually used (3 for Cormorant, 2 for Inter) to reduce payload by ~60–75%.

**Weight selection**:
- Cormorant Garamond: 400 (body of headings), 600 (emphasis), 700 (hero heading)
- Inter: 400 (body text), 500 (nav links, labels)

**Alternatives Considered**:
- `@import` in CSS: Slower; blocks rendering
- Self-hosted fonts: Requires manual updates; adds server config
- All weights (400–900): Adds 300–400kb unnecessarily
- `display=block`: Causes Flash of Invisible Text; poor UX

### 3.2 Typography Scale

**Decision**: 1.25x modular scale with `clamp()` for fluid sizing between breakpoints.

| Element | Size (fluid) | Line-Height | Weight |
|---------|-------------|-------------|--------|
| h1 | `clamp(2rem, 4vw, 3.125rem)` | 1.2 | 700 |
| h2 | `clamp(1.6rem, 3vw, 2.5rem)` | 1.3 | 600 |
| h3 | `clamp(1.28rem, 2.5vw, 2rem)` | 1.3 | 600 |
| body | `clamp(1rem, 1.5vw, 1.25rem)` | 1.6 | 400 |
| small | `clamp(0.875rem, 1vw, 1rem)` | 1.5 | 400 |

**Rationale**: 1.25x multiplier creates clear hierarchy without jarring jumps. `clamp()` reduces media query count — font sizes scale fluidly. Tight line-height on headings (1.2) feels elegant; generous line-height on body (1.6) meets WCAG readability. Cormorant is high-contrast serif — regular weight (400) works for most headings; reserve 600–700 for emphasis.

**Alternatives Considered**:
- Fixed pixel sizes at each breakpoint: More media queries, less fluid
- 1.5x modular scale: Too aggressive; h1 becomes overwhelming
- Single font weight throughout: Reduces visual hierarchy

---

## 4. Contact Page: Mailto Link

### 4.1 HTML Markup

**Decision**: Use `<a href="mailto:info@moonpublishingmedia.com">` as a standalone element, not embedded in a paragraph. Wrap in semantic HTML for prominence.

**Rationale**: Standalone display makes the email visually prominent (FR-008). The actual email address as link text provides maximum clarity. Screen readers announce it correctly. Meets WCAG requirement for descriptive link text.

**Alternatives Considered**:
- `<a>` within `<p>`: Less prominent; suggests email is incidental
- `<div>` with `role="link"`: Violates semantic HTML principle (Constitution II)

### 4.2 Email Obfuscation

**Decision**: Use plain `mailto:` link without obfuscation.

**Rationale**: The email is a business contact address intended for public inquiries. Server-side spam filtering handles automated spam effectively. Obfuscation adds friction and requires JavaScript. Mobile-first consideration: plain mailto has perfect native behavior on iOS/Android.

**Alternatives Considered**:
- JavaScript-based obfuscation: Adds JS dependency; Constitution I allows minimal inline JS but plain mailto is simpler
- HTML entity encoding: Ineffective against modern bots
- Contact form: Requires backend processing; violates static-site constraint
- Text substitution ("info [at] ...": Poor UX, fails accessibility

### 4.3 Styling for Prominence

**Decision**: Style the mailto link as a button-like CTA element using CSS — background color, generous padding, clear hover/focus states. Minimum 44px × 44px touch target for mobile accessibility.

**Rationale**: Button-like appearance signals interactivity without JavaScript. 44px minimum touch target meets WCAG mobile accessibility standards. Use `--color-accent` (#C4A0A0) for background. No rounded corners per Constitution.

### 4.4 Mobile & Fallback Behavior

**Decision**: No custom fallback needed. Operating systems handle mailto natively.

**Rationale**: iOS opens Mail (or prompts if no account configured). Android prompts email app selection. No JavaScript can reliably detect email client availability. The OS provides appropriate error messaging when no client is configured. This is explicitly called out as out-of-scope in the feature spec edge cases.

---

## Summary of All Decisions

| Area | Decision | Constitution Alignment |
|------|----------|----------------------|
| SVG Logo | Inline `<path>` with Bézier curves, `<title>`/`<desc>` for a11y | II (Semantic HTML), IV (Inline SVG) |
| CSS Tokens | Two-layer `:root` properties (primitive + semantic) | III (CSS custom properties) |
| CSS Reset | Custom 10–15 line reset | III (Single styles.css), IV (Zero deps) |
| Layout | Flexbox only, mobile-first column → row | III (Flexbox preferred) |
| Breakpoints | 3 breakpoints: base, 768px, 1200px (min-width) | III (Mobile-first, min-width) |
| Fonts | Google Fonts via `<link>` with preconnect + display=swap | IV (Only external resource) |
| Typography | 1.25x modular scale with `clamp()` | III (CSS custom properties) |
| Mailto | Plain `<a href="mailto:">`, no obfuscation, button-style CSS | I (Zero JS), II (Semantic HTML) |
