# Contributing

## Setup

```bash
git clone https://github.com/magitech-ai/<repo>.git
cd <repo>
uv sync
```

Contributing needs no published release — a clone and `uv sync` are enough.

Before writing code:

1. Read `CONTEXT.md` for the domain vocabulary. Use those words, not the
   generic ones.
2. Read `AGENTS.md` for project contracts and testing expectations.
3. Read a recent test in the file you are about to change and copy its shape.
   This project is TDD: failing test first, then implement.
4. Comment on the issue before you start, so two people do not build the same
   thing.

## Code Style

- Follow the Google Python Style Guide
- Ruff for linting and formatting
- mypy strict mode for type checking
- 88-character line length
- Conventional commit messages (`feat(scope):`, `fix(scope):`, etc.), no emojis

## Testing

```bash
# Full suite with the 100% statement and branch coverage floor
uv run pytest

# Unit tests only
uv run python -m pytest tests/unit
```

Requirement: all tests passing, 100% statement and branch coverage enforced
via each repo's `pyproject.toml` (`--cov-fail-under=100 --cov-branch`) and
re-checked by shared CI.

## Architecture Decision Records

See `docs/adr/` in each repository for its architectural decisions. To propose
a new ADR, create `docs/adr/NNNN-short-name.md` following the existing
template and submit it as part of a PR with a description of the decision.

## Issue Tracking & Triage

All repositories in `@magitech-ai` use GitHub Issues and the `gh` CLI with a
canonical five-role triage vocabulary:

| Label | Meaning |
| :--- | :--- |
| `needs-triage` | Maintainer needs to evaluate this issue |
| `needs-info` | Waiting on reporter for more information |
| `ready-for-agent` | Fully specified, ready for autonomous agent execution |
| `ready-for-human` | Requires human implementation or review |
| `wontfix` | Out of scope or will not be actioned |

## Pull Requests

Open a PR against `main` from a branch. CI must be green (Test & Lint, 100%
coverage, CodeQL). Nothing merges without the maintainer's word.
