# HealthChecks

## Purpose
Health check endpoints and registration glue used by the hosting layer.

## Typical contents
- Health check endpoint mapping and tags
- Readiness/liveness separation (optional)

## Out of scope
- Business logic
- Complex probes that alter state

## Notes
Health checks should be fast and safe. Prefer wiring checks defined in Infra-IoC.

## References
- https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks


