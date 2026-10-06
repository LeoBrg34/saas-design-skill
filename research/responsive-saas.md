# Responsive SaaS — research and decision rules for AI agents

> **Purpose:** enable an AI agent to transform a complex desktop SaaS interface into tablet and mobile layouts intelligently, without treating responsive design as “apply media queries at arbitrary widths”.
>
> **Output type:** research synthesis + decision rules suitable for conversion into an implementation Skill.
>
> **Research date:** 2026-10-06

---

## 0. Executive synthesis

Responsive SaaS design is primarily a **task-preservation and information-priority problem**, not a breakpoint problem.

A strong responsive system answers, in this order:

1. **What task is the user trying to complete?**
2. **Which information and controls are essential to complete that task?**
3. **What is the minimum usable inline size for each component?**
4. **Which relationships must remain spatially visible?**
5. **Which controls can move, collapse, group, or become progressive disclosure?**
6. **Does the interaction model change because input changes from pointer/keyboard to touch?**
7. **Only then:** at which width should the transformation occur?

The central rule for an AI agent should therefore be:

> **Do not choose a breakpoint first and then redesign. Determine the layout failure or task-pressure threshold first, then encode that threshold with a media query or container query.**

Three major design-system breakpoint scales illustrate why there is no universal breakpoint truth:

| System | Representative breakpoints |
|---|---|
| Atlassian | 320, 480, 768, 1024, 1440, 1768 px |
| Carbon | 320, 672, 1056, 1312, 1584 px |
| Material UI | 0, 600, 900, 1200, 1536 px |

The values differ because their layout assumptions differ. The invariant is not the number; the invariant is the **moment the current composition stops being usable**.

### Core principles

1. **Content first, device second.** Design transformations around minimum viable component width, not device names.
2. **Global responsiveness and component responsiveness are different.** Use viewport/media queries for shell-level changes; use container queries for reusable components.
3. **Preserve capability before preserving composition.** The mobile UI may look structurally different while exposing the same important actions.
4. **Mobile is not desktop minus pixels.** It often needs a different navigation model, ordering, disclosure strategy, touch model, and density.
5. **Do not hide merely because something does not fit.** Try compress → wrap → reorder → move → group → disclose before hide.
6. **Touch lowers allowable interaction density even when visual density remains high.**
7. **Tables and dashboards require task-aware transformation.** They cannot be solved by generic stacking.
8. **Horizontal scrolling is acceptable only when the two-dimensional relationship is itself meaningful.**
9. **Responsive transformations must survive zoom, text resizing, localization, long labels, keyboard navigation, and orientation changes.**
10. **A component should respond to the space it actually receives.** Container queries are especially appropriate inside dashboards, panels, split panes, cards, and embedded SaaS modules.

---

# 1. Research model: three evidence levels

This document distinguishes three kinds of evidence.

### Level A — normative / accessibility requirements

Examples: WCAG requirements for reflow, orientation, target size, text resizing, dragging alternatives, focus visibility.

These should become hard constraints in the Skill.

### Level B — official design-system and product patterns

Examples: Atlassian responsive navigation, Carbon tables and chart legends, Shopify container-responsive components, Notion mobile navigation, Vercel mobile bottom navigation.

These are strong implementation patterns, but not universal laws.

### Level C — synthesis / decision heuristics

These are derived rules such as a content-priority score, a table transformation decision tree, or when to prefer a bottom bar over a drawer.

They should be encoded as defaults with exceptions, not treated as standards.

---

# 2. Responsive architecture: viewport, container, and intrinsic behavior

## 2.1 Use viewport responsiveness for the application shell

Viewport-level media queries are most appropriate when the transformation depends on the **whole application frame**, for example:

- persistent side navigation → overlay navigation;
- two application panes → one pane;
- top navigation → bottom navigation;
- global page margins;
- shell-wide density mode;
- large desktop command surface → compact mobile shell.

Atlassian’s current navigation layout is a useful concrete example: side navigation and secondary panels are inline at desktop-scale widths and become collapsed/overlay regions below the desktop range.

## 2.2 Use container responsiveness for reusable components

Container queries should be preferred when the same component may appear:

- in the main canvas;
- in a dashboard tile;
- in a side panel;
- in a modal;
- inside a resizable split pane;
- in an embedded integration.

A `RevenueCard` that is 900 px wide on one page and 320 px wide in a dashboard should respond to **its own inline size**, not to whether the viewport happens to be 1440 px.

Shopify’s current Polaris web-component guidance explicitly supports responsive values based on a parent query container’s inline size. MDN describes the same principle: container queries style descendants based on their container rather than the viewport.

### AI rule

```text
IF a responsive decision is caused by application-shell space
    use a viewport/media query
ELSE IF a responsive decision is caused by local component space
    use a container query
ELSE
    prefer intrinsic CSS before adding a breakpoint
```

## 2.3 Prefer intrinsic layout before conditional layout

A breakpoint is unnecessary when CSS can solve the layout continuously.

Prefer:

```css
grid-template-columns: repeat(auto-fit, minmax(min(100%, 18rem), 1fr));
```

over a sequence of “4 columns / 3 columns / 2 columns / 1 column” breakpoints when the only requirement is “cards should never become narrower than their usable minimum”.

Prefer:

```css
padding-inline: clamp(1rem, 2vw, 2rem);
```

when spacing can vary continuously.

Prefer content-aware sizing (`min-content`, `max-content`, `fit-content()`, `minmax()`) where the component has natural minimums.

### Breakpoint should mean a mode change

Good breakpoint:
- sidebar becomes overlay;
- table becomes list;
- filters move into a sheet;
- chart legend changes position;
- settings switch from split view to drill-in navigation.

Weak breakpoint:
- margin changes from 23 px to 20 px only because a framework has a token at that width.

---

# 3. Breakpoint strategy

## 3.1 Do not infer device type from width

Width alone does not reliably tell the agent whether the user is on:

- a phone in landscape;
- a tablet in split-screen;
- a desktop window snapped to one side;
- a browser at 400% zoom;
- a foldable;
- an embedded webview.

Therefore the terms **desktop / tablet / mobile** in this document describe layout states, not hardware guarantees.

## 3.2 Semantic layout states

The Skill should reason in semantic states:

- **wide** — enough room for persistent navigation + main content + optional detail/context;
- **medium** — enough room for one primary canvas plus limited secondary chrome;
- **compact** — one primary task region at a time;
- **touch-coarse** — input mode requires larger hit areas and no hover dependency.

These states can overlap.

## 3.3 Derive thresholds from required widths

For a layout with:

- 240 px minimum side navigation;
- 640 px minimum primary workspace;
- 320 px optional detail panel;
- 24 px total inter-region gaps;

a three-pane composition has a practical minimum near:

`240 + 640 + 320 + 24 = 1224 px`

The exact breakpoint should be adjusted for page padding, scrollbars, localization, browser zoom, and component internals.

The important point is that the number is derived from **minimum viable regions**, not from “tablet starts at X”.

## 3.4 Default fallback breakpoint map

When an agent has no product-specific measurements yet, use a small number of provisional shell ranges and immediately validate them against content:

```text
compact shell: < 768 px
medium shell: 768–1023 px
wide shell: >= 1024 px
very wide enhancements: >= 1440 px
```

These are **starting test bands, not mandatory implementation values**. Atlassian’s current navigation behavior is close to this shell transition; Carbon and MUI use different exact values.

## 3.5 Breakpoint creation rule

Create a breakpoint only when at least one is true:

- a control becomes truncated or collides;
- the line length becomes clearly excessive;
- a component drops below its minimum usable width;
- scanning becomes significantly worse;
- a navigation region consumes disproportionate space;
- touch targets cannot maintain adequate size/spacing;
- a side-by-side relationship ceases to aid comprehension;
- the information hierarchy needs a new order;
- an overlay becomes more efficient than persistent chrome.

Do **not** create a breakpoint because:
- “this is a common iPhone width”;
- a CSS framework happens to expose a token;
- a mockup exists at 1440 / 768 / 375 only.

---

# 4. Content priority model

Responsive transformation should be driven by explicit priority.

## 4.1 Score each information/action unit

An AI agent can score an item from 0–3 on:

- **task criticality** — required to complete the current task;
- **decision value** — changes the user’s decision;
- **frequency** — used often in this context;
- **state awareness** — communicates important current system state;
- **actionability** — allows an important next action;
- **comparison value** — must be visible simultaneously with other values;
- **redundancy** — duplicated elsewhere;
- **recoverability** — easy to retrieve one tap/click away;
- **space cost** — consumes substantial inline space.

Suggested heuristic:

```text
priority =
  3 * task_criticality
+ 2 * decision_value
+ 2 * actionability
+ 1 * frequency
+ 1 * state_awareness
+ 1 * comparison_value
- 2 * redundancy
- 1 * recoverability
- 1 * space_cost
```

The formula is not a UX standard; it is a practical reasoning scaffold for agents.

## 4.2 Transformation ladder

When space decreases, evaluate in this order:

1. **KEEP** — retain full representation.
2. **COMPRESS** — reduce nonessential padding, decoration, or verbose wording.
3. **WRAP** — allow safe wrapping without changing information structure.
4. **REORDER** — move high-priority content earlier.
5. **GROUP** — combine related controls/content.
6. **MOVE** — relocate secondary content to another region.
7. **SUMMARIZE** — show a concise summary with access to details.
8. **DISCLOSE** — accordion, drawer, sheet, details page, overflow menu.
9. **HIDE** — only if optional/redundant and not required for task completion.

### Hard rule

Do not hide:
- validation errors;
- save/submit/destructive actions required for the task;
- status that materially changes the meaning of the page;
- active filters without another visible indication;
- navigation needed to exit the current flow;
- information required to interpret a chart or decision;
- functionality solely because it depends on hover on desktop.

---

# 5. Pattern: application grid and fluid layout

## DESKTOP

- Use a structured main grid for relationships that benefit from alignment.
- 12- or 16-column systems are implementation tools, not goals.
- Let dashboards with natural content widths stop growing; do not stretch every card indefinitely.
- Keep readable content regions capped rather than filling ultrawide screens.
- Allow workspace-style canvases (boards, timelines, editors) to be more fluid than settings or report pages.

## TABLET

- Reduce simultaneous regions before shrinking their internals below usable widths.
- Convert three regions → two, or two → one + overlay.
- Reduce outer margins before shrinking control hit areas.
- Maintain meaningful paired content only when both sides remain scannable.

## MOBILE

- Prefer one primary layout flow.
- Edge padding usually becomes smaller, but should remain consistent.
- Full-bleed is appropriate for data regions that benefit from width; text/form content can retain inset padding.
- Avoid arbitrary nested cards that waste horizontal space.

## RATIONALE

Atlassian explicitly distinguishes content that should use fluid grids (e.g. expansive boards) from structured content whose relationships degrade when stretched too far. Carbon also distinguishes fluid, fixed, and hybrid behavior.

## EXCEPTIONS

- Whiteboards, timelines, IDE-like canvases, maps and spreadsheets may intentionally remain wider than the viewport and use controlled panning/scrolling.
- Visual editors may preserve multi-pane modes in landscape tablet.

## FAILURE MODES

- Treating every wide monitor as a reason to expand every component.
- Keeping desktop page margins on 375 px mobile.
- Nesting a 16 px padded card inside another 16 px padded card inside a 16 px page gutter, leaving little usable space.
- Assuming the grid breakpoint should change because a sidebar opened; a component’s actual available space may be the better trigger.

---

# 6. Pattern: sidebars

## DESKTOP

- Persistent sidebar is appropriate for frequent, high-level navigation.
- Resizable sidebar is useful when labels, tree depth, or user-created names vary.
- A collapsed icon rail can be offered as a user preference or intermediate mode if icons are unambiguous and labels remain accessible.

## TABLET

Choose between:

1. **collapsed rail** when:
   - destinations are few and well-known;
   - icons have stable meaning;
   - retaining fast switching matters.

2. **overlay drawer** when:
   - navigation is deep/hierarchical;
   - labels are necessary;
   - primary content needs nearly full width.

Atlassian’s layout collapses side navigation to an overlay below desktop-scale ranges.

## MOBILE

Do not automatically convert every sidebar into a hamburger drawer.

Use:

- **bottom navigation** for roughly 3–5 very frequent, stable top-level destinations;
- **title-bar/menu drawer** for deep hierarchy or many destinations;
- **dedicated home/navigation screen** for complex tree navigation;
- **search-first navigation** where users mostly jump directly to entities.

Real product evidence:
- Notion mobile uses a persistent bottom navigation for Home, Search, Inbox, and creation.
- Vercel’s 2026 dashboard redesign introduced a floating bottom bar optimized for one-handed mobile use.
- Shopify app navigation appears in the left sidebar on desktop and in a title-bar dropdown on Shopify mobile.

## RATIONALE

Mobile navigation should optimize frequent switching and thumb reach, while secondary hierarchy can move behind disclosure.

## EXCEPTIONS

- Admin consoles with dozens of equally important modules may be better served by a searchable drawer than a bottom bar.
- A workflow application with a single core screen may need no persistent navigation at all.

## FAILURE MODES

- 8–10 bottom-nav items.
- Icon-only rail with obscure icons.
- Hamburger drawer that hides the only high-frequency destinations.
- Recreating the entire desktop nested tree at 320 px.
- Losing current-location context when the sidebar disappears.

---

# 7. Pattern: top navigation and global navigation

## DESKTOP

- Brand/workspace switcher, primary destinations, search, global create, help, and account controls can coexist.
- Keep the dominant navigation model stable; avoid simultaneous competing top nav + full side nav unless they represent different levels.

## TABLET

- Remove low-frequency text labels before removing important functions.
- Combine secondary actions into an overflow menu.
- Search may collapse from an expanded input to an icon-triggered overlay.
- Workspace/account switchers may become compact.

## MOBILE

- Preserve a visible route back and clear page title.
- Move primary recurring destinations to bottom navigation when appropriate.
- Put infrequent global actions behind a menu.
- Do not depend on breadcrumbs alone as the mobile back model.

## RATIONALE

The smaller viewport cannot support equal visual weight for all global functions. Navigation should reflect frequency and hierarchy.

## EXCEPTIONS

- Browser-like or editor-like SaaS may use a compact toolbar rather than consumer-style bottom tabs.

## FAILURE MODES

- Shrinking all desktop nav labels until unreadable.
- Keeping a 72 px desktop header plus a second 56 px mobile toolbar, wasting vertical space.
- Hiding “Create” or another core action inside a low-discoverability overflow without alternative access.

---

# 8. Pattern: dashboards

## DESKTOP

- Use a hierarchy, not a uniform card grid.
- Place the most decision-critical KPIs and controls first.
- Large analytical visualizations should receive more area than secondary status cards.
- Keep related filters close to the dashboard or visualization they affect.

Carbon’s dashboard guidance emphasizes prioritizing data by importance and limiting non-essential metrics.

## TABLET

- Typically move from multi-column analytical grid to 2 columns or asymmetric 2-column composition.
- Promote important wide charts to full row.
- Reorder rather than merely let CSS source order accidentally determine stacking.
- Reduce simultaneous secondary metrics.

## MOBILE

- Use a deliberate single-column sequence.
- Put the summary / KPI / primary next action first.
- Convert groups of small KPI cards into:
  - horizontal swipe/scroll only if each card is independent and discovery is clear; or
  - compact list/metric rows; or
  - one featured metric + “View all”.
- Keep charts large enough to interpret; do not squeeze four charts into two tiny columns.
- Move detailed exploration to dedicated chart/detail screens where needed.

## RATIONALE

A dashboard is an information hierarchy. Mobile forces that hierarchy to become explicit.

## EXCEPTIONS

- Operations dashboards used primarily in landscape tablets may preserve denser grids.
- Monitoring walls are not mobile-first tasks; provide a mobile summary rather than reproducing the wall.

## FAILURE MODES

- CSS auto-stacking produces low-priority cards before critical ones.
- Every widget gets equal height after stacking.
- 4-up KPI row becomes four tiny 80 px cards.
- Charts become unreadable but remain “technically responsive”.

---

# 9. Pattern: tables and data grids

This is one of the highest-risk areas for arbitrary responsive behavior.

## 9.1 First identify the table task

Ask:

```text
Is the user primarily:
A. comparing values across columns?
B. browsing entities/records?
C. performing bulk actions?
D. editing many cells?
E. scanning status?
F. reading a report where two-dimensional alignment is essential?
```

The answer determines the mobile transformation.

## DESKTOP

- Use the full table/data-grid model.
- Support sorting, filtering, selection, resizable columns, bulk actions, density controls where the task needs them.
- Give data tables significant width.
- Row actions may appear on hover only if they also appear on focus and are made persistent for touch.

Carbon explicitly makes row overflow actions persistent on touch devices even when desktop behavior uses hover.

## TABLET

Use a combination of:
- lower-priority column hiding;
- column priority;
- wrapping;
- horizontal scroll;
- sticky identifier column;
- expandable row details;
- condensed toolbar;
- responsive filter region.

