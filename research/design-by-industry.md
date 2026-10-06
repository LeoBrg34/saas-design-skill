# Design by Industry — SaaS UI/UX Research

**Research date:** 2026-10-06  
**Purpose:** executable research for an AI design skill that adapts UI direction to product category, audience, workflow, risk, data density and device context.

> The strongest conclusion of this research is that **industry should be treated as a prior, not a hard theme preset**. A cybersecurity product is not automatically dark; a FinTech product is not automatically blue; an AI product is not automatically gradient-heavy. The durable differences come from workflow topology, information density, consequence of error, auditability, user expertise, collaboration mode and device context.

## Confidence model

- **High** — supported by explicit standards/design-system guidance and/or convergent patterns across multiple real products.
- **Medium** — repeated product/market pattern with reasonable evidence, but not a universal functional requirement.
- **Low** — mostly a graphic/branding trend. Never encode as a hard rule without additional product evidence.

## Three layers the engine must keep separate

1. **Functional conventions** — patterns caused by the job itself. These have the highest weight: e.g. a SOC needs triage/drill-down; BI needs filters and alternative access to data; sales needs records/pipeline/activity.
2. **Market conventions** — learned expectations within a category. Useful for reducing onboarding cost, but breakable.
3. **Graphic trends** — dark mode, gradients, glass, neon, oversized radii, illustration fashions. These have the lowest default weight.

## Cross-industry rules

1. **Risk overrides aesthetics.** As consequence of error rises (money movement, security remediation, clinical action), increase explicit states, confirmation, auditability, provenance and reversibility; reduce decorative motion. **Confidence: High** · Sources: [S2], [S4], [S8], [S37].
2. **Density follows decision frequency and expertise, not modern-design fashion.** Expert recurrent workflows can justifiably be compact; provide density controls or role-based views rather than forcing large cards/whitespace. **Confidence: High** · Sources: [S26], [S29], [S30].
3. **Do not equate dashboards with value.** Use dashboards for monitoring/comparison; if the primary job is action, put the action queue/work object before charts. **Confidence: High** · Sources: [S16], [S17], [S21].
4. **Color is a scarce semantic channel.** In data-, risk- and status-heavy products, reserve strong color for meaning. Never make critical meaning color-only. **Confidence: High** · Sources: [S1], [S15], [S18], [S49].
5. **Mobile parity is often the wrong goal.** Preserve the user's mobile job, not every desktop control. SAP explicitly supports adaptive behavior when the use case changes by device. **Confidence: High** · Sources: [S30].
6. **Accessibility is not industry-specific polish.** WCAG 2.2 AA-level patterns (contrast, keyboard, focus, target size, semantic structure) are a baseline; healthcare and public-sector contexts may carry additional legal/procurement consequences. **Confidence: High** · Sources: [S1], [S11], [S32], [S38].
7. **AI adds a new trust layer to every industry.** Generated/inferred content and autonomous actions should be identifiable; important actions need review, reversibility and status transparency. **Confidence: High** · Sources: [S2], [S3], [S4].

---

## AI SaaS
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Knowledge workers, creators, analysts, developers, operators and domain specialists; often mixed expertise inside the same product. | **Confidence: High** · Sources: [S2], [S3], [S4] |
| **GOALS** | Express intent, provide context, obtain/generated output, inspect it, iterate, approve or apply actions, and recover from mistakes. Agentic products add delegation, status tracking and review. | **Confidence: High** · Sources: [S2], [S3], [S4] |
| **INFORMATION DENSITY** | Start low-to-medium around the prompt and current answer; expand to medium/high in artifacts, citations, tool traces, files, code, tables, agent runs and history. Progressive disclosure is preferable to exposing the whole execution surface at once. | **Confidence: High** · Sources: [S2], [S3] |
| **COLOR STRATEGY** | Neutral working canvas; one restrained brand accent; semantic colors for generated/AI state, warnings, tool status and destructive actions. Do not make 'AI' synonymous with rainbow gradients. AI presence should be identifiable without relying on color alone. | **Confidence: High** · Sources: [S2], [S3], [S1] |
| **TYPOGRAPHY** | Highly readable sans for conversation and long generated content; monospaced style only for code/technical tokens; strong heading structure in long answers and artifacts. Avoid novelty type in primary work surfaces. | **Confidence: High** · Sources: [S3], [S11] |
| **NAVIGATION** | Conversation/history rail plus contextual workspace is a strong pattern; persistent access to projects/files/agents/tools; clear separation between conversation, generated artifact and settings. Navigation must preserve context during long-running work. | **Confidence: High** · Sources: [S3] |
| **LAYOUT** | Composer-centered single column for simple chat; split view when output becomes a durable artifact, code, preview or analysis surface. Agentic work benefits from a task/status region rather than hiding execution in chat bubbles. | **Confidence: High** · Sources: [S3], [S4] |
| **COMMON COMPONENTS** | Prompt composer, attachment/context picker, starter prompts, model/agent controls, streaming response, citations, regenerate/edit, feedback, tool/activity cards, artifact pane, approval/undo, history/versioning. | **Confidence: High** · Sources: [S2], [S3], [S4] |
| **DATA VISUALIZATION NEEDS** | Usually secondary, but AI analytics products should embed charts next to natural-language explanation and show calculation/source provenance. Explanations should not replace underlying data. | **Confidence: Medium** · Sources: [S4] |
| **TRUST REQUIREMENTS** | Very high when AI can act, recommend, transform data or make high-impact suggestions. Identify generated content, communicate state, scope and uncertainty, expose source/provenance where useful, and make consequential changes reviewable/reversible. | **Confidence: High** · Sources: [S2], [S3], [S4] |
| **ACCESSIBILITY REQUIREMENTS** | Streaming states need live-region/status equivalents; generated content needs semantic headings; all controls need accessible names; multimodal output needs alternatives; keyboard, focus, reduced motion and predictable layout are essential. | **Confidence: High** · Sources: [S1], [S3], [S11] |
| **BRAND EXPECTATIONS** | Innovative and intelligent, but increasingly calm rather than sci-fi. Product credibility rises when the interface feels like a dependable work tool, not a demo. Personality can live in illustration, microcopy and onboarding rather than the core task canvas. | **Confidence: Medium** · Sources: [S2], [S3] |
| **MOTION** | Useful for streaming/progress, transitions between planning/executing/completed states and spatial continuity. Avoid perpetual glow, animated gradients or motion that implies certainty/progress without real system state. | **Confidence: High** · Sources: [S3] |
| **MOBILE IMPORTANCE** | Medium overall; high for consumer assistants and capture/review, lower for complex artifact editing or multi-agent orchestration. Mobile should prioritize prompting, review, approvals and quick edits over reproducing desktop complexity. | **Confidence: Medium** · Sources: [S3] |
| **COMMON DESIGN PATTERNS** | Chat + artifact, progressive disclosure of reasoning/status, inline citations, contextual action cards, undo/retry, human approval gates, version history, prompt examples. | **Confidence: High** · Sources: [S2], [S3], [S4] |
| **ANTI-PATTERNS** | Fake 'thinking' theater; unexplained autonomous actions; hiding source/calculation details; irreversible actions from a conversational suggestion; dense walls of generated text; AI-only iconography or color with no text label; constant animated gradient chrome. | **Confidence: High** · Sources: [S2], [S3], [S4] |

### Convention split

Functional convention: intent → generation/action → review/recovery. Market convention: conversational entry point and side rail/history. Graphic trend: gradients, glowing orbs and iridescent AI marks; these are optional and low-confidence.

### When breaking convention is useful

Break convention when the AI is subordinate to a primary domain workflow. Example: in a CRM, embed the copilot beside the deal rather than turning the entire product into chat.

---

