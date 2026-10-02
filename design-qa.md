# Design QA — WK Design mirror

Source: http://wk-design.ru/
Implementation checked: http://127.0.0.1:4173/
Captured and checked: 2026-10-02.
Browser: Codex in-app browser, using the same tab for normalized source/mirror comparisons.

## Findings

No actionable P0/P1/P2 differences remain. The native site files are retained.

## Viewport and density normalization

| Page | CSS viewport | Source and mirror screenshot pixels | Source full height | Mirror full height | Text / headings / section dimensions |
| --- | --- | --- | --- | --- | --- |
| index.html | 1440×900 | 1425×891 | 3800 | 3800 | Equal |
| about.html | 1440×900 | 1425×891 | 3483 | 3483 | Equal |
| contacts.html | 1440×900 | 1425×891 | 1160 | 1160 | Equal |
| policy.html | 1440×900 | 1425×891 | 6645 | 6645 | Equal |
| index.html | 390×844 | 375×812 | 4124 | 4124 | Equal |
| about.html | 390×844 | 375×812 | 3737 | 3737 | Equal |
| contacts.html | 390×844 | 375×812 | 1479 | 1479 | Equal |
| policy.html | 390×844 | 375×812 | 13012 | 13012 | Equal |

Browser captures exclude/normalize browser scrollbar space. Both source and mirror have identical screenshot dimensions for each compared state. No additional density scaling was applied for the focused comparisons. Contact sheets are scaled overview evidence; underlying top captures and focused crops remain available. Browser-owned scrollbar color can vary by origin and is excluded from design findings. Authored content, fonts, layouts, and colors were compared.

## Source truth and implementation evidence

- Source captures: `verification/source-{home,about,contacts,policy}-{desktop,mobile}-top.jpg`.
- Implementation captures: corresponding `verification/clone-...-top.jpg`.
- Full-view comparisons: `verification/contact-{home,about,contacts,policy}-{desktop,mobile}.jpg`; each contains original and mirror side by side at matching positions through the entire page, including footer.
- Focused typography comparisons: `verification/focused-home-mobile.png`, `verification/focused-policy-desktop.png`.
- Captured metrics and matching scroll positions: `verification/comparison-records.json`.
- Menu comparison: `verification/source-home-mobile-menu.jpg`, `verification/clone-home-mobile-menu.jpg`.
- Video and carousel states: `verification/clone-about-mobile-playing.jpg`, `verification/clone-home-mobile-slider-next.jpg`, `verification/interactions.json`.

## Required fidelity surfaces

- Fonts and typography: exact browser-served Manrope v20 WOFF2 CSS localized, including Cyrillic and all six unicode subsets; weights 200–800 retained. Heading family, weight, size, line height, bounding boxes and wrapping match on all eight route/viewport cases. Focused hero and legal text comparisons show matching typography.
- Spacing and layout rhythm: original Bootstrap CSS and native site CSS retained; all section heights and document heights match, with matching scroll positions in the final captures. Full comparisons include desktop grid, mobile stacking, header and footer.
- Colors and visual tokens: original palette and style declarations retained; no authored colors, radii, borders or other tokens changed. Visual comparisons match.
- Image quality and asset fidelity: original images, logo, sprite, favicons and MP4 copied without recompression. 33 original non-HTML/non-main-CSS files are byte-identical, including all images, original JS and video. No generated or replacement images/icons are used.
- Copy and content: all four pages retain identical DOM text. The entire privacy policy, public contact information, prices and product names are preserved.

## Interactions and verification

- Mobile menu opens/closes; selecting the advantages fragment closes the menu and releases body scroll.
- Internal page links, homepage/logo/breadcrumb links and catalog/advantages fragments resolve locally. External store, email and telephone URLs are preserved.
- Carousel next switches the active slide from Power bank Transparent to the dock station; previous restores the initial slide.
- The original 95,300,058-byte MP4 loads and plays (readyState 4, paused false, no video error); pause stops playback and returns the paused overlay.
- Console warnings/errors: none observed on the implementation across all routes and tested interactions.
- 55 internal resource/fragment references checked; all referenced files exist and return HTTP 200 locally.
- No external image/font/CSS/JS/video dependencies remain.
- Node syntax checks pass for all three original JS bundles.
- Original design/accessibility choices were preserved as requested; this was a fidelity check, not a redesign.

## Comparison history

1. Initial font capture used Google Fonts' generic TTF response. Side-by-side mobile comparison identified a Cyrillic font difference (P2). Fix: acquire the exact browser-served CSS and all six WOFF2 subsets. Post-fix evidence: focused mobile hero/legal text comparisons and all eight route/viewport comparisons show matching typography, dimensions and wrapping.
2. Initial captures made in two tabs used different native scroll distances despite equal CSS viewports. This was a capture-state mismatch, not a website defect. Recaptured source and mirror sequentially in the same tab; every final scroll position matches. Post-fix evidence: `verification/comparison-records.json` and all full-view contact sheets.

## Open questions

No open questions affecting the mirror. The original server has no public robots.txt or sitemap.xml (both return 404); the crawl followed every discovered page and asset reference recursively. Four unique HTML pages were found.

## Implementation checklist

- [x] Preserve all discovered pages and native source assets.
- [x] Localize the exact original font resources.
- [x] Adapt only hostname-dependent homepage URLs.
- [x] Compare complete desktop/mobile pages and focused typography.
- [x] Verify original menu, carousel, video and internal links.
- [x] Confirm resource completeness and original binary checksums.

## Follow-up polish

None requested. Future changes should start from this captured baseline.

final result: passed
