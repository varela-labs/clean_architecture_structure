# Common

## Purpose
Infrastructure-only helpers used by persistence adapters.

## Typical contents
- UnitOfWork implementation
- PagedList implementations
- Database initialization helpers (if accepted)

## Out of scope
- Domain primitives (they live in Domain)
- General utilities that should be in SharedKernel

## Notes
Keep infrastructure helpers private to Infrastructure. If reused across infrastructure projects, consider a separate infra-shared project later.


