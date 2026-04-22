# Security Policy

## Supported versions

Only the latest tagged release of aurtomator is supported. There are no backports to prior releases. If you run a fork, you are expected to track upstream and rebase or merge in fixes as they land. Unreleased `main` is considered unsupported between releases.

| Version | Supported |
| ------- | --------- |
| latest release | yes |
| older releases | no |

## Reporting a vulnerability

Report vulnerabilities privately through GitHub's Private Vulnerability Reporting. Do not open a public issue for security-impacting bugs.

1. Navigate to <https://github.com/staticwire/aurtomator/security/advisories/new>.
2. Fill in the advisory form: affected components, reproduction steps, impact, and any suggested mitigation.
3. Attach proof-of-concept material as draft advisory attachments where possible, rather than linking to external services.
4. Submit. The advisory is private between you and the maintainer until it is published.

Expect an initial acknowledgement within 7 days. aurtomator is a solo-maintained project. There is no formal SLA for triage, fix, or disclosure timelines beyond that initial acknowledgement, and timelines will vary with the severity and complexity of the issue. If you have not received an acknowledgement after 7 days, submit a new advisory noting the missed acknowledgement.

## Scope

In scope:

- `scripts/` — any defect that allows arbitrary code execution, secret exfiltration, or unintended writes outside the working tree.
- `strategies/` — injection via crafted upstream responses, YAML parsing issues, or command-injection through package configuration.
- `.github/workflows/` — misconfiguration that leaks `AUR_SSH_KEY`, `GPG_SIGNING_KEY`, `AUR_GIT_NAME`, or `AUR_GIT_EMAIL` secrets into logs, artifacts, forks, pull requests, or third-party actions.
- Anything else in this repository that can cause a fork to push a compromised package to AUR without the fork maintainer's intent.

Out of scope:

- Vulnerabilities in external tools invoked by aurtomator (`makepkg`, `yq`, `curl`, `git`, `namcap`, `shellcheck`, `shfmt`, `bats`). Report those to their respective upstream projects.
- The contents of AUR packages produced by forks. Each fork maintainer is responsible for the packages they publish; upstream aurtomator provides the automation framework, not the package contents.
- The fork-based distribution model itself (for example, "a malicious fork could push a bad package"). This is an inherent property of the template model and is documented in `README.md`.
- Issues in third-party GitHub Actions. Report to the action's maintainer; aurtomator pins by commit SHA to mitigate.

## Disclosure

Once a reported issue is fixed, the private advisory is published on the repository's Security tab. If a CVE has been assigned through GitHub's CNA, it is referenced in the published advisory and in the release notes of the version that contains the fix. Forks inherit the fix on their next rebase or merge from upstream; fork maintainers are encouraged to subscribe to repository releases to receive notifications when a security-relevant release is published.
