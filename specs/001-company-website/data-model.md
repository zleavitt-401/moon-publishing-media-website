# Data Model: Moon Publishing Media Company Website

**Feature Branch**: `001-company-website` | **Date**: 2026-02-19

This is a pure static HTML/CSS site with no database, API, or dynamic data. The "data model" describes the content entities, their structure, and relationships as they exist in HTML markup.

---

## Entities

### Page

The top-level entity. Each page is an independent HTML file sharing common structure.

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| title | `<title>` text | Yes | "Moon Publishing Media" (home) or "Contact — Moon Publishing Media" |
| meta_description | `<meta>` content | Yes | SEO description, unique per page |
| header | Header component | Yes | Identical across all pages |
| main | Main content | Yes | Unique per page |
| footer | Footer component | Yes | Identical across all pages |

**Instances**: `index.html` (Homepage), `contact.html` (Contact page)

**Validation**: Every page MUST have exactly one `<header>`, one `<main>`, one `<footer>`. Single `<h1>` per page.

---

### Header (shared component — copy-pasted across pages)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| logo | Inline SVG | Yes | Crescent moon + "Moon Publishing Media" wordmark |
| logo_link | `<a href="/">` | Yes | Always links to homepage |
| nav | `<nav>` | Yes | Contains "Contact" link |

**Validation**: Logo MUST be an `<a>` wrapping the SVG. Nav MUST contain at least the Contact link. Header markup MUST be identical in both HTML files.

---

### Footer (shared component — copy-pasted across pages)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| copyright | `<p>` text | Yes | "© 2026 Moon Publishing Media. All rights reserved." |

**Validation**: Footer markup MUST be identical in both HTML files.

---

### Hero Section (Homepage only)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| headline | `<h1>` | Yes | "Words that move you." |
| subheadline | `<p>` | Yes | Describes MPM's focus on self-care and wellness content |

**Validation**: `<h1>` used only here on the homepage. Subheadline MUST NOT mention any specific app or product name.

---

### About Section (Homepage only)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| heading | `<h2>` | Yes | "Who We Are" |
| description | `<p>` (one or more) | Yes | Company description — independent publisher of wellness/self-care content |

---

### Coming Soon Section (Homepage only)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| heading | `<h2>` | Yes | "Something New Is Coming" |
| description | `<p>` | Yes | Vague teaser about a digital product in development |
| status_label | Inline text | Yes | "Currently in development" |

**Validation**: MUST NOT contain app name, screenshots, or feature lists (App Teaser Policy per CLAUDE.md).

---

### Contact Content (Contact page only)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| heading | `<h1>` | Yes | "Say Hello" |
| intro_copy | `<p>` | Yes | Warm introductory text inviting contact |
| email_link | `<a href="mailto:...">` | Yes | info@moonpublishingmedia.com — displayed as standalone prominent element |

**Validation**: Email MUST be a clickable `mailto:` link. MUST be displayed as a standalone element, not inline within a paragraph (FR-008).

---

### Logo (SVG — embedded inline in Header)

| Field | Type | Required | Notes |
|-------|------|----------|-------|
| icon | SVG `<path>` | Yes | Crescent moon shape via Bézier curves |
| wordmark | SVG `<text>` | Yes | "Moon Publishing Media" in Cormorant Garamond |
| title | SVG `<title>` | Yes | Accessibility: "Moon Publishing Media" |
| description | SVG `<desc>` | Yes | Accessibility: describes logo content |

**Validation**: MUST use `role="img"` and `aria-labelledby` pointing to `<title>` ID. MUST remain legible at 80px minimum width.

---

## Entity Relationships

```
Page (index.html)
├── Header (shared)
│   ├── Logo (inline SVG)
│   └── Nav → links to contact.html
├── Main
│   ├── Hero Section
│   ├── About Section
│   └── Coming Soon Section
└── Footer (shared)

Page (contact.html)
├── Header (shared)
│   ├── Logo → links to index.html
│   └── Nav → "Contact" (current page)
├── Main
│   └── Contact Content
│       └── Email Link (mailto:info@moonpublishingmedia.com)
└── Footer (shared)
```

---

## State Transitions

N/A — This is a static site with no dynamic state. Navigation between pages is handled by standard `<a>` links (full page loads). The only interactive element is the mailto link, which delegates to the operating system's mail client handler.

---

## Design Tokens (CSS Custom Properties)

These are the "schema" for visual consistency across all entities:

| Token | Value | Used By |
|-------|-------|---------|
| `--color-bg` | `#FAF9F6` | Page background |
| `--color-text` | `#1C1C1C` | All text |
| `--color-accent` | `#C4A0A0` | Links, CTA, decorative elements |
| `--color-text-muted` | `#6B6B6B` | Secondary text (copyright, labels) |
| `--font-heading` | `'Cormorant Garamond', serif` | h1, h2, h3, logo wordmark |
| `--font-body` | `'Inter', sans-serif` | Body text, nav, footer |
| `--max-width` | `1140px` | Content container |
