## Summary

<!-- One or two sentences describing what this PR changes and why. The PR title becomes the squash-merge commit subject, so it must be Conventional-Commits compliant (e.g. `feat(strategy): add forgejo-tag detection`). -->

## Related issue

Fixes #<!-- issue number --> <!-- or "N/A" if this PR does not track an issue -->

## Type of change

- [ ] Bug fix
- [ ] New strategy
- [ ] New feature (non-strategy)
- [ ] Documentation
- [ ] CI / tooling
- [ ] Refactor (no behavior change)

## Checklist

- [ ] Commit messages follow Conventional Commits format
- [ ] `shellcheck -x -S warning scripts/*.sh strategies/*.sh` passes locally
- [ ] `shfmt -d -i 2 -ci scripts/*.sh strategies/*.sh` produces no diff
- [ ] `bats tests/` passes
- [ ] New scripts or strategies have BATS tests
- [ ] New strategies are documented in `README.md` and `docs/WORKFLOW.md`
- [ ] GitHub Actions changes pin by commit SHA with a version comment

## Notes for the reviewer

<!-- Call out trade-offs, deliberate omissions, follow-up work, or specific areas where you want feedback. If something in the checklist above does not apply, say why here rather than silently skipping it. -->
