# Extensions

## Purpose
Extension methods used by the hosting layer to register dependencies cleanly.

## Typical contents
- IServiceCollection extensions (AddXyz)
- IConfiguration binding helpers (thin)

## Out of scope
- Large imperative registration blocks (prefer Modules)
- Service locator patterns

## References
- https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection


