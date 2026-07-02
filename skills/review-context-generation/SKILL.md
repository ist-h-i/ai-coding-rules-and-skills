---
name: review-context-generation
description: Generate and maintain a durable project review context file with evidence-status-labeled claims for repeated review routing, output-quality review, adversarial review, and final merge decisions.
---

# Review Context Generation

## Goal

Create or update reusable review context so repeated PR reviews do not rediscover personas, output contracts, critical workflows, accepted risks, known issues, and project constraints from scratch.

## Use when

- Initial repository orientation or review setup is expected to support repeated MR/PR reviews.
- `review-output-quality` or `review-adversarial-risk` needs project context.
- Review noise is recurring because known issues, accepted risks, output contracts, or critical workflows are not documented.
- A project overlay exists and should be referenced from review workflows without replacing it.

## Do not use when

- The task only needs transient progress tracking. Use `planning-with-files`.
- The user only needs a final merge decision for one already-scoped review. Use `review-router` and required gates.
- The project wants permanent agent rules. Reference or update project overlay rules such as `AGENTS.project.md` instead.
- You would need to ask the user to fill a blank form from scratch.

## Default path

Prefer:

```text
docs/ai/review-context.md
```

If the project prefers hidden agent files, use:

```text
.agent/review-context.md
```

If the context belongs in permanent project rules, reference or update:

```text
AGENTS.project.md
```

## Evidence statuses

Use these statuses for important claims:

| Status | Meaning |
|---|---|
| `Verified` | Directly observed in repo files, docs, tests, runtime output, command output, or user input. |
| `Supported` | Backed by indirect evidence but not fully proven. |
| `Hypothesis` | Plausible inference that needs confirmation before being used as fact. |
| `Human-confirmed` | Confirmed by a human owner in the current or prior documented review context. |
| `Unknown` | Not inspected, unavailable, ambiguous, or outside current evidence. |

## Process

1. Inspect repository evidence first.
   - README and product docs,
   - project overlay rules,
   - docs, ADRs, schemas, examples, tests, generated artifacts, screenshots, or workflows,
   - review history when available.

2. Draft candidate context.
   - product / project identity,
   - project hero or product promise,
   - primary users / personas,
   - human and system / AI consumers,
   - critical workflows,
   - output quality standards,
   - domain review context,
   - architecture review context,
   - adversarial review context,
   - assets to protect,
   - threat / misuse model,
   - accepted risks,
   - known issues not to re-report,
   - review noise-control rules,
   - verification policy,
   - update triggers.

3. Label each important claim with evidence status and source.
   - Do not treat AI-inferred persona, project promise, accepted risk, or threat model as fact.
   - Mark unsupported items as `Hypothesis` or `Unknown`.

4. Ask the user only for missing or high-impact human judgment when needed.
   - persona or audience,
   - accepted risks,
   - assets to protect,
   - critical workflows,
   - known issues not to re-report,
   - safety boundaries.

5. Save or update the context file.
   - Preserve existing human-confirmed content unless contradicted by newer evidence.
   - Keep task progress out of this file.
   - Add update triggers so future agents know when context may be stale.

6. Wire consumers.
   - `review-router`, `review-output-quality`, `review-adversarial-risk`, and `review-final-merge-gate` should read this context when available.
   - `planning-with-files` remains responsible for task progress.

## Output

```text
Review context generation:
- Path:
- Created or updated:
- Facts found from repo:
- Human-confirmed items:
- Hypotheses needing confirmation:
- Unknowns:
- Review consumers:
- Update triggers:
- Next review skills that should read this file:
```

## Exit criteria

- A reusable review context file is created or updated.
- Important claims have evidence status and source.
- Human-provided context is requested only for high-impact gaps.
- Output quality and adversarial review can rely on the context instead of repeating repo-wide discovery.
- Known issues and accepted risks can suppress recurring review noise.
- Task progress is not stored in review context.

## Failure modes

| Failure | Correction |
|---|---|
| Asking the user to fill a blank template | Inspect repo evidence first and ask only targeted questions. |
| Treating inferred persona or threat model as fact | Mark it `Hypothesis` or `Unknown` until human-confirmed. |
| Replacing project overlay rules | Reference the overlay; update it only when the content is a durable project rule. |
| Storing task progress here | Move progress to `planning-with-files`. |
| Letting context go stale silently | Add update triggers and evidence sources. |
