# Contracts

## Purpose

External service request/response contracts and mapping helpers. These are NOT application boundary DTOs; they represent external schemas.

## Typical contents

- Provider-specific request/response shapes
- Mapping from external contracts to internal models

## Out of scope

- Reusing external schemas directly inside Domain

## Notes

Treat provider schemas as volatile. Always map them to internal stable models.
