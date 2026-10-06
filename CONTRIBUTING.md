# Contributing

This repository is a production instruction system, not a collection of design tips. Changes should improve agent decisions without unnecessarily increasing context size.

## Contribution principles

1. **Research is evidence, not an instruction.** Do not copy findings directly into `SKILL.md`.
2. **Every production rule must change a decision.** Remove advice that is merely descriptive or obvious.
3. **Preserve context.** Conditional findings must remain conditional.
4. **Higher-priority constraints win.** Accessibility, safety, task completion, product requirements, and data integrity outrank visual preference.
5. **Avoid aesthetic universalism.** No industry, brand adjective, or product category should automatically imply a palette, font, radius, gradient, or layout style.
6. **Prefer causes over symptoms.** Audit rules should direct agents toward structural fixes before decorative patches.
7. **Keep `SKILL.md` compact.** Move rationale, examples, edge cases, and citations into `references/` or `research/`.
8. **Maintain traceability.** Update `references/source-map.md` when a material rule changes.

## Where changes belong

| Change | Location |
|---|---|
| New evidence / long-form research | `research/` |
| Domain heuristics, decision trees, exceptions | `references/` |
| High-value cross-domain production rule | `SKILL.md` |
| Before-design validation | `checklists/pre-design.md` |
| Completion / release validation | `checklists/final-audit.md` |
| Demonstration of rule application | `examples/` |

## Rule review checklist

Before adding or changing a rule, ask:

- Does this produce a concrete design decision?
- Is the evidence strong enough for the strength of the wording?
- Is this actually context-dependent?
- Does it duplicate an existing rule?
- Could it conflict with accessibility, safety, usability, or product requirements?
- Is it better expressed as an exception or decision tree?
- Does the agent need this in `SKILL.md`, or only when a specific reference is opened?

## Benchmark claims

Do not add measured performance claims without a reproducible benchmark. Record at minimum:

- model/agent and version;
- prompt and task set;
- with-skill vs without-skill condition;
- evaluation rubric;
- evaluator protocol;
- sample size;
- raw or auditable results;
- known limitations.

Until such a benchmark exists, keep the README statement that no formal benchmark has been run.
