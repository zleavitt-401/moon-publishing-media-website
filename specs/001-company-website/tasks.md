# Tasks: Moon Publishing Media Company Website

**Input**: Design documents from `/specs/001-company-website/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-structure.md, quickstart.md

**Tests**: Not explicitly requested in the feature specification. Manual testing via quickstart.md checklist.

**Organization**: Tasks are grouped by user story to enable independent implementation and testing. US3 (Navigation) and US4 (Visual Identity) are cross-cutting concerns addressed in the Foundational phase since they underpin all other stories.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3, US4)
- Include exact file paths in descriptions

---

## Phase 1: Setup

**Purpose**: Create the three source files with document structure, Google Fonts, and shared `<head>` content per the page-structure contract.

- [x] T001 Create `styles.css` with CSS custom properties (`:root` block) defining all design tokens: `--color-bg: #FAF9F6`, `--color-text: #1C1C1C`, `--color-accent: #C4A0A0`, `--color-text-muted: #6B6B6B`, `--font-heading`, `--font-body`, `--max-width: 1140px`, spacing tokens. Add the custom lightweight CSS reset (box-sizing, margin/padding, font-smoothing, media elements) per research.md §2.2. File: `styles.css`
- [x] T002 [P] Create `index.html` with complete `<head>` (charset, viewport, title "Moon Publishing Media", meta description, Google Fonts preconnect + link per research.md §3.1, stylesheet link to `styles.css`) and empty `<body>` with semantic skeleton: `<header>`, `<main>`, `<footer>`. File: `index.html`
- [x] T003 [P] Create `contact.html` with complete `<head>` (charset, viewport, title "Contact — Moon Publishing Media", meta description, identical Google Fonts links, stylesheet link to `styles.css`) and empty `<body>` with semantic skeleton: `<header>`, `<main>`, `<footer>`. File: `contact.html`

**Checkpoint**: Three files exist. Both HTML files open in browser with no console errors. CSS loads and applies the warm off-white background color.

---

## Phase 2: Foundational — Shared Components & Visual Identity (US3 + US4)

**Purpose**: Build the shared header (with inline SVG logo), footer, base typography, and layout CSS that ALL user stories depend on. This phase delivers US3 (Navigation Between Pages) and US4 (Professional Visual Identity) since they are cross-cutting prerequisites.

**⚠️ CRITICAL**: No page-specific content (US1, US2) can begin until shared components and base styles are complete.

**Goal (US3)**: Visitor can navigate between homepage and contact page via logo click and Contact nav link. Header and footer are visually identical on both pages.

**Goal (US4)**: Consistent visual identity — Cormorant Garamond serif headings, Inter sans-serif body, warm color palette, muted dusty rose accents, zero rounded corners, distinctive inline SVG logo.

**Independent Test (US3)**: Click "Contact" link on index.html → loads contact.html. Click logo on contact.html → loads index.html. Header and footer look identical on both pages.

**Independent Test (US4)**: View either page — headings use serif font, body uses sans-serif, background is warm off-white, text is soft near-black, accent elements are dusty rose. No rounded corners anywhere. Logo crescent moon and wordmark are clearly recognizable.

### Implementation

- [ ] T004 Create the inline SVG logo in `index.html` `<header>`: crescent moon shape using `<path>` with cubic Bézier curves + "Moon Publishing Media" `<text>` wordmark using Cormorant Garamond. Include `role="img"`, `aria-labelledby="logo-title"`, `<title id="logo-title">Moon Publishing Media</title>`, `<desc id="logo-desc">Crescent moon icon with company wordmark</desc>`. Wrap SVG in `<a href="/" class="logo-link" aria-label="Moon Publishing Media home">`. Add `<nav>` with `<a href="contact.html">Contact</a>`. File: `index.html`
- [ ] T005 Add the shared footer to `index.html`: `<footer class="site-footer">` containing `<p>© 2026 Moon Publishing Media. All rights reserved.</p>`. File: `index.html`
- [ ] T006 Copy the identical header and footer markup from `index.html` to `contact.html` — byte-for-byte identical per constitution. File: `contact.html`
- [ ] T007 Add base typography styles to `styles.css`: `body` font-family using `var(--font-body)`, background `var(--color-bg)`, color `var(--color-text)`. Heading styles (h1, h2, h3) using `var(--font-heading)` with `clamp()` fluid sizing per research.md §3.2 typography scale (h1: `clamp(2rem, 4vw, 3.125rem)` weight 700 line-height 1.2; h2: `clamp(1.6rem, 3vw, 2.5rem)` weight 600 line-height 1.3). Base link styles with `--color-accent`. File: `styles.css`
- [ ] T008 Add layout styles to `styles.css`: `.site-header` with `display: flex; justify-content: space-between; align-items: center;` and padding. `.site-footer` with `display: flex; flex-direction: column; align-items: center;` padding, and `--color-text-muted` text. `main` with centered content container using `max-width: var(--max-width)` and `margin: 0 auto` with horizontal padding. File: `styles.css`
- [ ] T009 Add logo styles to `styles.css`: `.logo` SVG sizing with `max-width` responsive values (120px mobile, 160px desktop), `height: auto`, and `display: block`. `.logo-link` with no text-decoration. Nav link styles matching `--font-body` with `--color-text` color. File: `styles.css`
- [ ] T010 Add responsive media queries to `styles.css`: `@media (min-width: 768px)` for tablet adjustments (header padding, section spacing, logo size). `@media (min-width: 1200px)` for desktop adjustments (generous whitespace, larger section padding, logo at full size). Ensure content stays centered and readable at 2560px+ via `max-width` constraint. File: `styles.css`

