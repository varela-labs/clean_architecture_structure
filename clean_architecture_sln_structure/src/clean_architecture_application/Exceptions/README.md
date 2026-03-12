# Exceptions

## Purpose

Application-level exceptions for invalid requests or use case failures that are NOT pure domain invariant violations.

## Typical contents

- NotFoundException (use-case level)
- BadRequestException / ValidationException (application boundary validation)
- Forbidden/Unauthorized abstractions (if needed)

## Out of scope

- Transport exceptions (HTTP status codes directly)
- Infrastructure exceptions (database/network)

## Notes

Presentation maps these exceptions to HTTP responses; Messaging adapters map them to message outcomes.
