# Observability

## Purpose

Logging/metrics/tracing helpers at the transport edge.

## Typical contents

- Correlation ID conventions
- Metrics decorators (hit/miss, processing duration)
- Tracing helpers (ActivitySource, OpenTelemetry)

## Out of scope

- Hosting of exporters/servers (keep actual hosting setup in Program/Startup)
- Business policy metrics inside Domain

## Notes

Instrument at boundaries: HTTP and message processing are excellent points for telemetry.

## References

- <https://opentelemetry.io/docs/languages/net/>
- <https://github.com/prometheus-net/prometheus-net>
