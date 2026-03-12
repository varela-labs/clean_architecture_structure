# Infrastructure IoC Project Structure

This project is **Infrastructure (IoC / Composition)**. It contains the **composition root**: the place where we wire
interfaces (ports) to concrete implementations and build the application's object graph. Registering dependencies and exposing registration entry points to the hosting layer.

In Clean Architecture, the composition root lives in the **outermost layer**. Inner layers (Domain/Application) must not
reference DI containers or perform service location.

## Responsibilities

- Register services in the DI container (ports -> adapters).
- Bind configuration options (settings POCOs) and expose them via interfaces if needed.
- Centralize module-based registrations (Data, Caching, ExternalServices, Messaging adapters).
- Provide extension methods used by the hosting layer (Presentation) to add dependencies.

## Typical contents

- DI registration modules
- Options binding and validation (optional)
- Registration extension methods
- Health check registrations (wiring only)

## Out of scope (must not be here)

- Business policy (Domain/Application)
- EF Core DbContext, repository implementations (Infra-Data)
- Cache provider implementations (Infra-Caching)
- External HTTP clients/SDK implementations (Infra-ExternalServices)
- Web routing/controllers/middleware (Presentation)
- Concrete implementations (repositories, caches, clients) — those live in other Infrastructure projects
- Use case code (Application) and domain rules (Domain)

## Dependency rule

This project may reference Infrastructure projects and inner layers to wire everything together.
Inner layers must not reference this project.

## Recommended references

- Clean Architecture (Dependency Rule): https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- .NET Dependency Injection: https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection
- Options pattern: https://learn.microsoft.com/en-us/dotnet/core/extensions/options
- Composition Root concept (Martin Fowler): https://martinfowler.com/articles/injection.html
- ASP.NET Core DI fundamentals: https://learn.microsoft.com/en-us/aspnet/core/fundamentals/dependency-injection
