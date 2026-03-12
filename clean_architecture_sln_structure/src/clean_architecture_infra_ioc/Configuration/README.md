# Configuration

## Purpose
Configuration utilities for IoC wiring: binding, validation, environment switches (wiring only).

## Typical contents
- Options validation helpers
- Configuration binding helpers

## Out of scope
- Concrete settings consumed directly by inner layers
- Secrets management implementation

## Notes
Prefer binding settings here and exposing strongly-typed options to outer layers; inner layers should depend on abstractions.

## References
- https://learn.microsoft.com/en-us/dotnet/core/extensions/options


