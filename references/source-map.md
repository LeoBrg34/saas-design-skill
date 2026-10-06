# Research Traceability Map

This repository separates **evidence archives** (`research/`) from **production instructions** (`SKILL.md`, `references/`, `checklists/`). Use this map when a rule is disputed, high-risk, or needs deeper context.

| Production rule group | Primary research anchors | Evidence character |
|---|---|---|
| semantic color tokens | `color-intelligence.md` §§ 3–4 | mature design-system convention |
| text/non-text contrast, color-independent meaning, focus | `color-intelligence.md` § 2; `design-antipatterns.md` § 7 | normative accessibility |
| neutral-led product color / one primary action | `color-intelligence.md` § 3 | strong industry convention |
| color budget / saturation | `color-intelligence.md` § 5 | contextual heuristic with research/convention support |
| dark-mode remapping | `color-intelligence.md` § 6 | convergent design-system convention |
| semantic type roles / compact scale | `typography.md` §§ 1–3 | research + design-system convention |
| 12px supporting, 13–16px productive ranges | `typography.md` §§ 1, 3, 5, 12 | contextual product convention |
| font brand expression in headings first | `typography.md` § 4; `brand-personality.md` §§ 2, 7 | context-sensitive heuristic |
| 200% text resize / viewport-only type warning | `typography.md` §§ 6–7 | normative accessibility |
| brand axes, driver/modifier/guardrail | `brand-personality.md` §§ 2, 8, 13 | research-informed decision heuristic |
| structure from task, not personality | `brand-personality.md` §§ 3, 13 | decision heuristic supported by congruence/prototypicality evidence |
| industry as prior, workflow contract first | `design-by-industry.md` opening, Cross-industry rules, Decision Engine | convergent functional evidence + heuristic |
| risk overrides aesthetics | `design-by-industry.md` Cross-industry rules | high-confidence functional guidance |
| breakpoint from failure threshold | `responsive-saas.md` §§ 0–3, 31–35 | strong modern CSS/design-system guidance |
| container vs media queries | `responsive-saas.md` § 2, § 25 | platform/CSS guidance |
| table transformations by task | `responsive-saas.md` § 9, §§ 29–35 | strong task-aware convention |
| compact/mobile preserves task, not composition | `responsive-saas.md` §§ 4, 26, 32–35 | strong responsive synthesis |
| anti-pattern severity / release gate | `design-antipatterns.md` §§ 0, 12–24 | accessibility + usability + convergent heuristics |
| AI-template cluster detection | `design-antipatterns.md` §§ 12, 20–22 | emerging evidence / smell heuristic, not factual classifier |

## Contradictions intentionally resolved

1. **“Minimal” vs dense enterprise UI:** minimalism means lower visual noise and fewer competing treatments; it does not mean deleting needed information. Task/density wins.
2. **14px vs 16px body defaults:** dense recurring product work can use ~13–14px; standard/reading-forward UI trends larger. Role, density, font metrics, and accessibility determine the final value.
3. **44–48px touch targets vs WCAG target-size rules:** 44–48px is a comfort/platform aim for touch-first controls; WCAG compliance uses its own minimum/spacing criteria and exceptions. Do not conflate them.
4. **Horizontal scrolling:** avoid page-level overflow, but component-level horizontal scrolling is appropriate when a genuine 2D comparison/table/canvas relationship must be preserved.
5. **Dark backgrounds / “black = premium”:** dark mode and black are stylistic/contextual choices; neither is a trust, technicality, or luxury requirement.
6. **Rounded/angular personality:** shape associations are secondary and context-limited. Functional grouping/state semantics outrank personality mapping.
7. **Color psychology:** associations may guide a contextual prior but never replace semantic roles, contrast, culture, existing brand, or domain meaning.
8. **Industry conventions:** functional conventions are strong; graphic trends are weak. Never convert a repeated visual trend into a hard industry requirement.

## Confidence policy

When instructions conflict with a product-specific design system or stronger evidence, preserve the stronger source and document the exception. Low-confidence trend rules may trigger review but should not automatically block shipping.
