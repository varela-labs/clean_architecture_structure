# Presentation - Naming conventions

Presentation is the **delivery layer** (HTTP + messaging). Names should make endpoints and message entry points obvious and keep this layer thin.

## Controllers

**Rule:** Suffix with `Controller`, pluralized resource naming is OK.

✅ Preferred:

- `OrdersController`
- `BatchReceivesController`

**Rationale:** Aligns with ASP.NET Core conventions and discoverability.

---

## HTTP request/response models

**Rule:** Use `Request` / `Response` suffix to avoid mixing with Application DTOs.

✅ Preferred:

- `CreateOrderRequest`
- `OrderResponse`

**Rationale:** Transport models are volatile and should not leak inward.

---

## Middleware

**Rule:** Suffix with `Middleware`.

✅ Preferred:

- `ExceptionHandlingMiddleware`
- `CorrelationIdMiddleware`

---

## Hosted services

**Rule:** Suffix with `HostedService`.

✅ Preferred:

- `MessagePumpHostedService`
- `OutboxPublisherHostedService`

---

## Messaging consumers and processors

**Rule:** Treat consumers like controllers. Use `Consumer` for broker reception and `Processor` for message-to-use-case translation.

✅ Preferred:

- `OrderCreatedConsumer`
- `OrderCreatedProcessor`

**Rationale:** Separates broker mechanics (consumer) from mapping/dispatch (processor).

---

## Observability

**Rule:** Name by concern: `Metrics`, `Logging`, `Tracing`.

✅ Preferred:

- `PrometheusMetricsSetup`
- `RequestLoggingSetup`

---

## Quick checklist

- Can you tell if a type is HTTP, broker messaging, middleware, or hosting?
- Do names avoid embedding business logic vocabulary that belongs in Application/Domain?
