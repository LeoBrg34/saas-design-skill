# Typography Intelligence for SaaS — Research for an AI Skill

**Target file:** `research/typography.md`  
**Research date:** 2026-10-06  
**Purpose:** provide an AI agent with decision rules for choosing, scaling, applying, validating, and implementing typography in SaaS products.

---

## 0. How to read this research

This document is intentionally not a list of fashionable fonts. It separates three kinds of guidance:

- **[RESEARCH]** — supported by standards, accessibility guidance, controlled studies, or strong empirical evidence.
- **[CONVENTION]** — repeated practice across mature design systems and production products; useful default, but not a law.
- **[STYLE]** — brand/aesthetic preference. It may be strategically useful, but must never override legibility, accessibility, localization, or product constraints.

Confidence labels:

- **HIGH** — standards, multiple authoritative systems, or strong/repeated research.
- **MEDIUM** — mature industry convention with good rationale but limited controlled evidence.
- **LOW** — primarily stylistic or context-dependent.

### Core principle

Typography decisions must be made in this order:

1. **Accessibility and legibility**
2. **Content role**
3. **Platform**
4. **Information density**
5. **Interaction context**
6. **Localization/script**
7. **Performance constraints**
8. **Brand personality**
9. **Aesthetic preference**

If a branding choice conflicts with legibility or user text scaling, the branding choice loses.

---

# 1. TYPOGRAPHIC SYSTEM

## Rule 1 — Define semantic typography roles before choosing exact sizes

**TYPE:** [CONVENTION]  
**RULE:** Build the system around semantic roles such as `display`, `heading`, `title`, `body`, `label`, `caption`, `code`, and `metric` before defining component-specific font sizes.

**RATIONALE:** Material 3, Atlassian, Carbon, Spectrum, Fluent, Primer, and Vercel all group typography into reusable roles or tokens rather than treating every text instance as a unique size. Semantic roles reduce arbitrary variation and let an agent preserve hierarchy while changing density or platform.

**USE WHEN:** Always, especially when generating a design system or implementing reusable UI components.

**AVOID WHEN:** Only for extremely small prototypes where a full token system would be wasteful.

**EXCEPTIONS:** A marketing site may add campaign-specific display styles, but these should still map back to named roles.

**CONFIDENCE:** HIGH

**SOURCES:** [S08], [S09], [S10], [S11], [S12], [S13], [S15]

---

## Rule 2 — Prefer one primary UI family, then add fonts only for a distinct semantic job

**TYPE:** [CONVENTION]  
**RULE:** Default to one highly legible primary family for the product UI. Add a second family only if it has a clear role such as display branding, long-form editorial reading, or code.

**RATIONALE:** Apple recommends minimizing the number of typefaces because excessive mixing can obscure hierarchy. Atlassian separates app fonts from its marketing brand font. GitHub, Vercel, and Adobe use a primary sans plus a mono for code/data contexts.

**USE WHEN:** Product UI, dashboards, enterprise SaaS, productivity tools.

**AVOID WHEN:** Do not add a second family merely to make a design feel “more designed.”

**EXCEPTIONS:** Editorial products may intentionally use a serif for reading content and a sans-serif for interface chrome.

**CONFIDENCE:** HIGH

**SOURCES:** [S04], [S08], [S13], [S15], [S27]

---

## Rule 3 — Do not encode “sans-serif is always more readable on screen” as an AI rule

**TYPE:** [RESEARCH]  
**RULE:** Treat serif vs sans-serif as a contextual choice, not a universal readability rule.

**RATIONALE:** Controlled work and systematic reviews do not support a consistent universal legibility advantage for serif or sans-serif. A 2026 experiment found no interaction between serif/sans-serif choice and screen versus paper comprehension. Other controlled work found no meaningful reading-speed difference when serif presence was isolated. Typeface metrics, size, spacing, familiarity, rendering quality, and context matter more.

**USE WHEN:** Selecting body or UI families.

**AVOID WHEN:** Do not reject a serif purely because the medium is digital.

**EXCEPTIONS:** Dense control surfaces generally favor compact, neutral UI families by convention because they provide broad symbol coverage and predictable small-size behavior, not because serifs are inherently unreadable.

**CONFIDENCE:** HIGH

**SOURCES:** [S22], [S23]

---

## Rule 4 — Use monospace for code and alignment-sensitive symbolic content, not ordinary body copy

**TYPE:** [CONVENTION]  
**RULE:** Use a monospaced family for source code, terminal commands, identifiers when character distinction matters, and some alignment-sensitive values. Use proportional text for normal prose and most labels.

**RATIONALE:** GitHub exposes a dedicated monospace stack; Atlassian uses Atlassian Mono for app code contexts; Vercel uses Geist Mono; Spectrum uses Source Code Pro for code. Monospace is semantically useful but typically less space-efficient for prose.

**USE WHEN:** Code blocks, shell commands, hashes, technical identifiers, developer tools.

**AVOID WHEN:** Paragraphs, buttons, navigation, ordinary form labels.

**EXCEPTIONS:** A developer-focused brand may use mono selectively for short labels or metadata, but readability should be verified.

**CONFIDENCE:** HIGH

**SOURCES:** [S08], [S10], [S13], [S15]

---

## Rule 5 — Prefer tabular numerals for columns and changing metrics; do not force monospace for all numbers

**TYPE:** [CONVENTION]  
**RULE:** Use tabular figures (`font-variant-numeric: tabular-nums`) for aligned table columns, counters, financial values, timestamps, dashboards, and values that change in place. Use proportional numerals in prose.

**RATIONALE:** GOV.UK exposes a tabular option; Vercel uses tabular numerals in numeric label styles; Spectrum defines “Monospace numbers” for values where stable width improves comparison and reduces visual shifting.

**USE WHEN:** Analytics dashboards, finance, tables, timers, prices, KPIs.

**AVOID WHEN:** Long prose or headings containing occasional numbers where proportional rhythm looks more natural.

**EXCEPTIONS:** If the chosen family does not provide tabular figures, a dedicated numeric/mono style can be used selectively.

**CONFIDENCE:** HIGH

**SOURCES:** [S13], [S16], [S18]

---

## Rule 6 — Use regular weight for body text and medium/semibold for UI emphasis

**TYPE:** [CONVENTION]  
**RULE:** Default body and editable text to approximately 400. Use approximately 500–600 for controls, compact titles, selected navigation, and emphasis. Reserve 700+ for stronger headings or branding.

**RATIONALE:** Fluent, Material 3, Carbon, Atlassian, and Spectrum repeatedly use regular body text and medium/semibold/bold for titles and controls. This creates hierarchy without multiplying sizes.

**USE WHEN:** Nearly all product UIs.

**AVOID WHEN:** Do not use bold for entire paragraphs or make every control bold.

**EXCEPTIONS:** Font weight values are not visually equivalent between families. A “500” in one family can look like a “600” in another.

**CONFIDENCE:** HIGH

**SOURCES:** [S09], [S10], [S11], [S12], [S15]

---

## Rule 7 — Avoid light/thin weights at small UI sizes

**TYPE:** [RESEARCH + CONVENTION]  
**RULE:** Do not use Thin/ExtraLight/Light for small product text. If a thin brand face is required, increase its size and test contrast/rendering.

**RATIONALE:** Apple explicitly warns that thin weights are harder to read at small sizes and recommends regular, medium, semibold, or bold. WCAG also notes that unusually thin strokes can reduce effective legibility even when nominal font size is large enough for relaxed contrast thresholds.

**USE WHEN:** Any text below headline/display scale, especially mobile and dense dashboards.

**AVOID WHEN:** Small labels, helper text, disabled-looking-but-active text, placeholders, chart labels.

**EXCEPTIONS:** Large display typography can use lighter weights if contrast and rendering remain strong.

**CONFIDENCE:** HIGH

**SOURCES:** [S01], [S04]

---

## Rule 8 — Choose size by role and density, not one universal base size

**TYPE:** [CONVENTION]  
**RULE:** A SaaS product may legitimately use a 14px productive base or a 16–17px reading-oriented base. The AI should choose based on density and platform instead of enforcing “16px everywhere.”

**RATIONALE:** Carbon’s productive set uses a 14px base and expressive set a 16px base. Fluent Web uses 14/20 for Body 1. Atlassian uses 14/20 for default component body and 16/24 for long-form body. Material 3 uses 14/20 Body Medium and 16/24 Body Large. Apple’s iOS default is 17pt.

**USE WHEN:** Selecting a global product scale.

**AVOID WHEN:** Do not shrink important primary content simply to fit more data.

**EXCEPTIONS:** Highly constrained native desktop utilities may use smaller platform-native defaults; large-touch/mobile interfaces generally need larger text.

**CONFIDENCE:** HIGH

**SOURCES:** [S03], [S09], [S10], [S11], [S12]

---

## Rule 9 — Treat 12px as supporting text, not default primary reading text

**TYPE:** [CONVENTION]  
**RULE:** On web SaaS, 12px should normally be reserved for captions, metadata, compact labels, and secondary information. Primary body and actionable labels should usually be 14px or larger.

**RATIONALE:** Atlassian labels 12px body as secondary and says to use it sparingly. Carbon uses 12px labels/helper text but 14px productive body. Material uses 12px for Body Small, not the primary reading style. Apple recommends at least 11pt on iOS but a 17pt default.

