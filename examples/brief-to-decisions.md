# Example — Brief to Design Decisions

This is an example of how an agent should *reason in outputs*, not a mandatory visual style.

## Brief

Build a B2B AI security copilot for cloud-security teams. Expert users review findings, ask questions about an incident, approve suggested remediation, and inspect evidence. Brand traits: `technical`, `secure`, `premium`, `approachable`. Responsive web; desktop is primary, mobile is mainly review/approval.

## Input classification

```yaml
product_type: AI security copilot
industry: [cybersecurity, AI SaaS]
primary_jobs:
  - triage security finding
  - inspect evidence
  - ask for explanation
  - review proposed remediation
  - approve/reject action
users.expertise: expert
users.frequency: intensive
information_density: high
risk_level: high
consequence_of_error: high
platform: responsive_web
brand_personality: [technical, secure, premium, approachable]
```

## Conflict resolution

- Drivers: `technical`, `secure`.
- Modifier: `premium`.
- Modifier for support/onboarding: `approachable`.
- Guardrail: high consequence of error.

Security owns state clarity, auditability, approval, and motion ceiling. Technical owns density/data/code. Premium appears as precise typography, disciplined spacing, restrained surfaces. Approachable appears in explanations, onboarding, errors, and help — not in remediation consequences.

## Explicit design decisions

| Dimension | Decision |
|---|---|
| Core metaphor | finding/evidence workspace with assistant attached to the incident, not chat as the entire product |
| Density | high but calm; compact rows/tables with strong selected/critical-state hierarchy |
| Color | neutral-led product surface; one brand/action family; severity/status semantic ramps; no neon “cyber” default |
| Typography | 13–14px productive body/cells, 12–13px support, tabular numerals for metrics; mono only for IDs/log/code |
| Navigation | persistent desktop product navigation + incident context; mobile prioritizes finding review/approval/history |
| Layout | desktop split workspace: evidence/finding + contextual AI/action panel when needed; collapse to one primary region on compact widths |
| Geometry | restrained radius and elevation; grouping mostly by alignment/tonal surfaces |
| Motion | only real state/progress/orientation; reduced-motion safe; no ambient pulsing/glow |
| Trust | source links, evidence provenance, action preview, permission/scope, approval gate, audit history, undo/recovery where possible |
| Responsive | table comparison remains tabular with contained scroll where needed; mobile hides no unique approval consequence/state |

## Anti-patterns to reject

- generic violet/cyan AI gradient as primary identity;
- fake “AI is thinking...” animation disconnected from real state;
- autonomous remediation with no scope/review;
- glass cards over dense evidence;
- “premium” implemented as low-contrast thin type;
- mobile as a squeezed SOC dashboard;
- severity conveyed only by color;
- every finding represented as the same equal-weight card.

## Final check

The interface should read first as a credible security operations tool, second as an AI-assisted workflow, and only then as a branded visual experience. That ordering follows the skill priority model.
