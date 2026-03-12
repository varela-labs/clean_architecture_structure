# Controllers

## Purpose
HTTP endpoints (ASP.NET Core controllers). Controllers translate HTTP requests into Application use case requests and return responses.

## Typical contents
- Thin controller actions
- Model binding and request validation at the edge (basic shape checks)
- Calling IMediator / use case dispatcher

## Out of scope
- Business logic and domain rules
- Direct DbContext/repository usage (prefer going through Application use cases)

## Notes
A good controller is boring: map -> call use case -> map response.

## References
- https://learn.microsoft.com/en-us/aspnet/core/web-api/