**USE WHEN:** Timestamps, captions, dense secondary metadata.

**AVOID WHEN:** Main navigation, primary form input values, long paragraphs, critical alerts.

**EXCEPTIONS:** Some desktop professional tools can use 12–13px for dense secondary controls if zoom/scaling is excellent and the font has strong small-size metrics.

**CONFIDENCE:** HIGH

**SOURCES:** [S03], [S10], [S11], [S12]

---

## Rule 10 — Increase line height as text becomes longer and more paragraph-like

**TYPE:** [RESEARCH + CONVENTION]  
**RULE:** Use tighter leading for one-line controls/headings and more generous leading for multiline body text.

**RATIONALE:** Carbon separates compact 14/18 from long 14/20 and expressive 16/22 from long 16/24. Spectrum uses ~115–130% for compact/default type and 150% for body/code. WCAG requires layouts to survive user-applied line-height of at least 1.5× under SC 1.4.12; WCAG AAA 1.4.8 provides 1.5× as a readable presentation target.

**USE WHEN:** Every system with both controls and prose.

**AVOID WHEN:** Do not set the same fixed line-height ratio for every role.

**EXCEPTIONS:** Scripts with taller glyphs may require more leading; Spectrum uses 1.7× for CJK body text.

**CONFIDENCE:** HIGH

**SOURCES:** [S02], [S07], [S10], [S15]

---

## Rule 11 — Do not misread WCAG 1.4.12 as “all body text must default to 1.5 line-height”

**TYPE:** [RESEARCH]  
**RULE:** The AI must distinguish between a recommended readable default and a conformance requirement. WCAG 1.4.12 requires that content not break when a user applies 1.5× line height, 0.12em letter spacing, 0.16em word spacing, and 2× font-size paragraph spacing; it does not require those values as the authored default.

**RATIONALE:** This distinction prevents over-loose typography in dense UI while preserving accessibility.

**USE WHEN:** Auditing or generating WCAG-conformant interfaces.

**AVOID WHEN:** Never claim 1.5 line-height is universally mandatory for AA compliance.

**EXCEPTIONS:** Long-form body copy can still use ~1.5 by choice, and WCAG AAA visual-presentation guidance supports it.

**CONFIDENCE:** HIGH

**SOURCES:** [S02], [S07]

---

## Rule 12 — Keep body tracking close to the font’s default

**TYPE:** [CONVENTION]  
**RULE:** For body and normal UI text, start at the typeface’s native tracking. Make only small adjustments when the font or role clearly benefits.

**RATIONALE:** Mature systems use small role-specific tracking values rather than globally spreading or tightening text. Research on dyslexia-related spacing does not support arbitrary large inter-letter spacing; one study found increased inter-letter spacing could impair reading speed when not paired appropriately with word spacing.

**USE WHEN:** Body, labels, inputs, tables.

**AVOID WHEN:** Large positive tracking on paragraphs; heavy negative tracking on small text.

**EXCEPTIONS:** Very large display text may tolerate modest negative tracking; short uppercase labels may need positive tracking.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S10], [S12], [S24]

---

## Rule 13 — Build hierarchy with multiple signals, not color alone

**TYPE:** [CONVENTION + ACCESSIBILITY]  
**RULE:** Encode hierarchy through semantic role, size, weight, spacing, and position. Color may reinforce hierarchy but should not be the only differentiator.

**RATIONALE:** Primer explicitly warns against using color as the primary emphasis method. Spectrum defines hierarchy using size, weight, and color together. Relying on faint gray creates low-contrast failure risk.

**USE WHEN:** All interfaces.

**AVOID WHEN:** “Primary = dark gray; secondary = slightly lighter gray” with no structural distinction.

**EXCEPTIONS:** Dense tables may intentionally keep size constant and use weight/position to preserve density.

**CONFIDENCE:** HIGH

**SOURCES:** [S01], [S08], [S15]

---

# 2. UI TYPOGRAPHY

The ranges below are **decision ranges**, not universal laws. They represent convergence among Material, Fluent, Carbon, Atlassian, Spectrum, Primer, and Vercel.

## Rule 14 — Navbar and top navigation

**TYPE:** [CONVENTION]  
**RULE:** Use compact, stable, single-line text. Typical web SaaS range: **13–16px**, generally **500–600** for active/high-priority items and **400–500** for ordinary items.

**RATIONALE:** Navigation is scanned repeatedly and competes with content. Excessive size wastes horizontal space; too-small text reduces glanceability.

**USE WHEN:** Desktop navbar, tabs, segmented navigation.

**AVOID WHEN:** Do not use decorative display faces or very light weights.

**EXCEPTIONS:** Marketing navigation may use 16–18px when the page is spacious.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S09], [S13], [S15]

---

## Rule 15 — Sidebar navigation

**TYPE:** [CONVENTION]  
**RULE:** Typical desktop sidebar labels: **13–14px** in dense tools, **14–16px** in standard productivity apps. Use weight or background state for selection; do not rely only on tiny size differences.

**RATIONALE:** Sidebars can contain many repeated items and benefit from productive typography. Vercel identifies 14px labels as one of its most common styles; Carbon and Fluent use 14px as a productive body size.

**USE WHEN:** CRM, issue trackers, analytics, admin tools.

**AVOID WHEN:** Avoid 11–12px as the default navigation size.

**EXCEPTIONS:** Secondary nested metadata may be 12px if clearly noncritical.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S09], [S10], [S13]

---

## Rule 16 — Buttons

**TYPE:** [CONVENTION]  
**RULE:** Default button text should generally be **14–16px** with **500–600** weight. Tiny embedded controls may go to **12px**, but should not become the default product button.

**RATIONALE:** Material 3 uses Label Large 14/20 Medium; Vercel uses button sizes 12, 14, and 16 with 14 as default. Spectrum uses medium/bold component text for action buttons.

**USE WHEN:** Standard web product controls.

**AVOID WHEN:** Thin weights, all-uppercase by default, overly condensed fonts.

**EXCEPTIONS:** Platform-native components should follow their platform typography.

**CONFIDENCE:** HIGH

**SOURCES:** [S12], [S13], [S15]

---

## Rule 17 — Inputs and editable text

**TYPE:** [CONVENTION]  
**RULE:** Input values should use the primary UI/body face, normally **14–16px on web** and about **16–17pt/sp on mobile** where appropriate. Keep editable text at regular weight.

**RATIONALE:** Spectrum explicitly uses Regular for editable and user-entered content. Apple’s iOS default readable text size is 17pt; Material Body Large is 16sp.

**USE WHEN:** Text fields, search, textarea, combobox input.

**AVOID WHEN:** Decorative fonts, light weights, uppercase transformations of user input.

**EXCEPTIONS:** Dense native desktop tools may use platform-standard smaller sizes.

**CONFIDENCE:** HIGH

**SOURCES:** [S03], [S12], [S15]

---

## Rule 18 — Form labels and helper text

**TYPE:** [CONVENTION]  
**RULE:** Labels normally fall in **12–14px**; helper/error text typically **12–14px**, with contrast and spacing sufficient to remain readable. Labels can use 500–600 when separation from input text is needed.

**RATIONALE:** Carbon uses 12px productive label/helper styles; Atlassian uses 12px secondary body and 14px default body; Vercel uses 13–14px label styles heavily.

**USE WHEN:** Forms and settings.

**AVOID WHEN:** Critical errors in extremely small, low-contrast gray text.

**EXCEPTIONS:** Mobile can use 14–16px labels where space allows.

**CONFIDENCE:** HIGH

**SOURCES:** [S10], [S11], [S13]

---

## Rule 19 — Tables

**TYPE:** [CONVENTION]  
**RULE:** Dense desktop tables can use **12–14px** for cells and **12–14px medium/semibold** for headers. Prefer tabular figures for aligned numeric columns. Preserve row height and zoom behavior before shrinking below 12px.

**RATIONALE:** Productive design systems use 12–14px support/body sizes; tabular figures improve numeric alignment. Shrinking text is a poor first response to density.

**USE WHEN:** Analytics, finance, CRM, inventory, admin.

**AVOID WHEN:** 10–11px default table text for important data.

**EXCEPTIONS:** Extremely specialized data grids may use smaller text if the application provides robust user-controlled density/zoom and the audience explicitly prefers it.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S10], [S13], [S16], [S18]

---

## Rule 20 — Dashboard cards and KPI tiles

**TYPE:** [CONVENTION]  
**RULE:** Use at least three semantic levels: **metric**, **label/title**, and **supporting metadata**. Make changing numbers tabular. Do not enlarge every KPI to display scale; prominence should reflect decision importance.

**RATIONALE:** Atlassian provides dedicated Metric styles; Spectrum describes titles for high-signal card concepts; Vercel includes tabular label styles.

**USE WHEN:** Analytics and operational dashboards.

**AVOID WHEN:** Every card having a 48–72px number regardless of information priority.

**EXCEPTIONS:** Executive summary dashboards can intentionally use larger metrics.

**CONFIDENCE:** HIGH

**SOURCES:** [S11], [S13], [S15]

---

## Rule 21 — Cards

