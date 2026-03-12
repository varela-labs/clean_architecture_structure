# Repositories

## Purpose

Concrete implementations of Domain repository interfaces using EF Core and the configured provider.

## Typical contents

- Repository implementations (e.g., BatchReceiveRepository)
- Query methods using EF Core LINQ
- Unit of Work implementation if required by the Domain contract

## Out of scope

- Repository interfaces (they live in Domain by our decision)
- Use case orchestration (Application)

## Notes

Keep repositories focused on persistence details and data retrieval/storage. Do not embed business rules.

## References

- <https://learn.microsoft.com/en-us/azure/architecture/patterns/repository>
- <https://learn.microsoft.com/en-us/ef/core/>
