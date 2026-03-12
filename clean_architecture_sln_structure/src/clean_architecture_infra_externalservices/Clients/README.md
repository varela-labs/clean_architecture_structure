# Clients

## Purpose

Concrete client implementations used to talk to external systems. Keep each client focused on one external dependency.

## Typical contents

- Typed clients per provider/system
- Shared client base helpers (thin, optional)

## Out of scope

- Use case workflows
- Domain rules

## Notes

Prefer one folder per external system/provider when the project grows.
