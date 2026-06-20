# Feature Specification: Stream Reader Product Page + Website Professionalization

**Feature Branch**: `feature/stream-reader-page`
**Created**: 2026-06-19
**Status**: Draft
**Input**: User description: "Stream Reader product page + website professionalization for Moon Publishing Media"

## Clarifications

### Session 2026-06-19

- Q: Should the Privacy Statement page get its own link in the shared header nav, or stay footer-only/link-only? → A: Footer-only — Privacy Statement is linked from the footer and the Stream Reader privacy callout, not from the header nav.
- Q: Should the homepage keep its existing 2-column editorial CSS Grid (Hero left; "Who We Are" + Stream Reader block stacked right), or is restructuring in scope? → A: Keep existing grid — the Stream Reader block replaces the "Coming Soon" content in its existing slot (right column, bottom); no layout redesign.
- Q: If real image assets aren't available at implementation time, should the page ship with placeholders or be blocked until assets arrive? → A: Ship with clearly labeled placeholders now; swap in real assets as a follow-up commit when available.
- Q: Should the prefers-reduced-motion fallback for the streaming demo GIF be a dedicated still image or auto-derived from the GIF's first frame? → A: Auto-derived from the GIF's first frame — no separate fallback asset required.
- Q: Should the Privacy Statement page use the exact same full header/footer shell as the other three pages? → A: Yes — identical header (logo, Stream Reader, Contact links) and footer as every other page.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Organization Contact Learns About Stream Reader via Cold Email (Priority: P1)

A staff member at an organization that supports people with reading and focus challenges receives a cold email from MPM. They click a link to the Stream Reader page, want to quickly understand what the app does and who it's for, and decide whether to download it or recommend it to the people they serve.

**Why this priority**: This is the entire business driver for the feature. Without a credible, dedicated page that names the app and clearly explains its value, the cold-email outreach has nowhere to send people, and MPM's enrollment-only placeholder actively undermines credibility.

**Independent Test**: Load the Stream Reader page directly (as if clicking a cold-email link with no prior context). Without any other page visited, a reader can identify what the app is, what it does, who it's for, and how to get it (App Store) or try it (browser) — all above or just below the fold.

**Acceptance Scenarios**:

1. **Given** a visitor lands on the Stream Reader page directly, **When** the page renders, **Then** they see the app name, icon, tagline, an official Apple App Store download badge, and a secondary "try it in your browser" link to streamreader.app — all visible without scrolling past the hero
2. **Given** a visitor scrolls past the hero, **When** they reach the "what it does" section, **Then** they see the streaming demo GIF and 2–3 lines of plain-language, non-clinical copy describing the reading experience
3. **Given** a visitor continues scrolling, **When** they reach the features section, **Then** they see the Library screenshot (save and resume) and the Customization screenshot (font, size, speed, optional word coloring)
4. **Given** a visitor reaches the privacy callout, **When** they read it, **Then** they see a clear, standalone statement that the app requires no account, collects no data, and works fully offline, with a link to the full privacy statement
5. **Given** a visitor reaches the "who it's for" section, **Then** they read a few inclusive, non-clinical lines describing the kinds of readers the app helps
6. **Given** a visitor reaches the bottom of the page, **Then** they see the App Store badge and browser link repeated as a closing call to action
7. **Given** a visitor clicks the App Store badge, **When** the click is registered, **Then** they are taken to https://apps.apple.com/us/app/stream-reader/id6760571431
8. **Given** a visitor clicks the "try it in your browser" link, **When** the click is registered, **Then** they are taken to https://streamreader.app

---

### User Story 2 - Direct Visitor Discovers Stream Reader via the Homepage (Priority: P1)

A visitor reaches moonpublishingmedia.com directly (not via the cold email) — for example, while researching MPM as a company. They first perceive MPM as a self-care/wellness publisher, then discover that MPM has a published app, Stream Reader, and can click through to learn more.

**Why this priority**: Equal priority to Story 1 because the homepage is the credibility anchor — Apple reviewers and any other validator land here first. It must no longer hide the app behind a vague teaser, since that undermines both the cold-email destination and the company's transparency.

**Independent Test**: Load the homepage in isolation. Confirm MPM's self-care publisher identity is still the first impression, and that a named, linked Stream Reader block (not a vague teaser) is present and leads to the new page.

**Acceptance Scenarios**:

