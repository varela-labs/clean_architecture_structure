# Telemetry

## Purpose

Instrumentation for external calls: tracing, metrics, logging correlation.

## Typical contents

- OpenTelemetry instrumentation helpers
- ActivitySource configuration (infrastructure-side)
- Client metrics decorators

## Out of scope

- Hosting of metrics endpoints (Presentation concern)

## Notes

Expose telemetry via standard instrumentation so hosting layer can export it to the chosen backend.

## References

- <https://opentelemetry.io/docs/languages/net/>
- <https://learn.microsoft.com/en-us/dotnet/core/extensions/logging>