Do not remove sort/filter state.

## MOBILE

Choose one of four modes.

### Mode A — responsive list/card transformation

Best for **entity browsing**.

Each row becomes a vertical item with:
- primary identifier;
- 1–3 high-priority attributes;
- status;
- primary/overflow action;
- optional expandable details.

Shopify’s current table pattern explicitly supports a narrow list layout. MUI X Data Grid also provides a responsive list-view mode.

### Mode B — horizontally scrollable table

Best when **cross-column comparison is essential**.

Requirements:
- visible overflow cue;
- sticky primary identifier when feasible;
- no page-level horizontal scroll—contain it within the data region;
- preserve column headers;
- make touch scrolling reliable;
- do not shrink text to avoid scrolling.

### Mode C — column-priority table

Best when:
- only a few attributes are critical;
- remaining fields are genuinely secondary.

Show critical columns; move the rest into an expandable detail row or row detail screen.

### Mode D — dedicated full-screen data workspace

Best for:
- spreadsheet-like editing;
- financial matrices;
- complex query builders;
- high-density operational grids.

Mobile may provide a simplified overview plus an “Open data view” screen rather than pretending the desktop grid can collapse cleanly.

## RATIONALE

Tables encode relationships. Turning every table into cards can destroy comparison; forcing every table to scroll can make entity browsing unnecessarily difficult.

## EXCEPTIONS

- Tiny two-column key/value tables can often stack naturally.
- Data matrices where x/y positions have meaning should remain two-dimensional.

## FAILURE MODES

- Hiding columns with no way to retrieve the values.
- Putting the only sort control in a header that disappears in list mode. Shopify specifically warns against this.
- Losing select-all/bulk-action capability when the narrow layout removes the header.
- Converting to cards and repeating ten field labels per row, creating extreme vertical bloat.
- Keeping hover-only actions on touch.
- Using page-wide horizontal scrolling.
- Changing row order or data semantics between breakpoints.

---

# 10. Pattern: cards

## DESKTOP

- Cards can form multi-column grids when items are peers.
- Set a minimum card width based on content.
- Use Grid with `auto-fit/auto-fill + minmax()` for intrinsically responsive collections.
- Avoid stretching content-heavy cards to absurd widths.

## TABLET

- Let column count be determined by minimum viable card width.
- Featured cards may span full width.
- If a card has internal horizontal regions, use a container query to transform the card itself.

## MOBILE

- Usually one card per row.
- Consider removing redundant card chrome when cards are simply list items.
- Reorder card metadata by priority.
- Move tertiary actions into an overflow menu while keeping the primary action visible.

## RATIONALE

A card is a container pattern, not a mandate for borders and padding at every size.

## EXCEPTIONS

- Small stat tiles can remain 2-up if each retains adequate readability and touch targets.
- Media galleries may remain multi-column if thumbnails are the primary content.

## FAILURE MODES

- Arbitrary `grid-template-columns: repeat(4, 1fr)` plus breakpoint patches.
- Excessive nested card padding on mobile.
- Every card becomes identical height even though information importance differs.
- Hover-revealed actions disappear on touch.

---

# 11. Pattern: charts and data visualization

## DESKTOP

- Show full labels, axes, relevant legend, hover details, zoom/filter controls when useful.
- Preserve sufficient visual space for interpretation.
- Use linked chart interactions consistently in exploratory dashboards.

## TABLET

- Reduce tick density before reducing text size below comfortable reading.
- Move a right-side legend to top/bottom.
- Stack legend entries if needed.
- Allow secondary controls to collapse.
- Consider showing fewer simultaneous small multiples.

## MOBILE

Apply the following transformation order:

1. resize while preserving aspect and legibility;
2. reduce nonessential decoration/gridlines;
3. reduce tick frequency;
4. abbreviate labels only when meaning remains clear;
5. reposition or stack legend;
6. show fewer simultaneous series when the task allows;
7. provide series toggles;
8. move detailed controls into a sheet;
9. use a dedicated detail screen for complex exploration;
10. use controlled horizontal scrolling for time-series or dense x-axis data when preserving scale is more important than fitting everything at once.

Carbon’s legend guidance explicitly allows a mobile legend to revert to a stack, or—when necessary—to be hidden behind a visible “View legends” control. Carbon warns that simply hiding legends reduces clarity/accessibility.

### Touch behavior

- Hover tooltip must have tap/focus equivalent.
- Data points should not require pixel-perfect tapping.
- Drag-to-zoom/brush must have a non-drag alternative when required by WCAG 2.5.7.
- Provide a textual summary and, for decision-critical data, an accessible data representation.

## RATIONALE

Responsive charting is semantic compression. The objective is to preserve the insight, not every decorative mark.

## EXCEPTIONS

- Maps, timelines, heatmaps, network diagrams and financial charts may require panning/zooming.
- A complex chart may be replaced by a summary on the dashboard but remain fully available on a detail screen.

## FAILURE MODES

- Shrinking a 900 px chart to 300 px with identical ticks, legend and labels.
- Removing the legend with no alternative.
- Tooltips only on hover.
- Changing axis scale between desktop and mobile in a way that changes perceived meaning.
- Cropping chart labels.
- Replacing a comparison chart with a single KPI and losing the decision context.

---

# 12. Pattern: filters

## DESKTOP

- High-frequency filters can live inline above the data or in a side filter panel.
- Active filters should remain visible.
- Search + sort + filters should share coherent state.

## TABLET

- Keep the most important quick filters inline.
- Collapse secondary filters into a popover/drawer.
- Use removable chips for applied filters.
- Let filter controls wrap rather than collide.

Shopify’s current index-table guidance demonstrates responsive filter controls and active removable chips, and explicitly keeps filter/sort/pagination state coordinated.

## MOBILE

Recommended default:
- visible `Filter` button with active count;
- optional visible high-frequency single filter;
- full-height sheet/drawer for the complete filter set;
- active filter chips/summary outside the sheet;
- explicit Apply/Clear when filters are expensive or staged;
- live update is acceptable when results update quickly and context is preserved.

## RATIONALE

Mobile needs to preserve the **state of filtering** without dedicating half the screen to filter controls.

## EXCEPTIONS

- Search-centric products may expose filter tokens directly in the search field.
- Very small filter sets (e.g. 2 segmented choices) can remain inline.

## FAILURE MODES

- Applied filters become invisible after closing the drawer.
- A badge says “3 filters” but there is no easy reset.
- Filter drawer loses unsaved selections when dismissed accidentally.
- Desktop left rail remains 280 px on a 768 px tablet.
- Sort is incorrectly treated as a filter and becomes undiscoverable.

---

# 13. Pattern: forms

## DESKTOP

- Prefer single-column forms for cognitively complex input.
- Use two columns only when fields have a strong semantic relationship and their order remains obvious.
- Size short fields according to expected input when useful; do not make every field 100% width solely for aesthetics.
- Keep help/error text adjacent to its field.

## TABLET

- Collapse weak two-column groups to one column.
- Preserve strong pairs such as city/state only if both remain comfortable.
- Move secondary help panels below the form or into contextual disclosure.

## MOBILE

- Default to one-column flow.
- Keep labels above controls.
- Use correct input types and autocomplete semantics.
- Make primary actions easy to reach.
- If actions are sticky, ensure they do not obscure focused fields or error messages.
- Break very long administrative forms into meaningful sections/steps rather than one endless compressed page.

## RATIONALE

Forms need clear reading and focus order. A desktop two-column form often becomes a confusing zigzag under narrow width or text enlargement.

## EXCEPTIONS

- Very small paired values (month/year, min/max) can remain side-by-side if accessible and large enough.
- Dense expert tools may preserve compact multi-field rows on tablet landscape.

## FAILURE MODES

- Placeholder-only labels.
- Two-column DOM/source order that reads incorrectly when visually stacked.
- Fixed-height fields clipping 200% text.
- Error messages off-screen while submit remains sticky.
- Keyboard opening causes primary action to cover the current input.

---

# 14. Pattern: modals

## DESKTOP

- Use a modal for a focused, bounded task.
- Size it according to content; avoid full-screen by default.
- If content becomes a mini-page with deep navigation, it probably should be a page.

## TABLET

- Let the modal consume a larger percentage of viewport width.
- Keep adequate margins.
- Complex content can approach full-screen when needed.

## MOBILE

Choose:
- **center/bottom confirmation sheet** for short, simple decisions;
- **full-screen modal** for focused multi-step tasks;
- **dedicated page** for long forms, dense tables, or tasks needing navigation/context.

