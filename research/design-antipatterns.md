# Design Anti-Patterns for Modern SaaS Interfaces

> **Purpose:** executable research rules for an AI coding/design agent that must audit and correct its own frontend before declaring work complete.
>
> **Scope:** modern SaaS applications, dashboards, settings, workflow tools, data-heavy interfaces, and SaaS landing pages. Special attention is given to recurring defaults in AI-generated / vibe-coded UIs.
>
> **Important:** gradients, glass, blur, rounded corners, pills, shadows, large type, dark mode, cards, and animation are **not inherently bad**. They become anti-patterns when they damage hierarchy, comprehension, discoverability, accessibility, task efficiency, responsiveness, or product specificity.

---

## 0. How to use this document

An agent should use these rules in four passes:

1. **Structure pass** — information architecture, task priority, navigation, layout, responsive behavior.
2. **Interaction pass** — actions, feedback, errors, confirmations, modals, hidden functionality.
3. **Visual pass** — hierarchy, type, color, surfaces, effects, consistency, AI-template smell.
4. **Accessibility pass** — keyboard, focus, contrast, motion, reflow, target size, color-independent meaning.

Do not “fix” a page by mechanically flattening everything. The objective is **intentional design**, not stylistic austerity.

### Evidence classes

| Class | Meaning | How rules may use it |
|---|---|---|
| **A** | Normative accessibility standard or official platform requirement/guidance | May create hard fail conditions when directly applicable |
| **B** | Empirical usability/HCI study or structured usability testing | Strong default; exceptions need product evidence |
| **C** | Mature design system or professional UX research guidance | Strong heuristic; context-dependent |
| **D** | Convergent professional observations, current industry analysis, or emerging research | Use as smell/test, not as universal truth |

### Severity classes

| Severity | Meaning |
|---|---|
| **CRITICAL** | Blocks task completion, causes loss of access/functionality, creates severe accessibility failure, data-loss risk, or unusable responsive behavior |
| **HIGH** | Materially harms comprehension, discoverability, task efficiency, hierarchy, or accessibility |
| **MEDIUM** | Noticeable UX/design debt; usually does not block the core task |
| **STYLE PREFERENCE** | Primarily aesthetic/brand-related unless combined with another failure |

### Confidence

- **HIGH** — supported by A/B evidence or multiple strong independent sources.
- **MEDIUM** — supported by mature guidance and plausible mechanisms, but thresholds are heuristic.
- **LOW** — emerging pattern or style smell; use as a prompt for review, not an automatic rejection.

---

# 1. Visual anti-patterns

## AP-V01 — Decorative gradient overload

**ANTI-PATTERN**  
Multiple gradients are used as a default decoration across backgrounds, text, buttons, cards, borders, and glows without a semantic or brand role.

**WHY IT FAILS**  
When many regions use high color variation, visual weight becomes difficult to control. Important information competes with decoration, and contrast is harder to reason about across gradient extrema.

**EVIDENCE**  
- W3C notes that gradients can reduce apparent contrast and that the least-contrasting area must be considered for meaningful graphics/UI [S4]. **Class A**
- NN/g recommends using color and contrast intentionally and sparingly to create hierarchy; excessive emphasis undermines signal-to-noise [S10][S11]. **Class C**
- Research on website visual complexity finds that higher visual complexity can reduce search efficiency and information recall [S28]. **Class B**

**DETECTION HEURISTIC**
- Flag when a single app view uses decorative gradients in **3+ independent component roles** (e.g. page background + CTA + cards + text).
- Flag any gradient body text or essential label where contrast is not tested at the worst point.
- Flag when accent gradients are applied to both primary and secondary actions.

**BAD EXAMPLE**  
Purple-blue page background, gradient H1, gradient primary button, gradient icon tiles, gradient card borders, and cyan glow — all on the same dashboard.

**BETTER APPROACH**  
Assign gradients a role: brand hero, data encoding, media treatment, or one focal accent. Keep application work surfaces mostly stable and let hierarchy come from spacing, type, position, and a limited accent system.

**EXCEPTIONS**  
Brand-led marketing pages, entertainment, creative tools, or data visualizations where gradients encode continuous values.

**SEVERITY**  
STYLE PREFERENCE → MEDIUM if it harms hierarchy or contrast.

**CONFIDENCE**  
MEDIUM.

---

## AP-V02 — Purple/blue “AI gradient” as an unreasoned default

**ANTI-PATTERN**  
A violet/indigo/cyan gradient appears because the generator associates it with “modern AI SaaS,” not because the product’s brand, domain, or content calls for it.

**WHY IT FAILS**  
It makes products visually interchangeable and can communicate category cliché rather than product-specific identity. The issue is not the hues; it is the absence of a design decision.

**EVIDENCE**  
- 2026 HCI research explicitly identifies homogenization risk in web vibe coding and argues that frictionless generation can reinforce dominant design conventions [S26]. **Class B/D (emerging research)**
- Multiple independent professional analyses of AI-generated UI report the same recurring cluster: purple/blue gradients, glass cards, rounded grids, Inter, generic centered heroes [S29][S30][S31]. **Class D**
- Do **not** treat those articles as proof that purple is bad. Treat convergence as a smell indicating an unconstrained default.

**DETECTION HEURISTIC**
- If primary palette is violet/indigo/cyan **and** there is no explicit brand token/source/brief supporting it, mark `AI_DEFAULT_COLOR_RISK`.
- Raise confidence if combined with 3+ AI-smell markers from section 13.

**BAD EXAMPLE**  
A payroll compliance tool and a developer observability tool receive nearly identical indigo-to-cyan hero gradients despite different brands and users.

**BETTER APPROACH**  
Derive palette from brand, trust requirements, product category, content/data requirements, and existing identity. If purple is chosen, document the reason.

**EXCEPTIONS**  
The brand genuinely owns these colors; the product has a deliberate AI-category visual language; a campaign intentionally uses the convention.

**SEVERITY**  
STYLE PREFERENCE.

**CONFIDENCE**  
MEDIUM for the homogenization smell; LOW for any hue-specific judgment.

---

## AP-V03 — Gratuitous glassmorphism

**ANTI-PATTERN**  
Translucency/backdrop blur is applied to ordinary content cards, forms, metrics, tables, or every container simply to appear “premium.”

**WHY IT FAILS**  
Materials are useful when they communicate layering. When every content surface is translucent, foreground/background hierarchy becomes ambiguous, contrast varies with content behind it, and decorative processing can dominate the work.

**EVIDENCE**  
- Apple’s current materials guidance says Liquid Glass forms a distinct functional layer for controls/navigation, explicitly says **not to use Liquid Glass in the content layer**, and says to use it sparingly [S18]. **Class A/C**
- Apple also recommends thicker/more opaque materials when fine foreground content needs stronger contrast [S18]. **Class C**

**DETECTION HEURISTIC**
- Flag if `backdrop-filter`/glass treatment appears on **>30% of content containers** in a task-oriented app view.
- Flag nested glass surfaces.
- Flag glass behind dense text, forms, data tables, or charts unless worst-case contrast is verified.
- Flag when glass has no layering/navigation/overlay role.

**BAD EXAMPLE**  
Every dashboard KPI, filter, table wrapper, modal, and sidebar is a semi-transparent blurred panel.

**BETTER APPROACH**  
Use stable opaque or semantic surfaces for content. Reserve glass/translucency for navigation, overlays, floating controls, media overlays, or a small number of deliberate focal elements.

**EXCEPTIONS**  
Media-first experiences, spatial interfaces, operating-system-native glass patterns, or intentionally immersive branded experiences.

**SEVERITY**  
MEDIUM; HIGH if contrast/readability is unstable.

**CONFIDENCE**  
HIGH for Apple-platform guidance; MEDIUM cross-platform.

---

## AP-V04 — Excessive blur

**ANTI-PATTERN**  
Large blur values are applied broadly to backgrounds, cards, decorative blobs, modals, and hover states.

**WHY IT FAILS**  
Blur can erase useful spatial cues, create muddy boundaries, increase compositing cost, and make foreground contrast dependent on unpredictable backgrounds.

**EVIDENCE**  
- Apple materials guidance ties blur/translucency thickness to legibility and hierarchy, not decoration alone [S18]. **Class C**
- WCAG non-text contrast requires meaningful controls/graphics to remain perceivable against adjacent colors [S4]. **Class A**

**DETECTION HEURISTIC**
- Flag if more than two simultaneously visible layers use backdrop blur.
- Flag blur on the main reading/data surface.
- Flag blur where text contrast changes materially with underlying content.
- Treat exact blur radius as implementation-specific; do not hard-code a universal “bad” px value.

**BAD EXAMPLE**  
Blurred page background + blurred sidebar + blurred KPI cards + blurred dropdown + blurred modal.

**BETTER APPROACH**  
Choose one depth mechanism per relationship: solid surface, tonal surface, border, shadow, or blur. Use blur only when seeing softened background context adds value.

**EXCEPTIONS**  
Transient overlays or media controls where preserving background context is valuable.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
MEDIUM.

---

## AP-V05 — Shadow inflation

**ANTI-PATTERN**  
Almost every component casts a shadow, often with unrelated shadow recipes.

**WHY IT FAILS**  
Elevation stops encoding depth when everything is elevated. Excessive shadows create visual noise and can be especially ineffective in dark themes.

**EVIDENCE**  
- Atlassian’s elevation guidance reserves raised/overlay elevation for specific cases and warns that raised elevation creates visual noise; borders or whitespace may suffice [S19]. **Class C**
- Dark-mode elevation often needs surface-tone differences because shadows become harder to see [S19]. **Class C**

**DETECTION HEURISTIC**
- Flag >3 unrelated shadow tokens on one screen.
- Flag shadows on static flat groups that do not move, overlay, drag, or need special emphasis.
- Flag every card using “raised” elevation.
- Flag dark-mode designs that depend only on black shadows for separation.

**BAD EXAMPLE**  
Every card, button, input, badge, chart, and sidebar has a soft 20–40px shadow.

**BETTER APPROACH**  
Define a small elevation scale. Default surfaces are flat. Raise only moveable cards, floating controls, menus, popovers, and overlays — or one deliberate focal region.

**EXCEPTIONS**  
Highly skeuomorphic visual direction where depth itself is part of the brand language.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-V06 — Radius inflation / excessive border radius

**ANTI-PATTERN**  
Large rounded corners are applied indiscriminately to every container, including nested containers, tables, banners, controls, cards, and sections.

**WHY IT FAILS**  
The main problem is semantic flattening: components that should communicate different roles begin to share the same silhouette. Repeated large radii also amplify the “template” look.

**EVIDENCE**  
There is no strong general usability evidence that large radius itself is harmful. Current platform systems even prefer rounded/capsule shapes in some contexts [S17]. Therefore this is primarily a consistency/semantics rule, not a universal usability rule. **Class C/D**

**DETECTION HEURISTIC**
- Flag when >70% of visible containers use the same conspicuous large radius.
- Flag >3 arbitrary radius values without tokens.
- Flag nested containers where outer and inner radii create “rounded rectangle soup.”
- Never fail solely because `border-radius` is high.

**BAD EXAMPLE**  
A 28px-radius page shell containing 24px cards containing 20px metric tiles containing rounded icon boxes.

**BETTER APPROACH**  
Map radius to component role and scale. Some surfaces may be flat; controls may be more rounded; chips/pills can remain fully rounded where their shape carries meaning.

**EXCEPTIONS**  
Strong soft/consumer brand systems; OS-native capsule controls; touch-first products.

**SEVERITY**  
STYLE PREFERENCE → MEDIUM when semantic differentiation is lost.

**CONFIDENCE**  
MEDIUM.

---

## AP-V07 — Pill-shaped everything

**ANTI-PATTERN**  
Buttons, inputs, tabs, segmented controls, status labels, filters, navigation, KPI containers, and unrelated cards all use capsule silhouettes.

**WHY IT FAILS**  
Pills are effective for compact controls and chips, but when every component shares the same shape users lose quick visual categorization between action, selection, status, and content.

**EVIDENCE**  
- Apple explicitly supports capsule buttons in specific contexts but differentiates shapes based on arrangement/component role [S17]. **Class C**
- General consistency principles require similar things to behave similarly — which also implies different things should not be made misleadingly identical [S21]. **Class C**

