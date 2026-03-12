# Outbox

## Purpose
Optional: persistence support for the Outbox pattern to reliably publish domain/application events.

## Typical contents
- Outbox table entity/mapping (infrastructure-only)
- Outbox repository/dispatcher helpers (infrastructure-only)

## Out of scope
- Broker publishing code (that belongs in a Messaging project or Presentation adapters)
- Domain event definitions (they live in Domain)

## Notes
If you adopt Outbox, document it with an ADR and keep publishing concerns outside this project.

## References
- https://learn.microsoft.com/en-us/azure/architecture/patterns/transactional-outbox


