---
name: repository-quality
description: Discover and follow the repository-native validation workflow. Use during implementation, debugging, review, or completion checks when build, test, lint, format-check, type-check, or other quality gates must be identified or run without replacing the project's established tooling.
---

# Repository Quality

Use the repository's own quality system rather than an agent-preferred substitute.

## Discover canonical validation

1. Read `AGENTS.md` first.
2. Inspect repository-native command surfaces such as package scripts, Makefiles, task runners, build manifests, CI workflows, and existing scripts.
3. Prefer already-established build, test, lint, format-check, type-check, and project-specific verification commands.
4. When the application stack first establishes canonical commands, record them in `AGENTS.md` and, when useful, wrap multi-command validation in deterministic scripts under `scripts/checks/`.

## Preserve the checks

- Do not introduce a different formatter, linter, test framework, or type checker merely because you prefer it.
- Do not disable, weaken, skip, delete, or rewrite a failing check merely to make validation pass.
- Do not silently change test expectations to match broken implementation behavior.
- Change validation configuration only when the task actually requires that configuration change and the accepted artifacts authorize it.

## Validate proportionally

- During iteration, run the smallest relevant checks that provide fast feedback.
- Before completion, run every applicable canonical check required by `AGENTS.md`, the accepted plan, or CI policy.
- Treat visual or runtime verification as part of validation when the accepted plan requires it.
- If no meaningful validation exists yet, state that fact instead of inventing unrelated tooling.

## Report evidence

Report the exact commands or checks run, whether they passed, and any relevant limitation. Do not claim a check ran when it did not.