**DETECTION HEURISTIC**
- Flag if 3+ semantically different component classes are all `rounded-full`.
- Exempt chips/tags/segmented controls and isolated prominent buttons.
- Escalate if status pills look identical to clickable pills.

**BAD EXAMPLE**  
A status badge, search field, destructive action, nav item, and metric container all look like the same capsule.

**BETTER APPROACH**  
Reserve pills for compact selectable/status constructs and selected primary actions where appropriate. Use shape, fill, border, placement, and labels to preserve component taxonomy.

**EXCEPTIONS**  
Deliberate OS-specific UI language or highly constrained wearable interfaces.

**SEVERITY**  
STYLE PREFERENCE → MEDIUM.

**CONFIDENCE**  
MEDIUM.

---

## AP-V08 — Cards inside cards

**ANTI-PATTERN**  
Containers are repeatedly nested, each with its own border/background/radius/shadow despite no new semantic grouping.

**WHY IT FAILS**  
Nested common regions create too many grouping signals. Users must parse wrappers instead of content, while available space shrinks and responsive behavior becomes brittle.

**EVIDENCE**  
- NN/g visual hierarchy guidance says extra borders/backgrounds can create clutter and should be used sparingly [S10]. **Class C**
- Apple recommends using negative space, shapes, colors, materials, **or** separators to group related content — not all at once [S16]. **Class C**
- Atlassian warns against elevation for grouping when border or whitespace is sufficient [S19]. **Class C**

**DETECTION HEURISTIC**
- Flag visual containment depth >2 where nested layers have independent border/background/shadow.
- Ignore semantic structures required for interaction (e.g. card → popover; panel → table).
- Ask: “If the inner/outer wrapper is removed, is grouping or interaction meaning lost?” If no, remove it.

**BAD EXAMPLE**  
Page section → rounded card → glass card → metric card → rounded icon tile.

**BETTER APPROACH**  
Use whitespace and alignment first. Introduce a container only when it establishes a meaningful common region, interaction boundary, scrolling region, or elevation level.

**EXCEPTIONS**  
Complex builders/editors where nested scope is the actual mental model.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-V09 — Borders everywhere

**ANTI-PATTERN**  
Every row, section, card, button, metric, filter, input group, and panel is boxed with visible borders.

**WHY IT FAILS**  
When all boundaries are equally explicit, hierarchy becomes noisy and grouping becomes less meaningful.

**EVIDENCE**  
- NN/g recommends borders/backgrounds sparingly because they add visual clutter [S10]. **Class C**
- Mature design systems use subtle borders contextually, often as one option among whitespace/surface/elevation [S19][S20]. **Class C**

**DETECTION HEURISTIC**
- Flag if >70% of major non-form containers have explicit borders.
- Do not flag inputs/tables merely for having necessary boundaries.
- Flag if border, background contrast, and shadow all encode the same grouping simultaneously.

**BAD EXAMPLE**  
A dashboard where every element is a bordered rectangle separated by 12px gaps.

**BETTER APPROACH**  
Use alignment + spacing as default grouping. Add subtle borders where adjacency is otherwise ambiguous, especially in dense data layouts.

**EXCEPTIONS**  
Dense enterprise/data-grid interfaces where subtle separators materially improve row/column tracking.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-V10 — Excessive or poorly allocated whitespace

**ANTI-PATTERN**  
Whitespace separates elements that should be perceived together, pushes key tasks below the fold, or forces unnecessary scrolling in work-heavy SaaS screens.

**WHY IT FAILS**  
Whitespace supports grouping and reading, but more is not always better. Excessive gaps can break Gestalt proximity and lower information efficiency.

**EVIDENCE**  
- A controlled study found margins affected reading behavior and satisfaction, demonstrating that whitespace has functional effects rather than a simple “more is better” relationship [S27]. **Class B**
- Apple and NN/g both frame whitespace as a grouping/hierarchy tool [S11][S16]. **Class C**

**DETECTION HEURISTIC**
- Flag adjacent label/control or heading/content pairs separated by a gap larger than the separation between unrelated sections.
- Flag app screens where padding alone causes the main action/data to require an extra viewport of scrolling.
- Evaluate whitespace relationally, not with a universal px threshold.

**BAD EXAMPLE**  
A settings page uses 80–120px vertical gaps between every field, making eight settings require several screens.

**BETTER APPROACH**  
Use a spacing scale. Make within-group spacing smaller than between-group spacing. Tune density to task frequency and data volume.

**EXCEPTIONS**  
Marketing/editorial pages where pacing and visual storytelling are intentional.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH that relational spacing matters; MEDIUM for automated thresholds.

---

## AP-V11 — Glow everywhere

**ANTI-PATTERN**  
Neon outer glows are applied to cards, CTAs, icons, charts, and navigation simultaneously.

**WHY IT FAILS**  
Glow creates strong visual weight without necessarily conveying information. Multiple glows compete, blur edges, and can weaken contrast around fine elements.

**EVIDENCE**  
- WCAG focus guidance explicitly distinguishes valid focus indicators from shadow/glow outside a component; decorative glow should not be relied on as the only accessible state cue [S2]. **Class A**
- Visual-complexity evidence supports minimizing irrelevant visual noise [S28]. **Class B**

**DETECTION HEURISTIC**
- Flag more than one persistent glowing focal region in a work screen.
- Flag glow used as the only focus/selection indicator.
- Flag glow around long text or dense data.

**BAD EXAMPLE**  
Sidebar active item, every KPI card, primary button, and chart all emit colored glows.

**BETTER APPROACH**  
Use glow as a rare brand/accent or transient feedback effect. Use stable borders/fills/underlines for states.

**EXCEPTIONS**  
Gaming, music, cyberpunk or entertainment products with a deliberate visual language.

**SEVERITY**  
STYLE PREFERENCE → HIGH if it replaces accessible state indication.

**CONFIDENCE**  
MEDIUM.

---

## AP-V12 — Giant headings that consume the task

**ANTI-PATTERN**  
Display typography is sized for spectacle even in utilitarian product screens, forcing the actual workflow below the fold.

**WHY IT FAILS**  
Scale is a hierarchy tool. If routine page titles dominate the viewport, they steal priority from the task and reduce information density.

**EVIDENCE**  
- NN/g recommends scale differences that reflect actual importance and a small hierarchy of type sizes [S9][S10]. **Class C**
- Baymard and screen-reading research show readable text measure matters; typography must serve consumption, not merely visual impact [S12][S25]. **Class B/C**

**DETECTION HEURISTIC**
- Flag an app/dashboard page title >~10% of viewport height or requiring scrolling before first actionable content at common laptop heights.
- On marketing pages, treat as style preference unless the value proposition/action is pushed out of view.
- Do not enforce a universal maximum font size.

**BAD EXAMPLE**  
“Analytics” at 96px occupies half a 768px-tall dashboard before any metrics appear.

**BETTER APPROACH**  
Use display scale for marketing moments. Use compact page-title hierarchy in frequent workflow screens.

**EXCEPTIONS**  
Brand campaigns, editorial landers, presentation-like experiences.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
MEDIUM.

---

## AP-V13 — Excessive centered alignment

**ANTI-PATTERN**  
Long paragraphs, form labels, data, lists, dashboard sections, or complex choices are centered because the hero section was centered.

**WHY IT FAILS**  
Centering removes a consistent scan edge and is weakest for repeated multi-line information. It also contributes to generic hero-template structure when applied indiscriminately.

**EVIDENCE**  
- Apple emphasizes alignment for scanability and organization [S16]. **Class C**
- Research on line length and on-screen reading supports maintaining readable, predictable text geometry [S25]. **Class B**
- No evidence supports a blanket ban on centered text; short headings/marketing copy can work well.

**DETECTION HEURISTIC**
- Flag centered body copy >2–3 lines in task-oriented UI.
- Flag centered form labels, tables, or multi-item settings.
- Allow short hero copy, empty states, confirmations, and compact cards where centered alignment is intentional.

**BAD EXAMPLE**  
A pricing comparison or admin settings page centers all labels, explanations, controls, and values.

**BETTER APPROACH**  
Use a stable reading edge for dense/operational content. Center only small self-contained messages or deliberate marketing moments.

**EXCEPTIONS**  
Short empty states, success screens, focused marketing heroes.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
MEDIUM.

---

# 2. Hierarchy anti-patterns

## AP-H01 — Everything is emphasized

**ANTI-PATTERN**  
Many elements are simultaneously large, bold, saturated, elevated, animated, or outlined.

**WHY IT FAILS**  
Emphasis is relative. If everything has high visual weight, the interface has no useful hierarchy.

**EVIDENCE**  
- NN/g defines visual hierarchy as guiding attention according to intended importance and recommends using emphasis sparingly [S10][S13]. **Class C**
- Visual complexity can negatively affect search efficiency and recall [S28]. **Class B**

**DETECTION HEURISTIC**
- Perform a “squint test”: blur/screenshot; count dominant regions.
- Flag if 4+ unrelated regions appear equally dominant.
- Flag if more than two typography/color/elevation emphasis techniques are stacked on routine elements.

**BAD EXAMPLE**  
Four metric cards, three CTAs, sidebar selection, alert banner, and hero all use saturated accent fills.

**BETTER APPROACH**  
Define one primary focal target, a secondary layer, and quiet supporting information.

**EXCEPTIONS**  
Monitoring walls where multiple alerts are genuinely simultaneous priorities — but even then severity must be encoded.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-H02 — Competing primary CTAs

**ANTI-PATTERN**  
Two or more actions in the same decision context receive equal “primary” prominence.

**WHY IT FAILS**  
Users must stop to interpret which action is the intended next step.

**EVIDENCE**  
- Apple recommends keeping prominent buttons to one or two per view because too many increase cognitive load [S17]. **Class C**
- Baymard finds primary buttons need distinct prominence and warns that too many buttons overwhelm users [S14]. **Class B/C**

**DETECTION HEURISTIC**
- In one local action group, allow at most one `primary` action unless choices are intentionally equal.
- Flag two filled accent buttons side by side where one is clearly secondary/cancel/back.
- Destructive action must not accidentally inherit primary positive styling.

**BAD EXAMPLE**  
“Save”, “Export”, and “Invite team” all use identical bright filled buttons in the page header.

**BETTER APPROACH**  
Promote the most likely next action; downgrade secondary actions to neutral/outline/ghost/menu placement.

**EXCEPTIONS**  
True binary choices with equal importance.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-H03 — Too many accent colors

**ANTI-PATTERN**  
Several saturated hues are used for generic emphasis rather than stable semantic roles.

**WHY IT FAILS**  
Users cannot learn what color means, and visual priority fragments.

**EVIDENCE**  
- Apple says color should be used consistently, particularly when communicating status or interactivity [S22]. **Class C**
- WCAG requires meaning not be conveyed through color alone [S3]. **Class A**

**DETECTION HEURISTIC**
- Flag >2 non-semantic emphasis hues in one product view unless data visualization needs them.
- Map colors to roles: brand/primary, neutral, semantic success/warning/error/info, data series.
- Flag same hue used both for “interactive” and unrelated decorative text if it creates ambiguity.

**BAD EXAMPLE**  
Purple links, cyan buttons, orange selected tabs, pink active nav, and green generic icons.

**BETTER APPROACH**  
Create explicit color tokens and reserve saturated colors for semantic or priority roles.

**EXCEPTIONS**  
Charts, category coding, creative suites, or consumer products with a multi-color brand.

**SEVERITY**  
MEDIUM → HIGH if state meaning becomes ambiguous.

**CONFIDENCE**  
HIGH.

---

## AP-H04 — No primary/secondary action distinction

**ANTI-PATTERN**  
Actions with very different consequences have identical styling and placement.

**WHY IT FAILS**  
Users rely on visual and textual cues to identify logical next steps and destructive consequences.

**EVIDENCE**  
Baymard’s button research reports that users often rely on visual cues such as color and placement, and that primary actions need unique prominence [S14]. **Class B/C**