**TYPE:** [CONVENTION]  
**RULE:** A standard card usually needs a title style plus body/supporting text, not a custom miniature type scale. Typical pairing: title **14–18px / 500–700**, supporting body **13–16px / 400**.

**RATIONALE:** Spectrum’s documented card example uses Title + Body to create scan hierarchy. Atlassian and Material similarly use title/body semantic roles.

**USE WHEN:** Resource cards, project cards, settings cards.

**AVOID WHEN:** Five or more type sizes inside a small card.

**EXCEPTIONS:** Data visualization cards may also need metric and caption roles.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S11], [S12], [S17]

---

## Rule 22 — Modals and dialogs

**TYPE:** [CONVENTION]  
**RULE:** Modal headings should usually be **18–24px**, body **14–16px**, controls **14–16px**. Give explanatory body copy more line height than compact UI labels.

**RATIONALE:** Atlassian maps its medium heading to large component headers such as modal dialogs; Vercel notes 16px copy works well in simpler, larger views like modals.

**USE WHEN:** Dialogs, confirmations, focused forms.

**AVOID WHEN:** Huge marketing-style headings in transactional dialogs.

**EXCEPTIONS:** On mobile, modal/sheet title sizes can follow native platform text styles.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S11], [S13]

---

## Rule 23 — Notifications, toasts, and alerts

**TYPE:** [CONVENTION]  
**RULE:** Prioritize glanceability: normally **14–16px** for the main message, with concise supporting text at **12–14px** if needed. Weight only the highest-signal fragment.

**RATIONALE:** Notifications are transient and should be readable quickly. Research on glanceable text supports larger, non-condensed type. Mature systems keep alert typography close to body/component scales rather than caption scale.

**USE WHEN:** Toasts, banners, validation feedback.

**AVOID WHEN:** 11–12px primary notification text, all caps, condensed display fonts.

**EXCEPTIONS:** Persistent low-priority status labels can be smaller.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S14], [S15], [S25]

---

## Rule 24 — Charts

**TYPE:** [CONVENTION]  
**RULE:** Axis labels and legends may be compact (**11–13px**) but must remain readable and high enough contrast. Important values should use **12–16px+**. Use tabular figures where values align or update.

**RATIONALE:** Charts are spatially constrained, but text still conveys data. WCAG text contrast applies to rendered text; non-text graphical information has additional contrast requirements outside this document.

**USE WHEN:** Analytics charts and monitoring dashboards.

**AVOID WHEN:** Shrinking chart labels until they become decorative rather than readable.

**EXCEPTIONS:** Interactive hover/focus details can reveal full labels where dense axes must abbreviate, provided the chart remains understandable.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S01], [S15], [S18]

---

## Rule 25 — Tooltips

**TYPE:** [CONVENTION]  
**RULE:** Use compact but readable text, generally **12–14px**, with ordinary casing and enough line height for two or more lines.

**RATIONALE:** Tooltips are secondary but often explain unfamiliar controls, so they should not use “fine print” styling that defeats their purpose.

**USE WHEN:** Short contextual explanations.

**AVOID WHEN:** 10px text, low contrast, long prose, decorative fonts.

**EXCEPTIONS:** Native platforms should use platform conventions.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S01], [S09], [S10]

---

## Rule 26 — Mobile interfaces

**TYPE:** [RESEARCH + CONVENTION]  
**RULE:** Use scalable platform-aware text. For primary mobile body/UI text, start around **16–17sp/pt**; reserve **11–13** for captions/metadata. Allow layouts to grow or stack as text size increases.

**RATIONALE:** Apple lists 17pt as iOS/iPadOS default and 11pt as minimum; Material Body Large is 16sp. Apple explicitly recommends layouts that grow vertically or stack when Dynamic Type increases text.

**USE WHEN:** iOS, Android, responsive touch UI.

**AVOID WHEN:** Desktop-sized 12–13px primary UI simply scaled onto mobile.

**EXCEPTIONS:** Compact native controls may use platform-defined smaller text styles.

**CONFIDENCE:** HIGH

**SOURCES:** [S03], [S05], [S12]

---

# 3. TYPOGRAPHIC SCALE

## Cross-system comparison

| System | Product/body anchors | Large/display behavior | Notable lesson |
|---|---:|---:|---|
| Material 3 | 12/16, 14/20, 16/24 | 24–57sp headline/display | 15 semantic roles; size + weight + tracking |
| Fluent Web | Body 14/20; subtitles 16–20 | 24–68px | Product UI can be compact without being tiny |
| Carbon | Productive base 14; expressive base 16 | headings into 40–50px+ | Explicit productive vs expressive typography |
| Atlassian | Body 12/16, 14/20, 16/24 | headings 12–32 | 14px default components, 16px long-form |
| GOV.UK | Body 19/25, small 16/20 | headings 24–48, exceptional 80 | Content/service reading favors larger text |
| Vercel Geist | copy 13/14/16; button 12/14/16 | headings 14–72 | Distinguishes Label, Copy, Button, Heading |
| Adobe Spectrum | base 14; body commonly 16 at M | 10–73 scale | 1.125 scale, semantic role + t-shirt sizes |
| GitHub Primer | semantic rem tokens | product-specific | Uses rem, unitless line-height, ~80-char guidance |

**Interpretation:** There is no single “correct” modular scale for SaaS. Mature systems constrain the option set, attach semantics, and adapt density.

---

## Rule 27 — Use a small core scale for product UI

**TYPE:** [CONVENTION]  
**RULE:** Most SaaS product surfaces should be constructible from roughly **5–7 frequently used size steps**, even if the design system exposes more.

**RATIONALE:** Too many simultaneous type sizes weaken hierarchy. Material’s older guidance explicitly warns that too many sizes/styles can wreck layout; Spectrum says a single product does not need all available sizes.

**USE WHEN:** Product UI.

**AVOID WHEN:** Creating one-off values such as 13, 14, 15, 16, 17, 18, 19 all in the same screen.

**EXCEPTIONS:** Marketing systems may legitimately need more display steps.

**CONFIDENCE:** HIGH

**SOURCES:** [S15], [S28]

---

## Recommended product scale ranges

These are **AI decision ranges**, not standards:

| Role | Dense desktop SaaS | Standard SaaS | Mobile / reading-forward |
|---|---:|---:|---:|
| Caption / tertiary | 12/16 | 12–13/16–18 | 12–13/16–18 |
| Label / compact UI | 12–14/16–20 | 13–14/18–20 | 14–16/20–22 |
| Body secondary | 13–14/18–20 | 14/20 | 15–16/21–24 |
| Body primary | 14/20 | 16/24 | 16–17/22–26 |
| Small title | 14–16/20–22 | 16–18/22–26 | 17–20/23–28 |
| Section heading | 18–20/24–28 | 20–24/28–32 | 20–28/28–36 |
| Page title | 24–32/32–40 | 28–36/36–44 | 28–36/34–44 |
| Display/hero | uncommon | 40–64 | 32–48 |

### Recommended simple token set

For a typical desktop SaaS:

```text
text-xs   = 12
text-sm   = 14
text-md   = 16
text-lg   = 20
text-xl   = 24
text-2xl  = 32
display   = 40–48 (only when needed)
```

The AI should not automatically expose every token in every screen.

---

# 4. BRAND PERSONALITY

The following mappings are **[STYLE]** unless explicitly noted. They are useful design heuristics, not scientific truths.

## Rule 28 — Brand personality modifies the expressive layer, not the minimum legibility layer

**TYPE:** [STYLE + CONVENTION]  
**RULE:** Express brand most strongly in display/headline roles. Keep body, controls, tables, and helper text conservative unless the brand font has proven small-size legibility.

**RATIONALE:** Apple recommends custom fonts for headlines/subheadings while retaining system fonts for small body/caption text when needed. Material similarly recommends expressive display faces while keeping smaller body roles highly legible.

**USE WHEN:** Strongly branded SaaS.

**AVOID WHEN:** Applying a decorative brand face to forms, tables, or dense dashboards.

**EXCEPTIONS:** A custom brand family designed specifically as a UI superfamily can be used throughout after testing.

**CONFIDENCE:** HIGH

**SOURCES:** [S04], [S27]

---

## Brand decision heuristics

| Personality | Good default direction | Avoid |
|---|---|---|
| Enterprise | neutral/humanist sans, stable widths, 400 + 600 hierarchy | novelty that lowers scanning efficiency |
| Premium | restrained high-quality sans or serif display + neutral UI sans | ultra-thin small text |
| Technical | functional sans + mono for code/identifiers | mono everywhere |
| Developer-focused | UI sans + strong mono companion; tabular metrics | fake “terminal” styling for normal prose |
| Futuristic | geometric/neo-grotesk or variable display treatment | experimental letterforms in dense UI |
| Friendly | humanist/rounded sans, open counters, moderate weight | childish display forms for critical tasks |
| Playful | expressive display family, color/weight variation | decorative body text |
| Trustworthy | familiar forms, conservative hierarchy, high contrast | novelty, low contrast, extreme tracking |
| Editorial | serif is valid for reading; sans for interface chrome | assuming serif automatically equals “premium” |
| Minimalist | one versatile family, few sizes, hierarchy via weight/space | making everything identical in weight/size |

### AI constraint

