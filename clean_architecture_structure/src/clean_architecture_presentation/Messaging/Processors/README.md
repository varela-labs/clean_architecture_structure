# Messaging/Processors

## Purpose

Message processors translate incoming messages into Application requests and dispatch use cases (e.g., via MediatR).

## Typical contents

- One processor per message type/use case
- Mapping message -> request DTO
- Dispatching IMediator or use case interactor

## Out of scope

- Complex business logic (belongs in Application/Domain)
- Broker-specific code (keep in Consumers)

## Notes

Aim for small processor methods: validate envelope -> map -> dispatch -> map outcome.
