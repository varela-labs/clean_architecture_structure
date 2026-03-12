# Observability/Logging

## Purpose

Logging helpers and conventions for the hosting edge.

## Typical contents

- Structured logging helpers
- Log scopes for correlation
- PII-safe logging conventions

## Out of scope

- Logging framework configuration (keep in Program/Startup or environment config)

## Notes

Prefer structured logs. Avoid logging secrets or sensitive payloads.

## References

- <https://learn.microsoft.com/en-us/dotnet/core/extensions/logging>
