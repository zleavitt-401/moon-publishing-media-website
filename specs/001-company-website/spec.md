# Feature Specification: Moon Publishing Media Company Website

**Feature Branch**: `001-company-website`
**Created**: 2026-02-19
**Status**: Draft
**Input**: User description: "Two-page company website (Home + Contact) for moonpublishingmedia.com to satisfy Apple Developer Program organization enrollment and establish company credibility"

## User Scenarios & Testing *(mandatory)*

### User Story 1 - First Impression on Homepage (Priority: P1)

A visitor arrives at moonpublishingmedia.com for the first time — whether they are an Apple reviewer validating the company, a potential reader, or a curious visitor. They see a polished, professional homepage that immediately communicates Moon Publishing Media is a real, credible independent publisher focused on wellness and self-care content.

**Why this priority**: The homepage is the single most critical page. It must establish legitimacy at first glance. Apple reviewers and any external validator will land here first. If this page looks like a placeholder or template, the entire site fails its purpose.

**Independent Test**: Load the homepage in a browser on both mobile and desktop. The page should feel like a real publisher's site — not a generic template — with clear branding, a compelling headline, company description, and a teaser for upcoming work.

**Acceptance Scenarios**:

1. **Given** a visitor loads the homepage, **When** the page renders, **Then** they see the company logo (crescent moon + wordmark) in the top-left corner with a navigation link to the Contact page in the top-right
2. **Given** a visitor is on the homepage, **When** they scroll through the page, **Then** they encounter three distinct content sections in order: a hero with headline and subheadline, an "about" section describing the company, and a "coming soon" section teasing a digital product — followed by a footer with copyright
3. **Given** a visitor views the homepage on a mobile device (375px width), **When** the page renders, **Then** all content is readable, properly laid out, and nothing is cut off or horizontally scrolling
4. **Given** a visitor views the homepage on a desktop (1200px+ width), **When** the page renders, **Then** the layout uses generous whitespace and the content is comfortably centered, not stretched edge-to-edge

---

### User Story 2 - Contacting the Company (Priority: P1)

A visitor wants to reach out to Moon Publishing Media — whether they are a writer, a reader, or someone evaluating the company. They navigate to the Contact page and find a clear, warm invitation to get in touch along with a prominently displayed email address that opens their mail client when clicked.

**Why this priority**: Equal to P1 because a company website without a working contact method is incomplete. Apple Developer Program enrollment requires demonstrable contact information. The email link is the site's only interactive element and must work flawlessly.

**Independent Test**: Navigate to the Contact page. The email address should be visually prominent (not buried in body text), and clicking it should open the visitor's default email client with the correct address pre-filled.

**Acceptance Scenarios**:

1. **Given** a visitor is on any page, **When** they click the "Contact" link in the navigation, **Then** they are taken to the Contact page
2. **Given** a visitor is on the Contact page, **When** the page renders, **Then** they see a heading ("Say Hello"), warm introductory copy, and the email address info@moonpublishingmedia.com displayed prominently — not inline within a paragraph
3. **Given** a visitor clicks the email address on the Contact page, **When** the click is registered, **Then** their default email client opens with "info@moonpublishingmedia.com" pre-filled in the "To" field
4. **Given** a visitor is on the Contact page on mobile, **When** they tap the email address, **Then** the device's native email compose action is triggered

---

### User Story 3 - Navigating Between Pages (Priority: P2)

A visitor wants to move between the Homepage and Contact page seamlessly. The site provides consistent navigation across both pages with the logo linking back to the homepage and a "Contact" link always available.

**Why this priority**: Navigation is essential for usability but is a simpler concern than the content and functionality of either page. It supports the primary stories rather than standing alone.

**Independent Test**: From any page, the visitor should be able to reach the other page in one click. The header and footer should look identical on both pages.

**Acceptance Scenarios**:

1. **Given** a visitor is on the Contact page, **When** they click the logo in the header, **Then** they are taken back to the Homepage
2. **Given** a visitor is on the Homepage, **When** they click "Contact" in the navigation, **Then** they are taken to the Contact page
3. **Given** a visitor navigates between pages, **When** they compare the header and footer on each page, **Then** they are visually identical in layout, styling, and content

---

### User Story 4 - Professional Visual Identity (Priority: P2)

A visitor perceives Moon Publishing Media as a legitimate, established publisher through consistent visual design: warm color palette, elegant typography, intentional whitespace, and a distinctive logo. The site does not look like a default template or an AI-generated placeholder.

**Why this priority**: Visual identity supports credibility (P1 goal) but is a cross-cutting concern rather than a standalone user flow. It applies to all pages equally.

