# Responsive SaaS Decision Reference

Use this file when adapting complex SaaS across widths/input modes or deciding breakpoints, table behavior, navigation, filters, forms, charts, modals, or panels.

## Core model

```text
task
-> information/action priority
-> minimum usable geometry
-> intrinsic layout
-> local component transformations
-> global shell transformations
-> input-mode adaptations
-> accessibility constraints
-> encode with container/media queries
-> QA across continuous widths
```

Breakpoints are outputs of layout pressure, not inputs to design.

## Query choice

```text
IF decision depends on application-shell space:
    use media/viewport query
ELSE IF reusable component depends on its allocated space:
    use container query
ELSE:
    prefer intrinsic CSS
```

Use `minmax()`, `auto-fit/auto-fill`, content sizing, wrapping, and `clamp()` before adding unnecessary mode switches.

## Provisional shell bands

Only when measurements do not exist yet:

```text
compact: <768px
medium: 768–1023px
wide: >=1024px
very-wide enhancement: >=1440px
```

These are **test bands**, not mandatory breakpoints. Replace them when actual minimum region widths show a better threshold.

Create a breakpoint when a control collides/truncates, component falls below usable width, navigation consumes disproportionate space, side-by-side structure stops helping, touch targets fail, hierarchy must reorder, or an overlay becomes more usable than persistent chrome.

## Content-priority transformation

When space fails:

```text
compress -> wrap -> reorder -> group -> move -> summarize -> disclose -> hide
```

Never hide something only because it does not fit. Hide only when it is redundant/optional and easy to recover.

Mark P0/P1 information/actions before coding:
- task completion;
- current critical state;
- destructive/consequential controls;
- selection/filter/sort state when it changes interpretation;
- navigation context needed to stay oriented.

## Tables / grids

Classify the task first:

| Task | Narrow strategy |
|---|---|
| cross-row/column comparison | keep table; contain horizontal scroll; consider priority/sticky columns carefully |
| browse entities | list/card transformation may be better |
| bulk operations | keep selection + bulk actions + row identity |
| spreadsheet editing | dedicated full-screen/2D workspace |
| scan few priority fields | column-priority table with recoverable hidden fields |

Do not destroy table semantics just to avoid horizontal scrolling when the 2D relationship is the task.

## Navigation

Wide: persistent global + optional contextual navigation when density requires it.
Compact: one primary task region; replace persistent sidebars with drawer/rail/tabs/bottom navigation according to hierarchy/frequency. Preserve current location and access to deep navigation. Do not overload bottom navigation with secondary destinations.

## Filters

On compact layouts, a sheet/drawer is valid if closed state still exposes:
- active filter count;
- important active chips/summary;
- reset/clear;
- distinction between filter and sort;
- preserved state across opening/closing.

## Charts

Allowed simplifications: fewer ticks, moved legend, series toggle, reduced annotation. Never change axes or omit meaning in a way that changes the story without disclosure. Hover details need tap/focus access and accessible alternatives when required.

## Forms and overlays

- Mobile forms usually become one linear column unless a semantic pair strongly benefits from staying together.
- Focus order must match reading/visual order.
- If a modal/panel needs most of a compact viewport, use an intentional full-screen flow rather than a miniature desktop modal.
- Sticky headers/footers must not cover focused controls, validation, or safe areas.

## Input capability

Do not infer touch from width. Use capability queries (`hover`, `pointer`) where appropriate.
- no core hover-only behavior;
- small glyphs may keep small visuals but need larger hit regions;
- primary touch targets should aim for comfortable platform-scale hit areas while still meeting WCAG target-size/spacing requirements;
- gestures/dragging need alternatives when required.

## Accessibility validation

Test:
- ~320 CSS px reflow except essential 2D content;
- 200% text resize/zoom;
- portrait/landscape unless orientation is essential;
- text-spacing overrides;
- keyboard focus under sticky UI;
- reduced motion;
- long localization strings/user-generated names;
- arbitrary widths immediately before/after mode changes.

## Failure detectors

- global page horizontal scroll from ordinary content -> fix;
- desktop sidebar squeezed onto compact layout -> transform navigation;
- font size reduced first to make layout fit -> revert and restructure;
- mobile hides unique action with no discoverability -> restore/move/disclose;
- breakpoint exists only because framework has that token -> remove unless it corresponds to a real mode change;
- desktop/mobile variants duplicate state/business logic -> unify source of truth.

## Research anchors

Primary evidence: `research/responsive-saas.md` §§ 0–4, 9, 21–35, 37. Related: `research/design-antipatterns.md` §§ 6–7, 18–22; `research/typography.md` §§ 6–7.