## FinTech
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Consumers, finance teams, controllers, accountants, founders, operations and risk teams. Expertise ranges from novice to highly financial. | **Confidence: High** · Sources: [S5], [S6], [S7] |
| **GOALS** | Move, reconcile, inspect and control money; understand balances/transactions; approve spend; search entities; investigate exceptions; generate reports; complete onboarding/KYC/payment flows. | **Confidence: High** · Sources: [S5], [S7] |
| **INFORMATION DENSITY** | Medium-to-high. Money workflows need exact values, dates, statuses and audit context, but should surface the most decision-relevant totals first. | **Confidence: High** · Sources: [S5], [S7] |
| **COLOR STRATEGY** | Neutral surfaces with restrained brand accent. Reserve red/amber/green for financial or risk states and never make positive/negative meaning depend on color alone. Avoid using saturated brand color across large data surfaces. | **Confidence: High** · Sources: [S1], [S49] |
| **TYPOGRAPHY** | High-legibility sans; tabular numerals for balances, amounts and comparisons; clear distinction between labels, values and metadata. Avoid ultra-light weights for financial figures. | **Confidence: High** · Sources: [S48], [S49] |
| **NAVIGATION** | Object- and workflow-based: accounts, transactions, cards, expenses, bills, reports, settings. Global search is unusually valuable because users often know an ID, last four digits, customer or transaction identifier. | **Confidence: High** · Sources: [S5], [S7] |
| **LAYOUT** | Summary KPIs → prioritized exceptions → searchable table/detail. Dense tables and side panels are appropriate for operators; consumer flows can be much simpler and linear. | **Confidence: High** · Sources: [S5], [S7] |
| **COMMON COMPONENTS** | Balance/KPI cards, transaction tables, filters, date ranges, reconciliation states, approval queues, receipts/documents, account selectors, audit trails, status badges, risk/verification banners. | **Confidence: High** · Sources: [S5], [S7] |
| **DATA VISUALIZATION NEEDS** | Moderate to high: cash/spend trends, category breakdowns, budget vs actual, revenue and forecasting. Charts should retain exact values through labels/tooltips/table alternatives. | **Confidence: High** · Sources: [S7], [S18] |
| **TRUST REQUIREMENTS** | Extremely high. Show transaction state, timing, permissions, security and consequences. Confirm high-risk actions and preserve auditability. Familiar financial institution branding can increase comfort in account-linking flows. | **Confidence: High** · Sources: [S6], [S7] |
| **ACCESSIBILITY REQUIREMENTS** | WCAG baseline plus strong numeric readability, non-color state encoding, generous error messaging, accessible authentication and form labels. Financial loss raises the cost of ambiguous states. | **Confidence: High** · Sources: [S1], [S49] |
| **BRAND EXPECTATIONS** | Competent, stable, secure and efficient. Modern fintech can be warm or bold in marketing, but core money movement surfaces should reduce novelty and ambiguity. | **Confidence: Medium** · Sources: [S6], [S7] |
| **MOTION** | Low-to-moderate. Use to explain transitions, pending/settled states and progress. Avoid playful motion around payments, fraud alerts or destructive actions. | **Confidence: High** · Sources: [S7] |
| **MOBILE IMPORTANCE** | High for cards, consumer banking, receipt capture, approvals and on-the-go spend; medium for controller-grade reconciliation and reporting. | **Confidence: High** · Sources: [S7] |
| **COMMON DESIGN PATTERNS** | Dashboard summary, exact-value tables, side-panel detail, search-first retrieval, approval flow, receipt attachment, pending/posted distinction, step-by-step onboarding. | **Confidence: High** · Sources: [S5], [S6], [S7] |
| **ANTI-PATTERNS** | Decorative graphs without exact values; ambiguous transaction status; novelty copy during failures; overusing red/green without labels; hiding fees or timing; irreversible transfer/action with weak confirmation. | **Confidence: High** · Sources: [S1], [S6], [S7] |

### Convention split

Functional convention: precision, auditability and explicit state. Market convention: clean neutral dashboards, strong numbers, trust cues. Graphic trend: premium gradients/neon finance marketing should not leak into high-risk task surfaces.

### When breaking convention is useful

Break convention for low-risk personal-finance education or youth products, where friendlier illustration and more expressive color can improve engagement—while keeping money state precise.

---

## Cybersecurity
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | SOC analysts, security engineers, cloud security teams, CISOs, IT admins, developers and incident responders. | **Confidence: High** · Sources: [S8], [S10], [S14] |
| **GOALS** | Detect, prioritize, investigate and remediate risk; understand blast radius; correlate signals; tune rules; document incidents; prove posture/compliance. | **Confidence: High** · Sources: [S8], [S10] |
| **INFORMATION DENSITY** | High to very high. The design challenge is not reducing all density, but separating signal from noise and supporting rapid drill-down. | **Confidence: High** · Sources: [S8], [S10] |
| **COLOR STRATEGY** | Dark mode is optional, not a functional requirement. Use restrained neutrals and a disciplined severity scale. Critical colors must map consistently to risk levels and be paired with text/icon/shape. | **Confidence: High** · Sources: [S8], [S10], [S1] |
| **TYPOGRAPHY** | Compact, highly legible sans; monospaced text for IPs, hashes, paths, rule expressions and logs; tabular numerals for counts/scores. | **Confidence: High** · Sources: [S8], [S50] |
| **NAVIGATION** | Domain grouping plus investigation flow: overview/posture → analytics/events → assets/issues → rules/policies → logs/search → settings. Preserve filters and time range across drill-down where possible. | **Confidence: High** · Sources: [S8], [S9], [S10] |
| **LAYOUT** | Risk summary and action items above; dense filters, charts, lists/tables and detail panels below. Graph views are justified when relationships/attack paths are the actual task. | **Confidence: High** · Sources: [S8], [S10] |
| **COMMON COMPONENTS** | Severity badges, finding tables, attack-path graphs, asset inventory, timelines, event/log explorers, rule editors, filters, query builders, remediation instructions, ownership and ticket integrations. | **Confidence: High** · Sources: [S8], [S10] |
| **DATA VISUALIZATION NEEDS** | High: time series, distributions, attack paths, posture scores, top sources, asset relationships. Visualizations must enable investigation rather than just executive decoration. | **Confidence: High** · Sources: [S8], [S9], [S10] |
| **TRUST REQUIREMENTS** | Extremely high. Show why a finding is critical, evidence, affected resources, sampling/coverage limits, ownership and remediation. Avoid false precision in risk scores. | **Confidence: High** · Sources: [S8], [S9], [S10] |
| **ACCESSIBILITY REQUIREMENTS** | Keyboard-heavy workflows, focus visibility, non-color severity encoding, accessible graph alternatives, readable logs and reduced-motion support. Dense SOC interfaces still need WCAG-compliant contrast. | **Confidence: High** · Sources: [S1], [S11] |
| **BRAND EXPECTATIONS** | Technical, authoritative, secure, fast. 'Hacker neon' is a marketing trope rather than a product requirement. Enterprise buyers generally reward clarity and confidence more than cyberpunk aesthetics. | **Confidence: Medium** · Sources: [S10] |
| **MOTION** | Low. Use only for real-time state changes, graph focus, timeline updates and transitions. Avoid ambient animation that competes with alerts. | **Confidence: High** · Sources: [S8] |
| **MOBILE IMPORTANCE** | Low-to-medium for investigation; medium for alerts, acknowledgement, approvals and executive posture checks. | **Confidence: Medium** · Sources: [S8], [S10] |
| **COMMON DESIGN PATTERNS** | Overview → suspicious activity → filter → event/resource detail → remediation; severity-first lists; saved views; graph context; one-click pivot to raw logs. | **Confidence: High** · Sources: [S8], [S9], [S10] |
| **ANTI-PATTERNS** | Everything red; undifferentiated alert feeds; severity only by color; security theater animations; huge score with no evidence; graph visualizations with no task outcome; hiding sampling or data coverage. | **Confidence: High** · Sources: [S8], [S9], [S10] |

### Convention split

Functional convention: triage, evidence, drill-down and remediation. Market convention: compact technical dashboards and severity coding. Graphic trend: black/neon green, terminal motifs and glowing maps—optional.

### When breaking convention is useful

Break convention when serving non-security users. Wiz explicitly emphasizes making graph risk understandable across teams; simplify vocabulary and guide next action rather than imitating a SOC console.

---

## Developer tools
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Software engineers, platform engineers, DevOps/SRE, engineering managers and open-source maintainers. | **Confidence: High** · Sources: [S12], [S13], [S14] |
| **GOALS** | Build, review, deploy, debug, monitor and collaborate without losing technical context. | **Confidence: High** · Sources: [S12], [S13], [S14] |
| **INFORMATION DENSITY** | High, but expert-controlled. Users tolerate compactness when structure and shortcuts are strong. | **Confidence: High** · Sources: [S12], [S13] |
| **COLOR STRATEGY** | Neutral/dark-or-light editor-like surfaces; semantic status for success/failure/warnings; syntax colors for code/logs. Avoid brand colors that reduce diff/log legibility. | **Confidence: High** · Sources: [S11], [S50] |
| **TYPOGRAPHY** | Sans for chrome and metadata; monospace for code, logs, hashes, commands and identifiers. Dense but readable line-height; strong alignment matters more than decorative type. | **Confidence: High** · Sources: [S50] |
| **NAVIGATION** | Repository/project/service scoped navigation; command palette/search/keyboard shortcuts are first-class. Keep context close to work instead of routing users to generic dashboards. | **Confidence: High** · Sources: [S12], [S13] |
| **LAYOUT** | Multi-pane and split views are appropriate: tree/list → primary code/diff/log surface → contextual detail. Side panels should preserve the user's current technical context. | **Confidence: High** · Sources: [S13] |
| **COMMON COMPONENTS** | Code editor/diff, terminal/log viewer, status checks, issue/PR tables, command palette, branch/environment selectors, deployment timeline, metrics, filters, copy actions. | **Confidence: High** · Sources: [S12], [S13], [S14] |
| **DATA VISUALIZATION NEEDS** | Medium-high for observability and performance; lower for source-control flows. Time series and event correlation dominate over decorative dashboards. | **Confidence: High** · Sources: [S14] |
| **TRUST REQUIREMENTS** | High: exact state, reproducibility, permissions, commit/deploy provenance and failure details matter. AI-generated code/actions need review context. | **Confidence: High** · Sources: [S13], [S3] |
| **ACCESSIBILITY REQUIREMENTS** | Keyboard access is especially critical; focus, semantic structure, high contrast, not relying solely on red/green diffs, and accessible code/terminal controls. | **Confidence: High** · Sources: [S11], [S1] |
| **BRAND EXPECTATIONS** | Technical, efficient, direct and somewhat understated. Developer audiences punish excessive marketing inside the working surface. | **Confidence: Medium** · Sources: [S12], [S13] |
| **MOTION** | Minimal; status transitions and deployment progress only. Respect reduced motion. | **Confidence: High** · Sources: [S11] |
| **MOBILE IMPORTANCE** | Low for deep coding; medium for alerts, code review, issue triage and lightweight approvals. | **Confidence: High** · Sources: [S12], [S13] |
| **COMMON DESIGN PATTERNS** | Contextual diffs, inline comments, checks near changes, project tables/boards tied to source artifacts, keyboard shortcuts, compact filters, copied commands. | **Confidence: High** · Sources: [S12], [S13] |
| **ANTI-PATTERNS** | Cardifying code-heavy data; hiding IDs/technical details; forcing mouse workflows; glossy animations; modal-heavy navigation; breaking terminal/editor mental models for branding. | **Confidence: High** · Sources: [S11], [S13] |

