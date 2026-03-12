# EntityConfigurations

## Purpose
EF Core mapping configurations that describe how Domain entities are persisted.

## Typical contents
- IEntityTypeConfiguration<T> implementations
- Table/column mapping, indexes, constraints
- Value object conversions (if needed)

## Out of scope
- Attributes on Domain entities (prefer Fluent configuration to keep Domain clean)

## Notes
Prefer Fluent API mappings here instead of attributes on Domain models to keep the core framework-free.

## References
- https://learn.microsoft.com/en-us/ef/core/


