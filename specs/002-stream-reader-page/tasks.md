---

description: "Task list for Stream Reader Product Page + Website Professionalization"
---

# Tasks: Stream Reader Product Page + Website Professionalization

**Input**: Design documents from `/specs/002-stream-reader-page/`
**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/page-structure.md, quickstart.md

**Tests**: Not requested. This is a static HTML/CSS site with no test framework; verification is manual (browser, viewports, a11y, link graph) and lives in the Polish phase.

**Organization**: Tasks grouped by user story. Note: nearly all stories share two files (`styles.css` and the header/footer markup repeated in every `.html`), so cross-story `[P]` is limited — `[P]` is used only for genuinely independent files.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies on incomplete tasks)
- **[Story]**: US1–US5 maps to the user stories in spec.md

## Path Conventions

Static multi-file site at repo root: `index.html`, `streamreader.html`, `contact.html`, `privacy.html`, `styles.css`, `assets/`.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Asset scaffolding and shared metadata foundations

- [X] T001 [P] Create `assets/` and `assets/streamreader/` folders at repo root
- [X] T002 [P] Add placeholder image files (clearly labeled) to `assets/streamreader/` and `assets/` — authored as labeled **SVG** placeholders (environment lacks raster text rendering): `app-icon.svg`, `streaming-demo.svg`, `streaming-demo-static.svg`, `library.svg`, `customization.svg`, `app-store-badge.svg`, `og-streamreader.svg`; and `assets/favicon.svg`, `assets/og-image.svg` — real files swap in later
- [X] T003 [P] Add `assets/README.md` documenting placeholder status, the real-asset table, and the official Apple badge source URL

**Checkpoint**: Asset paths exist so HTML `src`/`href` references resolve during development.

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: The shared header, footer, and base page-chrome CSS that EVERY page and user story depends on. Must complete before story pages are built.

**⚠️ CRITICAL**: All user stories render the same header/footer; build it once here.

- [X] T004 Define the canonical shared header markup (logo → `/`, nav links: `Stream Reader → streamreader.html`, `Contact → contact.html`; NO Privacy link) per contracts/page-structure.md — applied identically to all four pages in later tasks
- [X] T005 Define the canonical shared footer markup (copyright + footer links: `Stream Reader → streamreader.html`, `Privacy Policy → privacy.html`) per contracts/page-structure.md — applied identically to all four pages
- [X] T006 In `styles.css`, updated `.site-header nav` to flex with gap + nav-link `:focus-visible`; no overflow at 375px
- [X] T007 In `styles.css`, extended `.footer-links` to flex-wrap with gap for the two-link footer
- [X] T008 [P] In `styles.css`, added `.demo-media` + `@media (prefers-reduced-motion: reduce)` CSS-only swap (animated → static), no JS
- [X] T009 [P] In `styles.css`, added `--color-accent-app: #2F6FED` placeholder var (finalize from real app art, contrast-checked)

**Checkpoint**: Shared chrome and base CSS hooks ready — story pages can now be assembled.

---

## Phase 3: User Story 1 - Stream Reader Product Page (Priority: P1) 🎯 MVP

**Goal**: A dedicated `streamreader.html` that names the app, shows the GIF + both screenshots, and presents the App Store badge as the primary above-the-fold action with streamreader.app as secondary.

**Independent Test**: Load `streamreader.html` directly (no other page visited). Confirm app name, icon, tagline, App Store badge (primary), and browser link (secondary) are visible without scrolling past the hero; the six sections appear in order; badge → App Store URL, browser link → streamreader.app.

### Implementation for User Story 1

