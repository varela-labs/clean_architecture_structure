# Clients/Soap

## Purpose

SOAP-based integrations (if applicable). Keep SOAP tooling confined to this folder.

## Typical contents

- SOAP client wrappers
- WSDL generated types (if you accept them here)
- Boundary mapping to/from application/domain contracts

## Out of scope

- SOAP types leaking into Application/Domain

## Notes

If tooling generates code, isolate it and map to internal contracts to avoid leakage.
