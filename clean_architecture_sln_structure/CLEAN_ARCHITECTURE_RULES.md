# Clean Architecture Rules

> Source: Internal ruleset extracted from *Clean Architecture* (Robert C. Martin) and organized for auditing.

CLEAN ARCHITECTURE - RULES & PATTERNS (fuller, paraphrased)
Paraphrased from topics/patterns covered throughout “Clean Architecture” by Robert C. Martin. Not copied verbatim.
Designed as a stable “source of truth” for humans and AI auditors.
Keywords: MUST / MUST NOT (required), SHOULD (recommended).

GOAL-001  [GOAL]  Easy change is the primary architectural goal
Rule: MUST design to minimize the cost of making the kinds of changes the system will face.
Intent: Architecture is successful when typical changes are simple and low-risk.
Implementation cues:

- Favor clear boundaries and small modules.
- Keep dependencies directional.

Common violations / smells:

- Common changes require coordinated edits across many layers/modules.

How to verify (audit):

- Measure number of modules touched per typical feature.

GOAL-002  [GOAL]  Architecture decisions are about options
Rule: MUST keep as many options open as practical, especially around volatile technology choices.
Intent: Options are preserved by delaying commitment and isolating details.

Implementation cues:

- Treat DB/web/framework as plugins.
- Use interfaces to defer decisions.

Common violations / smells:

- Core policy tied to a specific ORM/web framework.

How to verify (audit):

- Audit core for framework package references.

GOAL-003  [GOAL]  Behavior and structure are both valuable
Rule: MUST protect architectural integrity while delivering behavior.
Intent: Sacrificing structure eventually slows delivery of behavior.

Implementation cues:

- Create architectural guardrails.
- Refactor incrementally with tests.

Common violations / smells:

- “Just ship it” culture that accumulates irreversible coupling.

How to verify (audit):

- Track defect rate and lead time over time.

SRP-001  [SRP]  SRP is about actors, not “one method”
Rule: MUST separate responsibilities when they serve different stakeholders (actors).
Intent: Different actors change code for different reasons; mixing them creates coupling.

Implementation cues:

- Identify actors per module.
- Split by policy vs presentation vs persistence concerns.

Common violations / smells:

- One module changed by many teams/roles.

How to verify (audit):

- Map modules to actors during reviews.

SRP-002  [SRP]  Separate data representation from business policy
Rule: SHOULD keep formatting/reporting concerns out of policy modules.
Intent: Formatting changes should not force policy edits.

Implementation cues:

- Use presenters/view models outside policy.
- Keep entities free of formatting.

Common violations / smells:

- Entities containing string formatting / localization.

How to verify (audit):

- Search for formatting code in Domain/Application.

SRP-003  [SRP]  Treat “accidental duplication” as a code smell
Rule: SHOULD remove duplicated logic that looks similar but is maintained separately.
Intent: It causes divergence when requirements change.

Implementation cues:

- Centralize rules.
- Write tests that define one canonical rule.

Common violations / smells:

- Two “almost same” validators.

How to verify (audit):

- Duplicate detection / semantic search for similar logic.

OCP-001  [OCP]  Protect high-level policy from change
Rule: MUST keep high-level policy closed to modification by pushing variation behind polymorphic interfaces.
Intent: High-level code changes are costly and risky.

Implementation cues:

- Use strategy/handler registration.
- Prefer adding new classes over editing stable ones.

Common violations / smells:

- High-level policy changes every time a new variant is added.

How to verify (audit):

- Churn metrics on policy modules.

OCP-002  [OCP]  Separate direction of control from direction of dependency
Rule: SHOULD invert compile-time dependencies so control can flow from policy to details.
Intent: Allows policy to call details without depending on them.
Implementation cues:

- Ports owned by policy.
- Adapters implement ports.
Common violations / smells:
- Policy imports adapter implementations.
How to verify (audit):
- Project graph must show inward dependencies only.

OCP-003  [OCP]  Information hiding enables OCP
Rule: SHOULD hide volatile details behind stable interfaces and modules.
Intent: Hiding details reduces ripple effects.
Implementation cues:

- Keep DB schema, HTTP routes, broker config out of policy.
Common violations / smells:
- Policy contains SQL fragments or endpoint URLs.
How to verify (audit):
- Search for config keys/URLs in policy projects.

LSP-001  [LSP]  Prefer interfaces to deep inheritance
Rule: SHOULD prefer interfaces/composition over inheritance when behavior varies.
Intent: Inheritance often violates substitutability when invariants differ.
Implementation cues:

- Use composition.
- Split interfaces.
Common violations / smells:
- Subtype throws for base behavior.
How to verify (audit):
- Look for NotSupportedException / type checks.

LSP-002  [LSP]  LSP at boundaries: adapters must obey port contracts
Rule: MUST ensure adapters implement ports in a way that preserves expected semantics.
Intent: Otherwise swapping adapters breaks policy.
Implementation cues:

- Write contract tests for each adapter.
- Keep port contracts narrow.
Common violations / smells:
- Port includes methods only one adapter can support.
How to verify (audit):
- Run shared test suite for adapter implementations.

LSP-003  [LSP]  Avoid “strengthening preconditions”
Rule: MUST NOT require stricter inputs in a subtype than the base contract allows.
Intent: Clients relying on base contract will fail unexpectedly.
Implementation cues:

- Validate inputs at boundary, not per subtype quirks.
Common violations / smells:
- Special-case checks in clients.
How to verify (audit):
- Review validation differences across implementations.

ISP-001  [ISP]  Keep interfaces segregated by use case
Rule: MUST design ports around specific use case needs.
Intent: Reduces coupling and allows independent evolution.
Implementation cues:

- Read vs write ports.
- Admin vs user ports.
Common violations / smells:
- One giant interface used everywhere.
How to verify (audit):
- Interface method count and consumer diversity.

ISP-002  [ISP]  Avoid “fat” dependency surfaces across components
Rule: SHOULD prevent components from depending on large APIs when they need only a small subset.
Intent: Transitive coupling increases rebuild and redeploy scope.
Implementation cues:

- Split packages.
- Expose minimal APIs.
Common violations / smells:
- Common library referenced for one helper.
How to verify (audit):
- Dependency usage analysis.

DIP-001  [DIP]  Abstractions should be stable
Rule: SHOULD keep abstractions stable and free of volatile details.
Intent: Stable abstractions reduce ripple effects.
Implementation cues:

- Avoid framework types in interfaces.
- Use plain types/DTOs.
Common violations / smells:
- Interface methods expose EF types or HttpResponseMessage.
How to verify (audit):
- Scan port interfaces for framework types.

DIP-002  [DIP]  Factories prevent dependency leakage
Rule: SHOULD use factories to create details without pulling their constructors into policy code.
Intent: Keeps policy independent of concrete types.
Implementation cues:

- Factory interface in policy; factory implementation at edge.
Common violations / smells:
- Policy calls new Concrete().
How to verify (audit):
- Search for “new” of infra types in Application/Domain.

DIP-003  [DIP]  Concrete components are details
Rule: MUST keep concrete implementations in volatile components and wire them at the edge.
Intent: Supports plugin architecture.
Implementation cues:

- Implement ports in Infrastructure.
- Register in composition root.
Common violations / smells:
- Concrete infra class referenced directly by policy code.
How to verify (audit):
- Project reference audit + DI registrations.

COMP-001  [COMP]  A component is a unit of deployment
Rule: SHOULD structure components so they can be built and deployed independently where it adds value.
Intent: Independence improves team velocity and reduces risk.
Implementation cues:

- Clear public API.
- No cycles.
Common violations / smells:
- Tangled dependencies requiring synchronized releases.
How to verify (audit):
- Dependency graph & release notes analysis.

COMP-002  [COMP]  Relocatability is a component goal
Rule: SHOULD be able to relocate/replace components with minimal impact.
Intent: Supports evolving architecture and tooling.
Implementation cues:

- Use interfaces.
- Hide implementation details.
Common violations / smells:
- Hard-coded assumptions about component internals.
How to verify (audit):
- Replace an implementation with a stub in tests easily.

