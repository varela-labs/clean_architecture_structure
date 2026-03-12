# Modules

## Purpose

Registration modules per infrastructure capability (Data, Caching, ExternalServices, Messaging).

## Typical contents

- DataModule (register DbContextFactory, repositories, unit of work)
- CachingModule (register cache providers)
- ExternalServicesModule (register typed clients)
- MessagingModule (register publishers/consumers adapters when applicable)

## Out of scope

- Implementations themselves (repositories/providers/clients) — those are in their respective projects

## Notes

Module boundaries help keep registrations cohesive and prevent one giant bootstrapping file.
