# Abstractions/Persistence

## Purpose

Application-level persistence ports beyond repository interfaces in Domain (optional).

## Typical contents

- ITransaction, IUnitOfWork-like coordination (only if use cases require it)
- Read model/query services interfaces (if you separate read concerns)

## Out of scope

- DbContext, migrations, provider-specific features

## Notes

If Domain already owns repository interfaces, keep this folder minimal; only add what UseCases truly need.
