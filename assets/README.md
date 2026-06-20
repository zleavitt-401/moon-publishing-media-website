# Assets

All image files currently in this folder are **clearly labeled placeholders** (they render the word "PLACEHOLDER"). The pages reference these placeholder paths so the layout is complete and testable now; swap in the real artwork via a follow-up commit (per the asset-gating decision in the feature spec).

Placeholders are authored as **SVG** because this environment cannot rasterize text (no Ghostscript), and SVG renders crisp labels at any size. When real assets arrive you can either:

- save the real file under the same base name with the real extension (e.g. `app-icon.png`) and update the one `src=`/`href=` reference in the HTML, **or**
- keep the SVG name if the real asset is also an SVG.

## Site-wide

| File | Used by | Real asset to supply |
|------|---------|----------------------|
| `favicon.svg` | all pages (`<link rel="icon">`) | Final MPM favicon (SVG or .ico) |
| `og-image.svg` | homepage / contact / privacy Open Graph | 1200×630 share image |

## Stream Reader (`streamreader/`)

| File | Used by | Real asset to supply |
|------|---------|----------------------|
| `app-icon.svg` | streamreader hero, homepage block | App Store icon (1024×1024 PNG) |
| `streaming-demo.svg` | "What it does" section (animated) | Optimized streaming demo **GIF** (keep file size small — FR-023) |
| `streaming-demo-static.svg` | reduced-motion fallback | First-frame still exported from the GIF |
| `library.svg` | Features section | Library screenshot (save & resume) |
| `customization.svg` | Features section | Customization screenshot (font/size/speed/word-color) |
| `app-store-badge.svg` | hero + closing CTA | **Official, unmodified** Apple "Download on the App Store" badge — download from <https://developer.apple.com/app-store/marketing/guidelines/> · do NOT recreate it |
| `og-streamreader.svg` | streamreader Open Graph | 1200×630 share image (app icon or clean screenshot) |

## Reduced-motion note

`streaming-demo.svg` animates in an `<img>` tag. A CSS `@media (prefers-reduced-motion: reduce)` rule hides it and shows `streaming-demo-static.svg` instead — no JavaScript. When the real GIF is added, export its first frame to the static file so the swap stays seamless.
