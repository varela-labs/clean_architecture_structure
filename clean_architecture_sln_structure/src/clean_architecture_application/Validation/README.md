# Validation

## Purpose

Validation policies and validators for application requests.

## Typical contents

- Validators per request (FluentValidation)
- Validation behaviors/pipeline integration
- Validation result models

## Out of scope

- UI validation code (Presentation concern)

## Notes

Validate at the boundary of the use case. Domain enforces invariants; Application validates request shape and prerequisites.

## References

- <https://docs.fluentvalidation.net/>
- <https://mediatr.io/>