1. **Given** a visitor loads the homepage, **When** the page renders, **Then** they see MPM's existing hero and "Who We Are" content describing it as an independent self-care/wellness publisher, unchanged in substance
2. **Given** a visitor scrolls to where the old "Coming Soon" teaser used to be, **When** the page renders, **Then** they see a named Stream Reader block (app name, a short description, and a link to the Stream Reader page) instead of a vague, unnamed teaser
3. **Given** a visitor reads the Stream Reader block, **When** they look for forward-looking publisher content (e.g., future ebooks), **Then** any such language remains intentionally soft and unspecific, separate from the named, concrete Stream Reader content
4. **Given** a visitor clicks through the Stream Reader block, **When** the click is registered, **Then** they are taken to the dedicated Stream Reader page

---

### User Story 3 - Any Visitor Reaches Contact to Inquire (Priority: P2)

A reader, educator, or representative of an organization wants to ask a question, give feedback, or start a conversation about partnership/distribution. They navigate to the Contact page from anywhere on the site and find language that welcomes their specific kind of inquiry, plus easy access to related pages via footer links.

**Why this priority**: Important for completing the outreach loop (cold email → product page → contact), but secondary to the two pages that do the primary informing and converting.

**Independent Test**: Load the Contact page directly. Confirm the welcome copy explicitly addresses readers, educators, and organizations (not just generic "say hello" copy), and that footer links to other key pages are present and functional.

**Acceptance Scenarios**:

1. **Given** a visitor loads the Contact page, **When** the page renders, **Then** they see welcome copy that explicitly mentions readers, educators, and organizations as types of people who might reach out
2. **Given** a visitor is on the Contact page, **When** they look at the footer, **Then** they see links to the homepage, the Stream Reader page, and the privacy statement
3. **Given** a visitor clicks the email address, **When** the click is registered, **Then** their default mail client opens with info@moonpublishingmedia.com pre-filled

---

### User Story 4 - Consistent Navigation Across All Pages (Priority: P2)

A visitor moves between the Homepage, Stream Reader page, and Contact page. The shared header (including a new "Stream Reader" nav link) and footer look and behave identically everywhere.

**Why this priority**: Navigation consistency is a usability and credibility concern that touches all three pages, but is a supporting concern rather than a standalone value driver.

**Independent Test**: Visit each of the three pages and confirm the header (with logo, Stream Reader link, Contact link) and footer (with copyright and the same set of links) are visually and functionally identical across all of them.

**Acceptance Scenarios**:

1. **Given** a visitor is on any of the three pages, **When** they view the header, **Then** they see the logo, a "Stream Reader" nav link, and a "Contact" nav link (no Privacy Statement link in the header), identical across all pages
2. **Given** a visitor clicks "Stream Reader" in the header from any page, **When** the click is registered, **Then** they are taken to the Stream Reader page
3. **Given** a visitor clicks the logo from any page, **When** the click is registered, **Then** they are taken to the homepage
4. **Given** a visitor compares the footer across all three pages, **When** they look at content and links, **Then** the footer is identical everywhere

---

### User Story 5 - Visitor Verifies What Data Is Collected (Priority: P3)