Carbon’s modal scale becomes progressively wider as viewport width decreases and reaches 100% width at its smallest breakpoint. USWDS advises moving content to its own page when modal content becomes too large or interactive.

## RATIONALE

On small screens, the background context provided by a centered floating rectangle contributes little, while the reduced content area creates serious usability cost.

## EXCEPTIONS

- A tiny destructive confirmation can remain a compact dialog.
- OS-like bottom sheets can be excellent for short mobile choice sets.

## FAILURE MODES

- Desktop 640 px fixed-width modal overflowing a 375 px viewport.
- Nested scrolling inside a modal inside the page.
- Modal containing a full data grid.
- Dialog close/action controls become obscured by the virtual keyboard.
- Stacking modal on top of another modal/drawer without a clear focus model.

---

# 15. Pattern: drawers and side panels

## DESKTOP

- Inline detail panel is effective for master-detail workflows when the main list remains usable.
- Persistent secondary panels are appropriate when context must remain visible.
- Resizable panels can support expert workflows.

## TABLET

- Convert secondary panel to overlay if main content would fall below its minimum width.
- Preserve state when opening/closing.
- Consider mutually exclusive panes rather than squeezing both.

## MOBILE

- Use full-width overlay/detail route for substantial content.
- Use a bottom sheet for short contextual controls.
- Preserve a clear return path to the originating item/list.
- Keep commit/cancel actions reachable; sticky footer may be appropriate.

## RATIONALE

The purpose of a panel is contextual adjacency. Once the main view and panel cannot both remain useful, adjacency no longer justifies the space cost.

## EXCEPTIONS

- Landscape tablets may support split view.
- Small inspection panels containing only 2–3 fields may remain partial-width on large phones.

## FAILURE MODES

- 320 px panel leaves 40 px of main content visible.
- Closing/reopening loses edits.
- Overlay panel traps navigation state.
- Sticky panel footer hides focused fields.

---

# 16. Pattern: command palettes

## DESKTOP

- Centered command/search overlay is appropriate.
- Keyboard shortcut is a high-efficiency accelerator.
- Show recent actions/results and support keyboard navigation.

## TABLET

- Larger modal/sheet with visible trigger.
- Keyboard shortcut can remain for hardware keyboards but must not be the only access method.

## MOBILE

Transform from “keyboard command palette” to **full-screen search/action surface**:
- visible search/action trigger;
- recent destinations/actions;
- large touch rows;
- grouped results;
- no dependence on modifier-key shortcuts;
- dismiss/back behavior matching mobile navigation expectations.

Notion is a useful real example: desktop search supports `cmd/ctrl + K/P`, while mobile provides Search as a persistent navigation destination.

## RATIONALE

The concept to preserve is “fast universal access”, not the desktop floating rectangle or keyboard shortcut.

## EXCEPTIONS

- Tablet with hardware keyboard can expose both touch and keyboard command modes.

## FAILURE MODES

- Command palette exists on mobile but can only be opened by keyboard.
- Tiny action rows optimized for cursor precision.
- Search results rely on hover preview.
- Full-screen mobile palette has no clear back/dismiss behavior.

---

# 17. Pattern: search

## DESKTOP

- Search can be persistently visible in global chrome if it is high frequency.
- Rich result panes can expose categories, filters and previews simultaneously.

## TABLET

- Search field may collapse into an icon-triggered overlay if width is scarce.
- Maintain recent searches and filters.
- Use tabs/segmented result types when side-by-side categories no longer fit.

## MOBILE

- High-frequency product search should get a first-class entry point, often a tab or clearly visible action.
- Use full-width input and large results.
- Filters can move into a sheet.
- Result type switching should remain accessible without tiny controls.

Slack’s current search differs by platform: desktop exposes richer side/category presentation, while mobile uses touch-oriented result type controls and filter actions.

## RATIONALE

Search often becomes **more**, not less, important when hierarchical navigation is compressed.

## EXCEPTIONS

- Apps with only a few entities may not need global mobile search.

## FAILURE MODES

- Search icon has no label/accessible name.
- Mobile search loses filters available on desktop even though they are critical.
- Keyboard shortcut is documented as the primary entry.
- Search result preview requires hover.

---

# 18. Pattern: settings pages

## DESKTOP

- Side navigation + content pane works well for many settings categories.
- Large forms should be grouped into sections.
- Save behavior should be clear: per field, per section, or whole page.

## TABLET

- Narrower sidebar or category list can remain if main content stays usable.
- Otherwise move to a list/detail model.
- Contextual explanatory content can move below the setting.

## MOBILE

Use a drill-in hierarchy:

```text
Settings
  → Account
      → Email
      → Password
  → Workspace
  → Notifications
```

- One category per screen when content is substantial.
- Keep current category title and back path explicit.
- Preserve unsaved state if navigating to nested settings.
- Use search for very large settings taxonomies.

## RATIONALE

A desktop settings sidebar is usually a category index. On mobile, that index works better as navigation than as permanently visible chrome.

## EXCEPTIONS

- Tiny setting sets can remain one page with anchored sections.
- Some native mobile products intentionally limit advanced admin/security operations; however a responsive web SaaS should not remove essential account control solely for convenience.

## FAILURE MODES

- 40% of mobile width consumed by category nav.
- Every desktop section becomes an accordion, creating a 30-item accordion maze.
- Unsaved changes vanish when drilling between settings.
- Desktop-only setting is hidden without explanation or alternative.

---

# 19. Pattern: pricing pages

Pricing has two distinct responsive problems:

1. **plan selection**;
2. **feature comparison**.

They should not be solved identically.

## DESKTOP

- Plan cards can be side-by-side.
- Price, audience, primary differentiators and CTA must be visible without entering the comparison matrix.
- Detailed comparison can use a table/matrix below.

Current Notion and Slack pricing pages both present multiple plans plus deeper feature comparison.

## TABLET

- Use 2-up plan cards or horizontally scrollable snap cards only if plan identity remains obvious.
- Comparison matrix can reduce nonessential columns or become plan-selectable.
- Keep plan names aligned with compared values.

## MOBILE

### Plan selection
- Stack plans vertically, or use a deliberate plan selector if there are many.
- Keep plan name, price, billing basis, key differentiators, CTA and recommended badge together.

### Feature comparison
Choose:
- feature category → rows → values per plan;
- plan selector + feature list;
- horizontally scrollable matrix with sticky feature-name column when direct cross-plan comparison is essential.

Accordions are appropriate for feature categories, not for hiding the basic price/CTA.

## RATIONALE

The mobile user must still answer two questions quickly:
- “Which plan is for me?”
- “What do I gain by moving to the next plan?”

## EXCEPTIONS

- Two-plan products can keep a compact direct comparison.
- Enterprise-heavy products may emphasize contact/demo rather than exhaustive mobile matrix.

## FAILURE MODES

- Each plan card contains the entire 80-feature matrix.
- Feature matrix shrunk until text is microscopic.
- Recommended plan loses its context after stacking.
- Monthly/annual billing toggle scrolls off and users forget which prices they are comparing.
- Sticky plan headers obscure focus at zoom.

---

# 20. Pattern: landing pages

## DESKTOP

- Rich hero compositions, product visuals, comparison sections and multi-column proof can coexist.
- Decorative media can support positioning as long as the message and CTA remain clear.

## TABLET

- Reduce decorative competition.
- Collapse complex 2-column feature sections when one side falls below a readable width.
- Keep screenshots large enough to communicate actual product value.

## MOBILE

- One dominant headline/message.
- Primary CTA early.
- Secondary CTA remains available but visually subordinate.
- Product proof should follow quickly; do not force users through large decorative hero media first.
- Stack feature sections in deliberate narrative order.
- Reduce or defer heavy autoplay/decorative media.
- Logos/testimonials can become compact grids or controlled carousels only when all items remain reachable.
- Pricing teaser should preserve real decision information.

## RATIONALE

Landing-page responsiveness is narrative prioritization. The desktop composition often uses simultaneous text + visual proof; mobile converts that into a sequence.

## EXCEPTIONS

- Visual products may legitimately prioritize a product demo/image directly after a short headline.

## FAILURE MODES

- Desktop split hero simply shrinks to two 50% columns on 390 px.
- Screenshot becomes illegible decoration.
- CTA appears after several screens of media.
- Content order follows DOM convenience rather than persuasion/understanding.
- Mobile performance is degraded by desktop-scale videos/images.

---

# 21. TOUCH

## 21.1 Target size

WCAG 2.2 SC 2.5.8 requires pointer targets to be at least **24 × 24 CSS px**, with defined exceptions including sufficient spacing.

