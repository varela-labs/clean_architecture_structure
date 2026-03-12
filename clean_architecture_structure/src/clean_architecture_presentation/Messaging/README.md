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

- Apache Kafka overview: <https://docs.confluent.io/kafka-clients/dotnet/current/overview.html>
- Azure Service Bus (.NET) overview: <https://learn.microsoft.com/en-us/dotnet/api/overview/azure/messaging.servicebus-readme?view=azure-dotnet>
- Redpanda (Kafka-compatible) overview: <https://docs.redpanda.com/current/develop/kafka-clients/>
- RabbitMQ .NET overview: <https://www.rabbitmq.com/dotnet.html>
- Apache ActiveMQ (.NET) overview: <https://activemq.apache.org/components/nms/providers/activemq/>
