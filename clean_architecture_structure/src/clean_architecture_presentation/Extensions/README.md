# Extensions

## Purpose

Presentation-layer extension methods to keep Program/Startup clean and readable.

## Typical contents

- IServiceCollection extensions (AddApi, AddCors, AddAuth, AddSwagger)
- IApplicationBuilder extensions (UseApi, UseCustomCors, UseProblemDetails)

## Out of scope

- Large blocks of business logic
- Cross-layer wiring duplicated from Infra-IoC

## Notes

Extensions keep the hosting entry point small. Delegate wiring to Infra-IoC where possible.
