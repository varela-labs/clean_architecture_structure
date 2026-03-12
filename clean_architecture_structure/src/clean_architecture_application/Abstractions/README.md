# Abstractions

## Purpose

Ports owned by the Application layer. Outer layers implement these interfaces (adapters).

## Typical contents

- Persistence ports (e.g., transactional boundaries beyond repositories if needed)
- Messaging ports (publish/subscribe abstractions)
- Time/ID/environment ports

## Out of scope

- Concrete implementations (EF, Message Broker, HTTP clients)
- Dependency Injection registration

## Notes

Prefer small, client-specific interfaces. Interfaces belong where they are used (Dependency Inversion).

## References

- <https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html>
