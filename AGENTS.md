# Repository Agent Instructions

Keep this file short. It contains repository-wide invariants that are relevant in nearly every agent session. Put detailed or conditional procedures in `.agents/skills/`.

## Authority

1. Explicit decisions from the human owner are final.
2. This `AGENTS.md` defines repository operating rules. It is guidance, not the enforcement boundary: hard rules are enforced by `scripts/repo.py`, tests, and CI, and some agents (for example subagents that omit project instructions) never read this file.
3. The root `intent.md` and `spec.md` are the durable product baseline. Work happens in change packets, `changes/<id>/`, each with its own plan; there is no root plan. See `changes/README.md`.
4. Approved upstream artifacts constrain downstream ones. Never silently resolve a contradiction by overriding the upstream artifact; surface the conflict to the human owner.
5. Repository source, tests, and configuration are authoritative for the current implemented state. Approved change packets authorize intended changes.
6. `REVIEW.md` defines review policy, not product intent.
7. `docs/` is supporting/reference/history material. If `prototype/` exists, it is supporting discovery material. Neither overrides the baseline or an approved change.

## SDLC gates

- Run `python3 scripts/repo.py status --change <id>`. It computes each change's stage, freshness, approval and readiness from repository facts; never store or assert those states by hand.
- Artifacts are approved in order `intent -> spec -> plan`, only by the human owner, via digest-bound claims in `change.json`. Never infer approval from file contents, Git state, or your own judgment.
- Do not change anything outside the packet until status reports `readiness=ready`, and stay inside the change's declared `write_scope`.
- If implementation requires a material departure from the approved plan, stop, revise the plan, and obtain a fresh owner approval.
- Local approval is `unverified`: it detects stale approvals, not identity.

Use the `sdlc-artifacts` skill whenever creating, revising, approving, or closing a change.

## Working rules

- Use repository-local skills from `.agents/skills/` when their trigger applies.
- Treat Context7, Serena, and Graphify as optional capabilities, not mandatory gates.
- When the product stack becomes concrete, use the `repository-quality` skill to discover existing quality tooling or bootstrap a minimal stack-appropriate setup when it is missing.
- Do not force-push, rewrite history, hard-reset shared work, or delete unrelated changes unless explicitly instructed.
- Do not weaken tests, lint rules, type checks, security checks, or configuration merely to make validation pass.
- Do not commit tool caches or generated analysis metadata. The default `.gitignore` excludes known Serena and Graphify outputs.
- Prefer repository-native commands and conventions over agent preferences.
- Keep agent-specific adapters thin. Put shared policy in this file, skills, or deterministic scripts instead of duplicating it per agent.

## Canonical project commands

These are intentionally unset in the generic template. Once the product stack is established, use the `repository-quality` skill to discover or bootstrap the repository-native quality toolchain and replace the applicable `not configured` entries with exact commands. Use `not applicable` only for genuinely irrelevant gates.

- Build: not configured
- Test: not configured
- Lint: not configured
- Format check: not configured
- Type check: not configured

## Definition of done

Before reporting implementation complete:

- Confirm the approved change plan is satisfied or explicitly revised and re-approved.
- Run the applicable repository-native validation.
- If an optional self-contained workspace changed, run its applicable local quality checks too.
- Report the exact validation performed and its result.
- Review the change against `REVIEW.md`.
- Confirm no generated analysis metadata, credentials, or unrelated changes are included.
