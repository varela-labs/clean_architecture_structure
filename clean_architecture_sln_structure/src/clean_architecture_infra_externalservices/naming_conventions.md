# Infrastructure.ExternalServices - Naming conventions

Infrastructure.ExternalServices integrates with third-party systems. Names should protect the core from volatile external schemas and mechanisms.

## Clients

**Rule:** Suffix with `Client` for typed clients, and name by external system.

✅ Preferred:

- `PaymentsHttpClient`
- `CustomerProfileClient`

**Rationale:** Makes it clear this is I/O and external dependency.

---

## Adapters / gateways

**Rule:** For implementations of an inner-layer port, use `Adapter` or `Gateway`.

✅ Preferred:

- `PaymentsGatewayAdapter` implements `IExternalPaymentGateway`

**Rationale:** The word “adapter” signals boundary translation.

---

## External contracts

**Rule:** Keep external schemas separate and name by provider context.

✅ Preferred:

- `PaymentsCreateChargeRequestContract`
- `PaymentsCreateChargeResponseContract`

**Rationale:** Avoid leaking provider DTOs into Application/Domain.

---

## Auth helpers

**Rule:** Name by technical responsibility.

✅ Preferred:

- `OAuthTokenProvider`
- `HmacRequestSigner`

---

## Resilience policies

**Rule:** Name policies by client or capability.

✅ Preferred:

- `PaymentsResiliencePolicy`

---

## Quick checklist

- Do names make it obvious which types are “provider contracts” vs “internal contracts”?
- Could we swap providers without changing Application/Domain names?
