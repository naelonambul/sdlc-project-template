# Repository Agent Instructions

Keep this file short. It contains repository-wide invariants that are relevant in nearly every agent session. Put detailed or conditional procedures in `.agents/skills/`.

## Authority

1. Explicit decisions from the human owner are final.
2. This `AGENTS.md` defines repository operating rules and SDLC gates.
3. Accepted root artifacts form the active authority chain: `intent.md` -> `spec.md` -> `plan.md`.
4. Upstream accepted artifacts constrain downstream artifacts. Never silently resolve a contradiction by overriding the upstream artifact; surface the conflict to the human owner.
5. Repository source, tests, and configuration are authoritative for the current implemented state. Accepted artifacts authorize the intended change.
6. `REVIEW.md` defines review policy, not product intent.
7. `docs/` is supporting/reference/history material and never overrides accepted root artifacts.

## SDLC gates

- Root artifacts use `status: not-started`, `status: draft`, or `status: accepted`.
- Never infer human acceptance from file contents, Git state, or an agent's own judgment.
- Change an artifact to `accepted` only after the human owner explicitly approves it.
- Do not start `spec.md` until `intent.md` is accepted.
- Do not start `plan.md` until `spec.md` is accepted.
- Do not implement until `plan.md` is accepted.
- During later stages, continue reading all accepted upstream artifacts.
- If implementation requires a material departure from the accepted plan, stop, revise `plan.md`, and obtain human acceptance before continuing.

Use the `sdlc-artifacts` skill whenever creating, revising, or checking readiness of root artifacts.

## Working rules

- Use repository-local skills from `.agents/skills/` when their trigger applies.
- Treat Context7, Serena, and Graphify as optional capabilities, not mandatory gates.
- Do not force-push, rewrite history, hard-reset shared work, or delete unrelated changes unless explicitly instructed.
- Do not weaken tests, lint rules, type checks, security checks, or configuration merely to make validation pass.
- Do not commit tool caches or generated analysis metadata. The default `.gitignore` excludes known Serena and Graphify outputs.
- Prefer repository-native commands and conventions over agent preferences.
- Keep agent-specific adapters thin. Put shared policy in this file, skills, or deterministic scripts instead of duplicating it per agent.

## Canonical project commands

These are intentionally unset in the generic template. Once the application stack is established, replace `not configured` with the repository-native commands.

- Build: not configured
- Test: not configured
- Lint: not configured
- Format check: not configured
- Type check: not configured

## Definition of done

Before reporting implementation complete:

- Confirm the accepted plan is satisfied or explicitly revised.
- Run the applicable repository-native validation.
- Report the exact validation performed and its result.
- Review the change against `REVIEW.md`.
- Confirm no generated analysis metadata, credentials, or unrelated changes are included.