A privacy-conscious visitor (or an organization's IT/compliance reviewer) wants to understand exactly what data the app and the website collect before recommending Stream Reader to the people they serve. They navigate to the privacy statement and find a clear, accurate distinction between the app (collects nothing) and the websites (cookie-free aggregate analytics only).

**Why this priority**: Important for institutional trust (the audience includes organizations with compliance obligations), but it's a supporting/reference page rather than a primary conversion path.

**Independent Test**: Load the privacy statement directly. Confirm it separately and unambiguously describes the iOS app's data practices (none, fully offline) and the websites' data practices (cookie-free, aggregate, no personal data).

**Acceptance Scenarios**:

1. **Given** a visitor loads the privacy statement, **When** they read the app section, **Then** they learn the iOS app collects no data, requires no account, and works fully offline
2. **Given** a visitor loads the privacy statement, **When** they read the website section, **Then** they learn the websites use cookie-free, aggregate analytics that collect no personal data and set no cookies
3. **Given** a visitor reaches the privacy callout on the Stream Reader page, **When** they click the link, **Then** they are taken to this privacy statement

---

### Edge Cases

- What happens if the streaming demo GIF fails to load? The "what it does" section MUST remain meaningful via its surrounding copy even if the image fails.
- What happens when a visitor has `prefers-reduced-motion` enabled? The streaming GIF MUST present a static fallback image or a pause control instead of forcing autoplay motion.
- What happens when a visitor pastes a Stream Reader page link into an email or chat client? The link preview MUST render a title, description, and Open Graph image rather than a blank or generic preview.
- What happens when a screen reader user navigates the Stream Reader page? Every screenshot and the GIF MUST have descriptive alt text, and heading order MUST be logical with exactly one `<h1>`.
- What happens when a visitor with low vision views the dusty-rose-on-off-white text? Contrast MUST meet accessibility standards for body and heading text.
- What happens when a visitor reaches the Stream Reader page on a very narrow (375px) or very wide (2560px+) viewport? All sections, including the screenshots and GIF, MUST remain readable and properly laid out without horizontal scrolling or distorted images.
- What happens when the App Store badge or browser link is reached via keyboard only? Both MUST be focusable and activatable via keyboard, with a visible focus state.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The site MUST consist of exactly three primary navigable pages — Homepage, Stream Reader, and Contact — plus a Privacy Statement page reachable via footer and in-page links; the Privacy Statement page MUST use the identical shared header and footer as the three primary pages (see FR-002, FR-003)
- **FR-002**: All pages MUST share an identical header containing the company logo (linking to the homepage), a "Stream Reader" navigation link, and a "Contact" navigation link; the header MUST NOT include a separate Privacy Statement nav link
- **FR-003**: All pages MUST share an identical footer containing the copyright notice and links to the homepage, the Stream Reader page, and the privacy statement
- **FR-004**: The Stream Reader page MUST present, in order: a hero (app icon, app name, tagline, App Store badge as primary CTA, browser link as secondary CTA), a "what it does" section (demo GIF + descriptive copy), a features section (Library and Customization screenshots), a privacy callout (linking to the privacy statement), a "who it's for" section, and a closing CTA repeating the App Store badge and browser link
- **FR-005**: The Stream Reader page hero MUST display the tagline "One line. Your pace. Nothing in the way."
- **FR-006**: The App Store badge on the Stream Reader page MUST link to https://apps.apple.com/us/app/stream-reader/id6760571431 and MUST use official, unmodified Apple App Store badge artwork
- **FR-007**: The "try it in your browser" link on the Stream Reader page MUST link to https://streamreader.app and MUST be presented as a secondary action relative to the App Store badge
- **FR-008**: The "what it does" section copy MUST describe the reading experience in focus-framed, non-clinical language (text moves as one line at a controllable pace; eases mind-wandering, losing one's place, and re-reading) without using clinical or diagnostic terminology
- **FR-009**: The features section MUST display the Library screenshot (illustrating save-and-resume) and the Customization screenshot (illustrating font, size, speed, and optional word-coloring controls)
- **FR-010**: The privacy callout on the Stream Reader page MUST state that the app is standalone, requires no account, collects no data, and works fully offline, and MUST link to the privacy statement
- **FR-011**: The "who it's for" section MUST use inclusive, non-clinical language describing the kinds of readers the app helps
- **FR-012**: The homepage MUST retain its existing hero and "Who We Are" content establishing MPM as an independent self-care/wellness publisher
- **FR-013**: The homepage MUST replace its prior unnamed "coming soon" teaser with a named Stream Reader block that identifies the app and links to the Stream Reader page, occupying the same position in the existing 2-column editorial grid (right column, bottom) without restructuring the homepage layout
- **FR-014**: The homepage MAY retain softly open, intentionally vague language about future content (e.g., ebooks), kept separate from the named Stream Reader block
- **FR-015**: The Contact page MUST include welcome copy that explicitly addresses readers, educators, and organizations as potential inquirers
- **FR-016**: The Contact page MUST continue to display the email address info@moonpublishingmedia.com as a clickable mailto link
- **FR-017**: The privacy statement MUST separately describe the iOS app's data practices (collects nothing, fully offline, no account required) and the websites' data practices (cookie-free, aggregate analytics, no personal data collected, no consent banner required)
- **FR-018**: The marketing site MUST include exactly one analytics script (cookie-free Vercel Web Analytics) and no other tracking or analytics scripts
- **FR-019**: Every screenshot and the demo GIF on the Stream Reader page MUST include descriptive alt text
- **FR-020**: Every page MUST have a logical heading order with exactly one `<h1>`
- **FR-021**: Text/background color combinations, including dusty rose on off-white, MUST meet accessible contrast standards
- **FR-022**: The streaming demo GIF MUST respect the visitor's `prefers-reduced-motion` setting by displaying the GIF's first frame as a static fallback (no separate fallback asset required) or providing a pause control
- **FR-023**: The demo GIF MUST be optimized for file size to avoid materially slowing page load
- **FR-024**: All interactive elements (nav links, CTAs, badge, browser link, email link, footer links) MUST be reachable and operable via keyboard, with a visible focus state
- **FR-025**: The Stream Reader page MUST have a unique page title and meta description distinct from the homepage and Contact page
- **FR-026**: The site MUST include a favicon and an Open Graph image so that links shared in emails or chat render a title, description, and image preview
- **FR-027**: Rounded corners are permitted as a deliberate design choice on any page, applied consistently within a given component
- **FR-028**: The Stream Reader page MAY use a secondary accent color (the app's blue) in addition to MPM's existing warm palette, used deliberately around app screenshots and related content
- **FR-029**: The site MUST remain a static site requiring no build step, server-side processing, or JavaScript framework, with the sole exception of the one approved analytics script
- **FR-030**: The site MUST be fully readable and properly laid out on viewports from 375px to 2560px+ width with no horizontal scrolling

### Key Entities

- **Page**: A single web document accessible via URL (Homepage, Stream Reader, Contact, or Privacy Statement). Each page has an identical header, a main content area, and an identical footer.
- **Stream Reader Block**: A homepage component naming the app, briefly describing it, and linking to the Stream Reader page — replaces the prior vague "coming soon" teaser.
- **App Asset**: An image or animation used to represent Stream Reader (app icon, demo GIF, Library screenshot, Customization screenshot), each requiring descriptive alt text.
- **Call to Action**: An App Store badge (primary) or browser link to streamreader.app (secondary), appearing in the Stream Reader page hero and closing section.
- **Privacy Statement**: A page distinguishing the iOS app's data practices (none) from the websites' data practices (cookie-free aggregate analytics).
- **Contact Point**: The email address info@moonpublishingmedia.com, presented as a mailto link on the Contact page.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: A first-time visitor arriving at the Stream Reader page can identify the app's name, purpose, and how to get it within 10 seconds of landing, without scrolling past the hero
- **SC-002**: The App Store badge and browser link are both reachable and clickable from the top of the Stream Reader page and from its closing section
- **SC-003**: 100% of internal navigation links (header, footer, homepage Stream Reader block, privacy callout) resolve to the correct page with zero broken links
- **SC-004**: The homepage no longer contains any unnamed or vague reference to "an app in development" — the app is named and linked everywhere it is referenced
- **SC-005**: A visitor or compliance reviewer can determine, from the privacy statement alone, whether the app collects personal data (it does not) and whether the websites set cookies (they do not)
- **SC-006**: Pages pass an accessibility check covering alt text presence, single-`<h1>` heading order, sufficient text contrast, keyboard operability, and respect for reduced-motion preference
- **SC-007**: A Stream Reader page link pasted into an email or chat client renders a non-generic preview with a title, description, and image
- **SC-008**: All pages render correctly with no horizontal scrolling or content overflow from 375px to 2560px+ viewport width
- **SC-009**: The site produces no errors in the browser console during normal navigation across all four pages
- **SC-010**: The site deploys successfully as a static site with no build step, with analytics active and collecting visit data without displaying a cookie-consent banner

## Assumptions

- The constitution has already been amended (App Teaser Policy retired, rounded corners allowed, cookie-free analytics permitted) — confirmed as of this spec's creation.
- Tech stack remains pure HTML5 + CSS3, no frameworks or build tools, plus the single Vercel Web Analytics script.
- Image assets (streaming GIF, Library screenshot, Customization screenshot, app icon) will be placed in an assets folder; if any are missing at implementation time, the page ships with clearly labeled placeholders rather than blocking launch, and real assets are swapped in via a follow-up commit when available.
- App Store URL is https://apps.apple.com/us/app/stream-reader/id6760571431; browser version is https://streamreader.app.
- Contact email remains info@moonpublishingmedia.com.
- The privacy statement lives as its own page, linked from the footer and from the Stream Reader page's privacy callout.

## Out of Scope

- Any changes to streamreader.app (separate repository).
- The future ebook storefront.
- Organization-specific landing page content (carried by the cold email itself, not this site).
- Writing the cold email.
- App Store Connect setup and promo-code generation.
- Moving to Vercel Pro.
