# Solution-wide - Naming conventions

This document defines naming conventions for the **Clean Architecture** solution.

## Goals

Names should:

1. **Communicate purpose**: what the type is and what role it plays in the architecture.
2. **Stay stable when implementation changes**: avoid names that leak frameworks or infrastructure choices.
3. **Make boundaries obvious**: help readers instantly recognize layer ownership (Domain/Application/Infrastructure/Presentation).
4. **Improve auditability**: enable automated checks (including AI audits) to spot boundary leaks and misplaced responsibilities.

> Guiding principle: **Name by responsibility, not by mechanism.**  
> Example: prefer `OrderPublisher` (role) over `RabbitMqOrderPublisher` (mechanism), unless there are multiple mechanisms in the same scope and disambiguation is required.

---

## Conventions by layer (high level)

### Domain

Use **business language**. Avoid technical suffixes unless they represent a **business concept** (e.g., Event).

- Entities: `Order`, `BatchReceive`
- Value Objects: `Money`, `EmailAddress`, `Quantity`
- Domain Events: `OrderPlacedEvent`, `BatchReceiveCreatedEvent`
- Domain Services: `PricingDomainService`, `BatchReceiveDomainService` (only when needed)
- Repository Interfaces (ports): `IOrderRepository`, `IBatchReceiveRepository`
- Specifications: `ActiveOrdersSpecification`, `BatchReceiveByDateSpecification`
- Exceptions: `InvalidEmailAddressException`, `BusinessRuleViolationException`

### Application

Name by **use case intent** and **request/handler role**.

- Commands: `CreateOrderCommand`, `CancelOrderCommand`
- Queries: `GetOrderQuery`, `ListOrdersQuery`
- Handlers: `CreateOrderHandler`, `GetOrderHandler`
- Validators: `CreateOrderValidator`
- DTOs: `OrderDto`, `OrderListItemDto`
- Results: `CreateOrderResult`, `ListOrdersResult`
- Ports (interfaces): `IExternalPaymentGateway`, `IEventPublisher`, `IClock`

### Infrastructure

Name by **adapter responsibility**. It’s OK to be more technical here, but still prefer role-first naming.

- EF: `AppDbContext`, `OrderEntityConfiguration`, `EfOrderRepository`
- Caching: `MemoryCacheProvider`, `DistributedCacheProvider`
- External Services: `PaymentsHttpClient`, `PaymentsGatewayAdapter`
- Messaging: `RabbitMqPublisher` (when broker choice is essential in this project)
- Serialization: `JsonSerializerAdapter`, `XmlSerializerAdapter`

### Presentation

Name by **delivery mechanism role**.

- Controllers: `OrdersController`
- HTTP Models: `CreateOrderRequest`, `OrderResponse`
- Middleware: `ExceptionHandlingMiddleware`, `CorrelationIdMiddleware`
- Messaging: `OrderCreatedConsumer`, `OrderCreatedProcessor`
- Hosted services: `MessagePumpHostedService`

---

## Standard suffixes and when to use them

### Suffixes strongly recommended (common and unambiguous)

- `Command`, `Query`, `Handler`, `Validator`
- `Dto`, `Result`, `Request`, `Response`
- `Controller`, `Middleware`, `Consumer`, `Processor`
- `DbContext`, `Configuration` (EF mapping), `Repository` (implementation)
- `DomainService`, `Specification`, `Event`

### Suffixes to avoid unless necessary

- `Manager`, `Helper`, `Util`, `Common`, `Base`  
Prefer names that express the behavior: `CorrelationIdProvider` over `CorrelationHelper`.

### “Implementation” names

If the same role has multiple implementations in the same scope, disambiguate by mechanism:

- `InMemoryUserRepository` vs `EfUserRepository`
- `RabbitMqEventPublisher` vs `InProcessEventPublisher`

If there is only one, prefer the role name:

- `EventPublisher` (implementation detail stays in DI registration)

---

## Interface naming

- Prefix interfaces with `I`: `IClock`, `IOrderRepository`
- Use capability nouns: `IEventPublisher`, `IIdGenerator`
- Avoid generic “service” interfaces: prefer `ICustomerReadModel` or `IOrderNumberGenerator`

---

## Generic and base types

- Base types should be specific and minimal: `Entity<TId>`, `AggregateRoot<TId>`
- Avoid deep inheritance trees named `BaseXyzService` unless they are truly small and stable.

---

## Folder-to-name alignment

Folder names reinforce meaning. Prefer:

- `Entities/Order.cs`, not `Entities/OrderEntity.cs`
- `UseCases/Orders/Create/CreateOrderCommand.cs`
- `Messaging/Consumers/OrderCreatedConsumer.cs`

---

## Review checklist (human + AI)

- Can a reader tell **layer** and **role** from the type name?
- Does the name remain correct if we swap EF ↔ another ORM or RabbitMQ ↔ another broker?
- Are use case names written in **verb + noun** form (e.g., CreateOrder)?
- Are “transport models” (HTTP, broker message contracts) clearly labeled and kept out of Domain?
