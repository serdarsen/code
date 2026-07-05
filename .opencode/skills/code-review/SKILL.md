---
name: code-review
description: Code review checklist and quality standards for the 'code' EF Core showcase project
compatibility: opencode
metadata:
  project: code
---

## What I Do
- Review EF Core model configurations for correctness
- Review C# code for quality, performance, and adherence to patterns
- Review tests for completeness
- Provide actionable review feedback without rewriting code unless asked

## Code Quality Checklist
- SOLID principles followed
- DRY (Don't Repeat Yourself)
- Naming conventions: PascalCase for classes/methods, camelCase for parameters
- Async/await usage (avoid sync-over-async)
- Nullable reference types handled properly
- Appropriate log levels and structured logging

## EF Core Checklist
- Fluent API used over data annotations where appropriate
- Relationships configured correctly (cascade delete, required/optional)
- Indexes defined for query patterns
- No N+1 queries (Verify `.Include()` / `.ThenInclude()` usage)
- No SELECT N+1 in test assertions
- Migrations are reviewed before applying
- No unnecessary eager loading
- Split queries considered for large collections

## Testing Checklist
- Feature has corresponding tests
- Tests cover the happy path and edge cases
- PostgreSQL Testcontainers tests use a fresh container or database per run
- No test relies on shared mutable state
- `dotnet test` passes

## Architecture Checklist
- Feature is self-contained in its own module
- No circular dependencies between features
- DbContext configuration uses `IEntityTypeConfiguration<T>` classes
- Services are registered via extension methods