### Convention split

Functional convention: keep technical context adjacent to action. Market convention: monospace accents, dense chrome, dark-mode support, command palette. Graphic trend: terminal aesthetics and black backgrounds are optional.

### When breaking convention is useful

Break convention for beginner/no-code developer tools: trade density for guided workflows, previews and progressive disclosure while keeping an escape hatch to raw technical details.

---

## Analytics / BI
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Analysts, data teams, business users, executives and operational managers. | **Confidence: High** · Sources: [S15], [S16], [S17], [S19] |
| **GOALS** | Monitor KPIs, compare segments/time, detect anomalies, answer questions, drill into causes and share/report findings. | **Confidence: High** · Sources: [S16], [S17] |
| **INFORMATION DENSITY** | Medium-high. Overview dashboards should be selective; exploration surfaces can become dense. Density must follow decision hierarchy, not chart count. | **Confidence: High** · Sources: [S16], [S17] |
| **COLOR STRATEGY** | Mostly neutral canvas with a limited categorical/semantic palette. Color should encode data intentionally; do not spend scarce categorical colors on decoration. Pair color with shape/label when needed. | **Confidence: High** · Sources: [S15], [S18] |
| **TYPOGRAPHY** | Compact sans; strong numeric hierarchy; tabular figures; descriptive chart titles and captions; avoid all-caps and tiny axis text. | **Confidence: High** · Sources: [S15], [S18] |
| **NAVIGATION** | Dashboard/report collection → specific dashboard → drill-through/explore. Filters and date range should remain visible and predictable. | **Confidence: High** · Sources: [S17], [S19] |
| **LAYOUT** | Most important metric/question in the top-left/first scan region; one-screen monitoring where possible; exploration pages may scroll. Grid alignment is important for cross-chart comparison. | **Confidence: High** · Sources: [S16], [S17] |
| **COMMON COMPONENTS** | KPI cards, date ranges, filter bars, slicers, charts, tables, drill-through, legends, annotations, export/share, saved views. | **Confidence: High** · Sources: [S15], [S17], [S19] |
| **DATA VISUALIZATION NEEDS** | Very high—the product is the data interface. Prefer charts that answer a question; offer underlying data/table access; reduce marks and unnecessary encodings. | **Confidence: High** · Sources: [S15], [S16], [S18] |
| **TRUST REQUIREMENTS** | High. Users need metric definitions, date ranges, freshness, filters, lineage/semantic meaning and clarity about sampled or incomplete data. | **Confidence: High** · Sources: [S9], [S17], [S19] |
| **ACCESSIBILITY REQUIREMENTS** | Critical: alt text/captions, keyboard navigation, logical focus order, non-color encodings, data tables and manageable mark counts. Tableau and Power BI both explicitly support accessible alternatives. | **Confidence: High** · Sources: [S15], [S18] |
| **BRAND EXPECTATIONS** | Analytical, calm, precise. Brand should frame the data rather than compete with it. | **Confidence: High** · Sources: [S15], [S17] |
| **MOTION** | Low; transitions can preserve context when filtering or drilling. Avoid animated chart entrances on routine dashboards. | **Confidence: High** · Sources: [S15] |
| **MOBILE IMPORTANCE** | Medium for consumption and alerts; low-to-medium for authoring. Design separate mobile layouts rather than shrinking dense desktop dashboards. | **Confidence: High** · Sources: [S16], [S17] |
| **COMMON DESIGN PATTERNS** | Overview → compare/filter → drill-through → underlying rows; dashboard tiles; saved views; cross-filtering; focus mode. | **Confidence: High** · Sources: [S15], [S17] |
| **ANTI-PATTERNS** | Dashboard as poster; too many charts; 3D charts; redundant color; unlabeled metrics; inaccessible color scales; chart animation as decoration; horizontal-scroll-heavy mobile dashboard. | **Confidence: High** · Sources: [S15], [S16], [S18] |

### Convention split

Functional convention: data comparison and drill-down. Market convention: tile/grid dashboards and filter bars. Graphic trend: glassmorphism and colorful chart palettes should be treated skeptically when they reduce analytic clarity.

### When breaking convention is useful

Break convention for narrative analytics: a guided, editorial sequence can outperform a grid when the job is explanation rather than monitoring.

---

## CRM / Sales
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Sales reps, SDRs/BDRs, account executives, managers, RevOps and executives. | **Confidence: High** · Sources: [S20], [S21], [S22] |
| **GOALS** | Prioritize leads/deals, update records, understand account context, progress opportunities, forecast revenue and execute next actions. | **Confidence: High** · Sources: [S20], [S21] |
| **INFORMATION DENSITY** | High. CRM is a system of record, but role-based views should suppress irrelevant fields. Managers need denser pipeline views than reps. | **Confidence: High** · Sources: [S20], [S21] |
| **COLOR STRATEGY** | Neutral core with clear pipeline/status semantics; brand color for primary actions; use color sparingly in stage/status because pipelines already carry many labels and metrics. | **Confidence: High** · Sources: [S47] |
| **TYPOGRAPHY** | Density-aware sans with strong field/value hierarchy and readable compact tables. Numeric alignment is important for amounts and forecasts. | **Confidence: High** · Sources: [S48] |
| **NAVIGATION** | Object-based navigation is a stable convention: leads, contacts, accounts, opportunities/deals, activities, reports. Role-based home/command center can sit above it. | **Confidence: High** · Sources: [S20], [S21] |
| **LAYOUT** | Pipeline overview/table plus side-panel deal detail; record pages aggregate timeline, tasks, emails, related objects and next actions. Use progressive disclosure to avoid field overload. | **Confidence: High** · Sources: [S20], [S21] |
| **COMMON COMPONENTS** | Pipeline/kanban, record table, activity timeline, task list, stage progress, contact/account panel, forecast chart, filters, inline edit, notes/email/call actions. | **Confidence: High** · Sources: [S20], [S21], [S22] |
| **DATA VISUALIZATION NEEDS** | High for managers: pipeline health, conversion, forecast, rep performance and stage movement. Reps need smaller, action-oriented metrics. | **Confidence: High** · Sources: [S20], [S21] |
| **TRUST REQUIREMENTS** | High around data freshness, ownership, forecast semantics and AI recommendations. Users must distinguish system-of-record facts from inferred scores/suggestions. | **Confidence: High** · Sources: [S20], [S21] |
| **ACCESSIBILITY REQUIREMENTS** | Dense forms/tables need semantic labels, keyboard navigation and clear errors. Salesforce explicitly treats accessible components as the foundation. | **Confidence: High** · Sources: [S47], [S1] |
| **BRAND EXPECTATIONS** | Professional and energetic, but execution-focused. Friendly visuals can improve adoption; core record manipulation should remain conventional. | **Confidence: Medium** · Sources: [S20], [S22] |
| **MOTION** | Low-to-moderate. Dragging deals between stages, side-panel transitions and success feedback are useful; avoid celebratory motion on every update. | **Confidence: Medium** · Sources: [S20] |
| **MOBILE IMPORTANCE** | High for field sales, contact lookup, notes, calls and deal updates; lower for pipeline administration and report building. | **Confidence: High** · Sources: [S20] |
| **COMMON DESIGN PATTERNS** | Seller home with prioritized tasks, pipeline inspection, kanban by stage, record detail with activity timeline, inline field edits, AI next-best-action. | **Confidence: High** · Sources: [S20], [S21], [S22] |
| **ANTI-PATTERNS** | Showing every CRM field by default; burying next action; dashboard-first experience for reps; inconsistent stage colors; AI score without rationale; modal chains for routine updates. | **Confidence: High** · Sources: [S20], [S21] |

### Convention split

Functional convention: record + pipeline + activity + next action. Market convention: kanban stages, record side panels, dashboard/forecast views. Graphic trend: oversized KPI cards and playful sales gamification are optional.

### When breaking convention is useful

Break convention for very narrow vertical CRMs where the user's mental model is not 'lead/account/opportunity'. Name objects and navigation after the domain workflow instead of copying Salesforce vocabulary.

---

