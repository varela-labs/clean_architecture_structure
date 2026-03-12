# Entities

## Purpose
Domain entities: objects with identity and lifecycle. Entities enforce business invariants.

## Typical contents
- Aggregate roots and child entities
- Entity methods that guard invariants
- Factory methods for valid creation

## Out of scope
- DTOs/view models
- EF mapping attributes or configuration
- Repository implementations

## Notes
If a type has no identity and is defined by values, it likely belongs in ValueObjects.


