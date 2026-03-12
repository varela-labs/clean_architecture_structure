# Domain - Naming conventions

Domain is the **core policy**. Names must be **business-first** and should read like a domain language glossary.

## Why Domain naming is different

- Domain should remain valid even if we replace frameworks, databases, and message brokers.
- Technical suffixes add noise because the **folder already provides context** (e.g., `Entities/`).
- Domain names should help discover business rules and invariants quickly.

---

## Entities

**Rule:** Entities are named as **business nouns** (no `Entity` suffix).

✅ Preferred:

- `Order`
- `BatchReceive`
- `Customer`

❌ Avoid:

- `OrderEntity` (redundant)
- `TblOrder` (DB detail)
- `OrderModel` (ambiguous)

**Rationale:** In Domain, an entity *is* the concept; the suffix adds no meaning.

---

## Value Objects

**Rule:** Value objects use **business value names**, ideally reflecting the ubiquitous language.

✅ Preferred:

- `Money`
- `EmailAddress`
- `Quantity`
- `PlateNumber`

❌ Avoid:

- `MoneyVO` (technical)
- `EmailString` (leaks primitive)
- `EmailDto` (boundary type)

**Rationale:** Value objects protect invariants; names should encourage usage over primitives.

---

## Domain Events

**Rule:** Suffix with `Event` and use a **past tense** / “something happened” wording.

✅ Preferred:

- `OrderPlacedEvent`
- `BatchReceiveCreatedEvent`

❌ Avoid:

- `PlaceOrderEvent` (sounds like a command)
- `OrderCreatedMessage` (transport detail)

**Rationale:** Events are facts, not requests.

---

## Repository Interfaces (ports)

**Rule:** Prefix with `I`, suffix with `Repository`.

✅ Preferred:

- `IOrderRepository`
- `IBatchReceiveRepository`

**Rationale:** Domain owns the contract; Infrastructure provides implementations.

---

## Domain Services

**Rule:** Only when behavior cannot naturally live in an entity/value object. Suffix with `DomainService`.

✅ Preferred:

- `PricingDomainService`

❌ Avoid:

- `OrderService` (too generic)
- `OrderManager` (unclear responsibility)

**Rationale:** Keeps SRP and avoids “god services”.

---

## Specifications

**Rule:** Suffix with `Specification` and name by predicate.

✅ Preferred:

- `ActiveOrdersSpecification`
- `BatchReceiveByDateSpecification`

**Rationale:** Specs encode reusable business criteria.

---

## Exceptions

**Rule:** Name by violated rule/invariant. Suffix with `Exception`.

✅ Preferred:

- `InvalidEmailAddressException`
- `BusinessRuleViolationException`

**Rationale:** Exceptions become documentation.

---

## IDs and strong typing

If you adopt strongly-typed IDs:

- `OrderId`, `CustomerId` (not `OrderID`)

---

## Quick checklist

- Would this name still make sense if EF/RabbitMQ/ASP.NET disappeared?
- Does it read like a business term from a domain glossary?