**DETECTION HEURISTIC**
- For every action cluster, label actions as primary / secondary / tertiary / destructive.
- Flag clusters where all styles are identical despite different priority.
- Flag destructive action placed adjacent to primary with minimal differentiation.

**BAD EXAMPLE**  
“Delete workspace” looks identical to “Save changes.”

**BETTER APPROACH**  
Use semantic role, placement, copy, and style — not only color — to distinguish consequence and priority.

**EXCEPTIONS**  
Toolbar commands of genuinely equal weight.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-H05 — Density mismatch

**ANTI-PATTERN**  
The information density does not match the job: operational screens are over-spaced, or rare decision screens are crammed.

**WHY IT FAILS**  
SaaS users often scan, compare, monitor, and repeat actions. Density is a task parameter, not a fashion.

**EVIDENCE**  
- Carbon provides multiple table row densities and recommends matching density to data needs [S15]. **Class C**
- NN/g defines dashboards as at-a-glance, quickly consumable views, not expansive exploration surfaces [S24]. **Class C**

**DETECTION HEURISTIC**
- Compare number of repeated tasks/records to viewport.
- Flag tables where decorative padding halves visible rows without touch/accessibility reason.
- Flag dense decision forms where unrelated fields have no grouping or breathing room.

**BAD EXAMPLE**  
An admin table shows only four records on a laptop because each row is 96px tall.

**BETTER APPROACH**  
Offer compact/default/comfortable density where appropriate; use denser presentation for frequent expert workflows while preserving target size and readability.

**EXCEPTIONS**  
Touch-first environments or accessibility accommodations requiring larger targets.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

# 3. Typography anti-patterns

## AP-T01 — Uncontrolled font-size proliferation

**ANTI-PATTERN**  
Many near-duplicate font sizes are invented locally rather than mapped to semantic text styles.

**WHY IT FAILS**  
Hierarchy becomes noisy and inconsistent; small differences may not communicate clear rank.

**EVIDENCE**  
NN/g recommends a small number of type sizes to express hierarchy and stresses consistent visual systems [S9][S10]. **Class C**

**DETECTION HEURISTIC**
- Flag >5 distinct non-data font sizes on one app view unless each maps to a documented token.
- Flag near-duplicates (e.g. 13/14/15/16/17) used for equivalent labels.
- Numbers in charts/tables may need specialized tokens.

**BAD EXAMPLE**  
Every card defines its own title and body size.

**BETTER APPROACH**  
Use named tokens such as display, page-title, section-title, body, body-small, label, caption, numeric.

**EXCEPTIONS**  
Editorial/marketing pages with deliberate expressive typography.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-T02 — Weak or inverted typography hierarchy

**ANTI-PATTERN**  
Heading weight/size does not correspond to information structure, or secondary labels visually dominate content.

**WHY IT FAILS**  
Users cannot scan structure efficiently.

**EVIDENCE**  
NN/g identifies typography, scale, contrast, and grouping as core mechanisms of visual hierarchy [S9][S10]. **Class C**

**DETECTION HEURISTIC**
- Build DOM/visual outline: H1 > H2 > H3 > body should have perceptible but not theatrical differentiation.
- Flag headings that are smaller/lower contrast than unrelated metadata.
- Flag all headings sharing the same visual weight.

**BAD EXAMPLE**  
Page title 18px regular; card metadata 16px bold uppercase; primary metric 14px gray.

**BETTER APPROACH**  
Make semantic hierarchy visually legible and consistent across screens.

**EXCEPTIONS**  
Dense professional tools where hierarchy is conveyed more by position/grouping than large type.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-T03 — Illegible secondary text

**ANTI-PATTERN**  
Muted text is made so faint that descriptions, timestamps, helper text, or inactive-but-important information become difficult to read.

**WHY IT FAILS**  
“Secondary” does not mean “optional to perceive.”

**EVIDENCE**  
- WCAG minimum text contrast: 4.5:1 for normal text, 3:1 for qualifying large text [S1]. **Class A**
- NN/g documents usability and discoverability problems caused by low-contrast text [S23]. **Class C**

**DETECTION HEURISTIC**
- Hard fail if required text violates applicable WCAG contrast.
- Flag opacity-based `text-muted` tokens that fail on any supported surface.
- Test disabled states separately; legal WCAG exceptions do not automatically make poor legibility good UX.

**BAD EXAMPLE**  
12px gray helper text at ~2.5:1 on a light-gray card.

**BETTER APPROACH**  
Reduce prominence using size/weight/placement while maintaining readable contrast.

**EXCEPTIONS**  
Purely decorative non-content.

**SEVERITY**  
HIGH / CRITICAL when task-essential.

**CONFIDENCE**  
HIGH.

---

## AP-T04 — Disproportionate headings

**ANTI-PATTERN**  
Heading scale is driven by a generic marketing template rather than content importance or viewport.

**WHY IT FAILS**  
It distorts hierarchy and reduces usable viewport.

**EVIDENCE**  
See AP-V12; hierarchy and line-measure research [S9][S12][S25].

**DETECTION HEURISTIC**
- Flag headings wrapping into 3+ lines at common mobile widths because of size rather than content.
- Flag display headings that leave no visible supporting content/action at first viewport.
- Use responsive `clamp()` but validate actual screenshots.

**BAD EXAMPLE**  
64px mobile H1 turns a six-word title into five lines.

**BETTER APPROACH**  
Scale type with viewport and role; prioritize readable line breaks.

**EXCEPTIONS**  
Deliberately poster-like campaign pages.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-T05 — Font choice without role logic

**ANTI-PATTERN**  
Fonts are selected because they are trendy or randomly mixed, with no mapping to UI/body/display/code/data roles.

**WHY IT FAILS**  
Inconsistent typography weakens identity and can reduce legibility, especially for numbers and dense controls.

**EVIDENCE**  
Material’s typography guidance frames type as a hierarchy and brand system, not isolated font selection [S32]. **Class C**

**DETECTION HEURISTIC**
- Flag >2 text families plus monospace in an app unless role definitions exist.
- Ensure tabular/numeric data uses appropriate numeral behavior where alignment matters.
- Ensure all chosen weights actually load.

**BAD EXAMPLE**  
Serif labels, geometric sans table cells, humanist sans buttons, and display grotesk headings with no system.

**BETTER APPROACH**  
Define font roles and tokens; use a small coherent family set.

**EXCEPTIONS**  
Editorial or branded marketing systems intentionally mixing families.

**SEVERITY**  
STYLE PREFERENCE → MEDIUM.

**CONFIDENCE**  
MEDIUM.

---

## AP-T06 — Unbounded text measure

**ANTI-PATTERN**  
Body copy stretches across very wide content containers.

**WHY IT FAILS**  
Long lines make tracking line starts/ends harder; research supports moderate line lengths for effective screen reading.

**EVIDENCE**  
- Baymard recommends roughly 50–75 characters for body text and reports testing problems with overly long lines [S12]. **Class B/C**
- Dyson & Haselgrove found medium line lengths around 55 characters supported effective reading in their study [S25]. **Class B**

**DETECTION HEURISTIC**
- For prose, target roughly `50–75ch`; treat `>80ch` as audit warning.
- Do not apply prose measure to code, tables, timelines, or data grids.

**BAD EXAMPLE**  
A 1440px-wide settings explanation uses full-width paragraphs.

**BETTER APPROACH**  
Constrain prose independently of the overall layout width.

**EXCEPTIONS**  
Structured tabular/code content.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

# 4. Layout anti-patterns

## AP-L01 — Decorative cards with no grouping purpose

**ANTI-PATTERN**  
Content is converted into cards simply because “SaaS dashboards use cards.”

**WHY IT FAILS**  
Cards add boundaries, padding, and hierarchy signals. If everything is a card, no region is meaningfully grouped.

**EVIDENCE**  
NN/g and platform/design-system guidance favor intentional grouping with the lightest sufficient mechanism [S10][S16][S19].

**DETECTION HEURISTIC**
- For each card ask: does it represent an independent object, action scope, movable item, common region, or elevation?
- If not, test removing its border/background.
- Flag identical decorative cards used only to fill a grid.

**BAD EXAMPLE**  
Page title is in a card, filters in a card, table in a card, pagination in a card, each metric in a card.

**BETTER APPROACH**  
Use sections, alignment, whitespace, and dividers first. Use cards when the grouping itself has meaning.

**EXCEPTIONS**  
Entity-centric products where cards are the primary object representation.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-L02 — Nested containers without semantic scope

**ANTI-PATTERN**  
Multiple wrappers exist solely for styling.

**WHY IT FAILS**  
See AP-V08; nested regions reduce space and add parsing cost.

**DETECTION HEURISTIC**
- Audit DOM + screenshot.
- Flag wrapper layers that add only radius/padding/background while not changing scope, scroll, interaction, state, or grouping.

**BAD EXAMPLE**  
`section > panel > card > card-content > inset-panel` for one metric.

**BETTER APPROACH**  
Flatten presentation hierarchy while retaining semantic DOM where useful.

**EXCEPTIONS**  
Technical wrappers with no visual containment.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-L03 — Alignment drift

**ANTI-PATTERN**  
Headings, card content, tables, controls, and actions use unrelated left edges or baseline systems.

**WHY IT FAILS**  
Alignment is a primary scan and organization cue.

**EVIDENCE**  
Apple explicitly states that alignment improves scanability and communicates organization/hierarchy [S16]. Carbon grid guidance similarly enforces component/type alignment [S20]. **Class C**

**DETECTION HEURISTIC**
- Detect repeated edges differing by small arbitrary offsets (e.g. 20/24/28px) within the same column.
- Flag header controls not aligned with underlying data/content grid.
- Use grid overlays in visual audit.

**BAD EXAMPLE**  
Page title at x=32, filters at x=40, cards at x=24, table text at x=52.

**BETTER APPROACH**  
Define container widths, grid columns, gutters, and internal padding tokens.

**EXCEPTIONS**  
Intentional asymmetry with a clear visual system.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-L04 — Incorrect content width

**ANTI-PATTERN**  
A single max-width is applied to every content type.

**WHY IT FAILS**  
Prose benefits from constrained measure; tables/charts often need width; forms and settings need intermediate widths.

**EVIDENCE**  
- Carbon recommends giving data tables substantial main-content width [S15]. **Class C**
- Reading research supports constrained prose measure [S12][S25]. **Class B**

**DETECTION HEURISTIC**
- Flag full-width prose over wide desktop.
- Flag wide data tables compressed into narrow centered cards.
- Define width by content class: prose, form, dashboard, table/data grid, media.

**BAD EXAMPLE**  
A 680px max-width wraps a 12-column data table into unusable truncation.

**BETTER APPROACH**  
Use content-specific containers and allow dense data surfaces to claim more width.

**EXCEPTIONS**  
Products deliberately optimized for a fixed narrow working canvas.

**SEVERITY**  
HIGH for data usability; MEDIUM otherwise.

**CONFIDENCE**  
HIGH.

---

## AP-L05 — Rectangle-only dashboard

**ANTI-PATTERN**  
The dashboard is a uniform grid of same-size cards regardless of metric importance, trend, actionability, or comparison need.

**WHY IT FAILS**  
Uniform geometry implies equal priority and encourages a generic template rather than a decision surface.

**EVIDENCE**  
- Dashboards should surface at-a-glance actionable information [S24]. **Class C**
- Visual hierarchy requires priority to be reflected by scale, position, color, and grouping [S10]. **Class C**
- AI-design commentary repeatedly identifies identical card grids as a common generated default [S29][S30][S31]. **Class D**

**DETECTION HEURISTIC**
- Flag if >70% of dashboard modules have identical dimensions/style but represent unequal importance.
- Ask for each widget: “What decision/action does this support?”
- Flag decorative charts with no comparison/context.

**BAD EXAMPLE**  
Eight equal cards: revenue, uptime, critical incidents, avatar count, plan type, and tips all have equal visual weight.

**BETTER APPROACH**  
Prioritize: critical state/action → trends/comparisons → supporting detail. Vary presentation only when the information role differs.

**EXCEPTIONS**  
True modular monitoring grids where modules intentionally have equal status.

**SEVERITY**  
MEDIUM → HIGH.

**CONFIDENCE**  
HIGH.

---

