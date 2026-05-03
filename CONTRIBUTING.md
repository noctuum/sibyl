# Contributing to aurtomator

aurtomator is a template repository: the primary way to use it is to fork and run your own instance. Upstream contributions are welcome but strictly optional — nothing in this document implies an obligation to send fixes or features back.

## Before opening a PR

For anything beyond a typo or a one-line fix, open an issue or a draft PR first to agree on direction. This avoids wasted work on changes that will not be accepted.

Proposals that expand aurtomator into a general-purpose build bot, CI-hosted package build service, or multi-user orchestration system are out of scope. See the "Alternatives" section of `README.md` for tools that target that problem space.

## Development setup

```sh
sudo pacman -S --needed git bash shellcheck shfmt bats bats-assert bats-support go-yq
git clone https://github.com/staticwire/aurtomator.git
cd aurtomator
bats tests/
```

## Conventions

- Bash 5+ with `set -euo pipefail` at the top of every script.
- Functions in `snake_case`; globals in `UPPER_SNAKE`; function-local variables declared with `local`.
- Double-quote every expansion: `"$var"`, `"${array[@]}"`.
- Scripts must be `shellcheck` clean and formatted with `shfmt -i 2 -ci`.
- BATS tests are required for new scripts in `scripts/` and every new strategy in `strategies/`. Strategy tests must mock API responses — no live network access from the test suite.
- Commit messages follow Conventional Commits with a component scope, for example `feat(strategy): add forgejo-tag detection` or `fix(scripts): handle empty version output`.
- GitHub Actions are pinned by commit SHA with a trailing version comment: `uses: actions/checkout@abc1234def5678... # v4.1.7`.

## Running the full check locally

These are the exact commands CI runs — match them to ensure "passes locally" equals "passes in CI":

```sh
shellcheck -x -S warning scripts/*.sh strategies/*.sh
shfmt -d -i 2 -ci scripts/*.sh strategies/*.sh
bats tests/
```

## PR workflow

PRs are squash-merged. Individual commit messages inside a PR are not preserved in the main branch history — only the PR title becomes the squash commit subject. Because of that, the **PR title itself must be Conventional-Commits compliant**, including scope where appropriate. A PR titled `fix strategy bug` will not be merged as-is; retitle to something like `fix(strategy): handle empty release list from github-release`.

Keep PRs focused. One logical change per PR. Unrelated refactors go in a separate PR.

## Adding a new strategy

1. Create `strategies/<name>.sh` that accepts the YAML package config per the existing strategy contract, prints a single version string to stdout on success, and exits non-zero on failure. Copy the nearest existing strategy as a starting point rather than starting from scratch.
2. Add mocked BATS tests to `tests/strategies.bats` — strategy tests live in a single file, grouped by strategy. Tests must not perform live network requests; stub `curl` / API access using the fixtures in `tests/helpers/mock-curl.sh`.
3. Document the strategy in the strategies table in `README.md` and in `docs/WORKFLOW.md`.
4. Add a usage example to `packages/example.yml.sample`.
5. Run the full local check (shellcheck, shfmt, bats) before opening the PR.

## Reporting bugs

Use the issue templates under "Bug report" or "New strategy request". Security-impacting issues must not be filed as public issues — follow `SECURITY.md` instead.
