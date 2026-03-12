# Messaging

## Purpose
Messaging delivery mechanisms (broker consumers and message-to-use-case translation).

## Typical contents
- Consumers (subscribe/pull messages)
- Processors (translate message payload -> Application request -> dispatch)
- Message envelope parsing and validation

## Out of scope
- Broker configuration scattered across the codebase
- Business logic in processors

## Notes
Treat message consumers like controllers: translate and delegate.

## References
- https://www.rabbitmq.com/dotnet.html


