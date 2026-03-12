# Infrastructure.Data - Naming conventions

Infrastructure.Data contains persistence **implementations** (EF Core, mappings, migrations). Naming should clarify what is persistence-specific vs contract/policy.

## DbContext

**Rule:** Suffix with `DbContext`.

✅ Preferred:

- `AppDbContext` or `DefaultDbContext`

**Rationale:** Clear EF boundary and discoverability.

---

## Persistence Models (EF Core) — `PersistenceModels/`

Types located under `PersistenceModels` represent the **database persistence structure** and must not be confused with `Domain/Entities`.

Because the solution contains two conceptual “entity” layers (Domain Entities and persistence-level entities), naming must be explicit and unambiguous.

### Naming Convention

Persistence models must use a clear suffix:

**Recommended suffix:** `Record`

Examples:

- `CustomerRecord`
- `OrderRecord`
- `InvoiceRecord`
- `ProductRecord`

Alternative acceptable suffixes (if required by team standards):

- `DbModel` (e.g., `CustomerDbModel`)
- `EfModel` (e.g., `OrderEfModel`)
- `Row` (e.g., `InvoiceRow`)

### Rules

- Domain Entities must NOT use a suffix and must live in `Domain/Entities`.
- Persistence models MUST use a suffix and must live in `InfrastructureData/PersistenceModels`.
- Fluent API configuration classes should mirror the name:
  - `CustomerRecordConfiguration`
  - `OrderRecordConfiguration`

This convention ensures architectural clarity and prevents ambiguity when navigating or refactoring the solution.

---

## EF mappings

**Rule:** Suffix with `Configuration` (or `EntityConfiguration`) for `IEntityTypeConfiguration<T>` implementations.

✅ Preferred:

- `OrderConfiguration`
- `BatchReceiveConfiguration`

**Rationale:** Keeps Domain clean (Fluent mappings live here).

---

## Repository implementations

**Rule:** Suffix with `Repository`. If multiple implementations exist, prefix with mechanism.

✅ Preferred:

- `OrderRepository` (single implementation)
- `EfOrderRepository` (when you also have `InMemoryOrderRepository`)

**Rationale:** Infrastructure can be technical; the name should expose the adapter type.

---

## Unit of Work

**Rule:** If you implement it: `UnitOfWork` (implementation), `IUnitOfWork` (contract in Domain).

---

## Migrations

**Rule:** Leave EF-generated names as-is, but avoid mixing custom business logic in migration classes.

---

## Outbox (optional)

- `OutboxMessage` (table entity)
- `OutboxDispatcher` (infrastructure job)
- `OutboxRepository`

**Rationale:** Make the pattern explicit.

---

## Quick checklist

- Can a reader instantly tell this is EF/persistence detail?
- Are Domain names untouched (no leakage of `Db*` or `Table*` into Domain)?
