# Middleware

## Purpose

ASP.NET Core middleware for transport concerns: exception mapping, request logging, correlation, etc.

## Typical contents

- Exception handling middleware (map exceptions to ProblemDetails/HTTP codes)
- Correlation ID middleware
- Request/response logging middleware (careful with PII)

## Out of scope

- Business policy decisions
- Database or message broker client code

## Notes

Middleware should not know about Domain. It translates transport-level concerns only.

## References

- <https://learn.microsoft.com/en-us/aspnet/core/fundamentals/middleware/>
