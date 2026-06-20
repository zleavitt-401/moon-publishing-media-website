# Data Model: Stream Reader Product Page + Website Professionalization

This is a static site with no database, no forms that persist data, and no runtime data model. "Entities" below are content/structural entities expressed directly in HTML markup — documented here for consistency across the four pages, not as a database schema.

## Page

Represents one HTML document.

| Field | Description |
|---|---|
| `path` | Filename at repo root (e.g., `streamreader.html`) |
| `title` | Unique `<title>` text per page (FR-025) |
| `meta_description` | Unique `<meta name="description">` per page (FR-025) |
| `og_image` | Path to the page's Open Graph image (FR-026) |
| `h1` | Exactly one per page (FR-020) |
| `has_header` | Always true — identical shared header markup (FR-002) |
| `has_footer` | Always true — identical shared footer markup (FR-003) |

**Instances**: `index.html` (Homepage), `streamreader.html` (Stream Reader), `contact.html` (Contact), `privacy.html` (Privacy Statement — content unchanged this feature, only the shared header/footer markup is refreshed to match the other three pages and add the Stream Reader nav link).

## Shared Header

| Field | Description |
|---|---|
| `logo_link` | Links to `index.html` |
| `nav_links` | `[Stream Reader → streamreader.html, Contact → contact.html]` — no Privacy link (clarified) |

## Shared Footer

| Field | Description |
|---|---|
| `copyright_text` | "© 2026 Moon Publishing Media. All rights reserved." |
| `footer_links` | `[Stream Reader → streamreader.html, Privacy Policy → privacy.html]` (Home is already reachable via the logo, so it's not duplicated in the footer link list) |

## Stream Reader Block (Homepage)

Replaces the prior `.coming-soon` section content in the existing grid slot (right column, bottom — no layout change).

| Field | Description |
|---|---|
| `heading` | Names "Stream Reader" |
| `body_copy` | Short description of the app, self-care-publisher voice |
| `link` | → `streamreader.html` |
| `future_content_note` | Separate, intentionally vague sentence about future content (e.g. ebooks) — kept distinct from the named Stream Reader copy (FR-014) |

## Stream Reader Page Sections

In order, per FR-004:

1. **Hero**: app icon (`<img>`), app name, tagline ("One line. Your pace. Nothing in the way."), App Store badge (primary CTA, `<a><img></a>` to App Store URL), browser link (secondary CTA, `<a>` to streamreader.app)
2. **What It Does**: demo GIF (`<img>`, with `prefers-reduced-motion` static-frame swap via CSS) + 2–3 lines of copy
3. **Features**: Library screenshot + Customization screenshot, each with descriptive alt text
4. **Privacy Callout**: standalone block, links to `privacy.html`
5. **Who It's For**: a few inclusive, non-clinical lines
6. **Closing CTA**: App Store badge + browser link repeated

## App Asset

| Field | Description |
|---|---|
| `file` | Path under `assets/streamreader/` (or `assets/` for favicon/OG image) |
| `alt_text` | Required, descriptive (FR-019) |
| `placeholder_status` | "real" or "placeholder" — placeholders ship now per asset-gating clarification, swapped later |

**Instances**: app icon, demo GIF (+ derived static first-frame fallback image), Library screenshot, Customization screenshot, App Store badge (official Apple artwork), favicon, Open Graph image(s).

## Call to Action

| Field | Description |
|---|---|
| `type` | "primary" (App Store badge) or "secondary" (browser link) |
| `target_url` | `https://apps.apple.com/us/app/stream-reader/id6760571431` or `https://streamreader.app` |
| `appears_in` | Hero, Closing CTA |

## Contact Point

| Field | Description |
|---|---|
| `email` | `info@moonpublishingmedia.com` |
| `presentation` | `mailto:` link, standalone element (not inline in a paragraph) |
| `appears_in` | `contact.html` only (the duplicate homepage contact section is removed) |
