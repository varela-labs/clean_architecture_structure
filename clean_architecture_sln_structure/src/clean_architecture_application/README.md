# Application Project Structure

This project is the **Application** layer. It contains **application-specific business rules** (use cases) and the **boundaries/ports** that isolate the core policy from delivery and infrastructure details.

> In Clean Architecture terms: this is where **use cases** live and orchestrate Domain objects without knowing about frameworks, databases, HTTP, or message brokers.

## Dependency rule

Application depends on **Domain**. Outer layers depend on Application.

## Responsibilities

- Define **use case interactors** (commands/queries) and their handlers.
- Define **input/output models** and boundary contracts (DTOs, result models).
- Define **ports** (interfaces) the application needs (messaging, time, external services), implemented by outer layers.
- Define **cross-cutting policies** as behaviors (validation, logging abstraction, etc.) without framework coupling.

## Typical contents

- Use case handlers (commands/queries) organized by feature
- Application ports (interfaces) for external dependencies
- Validation and pipeline behaviors
- DTOs/Contracts and result models

## Out of scope (must not be here)

- Web controllers, middleware, filters, or transport bindings
- EF Core DbContext/migrations/mapping configurations
- RabbitMQ client code (consumers/publishers)
- Message broker client code and topology configuration
- DI container registrations / composition root
- Concrete HTTP clients, cloud SDKs, etc

## Recommended references

- Clean Architecture (The Dependency Rule): <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- MediatR (Mediator pattern for use-case dispatching): <https://github.com/LuckyPennySoftware/MediatR> / <https://mediatr.io/>
- FluentValidation (validation rules and patterns): <https://docs.fluentvalidation.net/>
- AutoMapper (mapping between models): <https://docs.automapper.io/en/stable/> / <https://github.com/LuckyPennySoftware/AutoMapper>