Never infer “trustworthy”, “premium”, “friendly”, etc. from font classification alone. Brand personality is created jointly by typography, color, spacing, copy, motion, imagery, and product behavior.

---

# 5. INFORMATION DENSITY

## Rule 29 — Reduce spacing before reducing primary text below the comfortable product range

**TYPE:** [CONVENTION]  
**RULE:** When a dashboard feels too loose, first tighten component padding, row height, gaps, and secondary content before shrinking important text.

**RATIONALE:** Mature productive systems such as Carbon achieve density using compact line heights and layout spacing while keeping body text around 14px.

**USE WHEN:** CRM, admin, analytics, professional tools.

**AVOID WHEN:** Solving density by making all text 11–12px.

**EXCEPTIONS:** User-selectable “compact density” modes may reduce both spacing and some secondary text.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S10], [S15]

---

## Density profiles for AI

### Dense dashboard

- Primary body/cells: **13–14px**
- Secondary labels: **12–13px**
- Line height: **1.3–1.45**
- Titles: **14–20px**, primarily differentiated by weight
- KPI metrics: **20–40px**, only for high-signal values
- Prefer 400 body + 500/600 emphasis
- Use tabular numerals
- Avoid expressive display fonts

### CRM

- Default UI/body: **14px / ~20px**
- Entity/page title: **24–32px**
- Table/list rows: **13–14px**
- Labels/helper: **12–14px**
- Preserve strong distinction between entity name, status, metadata, and actions

### Analytics

- Data cells/axis labels: **12–14px**
- Narrative interpretation: **14–16px**
- Metrics: semantic scale, not automatically huge
- Tabular figures strongly preferred
- Mono only when technical identifiers need it

### Developer tools

- UI chrome: **13–14px sans**
- Code: **12–14px mono** with sufficient line height
- Command output/logs: **12–14px mono**
- Documentation/explanations: **14–16px sans/serif**
- Do not make all UI monospace solely for “developer aesthetic”

### Simple productivity app

- Body/UI: **14–16px**
- Comfortable line height: **1.4–1.5**
- Fewer hierarchy levels
- Larger spacing can do more work than extra type sizes

### Landing page / marketing

- Body: **16–20px**
- Feature headings: **24–40px**
- Hero display: **40–72px desktop**, commonly **32–48px mobile**
- Wider expressive range allowed
- Keep CTA/component text closer to product UI scale

---

# 6. RESPONSIVE TYPOGRAPHY

## Rule 30 — Use relative units for web typography

**TYPE:** [RESEARCH + CONVENTION]  
**RULE:** Prefer `rem`/`em`-based typography tokens on the web so browser/user font settings can participate in scaling.

**RATIONALE:** Primer uses `rem` specifically for a more accessible browser zoom experience. GOV.UK outputs typography in relative units. WCAG techniques include relative font sizing.

**USE WHEN:** Web SaaS.

**AVOID WHEN:** Locking all text to fixed pixel assumptions and then preventing user resizing.

**EXCEPTIONS:** Design specs may document px equivalents for communication while implementation uses rem.

**CONFIDENCE:** HIGH

**SOURCES:** [S06], [S08]

---

## Rule 31 — Fluid typography is most useful for display/headings, not every UI label

**TYPE:** [CONVENTION]  
**RULE:** Use `clamp()` primarily where continuous scaling adds value: hero/display text and occasionally large headings. Keep most control labels and dense UI text on stable semantic tokens.

**RATIONALE:** Product UI benefits from predictable dimensions; display text benefits from responsive scaling across wide viewport ranges.

**USE WHEN:** Marketing pages, large page titles, editorial layouts.

**AVOID WHEN:** Buttons, inputs, table cells, compact nav items unless a tested system requires it.

**EXCEPTIONS:** Fully fluid design systems can work if carefully tested with zoom and localization.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S19], [S20]

---

## Rule 32 — Never use viewport-only font sizing that prevents user text enlargement

**TYPE:** [RESEARCH / ACCESSIBILITY]  
**RULE:** Do not use pure `vw`/`vh` as the primary font-size mechanism. A fluid `clamp()` should include relative font units and must be tested at 200% resizing/zoom.

**RATIONALE:** W3C documents misuse of viewport units as a WCAG 1.4.4 failure. MDN’s `clamp()` guidance recommends relative bounds and explicitly calls out 200% scaling.

**USE WHEN:** Implementing responsive type.

**AVOID WHEN:** `font-size: 2vw` for important text.

**EXCEPTIONS:** Decorative text that is not meaningful content may have more freedom, but should still not create layout failure.

**CONFIDENCE:** HIGH

**SOURCES:** [S19], [S20], [S21]

---

## Rule 33 — Constrain reading line length

**TYPE:** [RESEARCH + ACCESSIBILITY]  
**RULE:** For multi-line reading, target roughly **50–75 characters per line** as a practical default and ensure a mechanism can keep blocks at **≤80 characters** where WCAG AAA 1.4.8 is targeted.

**RATIONALE:** WCAG AAA specifies a mechanism for blocks of text to be no wider than 80 characters/glyphs (40 CJK). Baymard’s large-scale UX testing reports 50–75 characters as a strong practical range for body readability. Primer also recommends around 80 characters or less.

**USE WHEN:** Documentation, onboarding copy, settings explanations, marketing prose, long modal content.

**AVOID WHEN:** Stretching paragraphs across the entire desktop viewport.

**EXCEPTIONS:** Tables, code, data grids, charts, and deliberately horizontal formats are not ordinary reading columns.

**CONFIDENCE:** HIGH

**SOURCES:** [S07], [S08], [S26]

---

## Rule 34 — Responsive hierarchy should compress, not disappear

**TYPE:** [CONVENTION]  
**RULE:** On smaller screens, reduce the absolute gaps between display, headings, and body while preserving their ordering and semantic distinction.

**RATIONALE:** GOV.UK uses a responsive type scale where large headings shrink at small viewports while body anchors remain stable. Apple says relative hierarchy should remain visually distinct when text sizes change.

**USE WHEN:** Responsive SaaS and marketing pages.

**AVOID WHEN:** Making H1 and body nearly identical on mobile, or keeping a desktop 72px hero on a 320px screen.

**EXCEPTIONS:** Very short branded splash screens may intentionally preserve a large display moment.

**CONFIDENCE:** HIGH

**SOURCES:** [S04], [S16]

---

## Rule 35 — Let containers grow when text grows

**TYPE:** [RESEARCH / ACCESSIBILITY]  
**RULE:** Avoid fixed heights around text that can scale. At larger text sizes, rows may grow, labels may wrap, and horizontal groups may need to stack vertically.

**RATIONALE:** WCAG 1.4.4 requires 200% text resizing without loss of content/functionality. Apple explicitly recommends growing rows and stacking adjacent views for Dynamic Type.

**USE WHEN:** Buttons, form rows, cards, tabs, table-like lists, mobile layouts.

**AVOID WHEN:** `height` + `overflow:hidden` around user-facing text.

**EXCEPTIONS:** Intentional single-line truncation is acceptable in some UI components when the full value is available via focus/activation and functionality is preserved.

**CONFIDENCE:** HIGH

**SOURCES:** [S05], [S30]

---

# 7. ACCESSIBILITY & READABILITY

## Rule 36 — Meet WCAG text contrast before using “muted” typography

**TYPE:** [RESEARCH / STANDARD]  
**RULE:** Normal text must meet at least **4.5:1** contrast under WCAG 2.2 AA. Large-scale text may use **3:1**. Placeholder text is included.

**RATIONALE:** WCAG 2.2 SC 1.4.3.

**USE WHEN:** All product text.

**AVOID WHEN:** Styling secondary text by simply reducing opacity until it becomes faint.

**EXCEPTIONS:** Incidental/inactive/decorative text and logotypes have specific exemptions, but active information should not be treated as decorative.

**CONFIDENCE:** HIGH

**SOURCES:** [S01]

---

## Rule 37 — Support at least 200% text resizing without loss of content or function

**TYPE:** [RESEARCH / STANDARD]  
**RULE:** Test product UI at 200% text enlargement/zoom. No critical label, input, control, or content may become clipped, hidden, or unusable.

**RATIONALE:** WCAG 2.2 SC 1.4.4.

**USE WHEN:** Web applications and responsive UI.

**AVOID WHEN:** Declaring accessibility based only on visual inspection at 100%.

**EXCEPTIONS:** None for ordinary text covered by the criterion.

**CONFIDENCE:** HIGH

**SOURCES:** [S30]

---

## Rule 38 — Survive user text-spacing overrides

**TYPE:** [RESEARCH / STANDARD]  
**RULE:** The layout must not lose content or functionality when users apply at least: `line-height: 1.5`, paragraph spacing `2em`, letter spacing `0.12em`, word spacing `0.16em`.

**RATIONALE:** WCAG 2.2 SC 1.4.12.

**USE WHEN:** Web UI.

**AVOID WHEN:** Fixed-height buttons/labels that clip when spacing changes.

**EXCEPTIONS:** Language/script combinations that do not use one of these spacing properties.

**CONFIDENCE:** HIGH

**SOURCES:** [S02]

---

## Rule 39 — Avoid rasterized text when real text can achieve the design