For comfortable touch design, platform guidance is larger:
- Apple generally recommends at least **44 × 44 pt** hit regions.
- Android accessibility guidance recommends **48 × 48 dp** touch targets.

For a web SaaS Skill:

```text
hard accessibility floor: WCAG 24×24 CSS px or qualifying spacing exception
default touch design target: approximately 44–48 CSS px interaction region
```

The second line is a design recommendation, not a WCAG conformance equivalence.

## 21.2 Visual size != hit size

An icon can remain visually 20–24 px while its button/hit region is 44–48 px.

Do not enlarge every icon to 48 px.

## 21.3 Spacing

On compact touch interfaces:
- reduce decorative/page spacing before reducing hit areas;
- separate adjacent destructive and primary actions;
- keep icon buttons sufficiently spaced even if the icon glyph is small.

## 21.4 Hover

Hover must be an enhancement, not the only access path.

Use hover for:
- preview;
- affordance reinforcement;
- tooltip duplication;
- nonessential animation.

Do not use hover as the only way to reveal:
- row actions;
- edit controls;
- critical labels;
- navigation;
- validation/help required to use the control.

Notion’s mobile documentation explicitly notes that mobile has no hover states and exposes controls such as `•••` and `+` that are hover-revealed on desktop.

Prefer CSS capability queries:

```css
@media (hover: hover) and (pointer: fine) {
  /* hover enhancement */
}

@media (hover: none), (pointer: coarse) {
  /* persistent/touch-friendly affordance */
}
```

Do not use user-agent sniffing as the primary interaction decision.

## 21.5 Gestures

WCAG 2.5.7 requires an alternative to dragging unless dragging is essential.

Therefore:
- reorder by drag → also expose move controls/menu;
- swipe to delete → also expose delete action;
- drag chart range → also expose date/range controls;
- swipe carousel → also expose buttons/dots and standard scrolling.

---

# 22. RESPONSIVE TYPOGRAPHY

Responsive type should preserve **readability, hierarchy and zoom resilience**, not create dramatic viewport-dependent scaling.

## 22.1 Body text

Prefer stable `rem`-based body text.

Body text rarely needs aggressive fluid scaling between phone and desktop. Large viewport-only formulas create accessibility and readability risks.

WCAG 1.4.4 requires text to be resizable to 200% without loss of content/functionality. W3C lists incorrect viewport-unit-only resizing as a known failure pattern.

## 22.2 Headings

Headings can use bounded fluid sizing:

```css
font-size: clamp(1.75rem, 1.3rem + 2vw, 3.5rem);
```

The minimum must remain useful on mobile; the maximum prevents huge text on ultrawide screens.

## 22.3 Hierarchy compression

As width decreases:
- reduce the ratio between display/H1 and body before reducing body text;
- avoid six visually distinct heading levels on a small screen;
- preserve semantic heading levels even when visual sizes converge.

## 22.4 Line length

Keep prose constrained even on wide SaaS pages.

A practical target is roughly **45–80 characters per line**, with context-specific exceptions. W3C’s text-resizing techniques include keeping lines around 80 characters or fewer as an advisory technique.

## 22.5 Truncation

Truncate:
- known repetitive identifiers;
- secondary metadata;
- long user-generated names when the full value remains available.

Do not truncate:
- validation;
- irreversible action labels;
- primary page titles without alternate access;
- critical table values;
- plan/pricing meaning.

---

# 23. RESPONSIVE SPACING

Responsive spacing should not be a global “multiply everything by 0.75 on mobile”.

Separate:

- **page spacing**;
- **section spacing**;
- **component spacing**;
- **control hit-area spacing**.

## 23.1 Recommended behavior

As width decreases:

```text
page gutters: decrease
large section gaps: decrease moderately
card internal padding: may decrease
text-to-label spacing: mostly stable
touch hit areas: stable or increase
adjacent interactive separation: stable or increase
```

Example:

```css
.page {
  padding-inline: clamp(1rem, 3vw, 2rem);
}

.section {
  margin-block: clamp(1.5rem, 4vw, 4rem);
}
```

## 23.2 Failure mode

A common bad mobile optimization is to compress every dimension, resulting in:
- 12 px buttons;
- tightly packed icon rows;
- poor touch accuracy;
- visually stressful dense screens.

---

# 24. RESPONSIVE DENSITY

Density has at least three separate dimensions:

1. **information density** — how much information is visible;
2. **visual density** — padding/whitespace/decoration;
3. **interaction density** — number and proximity of interactive targets.

Desktop can support high interaction density because mouse/trackpad pointing is precise.

Mobile can still support high information density, but interaction targets should become more spacious.

### Example

A desktop data row can show:

`Name | Owner | Status | Updated | Revenue | Region | Actions`

Mobile might show:

```text
Name                    Status
Owner · Revenue
Updated
[overflow action target 44–48px]
```

Information is condensed and reordered; the interaction target is not made smaller.

---

# 25. MODERN CSS EVALUATION

## CSS Grid

### Use for
- 2D page layouts;
- dashboards;
- card collections;
- form groups;
- aligned comparison areas.

### Strength
Grid expresses relationships between rows and columns and works well with intrinsic sizing.

### Prefer
```css
repeat(auto-fit, minmax(...))
```
when the number of columns should emerge from available space.

### Avoid
forcing every layout into a 12-column abstraction when normal flow or Flexbox is simpler.

---

## Flexbox

### Use for
- toolbars;
- inline control groups;
- button rows;
- simple 1D arrangements;
- wrapping filter/action groups.

### Strength
Excellent for distributing and wrapping items in one dimension.

### Failure mode
Using Flexbox for a complex 2D dashboard and patching alignment with widths/margins.

---

## `minmax()`

High value for intrinsic SaaS layouts.

Use when a region should:
- never become smaller than a usable minimum;
- otherwise absorb remaining space.

Example:

```css
grid-template-columns:
  minmax(16rem, 22rem)
  minmax(0, 1fr);
```

The `minmax(0, 1fr)` pattern is especially useful to prevent long content from forcing overflow in flexible grid tracks.

---

## `clamp()`

Use for **bounded fluid values**:
- page gutters;
- display typography;
- section spacing;
- occasional component sizing.

Avoid using `clamp()` to disguise a component that actually needs a structural mode change.

If a sidebar needs to become an overlay, `clamp()` is not the solution.

---

## Container queries

### Strongly recommended for
- cards with horizontal/vertical variants;
- dashboard tiles;
- data modules embedded in different columns;
- filter/toolbars;
- components inside resizable panels;
- reusable form sections;
- responsive table/list components.

### Use media queries instead when
- the global shell changes;
- user preference is queried (`prefers-reduced-motion`, etc.);
- behavior depends on input/hover capability.

### AI rule

```text
component reused in multiple parent widths?
    YES → container query candidate
    NO  → intrinsic layout first, media query if shell-dependent
```

---

## Intrinsic layouts

Prefer layouts that naturally adapt via:
- `min-content`;
- `max-content`;
- `fit-content()`;
- `minmax()`;
- wrapping;
- `auto-fit`;
- normal flow.

This reduces brittle breakpoint counts.

---

## Logical properties

Prefer:
- `padding-inline`;
- `margin-inline`;
- `inset-inline-start/end`;
- `inline-size`;
- `block-size`.

over hard-coded left/right where layout should follow language direction.

This improves RTL/localization resilience and aligns with modern CSS’s inline/block model.

---

# 26. MOBILE SaaS: squeezed desktop vs genuinely adapted interface

## Squeezed desktop

Symptoms:

- desktop sidebar merely becomes narrower;
- 6-column tables use 10 px text;
- page-level horizontal scroll;
- hover interactions disappear;
- 2-column forms remain 2 columns;
- dashboard widgets simply become miniature;
- every desktop control is preserved inline;
- command palette still assumes keyboard shortcuts;
- modal remains a small floating rectangle;
- main content order is accidental CSS wrap order;
- navigation uses a hamburger regardless of task frequency.

## Genuinely adapted mobile SaaS

Characteristics:

- one primary task region at a time;
- explicit mobile navigation model;
- content order matches priority;
- table/list transformation chosen by task;
- visible active filter state;
- touch targets expanded;
- hover-only actions become persistent or menu-based;
- complex secondary controls move to sheets/detail screens;
- charts simplify while preserving meaning;
- settings use drill-in hierarchy;
- search becomes a first-class navigation mechanism where useful;
- dense expert workflows may get a dedicated full-screen mobile mode instead of a fake miniature desktop.

### Key principle

> **Feature parity does not require layout parity.**