# 5. UX / interaction anti-patterns

## AP-U01 — Hover-only essential actions

**ANTI-PATTERN**  
Actions or information required to complete a task exist only on pointer hover.

**WHY IT FAILS**  
Touch users do not have hover; keyboard and assistive-technology users may miss the interaction; discoverability drops.

**EVIDENCE**  
- NN/g notes hover states are unavailable to non-mouse users and advises against hiding icon labels/actions behind hover [S33][S34]. **Class C**
- WCAG requires keyboard accessibility and robust hover/focus content behavior [S5][S6]. **Class A**

**DETECTION HEURISTIC**
- Search CSS/JS for `:hover` or pointer-enter that reveals task-essential controls.
- Verify keyboard focus reveals equivalent function.
- On coarse-pointer/touch, ensure controls remain visible or have a direct activation route.

**BAD EXAMPLE**  
Row edit/delete actions appear only when the mouse hovers over the table row.

**BETTER APPROACH**  
Persist important actions; use contextual menus with visible triggers; allow hover as enhancement, not sole access.

**EXCEPTIONS**  
Purely supplementary previews/tooltips.

**SEVERITY**  
HIGH / CRITICAL if no alternative exists.

**CONFIDENCE**  
HIGH.

---

## AP-U02 — Ambiguous icon-only actions

**ANTI-PATTERN**  
Unfamiliar or overloaded icons replace labels for important actions.

**WHY IT FAILS**  
Most icons are not universal; users must guess meaning.

**EVIDENCE**  
NN/g usability research states that most icons need text labels and documents confusion from nonstandard icon meanings [S34]. **Class B/C**

**DETECTION HEURISTIC**
- Allow icon-only for widely familiar, contextual actions when space is constrained and accessible name exists.
- Flag icon-only primary navigation.
- Flag unfamiliar icons with no visible label and no robust tooltip.
- Always require accessible name.

**BAD EXAMPLE**  
A sparkle icon means “Generate report,” a hexagon means “Policies,” and a clock means “History” with no labels.

**BETTER APPROACH**  
Use icon + text for navigation and important actions; reserve icon-only for conventional controls.

**EXCEPTIONS**  
Dense expert toolbars with learned conventions and accessible help.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-U03 — Modal by default

**ANTI-PATTERN**  
Any create/edit/view action opens a modal regardless of task complexity or frequency.

**WHY IT FAILS**  
Modals interrupt flow, block context, and become cumbersome for repeatable or complex tasks.

**EVIDENCE**  
- NN/g: modal dialogs interrupt users and should be used only when interruption is worth the cost [S7]. **Class C**
- Carbon: use modals sparingly for short, non-frequent tasks; repeatable work should often live on the main page; very large content suggests a full page [S35]. **Class C**

**DETECTION HEURISTIC**
- Flag modal forms with multi-step complex workflows, long scrolling, nested navigation, or tasks repeated many times per session.
- Flag modal-on-modal.
- Flag read-only detail modals when side panel/in-page detail would preserve context better.

**BAD EXAMPLE**  
Editing a complex customer profile with 25 fields inside a 600px modal.

**BETTER APPROACH**  
Inline edit, side panel, dedicated detail page, or nonmodal drawer depending on context.

**EXCEPTIONS**  
Short confirmation, focused create/edit, urgent blocking decision.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-U04 — Ambiguous navigation

**ANTI-PATTERN**  
Labels, placement, icons, and hierarchy do not let users predict where navigation leads.

**WHY IT FAILS**  
Poor information scent increases searching and misclicks.

**EVIDENCE**  
NN/g research shows hidden and ambiguous navigation decreases discoverability and increases task cost [S36][S37]. **Class B/C**

**DETECTION HEURISTIC**
- Flag vague labels (“Explore”, “More”, “Workspace”) when they hide core destinations without context.
- Flag inconsistent nav labels for the same destination.
- Flag icons that conflict with established location conventions.

**BAD EXAMPLE**  
Billing is hidden under “Workspace,” while account settings are under an unlabeled gear and team settings under a kebab menu.

**BETTER APPROACH**  
Use user-language labels, stable location, clear selected state, and predictable grouping.

**EXCEPTIONS**  
Products whose users have strong domain terminology that testing validates.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-U05 — Hidden functionality without a discoverability strategy

**ANTI-PATTERN**  
Core features are tucked into menus, hover actions, gestures, or progressive disclosure solely to make the UI look clean.

**WHY IT FAILS**  
Hidden UI increases interaction cost and reduces discoverability.

**EVIDENCE**  
- NN/g quantitative testing found hidden navigation less discoverable and worse on task metrics [S37]. **Class B**
- Progressive disclosure is useful for advanced/rare options, not for hiding frequent primary tasks [S38]. **Class C**

**DETECTION HEURISTIC**
- Classify feature frequency/importance.
- Core frequent actions must not require guessing an unlabeled gesture/menu.
- Secondary/advanced functions may be progressively disclosed.

**BAD EXAMPLE**  
“Export” — a daily task — exists only in a three-dot menu beside the page title.

**BETTER APPROACH**  
Expose high-frequency/high-value actions; hide low-frequency complexity.

**EXCEPTIONS**  
Severe space constraints where a familiar visible trigger preserves discoverability.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-U06 — Excessive onboarding / coach-mark tour

**ANTI-PATTERN**  
First launch blocks the product with a long carousel or highlights every visible UI element before the user has context.

**WHY IT FAILS**  
Users want to start tasks; untimely instruction is easy to ignore and adds friction.

**EVIDENCE**  
NN/g onboarding research recommends instructional overlays be timely, unobtrusive, and tied to first encounter with the relevant feature; it shows overload as a poor pattern [S39]. **Class B/C**

**DETECTION HEURISTIC**
- Flag mandatory tours >3–5 steps before the user can perform a core task unless the domain demands setup.
- Flag overlays explaining standard controls.
- Prefer contextual education at moment of need.

**BAD EXAMPLE**  
Nine-step tour explains search, profile avatar, sidebar, settings, notifications, help, filters, sort, and export before the user sees their data.

**BETTER APPROACH**  
Get to value quickly; use empty states, sample data, inline hints, and contextual tips.

**EXCEPTIONS**  
Safety-critical setup, permissions, regulated workflows, or unavoidable initial configuration.

**SEVERITY**  
MEDIUM → HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-U07 — Confirmation fatigue

**ANTI-PATTERN**  
Routine reversible actions trigger confirmation dialogs.

**WHY IT FAILS**  
Users habituate and click through warnings automatically; the confirmation loses protective value.

**EVIDENCE**  
NN/g explicitly documents the “computer that cried confirm” effect and recommends confirmations for serious/irreversible consequences, not routine actions [S40][S41]. **Class C**

**DETECTION HEURISTIC**
- If action is low-impact and reversible, prefer immediate action + Undo.
- Confirmation is justified by high cost, irreversible loss, money/legal impact, privilege changes, or destructive bulk operations.
- Flag generic “Are you sure?” dialogs.

**BAD EXAMPLE**  
Confirm before archiving, muting, hiding, marking read, changing a filter, or leaving a non-edited page.

**BETTER APPROACH**  
Optimistic action + visible status + Undo; reserve strong confirmation for costly decisions.

**EXCEPTIONS**  
Regulated or safety-critical workflows.

**SEVERITY**  
MEDIUM; HIGH when warnings become ineffective around destructive actions.

**CONFIDENCE**  
HIGH.

---

## AP-U08 — Generic confirmation copy

**ANTI-PATTERN**  
Dialog says “Are you sure?” with “OK / Cancel.”

**WHY IT FAILS**  
It does not help the user verify the object, consequence, or action.

**EVIDENCE**  
NN/g recommends specific consequence-focused confirmations and action labels rather than generic Yes/No/OK [S41][S42]. **Class C**

**DETECTION HEURISTIC**
- Flag confirmation title/body missing object name/count/consequence.
- Flag affirmative button labels `OK`, `Yes`, `Confirm` when a specific verb can be used.

**BAD EXAMPLE**  
“Are you sure?” — [Cancel] [OK]

**BETTER APPROACH**  
“Delete 18 invoices? This can’t be undone.” — [Cancel] [Delete 18 invoices]

**EXCEPTIONS**  
Very simple acknowledgement dialogs where no action ambiguity exists.

**SEVERITY**  
HIGH for destructive actions.

**CONFIDENCE**  
HIGH.

---

# 6. Responsive anti-patterns

## AP-R01 — Desktop simply compressed

**ANTI-PATTERN**  
The desktop layout is reduced in width without reordering, collapsing, simplifying, or changing interaction models.

**WHY IT FAILS**  
Smaller viewports change available space, touch input, reading measure, and priority.

**EVIDENCE**  
- WCAG Reflow requires non-exempt content to work at 320 CSS px without two-dimensional scrolling/loss [S8]. **Class A**
- Apple requires layouts to adapt gracefully and notes that side-by-side content may need to stack as space/text size changes [S16]. **Class C**

**DETECTION HEURISTIC**
- Screenshot/test at 320, 375, 768, 1024, 1280+ widths.
- Flag arbitrary shrink-to-fit typography or controls.
- Flag layouts retaining desktop multi-column geometry when content becomes cramped.

**BAD EXAMPLE**  
Three-column dashboard simply shrinks cards to 105px wide on mobile.

**BETTER APPROACH**  
Reprioritize, stack, collapse, move secondary actions, change navigation pattern, and preserve touch targets.

**EXCEPTIONS**  
Canvas/map/editor experiences where zoom/pan is intrinsic.

**SEVERITY**  
CRITICAL if core content/functions become unusable.

**CONFIDENCE**  
HIGH.

---

## AP-R02 — Uncontained horizontal overflow

**ANTI-PATTERN**  
One wide component makes the entire page horizontally scroll.

**WHY IT FAILS**  
Users lose place and must pan for unrelated content; it violates Reflow for non-exempt content.

**EVIDENCE**  
WCAG Reflow explicitly recommends limiting two-dimensional scrolling to the content section that requires it (e.g. data table), not the whole page [S8]. **Class A**

**DETECTION HEURISTIC**
- At 320 CSS px, run `document.documentElement.scrollWidth > clientWidth`.
- If true, locate offender.
- Tables/maps/code may scroll inside their own region; normal prose/navigation/forms must reflow.

**BAD EXAMPLE**  
A 12-column table forces header, search, pagination, and page copy to pan horizontally.

**BETTER APPROACH**  
Contain the table’s overflow; keep surrounding UI within viewport.

**EXCEPTIONS**  
Essential two-dimensional canvases.

**SEVERITY**  
CRITICAL.

**CONFIDENCE**  
HIGH.

---

## AP-R03 — Table destroyed instead of adapted

**ANTI-PATTERN**  
A complex data table is blindly converted to stacked cards, hiding comparison relationships, or is squeezed until values truncate.

**WHY IT FAILS**  
Tables support finding, comparing, inspecting, and acting on records; preserving those jobs matters more than eliminating horizontal scroll.

**EVIDENCE**  
- NN/g identifies core table tasks including comparison and record actions [S43]. **Class C**
- WCAG explicitly allows two-dimensional scrolling for data tables where layout is required for meaning [S8]. **Class A**
- Carbon advises giving dense tables width and provides table-specific behaviors [S15]. **Class C**

**DETECTION HEURISTIC**
- Identify primary table task: scan, compare, act, edit.
- Do not card-transform if cross-row/column comparison is core.
- On mobile, prioritize columns, allow contained horizontal scroll, freeze identifiers when useful, or offer a detail view.

**BAD EXAMPLE**  
A financial table becomes 40 vertical cards, making price comparisons impossible.

**BETTER APPROACH**  
Preserve table semantics; reduce visible columns or provide controlled scroll/detail.

**EXCEPTIONS**  
Entity lists where each row is naturally independent and comparison is not important.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-R04 — Sidebar copied to mobile

**ANTI-PATTERN**  
Desktop sidebar remains permanently visible or simply becomes narrower on small screens.

**WHY IT FAILS**  
It consumes scarce width and may leave tiny content or targets.

**EVIDENCE**  
Responsive layout guidance supports relocating/collapsing sections while preserving access [S8][S16]. Hidden-navigation research shows that collapse has discoverability costs, so the replacement must remain obvious [S37]. **Class A/B/C**

