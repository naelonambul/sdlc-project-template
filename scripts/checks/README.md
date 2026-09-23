# Checks

Add project-native deterministic validation here when the application stack exists.

Guidelines:

- Prefer one canonical aggregate entry point when practical.
- Exit non-zero on failure.
- Keep output actionable and reproducible.
- Reuse existing project tools rather than introducing competing linters or formatters.
- Never weaken a check merely to make an agent change pass.
- Put expensive full-suite checks in commit/PR/CI paths rather than per-edit hooks.
