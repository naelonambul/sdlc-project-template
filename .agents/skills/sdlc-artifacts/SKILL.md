---
name: sdlc-artifacts
description: Manage the repository root artifact chain across `intent.md`, `spec.md`, and `plan.md`. Use when starting or refining project intent, interrogating requirements, drafting or revising intent/spec/plan, recording human acceptance, checking SDLC stage readiness, or deciding whether implementation is authorized.
---

# SDLC Artifacts

Treat `intent.md`, `spec.md`, and `plan.md` as one gated authority chain.

## Preserve gate semantics

- Use only `not-started`, `draft`, and `accepted` for artifact status.
- Never infer acceptance from non-empty content, Git state, a previous agent message, or your own judgment.
- Mark an artifact `accepted` only after the human owner explicitly approves it.
- Keep downstream artifacts `not-started` until their upstream gate is accepted.
- Continue reading every accepted upstream artifact throughout all later stages.
- Never let a downstream artifact silently contradict an accepted upstream artifact. Surface the conflict.

## Develop intent

1. Read the current `intent.md`.
2. Interrogate ambiguity before finalizing the draft. Cover problem, desired outcome, affected users/systems, constraints, scope boundaries, success criteria, and open questions.
3. Use any agent-specific interrogation interface only as a convenience. Preserve the same semantics when that interface is unavailable.
4. Write a self-contained `intent.md` with `status: draft`.
5. Iterate until the human owner explicitly accepts it.
6. Only then set `status: accepted` and record acceptance metadata when available.

Use `references/intent-template.md` as the structural guide.

## Develop specification

1. Require `intent.md` to be accepted.
2. Read the accepted intent in full.
3. Inspect the repository and apply relevant repository skills and policies.
4. Convert the intent into concrete requirements, behavior, architecture/design decisions, interfaces/data/dependencies, constraints, risks, and acceptance criteria.
5. Carry unresolved questions forward explicitly; do not invent an answer merely to complete the document.
6. Write `spec.md` with `status: draft`, iterate with the human owner, and mark it accepted only after explicit approval.

Use `references/spec-template.md` as the structural guide.

## Develop implementation plan

1. Require both `intent.md` and `spec.md` to be accepted.
2. Read both accepted artifacts and inspect the current repository state.
3. Produce a plan detailed enough that an agent entering with no conversation history can implement it.
4. Name files/components, order of work, tests/proof, major risks, mitigations, and rollback/recovery where relevant.
5. Challenge the plan: identify breakage risks, the riskiest step, and rejected alternatives when they matter.
6. Write `plan.md` with `status: draft`, iterate, and mark it accepted only after explicit human approval.

Use `references/plan-template.md` as the structural guide.

## Enforce the implementation gate

- Do not implement from a draft or not-started plan.
- During implementation, read `intent.md`, `spec.md`, and `plan.md`; do not treat the plan as the only authority.
- If implementation needs a material departure from the accepted plan, stop, revise the plan, and obtain human acceptance before continuing.
- Never revise an accepted upstream artifact merely to make an implementation easier or to retroactively justify code.
