# Contracts

## Purpose

Boundary data structures that cross into/out of Application. Keep them simple and stable.

## Typical contents

- DTOs for requests/responses (not EF entities)
- Error shapes used inside the application boundary
- Paginated/list result models

## Out of scope

- ASP.NET Core ActionResult or controller models
- Serialization attributes tied to a specific transport (unless explicitly accepted)

## Notes

Avoid exposing Domain entities directly to the outside world. Use contracts tailored to use cases.