The same capability may exist through a different interaction sequence on mobile.

---

# 27. ACCESSIBILITY REQUIREMENTS RELEVANT TO RESPONSIVE SaaS

## 27.1 Orientation — WCAG 1.3.4 (AA)

Do not force portrait or landscape unless orientation is essential.

A message saying “rotate your device” instead of supporting the current orientation is a known failure pattern.

### AI rule
Never lock SaaS web UI to landscape just because the desktop composition is wide.

---

## 27.2 Resize Text — WCAG 1.4.4 (AA)

Text must be resizable to 200% without loss of content or functionality.

### Test
- 200% text/zoom scenarios;
- labels;
- button text;
- tabs;
- form fields;
- sticky toolbars;
- modal titles/actions.

---

## 27.3 Reflow — WCAG 1.4.10 (AA)

Content should be usable without loss of information/functionality and without two-dimensional page scrolling at an equivalent width of **320 CSS px** for vertically scrolling content, except where a two-dimensional layout is essential.

W3C explicitly notes that responsive relocation of content is acceptable if information/functionality remains accessible.

### SaaS implication

A data table, map, diagram or spreadsheet may qualify as content whose meaning requires two dimensions, but the **whole page** should not become a two-dimensional scroll surface because one component is wide.

Contain overflow inside the relevant component.

---

## 27.4 Text Spacing — WCAG 1.4.12 (AA)

No loss of content/functionality when users override text spacing to the WCAG test values.

### Responsive implication
Avoid:
- fixed-height tabs/buttons that clip;
- rigid card heights;
- labels overlaid on controls;
- fixed-height nav rows that cannot grow.

---

## 27.5 Focus not obscured — WCAG 2.4.11 (AA)

Sticky headers, bottom action bars, cookie banners and mobile bottom navigation must not entirely hide the focused component.

W3C documents `scroll-padding` as one technique.

### SaaS implication
Test keyboard focus with:
- sticky data-table headers;
- sticky mobile save bar;
- floating support/chat widgets;
- bottom navigation;
- drawers and overlays.

---

## 27.6 Dragging movements — WCAG 2.5.7 (AA)

If an action uses dragging, provide a non-drag single-pointer alternative unless dragging is essential.

Examples:
- kanban reorder → “Move to…” action;
- column reorder → menu controls;
- slider with meaningful discrete values → input/step buttons where appropriate.

---

## 27.7 Target size — WCAG 2.5.8 (AA)

Minimum 24 × 24 CSS px unless an exception applies.

For touch-first design, target closer to the 44–48 platform-guidance range.

---

# 28. REAL PRODUCT / DESIGN-SYSTEM OBSERVATIONS

## Atlassian

Useful signals:
- viewport breakpoints are explicit;
- side nav becomes overlay below desktop width;
- layout regions have defined min/default/max widths;
- structured content does not necessarily benefit from infinite fluid expansion.

### Agent lesson
Use minimum useful region widths to decide when persistent panes stop being viable.

## Carbon

Useful signals:
- data-table actions become persistent on touch instead of hover-only;
- responsive modal widths increase as viewport decreases, reaching full width;
- chart legends may stack or move behind an explicit mobile disclosure;
- dashboards emphasize information hierarchy and limiting nonessential metrics.

### Agent lesson
Responsive adaptation affects interaction visibility and semantic density, not only geometry.

## Shopify / Polaris

Useful signals:
- current Polaris web components support container-based responsive values;
- app navigation changes from desktop sidebar to mobile title-bar menu;
- tables have narrow list behavior;
- narrow table layouts require sorting and selection controls to be relocated rather than silently lost;
- filter toolbar can wrap responsively and active filters can remain visible as chips.

### Agent lesson
A component transformation must preserve its **capabilities and state**, even when its desktop subcomponents disappear.

## Notion

Useful signals:
- desktop sidebar can be opened/closed;
- mobile uses persistent bottom navigation;
- mobile has no hover states and surfaces controls that are hover-revealed on desktop;
- desktop columns collapse to a single column on mobile;
- desktop search keyboard shortcuts become a visible mobile search destination.

### Agent lesson
A successful mobile product changes navigation, layout and interaction affordances simultaneously.

## Vercel

Its 2026 dashboard navigation redesign:
- moved horizontal tabs into a resizable sidebar;
- lets users hide the sidebar;
- introduced a floating mobile bottom bar optimized for one-handed use.

### Agent lesson
Desktop and mobile navigation can share information architecture while using different physical patterns.

## Slack

Useful signals:
- desktop and mobile search use platform-appropriate controls;
- mobile filtering is exposed through explicit filter actions;
- mobile navigation content can be user-customized/reordered.

### Agent lesson
On constrained screens, prioritization and personalization can outperform attempting to display everything permanently.

---

# 29. RESPONSIVE DECISION TREE

Use this tree for every major region/component.

```text
START
│
├─ 1. What is the user's primary task in this region?
│     ├─ unknown → infer from page purpose, primary CTA, frequency, data type
│     └─ known
│
├─ 2. Which elements are required for task completion or correct interpretation?
│     └─ mark as NON-HIDEABLE
│
├─ 3. Does the current layout fit at the component's actual inline size?
│     ├─ YES → keep current mode; allow intrinsic scaling
│     └─ NO
│
├─ 4. Is the failure caused by local component width or whole-app shell width?
│     ├─ local → container query / intrinsic redesign
│     └─ shell → media query / application-mode change
│
├─ 5. Can spacing/decorative density be reduced without hurting touch/readability?
│     ├─ YES → compress and retest
│     └─ NO
│
├─ 6. Can content safely wrap?
│     ├─ YES → wrap and retest
│     └─ NO
│
├─ 7. Can lower-priority content be reordered/grouped/moved?
│     ├─ YES → transform and retest
│     └─ NO
│
├─ 8. Is simultaneous visibility essential?
│     ├─ YES
│     │   ├─ 2D relationship essential?
│     │   │   ├─ YES → controlled component scroll/pan
│     │   │   └─ NO  → reduce secondary simultaneous content
│     │   └─ preserve key comparison elements
│     └─ NO → progressive disclosure / drawer / detail page
│
├─ 9. Does the input mode remove hover or precision?
│     ├─ YES → persist actions, enlarge targets, add gesture alternatives
│     └─ NO
│
├─ 10. Does the transformed UI preserve:
│      ├─ functionality?
│      ├─ state?
│      ├─ focus order?
│      ├─ semantic reading order?
│      ├─ access to hidden/moved details?
│      └─ correct interpretation?
│
└─ 11. Validate at zoom, 320 CSS px reflow, long text, RTL, touch, keyboard.
```

---

# 30. COMPONENT TRANSFORMATION MATRIX

| Component | Desktop | Tablet | Mobile | Avoid |
|---|---|---|---|---|
| Sidebar | persistent/resizable | rail or overlay | bottom nav, drawer, or nav screen | tiny persistent sidebar |
| Global nav | full labels/actions | compact + overflow | title + essential actions + bottom/menu nav | shrinking every item |
| Dashboard | hierarchical multi-column | 2-column/asymmetric | priority-ordered single column | blind CSS stacking |
| Table: entity browsing | full table | priority columns | list/card rows | microscopic table |
| Table: comparison | full table | scroll/priority | contained horizontal scroll | card conversion that destroys comparison |
| Data grid editing | full grid | simplified/full-screen | dedicated data workspace | fake 12-column mini-grid |
| Cards | multi-column | intrinsic 2–3 columns | 1 column / list-like | padding-heavy nested cards |
| Charts | full legend/axes | simplified ticks/legend | simplified + stacked/disclosed legend | resize-only |
| Filters | inline/side panel | partial inline + overflow | filter sheet + active chips | invisible active filters |
| Forms | 1–2 semantic columns | mostly 1 column | 1 column | zigzag order |
| Modal | bounded dialog | larger dialog | full-screen/sheet/page | fixed desktop width |
| Side panel | inline | overlay if pressured | full-screen/detail route | panel + unusable sliver |
| Command palette | centered + shortcut | large modal | full-screen search/actions | keyboard-only access |
| Search | persistent/rich | compact | first-class search screen/tab | hover preview dependency |
| Settings | sidebar + form | compact/list-detail | drill-in hierarchy | permanent mini-sidebar |
| Pricing | plan row + matrix | 2-up / adaptive matrix | stacked plans + adaptive comparison | tiny full matrix |
| Landing | simultaneous text/media | simplified split | sequential narrative | 50/50 split on phone |

---

# 31. BREAKPOINT STRATEGY FOR AN AI SKILL

## Phase 1 — infer structural minimums

For each major region, estimate:

```yaml
sidebar:
  min_inline: 240px
  mode_below_min: overlay

main_workspace:
  min_inline: 600px

detail_panel:
  min_inline: 320px
  optional: true
  mode_below_total_fit: overlay
```

Do not hard-code these exact numbers globally; derive from the actual design.

## Phase 2 — create shell transitions

Example:

```text
if sidebar + main + gaps no longer fit:
    collapse sidebar

if main + detail panel no longer fit:
    make detail panel overlay

if global actions no longer fit:
    preserve primary actions
    move secondary actions to overflow

if mobile layout reaches one-primary-region mode:
    switch navigation pattern
```

## Phase 3 — create component transitions

Example card:

```css
.card-wrapper {
  container-type: inline-size;
}

@container (width < 28rem) {
  .card {
    grid-template-columns: 1fr;
  }
}
```

The component does not care whether it is “on tablet”.

## Phase 4 — validate between breakpoints

Never test only at named breakpoints.

Test:
- exactly before;
- exactly after;
- midpoint;
- arbitrary values;
- split-screen values;
- zoom-generated effective widths.

A responsive UI that works only at 375, 768 and 1440 is not robust.

---

# 32. MOBILE PRIORITY RULES

When transforming a desktop screen to mobile, process elements in this priority order.

## P0 — never remove

- task-critical primary action;
- irreversible/destructive action access;
- current entity/page identity;
- validation/error state;
- active system status that changes interpretation;
- required input;
- required chart/table context;
- navigation escape/back path.

## P1 — keep directly visible if possible

- high-frequency actions;
- primary metric;
- primary status;
- search in search-heavy SaaS;
- high-frequency filter;
- current filter/sort summary;
- most-used top-level destinations.

## P2 — may compress/group

- secondary actions;
- metadata;
- secondary KPIs;
- redundant labels;
- low-frequency global actions.

## P3 — move to disclosure

- tertiary filters;
- long help/explanation;
- low-frequency configuration;
- supplementary columns;
- secondary chart series controls.

## P4 — may hide if genuinely redundant/optional

- duplicate decorative labels;
- purely decorative media;
- repeated explanatory copy already represented elsewhere.

### Hide test

Before hiding an element, the agent must answer:

1. Is the information/action redundant?
2. Can the task be completed correctly without it?
3. Can the user still retrieve it easily if needed?
4. Does hiding it alter interpretation?
5. Does hiding it create desktop/mobile capability disparity that matters?

If any answer is unfavorable, do not hide; transform instead.

---

# 33. AI IMPLEMENTATION RULES

These rules are intended to be directly convertible into a Skill.

## Rule 1 — analyze before coding

Before implementing responsive CSS, output internally:

```yaml
page_task:
primary_regions:
secondary_regions:
critical_actions:
critical_information:
comparison_relationships:
touch_risks:
hover_dependencies:
minimum_component_widths:
candidate_transformations:
```

## Rule 2 — prefer the smallest number of meaningful breakpoints

Every breakpoint must have a reason such as:
- nav mode switch;
- pane switch;
- table/list switch;
- filter mode switch.

Avoid dozens of component-specific viewport breakpoints when container queries or intrinsic layout are better.

## Rule 3 — preserve DOM semantics where possible

Use CSS reflow/reordering carefully.

Visual reordering must not create a keyboard/screen-reader order that contradicts the visual sequence.

If the semantic structure truly changes, render a responsive variant only when necessary and preserve:
- state;
- focus;
- labels;
- URL/navigation semantics.

## Rule 4 — no hover-only functionality

Every hover action requires:
- visible/focus equivalent on fine pointer;
- persistent/menu/tap equivalent on coarse pointer.

## Rule 5 — no global horizontal page scroll

Wide component:
```text
overflow inside component
```

not:
```text
body/page overflow-x
```

unless the product is intentionally a canvas application.

## Rule 6 — do not reduce font size as the first response to pressure

Transformation order:
1. reduce excess gap/padding;
2. wrap;
3. restructure;
4. disclose;
5. only then consider small typographic adjustment within a safe scale.

## Rule 7 — table behavior must be task-classified

```text
comparison task → preserve 2D relationship / horizontal component scroll
entity browse → list/card transformation
bulk operations → preserve selection + bulk action state
spreadsheet editing → dedicated full-screen grid
```

## Rule 8 — mobile action priority

At most:
- one clearly dominant primary page action;
- a small number of persistent secondary actions;
- rest in contextual overflow/sheet.

Do not make five actions equal-weight merely because desktop had room.

## Rule 9 — responsive filters preserve state visibly

Mobile filter drawer closed:
- show active count;
- show important active chips/summary;
- provide clear reset.

## Rule 10 — chart simplification cannot change the story

Allowed:
- fewer ticks;
- moved legend;
- series toggle;
- reduced annotation.

Not allowed:
- misleading axis change;
- removal of category meaning;
- data point omission that changes conclusion without disclosure.

## Rule 11 — touch mode is capability-driven

Use input capability (`hover`, `pointer`) rather than width alone.

A large touch tablet may need touch interaction rules despite desktop-like width.

## Rule 12 — mobile forms favor single linear focus order

Multi-column form → single column unless semantic pairing is strong.

## Rule 13 — sticky UI must account for focus and safe areas

Sticky top/bottom bars:
- add scroll padding;
- test focused controls;
- account for mobile browser/system safe areas;
- do not cover validation or CTA targets.

## Rule 14 — use logical properties

Prefer inline/block CSS to left/right for layouts expected to localize.

## Rule 15 — test long content before adding more breakpoints

Use:
- 2× normal nav label length;
- long German/French-like labels;
- long user-generated project names;
- large numeric values;
- empty states;
- error states.

## Rule 16 — progressive disclosure must preserve discoverability

A feature moved behind disclosure needs:
- visible trigger;
- meaningful label;
- state indication when active.

## Rule 17 — full-screen mobile is often better than miniature desktop overlay

If a modal/panel/task requires most of the viewport, intentionally make it full-screen and supply appropriate navigation.

## Rule 18 — avoid breakpoint-driven duplication of business logic

Desktop and mobile variants should share:
- state source;
- validation;
- data query;
- selection;
- sorting/filter values.

Shopify’s narrow-table guidance is a strong example: responsive subcomponents change, but the underlying selection/filter/sort state should remain one source of truth.

---

# 34. RESPONSIVE QA CHECKLIST

## Layout

- [ ] No accidental page-level horizontal scrolling at 320 CSS px equivalent.
- [ ] Every major component has a known minimum usable width.
- [ ] Layout works at arbitrary widths, not only mockup widths.
- [ ] Split panes collapse before either pane becomes unusable.
- [ ] Content order after stacking matches actual priority.
- [ ] Ultrawide layouts do not produce excessively stretched structured content.
- [ ] Long labels do not break navigation/toolbars.

## Breakpoints

- [ ] Every breakpoint corresponds to a documented mode change or failure threshold.
- [ ] Values immediately before and after each breakpoint were tested.
- [ ] Intermediate widths were tested.
- [ ] Container-responsive components were tested in multiple parents at the same viewport width.

## Navigation

- [ ] Current location remains understandable when sidebar disappears.
- [ ] Mobile top-level destinations are prioritized.
- [ ] Bottom nav is not overloaded.
- [ ] Deep navigation remains searchable/reachable.
- [ ] Back behavior is clear in drill-in mobile screens.

## Tables / data grids

- [ ] Table task was classified: compare, browse, bulk, edit, scan.
- [ ] Mobile transformation matches the task.
- [ ] Sorting remains available.
- [ ] Filtering remains available.
- [ ] Selection/bulk action remains available when required.
- [ ] Hidden columns are recoverable.
- [ ] Touch row actions are not hover-dependent.
- [ ] Horizontal scroll, if used, is contained in the component.
- [ ] Sticky columns/headers do not obscure focus.

## Dashboards

- [ ] KPI priority is explicit.
- [ ] Mobile stack order is intentional.
- [ ] Important charts remain interpretable.
- [ ] Low-priority widgets are summarized/moved rather than randomly hidden.
- [ ] Filters clearly indicate which widgets they affect.

## Charts

- [ ] Labels/ticks remain readable.
- [ ] Legend remains available.
- [ ] Hover details have tap/focus access.
- [ ] Gesture interactions have alternatives where required.
- [ ] Axis transformation does not change interpretation.
- [ ] Data summary/accessible alternative exists where needed.

## Filters

- [ ] Active filter count/state visible when filter UI is closed.
- [ ] Reset is discoverable.
- [ ] Sort remains distinct and discoverable.
- [ ] Filter state survives drawer/modal transitions appropriately.
- [ ] Result update behavior is clear.

