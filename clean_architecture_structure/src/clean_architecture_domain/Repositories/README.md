# Repositories

## Purpose

Repository interfaces: domain-level persistence/query contracts. Implementations live in Infrastructure.

## Typical contents

- IBatchReceiveRepository (example)
- IUnitOfWork (if used)
- Small, purpose-driven repository interfaces

## Out of scope

- EF Core DbContext, migrations
- SQL queries or ORM expressions tied to a provider

## Notes

Interfaces should be owned by the domain policy. Keep them minimal and aligned to use cases.