**DETECTION HEURISTIC**
- On narrow viewports, test whether persistent sidebar leaves adequate content width.
- If collapsed, ensure visible labeled trigger and clear current location.
- For 3–5 high-frequency destinations, consider visible bottom/tab navigation where platform/context fits.

**BAD EXAMPLE**  
240px sidebar remains in a 375px viewport, leaving 135px for content.

**BETTER APPROACH**  
Drawer, sheet, compact rail, bottom nav, or adaptive visible navigation based on task frequency.

**EXCEPTIONS**  
Tablet landscape / desktop-like widths where persistent navigation remains efficient.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-R05 — Arbitrary content hiding on small screens

**ANTI-PATTERN**  
Information disappears merely to make the layout fit, with no priority or alternate access.

**WHY IT FAILS**  
Responsive design may relocate content, but loss of information/functionality can be an accessibility failure.

**EVIDENCE**  
WCAG Reflow permits adjusting/relocating content but requires no loss of information or functionality for non-exempt content [S8]. **Class A**

**DETECTION HEURISTIC**
- Compare desktop/mobile feature and content inventory.
- Any hidden functional/content element needs classification: redundant, secondary-but-accessible-elsewhere, or intentionally unavailable with reason.
- Flag `display:none` at breakpoints on unique important content/actions.

**BAD EXAMPLE**  
Mobile hides account limits, export, timestamps, and error details with no alternate route.

**BETTER APPROACH**  
Reorder, collapse behind explicit disclosure, move to detail view, or prioritize columns — do not silently delete.

**EXCEPTIONS**  
Truly redundant decorative content.

**SEVERITY**  
CRITICAL/HIGH.

**CONFIDENCE**  
HIGH.

---

# 7. Accessibility anti-patterns

## AP-A01 — Insufficient text contrast

**ANTI-PATTERN**  
Foreground text lacks required luminance contrast.

**WHY IT FAILS**  
Text becomes unreadable for many users, particularly low-vision users.

**EVIDENCE**  
WCAG 2.2 SC 1.4.3 [S1]. **Class A**

**DETECTION HEURISTIC**
- Normal text: at least 4.5:1.
- Qualifying large text: at least 3:1.
- Test all interactive states and supported themes.
- Evaluate text over gradients/images at the least-contrasting point.

**BAD EXAMPLE**  
`#9CA3AF` small text on `#F3F4F6` without checking ratio.

**BETTER APPROACH**  
Use semantic text tokens with tested surface combinations.

**EXCEPTIONS**  
WCAG-defined exceptions such as incidental/logotype situations.

**SEVERITY**  
HIGH / CRITICAL if essential.

**CONFIDENCE**  
HIGH.

---

## AP-A02 — Missing or weak keyboard focus

**ANTI-PATTERN**  
Focus outline is removed or too subtle to track.

**WHY IT FAILS**  
Keyboard users lose orientation.

**EVIDENCE**  
WCAG Focus Visible and Focus Appearance guidance [S2][S44]. **Class A**

**DETECTION HEURISTIC**
- Tab through every interactive element.
- Hard fail if focus is visually absent.
- Prefer an indicator at least comparable to a 2 CSS-pixel perimeter and ~3:1 focus-state contrast as the stronger WCAG 2.4.13 guidance.
- Do not rely solely on shadow/glow outside component bounds.

**BAD EXAMPLE**  
`outline: none` with no replacement.

**BETTER APPROACH**  
Consistent focus ring using a token designed to survive light/dark surfaces.

**EXCEPTIONS**  
None for keyboard-operable interactive elements.

**SEVERITY**  
CRITICAL.

**CONFIDENCE**  
HIGH.

---

## AP-A03 — Color-only communication

**ANTI-PATTERN**  
Status or meaning is conveyed solely through hue.

**WHY IT FAILS**  
Not everyone perceives color differences reliably.

**EVIDENCE**  
WCAG SC 1.4.1 [S3]. **Class A**

**DETECTION HEURISTIC**
- Remove/desaturate color in screenshot: can statuses still be distinguished?
- Error/success/warning must have text, icon/shape, pattern, position, or other redundant cue.

**BAD EXAMPLE**  
A table marks failed rows only by red background.

**BETTER APPROACH**  
Icon + label + color; chart lines with labels/patterns where needed.

**EXCEPTIONS**  
Color may reinforce meaning, just not be the only cue.

**SEVERITY**  
CRITICAL/HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-A04 — Undersized targets

**ANTI-PATTERN**  
Interactive controls are too small or too tightly packed.

**WHY IT FAILS**  
Users with motor limitations and touch users are more likely to miss or activate adjacent controls.

**EVIDENCE**  
WCAG 2.2 SC 2.5.8 requires a 24×24 CSS px target or qualifying spacing/exception; Apple generally recommends 44×44 pt hit regions [S45][S17]. **Class A/C**

**DETECTION HEURISTIC**
- Hard audit against WCAG 24×24 CSS px or spacing exceptions.
- For touch-first primary controls, aim larger (platform guidance ~44×44pt).
- Measure hit area, not visual glyph size.

**BAD EXAMPLE**  
12px kebab icons spaced 4px apart in a mobile row.

**BETTER APPROACH**  
Expand invisible hit area while retaining compact visual icon.

**EXCEPTIONS**  
WCAG-defined inline/equivalent/essential/user-agent cases.

**SEVERITY**  
HIGH / CRITICAL if essential controls are unusable.

**CONFIDENCE**  
HIGH.

---

## AP-A05 — Motion ignores user preference

**ANTI-PATTERN**  
Nonessential movement continues even when the user requests reduced motion.

**WHY IT FAILS**  
Motion can trigger distraction, nausea, dizziness, or headaches for susceptible users.

**EVIDENCE**  
WCAG Animation from Interactions recommends disabling nonessential interaction-triggered motion and using `prefers-reduced-motion`; Apple says motion should be purposeful and optional [S46][S47]. **Class A/C**

**DETECTION HEURISTIC**
- Audit CSS/JS animations under `prefers-reduced-motion: reduce`.
- Remove/reduce transforms, parallax, large-scale movement; retain essential state communication through instant or opacity-based alternatives where appropriate.

**BAD EXAMPLE**  
Cards fly in and panels slide/zoom on every route even with reduced motion enabled.

**BETTER APPROACH**  
Provide reduced/instant transitions and preserve state clarity.

**EXCEPTIONS**  
Motion essential to meaning/function, with careful consideration.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-A06 — Non-text UI has insufficient contrast

**ANTI-PATTERN**  
Icons, field boundaries, focus/selection cues, chart lines, or controls disappear into adjacent surfaces.

**WHY IT FAILS**  
Users may not perceive the component or state.

**EVIDENCE**  
WCAG 1.4.11 requires 3:1 contrast for visual information necessary to identify UI components/states and meaningful graphical objects [S4]. **Class A**

**DETECTION HEURISTIC**
- Check essential icons, outlines, states, chart marks against adjacent colors.
- Test the least-contrasting part of gradients.
- Avoid ultra-thin lines that visually anti-alias below practical contrast.

**BAD EXAMPLE**  
1px `#3F3F46` input outline on `#27272A` dark surface, barely visible.

**BETTER APPROACH**  
Increase luminance contrast, thickness, fill difference, or redundant state cue.

**EXCEPTIONS**  
Inactive components and purely decorative graphics per WCAG.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

# 8. Dashboard anti-patterns

## AP-D01 — KPI wallpaper

**ANTI-PATTERN**  
Dashboard contains many KPI cards because metrics exist, not because users need to act on them.

**WHY IT FAILS**  
Dashboards are meant to support fast monitoring/action; irrelevant KPIs dilute signal.

**EVIDENCE**  
NN/g defines dashboards as at-a-glance information for rapid action and warns they are not expansive data-exploration views [S24]. **Class C**

**DETECTION HEURISTIC**
- Every KPI must answer: “What decision changes if this value changes?”
- Flag metrics with no target, trend, comparison, threshold, or action where such context is needed.
- Prefer fewer actionable metrics over a grid of vanity numbers.

**BAD EXAMPLE**  
“Total users 128,402” with no period, change, target, segment, or action.

**BETTER APPROACH**  
Show trend, benchmark/target, status, and relevant drilldown.

**EXCEPTIONS**  
Executive overview where raw totals are genuinely decision inputs.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-D02 — Decorative charts

**ANTI-PATTERN**  
Charts are included for visual interest without a question, comparison, or decision.

**WHY IT FAILS**  
Visualization consumes attention and can make data harder rather than easier to understand.

**EVIDENCE**  
NN/g recommends starting chart choice from the point the audience needs to understand and avoiding clutter [S48]. **Class C**

**DETECTION HEURISTIC**
- Require a stated chart question (“trend over time?”, “compare categories?”, “distribution?”).
- Flag chart with no axis/context/labels where interpretation requires guessing.
- Flag donut/gauge/area chart chosen solely for aesthetics when simpler encoding is clearer.

**BAD EXAMPLE**  
Three unlabeled sparkline cards only to “make the dashboard feel alive.”

**BETTER APPROACH**  
Use text/number when a chart adds no comparative insight; choose chart type by analytical task.

**EXCEPTIONS**  
Ambient monitoring where shape/trend recognition is itself useful.

**SEVERITY**  
MEDIUM → HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-D03 — Equal priority for unequal states

**ANTI-PATTERN**  
Critical incident, neutral usage metric, and onboarding tip receive equal card weight.

**WHY IT FAILS**  
The dashboard fails its monitoring purpose.

**EVIDENCE**  
Visual hierarchy guidance [S10] + dashboard purpose [S24].

**DETECTION HEURISTIC**
- Rank modules by urgency/actionability.
- Critical/exception state should be findable in a squint test.
- Tips/help must not outrank urgent operational state.

**BAD EXAMPLE**  
“3 services down” appears in the same gray card style as “Invite teammates.”

**BETTER APPROACH**  
Use placement, semantic state, concise copy, and direct action for exceptions.

**EXCEPTIONS**  
None when safety/business-critical state exists.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

# 9. Landing-page anti-patterns

## AP-P01 — Generic centered hero formula

**ANTI-PATTERN**  
Centered eyebrow → giant gradient headline → vague subhead → dual CTA → abstract product screenshot → three equal feature cards, regardless of product.

**WHY IT FAILS**  
No single element is necessarily wrong, but the composition is highly templated and often fails to express why this product differs.

**EVIDENCE**  
- Emerging HCI work supports a real homogenization risk in vibe-coded web design [S26]. **Class B/D**
- Independent AI-design analyses repeatedly identify this same composition as a generated default [S29][S30][S31]. **Class D**

**DETECTION HEURISTIC**
- If 5+ canonical AI-smell elements co-occur, require a redesign review.
- Ask whether the macrostructure follows the user’s decision journey or merely a template.

**BAD EXAMPLE**  
“Supercharge your workflow” over purple gradient + “Get started / Learn more” + three generic benefit cards.

**BETTER APPROACH**  
Choose a structure based on product evidence: problem → proof → workflow; interactive demo; customer outcome; data-led proof; comparison; role-specific entry.

**EXCEPTIONS**  
Simple products where the standard structure is genuinely the clearest.

**SEVERITY**  
STYLE PREFERENCE → MEDIUM if differentiation/value clarity suffers.

**CONFIDENCE**  
MEDIUM.

---

## AP-P02 — Vague benefit copy with no product evidence

**ANTI-PATTERN**  
Headline promises “smarter/faster/seamless/next-generation” without identifying what the product does.

**WHY IT FAILS**  
Users cannot form a concrete mental model or evaluate fit.

**EVIDENCE**  
This is primarily a content/information-scent problem supported by general usability principles of clarity, match to user language, and navigation scent [S21][S36]. **Class C**

**DETECTION HEURISTIC**
- Above the fold should let a target user answer: What is it? Who is it for? What meaningful outcome/function does it provide?
- Flag adjective-heavy copy with no domain nouns or concrete verbs.

**BAD EXAMPLE**  
“Transform the future of intelligent work.”

**BETTER APPROACH**  
“Monitor cloud costs by service, detect anomalous spend, and alert FinOps teams before budgets are exceeded.”

