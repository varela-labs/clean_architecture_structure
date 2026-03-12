# HostedServices

## Purpose
Background services hosted by ASP.NET Core for delivery concerns (message pumps, schedulers, etc.).

## Typical contents
- Message processing hosted services
- Timers/schedulers for delivery concerns

## Out of scope
- Core domain policy
- Database schema/migrations

## Notes
Hosted services should delegate to Application use cases for business actions.

## References
- https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services