**Checkpoint**: Both pages display identical header (logo + Contact nav link) and footer (copyright). Logo links to `/`, Contact link goes to `contact.html`. Typography shows Cormorant Garamond headings and Inter body text. Warm color palette visible. No rounded corners. Responsive from 375px to 1200px+.

---

## Phase 3: User Story 1 — First Impression on Homepage (Priority: P1) 🎯 MVP

**Goal**: Visitor sees a polished, professional homepage with three distinct content sections: hero (headline + subheadline), about (company description), and coming soon (vague teaser). The page establishes MPM as a credible publisher.

**Independent Test**: Load `index.html` in browser at 375px and 1200px. See logo in header, three content sections in order (hero → about → coming soon), footer with copyright. Content is readable, properly laid out, no horizontal scrolling. Feels like a real publisher's site.

### Implementation

- [ ] T011 [US1] Add the Hero section to `index.html` `<main>`: `<section class="hero">` containing `<h1>Words that move you.</h1>` and `<p>Moon Publishing Media is an independent publisher dedicated to wellness, self-care, and the stories that help us live better.</p>`. This is the only `<h1>` on this page. File: `index.html`
- [ ] T012 [US1] Add the About section to `index.html` `<main>` after hero: `<section class="about">` containing `<h2>Who We Are</h2>` and one or more `<p>` elements describing Moon Publishing Media as an independent publisher of wellness and self-care content. File: `index.html`
- [ ] T013 [US1] Add the Coming Soon section to `index.html` `<main>` after about: `<section class="coming-soon">` containing `<h2>Something New Is Coming</h2>`, a `<p>` with a vague teaser about a digital product in development, and a status label "Currently in development". MUST NOT include any app name, screenshots, or specific feature list per App Teaser Policy. File: `index.html`
- [ ] T014 [US1] Add component styles to `styles.css` for homepage sections: `.hero` with centered text, generous vertical padding, and prominent visual treatment for the headline. `.about` with comfortable reading width and section spacing. `.coming-soon` with distinct visual treatment (accent color for status label), section spacing. Add responsive adjustments for these sections in existing media query blocks. File: `styles.css`

**Checkpoint**: Homepage is fully functional — hero with "Words that move you.", about with company description, coming soon with vague teaser. All three sections visible in order. Responsive at 375px (stacked, readable) and 1200px+ (centered, generous whitespace). This is the MVP — the site could ship with just this page and pass Apple reviewer inspection.

---

## Phase 4: User Story 2 — Contacting the Company (Priority: P1)

**Goal**: Visitor navigates to the Contact page and finds a clear invitation to get in touch with a prominently displayed email address that opens their mail client.

**Independent Test**: Navigate to `contact.html`. See heading "Say Hello", warm introductory copy, and `info@moonpublishingmedia.com` displayed prominently as a standalone element (not inline in a paragraph). Click the email — mail client opens with the address pre-filled. Test on mobile (375px) — email link is easily tappable.

### Implementation

- [ ] T015 [US2] Add contact content to `contact.html` `<main>`: `<section class="contact">` containing `<h1>Say Hello</h1>`, `<p>We'd love to hear from you — whether you're a reader, a writer, or just curious about what we're building.</p>`, and a standalone `<a href="mailto:info@moonpublishingmedia.com" class="email-link">info@moonpublishingmedia.com</a>` (NOT inside a `<p>` — standalone per FR-008). File: `contact.html`
- [ ] T016 [US2] Add contact component styles to `styles.css`: `.contact` section with comfortable padding and centered layout. `.email-link` styled as prominent CTA — `var(--color-accent)` background, generous padding (minimum 44px × 44px touch target for mobile), `var(--color-bg)` text color, no text-decoration, zero rounded corners, clear hover/focus states (underline on hover, visible focus outline with `outline: 2px solid var(--color-text); outline-offset: 2px`). Add responsive adjustments for contact section in existing media query blocks. File: `styles.css`

**Checkpoint**: Contact page is fully functional — "Say Hello" heading, warm copy, prominent email link. Clicking email opens mail client. Email link is visually distinct (button-like CTA). Touch target is 44px+ on mobile. Both P1 stories now complete — site is ready for Apple Developer Program review.

---

## Phase 5: Polish & Cross-Cutting Concerns

**Purpose**: Final quality pass across both pages. Ensure cross-page consistency, edge case handling, and deployment readiness.

