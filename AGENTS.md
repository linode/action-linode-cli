# Agent Instructions

## Repository Shape

- This repository publishes a composite GitHub Action. Runtime behavior lives in [action.yml](action.yml); there is no source tree or generated build artifact.
- Treat [README.md](README.md) as the user-facing contract and [CONTRIBUTING.md](CONTRIBUTING.md) as the general contribution guide.
- The action supports Ubuntu-based runners. Do not imply macOS or Windows support without adding and passing coverage for those platforms.

## Editing Rules

- Treat action inputs and GitHub context values as untrusted. Never interpolate `${{ inputs.* }}` or `${{ github.* }}` directly into a `run:` script. Bind expressions through step-level `env:` entries, then reference shell variables with appropriate quoting or validation.
- Keep token masking before every other use of the token, and never print secret values.
- When adding or changing an input or runtime behavior, update [action.yml](action.yml), the relevant argument or example in [README.md](README.md), and coverage in [.github/workflows/test.yml](.github/workflows/test.yml) together.
- Preserve the existing composite-action and Bash style. Keep changes focused and avoid unrelated formatting churn.

## Validation

- There is no local build, unit-test, or lint command. The integration jobs in [.github/workflows/test.yml](.github/workflows/test.yml) are the executable test suite and run only on pushes.
- Tests invoke the checked-out action with `uses: ./` on `ubuntu-latest`. Authenticated scenarios require the repository's `LINODE_TOKEN` secret and network access.
- Add or adjust a focused integration scenario for each changed input path or installation mode.

## Pull Requests

- Target the default release branch, `v1`.
- PR titles must match `TPT-<number>: <subject>` unless an exemption label listed in [.github/workflows/validate-pr-title.yml](.github/workflows/validate-pr-title.yml) applies. Obtain a Jira ticket or explicit approval before creating a PR without that prefix.
- Follow [.github/pull_request_template.md](.github/pull_request_template.md) and keep each PR limited to one feature or fix.
