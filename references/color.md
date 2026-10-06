# Color Decision Reference

Use this file when choosing or auditing palette architecture, semantic color, dark mode, or data visualization.

## Decision order

1. Inventory semantic roles before hues.
2. Select a neutral scale that can carry most product surfaces/text.
3. Choose brand/action family only after role separation.
4. Build feedback ramps: info, success, warning, danger.
5. Add accents only for replaceable categorization/decorative differentiation.
6. Map roles separately for light and dark.
7. Validate hierarchy and WCAG contrast.
8. Validate brand fit last.

## Token contract

Recommended minimum:

```text
color.bg.canvas
color.bg.surface
color.bg.surface.subtle
color.bg.surface.elevated
color.text.primary
color.text.secondary
color.text.muted
color.text.disabled
color.border.subtle
color.border.default
color.border.strong
color.focus
color.action.primary.{bg,fg,hover,active}
color.action.secondary.{bg,fg}
color.feedback.{info,success,warning,danger}.{bg,fg,border,icon}
color.accent.{family}.{subtle,default,strong}
```

Components request roles, not raw hues. A red brand may still require a distinct destructive treatment if brand/action/danger would otherwise collide.

## Hard rules

- Essential status/action/selection meaning gets a second cue: text, icon, pattern, shape, position, label, or line style.
- Normal functional text: >= 4.5:1. Qualifying large text: >= 3:1.
- Required non-text state/control/graphic information: >= 3:1 against relevant adjacent colors.
- Focus must be visible; do not rely on a tiny color shift.
- One primary visual action per coherent action group when a primary exists.
- Success/warning/danger/info are semantic resources, not decoration.
- Charts need redundant encodings when series/status distinctions matter.

## Contextual color budget

Do not use 60/30/10 as a law. Budget chroma based on semantic pressure:

- **Dense operational/data/risk UI:** neutral-dominant; strong chroma mostly actions, states, selected items, important series.
- **Standard productivity:** neutral foundation + restrained brand/action accents.
- **Marketing:** larger brand-color areas allowed when readability remains stable.
- **High-risk domains:** lower average saturation and stricter semantic separation are useful defaults, not universal color psychology.

High saturation is a scarce resource. Large saturated surfaces generally need more restraint than small accents.

## Dark mode

Preserve roles, not values.
- Do not invert RGB/HSL mechanically.
- Establish depth mainly through surface lightness/tonal levels; shadow alone is weak on dark surfaces.
- Re-tune chroma and brightness of semantic colors for dark backgrounds.
- Pure black is neither mandatory nor forbidden.
- Avoid pure white everywhere on near-black; create text hierarchy without falling below contrast requirements.
- Test the dark theme as a separate product state, including focus, disabled, hover, charts, borders, overlays, and gradients.

## Gradient / glass rule

Keep only when it has a job: brand hero, continuous data encoding, media treatment, or functional layering. If it merely fills empty space, remove it. Test worst-case contrast across gradients.

## Failure detectors

- 3+ unrelated component roles use decorative gradients -> review.
- Accent appears on nearly every interactive element -> reduce competition.
- Primary, link, info, and selected state are indistinguishable -> split roles structurally and/or chromatically.
- Muted functional text fails contrast -> increase contrast; do not use illegibility as hierarchy.
- Red/green-only analytics -> add sign/label/icon/pattern/position.
- “AI purple” selected with no brand/product rationale -> treat as template smell, not a forbidden hue.

## Research anchors

Primary evidence: `research/color-intelligence.md` §§ 2–7, 13–19. Related: `research/brand-personality.md` §§ 2, 7–8; `research/design-antipatterns.md` §§ 1, 7, 10, 21–22.
