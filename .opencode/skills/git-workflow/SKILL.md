---
name: git-workflow
description: Branch creation, commit conventions, and PR workflow for the 'code' open-source project
compatibility: opencode
metadata:
  project: code
---

## What I do
- Sync local `main` with `origin/main` before starting work
- Create feature branches from `origin/main`
- Commit with descriptive messages referencing the GitHub issue
- Push branches and open pull requests against `origin/main`

## Sync Before Starting
- Before creating a feature branch, ensure local `main` is up to date:
  ```
  git checkout main
  git pull origin main
  ```

## Branch Naming Convention
```
feature/{issue-number}-{kebab-case-description}
```
Example: `feature/42-add-value-conversion-demo`

## Commit Convention
- Follow the Conventional Commits specification: https://www.conventionalcommits.org/en/v1.0.0/
- Use `<type>(<scope>): <description>` format where `type` is one of `feat`, `fix`, `docs`, `refactor`, `test`, `chore`, `ci`.
- Reference the GitHub issue number in the commit message footer with `Refs: #N`.
- Include the EF Core concept changed in the description when relevant.

Examples:
```
feat(identity): add many-to-many user-role configuration
```
```
fix(orders): resolve N+1 on order item loading
```
```
docs(value-conversion): add Money value converter README
```

## PR Workflow
- Create PR against `origin/main` branch
- Include PR title with issue number and description
- Reference the GitHub issue in the description using `Closes #N`

### PR Creation
- Push the feature branch before creating the PR:
  ```
  git push origin feature/{issue-number}-{description}
  ```
- Create a PR:
  ```
  gh pr create --base main --head feature/{issue-number}-{description} --title "GH-{number}: description" --body "Closes #{number}"
  ```
