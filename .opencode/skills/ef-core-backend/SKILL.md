---
name: ef-core-backend
description: EF Core backend patterns, project structure, and conventions for the 'code' open-source showcase project
compatibility: opencode
metadata:
  project: code
---

## What I Do
- Implement EF Core models, configurations, and migrations
- Write feature modules showcasing specific EF Core concepts
- Create DbContext configurations with Fluent API

## Tech Stack
- .NET (latest stable)
- Entity Framework Core
- PostgreSQL (development and production)
- Npgsql.EntityFrameworkCore.PostgreSQL
- xUnit + Testcontainers for integration testing

## Project Structure
```
code/
├── src/
│   └── Code/
│       ├── Features/
│       │   ├── FeatureName/
│       │   │   ├── Models/
│       │   │   ├── Configurations/
│       │   │   ├── Services/
│       │   │   └── README.md
│       │   └── ...
│       ├── Data/
│       │   ├── AppDbContext.cs
│       │   └── Migrations/
│       └── Program.cs
├── tests/
│   └── Code.Tests/
│       ├── Features/
│       └── ...
└── README.md
```

## DbContext Standards
- Register entities in `OnModelCreating` via `IEntityTypeConfiguration<T>` implementations.
- Apply configurations with `modelBuilder.ApplyConfigurationsFromAssembly()`.
- Use Fluent API over data annotations for separation of concerns.
- Enable sensitive data logging only in development.
- Use Npgsql-specific configuration (e.g., `EnableLegacyTimestampBehavior`, `AppContext.SetSwitch("Npgsql.EnableLegacyTimestampBehavior", true)`) as needed.

## Entity Configuration Standards
- Create a dedicated configuration class per entity implementing `IEntityTypeConfiguration<T>`.
- Use descriptive table and column names.
- Configure keys, indexes, relationships, and constraints explicitly.

```csharp
public class OrderConfiguration : IEntityTypeConfiguration<Order>
{
    public void Configure(EntityTypeBuilder<Order> builder)
    {
        builder.ToTable("Orders");
        builder.HasKey(x => x.Id);
        builder.Property(x => x.Status)
            .HasConversion<string>()
            .HasMaxLength(50);
        builder.HasMany(x => x.Items)
            .WithOne(x => x.Order)
            .HasForeignKey(x => x.OrderId);
    }
}
```

## Migration Standards
- Use `dotnet ef migrations add` for code-first migrations.
- Name migrations descriptively (e.g., `AddOrderStatusEnumConversion`).
- Review generated migration code before applying.
- Test migrations against PostgreSQL in CI via Testcontainers.

## Feature Module Standards
- Each feature lives in its own folder under `src/Code/Features/`.
- Include a `README.md` explaining the EF Core concept being demonstrated.
- Keep feature modules independent (avoid cross-feature coupling).
- Register feature services via extension methods.
