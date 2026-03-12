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
- Persistence Models (a.k.a. EF Entities)
- Repository implementations for Domain interfaces
- Migrations and provider setup
- Infrastructure query helpers

### PersistenceModels

This folder contains the **persistence models** (also referred to as *Persistence Models*) that represent the physical structure of the database (tables, columns, relationships) and are used by EF Core within this project. They are intentionally separated from the **Domain Entities** to prevent the domain layer from being polluted with infrastructure concerns such as auditing fields, soft delete flags, concurrency tokens, integration columns, legacy naming, or database-driven relationship structures that do not reflect real domain aggregates. Mapping between `PersistenceModels` and Domain Entities is handled within repositories or persistence adapters.

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