## Productivity
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Individuals and teams managing notes, tasks, documents, personal knowledge and lightweight workflows. | **Confidence: High** · Sources: [S23], [S24] |
| **GOALS** | Capture quickly, organize, retrieve, focus, edit, plan and complete work with minimal friction. | **Confidence: High** · Sources: [S23], [S24] |
| **INFORMATION DENSITY** | Low-to-medium by default, user-configurable upward. Personal productivity benefits from calm defaults and optional advanced structure. | **Confidence: High** · Sources: [S23], [S24] |
| **COLOR STRATEGY** | Neutral content canvas with restrained accent; allow user/project color coding but do not require it for comprehension. | **Confidence: Medium** · Sources: [S23] |
| **TYPOGRAPHY** | Readable editorial sans/serif mix is possible for documents, but application chrome should remain highly legible. Strong hierarchy and comfortable long-form reading matter. | **Confidence: Medium** · Sources: [S23] |
| **NAVIGATION** | Home/recent/favorites/search plus user-defined spaces/projects/pages. Quick capture and global search should remain available from anywhere. | **Confidence: High** · Sources: [S23], [S24] |
| **LAYOUT** | Content-first single canvas with collapsible side navigation; structured views (table, board, calendar, timeline) appear when content becomes operational. | **Confidence: High** · Sources: [S23] |
| **COMMON COMPONENTS** | Editor, task list, database/list, views, filters, calendar, reminders, quick-add, search, templates, favorites/recent. | **Confidence: High** · Sources: [S23], [S24] |
| **DATA VISUALIZATION NEEDS** | Low in general; modest charts/progress for habits, tasks or dashboards. Avoid turning simple productivity into BI. | **Confidence: High** · Sources: [S24] |
| **TRUST REQUIREMENTS** | Medium-high around sync, autosave, offline behavior, data loss and permissions. The UI should clearly communicate saved/synced state when relevant. | **Confidence: Medium** · Sources: [S24] |
| **ACCESSIBILITY REQUIREMENTS** | Keyboard shortcuts must coexist with discoverable controls; editor semantics, headings, focus, touch targets and reduced motion are important. | **Confidence: High** · Sources: [S1], [S32] |
| **BRAND EXPECTATIONS** | Calm, empowering, customizable and approachable. Visual restraint supports focus. | **Confidence: Medium** · Sources: [S23], [S24] |
| **MOTION** | Low; subtle task completion, view switching and reordering feedback. | **Confidence: High** · Sources: [S24] |
| **MOBILE IMPORTANCE** | High for capture, checklists, reminders and quick review; medium for database configuration and heavy editing. | **Confidence: High** · Sources: [S24] |
| **COMMON DESIGN PATTERNS** | Sidebar + flexible canvas, quick add, multiple views over same data, command/search entry, templates and user-controlled organization. | **Confidence: High** · Sources: [S23], [S24] |
| **ANTI-PATTERNS** | Over-configuring before value; forcing taxonomy; heavy dashboards for simple tasks; excessive notification badges; hidden autosave failures; mobile parity that reproduces desktop configuration complexity. | **Confidence: High** · Sources: [S23], [S24] |

### Convention split

Functional convention: fast capture, retrieval and focus. Market convention: flexible sidebar/canvas and multiple views. Graphic trend: minimalist beige/gray 'calm SaaS' styling is optional.

### When breaking convention is useful

Break convention when the productivity tool is intrinsically visual or spatial; a canvas-first model can replace list/page navigation.

---

## Project management
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Project managers, product/engineering teams, operations, marketing and cross-functional contributors. | **Confidence: High** · Sources: [S25], [S27], [S28] |
| **GOALS** | Plan scope, prioritize work, assign owners, track status/dependencies, coordinate handoffs, manage capacity and communicate progress. | **Confidence: High** · Sources: [S25], [S27] |
| **INFORMATION DENSITY** | Medium-high and highly user-adjustable. Backlogs often need compact mode; stakeholder views should be simplified. | **Confidence: High** · Sources: [S26], [S27] |
| **COLOR STRATEGY** | Neutral shell with semantic status/priority/assignee cues. Many simultaneous labels create color overload quickly; use text and grouping as primary structure. | **Confidence: High** · Sources: [S26] |
| **TYPOGRAPHY** | Compact sans; task title first, metadata secondary. Dense list views need strong alignment and truncation/tooltip strategies. | **Confidence: High** · Sources: [S26] |
| **NAVIGATION** | Workspace/project hierarchy with task views: list, board, backlog, timeline/Gantt, calendar, dashboard. Users should switch views without duplicating the underlying work. | **Confidence: High** · Sources: [S25], [S27] |
| **LAYOUT** | View-centric. Board for flow, list for scanning/editing, timeline for dependencies, workload for capacity, dashboard for portfolio status. | **Confidence: High** · Sources: [S25], [S27] |
| **COMMON COMPONENTS** | Task cards/rows, status, assignee, due date, priority, custom fields, comments, dependencies, filters, bulk actions, board, backlog, timeline, workload. | **Confidence: High** · Sources: [S25], [S26], [S27] |
| **DATA VISUALIZATION NEEDS** | Medium: progress, burndown, workload, portfolio risk and timing. The visual form should match the planning question. | **Confidence: High** · Sources: [S27] |
| **TRUST REQUIREMENTS** | High around ownership, due dates, dependency changes, notifications and automation. Audit/history is important for teams. | **Confidence: Medium** · Sources: [S27] |
| **ACCESSIBILITY REQUIREMENTS** | Drag-and-drop must have keyboard alternatives; board status cannot rely only on color; focus order in dense task surfaces must be predictable. | **Confidence: High** · Sources: [S1], [S32] |
| **BRAND EXPECTATIONS** | Energetic but workmanlike. More expressive color is tolerated than in security/finance, provided task readability survives. | **Confidence: Medium** · Sources: [S28] |
| **MOTION** | Moderate for reordering, drag/drop, timeline resizing and status transitions. Motion should clarify spatial change. | **Confidence: High** · Sources: [S25], [S27] |
| **MOBILE IMPORTANCE** | Medium-high for task updates, comments, capture and status checks; lower for dependency planning and dense portfolio views. | **Confidence: High** · Sources: [S27] |
| **COMMON DESIGN PATTERNS** | Same work represented across board/list/timeline/calendar; compact density toggle; quick filters; inline edits; bulk selection; full-screen focus mode. | **Confidence: High** · Sources: [S25], [S26], [S27] |
| **ANTI-PATTERNS** | Treating Kanban as universal; putting all fields on cards; no compact mode; drag-only interactions; dashboard charts disconnected from editable work; too many status colors. | **Confidence: High** · Sources: [S25], [S26] |

### Convention split

Functional convention: task object with multiple workflow views. Market convention: Kanban/list/timeline/calendar. Graphic trend: colorful card boards are common but should not dictate the whole system.

### When breaking convention is useful

Break convention when work is event-, asset- or document-centric rather than task-centric; use the domain object as the primary unit and expose tasks as secondary workflow metadata.

---

## Enterprise software
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Role-diverse employees, specialists, admins, managers and executives operating complex business processes across large organizations. | **Confidence: High** · Sources: [S29], [S30], [S31] |
| **GOALS** | Complete role-specific business processes accurately, handle exceptions, access records, approve work and coordinate across systems. | **Confidence: High** · Sources: [S29], [S30] |
| **INFORMATION DENSITY** | Medium-high to very high depending role. Enterprise design should support density modes and role-based reduction rather than one universal sparse layout. | **Confidence: High** · Sources: [S29], [S30] |
| **COLOR STRATEGY** | Tokenized, restrained, accessible and semantically consistent across many modules. Brand color is less important than cross-product coherence and state clarity. | **Confidence: High** · Sources: [S31], [S49] |
| **TYPOGRAPHY** | Systematic type ramp, readable compact styles and localization resilience. Avoid brand-specific typography that breaks dense tables or multilingual layouts. | **Confidence: High** · Sources: [S32], [S48] |
| **NAVIGATION** | Role/task-based global navigation plus local object/process navigation. Search and recent/favorites reduce deep hierarchy cost. | **Confidence: High** · Sources: [S29] |
| **LAYOUT** | Modular page/floorplan patterns; tables, forms and master-detail layouts are common. Responsive/adaptive behavior should change function where mobile context differs, not merely shrink desktop. | **Confidence: High** · Sources: [S30] |
| **COMMON COMPONENTS** | Data tables, forms, master-detail, filters, object pages, approval queues, notifications, search, role dashboards, dialogs/drawers, bulk actions. | **Confidence: High** · Sources: [S29], [S31] |
| **DATA VISUALIZATION NEEDS** | Medium-high, mainly operational KPIs, exceptions and trends. Data viz must connect to workflows/actions. | **Confidence: High** · Sources: [S31] |
| **TRUST REQUIREMENTS** | Very high: permissions, auditability, stability, predictable patterns and data integrity. Consistency across modules is a trust mechanism. | **Confidence: High** · Sources: [S29], [S31] |
| **ACCESSIBILITY REQUIREMENTS** | High and often procurement-critical. WCAG, keyboard, zoom/reflow, screen reader and localization should be design-system-level requirements. | **Confidence: High** · Sources: [S32], [S47], [S1] |
| **BRAND EXPECTATIONS** | Professional, coherent, durable, configurable. Delight is welcome but must not destabilize learned workflows. | **Confidence: High** · Sources: [S29] |
| **MOTION** | Low; purposeful transitions only. Enterprise apps often run for hours, so ambient motion becomes fatigue. | **Confidence: High** · Sources: [S29] |
| **MOBILE IMPORTANCE** | Varies by role. Approvals/field service can be mobile-critical; data entry/admin can remain desktop-first. Adaptive feature sets are valid. | **Confidence: High** · Sources: [S30] |
| **COMMON DESIGN PATTERNS** | Role-based home, worklists, master-detail, wizard for complex setup, compact/cozy density, responsive grids, persistent filters and saved variants. | **Confidence: High** · Sources: [S29], [S30] |
| **ANTI-PATTERNS** | Consumer-style oversimplification that hides necessary controls; monolithic mega-forms; inconsistent module navigation; desktop UI squeezed onto mobile; custom components bypassing the design system. | **Confidence: High** · Sources: [S29], [S30], [S31] |

