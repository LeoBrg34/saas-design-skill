# Typography Decision Reference

Use this file for semantic type roles, scale, dense SaaS typography, responsive type, numeric/code treatment, and font performance.

## Role before size

Classify text as one of: display, page heading, section heading, card title, body, secondary body, label, caption, button, input value, helper/error, navigation, table header, table cell, metric, code, numeric data, chart label, tooltip, notification.

Start with the smallest sufficient token set:

```text
caption -> label -> body -> title -> heading -> page-title
+ metric/code only when semantically necessary
```

Add a token only when an existing role cannot express the needed hierarchy.

## Practical size ranges

These are product defaults, not laws:

| Context | Primary text | Secondary | Typical page title |
|---|---:|---:|---:|
| Dense operational / analytics / developer | 13–14px | 12–13px | 24–32px |
| Standard SaaS | 14–16px | 13–14px | 28–36px |
| Reading-forward / simple productivity | 16px+ | 14–16px | 28–36px |
| Marketing body | 16–20px | — | display may reach ~40–72px desktop |

Treat 12px as supporting text, not default primary reading text. Routine product H1s do not need marketing-scale display typography.

## Weight and line-height

- Body: usually 400.
- UI emphasis: 500–600.
- Strong headings: 600–700 when the family supports it.
- Avoid light/thin weights for small functional text.
- Single-line UI: roughly 1.2–1.4 line-height ratio.
- Compact multiline: ~1.3–1.45.
- Long body copy: ~1.45–1.6; scripts with taller glyph needs may require more.
- Do not apply one global line-height to all roles.

## Density

Recover density in this order:
1. remove low-value metadata;
2. reduce excessive gaps/padding/row height;
3. simplify container chrome;
4. restructure content;
5. only then make a small, safe type adjustment.

Do not solve “dense SaaS” by making primary UI 11–12px.

## Numeric and technical content

- Use tabular numerals for values compared vertically or changing over time.
- Monospace: code, shell, identifiers, alignment-sensitive technical content.
- Do not make all numbers monospace if the primary family offers tabular figures.
- Do not make an entire developer product monospace merely for aesthetic signaling.

## Brand

Brand modifies expressive typography, not minimum legibility. Apply distinctive family/weight/tracking first to display and headings. Keep controls, tables, body, helper/error, and long reading content conservative unless the brand family is explicitly designed and tested for UI sizes.

Never infer `serif = premium`, `sans = readable`, or a personality trait from font classification alone.

## Responsive/accessibility

- Prefer `rem`/`em` in implementation; px equivalents may remain in specs.
- Fluid `clamp()` is most useful for display/large heading roles, not every label.
- Never make meaningful text depend only on `vw`/`vh`.
- Preserve hierarchy on mobile by compressing scale gaps, not deleting hierarchy.
- Let containers grow when text grows; avoid fixed-height clipping.
- Test 200% text resize/zoom and text-spacing overrides.
- Long reading blocks: roughly 50–75 characters per line; provide a way to stay <=80 when targeting the relevant AAA presentation criterion.
- Avoid sustained all-caps for reading/navigation by default.
- Normal functional text must satisfy contrast requirements, including meaningful secondary/help text.

## Font loading

When shipping web fonts:
- prefer WOFF2;
- load only styles actually used;
- variable fonts help when multiple weights/axes are genuinely needed;
- use `font-display` deliberately so text remains visible;
- metric-match fallbacks to reduce layout shift;
- preload only critical fonts;
- subset scripts/languages only when localization coverage is known.

System fonts are valid when brand value does not justify font cost.

## Failure detectors

- >~7 active size values with near-duplicates -> collapse to semantic tokens.
- >=5 routine product weights -> simplify.
- meaningful normal text <4.5:1 -> fix contrast.
- primary routine UI <=11px -> increase and recover density elsewhere.
- routine page title >40px without expressive reason -> review.
- decorative family in dense tables/forms/settings -> replace in productive roles.
- paragraph width >~80ch -> constrain reading measure.
- `font-size` meaningful content uses only viewport units -> fix.

## Research anchors

Primary evidence: `research/typography.md` §§ 1–8, 11–20. Related: `research/responsive-saas.md` §§ 22, 27, 33–35; `research/design-antipatterns.md` §§ 3, 7, 21.
