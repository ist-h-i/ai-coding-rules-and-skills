---
name: mr-readme-generation
description: Create or update an MR/PR README, GitHub PR explanation, or durable change-context document that preserves MR/PR概要, 仕様理解固定, impact, risks, rollback, domain meaning, architecture decisions, design rationale, verification, and notes for 後続AI再利用 and 人間レビュー準備. Use when a user asks for MR README作成, GitHub PR README, PR explanation, specification understanding record, or reusable review documentation, not when they only want approve/request changes.
---

# MR/PR README Generation

## Goal

Turn a GitLab Merge Request, GitHub Pull Request, branch, commit, or concrete change into a durable README that fixes shared understanding for humans and future AI coding agents.

The output explains what changed, why it matters, how to review it, how to roll it back, and which assumptions remain. It is not a defect hunt or merge approval gate.

## Use when

- Creating or updating a change-specific MR/PR README before or during human review.
- The user asks for MR explanation, MR README, GitHub PR README, PR explanation, review preparation, or specification understanding.
- The user needs durable change-context documentation, including PR explanation or reusable review documentation.
- Future agents should reuse context from the MR/PR without rereading the full discussion.
- Domain meaning, architecture rationale, rollback, or risk needs to be preserved with the change.

## Do not use when

- The user only wants approve, request changes, block, or merge readiness. Use `review-router`.
- No diff, MR, PR, branch, commit, or concrete change target is available.
- The user needs the next executable task prompt only. Use `handoff-generation`.
- The decision itself needs durable ADR treatment before the MR/PR README. Use `adr-review` first.

## Inputs

- MR/PR URL, title, description, branch name, issue, or ticket.
- Diff, changed files, commit messages, and generated artifacts.
- Existing README, docs, ADRs, schemas, tests, and project instructions.
- Verification evidence: test output, CI status, manual checks, or explicit missing checks.

## Process

1. Locate the output document.
   - Default to `docs/mr/<branch-or-mr>.md` for merge requests.
   - Default to `docs/pr/<branch-or-pr>.md` for pull requests.
   - Use `docs/change-context/<branch-or-change>.md` when the review target is not tied to an MR/PR.
   - Prefer an existing project convention or explicit user path if present.

2. Read enough evidence to explain the change.
   - MR/PR description or issue,
   - diff and changed files,
   - nearby docs and tests,
   - relevant ADRs or architecture notes,
   - validation evidence or missing validation.

3. Separate evidence status for important claims.
   - `Verified`: directly observed in code, docs, tests, logs, CI, or user input.
   - `Supported`: indirectly backed but not fully proven.
   - `Hypothesis`: plausible but unverified.
   - `Unknown`: unavailable, ambiguous, or not inspected.
   - `Falsified`: contradicted by evidence.

4. Write for review understanding.
   - Explain the intended behavior and boundaries.
   - Identify what a human reviewer should confirm as shared specification.
   - Do not convert optional review ideas into required fixes.

5. Preserve domain and architecture context.
   - For domain impact, record business object, rule, actor, state meaning, responsibility, and decision impact.
   - For architecture choices, record decision, alternatives, constraints, reversibility, and ADR status: none, new ADR candidate, or existing ADR update candidate.

6. Preserve operational context.
   - Record risks, mitigations, rollback path, verification, and unverified areas.
   - Mark missing evidence instead of filling gaps with guesses.

7. Route out when needed.
   - Use `review-router` if a merge decision or findings are requested.
   - Use `adr-review` if a hard-to-reverse architecture decision needs a durable ADR.
   - Use `handoff-generation` if the output must become a next-agent task.

## MR/PR README template

```markdown
# MR/PR README: <title>

## MR/PR概要

- Goal:
- User-visible or operator-visible change:
- Non-goals:
- Evidence status:

## 背景 / 要件

- Source request / issue:
- Problem:
- Constraints:
- Important assumptions:

## 変更内容マップ

- Changed areas:
- Key files:
- Data / API / workflow changes:
- Generated or migration artifacts:

## 影響範囲

- Users / roles:
- Systems / modules:
- Data and state:
- Operations / monitoring:
- Compatibility:

## リスクと軽減策

- Risk:
- Impact:
- Mitigation:
- Evidence:
- Remaining uncertainty:

## 切り戻し方針

- Rollback trigger:
- Rollback steps:
- Data or config considerations:
- Verification after rollback:

## ドメイン領域 / 業務意味

- Business object:
- Business rule:
- Business actor:
- Business state:
- Responsibility shift:
- Decision impact for reviewers:

## アーキテクチャー判断ログ

- Decision:
- Alternatives considered:
- Constraints:
- Reversibility:
- ADR status: none | new ADR candidate | existing ADR update candidate

## 設計思想 / alternatives

- Design intent:
- Why this approach:
- Rejected alternatives:
- Tradeoffs:

## 検証結果 / 未検証

- Verified:
- Supported:
- Hypothesis:
- Unknown:
- Falsified:

## 後続AI向け再利用メモ

- Stable context to reuse:
- Do not assume:
- Files or docs to read first:
- Follow-up skills to invoke:

## 人間レビューで固定したい理解

- Specification points to confirm:
- Domain points to confirm:
- Architecture points to confirm:
- Open questions:
```

## Output

```text
MR/PR README:
- Path:
- Created or updated:
- Evidence reviewed:
- Evidence gaps:
- ADR status:
- Review decision emitted: no
- Follow-up skills:
```

## Exit criteria

- The README exists at the selected path or the exact intended path is reported.
- Each required template section is present, even if some entries are `Unknown`.
- Important claims have evidence status.
- Review approval language is absent unless delegated to `review-router`.
- Future agents can identify changed intent, risks, rollback, domain meaning, and architecture rationale without rereading the full MR/PR conversation.

## Failure modes

| Failure | Correction |
|---|---|
| Treating the README as a code review | Explain specification and context; route findings or merge decisions to `review-router`. |
| Hiding missing evidence | Mark `Unknown` and state the next check. |
| Recording architecture rationale only in chat | Put durable rationale in the MR/PR README and invoke `adr-review` when the decision is hard to reverse. |
| Writing only a human summary | Include future-agent reuse notes, evidence status, rollback, and domain or architecture meaning. |
| Duplicating handoff instructions | Keep reusable MR/PR context here; use `handoff-generation` for the next executable task. |
