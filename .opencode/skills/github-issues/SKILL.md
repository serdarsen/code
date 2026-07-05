---
name: github-issues
description: GitHub Issue reading, requirement analysis, and PR conventions for the 'code' project
compatibility: opencode
metadata:
  project: code
---

## What I do
- Read GitHub issues and summarize requirements
- Identify EF Core feature work needed from issues
- Produce implementation and testing checklists
- Reference issues in commits and PRs

## Issue Conventions
- Each issue describes one EF Core concept or feature to showcase
- Issues include acceptance criteria for what the demo should cover
- Issues may reference official EF Core documentation for context

## Workflow
1. Read the issue description and comments thoroughly.
2. Identify the EF Core concept to demonstrate.
3. Produce a checklist:
   - Model/entity design
   - EF Core configuration
   - Migration (if schema changes are needed)
   - Service/API layer (if applicable)
   - Tests
   - Documentation

## PR References
- Include `Closes #N` in the PR description to auto-close the issue on merge.
- Reference the issue in commit messages with `GH-{number}`.
- Keep PRs focused on a single issue whenever possible.
