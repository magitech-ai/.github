# magitech-ai/.github

Org-wide defaults for the magitech-ai organization. GitHub treats this
specially named repository as the source of shared files for every repository
in the org that does not have its own copy.

## What lives here

- `.github/workflows/python-ci.yml` — reusable Python CI workflow
  (checkout → setup-uv → install → lint → test → enforce the 100%
  statement + branch coverage floor). Called from a repo's own `ci.yml`.
- `pull_request_template.md` — default PR template for all org repos.
- `.github/ISSUE_TEMPLATE/` — default bug report, feature request, and
  issue config for all org repos.
- `SECURITY.md` — default security policy (private vulnerability reporting).
- `CONTRIBUTING.md` — default contributor guide.

## How a repo opts in

CI: add a thin `.github/workflows/ci.yml` that calls the shared workflow:

```yaml
name: CI

permissions:
  contents: read

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    name: Test & Lint
    uses: magitech-ai/.github/.github/workflows/python-ci.yml@main
    with:
      python-version: "3.12"
```

Repos with sibling checkouts (a `path` dependency on another org repo) pass
`checkout-path`, `working-directory`, and `pre-commands` that clone the
sibling, e.g. `git clone --depth 1 https://github.com/magitech-ai/anima.git anima`.

Dependabot: per-repo only — each repo carries its own
`.github/dependabot.yml` (uv ecosystem, daily). It cannot come from this repo.

## How a repo overrides

Any file a repo carries itself shadows the org default: its own
`pull_request_template.md`, `SECURITY.md`, `CONTRIBUTING.md`, or issue
templates win over these. The shared workflow is opt-in per repo; nothing is
forced on a repo that does not call it.

## Coverage floor

All magitech-ai repos enforce 100% statement and branch coverage. The floor
lives in each repo's `pyproject.toml` (`--cov-fail-under=100 --cov-branch`)
and is re-checked by the shared workflow, so a repo whose pytest config loses
the floor still fails CI instead of silently passing.

## Not in this repo

- No publish/release workflows: no magitech-ai repo is on PyPI yet. They
  belong here as reusable workflows when the first repo publishes.
- No `dependabot.yml`: per-repo only (see above).
- No scorecard or other repo-specific jobs.