COMP-003  [COMP]  REP: reuse equals release
Rule: SHOULD manage reusable components with versioning and clear releases.
Intent: Consumers need stability guarantees.
Implementation cues:

- Semantic versioning.
- Changelog.
Common violations / smells:
- Breaking changes without version bump.
How to verify (audit):
- Check versioning discipline for shared libs.

COMP-004  [COMP]  CCP: co-change
Rule: SHOULD package classes that change together into the same component.
Intent: Minimizes component churn per change.
Implementation cues:

- Package by feature/use case.
- Co-locate cohesive policy.
Common violations / smells:
- Feature change spans many components.
How to verify (audit):
- Trace change sets across components.

COMP-005  [COMP]  CRP: reuse together
Rule: SHOULD avoid depending on a component for a small subset of its contents.
Intent: Reduces transitive coupling.
Implementation cues:

- Split large libraries.
- Avoid “Utils” monolith.
Common violations / smells:
- Huge shared libraries referenced everywhere.
How to verify (audit):
- Find components with large API surface and low per-consumer usage.

COUP-001  [COUP]  ADP: dependency graph must be acyclic
Rule: MUST prevent cycles between components/projects.
Intent: Cycles destroy independent work and complicate builds.
Implementation cues:

- CI check for cycles.
- Break cycles with interfaces.
Common violations / smells:
- Circular project references.
How to verify (audit):
- Automated graph detection from csproj.

COUP-002  [COUP]  Top-down design emerges from stable boundaries
Rule: SHOULD allow dependency structure to evolve from policy needs, not from bottom-up details.
Intent: Policies define what details must provide.
Implementation cues:

- Define ports from use cases.
- Implement in adapters.
Common violations / smells:
- Starting from DB schema and generating policy around it.
How to verify (audit):
- Check if DB migrations drive domain changes.

COUP-003  [COUP]  SDP: depend on stable
Rule: SHOULD direct dependencies toward more stable components.
Intent: Protects stable core from volatility.
Implementation cues:

- Move interfaces inward.
- Keep volatile adapters outward.
Common violations / smells:
- Stable core depends on volatile UI/DB libs.
How to verify (audit):
- Stability metrics: fan-in/fan-out + churn.

COUP-004  [COUP]  SAP: stable is abstract
Rule: SHOULD keep stable components more abstract to enable extension.
Intent: Avoid rigidity in highly depended-upon code.
Implementation cues:

- Prefer interfaces in stable core.
- Keep implementations outside.
Common violations / smells:
- Stable core is concrete and frequently edited.
How to verify (audit):
- Abstractness ratio for stable components.

CA-001  [CA]  Dependency Rule is non-negotiable
Rule: MUST ensure all source dependencies point inward to policy.
Intent: This is the defining rule of Clean Architecture.
Implementation cues:

- Outer depends on inner only.
- Ports in inner, adapters in outer.
Common violations / smells:
- Inner depends on outer.
How to verify (audit):
- Enforce project reference matrix.

CA-002  [CA]  Entities contain enterprise rules
Rule: MUST keep entities independent of application and infrastructure concerns.
Intent: Entities are the most reusable and most valuable policy.
Implementation cues:

- No DB/web/broker types.
- Methods enforce invariants.
Common violations / smells:
- Entities decorated with ORM or serialization attributes.
How to verify (audit):
- Scan Domain for framework namespaces.

CA-003  [CA]  Use cases orchestrate application rules
Rule: MUST place orchestration and application-specific flow in use case interactors/handlers.
Intent: Keeps UI/DB independent and testable.
Implementation cues:

- Input models.
- Output models.
- Call entities and gateways.
Common violations / smells:
- Controllers or repositories contain business orchestration.
How to verify (audit):
- Search for business branching in controllers.

CA-004  [CA]  Interface Adapters translate formats
Rule: MUST translate between external data formats and internal models at adapter boundaries.
Intent: Prevents leakage of UI/DB formats into policy.
Implementation cues:

- Controllers map HTTP -> input model.
- Presenters map output model -> response.
Common violations / smells:
- Use cases accept HttpRequest or return IActionResult.
How to verify (audit):
- Search for ASP.NET types in Application.

