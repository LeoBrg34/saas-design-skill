# Final SaaS UI Audit

A coding agent must run this before declaring the interface complete.

## Hierarchy
- [ ] Primary task/action is obvious.
- [ ] One action is visually dominant per coherent action group when appropriate.
- [ ] Unequal states/information do not receive equal weight.
- [ ] Routine content is not overwhelmed by giant headings or decorative chrome.

## Color
- [ ] Components consume semantic roles/tokens, not arbitrary raw colors.
- [ ] Normal text >=4.5:1; qualifying large text >=3:1 where WCAG applies.
- [ ] Required non-text UI/state graphics meet >=3:1 where applicable.
- [ ] Essential meaning is not color-only.
- [ ] Status colors are not repurposed ambiguously for decoration.
- [ ] Dark mode, if present, is mapped/tested independently rather than mechanically inverted.

## Typography
- [ ] Every text style has a semantic role.
- [ ] Type sizes/weights are a compact system rather than one-offs.
- [ ] Important small text is not thin/light.
- [ ] Metrics that need comparison use tabular numerals where available.
- [ ] Monospace appears only where content warrants it.
- [ ] Reading blocks have reasonable measure.
- [ ] 200% text resize/zoom does not clip or remove function.

## Density & consistency
- [ ] Density matches expertise, frequency, and decision volume.
- [ ] Spacing/radius/border/elevation/icon treatment follows coherent tokens.
- [ ] Cards have grouping meaning; nested wrappers are not decorative soup.
- [ ] Decorative effects have a named purpose.

## Responsive
- [ ] No accidental page-level horizontal scroll around 320 CSS px.
- [ ] Each breakpoint corresponds to a real mode change/failure threshold.
- [ ] Intermediate widths immediately around breakpoints were checked.
- [ ] Local components respond to allocated space where appropriate.
- [ ] Mobile preserves the job and critical capability, not desktop composition.
- [ ] Tables transform according to task.
- [ ] Filters expose active state even when collapsed.
- [ ] Long labels/user content/localization cases were checked.
- [ ] Hover-only behavior has touch/keyboard equivalents.

## Interaction
- [ ] Keyboard path reaches all core controls.
- [ ] Visible focus exists and is not obscured by sticky UI.
- [ ] Icon-only controls have accessible names and understandable affordance.
- [ ] Low-impact reversible actions avoid unnecessary confirmation friction.
- [ ] High-impact/irreversible actions name object, scope, and consequence.
- [ ] Loading, empty, error, permission, disabled, success, and destructive states are handled where relevant.

## Accessibility & motion
- [ ] Target-size/spacing requirements are satisfied; touch-first primary controls have comfortable hit areas.
- [ ] `prefers-reduced-motion` is respected.
- [ ] Orientation/reflow/text-spacing requirements are respected where applicable.
- [ ] Charts/data have accessible interpretation paths when needed.

## Industry & brand fit
- [ ] Workflow matches domain expectations without relying on visual stereotypes.
- [ ] Brand drivers are visible in appropriate channels.
- [ ] High-risk flows are more restrained than marketing expression.
- [ ] Trust/secure/enterprise claims have product evidence, not only visual symbolism.

## AI-template smell
- [ ] Palette has a product/brand rationale.
- [ ] Typography has a role/density rationale.
- [ ] Radius/elevation language has a rationale.
- [ ] At least one major layout decision depends on real product content/workflow.
- [ ] Cards/effects are selected by meaning, not template availability.
- [ ] Non-happy-path states exist.
- [ ] A stable token system exists.
- [ ] The UI would still feel product-specific without the logo.

> **Would this interface look obviously AI-generated or like a generic SaaS template?**

If yes, identify the cluster causing it and fix **structure/content specificity/hierarchy/type/component choice first**. Do not add more effects as a genericity fix.

## Release blockers

Do not ship/declare complete with:
- critical accessibility failure;
- core function unavailable by keyboard/touch;
- ordinary non-exempt page overflow at compact width;
- task-essential content/control not perceivable;
- destructive action easily confused with routine action;
- primary compact/mobile task impossible;
- unresolved AI-template cluster score >=8 without an intentional, documented design direction.
