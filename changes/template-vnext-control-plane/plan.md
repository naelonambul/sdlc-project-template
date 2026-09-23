# Implementation Plan: Template vNext control plane

## Summary

Replace the documentation-only SDLC control plane with a small executable one. The design follows the owner-supplied Template vNext plan (Revision 9, sections 5 and 7, tranches T2 to T5). The prerequisite hotfix (T0) lands separately first.

This is the bootstrap change. It is authorized under the pre-vNext process. Once the candidate `scripts/repo.py` exists, it validates this packet and its diff before merge. No runner authorizes its own creation.

## Files and components that change

- `changes/`: the `_template` skeleton (`change.json`, `plan.md`), `README.md` describing the change model, and this packet.
- Root `plan.md` and the duplicated `sdlc-artifacts/references/` skeletons are removed. Root `intent.md` and `spec.md` lose their editable acceptance front matter and carry a baseline-unestablished marker until a product-init change establishes them.
- `scripts/repo.py`: stdlib-only `status` and `verify`. `scripts/tests/`: `unittest` fixtures.
- `checks.json`: the check registry. The core group needs only Python and git. The optional prototype registers its own group.
- `.github/workflows/repository.yml`, `.github/pull_request_template.md`: CI and a machine-readable `Change-ID`.
- `.gitattributes`: LF line endings for digest-bound artifacts.
- `AGENTS.md`, `README.md`, `REVIEW.md`, `.agents/skills/*`, `docs/`, `evals/README.md`, `scripts/*/README.md`: point to `repo.py` instead of restating the algorithms.

## Order of work

1. `repo.py status`: computed stage, freshness, approval and readiness; ordered chain; baseline inheritance; candidate and history-anchored closure; Change-ID resolution; write-scope enforcement; instruction-shadowing and skill-adapter checks. Include fixtures.
2. `checks.json` and `repo.py verify`: argv, cwd, timeout, requires and paths; PR-base routing; full suite on `main` and for unmapped paths; `not-applicable` with a reason; `blocked` for missing tools; raw log and SHA-256 evidence. Include fixtures.
3. CI workflow: no path filters; `edited` PR events; per-PR cancel-in-progress concurrency; SHA-pinned actions; `fetch-depth: 0`; every job runs; an `if: always()` summary requires every job to succeed.
4. Documentation and skills point at the control plane.

## Tests and proof

- `python3 -m unittest discover -s scripts/tests -t .` covers every fixture listed in plan sections T2 and T3 of the owner's Template vNext plan.
- `python3 scripts/repo.py status --change template-vnext-control-plane` validates this packet and its diff, once this plan's approval claim is recorded.
- `python3 scripts/repo.py verify` runs registered checks and writes evidence.
- CI behavior (edited-event reruns, cancelled superseded runs, strict up-to-date merges, squash-merge closure anchor) needs a disposable GitHub repository. That proof is deferred to the owner, because it creates external state.

## Risks and mitigations

- Digest-bound approval claims detect staleness only. They are not identity proof, and the documentation says so.
- Line-ending conversion would change digests. `.gitattributes` pins LF for artifacts.
- The Node-based prototype must not become a generic dependency. Its check lives in its own group and CI job, and both are removed with the directory.

## Rollback or recovery

Revert the squash commit. The previous documentation-only process is restored as a whole.

## Open questions

- Owner trust mode (plan tranche T1): distinct agent identity, and whether to protect `main` on the public template repository.
