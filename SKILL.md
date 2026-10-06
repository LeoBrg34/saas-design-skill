---
name: saas-design
description: Production design intelligence for coding agents building or auditing SaaS interfaces. Converts product, industry, brand, density, responsive, color, typography, and anti-pattern research into executable UI decisions.
---

# SaaS Design — Production Skill

Use this skill to design, implement, refactor, or audit SaaS product UI and SaaS marketing surfaces. Optimize for task clarity, product specificity, resilient responsiveness, accessible operation, and coherent visual direction — not for generic “modern SaaS” aesthetics.

## WHEN TO USE THIS SKILL

Use when the task includes any of:
- creating or redesigning a SaaS screen, dashboard, workflow, settings area, onboarding flow, data view, or landing page;
- choosing color, typography, density, navigation, geometry, motion, or responsive behavior;
- translating brand traits or industry context into UI decisions;
- reviewing frontend work for visual/UX quality or “AI-generated template” smell;
- adapting desktop SaaS to tablet/mobile.

Do not use it as a substitute for product requirements, domain safety rules, user research, or an existing design system. If a product already has authoritative tokens/components, preserve them unless the task explicitly requires changing the system.

## PROGRESSIVE DISCLOSURE

Read only what the current decision needs:

| Need | Read |
|---|---|
| Palette, semantic color, light/dark, data-viz | `references/color.md` |
| Type scale, roles, density, font loading | `references/typography.md` |
| Brand traits, tone conflicts, expressive controls | `references/brand.md` |
| Breakpoints, mobile transformation, tables/charts/forms | `references/responsive.md` |
| Domain conventions and risk/density priors | `references/industries.md` |
| Audit, failure modes, AI-template smell, auto-fixes | `references/antipatterns.md` |
| Why a rule exists / research traceability | `references/source-map.md` |
| Before designing | `checklists/pre-design.md` |
| Before declaring complete | `checklists/final-audit.md` |

The six files under `research/` are evidence archives. Do not load them all unless a disputed or high-impact rule requires deeper traceability.

## INPUT ANALYSIS

Before styling, derive or infer this design context:

```yaml
product_type:            # dashboard, CRM, AI workspace, analytics, settings, landing, etc.
industry:                # may be hybrid
primary_jobs: []         # concrete user tasks, ordered
users:
  expertise: novice | mixed | expert
  frequency: occasional | recurring | intensive
brand_personality: []    # adjectives or existing brand traits
information_density: low | medium | high
platform: web | desktop | mobile | responsive_web
input_modes: []          # keyboard/mouse/touch/stylus as relevant
risk_level: low | medium | high
consequence_of_error: low | medium | high
accessibility_constraints: []
localization_constraints: []
existing_design_system:  # tokens/components if present
```

If inputs are missing, infer conservatively from the product and content. Do not invent a strong brand direction from a vague brief. Treat industry as a prior, not a visual preset.

## CONFLICT RESOLUTION

When rules conflict, use this priority:

```text
1. Legal, accessibility, safety, privacy, and irreversible-harm constraints
2. Task completion, data integrity, state clarity, and consequence-of-error controls
3. Explicit product requirements and business logic
4. Platform/input/localization/performance constraints
5. Information hierarchy, density, and audience expertise
6. Functional industry conventions and learned user expectations
7. Brand personality and product differentiation
8. Aesthetic trends and decorative novelty
```

Never let a lower layer break a higher one. If two brand traits conflict, do not average them across every property: assign them different jobs (driver / modifier / guardrail).

## DESIGN DECISION PIPELINE

### 1. Understand product
Identify the primary job, core objects, user expertise, frequency, risk, data volume, and required states. Put the main task before decoration. If the primary job is action, do not default to a dashboard of charts.

### 2. Determine industry expectations
Use industry only to infer workflow expectations, density, trust/audit needs, and familiar interaction models. Do **not** infer palettes or themes from stereotypes such as “fintech = blue”, “security = dark”, or “AI = purple gradient”. For hybrid products, combine workflow priors, e.g. `AI security copilot = security workflow + AI transparency`, not “generic AI chat theme”.

### 3. Determine brand personality
Normalize adjectives into these control axes: warmth, competence, status, energy, novelty, technicality, risk sensitivity, restraint. Choose at most **2 drivers**, then modifiers and guardrails. Structure comes from task; personality changes expression.

### 4. Select color strategy
- Define semantic roles before hex values.
- Use `primitive -> semantic -> component` tokens when component tokens are needed.
- Product work surfaces should usually be neutral-led; reserve chroma for action, status, categorization, data, and brand moments.
- Maintain one visually dominant primary action per coherent action region when a primary exists.
- Never encode essential meaning by color alone.
- Minimum targets: normal text `4.5:1`, qualifying large text `3:1`, required non-text UI/graphics `3:1`.
- Build dark theme by remapping semantic roles; never mechanically invert light theme.
- Treat saturation as a scarce resource. More important does not automatically mean more saturated.

### 5. Select typography strategy
Assign semantic roles first. Start with the smallest sufficient scale (`caption`, `label`, `body`, `title`, `heading`, `page-title`, plus `metric/code` only when needed).
- Dense product UI: primary text normally ~13–14px; standard product UI ~14–16px; reading-forward surfaces 16px+.
- Treat 12px as supporting text, not the default primary reading size.
- Use regular body weight; medium/semibold for UI emphasis. Avoid thin/light small text.
- Use tabular numerals for vertically compared/changing metrics.
- Use monospace for code, shell, identifiers, or alignment-sensitive technical content — not as a generic “developer” aesthetic.
- Long-form text: target roughly 50–75 characters per line.
- Use relative units; do not use viewport-only meaningful font sizing; survive 200% text resize.
- Brand expression belongs first in display/headline roles, not by sacrificing control/table readability.

