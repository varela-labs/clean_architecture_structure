# Infrastructure External Services Project Structure

This project is **Infrastructure (External Services)**. It contains adapters that integrate with **external systems**:
HTTP APIs, SOAP services, SDKs, or any third-party dependency that involves I/O. Keep all I/O and third-party concerns isolated and replaceable.

In Clean Architecture, external service calls are **details**. The **Application/Domain** define what they need via interfaces (ports),
and Infrastructure provides the concrete implementations.

## Responsibilities

- Implement external service ports (interfaces) owned by Application/Domain.
- Provide typed HTTP/SOAP clients and SDK wrappers.
- Handle technical concerns: auth headers, serialization, retries/timeouts, resilience, and telemetry.

## Typical contents

- Typed clients (HTTP/SOAP/SDK wrappers)
- Auth/credentials and request signing helpers (infrastructure-only)
- Serialization and contract mapping
- Resilience policies (retries, timeouts, circuit breakers)
- Telemetry instrumentation

## Out of scope (must not be here)

- Use case orchestration (Application concern)
- Domain rules/invariants (Domain concern)
- Web/API controllers and middleware (Presentation concern)
- DI composition root (Infra-IoC owns registrations)
- Business decisions (what to call and when) — belongs to Application use cases
- Controllers/middleware — belongs to Presentation
- DI composition root — belongs to Infra-IoC

## Dependency rule

Infrastructure depends on Domain/Application. Inner layers must not depend on this project.

## Recommended references

- Clean Architecture (Dependency Rule): <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- IHttpClientFactory: <https://learn.microsoft.com/en-us/dotnet/core/extensions/httpclient-factory>
- .NET resilience overview: <https://learn.microsoft.com/en-us/dotnet/core/resilience/>
- Polly (resilience library): <https://www.thepollyproject.org/> / <https://github.com/App-vNext/Polly>
- OpenTelemetry .NET: <https://opentelemetry.io/docs/languages/net/>
- Logging in .NET: <https://learn.microsoft.com/en-us/dotnet/core/extensions/logging>
- Options pattern: <https://learn.microsoft.com/en-us/dotnet/core/extensions/options>
