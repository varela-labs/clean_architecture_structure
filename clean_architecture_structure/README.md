# Clean Architecture Structure (Template From Scratch)

This repository describes a Clean Architecture template built with **.NET (latest LTS)** and designed for internal services that use:

- HTTP APIs (ASP.NET Core)
- Messaging (Kafka, RabbitMQ, Redpanda, ActiveMQ)
- Modular Infrastructure (EF Core, external services)
- SOLID + small methods + clear naming

> Goal: Keep business policy stable and independent from delivery and infrastructure details.

---

## 1) Project map

```text
clean_architecture_domain                     (Domain / Core Policy)
clean_architecture_application                (Application / Use Cases + Ports)
clean_architecture_infrastructure-data        (Infrastructure / Persistence adapters)
clean_architecture_infrastructure-external    (Infrastructure / External integrations)
clean_architecture_infrastructure-ioc         (Infrastructure / Composition Root)
clean_architecture_presentation               (Presentation / Hosting + Delivery)
```

---

## 2) Allowed dependency direction (source code dependencies)

The template follows the **Dependency Rule**: dependencies point **inward** toward policy.

```text
[Presentation]  --->  [Application]  --->  [Domain]
      |                    ^
      |                    |
      +----> [Infrastructure-IoC] ---+
                 |
                 +--> [Infrastructure-Data] --------> [Domain]
                 |
                 +--> [Infrastructure-External]  (implements ports owned by inner layers)
```

### Allowed references (ProjectReference)

- `clean_architecture_domain` references: **none**
- `clean_architecture_application` references: `Domain` (and optionally inner contracts projects if you split later)
- `clean_architecture_infrastructure-data` references: `Domain` (and `Application` only if it must implement application ports)
- `clean_architecture_infrastructure-external` references: `Application`/`Domain` ports it implements
- `clean_architecture_infrastructure-ioc` references: `Domain`, `Application`, and all Infra projects (it wires everything)
- `clean_architecture_presentation` references: `Application`, `Infra-IoC`

### Forbidden references (examples)

- Domain **must not** reference Application/Infra/Presentation
- Application **must not** reference Presentation or concrete Infra implementations (EF, Message Broker, SDKs)
- Infrastructure projects **must not** be referenced by Domain
- Presentation **must not** call EF DbContext directly (go through Application)

---

## 3) Layer responsibilities

### Domain (core policy)

- Entities, Value Objects, Domain Services, Domain Events
- Repository **interfaces** (ports) live here by decision (Option A)
- No frameworks (no ASP.NET Core, EF Core, Message Broker client, logging frameworks)

### Application (use cases + boundary)

- Use cases (commands/queries) and orchestration of domain objects
- Ports (interfaces) required by use cases (messaging/persistence/time/external services)
- Validation, behaviors/pipeline policies (e.g., request validation)
- Contracts/DTOs for use case input/output (not tied to HTTP)

### Infrastructure (details / plugins)

- Implements ports from Domain/Application:
  - EF Core repositories, DbContext, mappings, migrations
  - HTTP/SOAP/SDK adapters to external systems
- Contains technical policies (timeouts, retries, serialization) but not business policy

### IoC (composition root)

- Wires ports to adapters (DI registrations)
- Binds options/configuration
- Exposes clean `AddInfrastructure(...)` entry points for Presentation

### Presentation (delivery mechanisms)

- ASP.NET Core hosting, controllers, middleware
- Message Broker consumers/processors (as adapters)
- AuthN/AuthZ, health checks, observability (metrics/tracing/logging)
- Translates transport -> application requests; delegates business decisions to Application/Domain

---

## 4) Architectural guardrails (the "Source of Truth")

The repository uses a dedicated ruleset file as the authoritative source:

- `clean_architecture_rules.md`

This file is intended to be:

- Human-readable (clear MUST/SHOULD/MUST NOT language)
- AI-auditable (explicit verification steps and smells)
- Stable over time (versioned in the repository)

---

## 5) How to use AI as an auditor

### 5.1 Recommended workflow

1. Attach `clean_architecture_rules.md` in your AI session.
2. Ask Q to first map project references (csproj graph).
3. Ask Q to audit each project against the ruleset.
4. Require Q to output:
   - Violations (Rule IDs)
   - Evidence (file paths)
   - Fix suggestions limited to the scope of the rule

### 5.2 Prompts (copy/paste)

#### Prompt A — Build dependency graph

```text
You are auditing a .NET solution for Clean Architecture. 
1) Read all *.csproj and the *.sln.
2) Produce a dependency graph of ProjectReferences.
3) List any forbidden directions according to the provided ruleset file.
For every finding, include evidence: csproj path + the exact ProjectReference line(s).
```

#### Prompt B — Audit a single project against the ruleset

```text
Audit ONLY the project: <PROJECT_NAME>.
Use the attached ruleset as the single source of truth.
Output:
- Violations: {RuleId, Severity, Evidence(file paths), Why it violates}
- Suggested fixes: only changes needed to satisfy the rule (no refactors beyond scope)
- If no violation: say "PASS" and list the rules you checked.
```

#### Prompt C — Audit cross-cutting boundary leaks

```text
Search for boundary leaks across layers:
- Framework dependencies inside Domain/Application (EF Core, ASP.NET Core, Message Broker client, logging frameworks)
- Transport types in Application (ActionResult, HttpContext)
- Direct DbContext usage from Presentation
Return findings with file paths and the violating references/usings.
```

---

## 6) References

- Clean Architecture overview (Dependency Rule & circles): <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- .NET Dependency Injection: <https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection>
- EF Core: <https://learn.microsoft.com/en-us/ef/core/>
- IHttpClientFactory: <https://learn.microsoft.com/en-us/dotnet/core/extensions/httpclient-factory>
- Health checks: <https://learn.microsoft.com/en-us/aspnet/core/host-and-deploy/health-checks>
- Apache Kafka overview: <https://docs.confluent.io/kafka-clients/dotnet/current/overview.html>
- Azure Service Bus (.NET) overview: <https://learn.microsoft.com/en-us/dotnet/api/overview/azure/messaging.servicebus-readme?view=azure-dotnet>
- Redpanda (Kafka-compatible) overview: <https://docs.redpanda.com/current/develop/kafka-clients/>
- RabbitMQ .NET overview: <https://www.rabbitmq.com/dotnet.html>
- Apache ActiveMQ (.NET) overview: <https://activemq.apache.org/components/nms/providers/activemq/>