**TYPE:** [RESEARCH / STANDARD]  
**RULE:** Use actual text rather than images of text whenever the technology can reproduce the presentation.

**RATIONALE:** WCAG 1.4.5 exists so users can resize/recolor/reformat text and assistive technologies can access it. Apple also recommends avoiding rasterized text in widgets.

**USE WHEN:** Marketing banners, product UI, charts, illustrations with labels.

**AVOID WHEN:** Baking headlines into PNG/SVG paths solely for visual consistency.

**EXCEPTIONS:** Logos and cases where the exact textual presentation is essential.

**CONFIDENCE:** HIGH

**SOURCES:** [S29], [S31]

---

## Rule 40 — Avoid sustained all-uppercase UI text

**TYPE:** [RESEARCH + ACCESSIBILITY CONVENTION]  
**RULE:** Prefer sentence case or natural casing for navigation, buttons, labels, alerts, and paragraphs. If all caps is used, keep it short and nonessential to reading flow.

**RATIONALE:** W3C menu guidance advises avoiding all-uppercase text; Fluent recommends sentence case; Spectrum discourages all caps inside UI components. Research on capitalization is nuanced for isolated/glanceable words, but continuous text and common accessibility guidance do not support all caps as a default.

**USE WHEN:** Normal interface copy.

**AVOID WHEN:** Paragraphs, menus, primary buttons, long labels.

**EXCEPTIONS:** Short eyebrow/overline labels or specialized display treatments can use uppercase with extra tracking and adequate size.

**CONFIDENCE:** HIGH for “do not use sustained all caps”; MEDIUM for exact exceptions.

**SOURCES:** [S09], [S15], [S25], [S32]

---

## Rule 41 — Do not automatically select “dyslexia fonts”

**TYPE:** [RESEARCH]  
**RULE:** Do not claim OpenDyslexic, Dyslexie, or another specialized font universally improves reading for dyslexic users. Prefer strong general typography and, where practical, user font/spacing preferences.

**RATIONALE:** A 2026 meta-analysis of 15 empirical studies found no consistent or reliable reading-speed or accuracy benefit from dyslexia-specific fonts. Earlier controlled studies of OpenDyslexic and Dyslexie likewise found no improvement. Some individual studies report benefits, so the correct conclusion is not “they never help,” but “do not impose them as a proven default.”

**USE WHEN:** Accessibility logic, education tools, user-preference systems.

**AVOID WHEN:** Marketing a font switch as an evidence-based dyslexia cure.

**EXCEPTIONS:** If a user explicitly prefers a specialized font, honor the preference where feasible.

**CONFIDENCE:** HIGH

**SOURCES:** [S33], [S34], [S35]

---

## Rule 42 — Do not justify long digital body text by default

**TYPE:** [RESEARCH + ACCESSIBILITY]  
**RULE:** Left-align LTR body text and right-align RTL body text. Avoid full justification for ordinary web paragraphs.

**RATIONALE:** WCAG AAA 1.4.8 includes non-justified text as a visual presentation target; GOV.UK warns that justification creates uneven word spacing and can make text harder to read.

**USE WHEN:** Documentation, settings copy, marketing body text, modals.

**AVOID WHEN:** Standard product body copy.

**EXCEPTIONS:** Carefully typeset editorial layouts with hyphenation and professional justification may be acceptable, but should not be the default SaaS behavior.

**CONFIDENCE:** HIGH

**SOURCES:** [S07], [S36]

---

# 8. FONT PERFORMANCE

## Rule 43 — Use system fonts when brand value does not justify a web-font cost

**TYPE:** [CONVENTION + PERFORMANCE]  
**RULE:** If typography is not a core brand differentiator, a strong `system-ui` stack is a valid default for product UI.

**RATIONALE:** Fluent uses native type on each platform for familiar, accessible experiences. System fonts avoid font downloads and can inherit platform-native optimization.

**USE WHEN:** Internal tools, performance-sensitive apps, prototypes, products where brand typography is secondary.

**AVOID WHEN:** A distinctive typeface is central to product identity and budget allows it.

**EXCEPTIONS:** A custom font may still be justified if its metrics improve the specific product or its license/performance is well managed.

**CONFIDENCE:** HIGH

**SOURCES:** [S09], [S27]

---

## Rule 44 — Prefer WOFF2 for web font delivery

**TYPE:** [RESEARCH / WEB STANDARD]  
**RULE:** Serve web fonts in WOFF2 where supported.

**RATIONALE:** WOFF2 is a W3C Recommendation implemented in major browsers and uses improved compression.

**USE WHEN:** Self-hosted/custom web fonts.

**AVOID WHEN:** Shipping raw desktop TTF/OTF files as the primary web format.

**EXCEPTIONS:** Legacy browser requirements may require fallback formats, though modern SaaS often does not need them.

**CONFIDENCE:** HIGH

**SOURCES:** [S37]

---

## Rule 45 — Use variable fonts when you actually need multiple weights/styles/axes

**TYPE:** [RESEARCH + PERFORMANCE]  
**RULE:** Prefer a variable font when the product would otherwise load several static weights/styles. Do not assume a variable font is automatically smaller if only one weight is needed.

**RATIONALE:** MDN and web.dev note that one variable file can replace many static files and can be smaller than their combined size, but may be larger than a single static face.

**USE WHEN:** A family needs regular, medium, semibold, bold, optical size, or width variation.

**AVOID WHEN:** The interface only needs one or two static faces and the variable file is substantially larger.

**EXCEPTIONS:** A variable font may still be chosen for optical sizing or fine-grained width/grade control even without a raw size win.

**CONFIDENCE:** HIGH

**SOURCES:** [S38], [S39]

---

## Rule 46 — Limit the number of actually downloaded styles

**TYPE:** [PERFORMANCE CONVENTION]  
**RULE:** Product UI usually needs **2–3 effective weights**: regular plus one emphasis weight, with bold added only if necessary. Do not download every available weight because the font offers it.

**RATIONALE:** Each static font file adds transfer and request cost; variable fonts can mitigate this but can also contain unused data. Most mature UI systems rely heavily on regular and medium/semibold.

**USE WHEN:** Web product implementation.

**AVOID WHEN:** Loading 300/400/500/600/700/800 plus italics “just in case.”

**EXCEPTIONS:** Editorial or marketing sites may need a richer typographic palette.

**CONFIDENCE:** MEDIUM

**SOURCES:** [S09], [S10], [S38], [S39]

---

## Rule 47 — Use `font-display` deliberately so text remains visible

**TYPE:** [PERFORMANCE]  
**RULE:** Prefer `font-display: swap` or `optional` depending on whether the custom font must eventually replace the fallback. Do not leave critical text invisible while waiting for a font.

**RATIONALE:** Chrome performance guidance recommends `swap` or `optional`; web.dev explains how `font-display` controls blank text and font swapping.

**USE WHEN:** Web fonts.

**AVOID WHEN:** Long FOIT (flash of invisible text).

**EXCEPTIONS:** A short block period may be acceptable in rare tightly branded contexts, but should be measured.

**CONFIDENCE:** HIGH

**SOURCES:** [S40], [S41]

---

## Rule 48 — Match fallback metrics to reduce layout shift

**TYPE:** [PERFORMANCE]  
**RULE:** Choose metrically similar fallbacks and, when supported/appropriate, use `size-adjust`, `ascent-override`, `descent-override`, and `line-gap-override` to reduce font-swap CLS.

**RATIONALE:** Chrome and MDN document metric overrides specifically for matching fallback and primary fonts and mitigating layout shift.

**USE WHEN:** Important web fonts loaded after initial render.

**AVOID WHEN:** Arbitrary fallback stacks whose x-height and widths differ dramatically from the final font.

**EXCEPTIONS:** `font-display: optional` may avoid a late swap entirely in some conditions.

**CONFIDENCE:** HIGH

**SOURCES:** [S42], [S43], [S44]

---

## Rule 49 — Preload only fonts that are truly critical

**TYPE:** [PERFORMANCE]  
**RULE:** Do not preload every weight. Preload only fonts highly likely to be required above the fold.

**RATIONALE:** web.dev warns that preload consumes browser priority and bypasses some negotiation behavior; it should be used selectively.

**USE WHEN:** One critical brand/UI font needed immediately.

**AVOID WHEN:** Preloading a full family or rarely used italic/bold variants.

**EXCEPTIONS:** Highly controlled single-page experiences may justify more aggressive preloading after measurement.

**CONFIDENCE:** HIGH

**SOURCES:** [S41]

---

## Rule 50 — Subset by script/language carefully, never by wishful thinking

**TYPE:** [PERFORMANCE + INTERNATIONALIZATION]  
**RULE:** Use Unicode subsetting when it materially reduces payload, but ensure the actual supported languages, punctuation, symbols, and user-generated content remain covered.

**RATIONALE:** Large multilingual fonts can be very heavy; web font APIs and `unicode-range` can reduce transferred glyph data. However, missing glyphs cause fallback inconsistency and broken brand/UI appearance.

**USE WHEN:** Large CJK/multiscript families or known locale bundles.

**AVOID WHEN:** Latin-only subsetting for a product that accepts international names or content.

**EXCEPTIONS:** Locale-specific builds can safely load different subsets if fallback behavior is verified.

