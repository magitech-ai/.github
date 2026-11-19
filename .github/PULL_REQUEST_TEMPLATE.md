## Summary
Provide a concise, technical overview of the changes.

## Invariant Verification
- [ ] **Zero Ancestral Mentions Rule**: Verified zero forbidden ancestral names across all diffs.
- [ ] **Capability Seam Symmetry**: Service definitions, providers, and consumers cleanly separated.
- [ ] **Strict Typing**: Passes `uv run mypy src` with zero untyped definitions.
- [ ] **Lint & Format**: Passes `uv run ruff check` and `uv run ruff format --check`.
- [ ] **100% Coverage Floor**: Passes `uv run pytest` with 100% statement and branch coverage.

## Changes & Seams
- Details of modifications.

## Factory provenance (agent-produced PRs only)

- Trigger issue: #___
- Execution: bounded `hsh` session in an isolated worktree
- Verification (command + observed result, not a claim):
- Human gate: this PR is left open for review and merge; the agent did not merge it.

See `agents-home/docs/FACTORY.md` for the loop contract. Leave this section out
of PRs that were not produced by the factory loop.