CA-005  [CA]  Frameworks/Drivers are outermost
Rule: MUST keep frameworks and drivers (DB, web, messaging) in the outer ring.
Intent: Makes them replaceable.
Implementation cues:

- EF in Infrastructure.Data.
- RabbitMQ client in Messaging/Presentation adapter.
Common violations / smells:
- Framework base classes in Domain.
How to verify (audit):
- Package reference audit per project.

BND-001  [BND]  Draw boundaries to control change
Rule: MUST draw boundaries where volatility and change rates differ.
Intent: Boundaries prevent high-volatility code from infecting stable policy.
Implementation cues:

- Separate projects for policy vs details.
- Define ports.
Common violations / smells:
- Stable modules importing volatile libraries.
How to verify (audit):
- Churn and dependency analysis by module.

BND-002  [BND]  Input and output are details
Rule: MUST treat both input and output mechanisms as replaceable details.
Intent: UI and delivery can change without changing use cases.
Implementation cues:

- Input via controllers/consumers.
- Output via presenters/publishers.
Common violations / smells:
- Use cases reading from HttpContext or message broker directly.
How to verify (audit):
- Search for transport types in use case code.

BND-003  [BND]  Plugin architecture mindset
Rule: SHOULD design details as plugins to policy through interfaces.
Intent: Keeps core independent and extensible.
Implementation cues:

- Ports in policy.
- Adapters register via DI.
Common violations / smells:
- Policy references plugin implementations.
How to verify (audit):
- Check DI wiring occurs only at composition root.

BND-004  [BND]  Boundary crossing uses DTOs
Rule: SHOULD use simple data structures across boundaries.
Intent: Reduces coupling and avoids leaking frameworks.
Implementation cues:

- Immutable DTOs.
- Map at edges.
Common violations / smells:
- Passing EF entities across boundaries.
How to verify (audit):
- Search for entity types used in controllers responses.

BND-005  [BND]  Avoid “dreaded monolith” by internal boundaries
Rule: SHOULD keep strong internal boundaries even within a monolith.
Intent: Monolith can be clean if boundaries are enforced.
Implementation cues:

- Separate projects/modules.
- Inward dependencies.
- Feature packages.
Common violations / smells:
- Single project containing everything with free-for-all references.
How to verify (audit):
- Project count and reference rules.

BND-006  [BND]  Deployment components are not necessarily services
Rule: SHOULD choose appropriate boundary strength: classes -> components -> processes -> services.
Intent: Bigger boundaries cost more; use only when needed.
Implementation cues:

- Start with code-level boundaries.
- Escalate to process/service boundaries when justified.
Common violations / smells:
- Premature microservices.
How to verify (audit):
- ADR for boundary mode choices.

BND-007  [BND]  Threads/processes/services are boundary variants
Rule: SHOULD treat concurrency boundaries as architectural boundaries with clear contracts.
Intent: Keeps runtime concerns isolated.
Implementation cues:

- Define messaging or async ports.
- Keep thread management at edges.
Common violations / smells:
- Use cases managing threads directly.
How to verify (audit):
- Search for Thread/Task scheduling policy in Application.

HUM-001  [HUM]  Humble Object: push logic out of hard-to-test code
Rule: SHOULD move calculations/decisions out of UI/DB frameworks into testable policy modules.
Intent: Improves unit test coverage and reduces coupling to frameworks.
Implementation cues:

- Thin controllers and EF repositories.
- Logic in use cases/entities.
Common violations / smells:
- Complex branching inside controllers or EF queries.
How to verify (audit):
- Controller complexity metrics; test distribution.

HUM-002  [HUM]  Database gateways are adapters
Rule: MUST keep database access behind gateway/repository interfaces.
Intent: Use cases must not know about the DB/ORM.
Implementation cues:

- IGateway in policy.
- EF implementation in Infrastructure.
Common violations / smells:
- Use case depends on DbContext.
How to verify (audit):
- Scan Application for DbContext references.