**EXCEPTIONS**  
Established brands/products where category understanding is already universal.

**SEVERITY**  
HIGH for acquisition pages.

**CONFIDENCE**  
HIGH.

---

## AP-P03 — Multiple equal hero CTAs

**ANTI-PATTERN**  
Two or three hero CTAs look equally primary despite different commitment levels.

**WHY IT FAILS**  
Priority becomes ambiguous.

**EVIDENCE**  
Primary-action guidance [S14][S17].

**DETECTION HEURISTIC**
- One visually primary CTA per hero decision context.
- Secondary CTA may remain visible but lower emphasis.
- If audiences require two equal paths, label them by audience/outcome.

**BAD EXAMPLE**  
[Start free] [Book demo] [Watch video] all filled in bright accent.

**BETTER APPROACH**  
Primary: Start free. Secondary: Book a demo. Tertiary text link: Watch 90-sec demo.

**EXCEPTIONS**  
True audience split with equal business/user value.

**SEVERITY**  
MEDIUM/HIGH.

**CONFIDENCE**  
HIGH.

---

# 10. Dark-mode anti-patterns

## AP-DM01 — Mechanical color inversion

**ANTI-PATTERN**  
Light theme colors are simply inverted or backgrounds changed to near-black without adapting semantics, images, borders, charts, elevation, and assets.

**WHY IT FAILS**  
Dark mode is not a photographic negative. Assets can disappear, separators can vanish, and elevation requires different treatment.

**EVIDENCE**  
- Apple says dark colors are not necessarily inversions and recommends adaptive semantic colors [S49]. **Class C**
- NN/g documents graphics, contrast, divider, and asset failures in poorly implemented dark mode [S50]. **Class B/C**

**DETECTION HEURISTIC**
- Compare all semantic tokens, logos, illustrations, chart palettes, borders, overlays, and elevation in both themes.
- Flag one-to-one inversion scripts without theme-specific validation.

**BAD EXAMPLE**  
White becomes black, black becomes white, but chart/grid/divider/image colors stay untouched.

**BETTER APPROACH**  
Define semantic light/dark tokens and validate actual content in both.

**EXCEPTIONS**  
Very simple monochrome text experiences where inversion has been tested.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-DM02 — Dark mode relies on shadows alone

**ANTI-PATTERN**  
Depth/elevation is encoded only with dark shadows on already dark surfaces.

**WHY IT FAILS**  
Shadows become difficult to perceive.

**EVIDENCE**  
Atlassian explicitly notes dark-mode elevations rely on surface color differences in addition to shadows [S19]. Apple similarly uses different base/elevated dark surfaces [S49]. **Class C**

**DETECTION HEURISTIC**
- Turn off shadows: can users still distinguish overlay/elevated surfaces?
- Require tonal/layer separation where depth is important.

**BAD EXAMPLE**  
Popover and page background are both #111; only a black shadow separates them.

**BETTER APPROACH**  
Use semantic elevated surfaces plus restrained shadow/border.

**EXCEPTIONS**  
High-contrast outline-based systems.

**SEVERITY**  
MEDIUM/HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-DM03 — Over-saturated accents on dark backgrounds

**ANTI-PATTERN**  
Very saturated colors are used for small text/icons without practical contrast/legibility validation.

**WHY IT FAILS**  
Some saturated colors can visually blur or fail contrast on dark surfaces.

**EVIDENCE**  
NN/g documents legibility issues with saturated colors in dark mode and reiterates WCAG ratios [S50]. **Class B/C**

**DETECTION HEURISTIC**
- Test actual ratios; do not infer accessibility from saturation.
- Inspect small saturated text/icons for practical visibility, not just numerical pass.
- Reserve strongest saturation for larger/focal elements where suitable.

**BAD EXAMPLE**  
Tiny electric-blue metadata text on charcoal.

**BETTER APPROACH**  
Adjust luminance/saturation separately for dark theme.

**EXCEPTIONS**  
Large non-text decorative areas.

**SEVERITY**  
HIGH if contrast fails; otherwise MEDIUM.

**CONFIDENCE**  
HIGH.

---

## AP-DM04 — Pure white everywhere on near-black

**ANTI-PATTERN**  
All text uses maximum luminance regardless of hierarchy.

**WHY IT FAILS**  
It creates excessive visual intensity and destroys text hierarchy; font weight also appears different in dark polarity.

**EVIDENCE**  
NN/g notes that light text on dark backgrounds can appear heavier and that both overly thin and overly thick text can become problematic [S50]. Apple uses primary/secondary/tertiary label systems [S49]. **Class B/C**

**DETECTION HEURISTIC**
- Require semantic text levels while maintaining contrast.
- Do not lower secondary text below accessible contrast just to soften it.

**BAD EXAMPLE**  
Title, body, caption, metadata, and disabled labels are all #FFF.

**BETTER APPROACH**  
Use tested semantic foreground tokens with decreasing emphasis.

**EXCEPTIONS**  
Minimal displays with one level of text.

**SEVERITY**  
MEDIUM.

**CONFIDENCE**  
HIGH.

---

# 11. Animation anti-patterns

## AP-M01 — Animation for every interaction

**ANTI-PATTERN**  
Every hover, click, route, card, tab, number, and panel animates.

**WHY IT FAILS**  
Frequent motion consumes time and attention; repeated decorative motion can become exhausting.

**EVIDENCE**  
Apple explicitly says not to add motion for its own sake and generally to avoid motion on frequently occurring UI interactions beyond familiar system feedback [S47]. **Class C**
WCAG cautions against nonessential interaction-triggered motion [S46]. **Class A**

**DETECTION HEURISTIC**
- Inventory animations by frequency × amplitude × duration × task relevance.
- Flag decorative transforms on frequent controls.
- Allow subtle state transitions where they clarify causality.

**BAD EXAMPLE**  
Every card lifts/tilts, every icon rotates, every number counts up, every panel slides.

**BETTER APPROACH**  
Animate state change, spatial continuity, feedback, or orientation — not decoration by default.

**EXCEPTIONS**  
Playful/entertainment experiences where motion is part of the value.

**SEVERITY**  
MEDIUM → HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-M02 — Scroll-triggered reveal blocks reading

**ANTI-PATTERN**  
Content starts invisible and fades/slides in only after scrolling, delaying scanning.

**WHY IT FAILS**  
Users must wait for content they already requested; animation gets in the way of consumption.

**EVIDENCE**  
NN/g specifically reports that misused scroll-triggered text animations delay users [S51]. **Class C**

**DETECTION HEURISTIC**
- Flag essential text with initial `opacity:0`, transform, or delayed reveal tied to viewport entry.
- Decorative imagery can animate if content remains immediately available.

**BAD EXAMPLE**  
Every FAQ row waits 500ms after entering viewport before text appears.

**BETTER APPROACH**  
Keep information visible; animate nonessential decoration or very brief structural transitions.

**EXCEPTIONS**  
Narrative scrollytelling where staged reveal is the content model.

**SEVERITY**  
MEDIUM/HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-M03 — Blocking animation

**ANTI-PATTERN**  
Users cannot interact until a transition or celebration finishes.

**WHY IT FAILS**  
It makes repeat interactions slower and reduces agency.

**EVIDENCE**  
Apple recommends letting people cancel motion and not making them wait for animations, especially repeated ones [S47]. **Class C**

**DETECTION HEURISTIC**
- No routine animation should disable unrelated controls merely to finish.
- Flag route/overlay animations >~500ms that block input without necessity (duration threshold is heuristic, not standard).

**BAD EXAMPLE**  
A 1.2s page transition locks the app after every sidebar click.

**BETTER APPROACH**  
Keep interactions available; use short interruptible transitions.

**EXCEPTIONS**  
Atomic state transitions where interaction during the transition would corrupt state.

**SEVERITY**  
HIGH.

**CONFIDENCE**  
HIGH.

---

## AP-M04 — Persistent motion without control

**ANTI-PATTERN**  
Marquees, carousels, animated gradients, tickers, or decorative loops run continuously next to task content.

**WHY IT FAILS**  
Persistent motion competes for attention and can create accessibility barriers.

**EVIDENCE**  
WCAG 2.2.2 requires pause/stop/hide for certain automatically moving/blinking/scrolling content lasting more than five seconds when presented with other content [S52]. **Class A**

**DETECTION HEURISTIC**
- Detect infinite animations and auto-advancing content.
- If it lasts >5s and meets WCAG conditions, require pause/stop/hide unless essential.
- Honor reduced motion.

**BAD EXAMPLE**  
Infinite animated aurora behind a settings form.

**BETTER APPROACH**  
Static background, finite entrance, or user-controllable motion.

**EXCEPTIONS**  
Essential activity indicator or real-time motion representation, subject to applicable accessibility rules.

**SEVERITY**  
HIGH/CRITICAL.

**CONFIDENCE**  
HIGH.

---

# 12. AI-generated UI look: what is actually defensible?

There is now research supporting **design homogenization risk** in web vibe coding [S26], but there is not a scientific law that “purple + cards = AI.” The correct model is **cluster detection**.

A single marker is weak evidence. A cluster of unmotivated defaults is stronger evidence that the interface has not been sufficiently art-directed.

## Commonly recurring AI-template markers

Treat these as **D-class smell signals** unless they also cause a usability issue:

- violet/indigo/cyan gradient without brand rationale;
- gradient headline text;
- centered hero on nearly every page;
- generic “AI sparkles” iconography;
- Inter/system font everywhere with no typographic direction;
- Lucide/Heroicons defaults with no selection logic;
- 3 equal feature cards;
- identical rounded cards across unrelated information;
- `rounded-xl/2xl` or `rounded-full` nearly everywhere;
- 1px gray border around every surface;
- glass cards + glow + dark navy background;
- decorative blurred aurora blobs;
- unrequested dark mode;
- oversized hero headline;
- dual equal CTAs;
- vague copy such as “supercharge,” “reimagine,” “next-generation,” “seamless,” “powerful” with little product evidence;
- fake-looking dashboard mockup composed of generic rectangles;
- hover `translateY(-2px)` on every card;
- excessive gradient badges/pills;
- repeated “icon + heading + two lines” component triplets;
- perfectly symmetric sections even when content importance is asymmetric;
- empty states/onboarding/error/loading states absent because the generator optimized for the hero screenshot;
- visually polished happy path but no long-content, empty, error, permission, or loading handling;
- local one-off spacing/radius/color values rather than a coherent token system.

## AI smell scoring (heuristic, not a factual classifier)

```
score = 0

+1 for each unmotivated visual default marker
+2 if 3+ unrelated surfaces use the same card recipe
+2 if product-specific nouns/actions are missing above the fold
+2 if only the happy path is designed
+2 if no brand/design tokens exist
+2 if mobile is a compressed desktop layout
+2 if accessible focus/reduced-motion states are absent

0–3  : low concern
4–7  : review for generic/template feel
8–12 : strong AI-template smell; redesign pass required
13+  : do not ship without structural + visual re-art-direction
```

**Never** use this score to reject a UI solely because it uses a popular font, purple, cards, or rounded corners.

---

# 13. Classification matrix