**CONFIDENCE:** HIGH

**SOURCES:** [S39], [S45]

---

# 9. REAL SaaS / PRODUCT ANALYSIS

This section extracts decision patterns, not visual trends.

## GitHub / Primer

**Observed system**
- Primary stack currently includes **Mona Sans VF** followed by system fallbacks.
- Dedicated system monospace stack.
- Typography tokens use `rem`.
- Unitless line heights.
- Primer recommends keeping reading lines around **80 characters or less**.
- Hierarchy should not depend primarily on color.

**AI lesson**
- Developer products benefit from a neutral UI sans + dedicated mono.
- Accessibility can be encoded directly into token implementation (`rem`, unitless line-height).
- “Developer aesthetic” does not require monospace everywhere.

**SOURCES:** [S08]

---

## Vercel / Geist

**Observed system**
- Geist Sans + Geist Mono were designed for developer/designer contexts.
- Semantic classes distinguish Heading, Button, Label, and Copy.
- Default button is 14px; 12px is reserved for tiny embedded buttons.
- 14px label is described as one of the most common styles.
- Copy uses more line-height than labels.
- Tabular numerals appear in data-oriented label styles.
- Marketing headings extend up to 72px.

**AI lesson**
- Separate “single-line UI label” from “multiline copy” even when sizes are similar.
- Developer SaaS can be dense without making all text monospace or tiny.
- Marketing scale can be much more expressive than the product scale while still sharing a family.

**SOURCES:** [S13], [S46]

---

## Atlassian

**Observed system**
- Product fonts: Atlassian Sans + Atlassian Mono.
- Marketing/brand font is separated from app typography.
- Body L: 16/24 for long-form reading.
- Body M: 14/20 default component text.
- Body S: 12/16 secondary content, “use sparingly.”
- Semantic heading tokens map to page titles, modals, small components, and brand/marketing moments.

**AI lesson**
- One brand can legitimately maintain separate marketing and product typographic strategies.
- Density can be represented semantically instead of by arbitrary per-component font-size overrides.

**SOURCES:** [S11], [S47]

---

## Notion

**Observed system**
- Users can choose Default, Serif, or Mono typography for page content.
- A “Small text” option lets users increase information density.
- Page content and application UI are not forced into one immutable typographic personality.

**AI lesson**
- User preference can be a first-class typography variable.
- Serif/mono options can be appropriate for authored content without implying that the entire product chrome should switch.
- Density can be user-controlled rather than hardcoded.

**SOURCES:** [S48]

---

## Adobe Spectrum

**Observed system**
- Clear semantic roles: Heading, Title, Body, Detail, Component, Code, Monospace numbers.
- Body and Code use 1.5× line-height; CJK body can use 1.7×.
- Regular is default for body/editable text; Medium/Bold are used selectively for controls and high-signal concepts.
- A 1.125 (“Major Second”) size progression underpins the larger token set.
- Spectrum explicitly says one product does not need to use every available size.

**AI lesson**
- Large design systems can expose many tokens while individual products use a constrained subset.
- Script-aware line-height belongs in the typography model.
- Numeric typography deserves its own semantic role.

**SOURCES:** [S15], [S17], [S18]

---

## Carbon / IBM product ecosystem

**Observed system**
- Explicit **Productive** and **Expressive** type sets.
- Productive base: 14px.
- Expressive base: 16px.
- Compact body and long body use different line heights.
- Productive headings can remain small while using weight for hierarchy.

**AI lesson**
- “Product UI” and “marketing/editorial UI” should not be forced onto the same density model.
- Density should be an explicit system variable.

**SOURCES:** [S10]

---

# 10. FAILURE MODES

## Anti-pattern A — Too many sizes

**DETECT:** More than ~6–7 visibly active size steps on one product screen, or many one-off values differing by 1px.

**WHY IT FAILS:** Hierarchy becomes noisy and designers/developers lose a shared semantic system.

**FIX:** Collapse values into semantic tokens; differentiate with weight and spacing where possible.

**CONFIDENCE:** HIGH

---

## Anti-pattern B — Too many weights

**DETECT:** 300/400/500/600/700/800 all appear in normal product UI.

**WHY IT FAILS:** Visual distinctions become subtle/inconsistent and web-font payload grows.

**FIX:** Start with 400 + 600; add 500 or 700 only if the chosen family needs them.

**CONFIDENCE:** MEDIUM

---

## Anti-pattern C — Faint gray secondary text

**DETECT:** Important metadata, placeholders, or helper text below 4.5:1 contrast while not qualifying as large text.

**WHY IT FAILS:** WCAG failure and reduced readability.

**FIX:** Preserve hierarchy using size/weight/spacing first; keep contrast compliant.

**CONFIDENCE:** HIGH

---

## Anti-pattern D — Gigantic product headings

**DETECT:** 48–72px headings inside routine settings, CRM, or operational screens.

**WHY IT FAILS:** Consumes working area and exaggerates low-value hierarchy.

**FIX:** Reserve display scale for marketing, onboarding moments, or true high-level summaries. Product page titles usually live around 24–36px.

**CONFIDENCE:** MEDIUM

---

## Anti-pattern E — UI text too small

**DETECT:** 10–11px used for primary controls/body; 12px used everywhere to “fit more.”

**WHY IT FAILS:** Density is being solved at the expense of legibility.

**FIX:** Return primary UI to 14px+ web / platform defaults; reduce padding and secondary clutter.

**CONFIDENCE:** HIGH

---

## Anti-pattern F — Excessive uppercase

**DETECT:** Navigation, buttons, table headers, alerts, and labels all rendered in caps.

**WHY IT FAILS:** Creates visual shouting, reduces normal word patterns, and conflicts with multiple accessibility/system guidelines.

**FIX:** Use sentence case; reserve caps for very short overlines/eyebrows.

**CONFIDENCE:** HIGH

---

## Anti-pattern G — Wrong line-height everywhere

**DETECT:** One global `line-height: 1.2` or `1.5` applied to every role.

**WHY IT FAILS:** 1.2 can crush paragraphs; 1.5 can make compact buttons/tables feel vertically unstable.

**FIX:** Role-based leading: tighter for one-line UI, looser for body.

**CONFIDENCE:** HIGH

---

## Anti-pattern H — Decorative font in dense product UI

**DETECT:** Geometric/display/handwritten/contrast-heavy face used in tables, forms, or long settings copy.

**WHY IT FAILS:** Brand expression overrides scan efficiency.

**FIX:** Restrict expressive face to display/title roles; use UI workhorse for components.

**CONFIDENCE:** HIGH

---

## Anti-pattern I — Marketing and product feel like unrelated companies

**DETECT:** Different families, capitalization conventions, weight logic, and hierarchy with no shared tokens or brand bridge.

**WHY IT FAILS:** Weakens perceived product coherence.

**FIX:** Keep at least one shared dimension: family/superfamily, weight language, numeric style, or heading character. Allow marketing to be more expressive without abandoning the product identity.

**CONFIDENCE:** MEDIUM

---

## Anti-pattern J — Product and marketing forced into identical typography

**DETECT:** Dense dashboard uses the same 64px headings and oversized body scale as the landing page, or marketing is constrained to 14px product typography.

**WHY IT FAILS:** The two contexts have different density and communication goals.

**FIX:** Share semantic foundations but expose productive and expressive modes.

**CONFIDENCE:** HIGH

---

# 11. TYPOGRAPHY DECISION TREE

```text
START
│
├─ 1. What platform?
│   ├─ iOS/iPadOS → prefer system text styles / Dynamic Type; ~17pt primary default
│   ├─ Android → use sp + Material/platform scaling; ~16sp primary body
│   └─ Web/Desktop → continue
│
├─ 2. What is the text role?
│   ├─ code/command/hash → monospace
│   ├─ aligned/changing number → primary family + tabular nums
│   ├─ long-form reading → body role, 16px-ish default, ~1.45–1.6 line-height
│   ├─ compact UI/control → label/component role, 13–14px dense or 14–16px standard
│   └─ display/marketing → expressive role allowed
│
├─ 3. Information density?
│   ├─ high (CRM/analytics/devtool) → 14px productive base, 12–13px secondary
│   ├─ standard SaaS → 14–16px base
│   └─ reading/marketing → 16–20px body, larger headings
│
├─ 4. Brand requirement?
│   ├─ weak → system-ui or proven UI sans
│   ├─ strong custom family with good UI legibility → may use across product
│   └─ expressive/custom display only → pair with conservative UI/body family
│
├─ 5. Need multiple weights/styles?
│   ├─ yes → evaluate variable font
│   └─ no → static or system font may be smaller/faster
│
├─ 6. Need responsive display scaling?
│   ├─ yes → clamp(rem, rem + vw, rem), then test 200% zoom
│   └─ no → stable semantic rem token
│
├─ 7. Is content multiline?
│   ├─ yes → line-height ~1.4–1.6; constrain line length
│   └─ no → compact role-specific line-height
│
├─ 8. Is text critical/interactive?
│   ├─ yes → never style it as faint fine print; maintain WCAG contrast
│   └─ secondary → can reduce size/prominence within accessibility constraints
│
└─ 9. Validate:
    - 200% resize
    - text spacing override
    - localization / long strings
    - dark/light contrast
    - slow font load / fallback
    - mobile width
    - CJK/tall-script metrics where supported
END
```