- [X] T010 [US1] Create `streamreader.html` with the standard `<head>` (Google Fonts links, `styles.css` link), unique `<title>` and `<meta name="description">` (FR-025), favicon link, and Open Graph + twitter:card meta using `assets/streamreader/og-streamreader.png` (FR-026)
- [X] T011 [US1] Add the shared header (from T004) and shared footer (from T005) to `streamreader.html`, byte-identical to the canonical markup
- [X] T012 [US1] Build Section 1 (Hero) in `streamreader.html`: app icon `<img>` with alt, app name as the single `<h1>`, tagline exactly "One line. Your pace. Nothing in the way." (FR-005), App Store badge as `<a href="https://apps.apple.com/us/app/stream-reader/id6760571431"><img alt="Download on the App Store"></a>` primary CTA (FR-006), and secondary `<a href="https://streamreader.app">` browser link (FR-007)
- [X] T013 [US1] Build Section 2 (What It Does) in `streamreader.html`: streaming demo GIF `<img>` with descriptive alt + static-frame fallback wired to the reduced-motion rule (T008), plus 2–3 lines of focus-framed, non-clinical copy (FR-008)
- [X] T014 [US1] Build Section 3 (Features) in `streamreader.html`: Library screenshot and Customization screenshot, each `<img>` with descriptive alt text (FR-009, FR-019)
- [X] T015 [US1] Build Section 4 (Privacy Callout) in `streamreader.html`: standalone block stating standalone/no-account/no-data/offline, linking to `privacy.html` (FR-010)
- [X] T016 [US1] Build Section 5 (Who It's For) in `streamreader.html`: a few inclusive, non-clinical lines (FR-011)
- [X] T017 [US1] Build Section 6 (Closing CTA) in `streamreader.html`: repeat App Store badge + browser link (FR-004, SC-002)
- [X] T018 [US1] In `styles.css`, add Stream Reader page component styles (`.sr-hero`, `.sr-what`, `.sr-features`, `.sr-privacy`, `.sr-audience`, `.sr-cta`): warm MPM shell + app-blue secondary accent (T009) around screenshots; rounded corners as a deliberate, consistent choice (FR-027, FR-028); responsive layout for screenshots/GIF/badge without distortion (FR-030)

**Checkpoint**: `streamreader.html` is fully functional and independently testable — the MVP destination for cold-email links.

---

## Phase 4: User Story 2 - Homepage Names & Links Stream Reader (Priority: P1)

**Goal**: The homepage keeps MPM's self-care identity but replaces the vague "Coming Soon" teaser with a named Stream Reader block linking to the new page, and drops the duplicate inline contact section.

**Independent Test**: Load `index.html` in isolation. Confirm hero + "Who We Are" are intact; the old Coming Soon slot now holds a named Stream Reader block linking to `streamreader.html`; no unnamed "app in development" language remains; the embedded contact section is gone.

### Implementation for User Story 2

- [X] T019 [US2] In `index.html`, replace the shared header and footer with the canonical versions (T004/T005), adding the Stream Reader nav link
- [X] T020 [US2] In `index.html`, replace the `.coming-soon` section content with a named Stream Reader block (heading naming "Stream Reader", short self-care-voice description, link → `streamreader.html`) in the same grid slot — no layout restructuring (FR-013); keep any future-content language soft and separate (FR-014)
- [X] T021 [US2] In `index.html`, remove the embedded `<section class="contact" id="contact">` block (canonical contact now lives in `contact.html`) per clarification; verify the grid still renders correctly without it
- [X] T022 [US2] In `index.html` `<head>`, add favicon link and Open Graph/twitter:card meta using `assets/og-image.png`; keep the homepage's unique title/description (FR-025, FR-026)
- [X] T023 [US2] In `styles.css`, repurpose `.coming-soon` styles into `.stream-reader-teaser` (or equivalent) for the new block; remove now-unused `.contact`/`.status-label`/`.email-link` rules ONLY if no longer referenced by any page (verify against contact.html first), otherwise leave intact; update the `.page-grid` `grid-template-areas` to drop the removed `contact` area

**Checkpoint**: Homepage no longer hides the app; US1 + US2 both work independently.

---

## Phase 5: User Story 3 - Contact Welcomes Readers, Educators, Organizations (Priority: P2)

**Goal**: The Contact page welcomes the three audience types explicitly and exposes footer links.

**Independent Test**: Load `contact.html` directly. Confirm welcome copy explicitly mentions readers, educators, and organizations; footer links to Home (via logo), Stream Reader, and Privacy work; mailto link present.

### Implementation for User Story 3

- [X] T024 [US3] In `contact.html`, replace the shared header and footer with the canonical versions (T004/T005), adding the Stream Reader nav link
- [X] T025 [US3] In `contact.html`, update the welcome copy to explicitly address readers, educators, and organizations (FR-015); keep the `info@moonpublishingmedia.com` mailto link as a standalone element (FR-016)
- [X] T026 [US3] In `contact.html` `<head>`, add favicon link and Open Graph/twitter:card meta; keep the page's unique title/description (FR-025, FR-026)

**Checkpoint**: Contact completes the outreach loop; US1–US3 work independently.

---

## Phase 6: User Story 4 - Consistent Navigation Across All Pages (Priority: P2)

**Goal**: Header (with Stream Reader + Contact, no Privacy) and footer are byte-identical across all four pages.

**Independent Test**: Visit all four pages; diff the header and footer markup — identical everywhere; Stream Reader nav and logo links resolve from each page.

### Implementation for User Story 4

- [X] T027 [US4] In `privacy.html`, replace the shared header and footer with the canonical versions (T004/T005) — header/footer refresh ONLY; do NOT rewrite privacy.html body content (deferred per user direction)
- [X] T028 [US4] Diff the header markup across `index.html`, `streamreader.html`, `contact.html`, `privacy.html` and reconcile any differences so all four are byte-identical (FR-002)
- [X] T029 [US4] Diff the footer markup across all four pages and reconcile so all four are byte-identical (FR-003)

**Checkpoint**: Navigation is consistent site-wide; US1–US4 work independently.

---

## Phase 7: User Story 5 - Privacy Statement Reachable (Priority: P3)

**Goal**: The privacy statement is reachable from the footer (all pages) and the Stream Reader privacy callout. (Content rewrite deferred — wiring only.)

**Independent Test**: From the footer of any page and from the Stream Reader privacy callout, the link reaches `privacy.html`; the page renders with the shared chrome.

### Implementation for User Story 5

- [X] T030 [US5] Verify the footer Privacy Policy link (T005) and the Stream Reader privacy callout link (T015) both resolve to `privacy.html` from every page; fix any broken paths (FR-010, SC-003)

> **Deferred (tracked in plan.md Outstanding):** FR-017's full app-vs-website analytics disclosure rewrite of `privacy.html` content is intentionally NOT in scope this build.

**Checkpoint**: Privacy statement is reachable everywhere it should be.

---

## Phase 8: Polish & Cross-Cutting Concerns

**Purpose**: Site-wide concerns and manual verification mapped to spec criteria

- [X] T031 Added the single cookieless Vercel Web Analytics script before `</body>` on all four pages; verified exactly one script total per page (no other JS). NOTE: enabling Web Analytics in the Vercel dashboard is a deploy-time step (the script 404s in local dev; Vercel serves it in production).
- [X] T032 Accessibility pass: exactly one `<h1>` per page, 0 images missing alt, all interactive elements are native anchors with `:focus-visible` outlines, reduced-motion CSS swap in place (FR-019/020/022/024)
- [X] T033 [P] Contrast check found dusty rose `#C4A0A0` failed AA on bg (2.01:1) as text/CTA. Added `--color-accent-text: #925C5C` (4.56:1) for links/teaser/email-button; email button now white-on-#925C5C (5.37:1). Decorative rose kept. App-blue tagline 3.86:1 passes AA-large (large text). (FR-021)
- [X] T034 [P] GIF optimization N/A while placeholder (SVG, tiny); documented in `assets/README.md` for the real GIF (FR-023)
- [X] T035 Responsive pass: no horizontal overflow at 375/768/1280/2560px on any page; images scale via `max-width:100%` (FR-030, SC-008)
- [X] T036 Link-graph + console: all internal links resolve (zero MISSING); only 404 is the production-served analytics script (expected in local dev) (SC-003, SC-009)
- [X] T037 Share-preview: every page has unique title + description + favicon + OG/twitter tags; streamreader has its own OG image (SC-007)
- [X] T038 Ran quickstart verification in-browser. Deploy on Vercel + enabling Web Analytics is the remaining deploy-time action (SC-010)

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately.
- **Foundational (Phase 2)**: Depends on Setup. Defines shared header/footer/CSS hooks — BLOCKS all user stories.
- **User Stories (Phase 3–7)**: All depend on Foundational. US1 and US2 are both P1; US1 is the MVP destination and should go first. US3, US4, US5 follow.
- **Polish (Phase 8)**: Depends on all targeted stories being complete.

### User Story Dependencies

- **US1 (P1, Stream Reader page)**: After Foundational. The MVP — no dependency on other stories.
- **US2 (P1, Homepage)**: After Foundational. Links to `streamreader.html`, so best done after US1 exists (link target), but independently testable.
- **US3 (P2, Contact)**: After Foundational. Independent.
- **US4 (P2, Nav consistency)**: After US1–US3 page edits, since it reconciles header/footer across all four pages (including privacy.html).
- **US5 (P3, Privacy reachable)**: After US1 (privacy callout) and Foundational footer; mostly verification.

### File-Contention Notes (limits parallelism)

- `styles.css` is touched by T006–T009, T018, T023, T033 — these must be serialized (same file).
- The shared header/footer markup is applied per-page (T011, T019, T024, T027) — different files, but all derive from the same canonical source (T004/T005); reconcile in T028/T029.

### Parallel Opportunities

- Setup: T001, T002, T003 can run in parallel ([P]).
- Foundational: T008 and T009 are independent CSS additions ([P]); T006/T007 also edit `styles.css` so coordinate to avoid conflicts.
- Across stories: page bodies live in different files, so once Foundational is done, the body-content tasks of US1/US3 can proceed in parallel by different people — but every shared-CSS edit and every header/footer application must reconcile against the canonical source.
- Polish: T033 and T034 are independent ([P]).

---

## Implementation Strategy

### MVP First (User Story 1)

1. Phase 1: Setup (asset scaffolding).
2. Phase 2: Foundational (shared header/footer/CSS hooks).
3. Phase 3: US1 — `streamreader.html`.
4. **STOP and VALIDATE**: load `streamreader.html` standalone; confirm the independent test.
5. Deploy/demo — cold-email links now have a real destination.

### Incremental Delivery

1. Setup + Foundational → chrome ready.
2. US1 (Stream Reader page) → validate → deploy (MVP).
3. US2 (Homepage names the app) → validate → deploy.
4. US3 (Contact) → US4 (nav consistency) → US5 (privacy reachable) → validate each.
5. Polish (analytics, a11y, contrast, GIF, responsive, links, share preview, quickstart) → final deploy.

---

## Notes

- [P] = different files, no dependencies. Most `styles.css` and header/footer tasks are intentionally NOT [P] due to file contention.
- Assets ship as labeled placeholders; swap real files via a follow-up commit (asset-gating clarification).
- `privacy.html` content is NOT rewritten this build — header/footer refresh + linking only (FR-017 disclosure deferred).
- Commit after each task or logical group; every commit should be deployable (Constitution V).
