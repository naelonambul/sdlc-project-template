# Hook Implementations

Put fast deterministic guardrails here when the repository needs them.

Good candidates include:

- protected-path checks;
- secret or credential checks;
- narrowly scoped formatting/lint checks;
- prevention of unsafe repository mutations.

Keep shared enforcement logic agent-neutral. Agent-specific hook configuration should call these scripts rather than duplicate policy.

Do not put long-running full test suites or routine human approval prompts on every edit. Those belong at a later gate such as commit, pull request, or deployment.