- [ ] T017 Verify header and footer markup is byte-for-byte identical in `index.html` and `contact.html` — diff the shared sections. If any drift occurred during implementation, sync both files. Files: `index.html`, `contact.html`
- [ ] T018 Verify fallback font behavior: ensure `styles.css` font stacks include proper fallbacks (`serif` for headings, `sans-serif` for body) so the site remains fully readable if Google Fonts fail to load. File: `styles.css`
- [ ] T019 [P] Verify zero rounded corners across all elements in `styles.css` — search for any `border-radius` declarations and remove them. Ensure no inherited browser defaults add rounding (buttons, inputs if any). File: `styles.css`
- [ ] T020 [P] Verify no JavaScript exists in `index.html` or `contact.html` — no `<script>` tags, no inline event handlers, no JS files referenced. Files: `index.html`, `contact.html`
- [ ] T021 Final responsive check: verify both pages at 375px (no horizontal scroll, all content readable), 768px (tablet layout adjusts), 1200px (desktop with generous whitespace), and 2560px (content stays centered, not stretched). Adjust CSS if any layout issues found. Also verify zero browser console errors (no 404s for fonts/stylesheets, no invalid CSS warnings, no JS errors) on both pages. Files: `index.html`, `contact.html`, `styles.css`
- [ ] T022 Run quickstart.md testing checklist to validate all items pass. File: `specs/001-company-website/quickstart.md`

**Checkpoint**: Site is complete and deployment-ready. Both pages pass all acceptance scenarios from spec.md. No console errors. Responsive across all target viewports. Ready to push to GitHub for Vercel auto-deploy.

---

## Dependencies & Execution Order

### Phase Dependencies

- **Phase 1 (Setup)**: No dependencies — start immediately
- **Phase 2 (Foundational / US3+US4)**: Depends on T001 (CSS tokens + reset). T002 and T003 can run in parallel with each other but before T004–T006.
- **Phase 3 (US1 Homepage)**: Depends on Phase 2 completion (shared header/footer/styles must exist)
- **Phase 4 (US2 Contact)**: Depends on Phase 2 completion. Can run in parallel with Phase 3 (different files for content, shared CSS).
- **Phase 5 (Polish)**: Depends on Phases 3 and 4 completion

### User Story Dependencies

- **US3 (Navigation)** + **US4 (Visual Identity)**: Foundational — implemented in Phase 2, prerequisite for all other stories
- **US1 (Homepage)**: Depends on Phase 2 only. No dependency on US2.
- **US2 (Contact)**: Depends on Phase 2 only. No dependency on US1.
- **US1 and US2 can be implemented in parallel** after Phase 2, since they modify different `<main>` content in different HTML files. They share `styles.css` but touch different component selectors (`.hero`/`.about`/`.coming-soon` vs `.contact`/`.email-link`).

### Within Each Phase

- Phase 1: T001 first (CSS needed by HTML), then T002 + T003 in parallel
- Phase 2: T004 → T005 → T006 (sequential — logo first, then footer, then copy to contact.html). T007 → T008 → T009 → T010 (CSS in section order). HTML and CSS tracks can run in parallel.
- Phase 3: T011 → T012 → T013 (sequential — sections in page order). T014 after all sections exist.
- Phase 4: T015 then T016 (content before styles).
- Phase 5: T017–T020 can run in parallel. T021 after all fixes. T022 last.

### Parallel Opportunities

```
Phase 1:    T001 → [T002 ∥ T003]
Phase 2:    [T004→T005→T006] ∥ [T007→T008→T009→T010]
Phase 3+4:  [T011→T012→T013→T014] ∥ [T015→T016]  (after Phase 2)
Phase 5:    [T017 ∥ T018 ∥ T019 ∥ T020] → T021 → T022
```

---

## Implementation Strategy

### MVP First (Phase 1 + 2 + 3)

1. Complete Phase 1: Create files with document structure
2. Complete Phase 2: Shared header/footer, logo, base styles (delivers US3 + US4)
3. Complete Phase 3: Homepage content sections (delivers US1)
4. **STOP and VALIDATE**: Homepage is fully functional with logo, navigation, hero, about, coming soon. This alone satisfies the primary Apple Developer Program requirement.
5. Deploy if ready — single-page site with working navigation to contact page.

### Full Delivery (Add Phase 4 + 5)

6. Complete Phase 4: Contact page content (delivers US2)
7. Complete Phase 5: Polish, cross-page verification, responsive fine-tuning
8. Both P1 stories complete. All P2 stories (US3, US4) already delivered in Phase 2.
9. Deploy complete two-page site.

---

## Notes

- All file paths are relative to repository root (flat structure: `index.html`, `contact.html`, `styles.css`)
- No `src/`, `tests/`, or other subdirectories — this is a pure static site
- Commit after each phase checkpoint for clean git history
- Header/footer must be manually synced between both HTML files (no templating per constitution)
- CSS follows strict section order: variables → reset → base → layout → components → utilities → media queries
