# Extensions

## Purpose

Infrastructure extensions related to persistence (query helpers, paging, projections).

## Typical contents

- IQueryable extensions for paging (e.g., ToPagedListAsync)
- EF Core query helpers

## Out of scope

- Extensions that implement business rules (policy belongs in Domain/Application)

## Notes

Be careful: complex query logic can become hidden policy. Keep it technical (paging, includes) and document exceptions.
