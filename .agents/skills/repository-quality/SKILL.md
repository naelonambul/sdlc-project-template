---
name: repository-quality
description: Establish and run repository-native quality tooling. Use when a project's language, framework, build system, or runtime becomes concrete and lint, format, test, type-check, or build checks are missing or incomplete, or during implementation, debugging, review, and completion when canonical validation must be discovered, bootstrapped, recorded, or run without replacing established conventions.
---

# Repository Quality

Treat quality tooling as repository infrastructure. Reuse established tooling; bootstrap only after the product stack is concrete.

## Determine the current state

1. Read `AGENTS.md` and the accepted root artifacts relevant to the task.
2. Identify the language, framework, runtime, build system, and package manager from repository evidence or an explicit accepted human decision. Do not treat an exploratory prototype as a final stack decision.
3. Inspect repository-native command surfaces such as package scripts, build manifests, task runners, Makefiles, CI workflows, and existing scripts or config files.
4. Classify each applicable gate as established, partial, or absent: build, test, lint, format-check, type-check, and project-specific verification.
5. If the product stack is still unresolved, do not install competing quality tools. Surface the missing decision instead.

## Bootstrap missing quality tooling

When the stack is established and suitable quality tooling is absent or materially incomplete:

1. Choose the smallest conventional toolchain that fits the selected ecosystem.
2. Prefer official, framework-native, or ecosystem-standard tooling and the repository's existing package/build manager.
3. Prefer one formatter and one linter. If one established tool safely covers both roles, avoid adding an overlapping second tool.
4. Declare tools as repository dependencies, plugins, or toolchain configuration. Do not depend on untracked global installation.
5. Keep configuration in the ecosystem's conventional location and ignore only generated or machine-local output.
6. Expose reproducible commands for the applicable gates. Include a non-mutating format check as well as a formatting command when the formatter supports both.
7. Preserve lockfiles and version constraints according to the ecosystem's normal package-management practice.
8. If the tooling setup would materially depart from accepted artifacts or an accepted plan, revise the relevant artifact and obtain human acceptance before proceeding.
9. Run the new checks against the repository and fix starter configuration or source until the setup is genuinely usable. Do not weaken a rule merely to obtain a green result.
10. Record the exact canonical commands in `AGENTS.md`. If a stable multi-command wrapper improves reproducibility, place the shared deterministic wrapper under `scripts/checks/`.

## Stack-aware selection guidance

Use these as defaults only when no repository convention already exists:

- **JavaScript / TypeScript:** respect framework defaults first. Otherwise use the existing package manager with a conventional linter and formatter; add a TypeScript type-check command when TypeScript is part of the product stack.
- **Python:** prefer `pyproject.toml`-based configuration. A consolidated tool such as Ruff is a reasonable lint/format default when no convention exists; add the project's test runner and static type checker only when those gates are meaningful for the chosen stack.
- **Go:** prefer native `gofmt`, `go vet`, and `go test`; add an additional aggregate linter only when the project has a concrete reason for it.
- **Rust:** prefer Cargo-native `cargo fmt`, `cargo clippy`, and `cargo test`.
- **Swift / Xcode:** keep Xcode or SwiftPM build/test commands canonical. When adding style tooling from scratch, prefer established Swift ecosystem tooling and avoid redundant formatter/linter combinations.
- **Java / Kotlin:** integrate formatting and linting through the existing Gradle or Maven build rather than creating a parallel toolchain.
- **Other stacks:** follow the same rule: repository-native first, then the smallest official or ecosystem-standard toolchain that covers the applicable gates.

Do not replace an existing valid toolchain with one of these examples merely because it is newer or preferred by the agent.

## Preserve the checks

- Do not introduce a different formatter, linter, test framework, or type checker merely because you prefer it.
- Do not disable, weaken, skip, delete, or rewrite a failing check merely to make validation pass.
- Do not silently change test expectations to match broken implementation behavior.
- Change validation configuration only when the task actually requires that configuration change and the accepted artifacts authorize it.

## Canonical command contract

After the product stack is established, keep the applicable root commands in `AGENTS.md` current:

- Build
- Test
- Lint
- Format check
- Type check

Use `not applicable` for a genuinely irrelevant gate rather than leaving a stale `not configured` entry. Commands should be runnable from the repository root or explicitly include the required working-directory change.

A nested self-contained workspace such as optional `prototype/` may keep its own tooling. Its checks do not become a root product requirement unless the repository intentionally aggregates them.

## Validate proportionally

- During iteration, run the smallest relevant checks that provide fast feedback.
- Before completion, run every applicable canonical check required by `AGENTS.md`, the accepted plan, or CI policy.
- Treat visual or runtime verification as part of validation when the accepted plan requires it.
- If meaningful validation cannot yet exist because the product stack is not established, state that fact instead of installing speculative tooling.

## Report evidence

Report the exact commands or checks run, whether they passed, and any relevant limitation. Do not claim a check ran when it did not.
