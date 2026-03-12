# Domain Project Structure

This project is the **Domain** of the solution. It contains the **core business policy**: enterprise rules, domain models, and contracts that the rest of the system must respect. It is organized to keep business policy explicit and framework-free.

## Typical contents (What belongs here)

- **Entities**: business objects with identity and lifecycle.
- **Value Objects**: immutable types defined by their values (no identity).
- **Domain Events**: facts about something meaningful that happened in the domain.
- **Domain Services**: business operations that don't naturally belong to a single Entity or Value Object.
- **Repository Interfaces**: *contracts* that express what the domain needs for persistence/querying (implementations live outside the Domain).
- **Specifications**: reusable business predicates/criteria (kept persistence-agnostic).
- **Settings/Ports (interfaces only)**: domain-level abstractions for time, IDs, configuration needed by policy.
- Domain model types (entities, value objects)
- Domain events and domain services
- Repository interfaces and domain ports
- Shared domain primitives and base types

## Out of scope (What must NOT belong here)

- Frameworks (ASP.NET Core, EF Core, RabbitMQ client libraries, logging frameworks, DI containers)
- Infrastructure details (SQL/ORM mappings, migrations, HTTP clients, message brokers)
- Transport-specific types (ActionResult, HttpContext, DTOs tied to API contracts)
- EF Core mappings, DbContext, migrations
- ASP.NET Core controllers/middleware
- RabbitMQ consumers/publishers
- Any DI container registrations

## Dependency rule

The Domain **depends on nothing** outside itself. Other projects may depend on Domain, but Domain must not reference them.

## Naming conventions

Folder names follow common Clean Architecture + DDD terminology (Entity, Value Object, Domain Event, etc.). Names are chosen to make the architecture "scream" business intent rather than framework details.

### Last updated: 2026-03-11
