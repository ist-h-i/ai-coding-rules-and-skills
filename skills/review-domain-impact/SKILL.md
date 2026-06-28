---
name: review-domain-impact
description: Review whether a code change introduces, modifies, or removes business behavior, domain rules, workflow responsibility, state semantics, operational meaning, reporting meaning, notification timing, permissions, approval/completion criteria, or generated text used for business judgment. Use before technical review when domain impact may exist.
---

# Domain Impact Review

## Goal

Determine what business reality the change modifies and whether that domain change is explicit, authorized, and correctly represented.

## Use when

A change affects or may affect:
- business workflow,
- business rules,
- permissions or responsibility,
- status/state semantics,
- approval, rejection, completion, or escalation criteria,
- reporting, metrics, evaluation, or billing meaning,
- notifications with operational meaning,
- user-visible behavior that changes work decisions,
- data meaning, not only data shape,
- generated text used for business judgment,
- automation that replaces or changes a human step.

## Do not use when

- The change is purely mechanical formatting.
- The change is internal refactoring with verified unchanged behavior and no domain meaning change.
- The change only improves local readability.
- Domain behavior is already explicitly unchanged and verified.

## Process

1. Identify the domain object.

```text
Business object:
Business action:
Business state:
Business actor:
Business rule:
Business outcome:
```

2. Compare before and after business behavior.

```text
Before:
After:
Changed business meaning:
```

3. Classify the change.
   - no domain impact,
   - domain-preserving implementation change,
   - explicit domain change,
   - implicit domain change,
   - unauthorized domain change,
   - insufficient domain evidence.

4. Check evidence.
   - issue or requirement,
   - spec or docs,
   - user request,
   - ADR or decision record,
   - tests,
   - production behavior.

5. Identify responsibility shift.
   - who gains responsibility,
   - who loses responsibility,
   - who gets new information,
   - who may make a different decision because of the change.

6. Decide required action.
   - pass,
   - pass with domain note,
   - request domain clarification,
   - require product/domain owner approval,
   - require ADR/domain decision record,
   - block.

## Output

```text
Domain impact decision:
- Classification:
- Gate status: pass | pass with note | fail | insufficient evidence
- Business object:
- Business rule changed:
- Workflow changed:
- Responsibility changed:
- Evidence:
- Missing evidence:
- Required fix:
- Required approval:
- Residual domain risk:
```

## Exit criteria

- Domain impact classification is explicit.
- Business before/after is documented when impact exists.
- Missing owner approval or domain evidence is visible.
- A PR with possible domain impact is not approved by logic/design review alone.

## Failure modes

| Failure | Correction |
|---|---|
| Treating validation changes as logic only | Check whether acceptance criteria changed. |
| Treating enum/status changes as type-only | Check state semantics and operational meaning. |
| Treating notification changes as UX-only | Check responsibility and intervention timing. |
| Mixing domain with architecture | Decide what business truth changes before deciding system boundaries. |
