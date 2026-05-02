# Assignment 3: Reusable Workflows

## Overview

This repository demonstrates GitHub Actions reusable workflows by defining a reusable workflow and calling it from a parent workflow.

The example shows how to extract shared workflow logic into `.github/workflows/reusable-greet.yml` and invoke it twice from `.github/workflows/caller.yml` with different inputs.

## Repository Structure

- `README.md` - Project documentation.
- `.github/workflows/reusable-greet.yml` - Reusable workflow definition.
- `.github/workflows/caller.yml` - Workflow that calls the reusable workflow.

## Workflows

### `reusable-greet.yml`

- Trigger: `workflow_call`
- Inputs:
  - `name` (required string) — the name to greet.
- Job:
  - `greet` — prints a greeting message using `${{ inputs.name }}`.

### `caller.yml`

- Trigger: `push` to `main`
- Jobs:
  - `greet-semtech` — calls the reusable workflow with `name: Semtech`
  - `greet-siemens` — calls the reusable workflow with `name: Siemens`

## How It Works

1. The reusable workflow is defined in `.github/workflows/reusable-greet.yml`.
2. It exposes a `workflow_call` event with a `name` input.
3. The caller workflow uses `uses: ./.github/workflows/reusable-greet.yml` to invoke the reusable workflow locally.
4. Inputs are passed via `with:`.

## Example Usage

This repository is already configured to run on push to `main`.

```yaml
jobs:
  greet-semtech:
    uses: ./.github/workflows/reusable-greet.yml
    with:
      name: Semtech

  greet-siemens:
    uses: ./.github/workflows/reusable-greet.yml
    with:
      name: Siemens
```

## Best Practices

- Use reusable workflows for shared CI/CD logic across multiple repositories or modules.
- Keep inputs clear and documented.
- Prefer local reuse during development and repository reuse for cross-repo sharing.
- Use workflow outputs and environment variables when sharing results between jobs.

## Notes

- If you want to call this reusable workflow from another repository, update the `uses:` path to `owner/repo/.github/workflows/reusable-greet.yml@main`.
- Add secrets or additional inputs as needed for more complex workflows.

## License

This repository is released under the MIT License unless otherwise specified.