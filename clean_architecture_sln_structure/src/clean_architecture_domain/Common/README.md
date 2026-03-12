# Common

## Purpose

Shared domain building blocks used across multiple domain types. Keep this small and stable.

## Typical contents

- Base types (Entity, AggregateRoot)
- ValueObject base and primitives
- Domain exceptions
- Result/Error types

## Out of scope

- Anything feature-specific
- Framework or infrastructure concerns

## Notes

Prefer cohesion: only place items here when multiple domain concepts truly need them.
