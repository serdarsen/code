---
name: testing
description: Unit and integration testing patterns with xUnit and EF Core for the 'code' project
compatibility: opencode
metadata:
  project: code
---

## What I Do
- Write unit tests for service logic
- Write integration tests against EF Core with PostgreSQL via Testcontainers
- Verify EF Core queries produce correct SQL and results
- Ensure migrations are valid

## Testing Stack
- xUnit
- FluentAssertions or Shouldly
- Testcontainers.PostgreSQL
- Npgsql.EntityFrameworkCore.PostgreSQL

## Test Project Structure
```
tests/Code.Tests/
├── Features/
│   └── FeatureNameTests.cs
├── Data/
│   └── MigrationTests.cs
└── Usings.cs
```

## DbContext Test Pattern
- Use `Testcontainers.PostgreSQL` to spin up a fresh Postgres instance per test class.
- Use a shared fixture or base class for container lifecycle management.

```csharp
public class PostgresTestFixture : IAsyncLifetime
{
    private readonly PostgreSqlContainer _container = new PostgreSqlBuilder()
        .WithImage("postgres:16")
        .Build();

    public string ConnectionString => _container.GetConnectionString();

    public async Task InitializeAsync() => await _container.StartAsync();
    public Task DisposeAsync() => _container.DisposeAsync().AsTask();
}
```

## What to Test
- Entity configuration (keys, indexes, relationships)
- Query behavior (filtering, sorting, includes)
- Value conversions and owned types
- Migration application (no pending model changes)
- Custom conventions and interceptors

## Test Naming
- `{MethodOrConcept}_Should_{ExpectedBehavior}_When_{Scenario}`
- Example: `GetActiveOrders_Should_FilterByStatus_When_StatusIsActive`

## Conventions
- Tests must be deterministic and isolated.
- Clean up database state between test runs (use `EnsureDeleted` + `EnsureCreated` or transactional rollback).
- Use `DotNet.Testcontainers` for local development and CI — no provider switching.