## Forms

- [ ] Focus order matches visual order.
- [ ] Labels remain visible.
- [ ] Errors remain adjacent/reachable.
- [ ] Inputs work in portrait and landscape.
- [ ] Virtual keyboard does not cover active controls/actions.
- [ ] 200% text does not clip controls.
- [ ] Sticky footer does not hide focus/error state.

## Modal / drawer

- [ ] Width never overflows compact viewport.
- [ ] Long content has been reconsidered as a page/full-screen flow.
- [ ] No confusing nested scroll regions.
- [ ] Focus is managed correctly.
- [ ] Dismiss/back behavior is clear.
- [ ] Unsaved state is preserved or explicitly handled.

## Touch

- [ ] WCAG target-size minimum is met or valid spacing exception applies.
- [ ] Primary touch controls aim for comfortable ~44–48 size range.
- [ ] Small glyphs have expanded hit regions.
- [ ] Adjacent targets are not error-prone.
- [ ] No action exists only on hover.
- [ ] Swipe/drag has an alternative.

## Accessibility

- [ ] Portrait and landscape both work unless orientation is essential.
- [ ] 200% text resize works without loss.
- [ ] 320 CSS px reflow test passes except essential 2D components.
- [ ] Text-spacing override does not clip content.
- [ ] Keyboard focus is not obscured by sticky UI.
- [ ] Reading order remains meaningful after visual reordering.
- [ ] RTL/logical-property behavior tested when relevant.
- [ ] Reduced-motion preference respected for responsive transitions.

## Content

- [ ] Nothing critical was hidden solely to make layout fit.
- [ ] Truncation has a way to expose full values where needed.
- [ ] Mobile content hierarchy is explicit.
- [ ] User-created long names were tested.
- [ ] Empty/loading/error states were tested in every responsive mode.

## Performance

- [ ] Mobile does not download unnecessary giant media merely hidden by CSS when avoidable.
- [ ] Resize/layout logic is not driven by excessive JS listeners.
- [ ] Container queries are used intentionally, not wrapped around every element.
- [ ] Complex responsive variants do not duplicate expensive data fetching.

---

# 35. Compact agent policy

This can serve as the shortest executable mental model:

```text
1. Identify the task.
2. Mark non-hideable information/actions.
3. Determine minimum usable widths from content.
4. Let intrinsic CSS solve continuous resizing.
5. Use container queries for local component modes.
6. Use media queries for global shell/input/preference modes.
7. When space fails:
   compress → wrap → reorder → group → move → summarize → disclose → hide.
8. Transform navigation based on frequency and hierarchy.
9. Transform tables based on task, never with one universal rule.
10. Transform dashboards by priority, not source-order accident.
11. Preserve chart meaning; simplify representation.
12. Preserve visible filter/sort/selection state.
13. On touch: persistent affordances, larger targets, no hover dependency.
14. Prefer one-column mobile forms and one primary task region.
15. Use full-screen mobile surfaces when miniature desktop overlays stop helping.
16. Preserve semantics, state, focus order and capability across modes.
17. Validate 320 CSS px reflow, 200% text, orientation, long content, touch and keyboard.
18. Breakpoints are outputs of layout pressure—not inputs to design.
```

---

# 36. Sources

## Accessibility / standards

1. W3C — Understanding SC 1.4.10 Reflow  
   https://www.w3.org/WAI/WCAG21/Understanding/reflow

2. W3C — Understanding SC 1.4.4 Resize Text  
   https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html

3. W3C — Understanding SC 1.4.12 Text Spacing  
   https://www.w3.org/WAI/WCAG22/Understanding/text-spacing

4. W3C — WCAG 2.2 Quick Reference, Orientation 1.3.4  
   https://www.w3.org/WAI/WCAG22/quickref/

5. W3C — Understanding SC 2.4.11 Focus Not Obscured (Minimum)  
   https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum

6. W3C — C43: CSS scroll-padding to un-obscure content  
   https://www.w3.org/WAI/WCAG22/Techniques/css/C43

7. W3C — Understanding SC 2.5.7 Dragging Movements  
   https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements

8. W3C — Understanding SC 2.5.8 Target Size (Minimum)  
   https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum

## Modern CSS

9. MDN — CSS Container Queries  
   https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries

10. MDN — Using container size and style queries  
    https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_size_and_style_queries

11. MDN — `minmax()`  
    https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/minmax

12. MDN — `clamp()`  
    https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp

13. MDN — CSS Logical Properties and Values  
    https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Logical_properties_and_values

14. MDN — Card layout cookbook (`auto-fill` + `minmax`)  
    https://developer.mozilla.org/en-US/docs/Web/CSS/How_to/Layout_cookbook/Card

## Design systems

15. Atlassian Design System — Grid  
    https://atlassian.design/foundations/grid-beta/applying-grid

16. Atlassian Design System — Navigation layout and responsive behavior  
    https://atlassian.design/components/navigation-system/layout

17. Carbon Design System — 2x Grid  
    https://www.carbondesignsystem.com/building-blocks/foundations/2x-grid/overview

18. Carbon Design System — Data table guidelines  
    https://www.carbondesignsystem.com/building-blocks/core/components/data-table/guidelines

19. Carbon Design System — Modal guidelines  
    https://www.carbondesignsystem.com/building-blocks/core/components/modal/guidelines

20. Carbon Design System — Data visualization legends  
    https://www.carbondesignsystem.com/building-blocks/data-visualization/legends

21. Carbon Design System — Dashboards  
    https://www.carbondesignsystem.com/building-blocks/data-visualization/dashboards

22. U.S. Web Design System — Modal  
    https://designsystem.digital.gov/components/modal/

23. U.S. Web Design System — Text input  
    https://designsystem.digital.gov/components/text-input/

24. Material UI — Breakpoints  
    https://mui.com/material-ui/customization/breakpoints/

25. MUI X — Data Grid list view  
    https://mui.com/x/react-data-grid/list-view/

## Shopify / Polaris

26. Shopify — Polaris responsive values and query containers  
    https://shopify.dev/docs/api/polaris/using-polaris-web-components

27. Shopify — Query container  
    https://shopify.dev/docs/api/app-home/latest/web-components/layout-and-structure/query-container

28. Shopify — App navigation desktop vs mobile  
    https://shopify.dev/docs/api/app-home/latest/app-bridge-web-components/app-nav

29. Shopify — Migrating IndexTable / narrow list layout behavior  
    https://shopify.dev/docs/apps/build/app-home/migrate-from-polaris-react/index-table

## Real SaaS product evidence

30. Notion — Workspaces on mobile  
    https://www.notion.com/en-us/help/workspaces-on-mobile

31. Notion — Mobile vs desktop differences  
    https://www.notion.com/help/notion-for-mobile

32. Notion — Search  
    https://www.notion.com/help/search

33. Notion — Sidebar navigation  
    https://www.notion.com/help/navigate-with-the-sidebar

34. Vercel — 2026 dashboard navigation redesign  
    https://vercel.com/changelog/dashboard-navigation-redesign-rollout

35. Slack — Search on desktop and mobile  
    https://slack.com/help/articles/202528808-Search-in-Slack

36. Slack — Mobile app customization  
    https://slack.com/help/articles/29788684062739-Customize-the-Slack-mobile-app

37. Notion — Pricing  
    https://www.notion.com/pricing

38. Slack — Pricing and feature comparison  
    https://slack.com/pricing

## Touch guidance

39. Apple Human Interface Guidelines — Buttons / hit regions  
    https://developer.apple.com/design/human-interface-guidelines/buttons

40. Android Developers — Accessibility / touch target guidance  
    https://developer.android.com/guide/topics/ui/accessibility/apps

---

# 37. Final conclusion

The central mistake in responsive SaaS work is to model responsiveness as:

```text
desktop CSS
+ tablet breakpoint
+ mobile breakpoint
```

A better model is:

```text
task
→ information/action priority
→ minimum viable component geometry
→ intrinsic layout
→ local component transformations
→ global shell transformations
→ input-mode adaptations
→ accessibility constraints
→ breakpoint/container-query encoding
→ QA across continuous widths
```

A capable AI design agent should therefore **reason about what must remain usable and understandable before deciding what CSS to write**.

The quality bar is not:

> “Does the page fit at 375 px?”

It is:

> “Can the user still understand the same system, complete the important task, discover the important actions, interpret the data correctly, and operate it comfortably across narrow space, zoom, touch, keyboard, orientation changes and variable content?”

That is the standard the Skill should enforce.