### Convention split

Functional convention: role-based workflows, consistency, adaptive complexity. Market convention: left navigation, tables/forms and module dashboards. Graphic trend: 'modern enterprise' large-radius cards and oversized whitespace can actively harm dense workflows.

### When breaking convention is useful

Break convention when a specific role performs one narrow job repeatedly: a focused task app can outperform the parent suite's full enterprise shell.

---

## Healthcare SaaS
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Clinicians, practice staff, billers, administrators, patients and caregivers. Cognitive load and digital literacy vary widely. | **Confidence: High** · Sources: [S33], [S35], [S36] |
| **GOALS** | Schedule, document care, review patient data, communicate, bill/pay, manage forms, conduct telehealth and complete time-sensitive clinical/admin work. | **Confidence: High** · Sources: [S33], [S35], [S36] |
| **INFORMATION DENSITY** | Clinician side: high; patient side: low-to-medium. Clinical data should be prioritized by safety/relevance, not visual minimalism alone. | **Confidence: High** · Sources: [S37] |
| **COLOR STRATEGY** | Calm neutral surfaces and restrained accent; semantic alerts must be unambiguous and never color-only. Avoid decorative color that competes with clinical warnings. | **Confidence: High** · Sources: [S1], [S37] |
| **TYPOGRAPHY** | High legibility, generous enough size, predictable hierarchy, readable numbers/dates. Avoid ultra-light type and overly condensed fonts. | **Confidence: High** · Sources: [S38], [S1] |
| **NAVIGATION** | Clinician: schedule/patient/charting/billing/communications/reports. Patient: appointments/messages/results/forms/payments. Separate role experiences rather than exposing provider complexity to patients. | **Confidence: High** · Sources: [S33], [S34], [S35] |
| **LAYOUT** | Clinician work often centers on calendar/schedule or patient chart with contextual panels. Patient experiences should use straightforward task cards and stepwise flows. | **Confidence: High** · Sources: [S33], [S34], [S35] |
| **COMMON COMPONENTS** | Calendar/schedule, patient list/search, chart/note editor, results, forms/consent, messaging, telehealth, billing, insurance, reminders, portal task list. | **Confidence: High** · Sources: [S33], [S35], [S36] |
| **DATA VISUALIZATION NEEDS** | Medium: labs/vitals/trends, appointment utilization, revenue and population health. Clinical visualization needs exact values, units and reference context. | **Confidence: Medium** · Sources: [S37] |
| **TRUST REQUIREMENTS** | Extremely high due privacy, safety and clinical consequences. Make patient identity/context persistent, actions attributable, permissions clear and destructive/clinical actions deliberate. | **Confidence: High** · Sources: [S37], [S38] |
| **ACCESSIBILITY REQUIREMENTS** | Exceptionally high. HHS rules explicitly address web/mobile accessibility for covered recipients; telehealth must accommodate disability-related communication needs. WCAG-level accessibility should be treated as baseline, not polish. | **Confidence: High** · Sources: [S38], [S1] |
| **BRAND EXPECTATIONS** | Reassuring, humane, calm and competent. Healthcare does not require sterile blue; warmth can improve patient comfort if it never obscures safety/status. | **Confidence: Medium** · Sources: [S35] |
| **MOTION** | Low. Motion should guide progress, confirm state and support scheduling interactions; avoid decorative or time-pressuring effects. | **Confidence: High** · Sources: [S37] |
| **MOBILE IMPORTANCE** | High for patient portals, appointments, messaging, telehealth and payments; medium for clinician review; lower for heavy charting/billing. | **Confidence: High** · Sources: [S34], [S36] |
| **COMMON DESIGN PATTERNS** | Schedule-first clinician home, patient chart with persistent identity, secure portal, guided forms, task reminders, simple self-service booking and payments. | **Confidence: High** · Sources: [S33], [S34], [S35] |
| **ANTI-PATTERNS** | Tiny dense EHR text; alert fatigue; ambiguous patient context; color-only alerts; decorative dashboards before clinical tasks; forcing desktop charting patterns into patient mobile; inaccessible telehealth. | **Confidence: High** · Sources: [S37], [S38] |

### Convention split

Functional convention: patient safety, identity, clinical/admin workflow and accessibility. Market convention: schedule/chart/portal structures. Graphic trend: soft wellness palettes are appropriate for some patient experiences but not a substitute for clinical clarity.

### When breaking convention is useful

Break convention in wellness/private-practice products where warmth and friendliness reduce intimidation. Jane demonstrates that healthcare software can be intentionally approachable while still handling secure operational workflows.

---

## E-commerce SaaS
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Merchants, store operators, fulfillment teams, support staff, marketers and e-commerce managers. | **Confidence: High** · Sources: [S39] |
| **GOALS** | Manage products/orders/customers/inventory, fulfill orders, monitor sales, configure storefront/checkout and handle exceptions. | **Confidence: High** · Sources: [S39] |
| **INFORMATION DENSITY** | Medium-high in admin; low on setup/onboarding. Orders and inventory benefit from compact lists and bulk actions. | **Confidence: High** · Sources: [S39] |
| **COLOR STRATEGY** | Neutral admin canvas; brand accent for primary action; semantic fulfillment/payment/return states. Merchant brand colors belong in storefront preview, not necessarily admin chrome. | **Confidence: High** · Sources: [S39], [S1] |
| **TYPOGRAPHY** | Readable utilitarian sans; tabular numerals for prices/quantities; product names and order IDs need strong scanning hierarchy. | **Confidence: High** · Sources: [S39] |
| **NAVIGATION** | Core commerce objects: home, orders, products, customers, inventory, analytics, marketing, channels/settings. Search should support order/customer/product retrieval. | **Confidence: High** · Sources: [S39] |
| **LAYOUT** | Object lists with filters and bulk actions; order/product detail pages; dashboard for sales/operations; contextual editor/preview for storefront content. | **Confidence: High** · Sources: [S39] |
| **COMMON COMPONENTS** | Order table, status chips, product/media editor, inventory count, fulfillment timeline, customer detail, analytics cards/charts, bulk actions, filters, channel/store selector. | **Confidence: High** · Sources: [S39] |
| **DATA VISUALIZATION NEEDS** | Medium-high: sales, conversion, AOV, order volume, fulfillment and forecast trends. Operational tables are often more important than charts. | **Confidence: High** · Sources: [S39] |
| **TRUST REQUIREMENTS** | High for payments, fulfillment, refunds, inventory and customer data. Confirm irreversible actions and expose status/timestamps. | **Confidence: High** · Sources: [S39] |
| **ACCESSIBILITY REQUIREMENTS** | Admin needs WCAG baseline; merchant-created storefront tooling should encourage accessible content/contrast/alt text because the SaaS shapes downstream customer experiences. | **Confidence: Medium** · Sources: [S1] |
| **BRAND EXPECTATIONS** | Practical, optimistic and merchant-empowering. More visual expression is acceptable in onboarding/templates than in order operations. | **Confidence: Medium** · Sources: [S39] |
| **MOTION** | Low-to-moderate; useful in drag/reorder, media upload and fulfillment state. Storefront preview animation is separate from admin workflow. | **Confidence: Medium** · Sources: [S39] |
| **MOBILE IMPORTANCE** | High for order monitoring, inventory checks, fulfillment and notifications; lower for theme/storefront configuration and complex reporting. | **Confidence: Medium** · Sources: [S39] |
| **COMMON DESIGN PATTERNS** | Commerce object table → detail → action; status-heavy order lifecycle; sales overview; setup checklist; preview/editor split. | **Confidence: High** · Sources: [S39] |
| **ANTI-PATTERNS** | Marketing-site aesthetics inside order operations; weak distinction between paid/unpaid/fulfilled/refunded; hidden inventory effects; card grids replacing efficient order tables; mobile admin with missing critical actions. | **Confidence: High** · Sources: [S39] |

### Convention split

Functional convention: commerce objects and lifecycle states. Market convention: order/product/customer navigation and analytics dashboard. Graphic trend: highly visual storefront motifs should remain separated from operational admin UI.

### When breaking convention is useful

Break convention for creator/one-product commerce where the merchant primarily edits content and checks a small order stream; a content-first home can beat a traditional admin dashboard.

---

