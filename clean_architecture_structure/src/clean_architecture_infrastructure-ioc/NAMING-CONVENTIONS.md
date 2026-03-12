# Infrastructure.IoC - Naming conventions

Infrastructure.IoC is the **composition root** for wiring dependencies. Names should communicate registration intent and module boundaries.

## Entry points

**Rule:** Use clear verbs for DI registration entry points.

✅ Preferred:

- `DependencyInjectionConfiguration`
- `InfrastructureServiceCollectionExtensions`

Methods:

- `AddInfrastructure(...)`
- `AddPersistence(...)`

**Rationale:** Hosting layer should read like a checklist.

---

## Modules

**Rule:** Suffix with `Module` and name by capability.

✅ Preferred:

- `DataModule`
- `ExternalServicesModule`
- `MessagingModule`

**Rationale:** Prevents a single “god” registration file.

---

## Options / settings

**Rule:** Suffix with `Options` for POCO settings models.

✅ Preferred:

- `DatabaseOptions`
- `MessageBrokerOptions`

**Rationale:** Standard .NET naming, easy to search.

---

## Health checks wiring

**Rule:** Name by target system.

✅ Preferred:

- `DatabaseHealthChecksRegistration`
- `MessageBrokerHealthChecksRegistration`

---

## Quick checklist

- Do names describe wiring intent (what gets added) rather than implementation details?
- Is it easy to locate where a given interface is wired?