### 6. Determine density and hierarchy
Density follows task frequency, expertise, decision volume, and error cost — not fashion.
- Prefer fewer container styles, fewer accents, and stronger alignment over deleting useful information.
- When a dense screen feels crowded, tighten excessive padding/gaps and remove low-value metadata before shrinking primary text.
- Unequal information must not receive equal visual weight. Rank by urgency, actionability, frequency, and decision value.
- Group by proximity/alignment first, then spacing/divider, then tonal surface/card, then elevation only if depth has meaning.

### 7. Determine responsive behavior
Responsive design is task preservation, not “desktop + tablet + mobile breakpoints”.
1. Mark non-hideable information/actions.
2. Determine minimum usable widths from actual content.
3. Prefer intrinsic CSS for continuous resizing.
4. Use container queries for local component modes; media queries for application-shell modes.
5. When space fails: `compress -> wrap -> reorder -> group -> move -> summarize -> disclose -> hide`.
6. Create breakpoints only for a real mode change/failure threshold.
7. Never make core behavior hover-only. Touch rules depend on input capability, not width alone.
8. Avoid page-level horizontal overflow; contain essential 2D scrolling inside the relevant component.
9. Preserve state, focus order, sorting/filtering/selection, and business logic across variants.

For tables, classify the task before transforming:
- comparison -> preserve 2D relationship; contained horizontal scroll is acceptable;
- entity browse -> list/card transformation can work;
- bulk operations -> preserve selection and bulk actions;
- spreadsheet editing -> dedicated/full-screen grid may be necessary.

### 8. Generate UI
Use existing design-system primitives when available. Generate realistic domain content and non-happy-path states early enough that layout decisions reflect real information rather than placeholder rectangles. Keep marketing expression more permissive than product UI; keep critical workflows more restrained than both.

### 9. Run anti-pattern audit
Run four passes: **structure -> interaction -> visual -> accessibility**.

Hard failures to correct before completion:
- missing visible keyboard focus;
- essential meaning conveyed only by color;
- task-essential action available only on hover;
- non-exempt page overflow at ~320 CSS px;
- inaccessible text/non-text contrast where applicable;
- primary task impossible on compact layout;
- destructive/high-consequence action ambiguous or easy to trigger accidentally;
- nonessential motion ignoring reduced-motion preference.

Then remove generic-template defaults that have no rationale: card soup, radius inflation, pill-everything, gradients/glass/glow everywhere, competing CTAs, giant routine page titles, decorative charts, generic centered hero formulas, one-off token drift.

### 10. Correct problems
Fix causes, not symptoms.
- Weak hierarchy -> change priority/layout before increasing saturation.
- Generic SaaS look -> change macrostructure/content specificity before adding effects.
- Crowded screen -> remove low-value chrome or reflow before shrinking text.
- Mobile failure -> transform task structure before hiding features.
- Too many containers -> remove the weakest wrapper; use spacing/alignment.
- Reversible low-impact action -> prefer feedback/undo over blocking confirmation.
- Irreversible/high-impact action -> explicit confirmation naming object, scope, and consequence.

## PRODUCT-SPECIFICITY RULE

The interface should reveal what the product does even without its logo. At least one major layout or component decision must be tied to actual product objects, workflows, data relationships, or user priorities. Avoid generating the same “hero + 3 feature cards + gradient dashboard mockup” structure for unrelated products.

## SELF-AUDIT — REQUIRED BEFORE COMPLETION

Check all of the following:

```text
Hierarchy       Is the primary task/action obvious? Are unequal states weighted unequally?
Colors          Are roles semantic, contrast valid, status non-color-only, accent competition controlled?
Typography      Are roles/tokens coherent, readable, density-appropriate, and resize-safe?
Density         Does density match expertise/task frequency rather than aesthetic preference?
Consistency     Do spacing, radius, color, type, icons, and states follow a coherent system?
Responsive      Are transformations task-aware across arbitrary widths, not only mockup widths?
Accessibility   Keyboard, focus, contrast, target size, motion, reflow, text resize, semantics pass?
Industry fit    Does the workflow match domain expectations without visual stereotyping?
Brand fit       Are brand drivers visible without weakening task clarity or risk communication?
Anti-patterns   Are decorative/interaction patterns intentional rather than generator defaults?
```

Ask explicitly:

> **Would this interface look obviously AI-generated or like a generic SaaS template?**

If yes, identify the responsible cluster and correct it. Do **not** respond by adding more gradients, glass, glow, animation, or cards. First revisit structure, product-specific content, hierarchy, typography, and component choice.

## RELEASE GATE

Do not declare the frontend complete while a critical accessibility/task failure remains. Aesthetic choices such as gradients, glass, strong radius, pills, large display type, dark mode, or glow may remain **only with a deliberate rationale and no higher-priority failure**.

When uncertainty remains, prefer the more conventional interaction and the more restrained visual treatment, then document the tradeoff. Novelty is cheapest in expressive layers and most expensive in navigation, state, and high-risk workflows.
