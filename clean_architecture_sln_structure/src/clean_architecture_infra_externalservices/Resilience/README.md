# Resilience

## Purpose

Resilience policies for external calls: retries, timeouts, circuit breakers, bulkheads.

## Typical contents

- Policy definitions (Polly or built-in resilience)
- Policy registries / named policies
- Retry/backoff strategies

## Out of scope

- Use-case-specific branching logic

## Notes

Resilience is a technical concern; choose policies per client and document exceptions with ADRs.

## References

- https://learn.microsoft.com/en-us/dotnet/core/resilience/
- https://www.thepollyproject.org/
- https://github.com/App-vNext/Polly
