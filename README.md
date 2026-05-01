# Assignment 3: Reusable Workflows

## Overview

This repository contains the solution for Assignment 3 on reusable GitHub Actions workflows. It demonstrates how to create, configure, and consume reusable workflows to simplify CI/CD setup across multiple repositories or projects.

## Contents

- `README.md` - Project documentation and usage instructions.
- `.github/workflows/` - (If present) reusable workflow definitions and example workflow files.

## Key Concepts

- Reusable workflows allow you to define common CI/CD logic once and call it from other workflows.
- They improve maintainability by centralizing shared steps, jobs, and configuration.
- This repository is intended as a learning example for building reusable, modular GitHub Actions automation.

## Usage

1. Create a reusable workflow in a repository under `.github/workflows/`.
2. Reference the workflow using `uses: owner/repo/.github/workflows/workflow.yml@branch`.
3. Pass input parameters and secrets as needed.

Example call from another workflow:

```yaml
jobs:
  call-reusable-workflow:
    uses: owner/assignment3-reusable-workflows/.github/workflows/reusable-workflow.yml@main
    with:
      example-input: "value"
    secrets:
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Recommended Structure

- Keep reusable workflows in their own repository or a shared organization repo.
- Use clear input names and default values.
- Document expected inputs, outputs, and any required secrets.

## Notes

- If this repository is part of a classroom assignment, update the workflows and documentation to match the assignment requirements.
- Adjust branches, workflow file names, and input values as needed for your environment.

## License

This repository is released under the MIT License, unless otherwise specified.