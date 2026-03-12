# Messaging/Consumers

## Purpose
Broker consumers (RabbitMQ) responsible for receiving messages and passing them to processors.

## Typical contents
- RabbitMQ consumer wrappers
- DLQ handling hooks (technical)
- Deserialization to an envelope model

## Out of scope
- Calling repositories directly
- Implementing use cases here

## Notes
Keep consumers transport-focused. They should not know about Domain details beyond message contracts.


