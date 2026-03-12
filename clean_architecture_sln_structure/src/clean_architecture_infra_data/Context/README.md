# Context

## Purpose
EF Core DbContext and related persistence context infrastructure.

## Typical contents
- DbContext (e.g., DefaultDbContext)
- OnModelCreating applying configurations
- Connection configuration helpers (infrastructure-level)

## Out of scope
- Business rules in DbContext (policy belongs in Domain/Application)

## Notes
Keep DbContext focused on persistence configuration. Avoid adding business logic here.

## References
- https://learn.microsoft.com/en-us/ef/core/


