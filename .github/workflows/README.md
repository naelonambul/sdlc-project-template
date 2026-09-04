# Workflows

Add stack-specific GitHub Actions workflows only after the project has real canonical validation or deployment commands.

Prefer CI that calls the same deterministic scripts used locally instead of duplicating validation logic in YAML.

Typical progression:

1. build/test/lint/type/format checks;
2. policy or security checks;
3. agent-configuration evals when those have real cases;
4. deployment and approval gates when the project has deployment targets.

Do not add a fake green workflow merely to populate this directory.
