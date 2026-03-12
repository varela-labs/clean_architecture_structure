# Clients/Http

## Purpose

HTTP-based integrations using IHttpClientFactory and typed clients.

## Typical contents

- Typed HttpClient wrappers
- Request/response mapping at the boundary
- HTTP status handling and error translation

## Out of scope

- Direct HttpClient instantiation scattered across the codebase

## Notes

Use typed clients and centralize policies (timeouts/retries) in one place.

## References

- https://learn.microsoft.com/en-us/dotnet/core/extensions/httpclient-factory
