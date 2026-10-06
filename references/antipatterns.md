# SaaS Anti-Pattern & Correction Reference

Use this file after generation and during audits. The goal is intentional design, not flatness or stylistic austerity.

## Audit order

1. **Structure** — task priority, information architecture, navigation, density, responsive behavior.
2. **Interaction** — actions, feedback, errors, confirmation, discoverability, overlays.
3. **Visual** — hierarchy, color/type/surfaces/effects, consistency, token drift, template smell.
4. **Accessibility** — keyboard/focus, contrast, targets, semantics, motion, reflow/resize.

## Severity

- **CRITICAL:** blocks task/access, severe accessibility failure, data-loss risk, unusable responsive state.
- **HIGH:** materially harms comprehension/discoverability/efficiency/accessibility.
- **MEDIUM:** meaningful design debt.
- **STYLE:** acceptable when intentional and harmless.

## Common visual/UX failures

Flag the cause, not the ingredient:
- decorative gradient/glass/blur/glow/shadow overload;
- radius inflation / pill-everything;
- cards inside cards; borders around every surface;
- excessive whitespace or giant routine headings;
- everything emphasized / multiple primary CTAs / too many accents;
- density mismatch;
- type-size proliferation / weak secondary text / unbounded prose;
- alignment drift / wrong content width / rectangle-only dashboards;
- hover-only essential actions / ambiguous icon-only controls;
- modal by default / hidden functionality without discoverability;
- confirmation fatigue or generic “Are you sure?” copy;
- desktop merely compressed on mobile;
- arbitrary hiding or destroyed tables;
- color-only meaning / missing focus / undersized targets / ignored reduced motion;
- KPI wallpaper / decorative charts;
- mechanical dark-mode inversion / oversaturated dark accents;
- animation on every interaction / blocking or persistent motion.

## Hard auto-fixes

```text
missing visible focus
-> add consistent focus indicator; never ship outline:none without replacement

required text/non-text contrast fails
-> adjust semantic tokens until it passes

meaning is color-only
-> add text/icon/shape/pattern/position cue

core function is hover-only
-> make it persistent/discoverable or provide keyboard/touch equivalent

ordinary page overflows at 320px
-> reflow or contain essential 2D scrolling locally

nonessential motion survives reduced-motion
-> disable or replace with reduced/instant feedback
```

## Structural correction rules

- Container depth >2 with no semantic/interaction scope -> remove weakest wrapper; use proximity/spacing/divider.
- Unequal actions have equal primary emphasis -> choose one primary; downgrade the rest.
- Modal contains long/repeatable/complex workflow -> move inline, side panel, dedicated page, or full-screen compact flow.
- Dashboard gives equal card weight to unequal states -> rank urgency/actionability and promote exceptions.
- Persistent narrow sidebar destroys main task -> adaptive navigation.

## Confirmation logic

```text
reversible + low/medium impact
-> perform, show status, offer Undo when useful; no blocking confirmation by default

irreversible/high-cost/destructive/legal/financial consequence
-> explicit confirmation naming affected object/count + consequence
-> action-specific button text
-> destructive styling distinct from routine primary action
```

## AI-template smell

No single marker proves “AI-generated”. Detect clusters of unmotivated defaults.

Possible markers: generic purple/blue gradient, gradient headline, centered hero everywhere, sparkle icons, default font/icons with no direction, three equal feature cards, identical rounded cards, border on every surface, glass+glow+navy, giant hero type, dual equal CTAs, fake dashboard rectangles, universal hover-lift, repeated icon+heading+two-lines triplets, symmetric sections despite asymmetric importance, missing empty/loading/error/permission states, one-off style tokens, compressed-desktop mobile.

Heuristic score:

```text
+1 each unmotivated visual-default marker
+2 same card recipe across 3+ unrelated surfaces
+2 product-specific nouns/actions missing above fold
+2 happy path only
+2 no coherent design tokens
+2 mobile is compressed desktop
+2 focus/reduced-motion states absent

0–3  low concern
4–7  review generic/template feel
8–12 redesign pass required
13+  do not ship without structural + visual re-art-direction
```

Never reject solely because a popular font, purple, cards, or rounded corners are used.

## Mandatory question

> Would this interface look obviously AI-generated or like a generic SaaS template?

If yes, first change macrostructure, real product content, hierarchy, typography, or component choice. Do not “fix” genericity with more effects.

## Release gate

Block completion for critical accessibility/task failures. Before calling work “polished”, also fix competing primaries, modal-heavy core workflow, hidden core features, meaningless dashboard hierarchy, unreadable secondary text, unsupported token drift, untested mechanical dark inversion, and AI-smell score >=8 without a documented design direction.

Gradients, glass, pills, large radius, glow, centered short copy, dark mode, or large display type may remain when intentional and harmless.

## Research anchors

Primary evidence: `research/design-antipatterns.md` §§ 0–24. Related: all other research files for domain-specific correction rules.