## Marketing SaaS
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Marketers, growth teams, lifecycle/CRM marketers, content teams, agencies and SMB owners. | **Confidence: High** · Sources: [S40], [S41] |
| **GOALS** | Create campaigns, choose audiences, automate journeys, send/publish, monitor performance, attribute conversion and iterate. | **Confidence: High** · Sources: [S40], [S41] |
| **INFORMATION DENSITY** | Medium. Creation surfaces should be focused; analytics and segmentation can become high-density. | **Confidence: High** · Sources: [S40], [S41] |
| **COLOR STRATEGY** | More expressive brand color is acceptable than in finance/security, especially in creation. Analytics surfaces should return to neutral backgrounds with disciplined data colors. | **Confidence: Medium** · Sources: [S40] |
| **TYPOGRAPHY** | Friendly, readable sans with clear hierarchy. Editor preview may reflect campaign brand typography, but product chrome should remain stable. | **Confidence: Medium** · Sources: [S41] |
| **NAVIGATION** | Campaigns, audience/contacts, automations/journeys, content/templates, analytics/reports, integrations/settings. | **Confidence: High** · Sources: [S40], [S41] |
| **LAYOUT** | Campaign creation as stepwise builder or canvas; audience segmentation as filter/query builder; analytics as KPI + funnel/time-series + drill-down. | **Confidence: High** · Sources: [S40], [S41] |
| **COMMON COMPONENTS** | Campaign builder, template gallery, audience/segment builder, automation flow, calendar, preview, channel selector, A/B test, KPI cards, funnel, report table. | **Confidence: High** · Sources: [S40], [S41] |
| **DATA VISUALIZATION NEEDS** | High: delivery, opens/clicks, conversion, revenue attribution, funnels and period comparison. Bot/filtering or tracking caveats must be visible when they affect interpretation. | **Confidence: High** · Sources: [S40], [S41] |
| **TRUST REQUIREMENTS** | High around audience selection, send scope, tracking, attribution and irreversible sends. Pre-send review and recipient counts are key trust surfaces. | **Confidence: High** · Sources: [S40], [S41] |
| **ACCESSIBILITY REQUIREMENTS** | Product chrome plus campaign authoring assistance: accessible templates, alt text prompts, contrast checks and keyboard operation are valuable because output reaches external audiences. | **Confidence: Medium** · Sources: [S1] |
| **BRAND EXPECTATIONS** | Creative, energetic, approachable and confidence-building. The product may show more personality than enterprise/security tools. | **Confidence: Medium** · Sources: [S40], [S41] |
| **MOTION** | Moderate in builders, flow diagrams, previews and success states. Avoid animation that distracts from analytics or send confirmation. | **Confidence: Medium** · Sources: [S40] |
| **MOBILE IMPORTANCE** | Medium for monitoring/approvals; lower for complex campaign construction and automation flow editing. | **Confidence: Medium** · Sources: [S41] |
| **COMMON DESIGN PATTERNS** | Draft → audience → content → settings → review/send; automation canvas; dashboard with channel/filter/date comparison; segmentation rule builder. | **Confidence: High** · Sources: [S40], [S41] |
| **ANTI-PATTERNS** | Creative branding overwhelming metric legibility; send button without clear audience/context; vanity metrics without conversion context; confusing attribution; automation canvas with no textual/list representation. | **Confidence: High** · Sources: [S40], [S41] |

### Convention split

Functional convention: create → target → launch → measure. Market convention: campaign builders, journey canvases and analytics. Graphic trend: bright playful brand systems are common but should be separated from high-stakes send/revenue interpretation.

### When breaking convention is useful

Break convention for performance-marketing products used by analysts: reduce visual playfulness and increase density, comparison and keyboard efficiency.

---

## Collaboration tools
| Dimension | Design direction | Evidence |
|---|---|---|
| **USERS** | Cross-functional teams, knowledge workers, managers, external partners and distributed organizations. | **Confidence: High** · Sources: [S42], [S43], [S45] |
| **GOALS** | Communicate, catch up, coordinate, share files/knowledge, find past decisions, collaborate synchronously/asynchronously and reduce context switching. | **Confidence: High** · Sources: [S42], [S43], [S45] |
| **INFORMATION DENSITY** | Medium-high because message streams accumulate rapidly. The key design problem is triage and retrieval rather than displaying everything equally. | **Confidence: High** · Sources: [S44], [S45] |
| **COLOR STRATEGY** | Neutral message/content surfaces with clear unread/mention/status indicators. User avatars and channel/team identity can carry color, but attention signals need restraint. | **Confidence: High** · Sources: [S45] |
| **TYPOGRAPHY** | Highly readable conversational sans, compact metadata, clear message hierarchy. Long-form canvases/docs need document-grade hierarchy. | **Confidence: High** · Sources: [S42] |
| **NAVIGATION** | Persistent conversation/channel list + search + activity/mentions/favorites. Users benefit from customizable sections and recency/priority filters. | **Confidence: High** · Sources: [S43], [S44], [S45] |
| **LAYOUT** | Three-region desktop pattern is common: navigation/list → conversation/content → contextual thread/details. Flexible panes reduce context switching. | **Confidence: High** · Sources: [S45], [S46] |
| **COMMON COMPONENTS** | Channel/DM list, unread badges, message composer, threads, reactions, mentions, search, file preview, huddles/meetings, canvas/doc, tabs, notifications, presence. | **Confidence: High** · Sources: [S42], [S43], [S45] |
| **DATA VISUALIZATION NEEDS** | Low in core communication; moderate for admin/usage analytics and embedded domain apps. | **Confidence: High** · Sources: [S42] |
| **TRUST REQUIREMENTS** | High around audience/visibility, guest/external status, permissions, retention and who will receive a message. Public/private context must be obvious. | **Confidence: High** · Sources: [S43] |
| **ACCESSIBILITY REQUIREMENTS** | Keyboard navigation, focus management, live updates, accessible reactions/mentions, captions/transcripts for calls, reduced motion and screen-reader-friendly message structure. | **Confidence: High** · Sources: [S32], [S1] |
| **BRAND EXPECTATIONS** | Human, lively and social, but still organized. Personality can be stronger than in data/finance products because social cohesion is part of the job. | **Confidence: Medium** · Sources: [S42] |
| **MOTION** | Moderate for presence, messages, pane transitions and call states; should not cause layout shifts or steal attention during high-volume chat. | **Confidence: High** · Sources: [S45] |
| **MOBILE IMPORTANCE** | Very high. Messaging, catch-up, notifications and calls are core mobile workflows; configuration/admin can remain desktop-biased. | **Confidence: High** · Sources: [S44], [S45] |
| **COMMON DESIGN PATTERNS** | Persistent sidebar, unread/mentions triage, thread side pane, global search with filters, channel tabs, recaps/summaries, context-rich notifications. | **Confidence: High** · Sources: [S43], [S44], [S45] |
| **ANTI-PATTERNS** | Notification overload; ambiguous send audience; nested navigation that hides unread work; threads that lose parent context; search without filters; forcing every collaborative artifact into a chat stream. | **Confidence: High** · Sources: [S43], [S44], [S45] |

### Convention split

Functional convention: streams, triage, context and retrieval. Market convention: left conversation rail, threads, mentions, search. Graphic trend: colorful social chrome is optional; information architecture is the durable part.

### When breaking convention is useful

Break convention when collaboration is attached to a primary artifact (design, document, code, whiteboard). Put conversation beside the artifact instead of making channels the center of gravity.

---

# Industry × Design Matrix

| Industry | COLOR | TYPOGRAPHY | DENSITY | NAVIGATION | GEOMETRY | MOTION | TRUST | DATA | MOBILE |
|---|---|---|---|---|---|---|---|---|---|
| AI SaaS | Neutral + AI semantic accent | Readable sans + mono for code | Low→high progressive | History/projects + context | Soft/neutral, moderate radius | Medium, state-driven | Very high | Variable, provenance | High capture/review |
| FinTech | Neutral + restrained brand + strict semantic | Sans + tabular numerals | Med–high | Objects/workflows + search | Crisp, moderate radius | Low | Extremely high | Med–high exact | High |
| Cybersecurity | Neutral/dark optional + severity scale | Compact sans + mono | High–very high | Overview→events/assets/rules/logs | Crisp/technical | Low | Extremely high | Very high | Low–medium |
| Developer tools | Neutral/editor + semantic status | Sans + mono | High | Project/repo/service + command search | Compact/technical | Low | High | Med–high | Low–medium |
| Analytics / BI | Neutral + data palette | Sans + tabular | Med–high | Collections→dashboard→drill | Grid-aligned | Low | High | Very high | Medium consumption |
| CRM / Sales | Neutral + stage/status | Density-aware sans | High | Objects + seller home | Moderate radius | Low–medium | High | High | High field use |
| Productivity | Neutral + optional user color | Readable editorial/sans | Low–medium, configurable | Recent/favorites/search + spaces | Soft/moderate | Low | Medium–high | Low | High |
| Project management | Neutral + status/priority | Compact sans | Med–high | Workspace/project + views | Cards/rows, moderate radius | Medium spatial | High | Medium | Med–high |
| Enterprise software | Tokenized neutral + semantic | Systematic sans | Med–very high | Role + task/object hierarchy | Conservative/systematic | Low | Very high | Med–high | Role-dependent |
| Healthcare SaaS | Calm neutral + safety semantic | High-legibility sans | High clinician / low patient | Role-specific | Calm, moderate | Low | Extremely high | Medium | High patient |
| E-commerce SaaS | Neutral admin + lifecycle semantic | Utilitarian sans + tabular | Med–high | Commerce objects | Moderate | Low–medium | High | Med–high | High ops |
| Marketing SaaS | Expressive creation + neutral analytics | Friendly sans | Medium | Campaign/audience/automation/analytics | Friendly/moderate | Medium | High at send/attribution | High | Medium |
| Collaboration tools | Neutral streams + attention states | Conversational sans | Med–high | Conversations + search/activity | Friendly/moderate | Medium | High permissions | Low core | Very high |

---

# Cross-category decision rules

## 1. Determine workflow archetype before styling

Assign one or more workflow archetypes:

- **Conversation / generation** → AI SaaS.
- **Record + transaction** → FinTech, CRM, e-commerce, healthcare.
- **Triage + investigation** → cybersecurity, observability.
- **Explore + compare** → analytics / BI.
- **Create + publish + measure** → marketing.
- **Plan + move work through states** → project management.
- **Capture + organize + retrieve** → productivity.
- **Stream + catch up + coordinate** → collaboration.
- **Role-based process execution** → enterprise software.
- **Code/context + review + automation** → developer tools.