**Independent Test**: Show the site to someone unfamiliar with the project. They should be able to describe it as "a small publisher's website" without being told what it is. The design should feel warm, minimal, and intentional.

**Acceptance Scenarios**:

1. **Given** a visitor views any page, **When** they observe the typography, **Then** headings use an elegant serif font and body text uses a clean sans-serif font — both consistent across pages
2. **Given** a visitor views any page, **When** they observe the color scheme, **Then** the background is a warm off-white, text is a soft near-black (not harsh pure black), and accent elements use a muted dusty rose tone
3. **Given** a visitor views the logo, **When** they examine it at small sizes, **Then** the crescent moon shape and wordmark are both clearly recognizable and not blurry or distorted
4. **Given** a visitor views any page, **When** they observe the overall design, **Then** corner treatment (angular or rounded) is consistent and intentional across elements

---

### Edge Cases

- What happens when external fonts fail to load? The site MUST remain fully readable with fallback system fonts (serif for headings, sans-serif for body).
- What happens when a visitor accesses a URL that doesn't exist (e.g., /about)? Out of scope — the hosting platform handles 404 responses by default.
- What happens when the email link is clicked on a device with no email client configured? The operating system handles this behavior; the site is not responsible for client-side mail configuration.
- What happens when the site is viewed on very large screens (2560px+)? Content MUST remain centered and comfortably readable, not stretched to fill the full viewport width.

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The site MUST consist of exactly two pages: a Homepage and a Contact page
- **FR-002**: Both pages MUST share an identical header containing the company logo (left-aligned) and a "Contact" navigation link (right-aligned)
- **FR-003**: Both pages MUST share an identical footer containing the copyright notice "© 2026 Moon Publishing Media. All rights reserved."
- **FR-004**: The Homepage MUST display three content sections in order: Hero (headline + subheadline), About ("Who We Are"), and Coming Soon ("Something New Is Coming")
- **FR-005**: The Hero section MUST display the headline "Words that move you." and the subheadline "Moon Publishing Media is an independent publisher dedicated to wellness, self-care, and the stories that help us live better."
- **FR-006**: The app section MAY name Stream Reader, describe its features, show screenshots, and link directly to its App Store listing
- **FR-007**: The Contact page MUST display the heading "Say Hello", the introductory copy "We'd love to hear from you — whether you're a reader, a writer, or just curious about what we're building.", and the email address info@moonpublishingmedia.com as a clickable link that opens the visitor's mail client
- **FR-008**: The email address MUST be displayed prominently as a standalone element, not embedded inline within a paragraph
- **FR-009**: The company logo MUST link to the Homepage from any page
- **FR-010**: The site MUST be fully readable and properly laid out on devices from 375px to 2560px+ viewport width
- **FR-011**: The site MUST use two distinct typefaces: an elegant serif for headings and a clean sans-serif for body text
- **FR-012**: The site MUST use a warm color palette: off-white background, soft near-black text, and muted dusty rose accents
- **FR-013**: Rounded corners are permitted as a deliberate design choice; corner treatment MUST be applied consistently
- **FR-014**: The site MUST deploy and function correctly as a static site with no server-side processing
- **FR-015**: The site MUST include a company logo consisting of a crescent moon shape and "Moon Publishing Media" wordmark

### Key Entities

- **Page**: A single web document accessible via URL (Homepage or Contact). Each page has a header, main content area, and footer.
- **Logo**: The company's visual identity mark — a crescent moon shape paired with the "Moon Publishing Media" wordmark. Used consistently in the header of every page.
- **Contact Point**: The single method of reaching the company: email address info@moonpublishingmedia.com, presented as an interactive element that triggers the visitor's mail client.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Both pages render correctly and are fully readable on mobile (375px viewport) and desktop (1200px+ viewport) without horizontal scrolling or content overflow
- **SC-002**: The company logo is clearly recognizable at the size it appears in the page header — the crescent moon shape and wordmark are both distinguishable
- **SC-003**: Clicking the Contact navigation link from the Homepage successfully loads the Contact page, and clicking the logo from the Contact page successfully loads the Homepage — zero broken internal links
- **SC-004**: Clicking the email address on the Contact page triggers the device's mail client compose action with info@moonpublishingmedia.com pre-filled as the recipient
- **SC-005**: Both typefaces (serif headings, sans-serif body) load and render correctly, with readable fallback fonts displaying if external fonts fail to load
- **SC-006**: The site is perceived as a professional, credible publisher website by external observers — not as a template, placeholder, or auto-generated page
- **SC-007**: The site produces no errors in the browser console during normal navigation
- **SC-008**: The site deploys successfully as a static site and serves all pages without requiring any server-side processing, build steps, or environment configuration
