# Authentication

## Purpose

Technical authentication helpers for calling external services (tokens, signatures).

## Typical contents

- Token acquisition helpers
- Request signing / HMAC helpers
- Auth header builders

## Out of scope

- User authentication for your API (Presentation concern)

## Notes

Keep secrets out of code; integrate with secret stores via configuration and outer-layer wiring.