---

# 12. RECOMMENDED TYPOGRAPHY SCALE RANGES

## Dense SaaS product

```yaml
caption:       12px / 16px / 400
label-small:   12px / 16px / 500
label:         13-14px / 18-20px / 500
body:          14px / 20px / 400
title-small:   14-16px / 20-22px / 600
heading-small: 18-20px / 24-28px / 600
page-title:    24-32px / 32-40px / 600-700
```

## Standard SaaS product

```yaml
caption:       12-13px / 16-18px / 400
label:         14px / 20px / 500-600
body:          16px / 24px / 400
body-small:    14px / 20px / 400
title:         16-20px / 22-28px / 600
h3:            20-24px / 28-32px / 600
h2:            24-32px / 32-40px / 600-700
h1:            32-40px / 40-48px / 600-700
```

## Marketing / expressive

```yaml
body:          16-20px / 24-30px / 400
eyebrow:       12-14px / 16-20px / 600
feature-title: 24-40px / 30-48px / 600-700
hero-mobile:   32-48px / 36-54px
hero-desktop:  48-72px / 52-78px
```

**AI caution:** These are ranges. The chosen font’s x-height, width, optical size, and weight distribution can shift the visually equivalent result.

---

# 13. DASHBOARD TYPOGRAPHY RULES

1. Use **14px** as the default starting point for dense desktop body/cell text.
2. Use **12–13px** only for secondary metadata, captions, and low-priority chart labels.
3. Use **500–600** weight for column headers, active navigation, and card titles instead of adding unnecessary larger sizes.
4. Use **tabular numerals** for values compared vertically or values that update.
5. Do not use monospace for all numeric data if the primary family has tabular figures.
6. Keep KPI sizes proportional to importance; not every number is a hero.
7. Use compact line-height for single-line rows, but never clip at 200% resize.
8. Preserve at least 4.5:1 contrast for ordinary text, including helper and placeholder text.
9. Avoid uppercase table headers as a default.
10. If the screen feels crowded, remove low-value metadata or tighten spacing before shrinking primary text.

---

# 14. MARKETING TYPOGRAPHY RULES

1. Marketing may use a separate **expressive scale** from the product UI.
2. Display typography can be custom, serif, geometric, variable, or otherwise branded if short and legible.
3. Body copy remains a reading task; keep it conservative and comfortably spaced.
4. Typical marketing body starts at **16–20px**.
5. Hero headings may reach **48–72px desktop**, but scale down on mobile.
6. Use fluid `clamp()` only with accessible relative-unit behavior and 200% testing.
7. Do not stretch paragraphs across wide screens; target ~50–75 characters.
8. Keep CTA typography closer to product component scale: usually **14–16px / 500–600**.
9. Do not let brand typography force low-contrast thin text.
10. Marketing and product can differ in scale while sharing family, weight language, or other brand DNA.

---

# 15. RESPONSIVE RULES

1. Implement web tokens in `rem` where practical.
2. Keep core body size relatively stable; make large headings more responsive than labels.
3. Use `clamp()` primarily for display/headline roles.
4. Never use `vw`-only meaningful font sizes.
5. Test at **200% text resize/zoom**.
6. Test **320 CSS px width** / narrow mobile.
7. Test longest supported localization strings.
8. Allow rows/cards/modals to grow vertically.
9. Convert side-by-side label/value layouts to stacked layouts when large text requires it.
10. Preserve semantic hierarchy even when the scale compresses.
11. Increase leading for CJK/tall scripts when the chosen font requires it.
12. Avoid truncating critical controls; if truncation is unavoidable, expose the full text on focus/activation.

---

# 16. ACCESSIBILITY CHECKLIST

```text
[ ] Normal text contrast >= 4.5:1
[ ] Large text contrast >= 3:1 when using the WCAG large-text exception
[ ] Placeholder/helper text contrast checked
[ ] 200% text resize causes no loss of content/function
[ ] 320px/reflow behavior tested where applicable
[ ] Layout survives line-height 1.5
[ ] Layout survives letter-spacing 0.12em
[ ] Layout survives word-spacing 0.16em
[ ] Layout survives paragraph spacing 2em
[ ] Long reading blocks can stay <= 80 characters when targeting WCAG AAA visual presentation
[ ] Normal body text is not fully justified
[ ] Critical UI is not all caps
[ ] No thin/light small text
[ ] No important text baked into raster images
[ ] User font settings are not overridden by viewport-only sizing
[ ] Dynamic Type / sp scaling is supported on native mobile
[ ] Font fallback does not hide text or destroy layout
[ ] Dyslexia-specific font is not imposed as a false universal accessibility fix
[ ] Localization/scripts tested
```

---

# 17. AI-READY RULES

The following rules are intentionally phrased for direct conversion into an agent Skill.

```yaml
priority:
  - accessibility
  - semantic_role
  - platform
  - density
  - content_length
  - localization
  - performance
  - brand
  - aesthetics

families:
  default_max_ui_families: 1
  allow_second_family_if:
    - display_brand_role
    - editorial_reading_role
    - code_role
  mono_only_for:
    - code
    - shell
    - identifiers
    - alignment_sensitive_technical_content

weights:
  body_default: 400
  ui_emphasis: [500, 600]
  strong_heading: [600, 700]
  prohibit_small_text_weights_below: 400

web_product_density:
  dense:
    primary_body_px: [13, 14]
    preferred_body_px: 14
    secondary_px: [12, 13]
  standard:
    primary_body_px: [14, 16]
    preferred_body_px: 16
  reading:
    primary_body_px: [16, 20]

line_height:
  one_line_ui_ratio: [1.2, 1.4]
  compact_multiline_ratio: [1.3, 1.45]
  long_body_ratio: [1.45, 1.6]
  cjk_long_body_ratio: [1.5, 1.7]

controls:
  button_px: [14, 16]
  input_px: [14, 16]
  label_px: [12, 14]
  tooltip_px: [12, 14]
  notification_primary_px: [14, 16]

tables:
  cell_px: [12, 14]
  preferred_cell_px: 14
  numeric_feature: tabular-nums

responsive:
  use_relative_units: true
  allow_fluid_for:
    - display
    - large_heading
  prohibit_vw_only_font_size: true
  test_resize_percent: 200

readability:
  body_line_chars_preferred: [50, 75]
  body_line_chars_accessible_max_target: 80
  body_text_justified_default: false
  sustained_all_caps: false

contrast:
  normal_text_min: "4.5:1"
  large_text_min: "3:1"

performance:
  preferred_web_format: WOFF2
  font_display: [swap, optional]
  preload_only_critical: true
  variable_font_when_multiple_styles_needed: true
  metric_match_fallback: true

brand:
  apply_expressive_font_first_to:
    - display
    - heading
  keep_body_and_controls_legible: true
  never_override_accessibility_for_brand: true
```

---

# 18. AGENT DECISION POLICY

An AI generating a SaaS interface should perform the following reasoning sequence:

### A. Classify the product

```text
dense operational tool
standard productivity SaaS
developer tool
content/editorial product
marketing surface
mobile-first product
```

### B. Classify every text instance

```text
display
page heading
section heading
card title
body
secondary body
label
caption
button
input value
helper/error
navigation
table header
table cell
metric
code
numeric data
chart label
tooltip
notification
```

### C. Choose the smallest sufficient token set

The agent should first attempt to build the screen with:

```text
caption
label
body
title
heading
page-title
metric/code when needed
```

It should add a new token only if no existing semantic role can express the needed hierarchy.

### D. Apply density

- Dense tool → 14px productive base.
- Standard SaaS → 14–16px.
- Reading-forward surface → 16px+.
- Mobile → platform scaling, typically 16–17 primary.

### E. Apply brand

Brand may change:
- family,
- display weight,
- display tracking,
- heading style,
- optical axis,
- serif/sans classification.

Brand may **not** remove:
- contrast,
- readable primary size,
- user scaling,
- clear hierarchy,
- localization support.

### F. Validate

The agent must reject its own typography system if any of these occurs:

```text
primary UI < 12px
important text contrast below WCAG AA
thin small text
body paragraphs in all caps
body line > ~80 chars without a reason
viewport-only font sizing
fixed-height clipping at 200%
more than ~7 active size steps without strong justification
decorative display font used throughout a dense dashboard
many webfont weights loaded without use
fallback causes significant layout shift
```

---

# 19. ANTI-PATTERNS — MACHINE-DETECTABLE SUMMARY

