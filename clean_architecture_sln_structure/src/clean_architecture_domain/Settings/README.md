# Settings

## Purpose

Domain-level ports for configuration/time/IDs when domain policy needs them. Interfaces only.

## Typical contents

- IClock
- IGuidGenerator
- IDomainSettings (if truly needed)

## Out of scope

- IOptions<> usage
- Concrete configuration classes bound to appsettings.json

## Notes

Prefer passing values from Application into Domain rather than letting Domain read configuration.
