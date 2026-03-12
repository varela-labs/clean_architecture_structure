# Extensions

## Purpose

Infrastructure extension methods to wire client concerns (headers, query parameters, request building).

## Typical contents

- HttpRequestMessage builders
- Header helpers and request signing helpers

## Out of scope

- Business logic hidden as 'helpers'

## Notes

Keep extensions obvious; do not hide policy decisions in helpers.
