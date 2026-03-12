# Application - Naming conventions

Application contains **use cases** and **boundary contracts**. Names must make the system's capabilities obvious (Screaming Architecture).

## Why Application naming matters

- This layer expresses **what the system does** (verbs).
- It is the primary navigation path for developers and reviewers.
- Clear suffixes reduce ambiguity because many request/response types coexist.

---

## Use Case folders

**Rule:** Organize by business capability (feature) and by intent.

Example structure:

- `UseCases/Orders/Create/`
- `UseCases/Orders/Get/`
- `UseCases/Orders/List/`

---

## Commands / Queries

**Rule:** Use **verb + noun** with role suffix.

✅ Preferred:

- `CreateOrderCommand`
- `CancelOrderCommand`
- `GetOrderQuery`
- `ListOrdersQuery`

❌ Avoid:

- `OrderCreate` (unclear role)
- `OrderService` (too generic)

**Rationale:** The suffix tells the reader how the request flows through the system.

---

## Handlers

**Rule:** Suffix with `Handler` and match the request name.

✅ Preferred:

- `CreateOrderHandler` handles `CreateOrderCommand`
- `GetOrderHandler` handles `GetOrderQuery`

**Rationale:** Predictability improves discoverability and tooling navigation.

---

## Validators

**Rule:** Suffix with `Validator`, match the request name.

✅ Preferred:

- `CreateOrderValidator`

**Rationale:** Validators act at the boundary of the use case.

---

## DTOs

**Rule:** Suffix with `Dto` and scope by use case intent.

✅ Preferred:

- `OrderDto`
- `OrderListItemDto`
- `CreateOrderInputDto` (when you want explicit input model)
- `CreateOrderOutputDto` (when you want explicit output model)

❌ Avoid:

- `OrderModel` (ambiguous)
- `OrderEntity` (domain type)

**Rationale:** DTOs are boundary shapes, not domain objects.

---

## Results

**Rule:** Use `Result` / `Result<T>` or named result types, suffix with `Result`.

✅ Preferred:

- `CreateOrderResult`
- `ListOrdersResult`

**Rationale:** Results communicate success/failure and return payload shape.

---

## Ports (interfaces)

**Rule:** Prefix with `I`, name by capability.

✅ Preferred:

- `IEventPublisher`
- `IExternalPaymentGateway`
- `IClock`

**Rationale:** Dependency Inversion — Application owns what it needs.

---

## Behaviors / pipeline

**Rule:** Suffix with `Behavior` (if using MediatR pipeline).

✅ Preferred:

- `ValidationBehavior`
- `IdempotencyBehavior`

---

## Exceptions

**Rule:** Use case boundary failures: `NotFoundException`, `InvalidRequestException`, etc.

**Rationale:** Presentation maps these to transport errors.

---

## Quick checklist

- Does the name read like a business capability (Create, Cancel, Get, List)?
- Does the suffix make the role obvious (Command/Query/Handler/Dto)?
