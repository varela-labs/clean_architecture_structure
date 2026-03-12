# Abstractions/Messaging

## Purpose

Messaging ports used by use cases to publish/emit notifications without coupling to a broker.

## Typical contents

- IEventPublisher / IMessageBus interfaces
- Message contracts (if they are application-level) or references to Domain events
- Outbox abstractions (if your architecture uses outbox)

## Out of scope

- MessageBroker.Client usage
- Exchange/queue/routing configuration (Infrastructure/Presentation concern)
