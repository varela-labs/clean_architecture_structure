# Naming Rules (Auditable Ruleset)

> This file contains naming rules aligned with Clean Architecture principles.

NAMING RULESET
Last updated: 2026-03-11

## General

- Names MUST communicate responsibility and architectural role.
- Names MUST avoid leaking framework mechanisms unless disambiguation is required.
- Prefer verb+noun for use cases; prefer business nouns for domain concepts.
- Avoid vague suffixes: Manager/Helper/Util/Common unless strictly necessary and documented.

## Domain

- Entities: Business noun, NO 'Entity' suffix (e.g., Order, BatchReceive).
- Value Objects: Business value name, NO 'ValueObject' suffix (e.g., Money, EmailAddress).
- Domain Events: MUST end with 'Event' and describe a past fact (e.g., OrderPlacedEvent).
- Repository Interfaces: MUST be I*Repository (e.g., IOrderRepository).
- Domain Services: SHOULD end with 'DomainService' and be used sparingly.
- Specifications: MUST end with 'Specification' and name by predicate.
- Exceptions: MUST end with 'Exception' and describe the violated invariant/rule.

## Application

- Commands: MUST end with 'Command' and be verb+noun (CreateOrderCommand).
- Queries: MUST end with 'Query' (GetOrderQuery, ListOrdersQuery).
- Handlers: MUST end with 'Handler' and match request name.
- Validators: MUST end with 'Validator' and match request name.
- DTOs: MUST end with 'Dto' (OrderDto, OrderListItemDto).
- Results: SHOULD end with 'Result' (CreateOrderResult).
- Ports/Interfaces: MUST start with 'I' and name capability (IEventPublisher, IClock).
- Behaviors: SHOULD end with 'Behavior' (ValidationBehavior).

## Infrastructure.Data

- DbContext: MUST end with 'DbContext' (AppDbContext).
- EF mappings: SHOULD end with 'Configuration' (OrderConfiguration).
- Repository implementations: MUST end with 'Repository'; prefix with mechanism if multiple (EfOrderRepository).
- Outbox types: SHOULD make pattern explicit (OutboxMessage, OutboxDispatcher).

## Infrastructure.Caching

- Providers: SHOULD end with 'CacheProvider' (MemoryCacheProvider).
- Key builders: SHOULD end with 'CacheKeyBuilder'.
- Decorators: SHOULD end with 'Decorator' (MetricsCacheProviderDecorator).

## Infrastructure.Externalservices

- Typed clients: SHOULD end with 'Client' (PaymentsHttpClient / CustomerProfileClient).
- Port implementations: SHOULD end with 'Adapter' or 'Gateway' (PaymentsGatewayAdapter).
- External provider schemas: SHOULD end with 'Contract' or be clearly scoped (Payments...RequestContract).
- Auth helpers: name by mechanism (OAuthTokenProvider, HmacRequestSigner).
- Resilience: name by client/capability (PaymentsResiliencePolicy).

## Infrastructure.Ioc

- Registration entry points: use 'AddXyz' method naming; classes like 'DependencyInjectionConfiguration' or '*Extensions'.
- Modules: MUST end with 'Module' (DataModule, CachingModule).
- Options POCOs: SHOULD end with 'Options' (DatabaseOptions).

## Presentation

- Controllers: MUST end with 'Controller' (OrdersController).
- HTTP transport models: MUST end with 'Request'/'Response' (CreateOrderRequest).
- Middleware: MUST end with 'Middleware'.
- Background services: MUST end with 'HostedService'.
- Messaging: MUST use 'Consumer' for broker reception and 'Processor' for dispatch mapping.
