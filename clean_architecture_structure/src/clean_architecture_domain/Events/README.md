# Events

## Purpose

Domain events: immutable facts that something meaningful happened in the domain.

## Typical contents

- IDomainEvent interface
- Event records/classes (e.g., OrderPlaced)

## Out of scope

- Broker-specific message contracts
- MessageBroker/SDK dependencies

## Notes

Publishing/handling strategy (outbox, message bus) is implemented outside the Domain.
