# Specification artifact guide

Use the repository root `spec.md` only after `intent.md` is accepted.

Recommended structure:

```markdown
---
status: draft
accepted_by:
accepted_at:
---

# Specification

## Summary
## Requirements
### Functional
### Non-functional
## User experience and behavior
## Architecture and design
## Interfaces, data, and dependencies
## Security, privacy, and policy constraints
## Risks and concerns
## Acceptance criteria
## Open questions
```

Make requirements testable where practical. Preserve the accepted intent and flag contradictions instead of resolving them silently.
