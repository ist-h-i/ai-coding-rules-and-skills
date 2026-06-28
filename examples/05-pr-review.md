# Example: PR review

## Request

```text
Review this PR and tell me whether to merge.
```

## Workflow

Use:

```text
review-router → required gates → review-final-merge-gate
```

## Expected output

```text
Review route:
- Required gates: review-automated-gate, review-ai-quality, review-final-merge-gate
- Optional gates: evidence-ledger
- Skipped gates: review-domain-impact, adr-review, risk-gate

Decision:
- request changes

Gate summary:
- Automated: focused tests ran; large-file benchmark not run.
- AI quality: one major correctness finding.
- Domain: skipped; CSV escaping does not change business meaning.

Required fixes:
- [major] src/export.ts:42 — CSV escaping does not handle quotes.
  Evidence: Existing tests cover commas but not double quotes; implementation only wraps fields.
  Required fix: Escape double quotes according to CSV rules and add a regression test.

Suggestions:
- ...

Evidence reviewed:
- diff
- nearby tests
- focused test command output

Residual risk:
- Large-file performance was not benchmarked.
```
