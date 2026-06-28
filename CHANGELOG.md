# Changelog

## v2.1.0

Purpose: split PR/code review responsibility so automated checks, AI quality review, domain impact, and final merge decisions are explicit.

Changes:

- Added `review-router` for selecting required review gates.
- Added `review-automated-gate` for formatter/linter/typecheck/build/test/CI evidence.
- Added `review-ai-quality` for AI-assessable implementation review without final approval.
- Added `review-domain-impact` for business rules, state semantics, workflow, responsibility, and operational meaning.
- Added `review-final-merge-gate` as the only gate that emits final merge decisions.
- Converted `code-review-quality` into a compatibility adapter for legacy review prompts.
- Updated README, usage docs, workflow examples, and routing tables to use the new review model.

## v2.0.0

Purpose: raise the set from a usable v1 baseline to a personal/internal-use target of 95+ across kernel design, skill separation, safety, verification, review, evidence, and handoff quality.

Changes:

- Added kernel `Safety and External Effects` section.
- Added kernel minimal skill routing table.
- Added `risk-gate` skill.
- Added `controlled-implementation` skill.
- Kept v1 skill names where possible to reduce migration friction.
- Strengthened all skills with exit criteria, output contracts, and failure modes.
- Added Japanese usage guide.
- Added workflow examples.
- Added quality rubric.
- Added project overlay template.
