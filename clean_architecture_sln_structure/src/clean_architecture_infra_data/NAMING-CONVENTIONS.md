# Infrastructure.Data - Naming conventions

Infrastructure.Data contains persistence **implementations** (EF Core, mappings, migrations). Naming should clarify what is persistence-specific vs contract/policy.

## DbContext

**Rule:** Suffix with `DbContext`.

✅ Preferred:

- `AppDbContext` or `DefaultDbContext`

**Rationale:** Clear EF boundary and discoverability.

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
