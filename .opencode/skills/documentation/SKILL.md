---
name: documentation
description: Documentation generation standards for the 'code' EF Core showcase project
compatibility: opencode
metadata:
  project: code
---

## What I do
- Write and update README files for feature modules
- Add XML comments on public API surfaces
- Document EF Core concepts demonstrated by each feature
- Maintain the project-level README

## Project README
- Project overview and goals
- Prerequisites (.NET SDK version)
- Getting started (clone, build, run)
- Feature index with links to each module's README
- Contributing guidelines

## Feature Module README
Every feature must have a README.md explaining:

```markdown
# Feature Name

## EF Core Concept Demonstrated
- Which EF Core feature this module showcases

## How It Works
- Brief explanation of the concept

## Models
- Key entities involved

## Configuration
- Notable Fluent API or conventions used

## Sample Query
```csharp
// code snippet showing the feature in action
```

## When to Use This Pattern
- Practical scenarios where this EF Core feature is beneficial
```

## XML Comments
- Document all public methods and properties
- Include `<param>` and `<returns>` descriptions
- Note any exceptions that may be thrown
- Keep comments concise and meaningful

## GitHub Issue Documentation
- Reference the issue number in feature documentation
- Link feature to the original proposal or discussion
