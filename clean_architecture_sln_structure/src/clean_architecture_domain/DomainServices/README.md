# DomainServices

## Purpose
Domain services: business operations that don't fit naturally inside a single entity/value object.

## Typical contents
- Pure domain algorithms
- Policy that coordinates multiple entities (without infrastructure)

## Out of scope
- Use-case orchestration (belongs to Application)
- Calling repositories or external systems directly

## Notes
Keep services small. If it needs persistence or IO, define an interface (port) and let outer layers implement it.


