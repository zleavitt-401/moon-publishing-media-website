# Page Structure Contracts

**Feature Branch**: `001-company-website` | **Date**: 2026-02-19

These contracts define the required HTML structure for each page. Since this is a pure static site with no API, these contracts serve as the equivalent of endpoint/schema definitions — they specify what each "resource" (HTML page) must deliver.

---

## Contract: Homepage (`index.html`)

### Document Head

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Moon Publishing Media</title>
  <meta name="description" content="[SEO description for homepage]">
  <!-- Google Fonts preconnect + link -->
  <link rel="stylesheet" href="styles.css">
</head>
```

**Requirements**:
- `lang="en"` on `<html>`
- Viewport meta for responsive design
- Google Fonts loaded via `<link>` with `preconnect` and `display=swap`
- Single stylesheet reference to `styles.css`

### Document Body Structure

```
<body>
  <header>              ← SHARED (identical in both files)
    <a href="/">
      <svg>             ← Inline SVG logo (crescent moon + wordmark)
    </a>
    <nav>
      <a href="contact.html">Contact</a>
    </nav>
  </header>

  <main>
    <section>           ← Hero: h1 + subheadline
    <section>           ← About: h2 "Who We Are" + description
    <section>           ← Coming Soon: h2 + teaser + status label
  </main>

  <footer>              ← SHARED (identical in both files)
    <p>© 2026 Moon Publishing Media. All rights reserved.</p>
  </footer>
</body>
```

**Section Requirements**:

| Section | Required Elements | Constraints |
|---------|-------------------|-------------|
| Hero | `<h1>` "Words that move you.", `<p>` subheadline | Only `<h1>` on this page |
| About | `<h2>` "Who We Are", `<p>` description(s) | Must describe publisher identity |
| Coming Soon | `<h2>` "Something New Is Coming", `<p>` teaser, status text | NO app name, NO screenshots, NO feature list |

---

## Contract: Contact Page (`contact.html`)

### Document Head

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact — Moon Publishing Media</title>
  <meta name="description" content="[SEO description for contact page]">
  <!-- Google Fonts preconnect + link (identical to index.html) -->
  <link rel="stylesheet" href="styles.css">
</head>
```

### Document Body Structure

```
<body>
  <header>              ← SHARED (identical to index.html)
    <a href="/">
      <svg>             ← Inline SVG logo
    </a>
    <nav>
      <a href="contact.html">Contact</a>
    </nav>
  </header>

  <main>
    <section>           ← Contact content
      <h1>Say Hello</h1>
      <p>Introductory copy</p>
      <a href="mailto:info@moonpublishingmedia.com">
        info@moonpublishingmedia.com
      </a>
    </section>
  </main>

  <footer>              ← SHARED (identical to index.html)
    <p>© 2026 Moon Publishing Media. All rights reserved.</p>
  </footer>
</body>
```

**Requirements**:
- Email link MUST be a standalone `<a>` element, NOT inline within a `<p>`
- Email link MUST use `href="mailto:info@moonpublishingmedia.com"`
- `<h1>` is "Say Hello"

---

## Contract: Shared Components

### Header (identical in both files)

```html
<header class="site-header">
  <a href="/" class="logo-link" aria-label="Moon Publishing Media home">
    <svg role="img" aria-labelledby="logo-title" viewBox="0 0 [W] [H]" class="logo">
      <title id="logo-title">Moon Publishing Media</title>
      <desc id="logo-desc">Crescent moon icon with company wordmark</desc>
      <!-- Crescent moon path + wordmark text -->
    </svg>
  </a>
  <nav>
    <a href="contact.html">Contact</a>
  </nav>
</header>
```

**Invariants**:
- Markup byte-for-byte identical in both HTML files
- Logo always links to `/` (homepage)
- Nav always contains Contact link
- SVG includes `role="img"`, `aria-labelledby`, `<title>`, `<desc>`

### Footer (identical in both files)

```html
<footer class="site-footer">
  <p>© 2026 Moon Publishing Media. All rights reserved.</p>
</footer>
```

**Invariants**:
- Markup byte-for-byte identical in both HTML files
- Copyright year: 2026

---

## Contract: Stylesheet (`styles.css`)

### Section Order

```css
/* 1. CSS Custom Properties */
:root { ... }

/* 2. Reset */
*, *::before, *::after { ... }

/* 3. Base / Typography */
body { ... }
h1, h2, h3 { ... }
a { ... }

/* 4. Layout */
.site-header { ... }
.site-footer { ... }
main { ... }

/* 5. Components */
.hero { ... }
.about { ... }
.coming-soon { ... }
.contact { ... }
.logo { ... }
.email-link { ... }

/* 6. Utilities (if any) */

/* 7. Media Queries (mobile-first, min-width) */
@media (min-width: 768px) { ... }
@media (min-width: 1200px) { ... }
```

**Invariants**:
- Single file, no imports
- CSS custom properties defined first in `:root`
- Mobile-first: base styles for 375px, `min-width` breakpoints for larger
- Zero rounded corners (`border-radius: 0` or omitted entirely)
- Flexbox for layout (no Grid required)
