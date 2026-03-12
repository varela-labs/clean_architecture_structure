# Context/Factories

## Purpose
Factories for creating DbContext instances (e.g., IDbContextFactory) for safe usage in repositories/background jobs.

## Typical contents
- IDbContextFactory<DbContext> implementations
- IDesignTimeDbContextFactory for migrations tooling

## Out of scope
- Service registration (belongs in Infra-IoC)
- Hard-coded secrets/connection strings

## Notes
Use factories to avoid leaking DbContext lifetimes across async boundaries and to support background processing.

## References
- https://learn.microsoft.com/en-us/ef/core/dbcontext-configuration/#using-idbcontextfactory
- https://learn.microsoft.com/en-us/ef/core/managing-schemas/migrations/


