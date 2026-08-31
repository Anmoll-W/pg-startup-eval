# UI Standards and Taste Reference

All URLs checked 2026-08-28.

## 1. Nielsen 10 heuristics
All from https://www.nngroup.com/articles/ten-usability-heuristics/

1. Visibility of system status: timely feedback.
2. Match system and real world: user vocabulary.
3. User control and freedom: a marked exit.
4. Consistency and standards: follow convention.
5. Error prevention: prevent, do not report.
6. Recognition rather than recall: keep options visible.
7. Flexibility and efficiency: accelerators for experts.
8. Aesthetic and minimalist design: cut rare content.
9. Recognize, diagnose, recover from errors: plain language, cause, fix.
10. Help and documentation: prefer needing none.

## 2. WCAG 2.2, every screen

- 1.4.3 Contrast, AA: text 4.5:1, large text 3:1. https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
- 1.4.11 Non-text Contrast, AA: components and graphics 3:1. https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
- 2.5.8 Target Size, AA: 24 by 24 CSS px. https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
- 2.4.7 Focus Visible, AA: focus indicator visible. https://www.w3.org/WAI/WCAG22/Understanding/focus-visible.html
- 2.4.11 Focus Not Obscured, AA: focus never entirely hidden. https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum.html
- 1.4.10 Reflow, AA: no 2D scrolling at 320 CSS px. https://www.w3.org/WAI/WCAG22/Understanding/reflow.html
- 1.4.1 Use of Color, A: colour never the only signal. https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html

## 3. Platform guidance

| Topic | Apple HIG | Material 3 |
|---|---|---|
| Targets | control 44x44 pt, minimum 28x28 pt | touch 48x48 dp, pointer 44x44 dp |
| Type | iOS 17 pt default, 11 pt minimum | five roles: display, headline, title, body, label |
| Density | 12 pt bezelled, 24 pt unbezelled | 8 dp between targets |

https://developer.apple.com/design/human-interface-guidelines/accessibility , https://m3.material.io/foundations/designing/structure , https://m3.material.io/styles/typography/overview

## 4. Data-dense screens

- Right-align numbers for scannability. https://m2.material.io/components/data-tables
- Row 52 dp, header 56 dp, minimised cell padding. https://m2.material.io/components/data-tables
- Order rows meaningfully, support sorting. https://m2.material.io/components/data-tables
- Striping and borders hold reader place. https://www.nngroup.com/articles/data-tables/
- tabular-nums equalises figure width. https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric

UNSOURCED, kept out of the checklist: stripes beating rules, any optimal web row height.

## 5. Taste layer

This file carries no owner-specific taste. Owner taste, if present in
`local-context.md`, is binding: read that file before any mode and treat each rule in it
as a P1 finding source, cited as `TASTE/local`, ranked below every WCAG or Nielsen
criterion. When `local-context.md` is absent, sections 1 through 4 and the checklist below
are the complete standard, and checklist lines 10 and 12 through 15 report
`SKIP, no local taste file`.

## 6. Checklist

1. Body text contrast 4.5:1.
2. Large text contrast 3:1.
3. Borders, inputs, focus rings 3:1.
4. Targets at least 24 CSS px.
5. Touch targets at least 44 px.
6. Focus ring visible every tab stop.
7. No focused element hidden by chrome.
8. No horizontal scroll at 320 px.
9. Status shown by text or shape.
10. Exactly two computed font families.
11. Numbers right-aligned, tabular-nums set.
12. Zero em dash, en dash, arrow glyphs.
13. Zero emoji, "Welcome", hero heading.
14. Zero gradient or box-shadow.
15. scrollHeight equals clientHeight, lists excepted.

## 7. Refresh by 2026-11-28

1. https://www.nngroup.com/articles/ten-usability-heuristics/
2. https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
3. https://developer.apple.com/design/human-interface-guidelines/accessibility
4. https://m3.material.io/foundations/designing/structure
5. https://m2.material.io/components/data-tables
