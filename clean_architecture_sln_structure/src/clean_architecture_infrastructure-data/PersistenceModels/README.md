# PersistenceModels

This folder contains the **Persistence Models** used by EF Core to map the database structure (tables, columns, and relationships) within the `clean_architecture_infra_data` project.

## Purpose

In Clean Architecture / Hexagonal Architecture, the **Domain layer must remain independent of infrastructure concerns**.

Databases often introduce technical requirements such as:

- Auditing fields (`CreatedAt`, `UpdatedAt`, `RowVersion`)
- Soft delete flags (`IsDeleted`, `DeletedAt`)
- Integration or synchronization fields (`ExternalId`, `SyncStatus`)
- Legacy naming conventions
- Relationship structures that do not align with domain aggregate boundaries
- Concurrency tokens or database-specific constructs

To preserve domain purity, persistence models are separated from Domain Entities.

## Separation Principle

- **Domain Entities**
  - Represent business concepts
  - Contain invariants and behavior
  - Are persistence-agnostic
  - Live in `Domain/Entities`

- **Persistence Models**
  - Represent database structure
  - Contain technical persistence fields
  - May include navigation properties and foreign keys
  - Live in `Infrastructure Data/PersistenceModels`

Mapping between both models is performed inside repositories or persistence adapters.

## What Belongs Here

- EF Core persistence classes representing tables or views
- Navigation properties required for ORM mapping
- Foreign key properties
- Infrastructure-specific fields (audit, concurrency, integration)
- Persistence-only types strictly related to database mapping

Examples:

- `CustomerRecord`
- `OrderRecord`
- `OrderLineRecord`
- `InvoiceRecord`

## What Does NOT Belong Here

- Domain Entities
- Business rules or domain invariants
- Application DTOs
- API models
- Query/read models intended for UI (unless explicitly part of the data infrastructure design)

## Naming Convention

To avoid confusion with Domain Entities, persistence models must use an explicit suffix.

**Recommended:**

- `*Record`
- `CustomerRecord`
- `OrderRecord`

Alternative acceptable suffixes:

- `*DbModel`
- `*EfModel`
- `*Row`

Fluent API configuration classes should follow the same naming pattern:

- `CustomerRecordConfiguration`
- `OrderRecordConfiguration`

This explicit separation improves maintainability, architectural clarity, and long-term flexibility.
