# SDLC Project Template

A small, agent-neutral starter repository for an AI-native software development lifecycle.

This template turns the repository itself into the shared control plane for planning, implementation, verification, and review. It is inspired by the AI-Native SDLC playbook and generalizes the artifact-driven workflow so it can be used with different coding agents.

## Core workflow

```text
idea
  -> changes/<id>/  (intent -> spec -> plan, each approved by the owner in order)
  -> implementation + verification, inside the change's write scope
  -> merge accepted intent/spec into the root baseline
  -> closure.json -> pull request -> merge (squash by default)
```

The root `intent.md` and `spec.md` are the durable product baseline. A new product's first change is `product-init`, which establishes them. `python3 scripts/repo.py status` computes every change's stage, freshness, approval and readiness. See `changes/README.md`.

## Quick start

1. Create a new repository from this GitHub template and clone it.
2. Copy `changes/_template/` to `changes/<id>/` for a `product-init` change, with copies of the root `intent.md` and `spec.md`.
3. Ask an agent to interrogate the idea until the intent is concrete, then approve `intent.md` by adding a digest-bound claim to `change.json`.
4. Draft and approve `spec.md`, then the change's `plan.md`, in that order.
5. Implement only when `python3 scripts/repo.py status --change <id>` reports `readiness=ready`.
6. Run repository-native validation, review against `REVIEW.md`, merge the accepted intent and spec into the root, add `closure.json`, and open a pull request with `Change-ID: <id>`.

See `.agents/skills/sdlc-artifacts/SKILL.md` for the workflow.

## Repository control plane

- `AGENTS.md`: short, always-relevant repository invariants, gates, commands, and working rules.
- `REVIEW.md`: shared review rubric.
- `intent.md`, `spec.md`: durable product baseline (why, and what must be true).
- `changes/`: one packet per change, with its own plan; `changes/README.md` defines the model.
- `scripts/repo.py`: computes change status and enforces gates.
- `.agents/skills/`: on-demand shared agent procedures and tool policies.
- `scripts/`: deterministic checks and agent-neutral hook implementations.
- `evals/`: regression evaluations for agent behavior and configuration.
- `docs/`: supporting, reference, and historical documentation only.
- `prototype/`: optional, removable plain HTML/CSS/JavaScript discovery workspace with lint and formatting.
- `.github/`: pull-request and CI integration.

## Optional prototype workspace

`prototype/` is a self-contained UI/UX discovery workspace using vanilla HTML, CSS, and JavaScript. Its quality stack mirrors the proven Pungsu prototype setup: ESLint, Stylelint, HTMLHint, and Prettier. Run `npm install` once inside the directory on each project/machine, then use `npm run check` as its local validation command.

The directory is deliberately optional. Projects that do not need a frontend or UI prototype, including backend-only projects, can delete the entire `prototype/` directory. The root SDLC files, skills, scripts, and project commands do not depend on it, so no replacement config or cleanup should be required after deletion.

Prototype output is evidence and exploration, not authority. Any discovery that changes the baseline or an approved change must go back through the relevant owner approval.

## Authority model

The root baseline plus approved change packets are the SDLC authority. `docs/` and any optional supporting workspace such as `prototype/` must not override them. Concurrent initiatives are separate change packets; one pull request carries one change.

## Agent neutrality

SDLC semantics belong to the repository, not to a specific agent interface. Features such as interrogation commands, plan modes, subagents, or agent-specific hooks are optional convenience layers.

CLI and program installation are machine responsibilities. The repository stores how agents are expected to use those tools through version-controlled skills and policies.

Included shared skills:

- `sdlc-artifacts`
- `repository-quality`
- `context7`
- `serena`
- `graphify`

Optional tool unavailability must not silently change the SDLC gates.

Claude Code discovers these skills through thin `.claude/skills/<name>` symlinks to `.agents/skills/<name>`, and loads `AGENTS.md` only when no project `CLAUDE.md` shadows it. The template therefore ships no `CLAUDE.md`. See `docs/agent-surfaces.md` for the smoke-tested surfaces and known gaps.

## Project initialization

When a project chooses its application stack, establish the repository-native build, test, lint, format-check, and type-check commands, then record the canonical commands in `AGENTS.md`. Add deterministic wrappers and CI only when they represent real project behavior.

## Source material

The structure is informed by Anthropic's *The AI-Native SDLC playbook* (August 21, 2026), especially its artifact-driven handoffs, human gates, short always-loaded context, skills, deterministic guardrails, feedback loops, independent verification, PR review policy, and continuous evals.