| Pattern | Default class | Escalate when… |
|---|---|---|
| Gradient use | STYLE PREFERENCE | Contrast/hierarchy suffers → MEDIUM/HIGH |
| Purple/blue AI gradient | STYLE PREFERENCE | Generic identity + hierarchy issues → MEDIUM |
| Glassmorphism | STYLE PREFERENCE | Content-layer overuse / contrast instability → MEDIUM/HIGH |
| Blur | STYLE PREFERENCE | Readability/performance/hierarchy suffers → MEDIUM/HIGH |
| Shadows | MEDIUM | State/elevation ambiguity → HIGH |
| Large radius | STYLE PREFERENCE | Semantic differentiation collapses → MEDIUM |
| Pill everything | STYLE PREFERENCE | Status/action ambiguity → MEDIUM/HIGH |
| Cards inside cards | MEDIUM | Responsive/readability failure → HIGH |
| Borders everywhere | MEDIUM | Hierarchy becomes unreadable → HIGH |
| Excessive whitespace | MEDIUM | Workflow efficiency/task visibility suffers → HIGH |
| Excessive animation | MEDIUM | Motion accessibility or blocking → HIGH/CRITICAL |
| Glow effects | STYLE PREFERENCE | Replaces state/focus or harms contrast → HIGH |
| Giant headings | MEDIUM | Core task pushed out / mobile breaks → HIGH |
| Center alignment | STYLE PREFERENCE | Long operational content becomes hard to scan → MEDIUM |
| Competing primary CTAs | HIGH | Destructive ambiguity → CRITICAL risk |
| Low-contrast secondary text | HIGH | Task-essential / WCAG failure → CRITICAL |
| Hover-only functionality | HIGH | No keyboard/touch alternative → CRITICAL |
| Uncontained mobile overflow | CRITICAL | — |
| Missing keyboard focus | CRITICAL | — |
| Color-only state | HIGH/CRITICAL | — |
| Confirmation fatigue | MEDIUM | Weakens destructive warnings → HIGH |
| Dark-mode mechanical inversion | HIGH | Essential content disappears → CRITICAL |

---

# 14. AI UI Smell Test

Before shipping, answer **yes/no**:

1. Could I replace the logo/name with a competitor and leave 90% of the interface unchanged?
2. Did the palette come from a brief/design system, or from a default “modern SaaS” association?
3. Are purple/blue gradients, glass, glows, aurora blobs, or dark navy being used without a product-specific reason?
4. Are three or more unrelated sections represented by identical rounded cards?
5. Is every container rounded, bordered, and shadowed?
6. Are all actions pills?
7. Is the hero a centered headline + vague subhead + two CTAs + generic product mockup?
8. Does the page use generic benefit copy instead of concrete product nouns and actions?
9. Is every section perfectly symmetric despite unequal information priority?
10. Are animations mostly hover lifts/fades rather than state/orientation feedback?
11. Does the UI have a clear primary action per decision context?
12. Does the dashboard answer decisions, or merely display rectangles with numbers?
13. Are real empty/error/loading/permission/long-content states designed?
14. Does mobile reflect prioritization, or only compression?
15. Are spacing, radii, color, type, elevation, and motion driven by tokens?
16. Does the UI have a recognizable product-specific visual or interaction idea?
17. Does any decoration compete with the actual task?
18. Does the interface still communicate hierarchy in grayscale?
19. Does it still communicate hierarchy when blurred/squinted?
20. Is there any component whose only justification is “this makes it look modern”?

**Rule:** if ≥5 answers indicate generic defaults, perform an intentionality pass. If ≥8, do not call the design finished.

---

# 15. Pre-generation checklist

The coding agent must establish these before generating UI:

- [ ] Identify **user type**, core job, and frequency of use.
- [ ] Identify the **single most important action** on each screen.
- [ ] Identify secondary and destructive actions.
- [ ] Define content types: prose, form, table/grid, chart, media, navigation.
- [ ] Define desired density: compact / default / spacious, with reason.
- [ ] Define brand personality in operational terms (e.g. serious + technical + approachable).
- [ ] Define color roles, not just hex values.
- [ ] Define text styles/tokens.
- [ ] Define spacing scale.
- [ ] Define surface/elevation model.
- [ ] Define radius tokens and component-role mapping.
- [ ] Define responsive transformations, not only breakpoints.
- [ ] Define empty/loading/error/permission/offline states as applicable.
- [ ] Define keyboard/focus behavior.
- [ ] Define reduced-motion behavior.
- [ ] Decide which elements may use gradients/glass/shadows/motion and **why**.
- [ ] If using a trendy treatment, document its semantic/brand justification.
- [ ] For landing pages, define the decision journey before choosing section order.
- [ ] For dashboards, define the decisions/actions each module supports.
- [ ] For data tables, define whether the primary task is scanning, comparing, editing, or acting.

---

# 16. Post-generation visual audit

Run on rendered screenshots, not code alone.

## Hierarchy
- [ ] Squint/blur test reveals 1 primary region, then clear secondary grouping.
- [ ] No unrelated elements compete with the main task.
- [ ] Primary action is visually distinct.
- [ ] Destructive action cannot be mistaken for the recommended action.
- [ ] Color roles are consistent.
- [ ] Secondary text remains legible.

## Geometry
- [ ] Major content aligns to a coherent grid.
- [ ] Repeated internal padding uses tokens.
- [ ] Related items are closer than unrelated items.
- [ ] Cards/containers represent real grouping.
- [ ] No unnecessary nested common regions.
- [ ] Prose measure is controlled.
- [ ] Data-heavy content receives enough width.

## Effects
- [ ] Gradients have a defined role.
- [ ] Glass has a layering role.
- [ ] Shadows correspond to elevation or interaction.
- [ ] Glow is rare and not a state/focus substitute.
- [ ] Radius is coherent and role-driven.
- [ ] Pill shapes are not used for every component.
- [ ] Animation communicates change/causality/feedback or is removed.

## Consistency
- [ ] No arbitrary near-duplicate font sizes.
- [ ] No arbitrary near-duplicate spacing values.
- [ ] No arbitrary near-duplicate radii.
- [ ] Component states are consistent across screens.
- [ ] Same action uses same label and interaction model.

---

# 17. UX audit

- [ ] Core task can be discovered without onboarding.
- [ ] Core actions are not hover-only.
- [ ] Important navigation is visible or has a high-scent trigger.
- [ ] Icons have labels when meaning is not highly conventional.
- [ ] Tooltips contain supplemental, not essential, information.
- [ ] Modals are used only when focus/blocking is justified.
- [ ] Repeatable complex work is not trapped in modals.
- [ ] No nested modals.
- [ ] Low-impact reversible actions use Undo instead of confirmation where appropriate.
- [ ] High-impact irreversible actions have specific confirmations.
- [ ] Confirmation buttons use action verbs, not generic OK/Yes.
- [ ] Errors explain what happened and what to do next.
- [ ] User input is preserved when recoverable.
- [ ] The UI supports cancellation/escape/recovery.
- [ ] Empty states offer a meaningful next action.
- [ ] Loading states preserve layout and context where possible.
- [ ] Permissions and unavailable actions explain why.

---

# 18. Responsive audit

Test at **320, 375, 768, 1024, 1280, and a wide desktop**. Also test zoom/text enlargement.

- [ ] No page-level horizontal scroll at 320 CSS px except unavoidable exempt content.
- [ ] Wide tables/grids scroll inside their own container.
- [ ] Table surrounding controls (title/search/pagination) still reflow.
- [ ] Sidebar becomes an appropriate narrow-screen navigation model.
- [ ] Hidden content remains accessible elsewhere unless truly redundant.
- [ ] Touch targets remain adequate.
- [ ] Hover-only features have touch alternatives.
- [ ] Multi-column layout stacks/reorders according to priority.
- [ ] Ordering remains logical for keyboard/screen-reader flow.
- [ ] Forms do not rely on desktop horizontal grouping when labels/inputs no longer fit.
- [ ] Modals fit small viewports without horizontal scroll.
- [ ] Long titles/labels do not clip or overlap.
- [ ] User-controlled larger text does not break layout.
- [ ] Sticky UI does not consume an unreasonable share of mobile viewport.
- [ ] Charts simplify responsibly; labels remain legible.
- [ ] No breakpoint hides a unique primary action.
- [ ] Safe areas/platform insets are respected where applicable.

**Hard rule:** “mobile screenshot looks okay” is insufficient. Verify task completion and content parity.

---

# 19. Accessibility audit

## Keyboard
- [ ] Every interactive function is keyboard operable.
- [ ] Focus order follows logical task order.
- [ ] Focus never becomes trapped except intentionally inside modal/dialog patterns.
- [ ] Closing a modal returns focus appropriately.
- [ ] Focus indicator is visible on every interactive element.

## Contrast
- [ ] Normal text meets 4.5:1 where WCAG applies.
- [ ] Large qualifying text meets 3:1.
- [ ] Meaningful non-text UI/state graphics meet 3:1 where required.
- [ ] Gradient/image backgrounds are tested at worst-case positions.
- [ ] Light and dark themes are tested separately.

## Meaning
- [ ] Color is never the only status/meaning channel.
- [ ] Icon-only buttons have accessible names.
- [ ] Form controls have programmatic labels.
- [ ] Error messages identify the field/problem programmatically where applicable.

## Targets
- [ ] Pointer targets meet WCAG 2.5.8 size/spacing rules.
- [ ] Touch-first primary controls aim for larger platform-appropriate hit regions.

## Motion
- [ ] `prefers-reduced-motion` is honored.
- [ ] Important information is not communicated only through animation.
- [ ] Persistent auto-motion can be paused/stopped/hidden when required.
- [ ] Repeated interactions do not force users to wait for motion.

## Reflow/text
- [ ] Non-exempt content reflows at 320 CSS px.
- [ ] Increased text spacing does not clip/overlap content.
- [ ] Text zoom does not cause loss of functionality.

---

# 20. “Does this look AI-generated?” audit

Do not ask only “is it pretty?” Ask:

- [ ] Is there an identifiable reason for the palette?
- [ ] Is there an identifiable reason for the typography?
- [ ] Is there an identifiable reason for the radius/elevation language?
- [ ] Is there at least one layout decision tied to this product’s actual content?
- [ ] Are real nouns, data, and workflows present instead of placeholder abstractions?
- [ ] Does the layout change when content importance changes?
- [ ] Are components selected by task, not by template availability?
- [ ] Are cards used only where common-region/object grouping is meaningful?
- [ ] Are gradients/glass/glows absent unless they earn their place?
- [ ] Are non-happy-path states designed?
- [ ] Does mobile feel redesigned for constraints rather than scaled down?
- [ ] Is there a stable design-token system?
- [ ] Would a screenshot still feel like this product without the logo?
- [ ] Are visual choices consistent enough to seem deliberate, but varied enough to reflect meaning?
- [ ] Is any “modern SaaS” cliché present only because the prompt was vague?

If the answer pattern suggests a template, **change the structure before changing the colors**.

---

# 21. Automatic correction rules

These are intended for direct use by a coding agent.

## 21.1 Hard automatic fixes

```yaml
rules:
  - id: a11y-focus-visible
    when: "interactive element has no visible keyboard focus"
    severity: CRITICAL
    action: "add consistent accessible focus indicator; never ship outline:none without replacement"

  - id: a11y-text-contrast
    when: "required text fails WCAG contrast"
    severity: HIGH
    action: "adjust foreground/background semantic tokens until requirement passes"

  - id: a11y-color-only
    when: "status/action meaning is conveyed only by color"
    severity: HIGH
    action: "add text/icon/shape/pattern or another non-color cue"

  - id: a11y-target-size
    when: "pointer target fails WCAG 2.5.8 and no exception applies"
    severity: HIGH
    action: "increase hit area or spacing"

  - id: responsive-page-overflow
    when: "page scrollWidth > viewport width at 320px due to non-exempt content"
    severity: CRITICAL
    action: "identify offending component; make it reflow or contain required 2D scrolling locally"

  - id: hover-only-core-function
    when: "task-essential control is available only on hover"
    severity: CRITICAL
    action: "make control persistently discoverable or provide keyboard/touch equivalent"

  - id: reduced-motion
    when: "nonessential motion remains under prefers-reduced-motion"
    severity: HIGH
    action: "disable or replace movement with reduced/instant feedback"
```

## 21.2 Structural correction rules

```yaml
  - id: nested-card-soup
    when: "visual containment depth > 2 and inner wrappers add no semantic/interaction scope"
    severity: MEDIUM
    action: "remove the weakest wrapper; replace with spacing/alignment/divider"

  - id: duplicate-primary-actions
    when: "multiple unequal actions in one group use primary prominence"
    severity: HIGH
    action: "choose one primary action; downgrade others based on task priority"

  - id: modal-overreach
    when: "modal contains complex/repeatable/long workflow"
    severity: HIGH
    action: "move workflow inline, to side panel, or dedicated page"

  - id: dashboard-equal-cards
    when: "unequal dashboard information uses identical visual weight"
    severity: MEDIUM
    action: "rank by urgency/actionability; promote exceptions and decisions, demote supporting detail"

  - id: prose-too-wide
    when: "multi-paragraph prose exceeds ~80ch"
    severity: MEDIUM
    action: "constrain reading column, typically toward 50–75ch"

  - id: mobile-sidebar
    when: "persistent sidebar makes narrow content unusable"
    severity: HIGH
    action: "switch to adaptive drawer/rail/tab/bottom-nav pattern while preserving discoverability"
```

