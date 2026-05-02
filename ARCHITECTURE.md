# Architecture — Reusable Workflow Pattern

## The Problem This Solves
Without reusable workflows, every repo duplicates the
same CI steps — build, test, lint, deploy. A change 
to one step requires updating 15 repos. That's the 
problem I solve daily across 15 engineering teams 
at Siemens.

## How It Works
reusable-greet.yml defines the job with workflow_call
trigger and accepts `name` as an input parameter.

caller.yml invokes it twice with different inputs —
demonstrating that one workflow definition serves
multiple consumers.

## Local vs Cross-Repo Reuse
Local (this repo):
  uses: ./.github/workflows/reusable-greet.yml

Cross-repo (production pattern):
  uses: chinu0105/shared-workflows/.github/workflows/
        reusable-greet.yml@main

## When to Use Reusable Workflows
✓ Steps shared across 3+ repositories
✓ Security scanning (CodeQL, SonarCloud)  
✓ Docker build + push patterns
✓ Environment promotion gates

✗ Repo-specific business logic
✗ One-off scripts

## What I Would Add in Production
- secrets: inherit for passing tokens
- outputs: for passing build artifacts between caller 
  and reusable workflow
- Version pinning: @v1 tag instead of @main
- Separate shared-workflows repo as single source
