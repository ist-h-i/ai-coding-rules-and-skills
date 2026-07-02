# Review Context Template

Use this file as durable project review context for repeated PR, diff, generated-output, output-quality, and adversarial-risk reviews.

This file is not task progress. Use `planning-with-files` for task state.

## Evidence Status Key

| Status | Meaning |
|---|---|
| `Verified` | Directly observed in repo files, docs, tests, runtime output, command output, or user input. |
| `Supported` | Backed by indirect evidence but not fully proven. |
| `Hypothesis` | Plausible inference that needs confirmation before being used as fact. |
| `Human-confirmed` | Confirmed by a human owner in the current or prior documented review context. |
| `Unknown` | Not inspected, unavailable, ambiguous, or outside current evidence. |

## Product / Project Identity

| Claim | Status | Source |
|---|---|---|
| Product / domain: | Unknown |  |
| Project promise: | Unknown |  |
| Non-goals: | Unknown |  |

## Review Consumers

| Consumer | Output or workflow | Status | Source |
|---|---|---|---|
| Human users: |  | Unknown |  |
| Operators / reviewers: |  | Unknown |  |
| System consumers: |  | Unknown |  |
| AI consumers: |  | Unknown |  |

## Critical Workflows

| Workflow | Why it matters | Status | Source |
|---|---|---|---|
|  |  | Unknown |  |

## Output Quality Standards

| Medium / output | Contract or standard | Status | Source |
|---|---|---|---|
| UI / visual output: |  | Unknown |  |
| Reports / docs / generated text: |  | Unknown |  |
| CLI output: |  | Unknown |  |
| API / structured output: |  | Unknown |  |
| AI-facing output: |  | Unknown |  |

## Domain Review Context

| Domain rule or term | Review impact | Status | Source |
|---|---|---|---|
|  |  | Unknown |  |

## Architecture Review Context

| Boundary or contract | Review impact | Status | Source |
|---|---|---|---|
|  |  | Unknown |  |

## Adversarial Review Context

| Asset / actor / misuse path | Safety boundary or accepted posture | Status | Source |
|---|---|---|---|
| Assets to protect: |  | Unknown |  |
| Threat / misuse model: |  | Unknown |  |
| Critical blast-radius paths: |  | Unknown |  |

## Accepted Risks

| Risk | Acceptance rationale | Expiration / owner | Status | Source |
|---|---|---|---|---|
|  |  |  | Unknown |  |

## Known Issues Not To Re-report

| Issue | Suppression condition | Re-report when | Status | Source |
|---|---|---|---|---|
|  |  |  | Unknown |  |

## Review Noise-Control Rules

| Rule | Applies to | Status | Source |
|---|---|---|---|
| Do not invent persona, brand, product promise, accepted risk, or threat model. | output quality and adversarial review | Verified | `skills/review-output-quality/SKILL.md`, `skills/review-adversarial-risk/SKILL.md` |
| Treat missing required context as `insufficient evidence`. | all review gates | Verified | `skills/review-router/SKILL.md`, `skills/review-final-merge-gate/SKILL.md` |

## Verification Policy

| Change type | Required evidence | Status | Source |
|---|---|---|---|
| Behavior change: | focused test, integration test, or runtime check tied to acceptance criteria | Supported | `skills/test-first-verification/SKILL.md` |
| Refactor: | evidence that existing behavior is preserved | Supported | `skills/test-first-verification/SKILL.md` |
| Output change: | screenshot, rendered artifact, sample response, generated text, schema, or output contract | Supported | `skills/review-output-quality/SKILL.md` |
| Risky or external action: | explicit approval and risk-gate evidence | Supported | `skills/risk-gate/SKILL.md` |

## Update Triggers

Update this context when:

- project identity, users, or product promise changes,
- output contracts or design systems change,
- critical workflows, assets, or safety boundaries change,
- accepted risks or known suppressed issues change,
- architecture boundaries or public contracts change,
- review gates repeatedly ask for the same missing context.
