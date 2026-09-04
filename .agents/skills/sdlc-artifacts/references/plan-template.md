# Plan artifact guide

Use the repository root `plan.md` only after both `intent.md` and `spec.md` are accepted.

Recommended structure:

```markdown
---
status: draft
accepted_by:
accepted_at:
---

# Implementation Plan

## Summary
## Files and components that change
## Order of work
## Tests and proof
## Risks and mitigations
## Rollback or recovery
## Open questions
```

Make the plan executable by an agent that has the repository and accepted artifacts but no prior conversation context.
