# UseCases/_Shared

## Purpose

Shared helpers for use case handlers to avoid duplication while keeping methods small.

## Typical contents

- Base handler helpers (small, focused)
- Common query pagination helpers
- Guard clauses and mapping helpers (if not in Common)

## Out of scope

- Generic 'God' base classes with too much logic

## Notes

Keep this folder lean. If a helper is feature-specific, keep it inside the feature folder.