**Rule:** if the product's actual workflow archetype conflicts with its market label, the workflow wins.  
**Confidence: High** · Sources: [S8], [S12], [S16], [S20], [S25], [S29], [S40], [S43].

## 2. Compute consequence-of-error level

Use a 0–4 scale:

- **0 — reversible/creative:** brainstorming, note styling.
- **1 — low consequence:** task status, personal preference.
- **2 — operational:** campaign settings, deployment config, CRM edits.
- **3 — financial/security/organizational:** payment, refund, permission, security rule, large send.
- **4 — clinical/safety/critical infrastructure:** patient-context actions, incident containment, high-impact automated actions.

As level increases:

- reduce playful/ambient motion;
- increase confirmation and preview;
- show scope and affected objects;
- make state changes explicit;
- add audit/history;
- expose evidence/provenance;
- make undo/recovery visible;
- prefer text labels in addition to icon/color.

**Confidence: High** · Sources: [S2], [S4], [S8], [S10], [S37], [S38].

## 3. Compute density target

Inputs:

- expertise: novice / mixed / expert;
- items inspected per session;
- number of fields needed to decide;
- frequency of repeat use;
- desktop share;
- need for cross-row comparison.

Heuristic:

```text
density_score =
  +2 if expert recurrent workflow
  +2 if cross-row comparison is primary
  +2 if >20 objects routinely scanned
  +1 if keyboard-first
  -2 if novice onboarding
  -2 if single-object focused task
  -2 if mobile is primary
```

Map:
- score ≤ -2 → spacious;
- -1..2 → balanced;
- 3..5 → compact;
- ≥6 → compact + user density controls.

Do **not** use card size/whitespace as a proxy for premium quality.

## 4. Choose navigation by object topology

- **Many durable business objects:** object nav (CRM, commerce, finance).
- **Many streams:** conversation/channel rail + activity/search (collaboration).
- **Many technical scopes:** project/repo/service nav + command search (developer).
- **Many views over same work:** project nav + view switcher (PM/productivity).
- **Investigative funnels:** overview → filtered event/list → detail (security/BI).
- **Role-diverse suite:** role/global nav + local process/object nav (enterprise).
- **Conversational AI:** history/projects + contextual work surface, unless AI is embedded inside another domain product.

## 5. Choose color strategy by semantic pressure

Define `semantic_pressure` as the number/importance of states simultaneously encoded: severity, status, stage, ownership, category, success/error, data series.

- **Low pressure:** productivity, simple AI chat → brand can be more expressive.
- **Medium:** marketing, project management, CRM → moderate expression, controlled status palette.
- **High:** analytics, security, finance, healthcare → neutral canvas and disciplined semantic palette.

If color already carries risk/stage/data meaning, avoid spending saturated colors on card backgrounds or decorative gradients.

## 6. Typography rules by content type

- **Long reading / AI output / docs:** comfortable body scale and line length.
- **Dense records/tables:** compact sans with strong hierarchy.
- **Money/KPIs:** tabular numerals.
- **Code/logs/IDs:** monospace selectively.
- **Clinical/legal/high-risk:** never use low-contrast light weights for essential text.
- **Marketing creation:** previews may use campaign typography; product chrome should stay stable.

## 7. Geometry rules

Geometry is weakly determined by industry and strongly by density + brand.

- High-density expert surfaces → smaller radii, tighter spacing, clearer borders/dividers.
- Friendly creation/collaboration → moderate radii and softer grouping.
- Large rounded cards everywhere are a **graphic trend**, not an industry rule.
- In tables/forms, border and alignment frequently outperform shadow as hierarchy.

## 8. Motion rules

Use motion when it explains:

- spatial reordering;
- progress/state transition;
- relationship between origin and destination;
- live activity that materially changes user action.

Reduce motion as consequence-of-error and session duration increase.  
Never use animation as the only indicator of asynchronous state. **Confidence: High** · Sources: [S3].

## 9. Mobile decision

Classify every feature:

- **capture** — usually mobile-friendly;
- **review/approve** — usually mobile-friendly;
- **communicate** — strongly mobile-friendly;
- **monitor** — mobile-friendly if summarized;
- **author/configure** — often desktop-biased;
- **investigate/compare large data** — desktop-biased;
- **bulk manipulate** — desktop-biased.

Build a mobile workflow, not a compressed desktop screenshot. **Confidence: High** · Sources: [S30].

---

# Industry Design Decision Engine

## Inputs

```yaml
PRODUCT:
AUDIENCE:
PRIMARY_JOBS:
SECONDARY_JOBS:
RISK_LEVEL: 0-4
USER_EXPERTISE: novice | mixed | expert
DATA_VOLUME: low | medium | high | extreme
OBJECT_COUNT_PER_SESSION:
REALTIME: none | occasional | continuous
COLLABORATION: low | medium | high
MOBILE_SHARE: low | medium | high
REGULATORY_CONTEXT:
BRAND_TRAITS:
AI_AUTONOMY: none | assistive | proposes_actions | executes_actions
```

## Step A — Infer base industry prior

Map `PRODUCT` to one or more category priors. Hybrid products may blend priors, e.g.:

```text
AI security copilot
= cybersecurity workflow prior
+ AI transparency/action prior
NOT
= generic AI chat visual theme
```

Industry prior weight: **20–30%** of the decision.

## Step B — Apply hard overrides

Hard overrides outrank industry:

1. accessibility/legal requirements;
2. consequence of error;
3. user expertise and task frequency;
4. data density/cross-row comparison;
5. primary device;
6. real-time state;
7. permissions/auditability.

Combined override weight: **50–65%**.

## Step C — Apply brand modifiers

Brand changes the expression, not the workflow.

Examples:

```text
secure + premium
→ lower saturation, high contrast, exact spacing, controlled motion

friendly + enterprise
→ warmer accent, clearer language, softer illustration
  while retaining compact tables and predictable navigation

developer-first + playful
→ compact technical core + playful empty states/onboarding
  rather than playful code/log surfaces
```

Brand weight: **15–25%**.

## Step D — Generate explicit decisions

The engine must output:

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
  source_refs:
```

## Step E — Confidence rule

For each important output:

- **High:** direct functional/standards evidence + ≥2 convergent products/design systems.
- **Medium:** repeated market convention but workflow allows alternatives.
- **Low:** mostly style trend or inferred branding convention.

The engine should refuse to present a **Low-confidence visual trend as a functional requirement**.

---

# Worked example

## Input

```yaml
PRODUCT: cybersecurity SaaS
AUDIENCE: enterprise security teams
PRIMARY_JOBS:
  - monitor security posture
  - prioritize critical risks
  - investigate attack paths
  - remediate findings
RISK_LEVEL: 4
USER_EXPERTISE: expert
DATA_VOLUME: extreme
OBJECT_COUNT_PER_SESSION: 100+
REALTIME: continuous
COLLABORATION: high
MOBILE_SHARE: low
REGULATORY_CONTEXT: enterprise procurement, WCAG target
BRAND_TRAITS:
  - premium
  - technical
  - trustworthy
AI_AUTONOMY: proposes_actions
```

## Engine output

### Core metaphor
**Security operations / investigation workspace**, not generic SaaS dashboard and not chatbot-first.  
**Confidence: High** · Sources: [S8], [S9], [S10].

### Density
**Compact desktop-first with progressive drill-down and optional density controls.** The audience is expert, scans many findings and compares rows; oversized cards would reduce throughput.  
**Confidence: High** · Sources: [S8], [S26].

### Color
**Neutral base; one restrained brand accent; fixed severity tokens for critical/high/medium/low; status always reinforced by text/icon.** Dark mode may be supported, but it is not required to “look cyber.”  
**Confidence: High** for semantic strategy · Sources: [S8], [S10], [S1].  
**Confidence: Low** for dark mode as an industry identity.

### Typography
**Compact sans for UI, monospaced treatment for IPs/hashes/paths/queries, tabular numerals for counts/scores.**  
**Confidence: High** · Sources: [S8], [S50].

### Navigation
```text
Overview
Analytics / Events
Issues / Findings
Assets
Attack paths / Graph
Rules / Policies
Logs / Search
Reports
Settings
```

Persist account/project scope, time range and major filters across investigative pivots where feasible.  
**Confidence: High** · Sources: [S8], [S9], [S10].

### Layout
Top layer:
- posture + critical action items;
- high-signal trend/anomaly summary.

Primary work layer:
- dense finding/event table;
- fast filters/query;
- saved views.

Context layer:
- right-side detail panel or dedicated detail;
- evidence;
- affected assets;
- attack path;
- owner;
- remediation;
- related logs.

**Confidence: High** · Sources: [S8], [S10].

### Geometry
Small-to-moderate radii, clear dividers, compact vertical rhythm. Avoid huge floating cards and excessive glass/shadow.  
**Confidence: Medium** — derived from density and workflow more than an explicit security standard.

### Motion
Minimal. Use for:
- live update arrival;
- filter/drill transition;
- graph focus/path reveal;
- remediation progress.

No ambient scanning/grid/glow animations.  
**Confidence: High** on minimizing distraction; **Low** on any specific aesthetic. Sources: [S3], [S8].

### Data visualization
Use:
- time series for event volume;
- stacked distributions only when categories remain readable;
- attack-path graph where relationship is the decision;
- top-source tables;
- posture trends;
- direct pivot to raw logs.

Expose sampling/coverage caveats.  
**Confidence: High** · Sources: [S8], [S9], [S10].

### Trust mechanisms
- reason a finding is prioritized;
- evidence and affected resources;
- source/time window;
- ownership;
- remediation preview;
- approval before AI-proposed consequential action;
- audit trail;
- undo/rollback where technically possible.

**Confidence: High** · Sources: [S3], [S4], [S8], [S10].

### Accessibility
- WCAG 2.2 AA target;
- visible keyboard focus;
- no color-only severity;
- accessible names for icon controls;
- textual/tabular alternative for graphs;
- screen-reader announcements for real-time/AI status;
- reduced motion.

**Confidence: High** · Sources: [S1], [S3], [S11].

### Mobile strategy
Do not port the full SOC console. Prioritize:
- critical alert;
- acknowledge/assign;
- concise evidence;
- owner/contact;
- safe approval/escalation;
- posture summary.

Deep query/log/graph work remains desktop-first.  
**Confidence: Medium-High** — follows device/task adaptation principles [S30] and security workflow evidence [S8].

### Conventions to keep
- severity hierarchy;
- filterable findings/events;
- raw evidence;
- drill-down;
- audit history;
- role/ownership;
- technical identifiers.

### Conventions safe to break
- dark theme;
- neon green;
- world maps;
- “hacker” iconography;
- glowing graphs;
- terminal-styled navigation.

Those are visual tropes, not functional requirements.

---

# Practical output template for an AI skill

```md
## Direction
<1 paragraph>

