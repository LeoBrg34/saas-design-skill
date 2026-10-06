# Brand Personality Decision Reference

Use this file when a brief contains traits such as premium, secure, friendly, technical, playful, enterprise, futuristic, minimalist, trustworthy, or bold.

## Never map adjective -> visual cliché directly

Do not use rules such as `blue = trust`, `black = luxury`, `rounded = friendly`, or `dark = technical` as universal truths. Meaning depends on product, audience, market conventions, culture, task, and neighboring design signals.

Normalize traits into control axes:

```text
warmth         distant <-> approachable
competence     casual <-> expert/precise
status         utilitarian <-> premium/refined
energy         calm <-> dynamic/playful
novelty        conventional <-> innovative/futuristic
technicality   general-user <-> developer/technical
risk           low-stakes <-> regulated/secure/high-stakes
restraint      expressive <-> controlled/minimal
```

## Trait roles

Choose at most **2 drivers**. Other traits become:
- **modifier** — expression without rewriting foundations;
- **guardrail** — caps decoration/ambiguity when risk or seriousness is high.

Do not average conflicting traits across every property.

Examples:

| Traits | Split |
|---|---|
| friendly + enterprise | enterprise owns structure/density; friendly owns copy, geometry, illustration, micro-moments |
| premium + playful | premium owns palette restraint/type craft; playful owns one accent/illustration channel |
| technical + approachable | technical owns data/code/layout; approachable owns explanation, disclosure, error/help states |
| serious + innovative | serious sets palette/motion ceiling; innovation appears in composition/visualization/accent |
| secure + friendly | secure owns state/evidence/consequence; friendly owns onboarding/support tone |
| enterprise + minimalist | enterprise preserves information; minimalist reduces noise/container variety |
| futuristic + secure | secure owns product shell; futuristic treatment stays mostly in marketing/data art |

When unresolved: `accessibility > task performance > desired perception > audience expectations > category conventions > novelty`.

## Expression channels

Structure is primarily determined by task. Brand can modify:
- saturation and color complexity;
- type voice in headings/display;
- radius as a secondary cue;
- border/elevation restraint;
- illustration and imagery;
- empty states/onboarding;
- motion character;
- marketing composition;
- copy tone.

High-risk traits cap saturation, motion, translucency, ambiguity, and destructive-flow playfulness.

## Marketing vs product

Use different expression intensity:

```text
marketing          base + 1 or 2
product            base
critical workflow  base - 1
```

Critical workflows include permissions, billing, deletion, security incident, recovery, compliance, and destructive export/data operations.

## Credibility requires proof

For `trustworthy / secure / enterprise / technical`, style alone is insufficient. Add the relevant product evidence:
- trustworthy -> verifiable claims, reliability, clear status/support;
- secure -> permissions, audit trail, architecture/encryption detail, consequence clarity;
- enterprise -> governance, roles, integrations, scalability/admin visibility;
- technical -> APIs, code/examples, diagrams, metrics, inspectability;
- premium -> consistency, craft, precise typography, restrained noise, strong art direction.

A shield icon, dark palette, or generic “trusted by” strip is not a trust system.

## Rejection checks

Revise if:
- every trait is expressed through color;
- novelty changes core navigation without task benefit;
- friendliness weakens warnings/risk clarity;
- minimalism deletes needed labels or controls;
- premium creates low contrast/thin text;
- futuristic styling depends on illegible translucency;
- playful behavior enters destructive/security/billing/recovery moments;
- developer-first uses decorative code styling but poor real code affordances.

## Research anchors

Primary evidence: `research/brand-personality.md` §§ 0–4, 7–8, 10, 13, 16–18. Related: `research/color-intelligence.md` § 9; `research/typography.md` § 4; `research/design-by-industry.md` Cross-industry rules and decision engine.
