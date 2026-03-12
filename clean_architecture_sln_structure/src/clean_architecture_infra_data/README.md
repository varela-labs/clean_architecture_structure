# Infrastructure Data Project Structure

This project is **Infrastructure (Data)**. It contains **database and persistence details** (EF Core, provider configuration, migrations, and repository implementations). Keep it isolated from business policy.

In Clean Architecture, Infrastructure is an **outer layer**: it must not contain business policy. It implements the **ports/contracts** owned by the inner layers (Domain/Application).

## Responsibilities

- Implement **Domain repository interfaces** (and/or Application persistence ports) using EF Core.
- Configure EF Core: DbContext, mappings, migrations, provider options (PostgreSQL/Npgsql).
- Provide persistence utilities (paging, query helpers) as infrastructure details.

## Typical contents

- DbContext and EF Core configuration
- Entity mapping configurations
- Repository implementations for Domain interfaces
- Migrations and provider setup
- Infrastructure query helpers

## Out of scope (must not be here)

- Use case orchestration (Application concern)
- Domain rules/invariants (Domain concern)
- Web/API concerns (Presentation concern)
- Messaging broker code (RabbitMQ consumer/publisher)
- Domain entities/VOs (except as referenced types)
- Application use cases and orchestration
- HTTP controllers/middleware
- Broker SDK usage

## Dependency rule

Infrastructure depends on **Domain** (and sometimes Application if it implements Application ports).
Domain/Application must not depend on this project.

## Recommended references

- Clean Architecture (Dependency Rule): <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- EF Core documentation: <https://learn.microsoft.com/en-us/ef/core/>
- IDbContextFactory guidance: <https://learn.microsoft.com/en-us/ef/core/dbcontext-configuration/#using-idbcontextfactory>
- EF Core migrations: <https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/>
- Npgsql EF Core provider: <https://www.npgsql.org/efcore/>
- Repository pattern (general): <https://learn.microsoft.com/en-us/azure/architecture/patterns/repository>