HUM-003  [HUM]  Service listeners are controllers
Rule: MUST treat service listeners (message consumers, event handlers) like controllers.
Intent: They translate external events into use case input.
Implementation cues:

- Consumer maps message -> input model -> use case call.
Common violations / smells:
- Consumer contains business rules and persistence logic.
How to verify (audit):
- Search consumers for domain decisions.

HUM-004  [HUM]  Data mappers isolate persistence
Rule: SHOULD keep mapping between DB and domain outside domain entities.
Intent: Avoids persistence concerns shaping entities.
Implementation cues:

- EF configuration classes in infrastructure.
- Separate data models if needed.
Common violations / smells:
- Domain entities with ORM attributes everywhere.
How to verify (audit):
- Scan Domain for EF attributes.

MAIN-001  [MAIN]  Main is the ultimate detail
Rule: MUST keep composition/wiring in the outermost module.
Intent: Everything may depend on Main; Main should not be depended on by policy.
Implementation cues:

- DI registration here.
- Config here.
- No business rules.
Common violations / smells:
- Business logic in Program.cs.
How to verify (audit):
- Search for use case logic patterns in Startup/Program.

MAIN-002  [MAIN]  No service locator in core
Rule: MUST NOT resolve services from the container inside Domain/Application policy code.
Intent: Service locator couples policy to DI framework.
Implementation cues:

- Constructor injection in policy.
- Resolve only at edges.
Common violations / smells:
- IServiceProvider used inside use cases.
How to verify (audit):
- Search for IServiceProvider in Application/Domain.

SVC-001  [SVC]  Service boundaries must align with business capabilities
Rule: SHOULD define services around cohesive business capabilities, not technical layers.
Intent: Misaligned boundaries cause distributed coupling.
Implementation cues:

- Capability-based services.
- Clear data ownership.
Common violations / smells:
- Services split by UI vs DB vs business layers.
How to verify (audit):
- Review service boundaries vs use cases.

SVC-002  [SVC]  Service benefits are not automatic
Rule: SHOULD validate that service split improves deployability or team autonomy before doing it.
Intent: Services add latency and operational overhead.
Implementation cues:

- Prefer internal boundaries first.
- Split only when justified.
Common violations / smells:
- Network calls used to simulate modularity.
How to verify (audit):
- Measure operational complexity before/after split.

SVC-003  [SVC]  Cross-cutting concerns via mechanisms
Rule: SHOULD implement cross-cutting concerns via middleware/pipelines/decorators.
Intent: Avoids repetition and policy contamination.
Implementation cues:

- MediatR pipeline behaviors.
- ASP.NET middleware.
- Decorator pattern.
Common violations / smells:
- Logging/retry code duplicated in every handler.
How to verify (audit):
- Search for repeated cross-cutting code in use cases.

TEST-001  [TEST]  Tests must not break boundaries
Rule: SHOULD keep tests from reaching across layers in ways production code should not.
Intent: Test shortcuts can force production architecture compromises.
Implementation cues:

- Test via ports/use case APIs.
- Avoid coupling to internals.
Common violations / smells:
- Tests directly instantiate internal infra classes from core tests.
How to verify (audit):
- Test project reference rules.

TEST-002  [TEST]  Testing API
Rule: SHOULD design a stable testing API around use cases and ports.
Intent: Keeps tests resilient to refactoring.
Implementation cues:

- Helper builders around input models.
- Contract tests for ports.
Common violations / smells:
- Tests rely on internal class names and file structures.
How to verify (audit):
- Assess test fragility on refactor PRs.

TEST-003  [TEST]  Design for testability
Rule: MUST be able to unit test use cases without web host, DB, or broker.
Intent: Proves policy independence.
Implementation cues:

- Use fakes for gateways.
- No framework types in policy.
Common violations / smells:
- Need integration environment for simple rule tests.
How to verify (audit):
- Run unit test suite with network disabled.

EMB-001  [EMB]  Hardware independence
Rule: MUST keep hardware-specific code behind adapters.
Intent: Hardware changes should not force policy changes.
Implementation cues:

- HAL ports.
- Drivers in outer layer.
Common violations / smells:
- Domain uses GPIO/driver APIs.
How to verify (audit):
- Scan for driver libs in policy projects.

DETAIL-001  [DETAIL]  DB schema does not define domain
Rule: MUST NOT design domain entities as table-shaped records by default.
Intent: Domain should reflect business concepts, not storage.
Implementation cues:

- Model behavior and invariants.
- Map to tables in infra.
Common violations / smells:
- Every domain class is a 1:1 table mirror with no behavior.
How to verify (audit):
- Compare entity naming vs table naming.

DETAIL-002  [DETAIL]  ORM is replaceable
Rule: SHOULD isolate ORM usage to infrastructure modules.
Intent: Allows swapping or upgrading ORM without touching policy.
Implementation cues:

- EF only in infra.
- Ports hide query style.
Common violations / smells:
- IQueryable leaks into use case contracts.
How to verify (audit):
- Scan for IQueryable/DbSet in Application/Domain.

DETAIL-003  [DETAIL]  Web controllers are adapters
Rule: MUST keep HTTP-specific concerns in controllers and middleware.
Intent: Policy stays independent.
Implementation cues:

- Model binding and authorization at edges.
- Use case input models.
Common violations / smells:
- Use case depends on HttpRequest.
How to verify (audit):
- Scan Application for ASP.NET types.

DETAIL-004  [DETAIL]  Framework lock-in is a risk
Rule: SHOULD minimize framework surface area in your codebase.
Intent: Reduces upgrade cost and coupling.
Implementation cues:

- Wrap framework behind adapters.
- Avoid inheriting framework base classes in core.
Common violations / smells:
- Framework types appear in Domain entities.
How to verify (audit):
- Count framework references by layer.

ORG-001  [ORG]  Organization vs encapsulation
Rule: MUST enforce encapsulation with dependencies, not just folder layout.
Intent: Folders do not prevent coupling; dependency rules do.
Implementation cues:

- Project-level boundaries.
- Internal visibility.
- CI enforcement.
Common violations / smells:
- Pretty folders but unrestricted references.
How to verify (audit):
- Check enforcement mechanisms exist.

ORG-002  [ORG]  The devil is in implementation details
Rule: SHOULD make boundaries real with build-time rules and review checks.
Intent: Otherwise boundaries erode over time.
Implementation cues:

- Dependency tests.
- Static analysis for forbidden namespaces.
Common violations / smells:
- “We follow clean architecture” but core imports infra namespaces.
How to verify (audit):
- Automated checks + periodic audits.

ORG-003  [ORG]  Other decoupling modes
Rule: SHOULD be aware of alternative decoupling strategies and choose intentionally.
Intent: Different contexts need different tradeoffs.
Implementation cues:

- Layer, feature, ports/adapters, component packaging.
- Partial boundaries when needed.
Common violations / smells:
- One-size-fits-all packaging dogma.
How to verify (audit):
- ADR records for packaging choices.

MSG-001  [MSG]  Broker libraries stay out of policy
Rule: MUST NOT reference broker client libraries in Domain/Application.
Intent: Messaging is a delivery detail.
Implementation cues:

- Broker libs only in outer adapter projects.
- Use ports for publishing.
Common violations / smells:
- RabbitMQ.Client referenced by Application.
How to verify (audit):
- Package reference audit.

MSG-002  [MSG]  Consumers translate and delegate
Rule: MUST keep consumers focused on translation, acknowledgement, and calling use cases.
Intent: Business policy stays in use cases.
Implementation cues:

- Deserialize -> validate -> call use case.
- Retries/DLQ at adapter.
Common violations / smells:
- Consumer performs domain calculations and DB writes.
How to verify (audit):
- Scan consumers for repository usage and domain branching.

MSG-003  [MSG]  Publishers are gateways
Rule: SHOULD expose publishing via a policy-owned port and implement in infrastructure.
Intent: Allows switching brokers/transport.

Implementation cues:

- IEventPublisher in Application.
- RabbitPublisher adapter.
Common violations / smells:
- Use case creates ConnectionFactory directly.
How to verify (audit):
- Search for broker setup code outside composition root.
