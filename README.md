# SDLC Project Template

A small, agent-neutral starter repository for an AI-native software development lifecycle.

This template turns the repository itself into the shared control plane for planning, implementation, verification, and review. It is inspired by the AI-Native SDLC playbook and generalizes the artifact-driven workflow so it can be used with different coding agents.

## Core workflow

```text
idea
  -> intent.md (draft -> accepted)
  -> spec.md   (draft -> accepted)
  -> plan.md   (draft -> accepted)
  -> implementation + tests
  -> review / pull request
  -> merge / deploy / maintain
```

A downstream stage starts only after the upstream artifact has been explicitly accepted by the human owner. Later stages continue to read all accepted upstream artifacts.

## Quick start

1. Create a new repository from this GitHub template and clone it.
2. Start with `intent.md`. Ask an agent to interrogate the idea until the problem, outcome, constraints, scope, and open questions are concrete.
3. Explicitly accept `intent.md` when it is correct.
4. Draft `spec.md` from the accepted intent and accept it after review.
5. Draft `plan.md` from the accepted intent and spec and accept it after review.
6. Implement only from an accepted plan.
7. Run repository-native validation and review the change against `REVIEW.md` before merge.

See `.agents/skills/sdlc-artifacts/SKILL.md` for the artifact workflow.

## Repository control plane

- `AGENTS.md`: short, always-relevant repository invariants, gates, commands, and working rules.
- `REVIEW.md`: shared review rubric.
- `intent.md`: why the project/change exists and what outcome is wanted.
- `spec.md`: what must be true and the approved design/requirements.
- `plan.md`: how the accepted spec will be implemented and proven.
- `.agents/skills/`: on-demand shared agent procedures and tool policies.
- `scripts/`: deterministic checks and agent-neutral hook implementations.
- `evals/`: regression evaluations for agent behavior and configuration.
- `docs/`: supporting, reference, and historical documentation only.
- `prototype/`: ready-to-use plain HTML/CSS/JavaScript discovery workspace with lint and formatting.
- `.github/`: pull-request and CI integration.

## Prototype workspace

`prototype/` is preconfigured for disposable UI/UX discovery with vanilla HTML, CSS, and JavaScript. Its quality stack mirrors the proven Pungsu prototype setup: ESLint, Stylelint, HTMLHint, and Prettier. Run `npm install` once inside the directory on each project/machine, then use `npm run check` as the canonical prototype validation command.

Prototype output is evidence and exploration, not authority. Any discovery that changes an accepted root artifact must go back through the relevant human gate.

## Authority model

The root artifact chain is the current SDLC authority for the active project workflow. `docs/` and `prototype/` are supporting material and must not override accepted root artifacts.

This starter is intentionally optimized for one active project-level artifact chain at a time, which keeps a solo-developer workflow simple. A project that later needs independent concurrent initiatives can namespace its artifacts without changing the underlying gate semantics.

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

## Project initialization

When a project chooses its application stack, establish the repository-native build, test, lint, format-check, and type-check commands, then record the canonical commands in `AGENTS.md`. Add deterministic wrappers and CI only when they represent real project behavior.

## Source material

The structure is informed by Anthropic's *The AI-Native SDLC playbook* (August 21, 2026), especially its artifact-driven handoffs, human gates, short always-loaded context, skills, deterministic guardrails, feedback loops, independent verification, PR review policy, and continuous evals.
