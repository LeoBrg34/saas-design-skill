# Industry Decision Reference

Industry is a **prior**, not a theme preset. Prefer workflow topology, consequence of error, expertise, data density, auditability, collaboration, and device context over visual category clichés.

## Cross-industry hard rules

- Risk overrides aesthetics: higher consequence -> clearer scope/state, more auditability/reversibility, less decorative ambiguity/motion.
- Expert recurring workflows may be compact; density follows scan/decision frequency, not “modern spaciousness”.
- Use dashboards for monitoring/comparison; if the main job is action, foreground the queue/object/action.
- Color is scarce in status/data-heavy products; reserve strong chroma for meaning.
- Mobile parity is not the goal; preserve the mobile job.
- AI-generated/inferred content or autonomous actions require identifiable state, provenance where useful, review/reversibility, and status transparency.

## Industry matrix

| Industry | Primary interaction contract | Density default | Trust / risk emphasis | Avoid visual shortcut |
|---|---|---|---|---|
| AI SaaS | intent -> generation/action -> inspect -> iterate/approve/recover | low/med entry; med/high artifacts | identify generated state, progress, source/provenance, approval/undo | rainbow AI gradient, fake “thinking” theater |
| FinTech | inspect/move/reconcile/approve money | medium-high | exact values, audit context, consequence, reversibility | “blue = trust”, decorative financial charts |
| Cybersecurity | triage -> evidence -> prioritize -> drill down/remediate | high | severity clarity, scope, audit trail, incident state | mandatory dark/neon/cyberpunk shell |
| Developer tools | code/context/search/inspect/operate quickly | medium-high/high | technical fidelity, keyboard efficiency, exact states | mono everywhere, fake terminal visuals |
| Analytics / BI | compare/filter/drill/explain data | high | data provenance, interpretation, accessible alternatives | decorative dashboards/KPI wallpaper |
| CRM / Sales | records -> pipeline -> activity -> next action | medium-high | ownership/status/history, actionability | giant cards that reduce record scan efficiency |
| Productivity | capture -> organize -> retrieve -> focus/complete | low-medium | low friction, predictable state | feature-heavy chrome around simple tasks |
| Project management | work objects across board/list/timeline/workload views | medium-high | state/ownership/dependencies | forcing every workflow into identical cards |
| Enterprise | role-based complex workflows + governance | high | permissions, auditability, consistency, admin visibility | “enterprise = gray and boring” as style rule |
| Healthcare | safe role-separated workflow, documentation, scheduling/care tasks | medium-high | privacy, safety, accessibility, consequence clarity | decorative minimalism that hides context |
| E-commerce SaaS | product/order/customer/fulfillment lifecycle | medium-high | object/state clarity, exception handling | consumer-store aesthetics inside ops tooling |
| Marketing SaaS | create -> target -> launch -> measure | medium | previews, experiment/report state, explainable metrics | vanity-chart-first dashboard |
| Collaboration | streams -> triage -> context -> search/respond | medium-high | unread/mention/state continuity, retrieval | notification/color overload |

These are priors. Hybrid products blend contracts. Example: an AI CRM assistant should sit beside deal context and action state rather than converting the whole CRM into chat.

## Decision engine

```text
A. infer industry prior (about 20–30% of decision)
B. apply hard overrides:
   accessibility/legal, consequence of error, expertise/frequency,
   density/comparison, primary device, real-time state, permissions/auditability
C. apply brand modifiers to expression, not workflow
D. output explicit decisions + confidence
```

Do not present a low-confidence graphic trend as a functional requirement.

## Output fields for domain-sensitive work

```yaml
direction:
  core_metaphor:
  density:
  color:
  typography:
  navigation:
  layout:
  geometry:
  motion:
  data_visualization:
  trust_mechanisms:
  accessibility:
  mobile_strategy:
  common_components:
  avoid:
  conventions_to_keep:
  conventions_safe_to_break:
  rationale:
  confidence:
```

## Research anchors

Primary evidence: `research/design-by-industry.md` Cross-industry rules, industry sections, Industry × Design Matrix, Cross-category decision rules, Industry Design Decision Engine, Final synthesis. Related: all domain-specific sections of `research/color-intelligence.md` § 8.
