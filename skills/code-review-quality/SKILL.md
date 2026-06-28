---
name: code-review-quality
description: Compatibility adapter for legacy code review requests. Use when a user asks for code-review-quality, PR review, diff review, commit review, generated code review, or merge readiness; route the review through review-router, required review gates, and review-final-merge-gate instead of performing every review concern in one skill.
---

# Code Review Quality Adapter

## Goal

Preserve the old `code-review-quality` entry point while delegating real review work to focused gates.

## Use when

- Reviewing a PR, diff, commit, patch, or generated code.
- Deciding whether a change is safe to merge.
- A prompt or project instruction explicitly names `code-review-quality`.
- Older workflow docs or agents still call this skill.

## Do not use when

- The user only asks for a non-evaluative summary.
- No code, diff, or concrete design artifact is available to review.
- A narrower review gate has already been selected.

## Process

1. Invoke `review-router`.

2. Run only the required gates selected by the route.
   - Use `review-domain-impact` first when domain behavior may change.
   - Use `adr-review` for hard-to-reverse architecture or decision-record needs.
   - Use `risk-gate` before risky actions.
   - Use `review-automated-gate` for command and CI evidence.
   - Use `review-ai-quality` for implementation quality findings.
   - Use `evidence-ledger` when claims need evidence classification.

3. Use `review-final-merge-gate` for the only final merge decision.

4. If a required gate cannot be run, report `insufficient evidence` through the final gate instead of silently approving.

## Gate map

| Concern | Gate |
|---|---|
| Format, lint, typecheck, build, tests, CI | `review-automated-gate` |
| Correctness, edge cases, tests, API/design boundary, maintainability, scope | `review-ai-quality` |
| Business rules, workflow, state semantics, responsibility, operational meaning | `review-domain-impact` |
| Architecture decision memory | `adr-review` |
| Destructive, external, production, auth, secret, dependency, infra action | `risk-gate` |
| Unsupported readiness/performance/security/correctness claims | `evidence-ledger` |
| Merge decision | `review-final-merge-gate` |

## Output

```text
Review route:
- ...

Gate results:
- ...

Decision:
- ...

Required fixes:
- ...

Evidence reviewed:
- ...

Residual risk:
- ...
```

## Exit criteria

- The review route is explicit.
- Required gates are run or marked as missing evidence.
- Final decision comes from `review-final-merge-gate`.
- Domain and risk gates are not hidden inside technical review.

## Failure modes

| Failure | Correction |
|---|---|
| Recreating the old all-in-one review | Route to focused gates. |
| Approving from AI quality findings alone | Use `review-final-merge-gate`. |
| Missing domain impact | Run `review-domain-impact` before technical gates when domain meaning may change. |
| Treating green CI as approval | Keep mechanical evidence in `review-automated-gate` and merge decision in final gate. |