## Decision table
| Dimension | Decision | Why | Confidence | Sources |
|---|---|---|---|---|
| Color | ... | ... | High | S1, S8 |
...

## Conventions
### Keep
...
### Optional
...
### Break deliberately
...

## Component priorities
1. ...
2. ...

## Anti-patterns
- ...

## Responsive/mobile transformation
- Desktop: ...
- Tablet: ...
- Mobile: ...

## Validation checklist
- [ ] Primary job visible above aesthetic decoration
- [ ] Density matches expertise and scan volume
- [ ] High-risk actions have scope + confirmation
- [ ] Semantic state not color-only
- [ ] Keyboard/focus path tested
- [ ] Mobile workflow is task-adapted, not merely compressed
- [ ] Any AI-generated/inferred state is identified
- [ ] Low-confidence graphic trends are not encoded as hard rules
```

---

# Source index

- **[S1]** W3C — What's New in WCAG 2.2 — https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/
- **[S2]** IBM Carbon — Carbon for AI — https://www.carbondesignsystem.com/building-blocks/foundations/carbon-for-ai
- **[S3]** GitHub Primer — Copilot Accessibility Principles — https://www.primer.style/accessibility/foundations/copilot-principles/
- **[S4]** Microsoft — Responsible AI practices for Azure OpenAI — https://learn.microsoft.com/en-us/azure/foundry/responsible-ai/openai/overview
- **[S5]** Stripe Docs — Dashboard search — https://docs.stripe.com/dashboard/search
- **[S6]** Plaid — Inside the design of Plaid Link — https://plaid.com/blog/inside-link-design/
- **[S7]** Ramp — Products and platform — https://ramp.com/products
- **[S8]** Cloudflare — Security Analytics — https://developers.cloudflare.com/waf/analytics/security-analytics/
- **[S9]** Cloudflare — Custom dashboards — https://developers.cloudflare.com/analytics/custom-dashboards/
- **[S10]** Wiz — Cloud & AI Security Platform — https://www.wiz.io/platform
- **[S11]** GitHub Primer — Accessibility at GitHub — https://primer.style/accessibility/foundations/accessibility-at-github/
- **[S12]** GitHub — Issues — https://github.com/features/issues
- **[S13]** GitHub — Code review — https://github.com/features/code-review
- **[S14]** Datadog — Platform overview — https://www.datadoghq.com/
- **[S15]** Tableau — Build Accessible Dashboards — https://help.tableau.com/current/pro/desktop/en-us/accessibility_dashboards.htm
- **[S16]** Tableau — Best Practices for Effective Dashboards — https://help.tableau.com/current/pro/desktop/en-us/dashboards_best_practices.htm
- **[S17]** Power BI — Dashboard design tips — https://learn.microsoft.com/en-us/power-bi/create-reports/service-dashboards-design-tips
- **[S18]** Power BI — Design reports for accessibility — https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-accessibility-creating-reports
- **[S19]** Looker — Performant dashboard best practices — https://docs.cloud.google.com/looker/docs/best-practices/considerations-when-building-performant-dashboards
- **[S20]** Salesforce — Sales Cloud — https://www.salesforce.com/sales/cloud/
- **[S21]** Salesforce Help — Pipeline Inspection — https://help.salesforce.com/s/articleView?id=sales.pipeline_inspection.htm&language=en_US
- **[S22]** HubSpot — Pipeline management — https://www.hubspot.com/products/crm/pipeline-management
- **[S23]** Notion — Database views, filters, sorts & groups — https://www.notion.com/help/views-filters-and-sorts
- **[S24]** Microsoft Planner — Product overview — https://www.microsoft.com/en-us/microsoft-365/planner/microsoft-planner
- **[S25]** Jira — What is a board? — https://support.atlassian.com/jira-software-cloud/docs/what-is-a-jira-software-board/
- **[S26]** Jira — Board and backlog view settings — https://support.atlassian.com/jira-software-cloud/docs/customize-your-view-of-the-board-and-backlog/
- **[S27]** Asana — Product launches / board, timeline, workload — https://help.asana.com/s/article/product-launches?language=en_US
- **[S28]** monday.com — Work management — https://support.monday.com/hc/en-us/articles/115005305649-Get-started-with-monday-work-management
- **[S29]** SAP Fiori — Design principles — https://experience.sap.com/fiori-design-web/design-principles/
- **[S30]** SAP Fiori — Responsive and adaptive design — https://experience.sap.com/fiori-design-web/explore_category/sap-fiori/
- **[S31]** IBM Carbon — Design system overview — https://www.carbondesignsystem.com/getting-started/designing/overview
- **[S32]** Microsoft Fluent 2 — Accessibility — https://fluent2.microsoft.design/accessibility
- **[S33]** athenahealth — Patient engagement — https://www.athenahealth.com/solutions/athenaone/patient-engagement
- **[S34]** athenahealth — athenaPatient app — https://www.athenahealth.com/solutions/patient-engagement/athenapatient-app
- **[S35]** Jane App — Practice management — https://jane.app/
- **[S36]** SimplePractice — Getting started / portal, scheduling, telehealth — https://support.simplepractice.com/hc/en-us/articles/360020622052-Getting-started-with-SimplePractice-Video-training
- **[S37]** ONC — Usability and Provider Burden — https://healthit.gov/usability-and-provider-burden/
- **[S38]** HHS — Section 504 web/mobile accessibility fact sheet — https://www.hhs.gov/civil-rights/for-individuals/disability/section-504-rehabilitation-act-of-1973/ocr-detailed-504-fact-sheet/index.html
- **[S39]** Shopify — Order analytics — https://help.shopify.com/en/manual/fulfillment/managing-orders/analytics
- **[S40]** Mailchimp — Marketing Dashboard — https://mailchimp.com/help/about-email-analytics/
- **[S41]** Mailchimp — Reports — https://mailchimp.com/help/getting-started-reports/
- **[S42]** Slack — Features — https://slack.com/features
- **[S43]** Slack — Channels — https://slack.com/features/channels
- **[S44]** Slack — Search — https://slack.com/help/articles/202528808-Search-in-Slack
- **[S45]** Microsoft Teams — New chat and channels experience — https://support.microsoft.com/en-us/teams/teams-channels/explore-the-new-chat-and-channels-experience-in-microsoft-teams
- **[S46]** Microsoft Teams — Tabs design — https://learn.microsoft.com/en-us/microsoftteams/platform/tabs/design/tabs
- **[S47]** Salesforce Lightning Design System — Accessibility — https://www.lightningdesignsystem.com/2e1ef8501/p/641741
- **[S48]** Salesforce Lightning Design System — Typography — https://www.lightningdesignsystem.com/2e1ef8501/p/93288f-typography
- **[S49]** IBM Carbon — Accessibility / color contrast — https://www.carbondesignsystem.com/building-blocks/foundations/accessibility/color
- **[S50]** GitHub Primer — Product foundations — https://primer.style/product/getting-started/foundations/

---

## Final synthesis

The most reliable way to design “by industry” is not to memorize visual stereotypes. The engine should predict the **interaction contract** demanded by the domain:

- AI → transparency, control, iteration and recovery.
- FinTech → exactness, state and auditability.
- Cybersecurity → triage, evidence, prioritization and drill-down.
- Developer tools → technical context and keyboard efficiency.
- Analytics → comparison, filtering, explainability and accessible data.
- CRM → records, pipeline, activities and next action.
- Productivity → capture, retrieval and low-friction focus.
- Project management → work objects represented across multiple views.
- Enterprise → role-based complexity with system-wide consistency.
- Healthcare → safety, privacy, accessibility and role-separated workflows.
- E-commerce → commerce objects and lifecycle states.
- Marketing → create, target, launch and measure.
- Collaboration → streams, triage, context and search.

After that contract is satisfied, brand personality can shape saturation, radius, typography flavor, illustration and motion. That ordering prevents an AI from producing interfaces that merely *look like* an industry while violating the way people in that industry actually work.
