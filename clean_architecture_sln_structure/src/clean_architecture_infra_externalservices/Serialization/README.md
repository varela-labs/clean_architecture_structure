# Serialization

## Purpose

Serialization configuration and helpers for external payloads (JSON/XML).

## Typical contents

- Serializer settings (JSON options, XML settings)
- Converters/adapters for provider quirks

## Out of scope

- Transport serialization rules leaking into Application boundary DTOs

## Notes

Prefer mapping provider payloads to internal models early; keep serialization details here.
