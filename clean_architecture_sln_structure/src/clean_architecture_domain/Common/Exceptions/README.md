# Common/Exceptions

## Purpose

Domain-level exceptions that express business rule violations in a precise, testable way.

## Typical contents

- DomainException
- BusinessRuleViolationException
- InvariantViolationException

## Out of scope

- HTTP-specific exceptions
- Infrastructure exceptions (SqlException, HttpRequestException)

## Notes

Outer layers may translate these exceptions into transport responses (HTTP, messages).