## 21.3 Visual smell correction rules

```yaml
  - id: unmotivated-ai-gradient
    when: "purple/blue/cyan gradient is primary visual identity but no brand/design rationale exists"
    severity: STYLE_PREFERENCE
    action: "replace with brand/domain-driven palette OR document and keep a deliberate rationale"

  - id: glass-overuse
    when: "glass/backdrop blur appears on ordinary content surfaces repeatedly"
    severity: MEDIUM
    action: "return content surfaces to stable opaque/semantic layers; reserve glass for functional layering"

  - id: border-shadow-redundancy
    when: "same container uses border + shadow + strong background contrast without need"
    severity: MEDIUM
    action: "retain the lightest sufficient grouping/elevation signal"

  - id: pill-everything
    when: "3+ semantically distinct component classes all use full-capsule shape"
    severity: STYLE_PREFERENCE
    action: "restore shape differentiation between status, selection, input, navigation, and action"

  - id: type-token-drift
    when: "near-duplicate type sizes/weights exist without semantic tokens"
    severity: MEDIUM
    action: "map text to a reduced semantic type scale"

  - id: spacing-token-drift
    when: "many arbitrary spacing values appear in equivalent contexts"
    severity: MEDIUM
    action: "normalize to spacing tokens while preserving hierarchy"

  - id: decorative-motion
    when: "animation has no feedback/orientation/state/story function"
    severity: MEDIUM
    action: "remove it or reduce to subtle non-blocking transition"

  - id: ai-template-cluster
    when: "AI smell score >= 8"
    severity: MEDIUM
    action: "redesign macrostructure first; then revise typography/color/components"
```

## 21.4 Confirmation logic

```text
IF action is reversible AND low/medium impact:
    perform action
    show status feedback
    offer Undo when valuable
    DO NOT show blocking confirmation by default

IF action is irreversible OR high-cost OR destructive OR legally/financially consequential:
    show explicit confirmation
    name the affected object/count
    state the consequence
    use action-specific button text
    visually distinguish destructive action
```

## 21.5 Surface-selection logic

```text
Need grouping?
    first try alignment + proximity
    then whitespace
    then subtle divider/border
    then tonal surface/card
    use elevation only when depth/overlay/movement/priority needs it
    use glass only when background context/layering is part of the meaning
```

## 21.6 Responsive transformation logic

```text
For each desktop region:
    classify priority = primary / secondary / tertiary
    classify behavior = read / compare / edit / navigate / monitor / act

At narrower widths:
    preserve primary content/actions
    stack independent regions
    collapse secondary navigation with a clear trigger
    move tertiary controls into explicit menus/drawers
    keep comparison structures tabular when comparison is essential
    contain necessary horizontal scroll locally
    never silently remove unique functionality
```

---

# 22. Release gate for coding agents

An agent **must not** mark frontend work as complete if any of the following remain:

### Blockers
- CRITICAL accessibility failure.
- Core function unavailable by keyboard/touch.
- Non-exempt page-level horizontal overflow at 320px.
- Task-essential text/control not perceivable.
- Destructive action easily confused with routine primary action.
- Major mobile layout makes the primary task impossible.

### Must-fix before “polished”
- Competing primary CTAs.
- Unnecessary modal-heavy workflow.
- Core features hidden without discoverability.
- Dashboard hierarchy does not reflect urgency/actionability.
- Secondary text is technically/visually too weak.
- AI-smell score ≥8 with no documented intentional design direction.
- Multiple unsupported one-off spacing/type/radius/color values.
- Dark mode is an untested mechanical inversion.
- Nonessential repeated motion ignores reduced-motion preference.

### May remain with documented rationale
- Gradient.
- Glassmorphism.
- Large radius.
- Pills.
- Large display type.
- Centered short copy.
- Strong shadows.
- Glow.
- Unusual asymmetry.

The rationale must state **what user/product/brand purpose the choice serves** and confirm it does not violate hierarchy, responsive behavior, or accessibility.

---

# 23. Source index

**[S1] W3C — Understanding SC 1.4.3 Contrast (Minimum)**  
https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html

**[S2] W3C — Understanding SC 2.4.13 Focus Appearance**  
https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance

**[S3] W3C — Understanding SC 1.4.1 Use of Color**  
https://www.w3.org/WAI/WCAG22/Understanding/use-of-color.html

**[S4] W3C — Understanding SC 1.4.11 Non-text Contrast**  
https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html

**[S5] W3C — Keyboard Accessible**  
https://www.w3.org/WAI/WCAG22/Understanding/keyboard-accessible.html

**[S6] W3C — Understanding SC 1.4.13 Content on Hover or Focus**  
https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html

**[S7] Nielsen Norman Group — Modal & Nonmodal Dialogs: When (& When Not) to Use Them**  
https://www.nngroup.com/articles/modal-nonmodal-dialog/

**[S8] W3C — Understanding SC 1.4.10 Reflow**  
https://www.w3.org/WAI/WCAG22/Understanding/reflow.html

**[S9] Nielsen Norman Group — 5 Principles of Visual Design in UX**  
https://www.nngroup.com/articles/principles-visual-design/

**[S10] Nielsen Norman Group — Visual Hierarchy in UX: Definition**  
https://www.nngroup.com/articles/visual-hierarchy-ux-definition/

**[S11] Nielsen Norman Group — Visual Design: Glossary**  
https://www.nngroup.com/articles/visual-design-cheat-sheet/

**[S12] Baymard — Readability: The Optimal Line Length**  
https://baymard.com/research-articles/line-length-readability

**[S13] Nielsen Norman Group — Signal–to–Noise Ratio**  
https://www.nngroup.com/articles/signal-noise-ratio/

**[S14] Baymard — Button Design: Best Practices for Optimal UI Buttons**  
https://baymard.com/blog/button-design

**[S15] Carbon Design System — Data Table Usage**  
https://v10.carbondesignsystem.com/components/data-table/usage/

**[S16] Apple Human Interface Guidelines — Layout**  
https://developer.apple.com/design/human-interface-guidelines/layout

**[S17] Apple Human Interface Guidelines — Buttons**  
https://developer.apple.com/design/human-interface-guidelines/buttons

**[S18] Apple Human Interface Guidelines — Materials / Liquid Glass**  
https://developer.apple.com/design/human-interface-guidelines/materials

**[S19] Atlassian Design System — Elevation**  
https://atlassian.design/foundations/elevation/

**[S20] Carbon Design System — 2x Grid**  
https://www.carbondesignsystem.com/building-blocks/foundations/2x-grid/guidelines

**[S21] Apple Human Interface Guidelines — Design Principles**  
https://developer.apple.com/design/human-interface-guidelines/design-principles

**[S22] Apple Human Interface Guidelines — Color**  
https://developer.apple.com/design/human-interface-guidelines/color

**[S23] Nielsen Norman Group — Low-Contrast Text Is Not the Answer**  
https://www.nngroup.com/articles/low-contrast/

**[S24] Nielsen Norman Group — Dashboards: Making Charts and Graphs Easier to Understand**  
https://www.nngroup.com/articles/dashboards-preattentive/

**[S25] Dyson & Haselgrove — The influence of reading speed and line length on the effectiveness of reading from screen**  
https://www.sciencedirect.com/science/article/pii/S1071581901904586

**[S26] Shin et al. (2026) — Interrogating Design Homogenization in Web Vibe Coding**  
https://arxiv.org/abs/2603.13036

**[S27] Chaparro et al. — Reading Online Text: A Comparison of Four White Space Layouts**  
https://portfolio.erau.edu/en/publications/reading-online-text-a-comparison-of-four-white-space-layouts/

**[S28] CHI 2020 — Keep it Simple: How Visual Complexity and Preferences Impact Search Efficiency on Websites**  
https://doi.org/10.1145/3313831.3376849

**[S29] SmoothUI — AI Design Slop: Why AI-Generated UI Looks Generic — and the Fix**  
https://smoothui.dev/blog/ai-design-slop

**[S30] Foundey — AI Slop in UX: Why AI-Generated Interfaces Miss the Mark**  
https://foundey.com/blog/ai-slop-in-ux-design

**[S31] The Crit — Why Your Vibe-Coded App Looks Like Every Other AI App**  
https://thecrit.co/resources/vibe-coding-design-guide

**[S32] Material Design — Understanding Typography**  
https://m2.material.io/design/typography/understanding-typography.html

**[S33] Nielsen Norman Group — Button States: Communicate Interaction**  
https://www.nngroup.com/articles/button-states-communicate-interaction/

**[S34] Nielsen Norman Group — Icon Usability**  
https://www.nngroup.com/articles/icon-usability/

**[S35] Carbon Design System — Modal Usage**  
https://www.carbondesignsystem.com/building-blocks/core/components/modal/guidelines

**[S36] Nielsen Norman Group — Beyond the Hamburger: Navigation Discoverability on Desktop**  
https://www.nngroup.com/articles/find-navigation-desktop-not-hamburger/

**[S37] Nielsen Norman Group — Hamburger Menus and Hidden Navigation Hurt UX Metrics**  
https://www.nngroup.com/articles/hamburger-menus/

**[S38] Nielsen Norman Group — Progressive Disclosure**  
https://www.nngroup.com/articles/progressive-disclosure/

**[S39] Nielsen Norman Group — Mobile-App Onboarding: Components and Techniques**  
https://www.nngroup.com/articles/mobile-app-onboarding/

**[S40] Nielsen Norman Group — Preventing User Errors: Avoiding Conscious Mistakes**  
https://www.nngroup.com/articles/user-mistakes/

**[S41] Nielsen Norman Group — Confirmation Dialogs Can Prevent User Errors — If Not Overused**  
https://www.nngroup.com/articles/confirmation-dialog/

**[S42] Nielsen Norman Group — UI Copy: Command Names and Keyboard Shortcuts**  
https://www.nngroup.com/articles/ui-copy/

**[S43] Nielsen Norman Group — Data Tables: Four Major User Tasks**  
https://www.nngroup.com/articles/data-tables/

**[S44] W3C — Understanding SC 2.4.7 Focus Visible**  
https://www.w3.org/WAI/WCAG22/Understanding/focus-visible

**[S45] W3C — Understanding SC 2.5.8 Target Size (Minimum)**  
https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum

**[S46] W3C — Understanding SC 2.3.3 Animation from Interactions**  
https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions

**[S47] Apple Human Interface Guidelines — Motion**  
https://developer.apple.com/design/human-interface-guidelines/motion

**[S48] Nielsen Norman Group — Choosing Chart Types: Consider Context**  
https://www.nngroup.com/articles/choosing-chart-types/

**[S49] Apple Human Interface Guidelines — Dark Mode**  
https://developer.apple.com/design/human-interface-guidelines/dark-mode

**[S50] Nielsen Norman Group — Dark Mode: How Users Think About It and Issues to Avoid**  
https://www.nngroup.com/articles/dark-mode-users-issues/

**[S51] Nielsen Norman Group — Scroll-Triggered Text Animations Delay Users**  
https://www.nngroup.com/articles/scroll-animations/

**[S52] W3C — Understanding SC 2.2.2 Pause, Stop, Hide**  
https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html

**[S53] W3C — Understanding SC 1.4.12 Text Spacing**  
https://www.w3.org/WAI/WCAG22/Understanding/text-spacing

---

# 24. Final operating principle

> **Do not optimize for “looks modern.” Optimize for: clear task priority, understandable structure, intentional visual language, resilient responsive behavior, recoverable interactions, and accessible operation.**

A coding agent should consider its frontend complete only when:
1. the primary user task is obvious,
2. the interface has a defensible hierarchy,
3. decorative choices have a reason,
4. responsive transformations preserve meaning and functionality,
5. accessibility rules pass,
6. common error/empty/loading states are handled, and
7. the result no longer looks like an unconstrained statistical average of SaaS templates.
