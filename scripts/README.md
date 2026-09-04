# Deterministic Scripts

Use this directory for repository-controlled, deterministic behavior.

- `checks/`: build, test, lint, format, type-check, policy, and other repeatable validations.
- `hooks/`: fast agent-neutral guardrail implementations that agent-specific hook/config layers may call.

Do not add placeholder scripts that pretend to validate a stack that does not exist. Once the project has real canonical commands, prefer stable wrappers with deterministic exit codes so both humans, agents, hooks, and CI can call the same implementation.
