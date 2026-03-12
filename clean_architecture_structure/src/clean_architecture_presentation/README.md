# Presentation Project Structure

This project is **Presentation / Delivery**. It hosts the application (ASP.NET Core) and exposes the system to the outside world:
HTTP endpoints and message-driven endpoints (e.g., RabbitMQ consumers). Keep this layer thin.

In Clean Architecture, Presentation is an **outermost layer**. It must remain thin: it translates incoming requests/messages into
Application input models and calls Application use cases.

## Responsibilities

- Host the ASP.NET Core application (startup, routing, middleware).
- Define **controllers** (or minimal APIs) that translate HTTP requests to use case requests.
- Define **message consumers/processors** that translate broker messages to use case requests.
- Handle transport concerns: authentication/authorization, exception mapping, request logging, correlation, metrics, health endpoints.

## Typical contents

- Controllers (HTTP endpoints) and API-specific models (if needed)
- Middleware for transport-level error handling and logging
- Authentication/authorization wiring at the edge
- Hosted services for background processing
- Messaging consumers/processors that call Application use cases
- Observability: metrics, tracing, correlation

## Out of scope (must not be here)

- Business rules and invariants (Domain)
- Use case orchestration logic (Application)
- Persistence details (Infra-Data) and external client implementations (Infra-ExternalServices)
- DI composition root beyond calling into Infra-IoC (avoid duplicating wiring here)
- Domain rules and entities modifications for transport needs
- Persistence or external client implementations (those are Infrastructure)
- Use case orchestration logic beyond request mapping

## Dependency rule

Presentation depends on Application (and the IoC wiring project). Inner layers must not depend on Presentation.

## Recommended references

- Clean Architecture (Dependency Rule): <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- ASP.NET Core fundamentals: <https://learn.microsoft.com/en-us/aspnet/core/>
- Controllers/Web API: <https://learn.microsoft.com/en-us/aspnet/core/web-api/>
- Middleware: <https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/>
- Hosted services: <https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services>
- Health checks: <https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks>
- Authentication: <https://learn.microsoft.com/en-us/aspnet/core/security/authentication/> / JWT Bearer: <https://learn.microsoft.com/en-us/aspnet/core/security/authentication/jwtbearer>
- RabbitMQ .NET client overview: <https://www.rabbitmq.com/dotnet.html>
- prometheus-net: <https://github.com/prometheus-net/prometheus-net>
- OpenTelemetry .NET: <https://opentelemetry.io/docs/languages/net/>
