# Bootstrapping

## Purpose

Top-level service registration entry points. This is where the hosting layer calls into IoC to wire the solution.

## Typical contents

- InjectorBootstrapper / DependencyInjectionConfiguration equivalents
- One public method to register all dependencies (e.g., AddInfrastructure)

## Out of scope

- Business logic
- Environment-specific hosting setup (Kestrel, routing) — keep that in Presentation

## Notes

Keep bootstrapping methods thin: delegate to Modules to keep code SOLID and easy to maintain.
