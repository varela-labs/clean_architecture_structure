# UseCases

## Purpose

The heart of the Application layer: orchestrates Domain objects to fulfill user goals.

## Typical contents

- Feature folders with commands/queries and handlers
- Input/Output models and mapping calls
- Calls to Domain repositories via interfaces
- Raising domain events (as data) to be published by outer layers

## Out of scope

- HTTP concerns (routing, ActionResult, headers)
- Database provider specifics (EF, SQL)

## Notes

Organize by business capability ('screaming architecture'). Use MediatR or explicit interactors to dispatch use cases.

## References

- <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
- <https://mediatr.io/>