```yaml
anti_patterns:
  too_many_sizes:
    trigger: "screen uses >7 active font-size values or repeated one-off adjacent values"
    action: "collapse into semantic scale"

  too_many_weights:
    trigger: "normal product UI uses >=5 distinct font weights"
    action: "reduce toward regular + emphasis + optional strong"

  low_contrast_secondary_text:
    trigger: "meaningful normal text contrast <4.5:1"
    action: "increase luminance contrast; preserve hierarchy via other signals"

  giant_product_heading:
    trigger: "routine app page title >40px without expressive reason"
    action: "reduce to product title range"

  tiny_primary_ui:
    trigger: "primary web body/control text <=11px"
    action: "increase size; recover density from spacing/layout"

  excessive_uppercase:
    trigger: "multiword navigation/buttons/body use sustained uppercase"
    action: "use sentence/natural case"

  bad_line_height:
    trigger: "multiline body <1.3 or global leading ignores semantic role"
    action: "assign role-based line-height"

  decorative_dense_ui:
    trigger: "display/decorative family used for tables/forms/long settings copy"
    action: "use legible UI workhorse for dense roles"

  marketing_product_mismatch:
    trigger: "no shared typographic DNA between landing and app"
    action: "share family/superfamily or hierarchy/weight logic"

  marketing_product_overmerge:
    trigger: "marketing and dashboard forced onto identical scale"
    action: "create productive and expressive modes"

  font_performance_overload:
    trigger: "unused font variants preload/download"
    action: "subset styles; consider variable font or system stack"

  inaccessible_fluid_type:
    trigger: "font-size uses only vw/vh"
    action: "use relative-unit clamp and test 200%"
```

---

# 20. WHAT IS RESEARCH VS CONVENTION VS STYLE?

## Strong research / standards

- WCAG contrast thresholds.
- 200% text resizing.
- Text-spacing override tolerance.
- Avoid images of text where real text works.
- Viewport-only typography can fail resize requirements.
- Dyslexia-specific fonts do not have reliable universal benefit.
- Serif vs sans-serif is not a universal screen-legibility rule.

## Strong design-system conventions

- Semantic type tokens.
- One primary UI family plus optional mono/display family.
- 14px productive body for dense desktop tools.
- 16px-ish body for general reading/product contexts.
- Regular body + medium/semibold UI emphasis.
- Dedicated tabular/numeric styles.
- Tighter UI leading, looser body leading.
- Smaller product scale, larger marketing scale.

## Style preferences only

- Serif = premium.
- Geometric sans = futuristic.
- Rounded sans = friendly.
- Mono = technical.
- Tight display tracking = modern.
- Huge headings = premium/minimal.
- All-lowercase branding = contemporary.

An AI may use these stylistic associations only when they match the stated brand direction. It must never present them as universal usability truths.

---

# 21. SOURCE REGISTRY

**Primary standards and platform guidance**

- **[S01] W3C — WCAG 2.2, Understanding SC 1.4.3 Contrast (Minimum).**  
  https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum

- **[S02] W3C — WCAG 2.2, Understanding SC 1.4.12 Text Spacing.**  
  https://www.w3.org/WAI/WCAG22/Understanding/text-spacing

- **[S03] Apple — Human Interface Guidelines: Accessibility.**  
  https://developer.apple.com/design/human-interface-guidelines/accessibility

- **[S04] Apple — Human Interface Guidelines: Typography / accessibility typography guidance.**  
  https://developer.apple.com/design/human-interface-guidelines/typography

- **[S05] Apple — Human Interface Guidelines: Layout, Dynamic Type adaptation.**  
  https://developer.apple.com/design/human-interface-guidelines/layout

- **[S06] W3C — WCAG techniques / Resize Text.**  
  https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html

- **[S07] W3C — Understanding SC 1.4.8 Visual Presentation.**  
  https://www.w3.org/WAI/WCAG21/Understanding/visual-presentation

**Official design systems**

- **[S08] GitHub Primer — Typography.**  
  https://primer.style/product/getting-started/foundations/typography/

- **[S09] Microsoft Fluent 2 — Typography.**  
  https://fluent2.microsoft.design/typography

- **[S10] IBM Carbon — Typography / type sets.**  
  https://www.carbondesignsystem.com/building-blocks/foundations/typography/type-sets

- **[S11] Atlassian Design System — Typography.**  
  https://atlassian.design/foundations/typography

- **[S12] Android Developers — Material 3 typography scale.**  
  https://developer.android.com/develop/ui/compose/designsystems/material3

- **[S13] Vercel Geist — Typography.**  
  https://vercel.com/geist/typography

- **[S14] Nielsen Norman Group — Typography for Glanceable Reading.**  
  https://www.nngroup.com/articles/glanceable-fonts/

- **[S15] Adobe Spectrum — Typography system.**  
  https://spectrum.adobe.com/foundations/typography/typography-system

- **[S16] GOV.UK Design System — Type scale.**  
  https://design-system.service.gov.uk/styles/type-scale/

- **[S17] Adobe Spectrum — Applying the type system.**  
  https://spectrum.adobe.com/foundations/typography/applying-the-type-system

- **[S18] Adobe Spectrum — Monospace numbers / typography system.**  
  https://spectrum.adobe.com/foundations/typography/typography-system

**Responsive typography**

- **[S19] W3C — F94: incorrect viewport units can fail Resize Text.**  
  https://www.w3.org/WAI/WCAG22/Techniques/failures/F94

- **[S20] MDN — CSS `clamp()` and accessibility.**  
  https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp

- **[S21] MDN — Variable fonts / CSS fonts guidance.**  
  https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Fonts/Variable_fonts

**Peer-reviewed / research**

- **[S22] Richardson, J. T. E. (2022) — The Legibility of Serif and Sans Serif Typefaces.**  
  https://link.springer.com/book/10.1007/978-3-030-90984-0

- **[S23] 2026 experiment — serif vs sans-serif and screen vs paper comprehension.**  
  https://doi.org/10.1080/0144929X.2026.2678378

- **[S24] Galliussi et al. (2020) — inter-letter/inter-word spacing and dyslexia-friendly features.**  
  https://pubmed.ncbi.nlm.nih.gov/32172467/

- **[S25] W3C — Menu Styling readability; avoid uppercase where possible.**  
  https://www.w3.org/WAI/tutorials/menus/styling/

- **[S26] Baymard — Readability: optimal line length, 50–75 characters.**  
  https://baymard.com/research-articles/line-length-readability

- **[S27] Apple — Branding; custom font in headlines while preserving legible body.**  
  https://developer.apple.com/design/human-interface-guidelines/branding

- **[S28] Material Design legacy typography guidance — limited scales and readable hierarchy.**  
  https://m1.material.io/style/typography.html

- **[S29] W3C — Understanding SC 1.4.5 Images of Text.**  
  https://www.w3.org/WAI/WCAG22/Understanding/images-of-text

- **[S30] W3C — WCAG 2.2 Resize Text.**  
  https://www.w3.org/WAI/WCAG22/Understanding/resize-text.html

- **[S31] Apple — Widgets, text should remain real/scalable and generally >=11pt.**  
  https://developer.apple.com/design/human-interface-guidelines/widgets

- **[S32] Fluent 2 — sentence case and avoidance of all caps.**  
  https://fluent2.microsoft.design/typography

- **[S33] Azzarello et al. (2026) — meta-analysis of dyslexia-friendly fonts.**  
  https://pubmed.ncbi.nlm.nih.gov/42536336/

- **[S34] Kuster et al. — Dyslexie font does not benefit reading in children with or without dyslexia.**  
  https://pubmed.ncbi.nlm.nih.gov/29204931/

- **[S35] Wery & Diliberto — OpenDyslexic reading rate and accuracy.**  
  https://pubmed.ncbi.nlm.nih.gov/26993270/

- **[S36] GOV.UK — Font override guidance, alignment and justification.**  
  https://design-system.service.gov.uk/styles/font-override-classes/

**Web font engineering**

- **[S37] W3C — WOFF 2.0 Recommendation.**  
  https://www.w3.org/TR/WOFF2/

- **[S38] MDN — Variable fonts.**  
  https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Fonts/Variable_fonts

- **[S39] web.dev — Variable fonts and web typography/performance.**  
  https://web.dev/articles/variable-fonts

- **[S40] Chrome for Developers — Font display performance insight.**  
  https://developer.chrome.com/docs/performance/insights/font-display

- **[S41] web.dev — Best practices for fonts.**  
  https://web.dev/articles/font-best-practices

- **[S42] Chrome for Developers — framework tools for font fallbacks / CLS.**  
  https://developer.chrome.com/blog/framework-tools-font-fallback/

- **[S43] MDN — `size-adjust`.**  
  https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40font-face/size-adjust

- **[S44] MDN — `ascent-override` and font metric overrides.**  
  https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40font-face/ascent-override

- **[S45] web.dev — Reducing web font size / subsetting / variable fonts.**  
  https://web.dev/articles/reduce-webfont-size

**Product-specific sources**

- **[S46] Vercel — Geist font.**  
  https://vercel.com/font

- **[S47] Atlassian — Typography overview and app vs brand fonts.**  
  https://atlassian.design/foundations/typography

- **[S48] Notion Help — page typography choices and Small text density option.**  
  https://www.notion.com/help/customize-and-style-your-content

---

# 22. FINAL RULE FOR THE FUTURE SKILL

The Skill must never output a font choice without also outputting:

```text
1. semantic role
2. intended size range
3. weight
4. line-height
5. tracking behavior
6. numeric feature if relevant
7. density rationale
8. responsive behavior
9. accessibility validation
10. performance/loading strategy
11. confidence level
12. whether the decision is research-backed, convention, or style preference
```

A typography system is not “Inter + 16px.”

A strong AI typography system is a constrained decision model that knows **why** text is being shown, **how much** information must fit, **how users may resize it**, **how the font will load**, and **which visual choices are evidence versus taste**.
